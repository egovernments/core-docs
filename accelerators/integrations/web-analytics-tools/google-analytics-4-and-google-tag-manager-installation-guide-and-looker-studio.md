# Google Analytics 4 & Google Tag Manager Installation Guide & Looker Studio

**Prerequisites**

Before starting, ensure:

* ✔ You have a Google account with access to **Google Analytics** and **Google Tag Manager**
* ✔ You have **admin access** to your web application’s codebase
* ✔ (Optional, for dashboards) Access to **Looker Studio**

***

## PART 1 — Understanding the Basics

Before starting, understand these 3 things clearly:

### **1)** Google Analytics (GA4)

This is where:

* You see reports
* You see page views
* You see button clicks
* You create dashboards

### **2)** Google Tag Manager (GTM)

This is where:

* You configure tracking logic
* You create Tags
* You create Triggers
* You send data to GA4

This is where:

* You see reports
* You see page views
* You see button clicks
* You create dashboards

GTM collects and sends data. GA4 stores and shows reports.

```
Your Website → GTM → GA4 → Reports
```

***

## **Part 2: Create Google Analytics (GA4) From Scratch**

### **Step 1: Create GA4 Property**&#x20;

1. Visit [https://analytics.google.com/](https://analytics.google.com/)
2. Click Admin Icon (⚙ bottom left)
3. Click Create Property
4. Enter : &#x20;

* Property Name → Example: Digit UAT
* Time Zone → India
* Currency → INR

5. Click Next -> Create

<figure><img src="../../../.gitbook/assets/Screenshot from 2026-02-23 14-30-36.png" alt=""><figcaption></figcaption></figure>

***

### **Step 2: Create Web Data Stream**

After property creation:

1. Click Data Streams
2. Click Web
3. Enter:

* Website URL → https://your-website-url.com
* Stream name → Digit UAT Web

4. Click Create Stream

<figure><img src="../../../.gitbook/assets/unknown (2).png" alt=""><figcaption></figcaption></figure>

***

### Get Measurement ID

After creating stream:

You will see:

| Measurement ID: G-XXXXXXXXXX |
| ---------------------------- |

This is VERY important.

Example:

| G-ES6F04ZG5Q |
| ------------ |

<figure><img src="../../../.gitbook/assets/unknown (4).png" alt=""><figcaption></figcaption></figure>

You will use this in GTM.

***

## PART 3 — Create Google Tag Manager (GTM)

Go to:\
[https://tagmanager.google.com/](https://tagmanager.google.com/)

### Step 1: Create Account

1. Click Create Account
2. Enter:

* Account Name → Digit
* Country → India
* Container Name → Your website URL
* Target Platform → Web

3. Click Create

<figure><img src="../../../.gitbook/assets/unknown (5).png" alt=""><figcaption></figcaption></figure>

***

### What is a Container?

Container = One tracking setup for one environment.

You can create:

* Digit QA Container
* Digit UAT Container
* Digit PROD Container

Best Practice:

* Separate container per environment<br>

<figure><img src="../../../.gitbook/assets/unknown (6).png" alt=""><figcaption></figcaption></figure>

***

### Step 2: Install GTM + GA4 on Website

Instead of directly pasting only the default GA4 gtag.js snippet into index.html, we implemented a unified, duplicate-safe setup using a centralized analytics JavaScript file hosted in S3.

This ensures:

* No duplicate page\_view events
* Centralized analytics control
* Environment-specific configuration (QA / UAT / PROD)
* No need to modify application code for every environment
* Clean GTM + GA4 integration

***

#### Step 2.1 — Initial GA4 Installation Snippet (From Analytics)

```json5
<!-- Google tag (gtag.js) -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-SWNFWJXDJM"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-SWNFWJXDJM');
</script>
```

From:

`GA4 → Admin → Data Streams → Web → Install Manually`

Google provides this default snippet:<br>

<figure><img src="../../../.gitbook/assets/unknown (7).png" alt=""><figcaption></figcaption></figure>

However, this approach alone can cause duplication when GTM is also used.

So instead of directly using this snippet in index.html, we created a unified analytics loader.

***

#### Step 2.2 — Unified GTM + GA4 Script (Duplicate-Safe)

We created a centralized script that:

* Initializes dataLayer safely
* Bootstraps GTM
* Pushes GA4 configuration into dataLayer
* Prevents duplicate page\_view events
* Loads GA4 in compatibility mode
* Adds \<noscript> fallback

***

#### Main Setup Script

```json5
// -------------------------------------------
// Google Tag Manager + GA4 (Unified + Duplicate-Safe)
// -------------------------------------------
(function setupAnalytics() {
  console.info("GTM + GA4 unified setup (duplicate-safe)");

  // Create dataLayer if not exists
  window.dataLayer = window.dataLayer || [];

  // GTM bootstrap event
  window.dataLayer.push({
    "gtm.start": new Date().getTime(),
    event: "gtm.js"
  });

  // Inject GTM script
  var gtmScript = document.createElement("script");
  gtmScript.async = true;
  gtmScript.src = "https://www.googletagmanager.com/gtm.js?id=GTM-MJ2JCF3D";
  document.head.appendChild(gtmScript);

  // GA4 config pushed into dataLayer (GTM will handle it)
  window.dataLayer.push({
    event: "ga4.config",
    ga_measurement_id: "G-SWNFWJXDJM",
    send_page_view: true
  });

  // Insert <noscript> fallback
  document.addEventListener("DOMContentLoaded", function () {
    var noscript = document.createElement("noscript");
    noscript.innerHTML =
      '<iframe src="https://www.googletagmanager.com/ns.html?id=GTM-MJ2JCF3D" ' +
      'height="0" width="0" style="display:none;visibility:hidden"></iframe>';
    document.body.insertBefore(noscript, document.body.firstChild);
  });

})();
```

***

#### GA4 Compatibility Loader (No Duplicate Page View)

```json5
// -------------------------------------------
// GA4 gtag.js Loader (For compatibility only, no duplicate page_view)
// -------------------------------------------
(function loadGA4() {
  // Load GA4 script
  var gaScript = document.createElement("script");
  gaScript.async = true;
  gaScript.src = "https://www.googletagmanager.com/gtag/js?id=G-SWNFWJXDJM";
  document.head.appendChild(gaScript);

  // Setup gtag API
  window.dataLayer = window.dataLayer || [];
  window.gtag = function () {
    window.dataLayer.push(arguments);
  };

  // Initialize session
  gtag("js", new Date());

  // Disable GA4 auto page_view (GTM already handles pageviews)
  gtag("config", "G-SWNFWJXDJM", {
    send_page_view: false
  });
})();
```

***

#### Step 2.3 — Host Script in S3 (Centralized Control)

Instead of embedding this code in the app directly, we hosted it in an S3 bucket:

[https://hcm-demo-assets.s3.ap-south-1.amazonaws.com/analytics/consoleAnalyticsDemo.js](https://hcm-demo-assets.s3.ap-south-1.amazonaws.com/analytics/consoleAnalyticsDemo.js)

This allows:

* Centralized updates
* No app redeploy needed for analytics changes
* Better environment control

***

#### Step 2.4 — Add Script via Environment Configuration

Instead of editing index.html, the analytics file is injected using environment configuration.

Example reference in Helm environment YAML:

[https://github.com/egovernments/health-campaign-devops/blob/hcm-demo-new/config-as-code/helm/environments/hcm-demo-new.yaml#L150](https://github.com/egovernments/health-campaign-devops/blob/hcm-demo-new/config-as-code/helm/environments/hcm-demo-new.yaml#L150)

This ensures:

* Each environment (QA / UAT / PROD) loads its own:
* GTM Container ID
* GA4 Measurement ID
* No mixing of analytics data
* Clean DevOps-driven setup

***

## Final Architecture

```
Application
  ↓
Loads analytics JS from S3
  ↓
GTM injected dynamically
  ↓
GA4 config pushed into dataLayer
  ↓
GTM handles all tracking
  ↓
Events sent to correct GA4 property
```

***

## Why This Approach Is Better Than Default Snippet

|                      **Default gtag Snippet** |                  **Unified S3-Based Setup** |
| --------------------------------------------- | ------------------------------------------- |
|                    Hardcoded in index.html    |                   Centralized external JS   |
|                 Risk of duplicate page views  |                          Duplicate-safe     |
|                Manual environment changes     |                      Environment-driven     |
|                            Less scalable      |                       Enterprise scalable   |

***

## PART 4 — Connect GTM to GA4

Now we connect GA4 (Measurement ID) to GTM.

***

### Step 1: Create GA4 Configuration Tag

In GTM:

1. Go to Tags
2. Click New
3. Click Tag Configuration
4. Choose → Google Analytics: GA4 Configuration

Paste:

```
Measurement ID → G-XXXXXXXXXX
```

***

### Step 2: Add Trigger

Click Triggering\
Choose:

```
All Pages
```

Meaning:\
Every page load will send data.

Save it as:

```
GA4 - Configuration
```

<figure><img src="../../../.gitbook/assets/unknown (8).png" alt=""><figcaption></figcaption></figure>

***

### Step 3: Click Submit → Publish

Now your GA4 is connected&#x20;

***

## PART 5 — Verify Installation

Open website.

In GA4:

* Go to Realtime
* You should see your visit.

If not:

* Use GTM → Preview mode
* Check Tag fired or not

<figure><img src="../../../.gitbook/assets/unknown (9).png" alt=""><figcaption></figcaption></figure>

***

## PART 6 — Track Page Views Properly

By default:\
GA4 tracks page\_view automatically.

But if SPA (React app like yours):

You may need:

* History Change Trigger
* Manual Page View Event

***

## PART 7 — Track Button Clicks

Example:\
Track "Create Campaign" button click.

***

### Step 1: Enable Built-in Variables

In GTM:\
Variables → Configure → Enable:

* Click Text
* Click Classes
* Click ID
* Click URL<br>

<figure><img src="../../../.gitbook/assets/unknown (10).png" alt=""><figcaption></figcaption></figure>

***

### Step 2: Create Trigger

Go to:\
Triggers → New

Choose:

```
Click - All Elements
```

Select:

```
Some Clicks
```

Condition example:

```
Click Text equals Create Campaign
```

Save as:

```
Trigger - Create Campaign Click
```

<figure><img src="../../../.gitbook/assets/unknown (11).png" alt=""><figcaption></figcaption></figure>

***

### Step 3: Create Event Tag

Tags → New

Choose:

```
Google Analytics: GA4 Event
```

Select:

* Configuration Tag → GA4 Configuration

Event Name:

```
create_campaign_click
```

Trigger:

```
Trigger - Create Campaign Click
```

<figure><img src="../../../.gitbook/assets/unknown (12).png" alt=""><figcaption></figcaption></figure>

Save & Publish.

***

## PART 8 — Event Parameters Not Showing?

Very common issue&#x20;

GA4 does NOT auto show parameters.

You must register them manually.

***

### Step 1: Register Custom Dimension

Go to:

GA4 → Admin → Custom Definitions

Click:

```
Create Custom Dimension
```

Fill:

* Name → Campaign Name
* Scope → Event
* Event Parameter → campaign\_name

Save.

Now parameter appears in reports.\
<br>

<figure><img src="../../../.gitbook/assets/unknown (13).png" alt=""><figcaption></figcaption></figure>

***

## PART 9 — Create Dashboard

Go to:

GA4 → Explore

OR

Reports → Library → Create Custom Report

Example dashboard:

* Page Views
* Button Clicks
* Top Campaign
* Users
* Sessions

<figure><img src="../../../.gitbook/assets/unknown (14).png" alt=""><figcaption></figcaption></figure>

***

## PART 10 — QA / UAT / PROD Setup (Important)

Best practice:

| **Environment** | **GA4 Property** | **GTM Container** |
| --------------- | ---------------- | ----------------- |
| QA              | Separate         | Separate          |
| UAT             | Separate         | Separate          |
| PROD            | Separate         | Separate          |

Do NOT mix them.

***

## PART 11 — Export / Import GTM Container

For moving QA to UAT:

GTM → Admin → Export Container

In UAT:\
Admin → Import Container\
Choose:

* Merge
* Overwrite conflicting tags

<figure><img src="../../../.gitbook/assets/unknown (16).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/unknown (15).png" alt=""><figcaption></figcaption></figure>

***

## PART 12 — Debugging Checklist

If not working:

Is GTM script added?\
Is container published?\
Is correct Measurement ID used?\
Is trigger firing in Preview?\
Is event visible in Realtime?\
Are parameters registered as custom dimensions?

***

## Final Architecture

```
React App
   ↓
dataLayer.push()
   ↓
GTM Trigger
   ↓
GA4 Event Tag
   ↓
Google Analytics
   ↓
Reports & Dashboard
```

***

\
Common Mistakes & Troubleshooting Guide
---------------------------------------

This section covers the most common issues faced during GA4 + GTM setup and how to resolve them.

***

### Events Are Not Showing in GA4

#### Possible Causes

* GTM container not published
* Wrong Measurement ID used
* Trigger not firing
* Event name mismatch
* Looking at wrong GA4 property
* Checking standard reports instead of Realtime<br>

#### How to Fix

1. Open GTM → Preview Mode
2. Verify tag is firing.
3. Check Measurement ID in:
4. GA4 → Admin → Data Streams
5. Compare with ID used in GTM.
6. Confirm you are viewing the correct property (QA/UAT/PROD).
7. Check:
8. GA4 → Realtime report.
9. Wait 5–10 minutes (Realtime is instant, standard reports are delayed).

***

### Event Parameters Not Showing in Reports

#### Why This Happens

GA4 does NOT automatically show custom parameters in reports.

Even if event is firing, parameters will not appear unless registered.

#### How to Fix

Go to: `GA4 → Admin → Custom Definitions`

1. Click: `Create Custom Dimension`
2. Set:\
   Scope → Event\
   Event Parameter → exact parameter name
3. Save.

After registration:

* It only applies to future data.
* It may take 24 hours to reflect in standard reports.

***

### QA Data Showing but UAT Not Showing

#### Possible Causes

* Wrong Measurement ID configured
* Wrong GTM container used
* UAT container not published
* Analytics script not loaded in UAT
* Environment config not updated

#### How to Fix

1. Inspect page → Check Network tab:
2. Confirm correct GTM container ID.
3. Verify:\
   UAT GA4 property exists.\
   Correct Measurement ID is used.
4. Check Helm / env YAML configuration.
5. Use GTM Preview in UAT.
6. Confirm events appear in UAT property Realtime.

***

### Tags Showing Old Measurement ID

#### Why It Happens

* GA4 Configuration tag not updated
* Old container version published
* Environment pointing to old analytics JS
* Browser cache issue

#### How to Fix

Go to: `GTM → Tags → GA4 Configuration`

1. &#x20;Update Measurement ID.
2. Click: `Submit → Publish`
3. Hard refresh browser (Ctrl + Shift + R).
4. Confirm correct container version is live.
5. If using S3-hosted analytics file: Verify updated file is deployed.

***

### Duplicate Page Views

#### Why It Happens

* GA4 auto page\_view enabled
* GTM also sending page\_view
* Both gtag.js and GTM firing page\_view

#### How to Fix

If using GTM as main controller:

```json5
gtag('config', 'G-XXXXXXX', {
  send_page_view: false
});
```

And let GTM handle pageview tracking.

***

### Custom Events Not Firing

#### Possible Causes

* dataLayer.push() event name mismatch
* Custom Event Trigger name mismatch
* Trigger condition incorrect
* Code not executed before GTM loads

#### How to Fix

Check console: `window.dataLayer`

1. Verify event name matches exactly in:
2. dataLayer.push()
3. GTM Custom Event Trigger
4. Use GTM Preview mode.
5. Ensure event fires after GTM loads.

***

### Realtime Shows Data but Reports Don’t

#### Why

* Standard reports take time to process.
* Custom dimensions registered late.
* Date range filter issue.

#### Fix

* Check date range (top right corner).
* Wait up to 24 hours for full reports.
* Confirm custom dimension registered before event triggered.

***

### Container Changes Not Reflecting

#### Why

* Forgot to click Publish.
* Looking at old container version.
* Wrong environment container.
* Browser cache.

#### Fix

1. GTM → Versions → Confirm latest published.
2. Check container ID on page source.
3. Hard refresh.
4. Confirm environment config correct.

***

## Quick Technical Debug Order (Practical Version)

When something fails, always check in this order:

1. Page Source → Is GTM container ID correct?
2. GTM Preview → Is tag firing?
3. GA4 Realtime → Is event arriving?
4. Custom Definitions → Are parameters registered?
5. Reports → Check date filter

***

## Best Practices (Very Important)

#### Environment Architecture

* Use separate GA4 properties for QA, UAT, and Production.
* Use separate GTM containers for each environment.
* Never mix Measurement IDs across environments.
* Ensure environment-specific configuration via env files or deployment setup.

***

#### Naming & Event Design

* Use snake\_case for all event names.
* Keep naming consistent across all environments.
* Avoid changing event names after deployment.
* Maintain a centralized event naming convention document.

***

#### Testing & Deployment

* Always test tags in GTM Preview Mode before publishing.
* Verify events in GA4 Realtime before validating reports.
* Publish only after confirming correct Measurement ID and container.
* Document every tag, trigger, and parameter created.

***

#### Parameter Management

* Register all custom parameters as Custom Dimensions in GA4.
* Keep parameter names consistent with dataLayer pushes.
* Avoid renaming parameters after production release.

## Analytics Debug Checklist&#x20;

| **Check Item**         | **Where to Verify**            | **Expected Result**                | **Action if Fails**                       |
| ---------------------- | ------------------------------ | ---------------------------------- | ----------------------------------------- |
| GTM Script Loaded      | View Page Source / Network Tab | GTM container ID visible           | Fix environment config / script injection |
| Correct Container ID   | Page Source                    | QA/UAT/PROD ID matches environment | Update analytics file                     |
| Container Published    | GTM → Versions                 | Latest version published           | Submit → Publish                          |
| Tag Firing             | GTM Preview Mode               | Tag shows “Fired”                  | Fix trigger conditions                    |
| Correct Measurement ID | GA4 Config Tag                 | G-XXXX matches property            | Update GA4 Config                         |
| Event Visible          | GA4 → Realtime                 | Event appears instantly            | Check property selection                  |
| Parameters Visible     | GA4 → Custom Definitions       | Parameter registered               | Create Custom Dimension                   |
| Reports Showing Data   | GA4 Reports                    | Data visible in date range         | Wait 24 hrs / adjust filter               |
| Duplicate Page Views   | GA4 Realtime                   | Only one page\_view                | Disable send\_page\_view in gtag          |
| Environment Separation | GA4 Properties                 | QA data not mixing with PROD       | Separate containers & IDs                 |

***

## Introduction to Looker Studio – Basics and interface overview

Looker Studio is where data visualization happens.

&#x20;It allows you to connect data sources such as Google Analytics, Matomo, Excel sheets, or any other supported data source of your choice.&#x20;

You can create reports, add selected metrics like Sessions, Users, and Events, and apply filters and controls to focus on specific data.&#x20;

It also enables you to create calculated fields for custom KPIs and group related values when needed.

Here is what Looker Studio looks like

### 1. Create a new asset (Report, Data Source, or Exploration)

This option allows you to start something new in Looker Studio. You can create a report to build dashboards, add a data source to connect new data, or create an exploration to analyze data in more detail.

<figure><img src="../../../.gitbook/assets/unknown (17).png" alt=""><figcaption></figcaption></figure>

### 2. Create a New Report

This option allows you to start a new blank dashboard in Looker Studio, where you can connect a data source, add charts and controls, and build your report from scratch.

<figure><img src="../../../.gitbook/assets/unknown (18).png" alt=""><figcaption></figcaption></figure>

### 3. Report Editor Screen

This is the main workspace in Looker Studio where you build and edit dashboards. Here, you add charts, select metrics and dimensions, insert controls, and customize the layout and styling of your report.

<figure><img src="../../../.gitbook/assets/unknown (19).png" alt=""><figcaption></figcaption></figure>

### 4. Add Data Source

This option allows you to connect a new data source to your report in Looker Studio, such as Google Analytics, Matomo, or an Excel/Google Sheets file, so you can start using its fields (dimensions and metrics) in your dashboard.

<figure><img src="../../../.gitbook/assets/unknown (20).png" alt=""><figcaption></figcaption></figure>

### 5. Data Panel

After you add a data source in Looker Studio, this is where your data appears. The Data Panel displays all the available fields from the connected source.

<figure><img src="../../../.gitbook/assets/unknown (21).png" alt=""><figcaption></figcaption></figure>

These fields are categorized as:

Dimensions – A Dimension is a descriptive field. It represents categories such as date, country, page name, or campaign. Identified by icons such as ABC (text), Calendar (date), or Location (geographic).

Metrics – A Metric is a numerical field. It represents measurable values such as sessions, users, events, or page views. Metrics are calculated or aggregated to show totals, averages, or counts. Identified by the 123 number icon, indicating numeric values that can be calculated or aggregated.

You use the Data Panel to select fields when creating visualizations.

<figure><img src="../../../.gitbook/assets/unknown (22).png" alt=""><figcaption></figcaption></figure>

### 6. Add a Chart

This option allows you to insert a visualization into your report in Looker Studio, such as a time series, bar chart, pie chart, table, or scorecard etc.

<figure><img src="../../../.gitbook/assets/unknown (23).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/unknown (24).png" alt=""><figcaption></figcaption></figure>

<br>

### 7. Properties Panel

The Properties panel in Looker Studio changes depending on the visualization you select. Each chart has its own configuration options. The panel is divided into two sections - Setup & Style

* Use the options in the SETUP tab to configure the visualization’s data, chart type, filters, and other functional settings. This is where you define what information the visualization displays and how it behaves.
* Use the options in the STYLE tab to configure the visualization’s appearance, including layout, colors, labels, formatting, and overall visual presentation. This controls how the visualization looks on the report page.

<figure><img src="../../../.gitbook/assets/unknown (25).png" alt=""><figcaption></figcaption></figure>

### 8. Add a Control

This option allows you to insert interactive filters into your report in Looker Studio, such as a date range selector or drop-down filter. By default, any control you add applies to the charts on that specific page of the report.

<figure><img src="../../../.gitbook/assets/unknown (26).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/unknown (27).png" alt=""><figcaption></figcaption></figure>

***

### Connecting Data - Linking Google Analytics (GA) or any other data source

1. Click on Add Data in the report editor of Looker Studio.
2. A list of available connectors will appear.

<figure><img src="../../../.gitbook/assets/unknown (28).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/unknown (29).png" alt=""><figcaption></figcaption></figure>

3. Choose your data source, such as:
4. Google Analytics
5. Matomo
6. Excel / Google Sheets
7. Or any other supported connector
8. Click on the connector you want to use.
9. Select the appropriate account, property, and dataset (if applicable).
10. Click Add to connect the data source to your report.

Once connected, the data source becomes available to use in your visualizations.

***

### &#x20;Visualizations – Charts, tables, and graphs

To add a visualization in Looker Studio:

1. Click on Add a Chart from the top toolbar.
2. Select the type of visualization you want (such as a time series, bar chart, table, or scorecard).
3. Click or drag on the canvas to place the visualization.
4. In the SETUP tab, choose the required fields from the Data Panel.

Once added, the visualization will display data based on the selected fields, and you can adjust its appearance using the STYLE tab if needed.

***

### Adding Filters

In Looker Studio, filters can be added in two ways:

#### 1. Adding a Filter Using a Control (Add a Control)

This method allows users viewing the report to interact with the data without editing the report structure.

Steps to add the control (in Edit mode):

* Click on Add a Control from the top toolbar.
* Select a control type (e.g., Drop-down list or Date range control).
* Place it on the report canvas.
* In the SETUP tab, select the field the control should filter by.

How it works:

* When the report is opened in viewer mode, users can select values from the control (for example, choose a specific date range or category).
* The charts on that page update automatically based on the selected value.
* Viewers can change selections multiple times.
* They can also reset the control to return to the default view.

By default, controls apply to all visualizations on that page unless scope is modified.

#### 2. Adding a Filter from the SETUP Tab

This method is configured in edit mode and applies only to a specific visualization.

Steps:

* Select the visualization you want to filter.
* Go to the SETUP tab in the Properties panel.
* Scroll to the Filter section.
* Click Add a Filter.
* Choose Create a Filter.
* Set up the condition:
* Select Include or Exclude.
* Choose the field.
* Define the condition type (e.g., Equals, Contains, RegExp Match, Greater than, etc.).
* Enter the value(s).
* Click Save.

<figure><img src="../../../.gitbook/assets/unknown (30).png" alt=""><figcaption></figcaption></figure>

How it works:

* The condition you set determines which data is shown or hidden in that visualization.
* The filter is fixed and only affects the selected chart.
* It can only be edited or removed in edit mode.
* Viewers cannot modify this filter.

***

### Creating Calculated Fields

In Looker Studio, a calculated field is used when the existing fields are not sufficient for your reporting needs. It allows you to use available data to create a new custom field (metric or dimension).

Starting from the Data Panel

* Go to the Data Panel.
* Click on Add a Field.
* Enter a name for your new field.
* Write the formula.
* Click Save.

<figure><img src="../../../.gitbook/assets/unknown (31).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/unknown (32).png" alt=""><figcaption></figcaption></figure>

## Use Case 1: Creating a Custom Dimension (Page Name)

#### Problem

In the Console QA + UAT environment, the Page Title appeared as a unified value like “DIGIT HCM” for multiple screens. This made it difficult to identify specific pages such as Login or Dashboard.

#### Solution

We created a custom dimension using Page Path and Screen Class to define meaningful page names.

#### Steps:

* Go to the Data Panel.
* Click Add a Field.
* Enter a field name (e.g., Custom Page Name).
* Add the formula:

CASE

&#x20; WHEN REGEXP\_CONTAINS(Page path and screen class, "employee/user/login") THEN "Login"

&#x20; WHEN REGEXP\_CONTAINS(Page path and screen class, "dashboard") THEN "Dashboard"

&#x20; ELSE "Other"

END

* Click Save.

<figure><img src="../../../.gitbook/assets/unknown (33).png" alt=""><figcaption></figcaption></figure>

#### What this does:

* Checks the page path.
* Assigns a readable name based on conditions.
* Creates a new dimension that can be used in visualizations.

## Use Case 2: Creating a Custom Metric (Average Time Per User)

#### Problem

We needed to calculate average time on a page that was not directly available.

#### Solution

We created a custom metric using existing numeric fields.

Example formula:

User engagement / Total users

#### Steps:

* Go to the Data Panel.
* Click Add a Field.
* Enter a name (e.g., Avg Time on Page).
* Add the formula.
* Click Save.

<figure><img src="../../../.gitbook/assets/unknown (34).png" alt=""><figcaption></figcaption></figure>

#### What this does:

* Uses existing metrics.
* Performs a calculation.
* Creates a new measurable value that can be added to charts or scorecards.

#### Key Difference

* The first example creates a new category (dimension).
* The second example creates a new calculated number (metric).

Both are created using formulas but serve different analytical purposes.

\
<br>

\
\
<br>
