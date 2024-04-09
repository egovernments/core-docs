# Android Web View & How To Generate APK

## Overview

This document will help us generate the APK for Citizen and Employee applications.

## Steps

### 1. Android Web View <a href="#id-1.-android-web-view" id="id-1.-android-web-view"></a>

Android offers a variety of ways to present content to a user. To provide a user experience that’s consistent with the rest of the platform, it’s usually best to build a native app that incorporates framework-provided experiences, such as [Android App Links](https://developer.android.com/training/app-links) or [Search](https://developer.android.com/guide/topics/search). Additionally, you can use Google Play-based experiences, such as [App Actions](https://developer.android.com/guide/actions) and [Slices](https://developer.android.com/guide/slices), where Google Play services are available. Some apps, however, may need increased control over the UI. In this case, a `WebView` is a good option for displaying trusted first-party content.

<div align="left">

<figure><img src="../../../.gitbook/assets/figure1.png" alt="" width="340"><figcaption></figcaption></figure>

</div>

In Egov we create only responsive web apps instead of native apps (Android, IOS). The Android web view is used to render the out web application.

<div align="left">

<figure><img src="../../../.gitbook/assets/Screenshot_2023-12-18-11-27-42-71_9751719c52650ee4605aed3597f307d8.jpg" alt="" width="375"><figcaption></figcaption></figure>

</div>

### 2. Generate APK For Citizen & Employee Applications <a href="#id-2.-how-to-generate-apk-for-citizen-and-employee-application" id="id-2.-how-to-generate-apk-for-citizen-and-employee-application"></a>

1. Clone the [GitHub - egovernments/DIGIT-OSS: eGov Foundation's Open source repository of the DIGIT](https://github.com/egovernments/DIGIT-OSS) repo.
2. Open the below location in the [Android studio](https://developer.android.com/studio).

{% embed url="https://github.com/egovernments/DIGIT-OSS/tree/master/frontend/mono-ui/web/rainmaker-webview" %}

<figure><img src="../../../.gitbook/assets/Screenshot 2023-12-18 at 11.31.54 AM.png" alt=""><figcaption></figcaption></figure>

**Generate APK for citizen application**

1. Go to build. Gradle file there we have created multiple environments(UAT and PROD), please select the environment where you want to generate APK and put your web application URL.
2.  Update the web application URL as required Application URL.

    `buildConfigField 'String', 'url', '"https://uat.digit.org/citizen/user/register"'`

    also, specify the citizen gateway hostname if not using Mastercard,

    `buildConfigField 'String', 'gatewayHost', '"migs.mastercard.co.in"'`

<figure><img src="../../../.gitbook/assets/Screenshot 2023-12-18 at 11.35.46 AM.png" alt=""><figcaption></figcaption></figure>

3\. Save the file on the left side of the Android studio. Click Build Variants and select the applicable build variant.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-12-18 at 11.37.35 AM.png" alt=""><figcaption></figcaption></figure>

4\. Click on **Build** menu, select **Build APK(s)** submenu.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-12-18 at 11.38.42 AM.png" alt=""><figcaption></figcaption></figure>

It will take some time to generate and it will show generated location.

**Generating APK for employee application**

1\. Go to build. Gradle file there we have created multiple environments (UAT and PROD), please select the environment where you want to generate APK and put your web application URL.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-12-18 at 11.37.35 AM.png" alt=""><figcaption></figcaption></figure>

2\. Save the file, left side of the android studio click Build variants, and select build variant.

<figure><img src="../../../.gitbook/assets/figure9.png" alt=""><figcaption></figcaption></figure>

3\. Click on the build menu, and select Build APK(s) submenu.

<figure><img src="../../../.gitbook/assets/figure11.png" alt=""><figcaption></figcaption></figure>

It will take some time to generate and it will show generated location.

### 3. Generate APK For Production <a href="#id-3.-generating-apk-for-production" id="id-3.-generating-apk-for-production"></a>

1. Follow the 3rd and 4th steps mentioned above.
2. Click on the **Build** menu and select **Generate Signed Bundle / APK**.

<figure><img src="../../../.gitbook/assets/figure10.png" alt=""><figcaption></figcaption></figure>

3. Select 1st radio button - **Android App Bundle.**

<figure><img src="../../../.gitbook/assets/figure12.png" alt=""><figcaption></figcaption></figure>

4. Enter the information presented in the form and click on **Next.**

<figure><img src="../../../.gitbook/assets/figure13.png" alt=""><figcaption></figcaption></figure>

5. Upload the APK generated by the 4th step and upload it to the play store.

## Related Links

[How to debug android app using Chrome browser](faqs/debug-android-app-using-chrome-browser.md)