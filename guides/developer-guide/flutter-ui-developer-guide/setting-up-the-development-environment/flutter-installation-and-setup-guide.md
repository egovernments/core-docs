# Flutter Installation and setup Guide



1. Install flutter in your device&#x20;
   * [Install Flutter](https://docs.flutter.dev/get-started/install) &#x20;
   * [Setup an Editor](https://docs.flutter.dev/get-started/editor)\

2. After installation of flutter, to check the installed version , you can use the command  **flutter --version**

**Note: Version might vary based on the current version used in the project**

<figure><img src="https://lh4.googleusercontent.com/itLJFo7KgDfwn0va0DTnXiTY7fWN2qz-mXuJSq8JYc-l1dFZ5spv9qQbct-HZRHK2n71-BWnuB_94ij5VrXgEdB6ceowF5W7tglDY4TbvCNsBusH2Zq7bAI_LtX7lgX269NYzBi4IzjbdZJP8PXus0g" alt=""><figcaption></figcaption></figure>

3. After installation of flutter, run **flutter doctor** command

&#x20;  The Flutter Doctor performs the following tasks:

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

4. If you want to run in local Chrome, make sure web security is disabled to avoid CORS error. Below are the steps to disable the web security of Chrome&#x20;

* `Go to the folder where your flutter is added--flutter\bin\cache and remove a file named: flutter_tools.stamp`
* `Go to flutter\packages\flutter_tools\lib\src\web and open the file chrome.dart.`
* `Find '--disable-extensions'`
* `Add '--disable-web-security'`

\
