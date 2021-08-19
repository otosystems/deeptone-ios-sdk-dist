<p align="center">
  <a href="#requirements">Requirements</a> • <a href="#getting-started">Getting Started</a> • <a href="#installation">Installation</a> • <a href="#api-reference">API Reference</a>
</p>

## Requirements

-   iOS 11.0+
-   Xcode 12.0
-   Swift 5.3

## Getting Started

First import **DeeptoneSDK**:

```swift
import DeeptoneSDK
```

```swift
let KEY = "YOUR_LICENSE_KEY"
let filePath = Bundle.main.path(forResource: "YourModel", ofType: "model")
let deeptone = Deeptone(key: KEY, modelPath: filePath!)

deeptone.start() { result in
    switch (result) {
    case Result.Success:
        print("SDK is ready!")
    case Result.Failure(let error):
        print("Something went wrong! Error: ", error)
    }
}

...
// Get predictions from file
let audioFile = Bundle.main.path(forResource: "YourAudioFile", ofType: ".m4a")
let data: DeeptoneOutput = try! deeptone.loadAudioFile(filePath: audioFile!)


// Get predictions from the microphone
var deeptoneStream: DeeptoneStream?
...
func startRecording() {
        deeptoneStream = self.deeptone.stream(
                onData: { (data: DeeptoneOutput) in
                    // Handle data over time
                },
                onSuccess: { (data: DeeptoneOutput) in
                    // Handle data at the end of the stream
                },
                onError: { (error: DeeptoneSDKError) in
                    //  Handle errors
                })

        let input = self.audioEngine.inputNode
        let format = input.inputFormat(forBus: 0)

        input.installTap(onBus: 0, bufferSize: 8192, format: format, block: { (buf, when) in
            self.deeptoneStream?.write(audioBuffer: buf)
        })

        self.audioEngine.prepare()
        do {
            try self.audioEngine.start()
        } catch {
            debugPrint("BOOM!")
        }
    }

    func stopRecording () {
        guard let deeptoneStream = self.deeptoneStream else {
            return
        }

        deeptoneStream.close()
        self.audioEngine.inputNode.removeTap(onBus: 0)
        self.audioEngine.stop()
        self.audioEngine.reset()
    }
...
```

## API Reference

Please refer to the [documentation](https://otosystems.github.io/deeptone-ios-sdk-dist) for further details on types.

## Installation

The recommended approach to use _DeeptoneSDK_ in your project is using the [CocoaPods](http://cocoapods.org/) package manager, as it provides flexible dependency management and dead simple installation.

### CocoaPods

Install CocoaPods if not already available:

```bash
$ [sudo] gem install cocoapods
$ pod setup
```

Go to the directory of your Xcode project, and Create and Edit your Podfile and add _DeeptoneSDK_:

```bash
$ cd /path/to/MyProject
$ pod init
$ edit Podfile
# Uncomment the next line to define a global platform for your project
# platform :ios, '11.0'

target 'MyProject' do
  # Comment the next line if you don't want to use dynamic frameworks
  use_frameworks!

  # Pods for MyProject
  pod 'DeeptoneSDK', '~> 1.5.0'
end
```

Install into your project:

```bash
$ pod install
```

If CocoaPods did not find any of _DeeptoneSDK_ dependencies execute this command:

```bash
$ pod repo update
```

Open your project in Xcode from the .xcworkspace file (not the usual project file)

```bash
$ open MyProject.xcworkspace
```

*** 

**[Open Source Software & Licenses](https://github.com/otosystems/ossnotice/blob/master/NOTICE.md)**
