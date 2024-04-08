---
description: Steps to generate APKs and App bundles for Android applications
---

# Generate Android APKs & App Bundles

## Overview

Follow the steps on this page to build the APK and IPA for deploying in Play Store and App-store.

## Steps

### Generate APK For Testing&#x20;

1. Follow the [Flutter Installation and setup Guide](../setup-development-environment/flutter-installation-and-setup-guide.md) and [Run the Application](../setup-development-environment/run-application.md) till the Flutter pub is set up.
2.  Run the below command in your terminal from theroot of the project to generate the APK&#x20;

    **`flutter build apk --release`**

<figure><img src="https://lh5.googleusercontent.com/i5RVBw4Xi1kLQZJ3Lv6kmAx-wjDKcVgIeq_1Xg-Dc5ksIzR1CHSNyI7ed7zYwva79eU6nenF837ZsNhNU29XAq4vbhS1BaETLUFmzDRc4zBVpSQTsZhfx-56rp3QqMBJnzJrK80sST5Do6DYOyduVls" alt=""><figcaption></figcaption></figure>

### Generate & Publish App Bundle To Play Store

#### Pre-requisites

* Prior knowledge of generating unique key store files for your application ( Reference links: [Generating key store for your Android application](https://docs.oracle.com/cd/E35822\_01/server.740/es\_admin/src/tadm\_ssl\_jetty\_keystore.html))
* Changing the App name&#x20;
* Changing App Logo (Ref Link: [Changing app logo in Flutter](https://www.geeksforgeeks.org/flutter-changing-app-icon/))
* Prior knowledge of app bundle creation for publishing in the Play Store
* Terms and Conditions and Privacy Documents for your application

{% hint style="info" %}
**Note:** The generated key store file needs to be added to the Android/app folder of your project. This is needed for publishing the next version of your application.&#x20;

![](<../../../../.gitbook/assets/image (158).png>)
{% endhint %}

#### Steps

1. Add a key.properties file inside your Android folder which is a reference to your key store file. Below is the sample key.properties file.

```
storePassword=muktasoft
keyPassword=muktasoft
keyAlias=upload
storeFile=muktasoft.jks
```

2. Run the below command in your terminal from the root of the project to generate the App bundle to publish in the play store.

**`flutter build app bundle`**

<figure><img src="../../../../.gitbook/assets/image (120).png" alt=""><figcaption></figcaption></figure>
