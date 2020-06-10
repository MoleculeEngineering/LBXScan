

# iOS QR code, barcode 
[![Platform](https://img.shields.io/badge/platform-iOS-red.svg)](https://developer.apple.com/iphone/index.action)
[![Language](http://img.shields.io/badge/language-OC-yellow.svg?style=flat
             )](https://en.wikipedia.org/wiki/Objective-C)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](http://mit-license.org)
![CocoaPods Version](https://img.shields.io/badge/pod-v2.3-brightgreen.svg)

[swift version click here] (https://github.com/MxABC/swiftScan)

[DIY parameter understanding reference tool click here] (https://github.com/MxABC/LBXScanUITool)

QQ exchange group: 522806629 

-[iOS scan code package] (#iOS scan code package)
-[DIY](#Set parameter custom effect)
-[Imitate other apps] (#Imitate other apps (this can be done by setting parameters))
-[Install] (#Installation with CocoaPods)
-[DIY parameter introduction] (#DIY parameter introduction)
-[Interface Effect] (#Interface Effect)


### iOS scan code package
-Scan code recognition package: System API (AVFoundation), ZXing, ZBar
-Scan code interface effect package
-QR code, barcode
-Recognize after getting pictures in album

### Set parameter custom effect

-The background color of the area around the scanning frame can be set
-Scan code frame color can also be set
-The color and size of the 4 corners of the scanning frame can be set
-It can be set to only recognize the image area in the scan code frame
-Can set the current picture after scanning successfully
-Animation effect selection: the line moves up and down, the grid form moves, and the middle line does not move (the effect of general barcode scanning)

### Imitate other apps (this can be done by setting parameters)
-Imitate the QR code scanning interface
-Alipay scan code frame effect
-Scanning frame effect on WeChat

### historic version
#### 2.3 
-Modify ZXing memory modification bug, improve the memory release after ZXing scan code is completed
-Demo camera and album permission access code optimization
-ZBar modification parameters support ITF-14
-Scan the code to start the camera prompt optimization and place it in the middle position

#### 2.2 
-Downloadable by library (native, ZXing, ZBar)

#### 1.x 
-1.x

### Installation with CocoaPods
> A function can be installed independently, ZXing has been downloaded to this project, solving the problem of slow download speed of the previous version


***
-Install all libraries including UI 

```ruby
 pod'LBXScan','~> 2.3'
```
It is recommended to write in the following group, and group by folder after installation, otherwise all files are in one folder, very messy

```ruby
pod'LBXScan/LBXNative','~> 2.3'
pod'LBXScan/LBXZXing','~> 2.3'
pod'LBXScan/LBXZBar','~> 2.3'
pod'LBXScan/UI','~> 2.3'
```

-Only install the system's native API package library  

```ruby
pod'LBXScan/LBXNative','~> 2.3'
```

-Only install ZXing package library 

```ruby
pod'LBXScan/LBXZXing','~> 2.3'
```

-Only install ZBar package library 

```ruby
pod'LBXScan/LBXZBar','~> 2.3'
```

-Only install UI

```ruby
pod'LBXScan/UI','~> 2.3'
```
-Install any combination

> You can install any combination through the above installation method


### Demo test
-xcode version: xcode9.2
-Download the project and open LBXScanDemo.xcworkspace in DemoTests
-Demo provides tests to select the corresponding library to scan code recognition, album selection picture recognition, generate barcode, etc.

### UI DIY parameter introduction

Please refer to the auxiliary understanding reference tool: [LBXScanUITool](https://github.com/MxABC/LBXScanUITool)


```obj-c
-(LBXScanViewStyle*)DIY
{
//Set the scan code area parameters
LBXScanViewStyle *style = [[LBXScanViewStyle alloc]init];

//The center position of the scan code frame is shifted up by offset pixels from the center position of the View (generally the scan code frame is a little above the center position of the view)
style.centerUpOffset = 44;



//The type of the 4 corners around the scan code frame is set on the top of the frame, and you can modify it to see the effect yourself
style.photoframeAngleStyle = LBXScanViewPhotoframeAngleStyle_On;

//Draw line width at 4 corners around scan code box
style.photoframeLineW = 6;

//Horizontal length of 4 corners around the scanning frame
style.photoframeAngleW = 24;

//Vertical height of 4 corners around the scanning frame
style.photoframeAngleH = 24;


//Animation type: grid form, imitating Alipay
style.anmiationStyle = LBXScanViewAnimationStyle_NetGrid;

//Animated picture: grid picture
style.animationImage = [UIImage imageNamed:@"CodeScan.bundle/qrcode_scan_part_net"];;

//The color of the 4 corners around the scan code box
style.colorAngle = [UIColor colorWithRed:65./255. green:174./255. blue:57./255. alpha:1.0];

//Whether to display the scan code box
style.isNeedShowRetangle = YES;
//Scan code box color
style.colorRetangleLine = [UIColor colorWithRed:247/255. green:202./255. blue:15./255. alpha:1.0];

//The color of the non-scanning code frame area (the color around the scanning code frame, generally darker)
//Must be created by [UIColor colorWithRed: green: blue: alpha:], internally need to be parsed into RGBA
style.notRecoginitonArea = [UIColor colorWithRed:0 green:0 blue:0 alpha:0.6];

return style;
}
```

### Use Scanner Controller LBXScanViewController

If you need to use the provided scan code controller LBXScanViewController (included in the UI module), you need to add the pre-compiled header file xx.pch file in your project or add the corresponding macro in the corresponding call place (LBXScanViewController code contains all Library and UI, so you need to add macros according to the situation of the library you downloaded)

For example, in the current project Demo, PrefixHeader.pch, I downloaded all the modules in my demo, so the macros of each module are defined below

```

#ifdef __OBJC__
#import <Foundation/Foundation.h>
#import <UIKit/UIKit.h>

#define LBXScan_Define_Native //Native module downloaded
#define LBXScan_Define_ZXing //downloaded the ZXing module
#define LBXScan_Define_ZBar //downloaded ZBar module
#define LBXScan_Define_UI //downloaded the interface module
#endif

```

Scanning results processing, you can achieve the delegate method scanResultWithArray or inherit the controller LBXScanViewController, and then override the scanResultWithArray method


# Interface effects
![image](https://github.com/MxABC/Resource/blob/master/scan12.gif)
