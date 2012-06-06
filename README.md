iOS OTA Buddy
=============

Command line tool to aid in distributing iOS appliactions OTA using the ITMS-protocol (supported by all iOS4 devices and later).

#### Overview
The easiest way to distribute ad-hoc builds is to download them through Safari, this is supported from iOS4. OTA-builds are perfect when you want to distribute to a limited audience, e.g. nightly builds, test builds, debug builds etc.
After building your application archive (.ipa) and signing it with your ad-hoc distribution provisioning profile you some additional steps to enable OTA distribution.

First of all, you need a web-server or dropbox account to put the files. If you want to use Dropbox, simply put your files in the Public folder and right-click to get the public URL.

To download the application from your phone you need an _itms-services_ link that points to a _plist_-file containing some metadata regarding your application. The plist contains (among other things) the URL to the actual application file (.ipa).

To install an ad-hoc application on your device you need to install the provisioning profile used, which also needs to contain your device UUID (see Apple's documentation on this).

This tool will help you extract the provisioning profile used, create the necessary .plist and generate the itms-link.

#### Step by step

##### Setup
1. Build your application archive with Xcode or xcodebuild
2. In Xcode Organizer, select Share, sign your application and save the application.ipa
3. Move the application.ipa and otabuddy.sh file to your distribution folder (on the web-server/dropbox)
4. Enable execution "chmod +x otabuddy.sh"

#### Usage
5. Extract the .mobileprovision to adhoc.mobileprovision by running "./otabuddy provisioning application.ipa adhoc.mobileprovision"
6. Create the .plist file by running "./otabuddy.sh plist application.ipa http://domain.com/path/distribution/application.ipa application.plist"
7. Generate the itms-services link by running "./otabuddy.sh itms http://domain.com/path/distribution/application.plist"
8. Create a HTML-file with an anchor with the itms-link created in step 7 and a link to the provisioning profile extracted in 5.
9. Visit your HTML-file and download your application. Remember to download the provisioning profile first.
10. Enjoy!