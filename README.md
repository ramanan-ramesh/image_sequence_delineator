# image_sequence_delineator

[comment]: <> (Introduction)
A simple widget for animating a set of images with full custom controls as an alternative to using a GIF file.

**If you have a GIF file you would like to use with this package, I recommend [EZGIF](https://ezgif.com/split) to convert your GIF file to an image
 sequence.**

**It is highly recommended to read the documentation and run the example project on a real device to fully understand and inspect the full range
 of capabilities.**

[comment]: <> (ToC)
[Media](#media) | [Description](#description) | [How-to-Use](#howtouse)

[comment]: <> (Recent)
## Recent
* **[fullPaths] is added. If you would like to specify a list of endpoints for the frames in your image sequence animator, use this value. If set, values for
  [folderName], [fileName], [suffixStart], [suffixCount], [fileFormat] and [frameCount] will be ignored.**

* **[isOnline] is added. If your [folderName] is an online path, this value should be set to true.**

* **[waitUntilCacheIsComplete] is added. If you want the [ImageSequenceDelineator] to wait until the entire image sequence is cached, this value should be set
  to true i. Otherwise, the [ImageSequenceAnimator] will invoke [onReadyToPlay] and start playing if [isAutoPlay] is set to true when it approximates that the
  remaining caching can be completed without causing stutters. This value is only used if [isOnline] is set to true.**

* **[cacheProgressIndicatorBuilder] is added. If you want to display a widget until the [ImageSequenceDelineator] is ready to be played, use this function.**
* * *

[comment]: <> (Description)
<a name="description"></a>
## Description
This simple widget for animating a set of images **(a.k.a an image sequence)** with full custom controls as an alternative to using a GIF file.

GIF files are, as far as I know, not possible to control. With this package, you will have full control over your image sequence like controlling a
video. You can loop, boomerang, change the color, play, pause, stop, skip, rewind, restart and more.


[comment]: <> (How-to-Use)
<a name="howtouse"></a>
## How-to-Use
First, add your image sequence to your assets and update the "pubspec.yaml" accordingly.

Then create an ImageSequenceDelineator widget as shown in the example:

```
ImageSequenceDelineator(
  "assets/ImageSequences/MyImageSequence",  //folderName
  "Frame_",                                 //fileName
  0,                                        //suffixStart
  5,                                        //suffixCount
  "png",                                    //fileFormat
  60,                                       //frameCount
 {Key key,
  fps               : 60,
  isLooping         : false,
  isBoomerang       : false,
  isAutoPlay        : true,
  color             : Colors.white,
  onReadyToPlay     : _onReadyToPlay,
  onStartPlaying    : _onStartPlaying,
  onPlaying         : _onPlaying,
  onFinishPlaying   : _onFinishPlaying})

ImageSequenceDelineator(
  "https://www.domain.com/ImageSequenceDelineator/MyImageSequence",  //folderName
  "Frame_",                                                 //fileName
  0,                                                        //suffixStart
  5,                                                        //suffixCount
  "png",                                                    //fileFormat
  60,                                                       //frameCount
 {Key key,
  fullPahts         :               [],
  fps               :               60,
  isLooping         :               false,
  isBoomerang       :               false,
  isAutoPlay:                       true,
  isOnline:                         true,
  waitUntilCacheIsComplete:         true,
  cacheProgressIndicatorBuilder:    _cacheProgressIndicatorBuilder,
  color             :               Colors.white,
  onReadyToPlay     :               _onReadyToPlay,
  onStartPlaying    :               _onStartPlaying,
  onPlaying         :               _onPlaying,
  onFinishPlaying   :               _onFinishPlaying})

Widget _cacheProgressIndicatorBuilder(BuildContext _context , double _progress);
void   _onReadyToPlay(ImageSequenceDelineatorState _imageSequenceAnimator);
void   _onStartPlaying(ImageSequenceDelineatorState _imageSequenceAnimator);
void   _onPlaying(ImageSequenceDelineatorState _imageSequenceAnimator);
void   _onFinishPlaying(ImageSequenceDelineatorState _imageSequenceAnimator);
```

**Further Explanations:**

*For a complete set of descriptions for all parameters and methods, see the [documentation](https://pub.dev/documentation/image_sequence_animator/latest/).*

* [isLooping] will override [isBoomerang] if both are set to true.
* All [ImageSequenceProcessCallback] callbacks will return a reference to the created [ImageSequenceAnimator] state. You can save this instance for
 further actions.
* Use [ImageSequenceDelineatorState]'s
[void setIsLooping(bool isLooping)], [void setIsBoomerang(bool isBoomerang)], [void setColor(Color color)], [void play({double from: -1.0})],
[void rewind({double from: -1.0})], [void pause()], [void skip(double value, {double percentage: -1.0})], [void restart()], [void stop()]
methods for the corresponding actions.
* Use [ImageSequenceDelineatorState]'s [bool get isLooping], [bool get isBoomerang], [double get currentProgress], [double get totalProgress],
[double get currentTime] and [double get totalTime] methods to get the respective values.


[comment]: <> (Notes)
## Notes
I started using and learning Flutter only some weeks ago so this package might have some parts that don't make sense, that should be completely
different, that could be much better, etc. Please let me know! Nicely!

Any help, suggestion or criticism is appreciated!

Cheers.