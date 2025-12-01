# Google Analytics 4 & Google Tag Manager Installation Guide

**Prerequisites**

Before starting, ensure:

* ✔ You have a Google account with access to **Google Analytics** and **Google Tag Manager**
* ✔ You have **admin access** to your web application’s codebase
* ✔ (Optional, for dashboards) Access to **Looker Studio**

***

### **Part 1: Google Analytics 4 (GA4) Setup**

#### **Step 1: Create a GA4 Property**

1. Visit `analytics.google.com` and sign in
2. Click **Admin** → **Create Property**
3. Enter:
   * **Property name** (e.g., _DIGIT Portal - Production_)
   * **Reporting time zone** & **Currency**
4. Click **Next**, specify business info → **Create**

#### **Step 2: Create a Data Stream**

1. Select **Web**
2. Enter Website URL (example: `https://your-domain.gov.in`)
3. Set Stream name (example: _Main Website_)
4. Keep **Enhanced Measurement** enabled
5. Click **Create Stream**

#### **Step 3: Note Your Measurement ID**

Format: **G-XXXXXXXXXX**\
→ You'll need this for integration

***

### **Part 2: Google Tag Manager (GTM) Setup**

#### **Step 1: Create GTM Account + Container**

1. Visit `tagmanager.google.com` → **Create Account**
2. Add:
   * Account name = Organization name
   * Country
3. Container name = Website URL
4. Target platform = **Web**
5. Accept Terms of Service

#### **Step 2: Embed GTM Snippets**

Insert into your web app:

**Inside `<head>`**

```html
<script>/* GTM HEAD CODE */</script>
```

**Right after `<body>` open**

```html
<noscript>/* GTM BODY CODE */</noscript>
```

Container ID format: **GTM-XXXXXXX**

***

### **Part 3: Web Application Integration (Workbench UI)**

We are enabling analytics for **workbench-ui** using **Nginx-based custom JavaScript injection** as part of the Helm configuration.\
In the `hcm-demo-latest` environment, the following configuration injects external analytics scripts into the application at runtime:

```yaml
workbench-ui:
  custom-js-injection: |
    sub_filter.conf: "
      sub_filter  '<head>' '<head>
      <script src=https://hcm-demo-assets.s3.ap-south-1.amazonaws.com/demo/globalConfigsWorkbenchDemo.js type=text/javascript ></script>
      <script src=https://hcm-demo-assets.s3.ap-south-1.amazonaws.com/analytics/analytics.js type=text/javascript ></script>
      ';"  
```

The injected file `analytics.js` (hosted at\
`https://hcm-demo-assets.s3.ap-south-1.amazonaws.com/analytics/analytics.js`)\
contains everything required for analytics, including loading Google Tag Manager and custom Google Analytics scripts.

Example expected content of `analytics.js`:

```javascript
// -------------------------------------------
// Google Tag Manager (GTM) Initialization
// -------------------------------------------
(function setupGTM() {
  console.info("Google Tag Manager initialized");

  // Create dataLayer if not present
  window.dataLayer = window.dataLayer || [];
  window.dataLayer.push({
    "gtm.start": new Date().getTime(),
    event: "gtm.js"
  });

  // Insert GTM script
  var gtmScript = document.createElement("script");
  gtmScript.async = true;
  gtmScript.src = "https://www.googletagmanager.com/gtm.js?id=GTM-XXXXXXX";

  var firstScript = document.getElementsByTagName("script")[0];
  firstScript.parentNode.insertBefore(gtmScript, firstScript);

  // Noscript fallback (iframe)
  var noscript = document.createElement("noscript");
  noscript.innerHTML =
    '<iframe src="https://www.googletagmanager.com/ns.html?id=GTM-XXXXXXX" height="0" width="0" style="display:none;visibility:hidden"></iframe>';

  document.addEventListener("DOMContentLoaded", function () {
    document.body.insertBefore(noscript, document.body.firstChild);
  });
})();

// -------------------------------------------
// Google Analytics 4 Loader
// -------------------------------------------
(function loadGA4() {
  console.info("Loading Google Analytics 4");

  // Load GA4 script
  var ga4Script = document.createElement("script");
  ga4Script.async = true;
  ga4Script.src = "https://www.googletagmanager.com/gtag/js?id=G-XXXXXXX";
  document.head.appendChild(ga4Script);

  // GA4 configuration
  ga4Script.onload = function () {
    window.dataLayer = window.dataLayer || [];
    function gtag() {
      dataLayer.push(arguments);
    }
    gtag("js", new Date());
    gtag("config", "G-XXXXXXX", { send_page_view: true });
  };
})();

```

**Reference**&#x20;

Devops changes&#x20;

{% embed url="https://github.com/egovernments/health-campaign-devops/blob/861f4e33377a24fb0be0f84bbbe839ec3588e210/config-as-code/helm/environments/hcm-demo-latest.yaml#L142" %}

Analytics Script

{% embed url="https://hcm-demo-assets.s3.ap-south-1.amazonaws.com/analytics/analytics.js" %}

***

### **Step 2: Configure GA4 Tag in GTM**

1. In GTM: **Tags → New**
2. Name: **GA4 Configuration**
3. Select:
   * **Tag Configuration → Google Analytics: GA4 Configuration**
4. Enter **Measurement ID**
5. Trigger → **All Pages**
6. Save

#### **Step 3: Publish Container**

📌 GTM → **Submit → Version name + Publish**

***

### **Part 4: Verification & Debugging**

#### 🔍 Debug Options

| Tool                    | Usage                               |
| ----------------------- | ----------------------------------- |
| **GA4 DebugView**       | Shows events in real-time           |
| **GTM Preview Mode**    | Validates tag triggers on live site |
| **GA4 Realtime Report** | Live users + active pages           |

**Enable Debug Mode Manually**

```js
gtag('config', 'G-XXXXXXXXXX', { debug_mode: true });
```

**Data Retention**

GA4 → Admin → Data Settings → Data Retention\
Set according to compliance needs

***

### **Part 5: Looker Studio (Dashboarding & Reporting)**

🎯 Purpose: Create **custom analytics dashboards** using GA4 data

#### **Step 1: Open Looker Studio**

Go to:\
[https://lookerstudio.google.com/](https://lookerstudio.google.com/)

Click **Create → Report**

#### **Step 2: Connect GA4 Data Source**

1. Under **Select a data source**
2. Choose:\
   → **Google Analytics**
3. Select your GA4 property & data stream
4. Click **Add → Add to Report**

#### **Step 3: Build Dashboards**

You can now:\
✔ Add charts (Time series, tables, geo maps, funnels)\
✔ Customize filters (e.g., Application Module, Page Type)\
✔ Create KPIs like:

* [ ] Total Users
* [ ] Avg Engagement Time
* [ ] Conversion Events
* [ ] Event Counts per Page
* [ ] Government service module adoption metrics

#### **Step 4: Apply Filters for Govt Use-Cases**

Example recommended filters:

| Filter          | Purpose                 |
| --------------- | ----------------------- |
| Tenant ID       | City/ULB performance    |
| Service Module  | eGov product usage      |
| Page Name       | Screen-level visibility |
| Device Category | Web/Mobile split        |

#### **Step 5: Sharing & Publishing**

You can:

* Share internally with view/edit permissions
* Embed dashboard inside DIGIT admin panels (iframe)
* Schedule PDF email reports to stakeholders
