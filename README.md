# iOS Inject Dylib and Resign non-app-store IPA

The resign tool is used to inject a dylib into an development/ad-hoc/enterprise signed ipa.

## Pre-requisite tools
- optool (Is available with xcode install)
- grealpath (install using `brew install coreutils`)
- Plistbuddy (should be available in mac by default)
- Codesign (should be available in mac by default)

## Usage
```bash
$ ./resign sample-config.conf
```
The `sample-config.conf` file contains all of the required paths for the script.

## Config file
```bash
# Path to the ipa file
IPA_PATH="./MyApp.ipa"

# Path to the dylibs directory which contains all of the dylibs to be injected
DYLIBS_PATH="./Dylibs"

# The new bundle-id of the ipa 
NEW_BUNDLE_IDENTIFIER="com.app.new.id"

# The new ipa file name
RESIGNED_IPA_NAME="app-injected-resigned.ipa"

# Path to the entitlements plist for the given provisioning profile
ENTITLEMENTS_PATH="<PATH-TO-ENTITLEMENTS-FILE>.plist"

# Path to the provisioning profile
PROVISIONING_PATH="<PATH-TO-PROVISIONING-FILE>.mobileprovision"

# Code-signing id
CODESIGN_ID="<CODE-SIGNING-ID>"
```

## References - 
- [1](https://coderwall.com/p/qwqpnw/resign-ipa-with-new-cfbundleidentifier-and-certificate) Resigning with new bundle id
- [2](https://stackoverflow.com/a/32274908/1518924) Using entitlements in the code-signing process (this solves the missing application-identifier problem)
- [3](https://github.com/Carthage/Carthage/issues/1401#issuecomment-248618314) Code-signing the frameworks 
- [4](https://stackoverflow.com/a/29932317/1518924) Code-signing the frameworks 
- [5](https://github.com/depoon/iOSDylibInjectionDemo/blob/master/patchapp.sh)Using optool to inject the dylib onto the ipa