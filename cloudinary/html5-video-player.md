# HTML5 Video Player

![HTML5 video player](https://res.cloudinary.com/cloudinary/image/upload/w_500/html5_video_player.png)

Once upon a time, in long forgotten browser versions, getting a video into a website required creating and embedding Flash resources. But these days, all modern browsers support HTML5, including the HTML5 `<video>` tag, which means you’ve got a built-in video player that anyone can use.

At first glance, the default HTML5 video player may not look like a fairy tale come true, but the built-in functionality packs more value than you might think. Even if you need more than what the `<video>` tag gives you out-of-the box, you can always use a bit of CSS and Javascript to build on top of the `<video>` tag to enhance and customize it to your heart’s content.

To complement the options available with the HTML5 video tag, Cloudinary offers a set of video transcoding and transformation capabilities, with all processing done in the cloud. The resulting output can be delivered on-the-fly, or you can prepare your video transformations eagerly beforehand, to ensure fast delivery even to the first user.

When you use the HTML5 video player together with Cloudinary’s video functionality, you’ll see that you can do some pretty cool things with very minimal code or time investment.

## What’s in an HTML5 video tag?

Many websites embed proprietary video players with a variety of bells and whistles, but in many cases, the basic HTML5 `<video>` tag provides everything you need to deliver videos as part of your website content. For example, completely whistle-free HTML5 video player code, enables you to:

* Specify the width and height of the player.
* Display or hide the video controls, including play/pause, volume, full-screen toggle, and seek slider.
* Set a poster image to display while the video is downloading or not playing.
* Provide a set of videos in different formats, so that each browser can play a format it supports.
* Include closed-caption subtitles or captions in multiple languages \(great for SEO!\).
* Tell the browser whether to start downloading the video when the page loads or only when the user presses **Play**.
* Control whether to automatically play the video as soon as it’s ready.
* Decide whether to play once or in a loop.
* Indicate if you’d like to play the video without sound \(muted\). For example, Facebook does this when it autoplays videos.

The following simple HTML renders a 640x480 video player with video controls. Each browser will select the video file with the most appropriate format for it \(`webm`, `mp4`, or `ogv`\). Because subtitle tracks were provided, the video controls include a closed-captioning list of languages.

```markup
<video width="640" height="480" poster="CloudinaryTales.jpg" controls>
 <source src="CloudinaryTales.webm" type="video/webm">
 <source src="CloudinaryTales.ogv" type="video/ogg">
 <source src="CloudinaryTales.mp4" type="video/mp4">
 <track src="subtitles-en.vtt" kind="subtitles" srclang="en" 
        label="English" default>
 <track src="subtitles-fr.vtt" kind="subtitles" srclang="fr"
        label="French">
</video>
```

You can find more details about the `<video>` tag on the [w3schools](http://www.w3schools.com/tags/tag_video.asp) website.

## Transforming and transcoding to a glass slipper fit

So now you know how easy it is to fit an HTML5 video player into your Web page.

But what about preparing and optimizing your video content fit your player?

What good is a glass slipper, if Cinderella’s foot doesn’t fit?

In other words, if your videos, or the videos your users upload, are the wrong format or wrong size for your site’s art design, if they are too heavy or too long to download, or they otherwise fail to deliver the impact needed to capture the attention of your users and keep them watching, then that convenient HTML5 video player just isn’t enough.

### Formats, formats, formats

To start with, the video that you or your users want to upload, might not even be a standard Web format. Even if it is, you should have your movies available in [WebM](https://en.wikipedia.org/wiki/WebM), [Ogg \(aka Theora\)](https://en.wikipedia.org/wiki/Theora), and [MP4](https://en.wikipedia.org/wiki/MPEG-4_Part_14) formats, to ensure that the optimal format is delivered for each browser.

Cloudinary enables you to easily [transcode your videos](https://cloudinary.com/documentation/video_manipulation_and_delivery#transcoding_videos) from a long list of possible video input formats \(including non-Web formats\) to all the three of the formats mentioned above. The transcoding is performed on the cloud, with no need to install any video processing software. You can transcode and deliver on-the-fly, or eagerly during the upload process. All you need to do to transcode a video to a single format on-the-fly, is to deliver it with the new format as the extension type. For example:

![thumb: w\_400, with\_code: false](https://res.cloudinary.com/demo/video/upload/dog.webm)

The easiest way to transcode to multiple formats is to use the `cl_video_tag` SDK method in your code. For example, this tiny line of code:

### ruby

```text
cl_video_tag("dog")
```

### php

```text
cl_video_tag("dog")
```

### python

```text
CloudinaryVideo("dog").video()
```

### nodejs

```text
cloudinary.video("dog")
```

### java

```text
cloudinary.url().videoTag("dog")
```

### jquery

```text
$.cloudinary.video("dog")
```

automatically generates an entire `<video>` HTML snippet, including automatically generating the `<source>` URLs for transcoding to all three formats. And it always puts the WebM format first, since that format generally produces smaller formats, so that browsers that support it, will always deliver the smaller format.

More details about this tag [below](html5-video-player.md#all_for_one_and_one_for_all).

When you transcode video on-the-fly, the conversion may take some time the first time a user accesses it, but all subsequent requests to the same URL are delivered quickly via the CDN cache. To avoid the lag time even for your first viewer, use [eager transformations](https://cloudinary.com/documentation/upload_videos#eager_video_transformations) to prepare your content as part of the upload process.

### Optimize your HTML5 video for quick delivery

Many videos are recorded at very high quality. And especially if your site includes user-generated video content where the original quality is outside your control, it’s important to make sure you will be able to deliver those videos at an acceptable size and speed.

Delivering in the right file format and via CDN, as described in the previous section, already goes a long way towards improving delivery times. Furthermore, when Cloudinary transcodes or transforms any video, it also automatically optimizes the video for optimal Web viewing, using best practices for quality, bitrate, codecs, and more.

But, if you still want to cut the file size of the delivered video, there are lots of other steps you can take.

To control the physical size of videos uploaded to your site, you can use resize or crop the video as an [eager transformation](https://cloudinary.com/documentation/upload_videos#eager_video_transformations) to ensure that the videos your users upload will not exceed a maximum physical size.

For example, even if users watch your videos in full screen size, a 1280X720 frame size is generally plenty for most purposes. So, you can limit videos to this maximum size with an upload command such as the following:

### ruby

```text
Cloudinary::Uploader.upload("my_video.mp4",:resource_type => :video,
  :eager =>   { :width => 1280, :height => 720, :crop => :scale })
```

You can also take advantage of eager cropping transformations to resize videos if users upload videos with aspect ratios different than that of the video player you want to include.

When relevant, you can limit the video length by [trimming long videos](https://cloudinary.com/documentation/video_manipulation_and_delivery#trimming_videos) to a certain duration of time, using the `duration` parameter.

In some cases, adjusting the [quality](http://video_manipulation_and_delivery/#quality_control) and [bitrate](https://cloudinary.com/documentation/video_manipulation_and_delivery#bit_rate_control) settings can also decrease file size without having a significant impact on the visually perceived quality. For example:

_**Changing the quality of an uploaded 9.8 MB mp4 video to 50, or changing the bitrate to 500 kilobits reduced the file size of**_ [_**this video**_](https://cloudinary.com/documentation/video_manipulation_and_delivery#quality_control) _**to around 1 MB.**_

For videos that you are delivering in their original format, and with no other custom transformations, you can set the `video_codec` to `auto`, to normalize and optimize the video for web, including the audio settings.  
Alternatively, you can [manually select the video\_codec settings](https://cloudinary.com/documentation/video_manipulation_and_delivery#video_codec_settings).

### Capturing your audience

It’s often the little things that make the difference. You want to make sure you grab your audience’s attention and get them to press that play button. And of-course you want them to keep watching after they start.

#### Grand opening

The HTML5 video player supports displaying an initial poster image, to hint to users what the video’s all about while it’s downloading or before they play it, but where does that image come from?

An easy way is to have Cloudinary automatically generate an image from a frame in your video. By default, it takes the middle frame, but you can select any other frame by specifying an offset time. You can also select any other image in your Cloudinary image library to act as your opening poster image.

Whatever image you choose, you can apply any [image transformations](https://cloudinary.com/documentation/image_transformations) you want; you can zoom in, add special effects or artistic filters, overlays, and much more.

For example, for the poster image below, we use second 0:36 of this cool Edinburgh time lapse video by [Betsy Weber](https://www.flickr.com/photos/betsyweber/22461144502/), and we overlay a transparent movie curtain .png file along with some text.

### ruby

```text
:poster => { :transformation => 
    [ { :width => 1850, :crop => "scale" },
      { :overlay=>"movie_curtain_overlay_new"},
      { :overlay=>"text:Courier_80_bold:Once%20upon%20a%20time...", 
         :gravity=>"north", :y=>60 },
      { :start_offset=>36 } ] }
```

![Poster image for HTML5 video player](https://res.cloudinary.com/demo/video/upload/c_scale,w_1850/l_movie_curtain_overlay_new/l_text:Courier_80_bold:Once%20upon%20a%20time...,g_north,y_60/so_36/w_1400/castle_timelapse.jpg)

#### Thickening the plot

That opening image is just the start of the fun. There are many things you can do with the video itself, depending on your video’s purpose and audience. Here are just a few examples of what’s possible, with a single line of code:

* Apply improvement effects to your video to adjust contrast or saturation.
* Add fade in and fade out effects.
* Display the video with rounded corners, or even as a circle or oval. Or show the video with a vignette effect.
* Add overlays at specified times and locations. For example, you could add callouts to a video demonstration without the need to edit the original video.
* Overlay video on video, such as a sign-language interpreter or a narrator for a demo.
* Rotate a video; not only 90 degrees to allow for portrait videos, but to any angle you please.
* Concatenate two videos, for example to include an advertisement at the start.
* Accelerate or decelerate the play speed.

If you are accepting video uploads from users, you may want to consider defining the transformations in an [upload preset](https://cloudinary.com/documentation/upload_videos#upload_presets), making it easier to apply your selected effects to all incoming videos.

Or you might want to allow your users to select from a list of effects, and you can apply the selected options as eager transformations, upon upload.

### All for one and one for all

We’ve described a lot of things you can do with your video using Cloudinary upload and transformation functionality, and we’ve shown you how you can then play your masterpiece in the built-in video player, using the `<video>` tag.

We already hinted earlier about the `cl_video_tag` SDK helper method, which you can use to automatically generate a `<video>` HTML snippet. So let’s show you how it’s done, and how you can actually include almost everything we’ve talked about so far, inside a single `cl_video_tag`.

The `cl_video_tag` is can be used in all supported SDK frameworks \(Ruby, PHP, Javascript, Python, Node.js, .NET, and more\). The basic syntax \(shown here in Ruby\) is:

```ruby
cl_video_tag(public_id, options = {})
```

Where the `public_id` is the name of a video that has been uploaded to your Cloudinary account, and the `options` include a bunch of optional settings, such as:

* Formats to include for the `<video>` sources \(default webm, mp4 and ogv\).
* A poster image \(default = middle frame\), and any transformations to apply on that image.
* Any transformations you want to apply to the transformed video.
* fallback text content for \(ancient\) browsers that don’t support any of the output source formats.
* any attribute of the HTML5 `<video>` tag \(to customize those player options we mentioned [earlier in this article](html5-video-player.md#what_s_in_an_html5_video_tag)\).

As we mentioned previously, the `cl_video_tag` method call can look as simple as this:

```text
|ruby
cl_video_tag("castle_timelapse")

|php
cl_video_tag("castle_timelapse")

|python
CloudinaryVideo("castle_timelapse").video()

|nodejs
cloudinary.video("castle_timelapse")

|java
cloudinary.url().videoTag("castle_timelapse")

|jquery
$.cloudinary.video("castle_timelapse")
```

That one little line of code, applying default values, generates this:

```markup
<video 
  poster="https://res.cloudinary.com/demo/video/upload/castle_timelapse.jpg">  
  <source 
    src="https://res.cloudinary.com/demo/image/upload/castle_timelapse.webm" 
    type="video/webm"/>  
  <source 
    src="https://res.cloudinary.com/demo/image/upload/castle_timelapse.mp4" 
    type="video/mp4"/>  
  <source 
    src="https://res.cloudinary.com/demo/image/upload/castle_timelapse.ogv" 
    type="video/ogg"/>  
</video>
```

But as you saw from the list of options above, you can really go all out with this tag.

In the following example:

* We use the custom poster image we talked about [earlier in this post](html5-video-player.md#grand_opening), for a theatrical opening.
* We set our timelapse video to `loop`, for those who want to enjoy more than one sunrise and sunset.
* We `crop` the video to `640`x`480` \(4:3 aspect ratio\) using the `pad` method, so that one size video player can host videos uploaded in both 4:3 and 16:9 ratios.
* We lower the `quality` to `70`, which decreases the file size from 17.5 MB to 8.2 MB.
* We shorten the `duration` of the video to `60` seconds, resulting in a 2.9 MB file.
* We add a **fade-in effect**.
* We add a little princess `overlay` to our castle video for some extra cuteness points.
* And of-course by default, we still get the video player `controls` and video output in all `three formats`.

### ruby

```text
cl_video_tag("castle_timelapse.mp4",  
  :loop => true, 
  :poster => { :transformation => 
    [ { :width => 1850, :crop => "scale" },
      { :overlay=>"movie_curtain_overlay_new"},
      { :overlay=>"text:Courier_80_bold:Once%20upon%20a%20time...", 
         :gravity=>"north", :y=>60 },
      { :start_offset=>36 } ] },
  :transformation => [  
    { :crop=>"pad", :height=>480, :width=>640, :quality=>70, 
       :duration=>"60", :effect=>"fade:4000" },  
    { :overlay=>"princess_small", :height=>100, :start_offset=>"0.5", 
      :gravity=>"west", :y=>80}  
    ])
```

Here’s the `<video>` tag it generates:

### html

```text
<video controls="controls" height="360" loop poster="https://res.cloudinary.com/demo/video/upload/c_scale,w_1850/l_movie_curtain_overlay_new/l_text:Courier_80_bold:Once%20upon%20a%20time...,g_north,y_60/so_36/castle_timelapse.jpg" preload="none" style="margin: 0 auto;display: block" width="640">

  <source src="https://res.cloudinary.com/demo/video/upload/c_pad,h_480,w_640,q_70,du_60,e_fade:4000/l_princess_small,h_100,so_0.5,g_west,y_80/castle_timelapse.webm" type="video/webm" />

 <source src="https://res.cloudinary.com/demo/video/upload/c_pad,h_480,w_640,q_70,du_60,e_fade:4000/l_princess_small,h_100,so_0.5,g_west,y_80/castle_timelapse.mp4" type="video/mp4" />

  <source src="https://res.cloudinary.com/demo/video/upload/c_pad,h_480,w_640,q_70,du_60,e_fade:4000/l_princess_small,h_100,so_0.5,g_west,y_80/castle_timelapse.ogv" type="video/ogg" />

</video>
```

And here’s the final video. Grab the popcorn!

```text
<video controls="controls" height="360" loop poster="https://res.cloudinary.com/demo/video/upload/c_scale,w_1850/l_movie_curtain_overlay_new/l_text:Courier_80_bold:Once%20upon%20a%20time...,g_north,y_60/so_36/castle_timelapse.jpg" 
preload="none" 
style="margin: 0 auto;display: block" width="640">
<source src="https://res.cloudinary.com/demo/video/upload/c_pad,h_480,w_640,q_70,du_60,e_fade:4000/l_princess_small,h_100,so_0.5,g_west,y_80/castle_timelapse.webm" type="video/webm" /> </source>
<source src="https://res.cloudinary.com/demo/video/upload/c_pad,h_480,w_640,q_70,du_60,e_fade:4000/l_princess_small,h_100,so_0.5,g_west,y_80/castle_timelapse.mp4" type="video/mp4" /></source>  
<source src="https://res.cloudinary.com/demo/video/upload/c_pad,h_480,w_640,q_70,du_60,e_fade:4000/l_princess_small,h_100,so_0.5,g_west,y_80/castle_timelapse.ogv" type="video/ogg" /></source></video>
```

## Adding a few more magic touches to your Video Player

While every modern browser provides a media player for the `<video>` tag with the main features we talked about above, each browser’s player looks a bit different. If you want to ensure a consistent look and feel of your browser, or if you want to add extra controls and other fancy stuff, you can do it with a bit \(or a lot, depending on how adventurous you are\) of CSS and Javascript on top of the built-in `<video>` tag.

We won’t go into the details of that here, but it’s not hard to find more information on this subject.

For example, here’s one [article series](http://goodheads.io/2016/06/01/build-youtube-part-1/) that walks you through the steps of building your own comprehensive YouTube application \(or YourTube as this in-depth tutorial aptly calls it\).

## The moral of the story...

As we’ve seen, embedding a video in your website these days is as simple as adding a `<video>` tag to your HTML page.

And outputting video that can run in all browsers, download quickly, and keep your audience watching, is as simple as a Cloudinary dynamic URL with transcoding, resizing, and manipulation parameters to make the video fit your design and your users..

Furthermore, you can generate the HTML code and the video transformation code at once, using the `cl_video_tag` SDK helper method.

And so, the `HTML5 <video> tag` and the Cloudinary `cl_video_tag` went off into the sunset, hand-in-hand as the perfect couple. And they lived happily ever after.

OK, OK, that’s a bit sappy. But I think you get the idea.

You can do everything described in this post by subscribing to any of Cloudinary’s plans, including the [free plan](https://cloudinary.com/signup).

