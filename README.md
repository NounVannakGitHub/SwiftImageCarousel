# SwiftImageCarousel
 
SwiftImageCarousel is a UIPageController-based framework that implements scrolling, zooming and automatic swiping carousel in a Swift applicatoion.

All it needs from you is to supply it with valid image URLs and it is good to go. 

## Preview

![](http://i.giphy.com/AetMTdLtlwn72.gif)   

## Features

- Horizontal image swiping that can be pinched and zoomed.
- A timer to make the horizontal image swiping automatic.
- Asynchronous image downloading that does not block the main thread. All you have to do is provide the URLs.
- Customizable page controls appearance (the dot colors and background) -they can be set up through delegate protocol.

## Installation 

### CocoaPods 

[CocoaPods](https://cocoapods.org/) is a dependency manager for Cocoa projects. You can install it with the following command:

```
$ gem install cocoapods
```

To integrate SwiftImageCarousel into your Xcode project using CocoaPods, specify it in your ```Podfile```:

```
source 'https://github.com/Centroida/SwiftImageCarousel.git'

platform :ios, '10.0'
use_frameworks!

target '<Your Target Project Name>' do
pod 'SwiftImageCarousel', '1.0.1'
end

```

### Alternatively:

- Git submodule add https://github.com/Centroida/SwiftImageCarousel.git.
- Drag the SwiftImageCarousel.xcodeproj file into your Xcode project (Xcode will ask to create a workspace file if your project does not have one already)
- Under the main app target, open the General tab and add SwiftImageCarousel under the Embedded Binaries section
- Build the SwiftImageCarousel as a target before you import it
- It is ready to be imported and used

<b>OR</b>

- Download directly from the github link https://github.com/Centroida/SwiftImageCarousel
- Run your project, right click on the name of your project in the files navigator and choose "Add Files to <i>NameOfYourProject</i>"
- Find SwiftImageCarousel.xcodeproj and add it
- Under the main app target, open the General tab and add SwiftImageCarousel under the Embedded Binaries section
- Build the SwiftImageCarousel as a target before you import it
- It is ready to be imported and used

## Usage

### Importing the framework 

```swift
import SwiftImageCarousel
```
### Providing the images as URLs and instantiating a VC with carousel that takes over the screen

Make sure you do this in viewDidAppear(),because it will not work in viewDidLoad().

```swift   
import UIKit
import SwiftImageCarousel

class RandomViewController: UIViewController {
    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)
        let s = UIStoryboard (name: "Main", bundle: Bundle(for: InitialPageViewController.self))
        let vc = s.instantiateInitialViewController() as! InitialPageViewController
        vc.contentImageURLs = [ "<Your First URL>", "<Your Second URL>", "<Your Third URL>"]

        self.present(vc, animated: true, completion: nil)
    }
    
}
```


### Providing the images as URLs and embedding the carousel

```swift
    ///  The UIView declared in Main.Storyboard.
    @IBOutlet weak var containerView: UIView!

    override func viewDidLoad() {
        super.viewDidLoad()

        let s = UIStoryboard (name: "Main", bundle: Bundle(for: InitialPageViewController.self))
        let vc = s.instantiateInitialViewController() as! InitialPageViewController

        vc.contentImageURLs = ["<Your First URL>", "<Your Second URL>", "<Your Third URL>"]

        // Lets add it to container view.
        vc.willMove(toParentViewController: self)
        containerView.addSubview(vc.view)
        vc.view.frame = CGRect(x: 0, y: 0, width: containerView.frame.width, height: containerView.frame.height)
        self.addChildViewController(vc)
        vc.didMove(toParentViewController: self)
    }
```

### Setting up the InitialPageViewControllerDelegate

After you create InitialPageViewController programatically, setup the pageVCDelegate to self:

```swift
       let s = UIStoryboard (name: "Main", bundle: Bundle(for: InitialPageViewController.self))
       let vc = s.instantiateInitialViewController() as! InitialPageViewController
       vc.pageVCDelegate = self
```

And do not forget to add InitialPageViewControllerDelegate as an extention to your custom-class View Controller:

```swift
        extension RandomViewController: InitialPageViewControllerDelegate {} 
```

## SwiftImageCarousel Variable Configuration
  
  -- <b><i>contentImageURLs</i></b> - this is an array of strings (the URls to be provided). It is empty, so you need to provide the string URLs.
 
 -- <b><i>isTimerOn</i></b> - a boolean value defining whether the automatic swiping timer is on. Its default value is TRUE. If you want it off, set it to FALSE.
  
  -- <b><i>swipeTimeIntervalSeconds</i></b> - a DOUBLE integer defining the interval on which the carousel swipes automatically in seconds. Default value is 3 seconds. Set it to whatever you like.
 
 -- <b><i>pageVCDelegate</i></b> - the delegate variable that needs to be set to self, if access to its functions (they are all optional) is needed: 
  - the most important function is: <b><i>setupAppearance</i></b> which helps set up the appearance of the page controls (as its name describes). This is how to implement it:
  Set the delegate to self, and add extension to current view controller of InitialPageViewControllerDelegate to implement the function and notice the change in colors in the first page control.
  
  [![Screen Shot 2017-01-16 at 7.04.42 PM.png](https://s27.postimg.org/lc1aik39v/Screen_Shot_2017_01_16_at_7_04_42_PM.png)](https://postimg.org/image/pl60kq6j3/)
  - <b><i>didStartTimer</i></b> - gives you the timer and its properties in case you need them or you want to change them.
  - <b><i>didGetNextITemController</i></b> gives you the coming pageItemController and its properties when the timer is on.
  - <b><i>didUnwindToPageViewController</i></b> gives you the pageItemController when unwinding from zoomable page view controller.
  
  
## Issues
  
  No issues so far with the framework no matter whether it is used in portrait mode or in landscape mode.
  And this is why we put it up here for everybody to use - we would love you to share comments and give ideas. 
  
## Requirements
  
  SwiftImageCarousel was tested and is working with the latest available version of software - XCode Version 8.2.1 and Swift 3.0.
  
## License

Copyright (c) 2017 Centroida

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

  

