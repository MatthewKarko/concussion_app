# How to Run the App

## As a Developer
### Requirements
- All requirements are defined in the expo documentation [here](https://docs.expo.dev/get-started/installation/)
- `npm` is used as the package manager (not `yarn`).
- You will need to ensure that [android studio (with an emulator)](https://docs.expo.dev/workflow/android-studio-emulator/) is setup for running on android.
- Similarly, the ios development [setup guide](https://docs.expo.dev/workflow/ios-simulator/) must be followed.
### Running 
Simply execute `npm run android` or `npm run ios` to launch the app.
## As a User
- An app binary must be installed. Binaries can be found in the [downloads section](https://bitbucket.org/w12-1-capstone/w12_1_capstone/downloads/) of the bitbucket repository.
- Depending on the operating system of your mobile device (IOS or Android), you will need to transfer the corresponding binary file onto the device.
- Currently, only Android apps can install the direct `app.apk` file on mobile devices. This is due to IOS security restrictions (An apple developer account is required for installation)
# Running Tests
Please read below for detail on running both unit and e2e tests.
## Unit Testing
To run unit tests, simple run the command `npm run test`.
## End-to-End Testing
Please read the below information for running e2e tests.

### Dependencies
Please note that all app binaries can be built using the external eas build server, however it is recommended to build these locally.

Both these binaries must be placed in the correct location according to the .detoxrc.json file.
#### IOS (Mac Only)
- For running IOS tests, `applesimutil` needs to be installed.
- A binary `.app` file is required to run the detox tests from.
- A local build can be generated using this command `npx eas-cli build --platform ios --profile preview --non-interactive --local`, however it is highly temperamental and requires the correct versions of dependencies including fastlane, xcode and cocoapods. It is recommendded to try using the latest versions. For example, it seems that xcode 12.4 or below causes errors with fastlane. Refer to this [link](https://docs.expo.dev/build-reference/infrastructure/#image--macos-big-sur-114-xcode-125) for the exact server infrastructure eas servers use. You will need to use a mac os that supports using above xcode 12.4.

#### Android (Windows and Mac)
- 2 binaries are required, a "Test" apk, and the "actual app" apk.
- These binaries can be built locally with the corect setup using the 'debug' and 'preview' profiles in the `eas.json` configuration. 
- A Dockerfile and docker-compose.yml setup has been provided which uses Docker for building the binaries. Once the container has completed the build process, these binaries can be copied from the exited container to the host using the `docker cp` command. The app binary will be named located at `CONTAINER_NAME:/app/android.apk`.
- Running the tests on Android requires using a 64-bit emulator.
- Currently, running android tests are temperamental and not recommended.

### Running the tests
These tests can be run on IOS and android with the following commands, respectively:
- `npm run e2e-ios`
- `npm run e2e-android`

