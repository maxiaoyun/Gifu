<img src="https://db.tt/mZ1iMNXO" width="100" />

Adds performant animated GIF support to UIKit, without subclassing `UIImageView`. If you're looking for the Japanese prefecture, click [here](https://goo.gl/maps/CCeAc).

#### Why?

Because Apple's `+animatedImage*` is not meant to be used for animated GIFs (loads all the frames in memory), and the few third party implementations that got it right (see [Credits](#credits)) still require you to use a `UIImageView` subclass, which is not very flexible and might clash with other application-specific functionality.

#### How?

Gifu is a `UIImage` subclass and `UIImageView` extension written in Swift.
It uses `CADisplayLink` to animate the view and only keeps a limited number of
frames in-memory, which exponentially minimizes memory usage for large GIF files (+300
frames).

The figure below summarizes how this works in practice. Given an image
containing 10 frames, Gifu will load the current frame (red), pre-load the next two frames in this example (orange),
and nullify all the other frames to free up memory (gray):

<img src="https://db.tt/ZLfx23hg" width="300" />

#### Install

If you use [Carthage](https://github.com/Carthage/Carthage), add this to your `cartfile`: `github "kaishin/gifu"`.

If your prefer Git submodules or want to support iOS 7, you want to add the files in `source` to your Xcode project.

#### Usage

Call `setAnimatableImage(named:)` or
`setAnimatableImage(data:)` on your `UIImageView` (or its subclass):

```swift
let imageView = UIImageView(...)

imageView.setAnimatableImage(named: "computer-kid.gif")
// imageView.setAnimatableImage(data: NSData(...))
```

The image view will not start animating until you call `startAnimatingGIF()`
on it. You can stop the animation anytime using `stopAnimatingGIF()`, and resume
it using `startAnimatingGIF()`. These methods will fallback to UIKit's `startAnimating()` and `stopAnimating()`
if the image view has no animatable image.

Likewise, the `isAnimatingGIF()` method returns the current animation state of the view if it has an animatable image,
or UIKit's `isAnimating()` otherwise.

#### Demo App

<img src="https://db.tt/ZoUNLHGp" width="300" />

#### Compatibility

- iOS 7+

#### Roadmap

The usual suspects:

- Add documentation.
- Write some basic tests.

Needless to say, you are welcome to contribute.

#### Credits

- The animation technique described above was originally spotted on
[OLImageView](https://github.com/ondalabs/OLImageView), then improved in [YLGIFImage](https://github.com/liyong03/YLGIFImage).

- The font used in the logo is [Azuki](http://www.myfonts.com/fonts/bluevinyl/azuki/)

- Kudos to my colleague [Tony DiPasquale](https://github.com/tonyd256) for helping out with the factory methods.

- The characters used in the icon and example image in the demo are from [Samurai Champloo](https://en.wikipedia.org/wiki/Samurai_Champloo).

#### License

See LICENSE.
