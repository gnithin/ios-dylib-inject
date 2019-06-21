# ios-dylib-inject

The ios-dylib-inject script is used to inject a dylib into a development/ad-hoc/enterprise-signed ipa and resign it with a given provisioning profile and code-signing certificate.

This will not work with app-store ipas.

## Pre-requisite tools
- optool (Is available with xcode install)
- grealpath (install using `brew install coreutils`)
- Plistbuddy (should be available in mac by default)
- Codesign (should be available in mac by default)

## Usage
```bash
$ ./resign sample-config.conf
```
- The `sample-config.conf` file contains all of the required paths for the script
- All of the dylibs should be added into a directory and the directory path must be specified in the config file
- The new ipa will be in the same directory as the original ipa

## Config file
Here are the contents of the config file and their details (NOTE: All the keys are required) -
```bash
# Path to the ipa file. Make sure that app-name and the ipa name are the same.
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

### Miscellaneous help for setting up the config
- Provisioning profile is usually available at path - `~/Library/MobileDevice/Provisioning\ Profiles/`
- The codesigning-id can be fetched by using the command - 
  ```console
  $ security find-identity -v -p codesigning
  ```
  This will list all of the certificates present in the key-chain
- When not sure about the entitlements file, you can create one from the provisioning profile itself
	- Run
    ```console
    $ security cms -D -i "<provisioning-profile>.mobileprovision"
    ```
    - Copy the entire `<dict>` where the `<key>` is `Entitlements`, into a separate file, and wrap that around a `<plist>` tag
    - Refer [this](https://stackoverflow.com/questions/28371652/ios-8-1-3-enterprise-distribution-application-is-missing-the-application-ide/32274908#32274908) in case of issues

NOTE: The certificates(code-signing-id) & provisioning-profile need to be valid and related. This will not work otherwise

## References - 
- [[1](https://coderwall.com/p/qwqpnw/resign-ipa-with-new-cfbundleidentifier-and-certificate)] Resigning with new bundle id
- [[2](https://stackoverflow.com/a/32274908/1518924)] Using entitlements in the code-signing process (this solves the missing application-identifier problem)
- [[3](https://github.com/Carthage/Carthage/issues/1401#issuecomment-248618314)] Code-signing the frameworks 
- [[4](https://stackoverflow.com/a/29932317/1518924)] Code-signing the frameworks 
- [[5](https://github.com/depoon/iOSDylibInjectionDemo/blob/master/patchapp.sh)] Using optool to inject the dylib onto the ipa


## LICENSE 
See LICENSE file 
