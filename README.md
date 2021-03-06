# SnapteeSDKExample

iOS Snaptee SDK example project

## iPhone version

1. Design T-shirt with the image from your app

    ![](screenshots/iphone01.PNG)

2. Different color and clothing are available to choose

    ![](screenshots/iphone02.PNG)

3. Order the T-shirt directly in the app

    ![](screenshots/iphone03.PNG)

4. Support Credit Card, Paypal and Alipay (Chinese users)

    ![](screenshots/iphone06.PNG)

## iPad version

1. Design T-shirt with the image from your app
    ![](screenshots/ipad02.png)

2. Different color and clothing are available to choose
    ![](screenshots/ipad03.png)

3. Order the T-shirt directly in the app
    ![](screenshots/ipad04.png)

4. Support Credit Card, Paypal and Alipay (Chinese users)
    ![](screenshots/ipad05.png)


## More screenshots

https://github.com/snaptee/SnapteeSDK-iOS-Example/tree/master/screenshots

## Localization

Snaptee SDK supports the following languages
- English
- Japanese
- French
- German
- Korean
- Thai
- Indonesian
- Simplified Chinese
- Traditional Chinese

## Supported Devices
- iPod, iPhone and iPad
- iOS 6.0 or above

## To install:

#### Working environment
- Latest Xcode
- Deployment Target 6.0 or above
- Please add the following frameworks in "Link Binary With Libraries" in "Build Phases"
   - QuartzCore.framework
   - UIKit.framework
   - Foundation.framework
   - MessageUI.framework
   - libsqlite3.dylib
   - MobileCoreServices.framework
   - CoreGraphics.framework
   - Security.framework
   - SystemConfiguration.framework
![](screenshots/xcode01.png)


#### Snaptee SDK example project
Please download the latest version from https://github.com/snaptee/SnapteeSDK-iOS-Example/releases

**If you are upgrading from older version, make sure that you removed the older library and add all new files to Xcode**


1) Add Snaptee SDK static library to your project (located in SDK example project, "/Frameworks/Snpatee")
- /Assets/
- /include/
- libSnapteeSDKLibrary.a

2) In your app, add the following code to present Snaptee

- Import Snaptee View Controller in your header (.h) and set STViewControllerDelegate
```objc
#import "STViewController.h"
@interface ViewController : UIViewController <STViewControllerDelegate>
@end
```

- Initialize Snaptee View Controller

```objc

    /**
     affiliateId: Assigned by Snaptee
     app_name: Optional. Will be shown in the action sheet when leaving Snaptee e.g. "Back to app_name"
     language: Optional. force SDK to display in a specific language (STLanguageDefault means to use device's language setting)
     */

    [STAffiliateManager instance].affiliateId = @"sdk-demo";
    [STAffiliateManager instance].appName = @"Snaptee SDK Example"; // Optional
    [STAffiliateManager instance].language = STLanguageDefault; // Optional

    /*
     image: UIImage passing to Snaptee
     caption: Optional. Description of the image. Typically entered by users
     */
    STViewController * stViewController = [[STViewController alloc] initWithImage:[UIImage imageNamed:@"sample2.jpg"]
                                                                          caption:@"Funny bear!"];
    [stViewController setST_delegate:self];
    [stViewController setModalPresentationStyle:UIModalPresentationFormSheet];

    [self presentViewController:stViewController animated:YES completion:nil];

```
- Include the following delegate function to dismiss

```objc
- (void)STViewControllerDidFinish:(STViewController *)viewController{
    [viewController dismissViewControllerAnimated:YES completion:nil];
}
```

- Optional delegate functions for your app to track the status
```objc
- (void)STViewControllerDidSaveDesign:(STViewController *)viewController{
    NSLog(@"Snaptee: Design saved!");
}
- (void)STViewControllerWillCheckout:(STViewController *)viewController{
    NSLog(@"Snaptee: Ready to checkout!");
}
- (void)STViewControllerDidCheckout:(STViewController *)viewController
                               item:(STOrderItem*)orderItem{
    NSLog(@"Snaptee: Order completed, order ID = %@", orderItem.orderId);
    NSLog(@"Snaptee: trackingURL = %@", orderItem.trackingURL);
}

```

#### iOS 9 Reminder

Since iOS 9 comes with [App Transport Security](https://developer.apple.com/library/prerelease/ios/technotes/App-Transport-Security-Technote/), you need to add the following to your app's Info.plist to ensure all the images are shown correctly.

```xml
<key>NSAppTransportSecurity</key>
<dict>
	<key>NSExceptionDomains</key>
	<dict>
		<key>d1tb5im0xynh1.cloudfront.net</key>
		<dict>
			<key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
			<false/>
			<key>NSThirdPartyExceptionAllowsInsecureHTTPLoads</key>
			<true/>
		</dict>
		<key>paypal.com</key>
		<dict>
			<key>NSIncludesSubdomains</key>
			<true/>
			<key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
			<false/>
		</dict>
	</dict>
</dict>
```

You may also open the example code to compare the plist file with your owns if you got problem when loading images.

## Make a T-shirt button

It is recommended to use this graphic or text "Make a T-shirt" to start the T-shirt design flow

![](materials/Create-Tshirt@2x.png)

## To test:

- check out with coupon code when using development ID
- coupon code: st_sandbox

## Dashboard:

The following website is the dashboard of the program. You may find statistics inside there.
(Username and password are assigned by Snaptee)

https://snaptee.co/affiliate






