# IdxDmpSdk

[![Version](https://img.shields.io/cocoapods/v/IdxDmpSdk.svg?style=flat)](https://cocoapods.org/pods/IdxDmpSdk)
[![License](https://img.shields.io/cocoapods/l/IdxDmpSdk.svg?style=flat)](https://cocoapods.org/pods/IdxDmpSdk)
[![Platform](https://img.shields.io/cocoapods/p/IdxDmpSdk.svg?style=flat)](https://cocoapods.org/pods/IdxDmpSdk)

## Example

To run the example project, clone the repo, and run `pod install` from the Example directory first.

## Requirements

## Installation

IdxDmpSdk is available through [CocoaPods](https://cocoapods.org). To install
it, simply add the following line to your Podfile:

```ruby
pod 'IdxDmpSdk'
```

## Integration DataManagerProvider example

```swift
class ViewController: UIViewController {
    var dmp: DataManagerProvider?
    
    ...

    override func viewDidLoad() {
        super.viewDidLoad()

        self.dmp = DataManagerProvider(providerId: providerId, monitoringLabel: "My app name") {_ in
          // Success callback
        }
    }

    ...
    
    @IBAction func handleShowAd() {
        guard let dmp = self.dmp else {
            return
        }

        let adRequest: GAMRequest = GAMRequest()
        let userId: String = dmp.getUserId() ?? ""

        adRequest.customTargeting = ["dxseg": dmp.getDefinitionIds(), "dxu": userId, "permutive": userId]
    }

    ...
}
```

## Integration DMPWebViewConnector example

```swift
class ViewController: UIViewController {
    var dmpWebViewConnector: DMPWebViewConnector?
    
    ...

    override func viewDidLoad() {
        super.viewDidLoad()
        // You have to set your WKWebView instance
        connector = DMPWebViewConnector(yourWebView.configuration.userContentController)
    }

    ...
    
    @IBAction func handleShowAd() {
        guard let connector = self.connector else {
            return
        }

        let adRequest: GAMRequest = GAMRequest()

        let userId: String = connector?.getUserId() ?? ""
        let defintionsIds: String = connector?.getDefinitionIds() ?? ""

        adRequest.customTargeting = ["dxseg": defintionsIds, "dxu": userId, "permutive": userId]
    }

    ...
}
```

## Author

Brainway LTD, https://brainway.co.il/

## License

IdxDmpSdk is available under the MIT license. See the LICENSE file for more info.
