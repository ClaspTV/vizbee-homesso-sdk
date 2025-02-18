# VizbeeHomeSSOKit SDK

The VizbeeHomeSSOKit SDK is a wrapper built on top of the Vizbee Continuity SDK, facilitating automatic sign-in capabilities between mobile and TV devices. 

## Enhancing VizbeeHomeSSOKit
1. Navigate to the Project Directory: 
- It should be located in the path `./VizbeeKit/VizbeeHomeSSOKit`

2. Review the Folder Structure: 
- Familiarize yourself with the folder structure to understand where different components of the SDK are located.

3. Understand the Test Structure: 
- Review the structure of the unit tests folder (VizbeeHomeSSOKitUnitTests) and understand the purpose of each file. 
***Note the presence of mocked classes in the MockedClasses subfolder, which are likely used for testing purposes.***

4. Review the Main Code Structure: 
- Explore the VizbeeHomeSSOKit folder to understand the structure of the main SDK code. 
- Pay attention to the various Swift files, including VZBHomeSSOManager.swift, VZBHomeSSOAdapter.swift, VZBHomeSSOHandler.swift, and others. 
- Take note of any subfolders within VizbeeHomeSSOKit and their contents, such as the model folder containing Swift files for defining data models.

5. Understand the Responsibilities of Each Class:
- Read through the code of each Swift file to understand the responsibilities and functionalities of the classes within.

6. Explore Unit Tests:
Review the unit tests provided in the VizbeeHomeSSOKitUnitTests folder to understand how different components of the SDK are tested.
Study how mocked classes are used within the tests, such as MockSignInAdapter.swift, MockEventManager.swift, etc.

7. Set Up Development Environment:
Ensure that you have the necessary development environment set up, including Xcode or any other required tools or dependencies.

8. Make Changes or Fixes:
- Once you have a good understanding of the codebase, you can start making changes or fixes as needed.
- Ensure to follow any existing coding conventions or guidelines established within the project.

9. Run Unit Tests:
- Before committing any changes, run the unit tests to ensure that your modifications haven't introduced any regressions.
- If necessary, update or create additional unit tests to cover new functionality or changes.

10. Commit Changes:
- Once your changes have been tested and verified, commit them to the repository with clear and descriptive commit messages.

11. Submit Pull Request:
- Submit a pull request for your changes to be reviewed by other team members before merging into the develop branch.

##### Below is the breakdown explaining each class and it's responsiblities in short :- 
**VZBHomeSSOManager.swift:**
    This class serves as the main entry point for handling single sign-on (SSO) operations within the Vizbee Home SDK.
    It provides methods for initiating SSO flows.

**VZBHomeSSOAdapter.swift:**
    This protocol defines methods that the application needs to implement to provide information about the user's sign-in status and to receive TV sign-in status updates.
    **getSignedInInfo(callback:):** The application should implement this method to provide the SDK with information about the user sign-in status via the given method.
    **onReceiveTVSignInStatus(_:):** The SDK invokes this method to pass the sign-in status of the TV to the application.

**VZBHSSOConstants.swift:**
    This file contains constants used throughout the SSO functionality, such as keys.
    
**VZBHomeSSOHandler.swift:**
    This class is responsible for handling most of the logic related to single sign-on (SSO) operations within the Vizbee Home SDK.

**model/VZBTVSignInStatus.swift:**
    This class represents the sign-in status of a TV.
    **Properties:**
    **signInType:** A string indicating the type of sign-in.
    **signInState:** An enumeration representing the state of the sign-in process.
    **customData: Optional** custom data associated with the sign-in status.
    
**model/VZBSignInInfo.swift:**
    This class represents sign-in information, including the type of sign-in and whether the user is signed in.
    **Properties:**
    **signInType:** A string indicating the type of sign-in.
    **isSignedIn:** A boolean indicating whether the user is signed in.
    **customData: Optional** custom data associated with the sign-in information.
    
**model/VZBSignInState.swift:**
    This enumeration represents the different states of a sign-in process.
    **Cases:**
    **.signInNotStarted:** Sign-in process has not started.
    **.signInInProgress:** Sign-in process is in progress.
    **.signInCompleted:** Sign-in process completed.
    **.signInFailed:** Sign-in process failed.
    **.signInCancelled:** Sign-in process was cancelled.
    
**VizbeeHomeSSOKitUnitTests/:**
    This directory contains unit tests for the **VizbeeHomeSSOKit**.

**VZBHomeSSOManagerTests.swift:**
    This test class contains unit tests for the **VZBHomeSSOManager** class.
    
**VZBHomeSSOHandlerTests.swift:**
    This test class likely unit tests for the **VZBHomeSSOHandler** class.
    
**MockedClasses/:**
    This directory contains mocked classes used for testing purposes.
    **MockSignInAdapter.swift, MockEventManager.swift, MockSessionManager.swift, MockSession.swift**
    These classes provide mock implementations of dependencies used within the SDK.

