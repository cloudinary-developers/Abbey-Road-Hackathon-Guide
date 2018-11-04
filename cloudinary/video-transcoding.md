# Video Transcoding

![Video transcoding and manipulation](https://res.cloudinary.com/cloudinary/image/upload/w_500/v1441199857/video_transcoding_manipulation.jpg)

Videos are becoming more prolific with people having the capability to capture videos with a wide variety of cameras, including smartphone cameras that are available almost everywhere. Web and mobile applications that display videos online can be faced with a challenge when the videos are created or uploaded from different devices and in various formats, and then need to be delivered in **a multitude of resolutions and aspect ratios to various web browsers, laptops and all kinds of mobile devices** in HTML5 web friendly video formats.

On top of that, the videos may need to be further manipulated to fit the graphic design of the web application, whether that entails cropping, resizing, rotating, trimming, adding overlays, or even applying filters and various effects.

Developing and then supporting the backend required to transform videos from hi-res originals to HTML5 web friendly video formats that fit the graphic design of your application is a non-trivial technical process that requires considerable computational power. There are also many advanced tuning properties related to video encoding in the trade off between visual quality and file size, and doing this correctly can save a lot of bandwidth and load videos faster. Many developers spend considerable time building in-house solutions to support online videos.

Cloudinary offers a solution to all your development needs with:

* No need to install any complex software - **all video processing takes place in the cloud**, together with an Interactive Media Library for browsing through your media files and SDKs for all popular web and mobile development frameworks for easy integration with HTML5 sites and mobile apps.
* No need to learn how to fine tune video creation - all the best practices are already automatically applied with conversion to all formats **\(MP4, WebM, OGV, FLV\)** for optimized viewing on all web browsers and mobile devices, improving your website's loading speed while reducing your bandwidth requirements and IT costs.
* No need to write complex code for video processing - all code is already available as a service with a URL based API for video transcoding and manipulation.
* No need to deploy servers for video processing - it's a hosted solution.
* No need to pre-generate all video manipulations - video transformations are done on the fly, streamed via a CDN.

## Cloud-based video manipulation

Manipulating videos to fit the graphic design of the web application doesn't need to be complicated and hard to implement even if the video needs to be delivered in different sizes, formats and resolutions while supporting all the different web browsers, laptops and mobile devices. Cloudinary's rich set of video manipulation capabilities include: [resizing and cropping](https://cloudinary.com/documentation/video_manipulation_and_delivery#resizing_and_cropping_videos), [rotating](https://cloudinary.com/documentation/video_manipulation_and_delivery#rotating_videos), modifying [quality](https://cloudinary.com/documentation/video_manipulation_and_delivery#quality_control), adjusting [video codec settings](https://cloudinary.com/documentation/video_manipulation_and_delivery#video_codec_settings), controlling [bit rate](https://cloudinary.com/documentation/video_manipulation_and_delivery#bit_rate_control), [video trimming](https://cloudinary.com/documentation/video_manipulation_and_delivery#trimming_videos), [thumbnail generation](https://cloudinary.com/documentation/video_manipulation_and_delivery#generating_video_thumbnails), [conversion to animated GIF](https://cloudinary.com/documentation/video_manipulation_and_delivery#creating_animated_gifs), adding [text](https://cloudinary.com/documentation/video_manipulation_and_delivery#adding_text_captions), [image](https://cloudinary.com/documentation/video_manipulation_and_delivery#adding_image_overlays) and [video](https://cloudinary.com/documentation/video_manipulation_and_delivery#adding_video_overlays) overlays, [special effects](https://cloudinary.com/documentation/video_manipulation_and_delivery#video_effects) and lots [more](https://cloudinary.com/documentation/video_manipulation_and_delivery#video_transformations_reference). Videos are delivered using dynamic URLs with on-the-fly transcoding and real-time manipulation while streaming the video content via a worldwide CDN with streaming support for the best performance.

The following are some examples of manipulating a video called `funny_dog` that was uploaded to Cloudinary.

**NodeJS:**

```text
cloudinary.video("funny_dog")
```

### Video resizing and cropping

Resize the video to a width of 200 pixels and a height of 150 pixels using the `fill` cropping mode and focusing on the bottom of the video in the case that only a portion of the video is used:

**NodeJS:**

```text
cloudinary.video("funny_dog", {width: 200, height: 150, gravity: "south", crop: "fill"})
```

[funny\_dog.mp4 resized to 200x150 with fill and south gravity](https://res.cloudinary.com/demo/video/upload/w_200,h_150,c_fill,g_south/funny_dog.mp4)

Resize the video to a width of 300 pixels and a height of 200 pixels using the `pad` cropping mode and use a blue background in the case that the video needs padding:

**NodeJS:**

```text
cloudinary.video("funny_dog", {width: 300, height: 200, background: "#0e4167", crop: "pad"})
```

### Video overlays, trimming, transcoding and more

Scale the width to 300 pixels, the height to 200 pixels, set the quality to 40 and add an overlay saying "Funny Dog" in Roboto 30px white text starting at the 3 second mark and 10 pixels from the bottom of the video:

Transcode the video to the `webm` format and apply the best codec settings for web viewing with the `vc_auto` parameter, add the `cloudinary_icon` image overlay with a width of 160 pixels and 10 pixels from the northeast corner with a brightness of 200% and an opacity of 70%, and adjust the total width to 350 pixels and the height to 150 pixels while padding with a blue background:

**NodeJS**

```text
cloudinary.video("funny_dog", {transformation: [
  {width: 300, height: 200, quality: 40, crop: "scale"},
  {overlay: "text:Roboto_30px_bold:Funny%20Dog", color: "white", gravity: "south", y: 10, start_offset: "3"}
  ]})
```

[funny\_dog.mp4 padded to 350x150 and transcoded to webm with an overlay](https://res.cloudinary.com/demo/video/upload/vc_auto/l_cloudinary_icon,g_north_east,e_brightness:200,o_70,x_10,y_10,w_160/w_350,h_150,c_pad,b_rgb:0e4167/funny_dog.webm)

There are plenty of additional video and image manipulation options that you can choose from, we have only shown a few here to give a small taste of how easy it is to manipulate your videos. See our [video documentation](https://cloudinary.com/documentation/video_manipulation_and_delivery) for more details and examples.

## Creating an image thumbnail from a video

You can also easily create image thumbnails of any frame in a video and then apply any of Cloudinary's [image transformations](https://github.com/cloudinary-developers/canadian-music-week-hackathon-guide-/tree/39a9b1c59498323c6876cd302c24ff20894ab40f/documentation/image_transformations/README.md) to the result. For example, to create an image thumbnail of the frame at 1 second in the `funny_dog` video in JPG format, scaled to a width of 250 pixels and a height of 150 pixels:

![jpg created from funny\_dog.mp4 scaled to 250x150](https://res.cloudinary.com/demo/video/upload/w_250,h_150,c_scale,so_1/funny_dog.jpg)

To create a circular 300x300 sharpened image thumbnail in JPG format of the frame at the 15% mark of the `funny_dog` video, and then adding the `cloudinary_icon` image overlay with a north gravity and resizing to a width of 50% of the total image with 40% opacity:

![Sharpened, rounded jpg created from the frame at 15% of funny\_dog.mp4 filled to 300x300 with an overlay](https://res.cloudinary.com/demo/video/upload/w_300,h_300,c_fill,r_max,e_sharpen,so_15p/l_cloudinary_icon,w_0.5,fl_relative,o_40,g_north/funny_dog.jpg)

## Summary

Video uploading and delivery has become more and more popular and developers face a significant challenge handling these video files for embedding in their web and mobile apps while maintaining complex clusters to handle video uploading and transcoding. Cloudinary eliminates all the R&D work involved, and with a single line of code videos are uploaded to the cloud, and then with dynamic URLs, videos are automatically converted to all required video formats and manipulated to fit the graphic design of web applications and the various devices and resolutions.

The video manipulation features are available to all our free and paid plans. If you don't have a Cloudinary account, you are welcome to [sign up to our free account](https://cloudinary.com/signup) and try it out.

