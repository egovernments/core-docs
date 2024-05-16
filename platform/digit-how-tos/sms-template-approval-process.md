# SMS Template Approval Process

## Overview

According to TRAI’s regulation on unsolicited commercial communication, all teleco's must verify every sms content before delivering it (Template scrubbing). For this all the businesses using SMS need to register Entities, SenderIDs, SMS templates in a centralised DLT portal.

Below are the steps to register the SMS template in a centralised DLT portal and to add the template in the SMS country portal (Service provider).

**Step 1:** Visit **Airtel DLT portal**([![](https://dltconnect.airtel.in/static/img/fav.png)AIRTEL DLT](https://dltconnect.airtel.in/login/) ) and select your area of operation as **Enterprise** then click on next.

<figure><img src="../../.gitbook/assets/dlt1.png" alt=""><figcaption></figcaption></figure>

**Step 2:** Login into the portal by entering the proper credentials and OTP.

{% hint style="info" %}
Please contact the HR manager for the credentials and the OTP.
{% endhint %}

<figure><img src="../../.gitbook/assets/dlt2.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/dlt3.png" alt=""><figcaption></figcaption></figure>

**Step 3:** Now select the **Template** from option and then click on **content templates**.

<figure><img src="../../.gitbook/assets/dlt4 (1).jpeg" alt=""><figcaption></figcaption></figure>

Now click on **Add** button to go to next section

<figure><img src="../../.gitbook/assets/dlt5.jpeg" alt=""><figcaption></figcaption></figure>

**Step 4:** Select the option mentioned in the image below.

<figure><img src="../../.gitbook/assets/dlt6.jpeg" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Note:\
a) For placeholder text (dynamic text in message) mention **{#var#}** in the message. Each **{#var#}** can contains 0-30 character. If dynamic text is supposed to go more than 30 characters in length, then two **{#var#}** have to mention side by side. Now the dynamic text can be up to 60 characters.\
**Example**:- _Hi Citizen,_\
_Click on this link to pay the bill {#var#}{#var#}_\
\
_EGOVS_\
\
b) It is mandatory to mention _**EGOVS**_ at the end of every message.\
\
c) Select Template message Type as Regional if the message is in other language rather than english.
{% endhint %}

After clicking on Save button, template is added in the portal, Now wait for the approval of the template.\
Once the template get approved save the template id and the message.

<figure><img src="../../.gitbook/assets/dlt7.jpeg" alt=""><figcaption></figcaption></figure>

**Step 5:** Repeat process from **Step 3** to **Step 4** to register template in DLT portal.

{% hint style="info" %}
Note: The below steps are to add approved templates in the SMS Country web portal. These steps might be different for other service providers but the data required for any service provider would be the same.
{% endhint %}

**Step 6:** Now, login into SMS Country portal ([SMS Marketing Solution Provider | SMS & Voice Marketing APIs - SMSCountry](https://www.smscountry.com/Index.aspx?msg=Logged%20out%20successfully) ) by entering proper credentials.

{% hint style="info" %}
Please contact the HR manager for the credentials.
{% endhint %}

<figure><img src="../../.gitbook/assets/dlt8.png" alt=""><figcaption></figcaption></figure>

**Step 7:** Select option Features, then click on Manage button under Template section.

<figure><img src="../../.gitbook/assets/dlt9.jpeg" alt=""><figcaption></figcaption></figure>

Then click on **Add DLT Template** button.

<figure><img src="../../.gitbook/assets/dlt10.jpeg" alt=""><figcaption></figcaption></figure>

**Step 8:** Mention the template id and message of approved template which we have saved earlier in step 4. And select sender id as **EGOVFS**

<figure><img src="../../.gitbook/assets/dlt11.png" alt=""><figcaption></figcaption></figure>

After adding all the above details click on **Add Template** button.\
Now the DLT approved template get added into SMS Country portal and it is ready to use.

{% hint style="info" %}
Select ISLanguage check box if the message is in other language rather than english.
{% endhint %}

**Step 9:** Repeat process from **Step 7** to **Step 8** to add approved template in SMS Country portal.