## Build & Run 
***Note :- Will work only if Contuity SDK has not been set up properly.***
### Build VizbeeHomeSSOKit
**From XCode**
After all dependencies are installed, open `VizbeeHomeSSOKit.xcworkspace` and select `VizbeeHomeSSOKit` as a target and hit run button from XCode
The latest VizbeeHomeSSOKit framework can be seen in `Products` folder (Which is Debug version)

**From Command Line**

    $ cd ./VizbeeKit
    $ xcodebuild -workspace ./VizbeeKit.xcworkspace  -scheme VizbeeHomeSSOKit -sdk iphonesimulator -destination 'platform=iOS Simulator,id=<device_uuid>' build

### Build & Run SampleApp
**From Xcode:** 
    Open VizbeeKit.xcworkspace, select SampleApp as the target, and hit the run button.

## Testing
### Unit Testing (TODO)
All unit tests are written under target `VizbeeHomeSSOKitUnitTests` and the host application is `VizbeeKitTestsApp`

**Run on simulator:**

    $ xcodebuild -workspace VizbeeKit.xcworkspace -scheme VizbeeHomeSSOKitUnitTests -sdk iphonesimulator -destination 'platform=iOS Simulator,id=68E97908-DD4C-4FE2-9CCA-0C9DDC35326D' clean test | xcpretty

### Manual Testing

1. Launch Xcode and open the project that contains the unit tests you want to run.
2. In the Xcode project navigator, go to .VizbeeKit/VizbeeHomeSSOKitUnitTests
3. Select the target "VizbeeHomeSSOKitUnitTests".
4. With the test target selected, you can run the tests by either:
   a. Clicking the play button (▶️) located next to the test target name.
   b. Choosing Product > Test from the Xcode menu bar.
   c. Pressing Command + U on your keyboard.
5. Xcode will execute the unit tests, and the results will be displayed in the Xcode Test Navigator. You can see which tests passed, failed, or encountered errors

## Build & Publish Debug SDK

Debug version of the VizbeeHomeSSOKit SDK helps to see the logs to find any bugs at initial stages of VizbeeHomeSSOKit integration in any of the customer apps
The following instructions outline the process of publishing VizbeeHomeSSOKit-Debug updates using Cocoapods & Carthage.
### Step 1: Preparing a debug build
1. Update VizbeeHomeSSOKit internal changelog with new version diff: `$ vim ./VizbeeKit/VizbeeHomeSSOKit/ChangeLog.md`

### Step 2: Assembling a debug build
1. Change directory to VizbeeHomeSSOKit `$ cd ./VizbeeKit/VizbeeHomeSSOKit` and execute `build.sh` as in ex. `$ ./build.sh 1.0.0 1 Debug`, which will generate the VizbeeHomeSSOKit.xcframework under `./Vizbeekit/archives/VizbeeHomeSSOKit` folder and moves them to `./VizbeeKit/dist/VizbeeHomeSSOKit` by packaging for different dependency(SPM, Cocoapods, Carthage & Manual) managers to be published.

