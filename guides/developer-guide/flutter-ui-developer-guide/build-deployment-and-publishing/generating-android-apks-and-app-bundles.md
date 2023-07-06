---
description: Overview of generating APKs and App bundles for Android applications
---

# Generating Android APKs and App Bundles

### Generating APK for testing

1. Follow the [Flutter Installation and setup Guide](../setup-development-environment/flutter-installation-and-setup-guide.md) and [Run the Application](../setup-development-environment/run-application.md) till flutter pub get step.
2.  Run the below command in your terminal from root of the project to generate the APK&#x20;

    **`flutter build apk --release`**

<figure><img src="https://lh5.googleusercontent.com/i5RVBw4Xi1kLQZJ3Lv6kmAx-wjDKcVgIeq_1Xg-Dc5ksIzR1CHSNyI7ed7zYwva79eU6nenF837ZsNhNU29XAq4vbhS1BaETLUFmzDRc4zBVpSQTsZhfx-56rp3QqMBJnzJrK80sST5Do6DYOyduVls" alt=""><figcaption></figcaption></figure>

### Generating and Publishing app bundle to Play Store

#### Pre-requisites:

* Prior knowledge of generating unique key store file for your application ( Reference links : [Generating key store for your android application](https://docs.oracle.com/cd/E35822\_01/server.740/es\_admin/src/tadm\_ssl\_jetty\_keystore.html))
* Changing the App name&#x20;
* Changing App Logo (Ref Link: [Changing app logo in flutter](https://www.geeksforgeeks.org/flutter-changing-app-icon/))
* Prior knowledge of app bundle creation for publishing in Play Store
* Terms and Conditions and Privacy Documents for your application

{% hint style="info" %}
Note: The generated key store file need to be added to the android/app folder of your project. This is needed for publishing next version of your application.&#x20;

![](<../../../../.gitbook/assets/image (10).png>)
{% endhint %}

1. After the above steps add a key.properties file inside your android folder which is a reference to your key store file, Below is the sample key.properties file&#x20;

```
storePassword=muktasoft
keyPassword=muktasoft
keyAlias=upload
storeFile=muktasoft.jks
```

2. Run the below command in your terminal from root of the project to generate the App bundle to publish in play store&#x20;

**`flutter build app bundle`**

<figure><img src="../../../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>
