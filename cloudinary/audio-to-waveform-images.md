# Audio to Waveform Images

![Generate waveform of uploaded audio and video files](https://res.cloudinary.com/cloudinary/image/upload/w_500/waveform_post.png)

Many social networks, websites and messaging applications allow users to upload a wide variety of media files, and although the majority of files are in the form of images and video clips, a significant minority are audio files. When the website or application subsequently needs to display a thumbnail that describes the uploaded content, images can be cropped and resized down to scale, and a single frame from a video clip can be converted to an image and then also cropped and resized down to scale.

So what do you display when you need something to uniquely and visually represent an audio file? A useful solution is to display a [waveform](https://en.wikipedia.org/wiki/Waveform) image, which is a visual representation of the audio file and is presented as a graph of the sound amplitude against time.

## Creating waveform images

Cloudinary's media management service has support for uploading, manipulating and managing all kinds of media files, including images, videos and audio files. You can create waveform thumbnails of audio files just as easily as you can create thumbnails for images and videos, with fine control over the look & feel of the generated waveform image to match your graphic design and the responsive layouts of all devices and browsers. All the audio processing, image generation and manipulation takes place on-the-fly and in the cloud using dynamic URLs, and with no need to install any complex software.

Creating an image waveform from an audio file [uploaded to your Cloudinary account](https://cloudinary.com/documentation/upload_videos) is as simple as changing the file extension \(format\) of the Cloudinary audio delivery URL to an image format like PNG, and enabling the `waveform` flag \(`fl_waveform` in URLs\). By default, the resulting waveform image is delivered with a high resolution, so you will also want to scale down the resulting image.

For example, to generate a PNG waveform image of the `bumblebee.mp3` audio file uploaded to Cloudinary's demo account, scaled to a height of 200 pixels and a width of 500 pixels:

![Audio waveform image of 500x200](https://res.cloudinary.com/demo/video/upload/h_200,w_500,fl_waveform/bumblebee.png)

Note that as well as generating waveform images from audio files, you can also generate waveform images from the audio track of a video file in the same way as described above: simply change the file extension of a Cloudinary video URL to an image format like PNG, and enable the `waveform` flag \(`fl_waveform` in URLs\).

## Customizing the waveform image

You can also control the colors used in the waveform image with the `color` parameter \(`co` in URLs\) to set the color for the waveform \(default `white`\) and the `background` parameter \(`b` in URLs\) to set the background color of the image \(default `black`\).

For example, to generate the same PNG waveform image of the `bumblebee.mp3` audio file in the example above in inverted colors - with the waveform rendered in black on a white background:

![Black on white waveform image](https://res.cloudinary.com/demo/video/upload/h_200,w_500,fl_waveform,co_black,b_white/bumblebee.png)

If you only want to capture the waveform of a specific segment of the audio file, you can use a combination of the following 3 parameters to specify the section of the audio file to sample for the waveform:

* `start_offset` \(`so` in URLs\) specifies the start of the sample.
* `end_offset` \(`eo` in URLs\) specifies the end of the sample.
* `duration` \(`du` in URLs\) specifies the duration of the sample.

For example, to display a PNG waveform image of a sample from the 2 second mark until the 4 second mark of the `bumblebee.mp3` audio file uploaded to Cloudinary's demo account, scaled to a height of 250 pixels and a width of 400 pixels, with the waveform rendered in blue on a green background:

![Waveform of a partial audio cut with color customization](https://res.cloudinary.com/demo/video/upload/h_250,w_400,fl_waveform,so_2,eo_4,co_blue,b_rgb:02b30a/bumblebee.png)

## Visualization of uploaded audio files made simple

Waveform images are a nice way to visualize audio files, and are useful for user generated content, social networks and social messaging apps. With Cloudinary you can easily generate images of the waveforms of audio files, with the images generated on-the-fly using dynamic delivery URLs and delivered optimized via a fast CDN. The generated image thumbnails for audio, as well as [image](https://cloudinary.com/documentation/image_transformations#resize_dimensions) and [video](https://cloudinary.com/documentation/video_manipulation_and_delivery#generating_video_thumbnails) files, can be [further manipulated](https://cloudinary.com/documentation/image_transformations) to match any graphic design and any responsive layout, just like any other image uploaded to Cloudinary.

Full audio support including upload, manipulation, streaming and waveform generation is available in all Cloudinary's plans, including the free tier. Try it yourself by [opening a free account](https://cloudinary.com/signup).