### Step 3: Publishing to CocoaPods
1. Copy the generated VizbeeHomeSSOKit framework ZIP, `./VizbeeKit/dist/VizbeeHomeSSOKit/CocoaPods/VizbeeHomeSSOKit-1.0.0-1-Debug.zip` to Amazon S3 Vizbee bucket: [Link](https://s3.console.aws.amazon.com/s3/buckets/vizbee/vizbee-homessokit/debug/iOS/Cocoapods/)
2. Configure Vizbee CocoaPod repo. **(First time setup only)** `$ pod repo add vizbeekit-debug https://git.vizbee.tv/Vizbee/Specs.git`
3. Publish PodSpec to Vizbee CocoaPod repo ```$ pod repo push vizbeekit-debug VizbeeHomeSSOKit-Debug.podspec``` from Remote-SDK-iOS/VizbeeKit/VizbeeHomeSSOKit folder.

### Step 4: Publishing to Carthage
1. Copy the archived VizbeeHomeSSOKit.framework ZIP, `./VizbeeKit/dist/VizbeeHomeSSOKit/Carthage/VizbeeHomeSSOKit-1.0.0-Debug-framework.zip` to Amazon S3 Vizbee bucket:  [Link](https://s3.console.aws.amazon.com/s3/buckets/vizbee/vizbee-homessokit/debug/iOS/Carthage)
2. Copy `./VizbeeHomeSSOKit-Debug.json` to Amazon S3 Vizbee bucket: [Link](https://s3.console.aws.amazon.com/s3/buckets/vizbee/vizbee-homessokit/debug/iOS/Carthage) from Remote-SDK-iOS/VizbeeKit/VizbeeHomeSSOKit folder.

### Step 5: Using it in Customer/Demo apps
1. Cocoapods `pod 'VizbeeHomeSSOKit-Debug', '1.0.0'`
2. Carthage `binary "https://s3.console.aws.amazon.com/s3/buckets/vizbee/vizbee-homessokit/debug/iOS/Carthage/VizbeeHomeSSOKit-Debug.json" == 1.0.0`

## Build & Publish Release SDK

VizbeeHomeSSOKit is distributed to clients via CocoaPods, Carthage and manually hosted in Google Drive.
The following instructions outline the process of releasing and publishing VizbeeHomeSSOKit updates.

### Step 1: Preparing  a release build

1. Update VizbeeHomeSSOKit internal changelog with new version diff: `$ vim ./VizbeeKit/VizbeeHomeSSOKit/ChangeLog.md`

### Step 2: Assembling a release build

1. Change directory to VizbeeHomeSSOKit `$ cd ./VizbeeKit/VizbeeHomeSSOKit` and execute `build.sh` as in ex. `$ ./build.sh 1.0.0 1 Release`, which will generate the VizbeeHomeSSOKit.xcframework under `./Vizbeekit/archives/VizbeeHomeSSOKit` folder and moves them to `./VizbeeKit/dist/VizbeeHomeSSOKit` by packaging for different dependency(SPM, Cocoapods, Carthage & Manual) managers to be published.
3. Newly generated VizbeeHomeSSOKit framework will be located in `./VizbeeKit/dist/VizbeeHomeSSOKit`

### Step 3: Publishing to CocoaPods
1. Copy the generated VizbeeKit framework ZIP, `./VizbeeKit/dist/VizbeeHomeSSOKit/CocoaPods/VizbeeHomeSSOKit-1.0.0-1-Release.zip` to Amazon S3 Vizbee bucket: [Link](https://s3.console.aws.amazon.com/s3/buckets/vizbee/vizbee-homessokit/release/iOS/Cocoapods/)
2. Configure Vizbee CocoaPod repo. **(First time setup only)** `$ pod repo add vizbeekit https://git.vizbee.tv/Vizbee/Specs.git`
3. Publish PodSpec to Vizbee CocoaPod repo ```$ pod repo push vizbeekit VizbeeHomeSSOKit.podspec``` from Remote-SDK-iOS/VizbeeKit/VizbeeHomeSSOKit folder.

### Step 4: Publishing to Carthage
1. Copy the archived VizbeeHomeSSOKit.framework ZIP, `./VizbeeKit/dist/VizbeeHomeSSOKit/Carthage/VizbeeHomeSSOKit-1.0.0-framework.zip` to Amazon S3 Vizbee bucket:  [Link](https://s3.console.aws.amazon.com/s3/buckets/vizbee/vizbee-homessokit/release/iOS/Carthage/)
2. Copy `./VizbeeHomeSSOKit.json` to Amazon S3 Vizbee bucket: [Link](https://s3.console.aws.amazon.com/s3/buckets/vizbee/vizbee-homessokit/release/iOS/Carthage/) from Remote-SDK-iOS/VizbeeKit/VizbeeHomeSSOKit folder.

### Step 5: Publishing to Google Drive
1. Copy the archived VizbeeHomeSSOKit.framework ZIP, `./VizbeeKit/dist/Manual/VizbeeHomeSSOKit-1.0.0-1-Release.zip`  to Google Drive : [Link](https://drive.google.com/drive/u/0/folders/1_G2NDYZnPbQ5WwXPRS1blKzs-5vWWPwi)
2. Move the previous VizbeeHomeSSOKit-X.X.X-framework.zip into the Archive/VizbeeHomeSSOKit folder of Google Drive.

### Step 6: Publishing to Swift Package Manager
1. Checkout the repo https://github.com/ClaspTV/vizbee-homesso-sdk.git
3. Replace `VizbeeHomeSSOKit.xcframework` in `vizbee-homesso-sdk` with `/VizbeeKit/dist/VizbeeHomeSSOKit/SPM/VizbeeHomeSSOKit.xcframework`
4. Commit and Push the changes to master repo of vizbee-ios-sdk
5. Create a tag and push to remote
        ```
        git tag 1.0.0
        git push --tags
        ```
        
### Step 7: Tagging release - TBD
1. Check in all updated version files to GIT: `.plists`, `VizbeeHomeSSOKit.podspec`, `VizbeeHomeSSOKit.json`, and `ChangeLog.md`
2. Tag release: `$ git tag v1.0.0-homesso-sdk`
3. Merge changes into `develop` and `master` branches
4. Push to remote repository: `$ git push origin master develop --tags`

### Step 8: Updating Demo apps - TODO
[//]: # (1. Update both Vizbee Demo apps with the newly publish SDK.)
[//]: # (2. Check in SDK update changes to master branch and push to remote repo)
[//]: # (3. Archive demo app source code:)

### Step 9: Updating Vizbee Console with new release
1. Update public release notes.
2. Update iOS integration guides with new version.
