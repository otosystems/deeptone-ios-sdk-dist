<p align="center">
  <a href="#requirements">Requirements</a> • <a href="#getting-started">Getting Started</a> • <a href="#installation">Installation</a> • <a href="#api-reference">API Reference</a>
</p>

## Requirements

- iOS 11.0+
- Xcode 11.2+
- Swift 5.0+

## Getting Started

First import __DeeptoneSDK__:

```swift
import DeeptoneSDK
```

```swift
let filePath = Bundle.main.path(forResource: "YourModel", ofType: "model")
let deeptone = try! Deeptone(modelPath: filePath!)

let audioFile = Bundle.main.path(forResource: "Your4SecsAudioFile", ofType: ".m4a")
let data: DeeptoneOutput = try! deeptone.loadAudioFile(filePath: audioFile!)
```

## Installation

The recommended approach to use _DeeptoneSDK_ in your project is using the [CocoaPods](http://cocoapods.org/) package manager, as it provides flexible dependency management and dead simple installation.

### CocoaPods

Install CocoaPods if not already available:

``` bash
$ [sudo] gem install cocoapods
$ pod setup
```
Go to the directory of your Xcode project, and Create and Edit your Podfile and add _DeeptoneSDK_:

``` bash
$ cd /path/to/MyProject
$ pod init
$ edit Podfile
# Uncomment the next line to define a global platform for your project
# platform :ios, '9.0'

target 'MyProject' do
  # Comment the next line if you don't want to use dynamic frameworks
  use_frameworks!

  # Pods for MyProject
  pod 'DeeptoneSDK', '~> 0.1'
end
```

Install into your project:

``` bash
$ pod install
```

If CocoaPods did not find any of _DeeptoneSDK_ dependencies execute this command:

```bash
$ pod repo update
```

Open your project in Xcode from the .xcworkspace file (not the usual project file)

``` bash
$ open MyProject.xcworkspace
```

## [API Reference](https://otosystems.github.io/deeptone-ios-sdk-dist)
