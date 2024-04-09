# Flutter Installation & Setup Guide

## Steps

1. Install Flutter on your device&#x20;
   * [Install Flutter](https://docs.flutter.dev/get-started/install) &#x20;
   * [Setup an Editor](https://docs.flutter.dev/get-started/editor)\

2. After installation of Flutter, to check the installed version, use the command  **flutter --version**

{% hint style="info" %}
**Note: Version might vary based on the current version used in the project**
{% endhint %}

<figure><img src="https://lh4.googleusercontent.com/itLJFo7KgDfwn0va0DTnXiTY7fWN2qz-mXuJSq8JYc-l1dFZ5spv9qQbct-HZRHK2n71-BWnuB_94ij5VrXgEdB6ceowF5W7tglDY4TbvCNsBusH2Zq7bAI_LtX7lgX269NYzBi4IzjbdZJP8PXus0g" alt=""><figcaption></figcaption></figure>

3. Run the **Flutter Doctor** command once the Flutter is installed. The Flutter Doctor performs the following tasks:
   * Downloads missing files required by the development environment.
   * Ensures we’ve installed the following:
   * Android SDK
   * Apple Xcode (on Mac)
   * Ensures that we’ve agreed to all software development licenses.
   * Checks the Android Studio IDE setup and recommends any changes required to get it working with Flutter.
   * Checks for connected devices.
   * Verifies that Flutter can recognize any connected hardware devices.
   * Recommends any changes required to get them connected and working.
   * Outputs a diagnosis, listing out issues found and recommendations.
4. If you want to run in local Chrome, make sure web security is disabled to avoid CORS errors.&#x20;

Find below the steps to disable the web security of Chrome&#x20;

{% hint style="info" %}
* `Go to the folder where your flutter is added--flutter\bin\cache and remove a file named: flutter_tools.stamp`
* `Go to flutter\packages\flutter_tools\lib\src\web and open the file chrome.dart.`
* `Find '--disable-extensions'`
* `Add '--disable-web-security'`
{% endhint %}

