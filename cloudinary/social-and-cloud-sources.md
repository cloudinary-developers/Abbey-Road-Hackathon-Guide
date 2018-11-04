# Social and Cloud Sources

![JavaScript Upload widget with third party media sources](https://cloudinary-res.cloudinary.com/image/upload/w_700/upload_widget_media_sources_post.jpg)

As developers of web apps, you often need to let users upload files to your app - mainly images and videos. You want the upload interface you provide to offer an intuitive user experience, including the ability to drag & drop multiple media files, preview thumbnails of selected images and videos, view upload progress indication and more. Since we now all live in the cloud era, chances are that many of your users also store media files in the cloud rather than only locally on hard drives and mobile devices, so the option to pick files from social networks like Facebook, cloud storage services such as Dropbox, photo services like Google Photos and more is a big advantage.

**Introducing the new and improved Cloudinary Upload Widget** - now allowing your users to interactively select images from their **Facebook** and **Google Photos** albums, from their **Dropbox** accounts or from the results of a **Google Image Search**.

By including a small JavaScript library and adding a single JavaScript call, you can embed a complete interactive upload UI experience in your web applications:

```javascript
<script src="//widget.cloudinary.com/global/all.js" 
        type="text/javascript"></script>

<script type="text/javascript">
  cloudinary.openUploadWidget(
    { 
      cloud_name: 'demo', 
      upload_preset: 'a5vxnzbp', 
      sources: [ 'local', 'url', 'camera', 'image_search', 
                 'facebook', 'dropbox', 'google_photos' ],
      google_api_key: '.....' }, 
    function(error, result) { console.log(error, result) });
</script>
```

Here's a live example. Click the button below to see the widget in action and try out the different media source tabs.

[Upload Images](social-and-cloud-sources.md)

```javascript
function waitForjQuery(method) {
  if (window.jQuery)
    method();
  else {
    setTimeout(function() { waitForjQuery(method) }, 50);
  }
}

function insertScript(src, callback) {
  var script = document.createElement('script');
  script.onload = callback;
  script.type = 'text/javascript';
  script.async = true;
  script.src = src;
  var s = document.getElementsByTagName('script')[0];
  s.parentNode.insertBefore(script, s);
}

waitForjQuery(function() {
  insertScript('//widget.cloudinary.com/global/all.js', function() {
    cloudinary.applyUploadWidget(document.getElementById('upload_widget_opener'),
      {
        cloud_name: 'hzxyensd5',
        upload_preset: 'aoh4fpwm',
        sources: [ 'local', 'url', 'camera', 'image_search',
'facebook', 'dropbox', 'google_photos' ],
        google_api_key: 'AIzaSyDaQj7FO1IQtp9DSB5YNP5jjG6f_mItEQ4' ,
        theme: 'white',
        thumbnails: '.upload_multiple_images_holder',
        button_caption: "Upload images - Open the Upload Widget"
      },
      function(error, result) { if (console && console.log) { console.log(error, result) } }
    );
  });
});
```

```css
.blog-post .post-holder a.cloudinary-button { color: white }
```

To see the upload widget in action with all media sources, including the Camera and Dropbox sources that require HTTPS, see the following [demo page](https://demo.cloudinary.com/default):

[https://demo.cloudinary.com/default](https://demo.cloudinary.com/default)

## From upload API to complete upload UI

A little bit of history... When Cloudinary's image management service was first introduced back in 2012, it included a [cloud-based API](https://cloudinary.com/documentation/image_upload_api_reference#upload) for uploading images to the cloud and for delivering those images with dynamic manipulations to match your graphic design. The API was powerful, but only when we added SDKs for popular development frameworks such as Ruby on Rails, PHP and Node.js, did developers find it easy enough to use from their back-end applications.

That wasn't enough either. We wanted to eliminate the need for developers to have a server-side upload infrastructure at all, so we added support for [direct upload from the browser](https://cloudinary.com/blog/direct_image_uploads_from_the_browser_to_the_cloud_with_jquery) using a JavaScript library \(jQuery plugin\). Then, the web development world moved towards Single-Page Applications \(SPAs\), so we took it one step further and introduced [unsigned direct upload from the browser](https://cloudinary.com/blog/direct_upload_made_easy_from_browser_or_mobile_app_to_the_cloud), thus eliminating the need for a server component at all.

While we focused on API and developer components behind-the-scenes, we continued to listen to our customers, and answered with our first front-end user interface component: [the Upload Widget](https://cloudinary.com/blog/introducing_a_complete_and_modern_ui_widget_for_cloud_based_image_uploading). It's a very customizable UI component that supports drag & drop, camera photo capturing, progress indications, interactive image cropping, media preview thumbnails and a lot more.

And now, we are happy to introduce the next phase of the Upload Widget: enabling your users to upload images from third-party cloud storage services and social networks.

## Uploading images from third party sources

When using the JavaScript function to open the widget, you can now select up to 7 different media sources to include as tabs within the upload widget's UI. When users select the Facebook, Dropbox, or Google Photos tab, they are prompted to connect to the relevant account. After a successful connection, they can interactively browse through the image search results, their Facebook albums, an image stream of their Google Photos, or the folders & files in their Dropbox account.

The files selected from the remote media sources are then uploaded directly to your Cloudinary account, and are available for [dynamic manipulations](https://cloudinary.com/documentation/image_transformations) to match your graphic design. Furthermore, the files are delivered to your users via CDN URLs, optimized for any device, any browser and in any resolution.

### Select files from Google image search results

Create your Google Search API key, [select](https://github.com/cloudinary-developers/canadian-music-week-hackathon-guide-/tree/39a9b1c59498323c6876cd302c24ff20894ab40f/documentation/upload_widget/README.md#image_search_tab) whether to allow users to search the whole web or a narrowed down set of predefined sites, and whether to include copyright protection modes \(e.g., only images of wikimedia.org that are free to use commercially\). Users can type any search term and then select one or more images from the results.

![width: 700, height: 350](https://cloudinary-res.cloudinary.com/image/upload/w_700,dpr_2.0,q_auto,f_auto/upload_widget_google_image_search_results.jpg)

### Select photos from Facebook albums

You can allow your users to connect to Facebook and browse through their Facebook photos and albums. Users can select multiple photos from Facebook that will be uploaded to your web application, and then be available for further management, delivery and graphic manipulation - such as resizing & cropping.

![width: 240, height: 192, float: left, margin: 0 5px 10px 0](https://cloudinary-res.cloudinary.com/image/upload/w_240,dpr_2.0,q_auto,f_auto/upload_widget_facebook_connect_prompt.jpg)

![width: 480, height: 238, float: left, margin: 0 0 10px 5px](https://cloudinary-res.cloudinary.com/image/upload/w_480,dpr_2.0,q_auto,f_auto/upload_widget_facebook_album_browsing.jpg)

Note: None of your users' personal information is collected or used by the Media Upload Facebook application.

### Select images or videos from Google Photos

Similar to the Facebook media source, you can allow your users to connect to their Google Photos account and browse through all their media files. Selected images can either be uploaded as-is to your Cloudinary account or interactively cropped by your users before uploading.

![width: 480, height: 237, float: left, margin: 0 5px 10px 0](https://cloudinary-res.cloudinary.com/image/upload/w_480,dpr_2.0,q_auto,f_auto/upload_widget_google_photos_browsing.jpg)

![width: 240, height: 191, float: left, margin: 0 0 10px 5px](https://cloudinary-res.cloudinary.com/image/upload/w_240,dpr_2.0,q_auto,f_auto/upload_widget_google_photos_interactive_cropping.jpg)

### Select files from a Dropbox account

Dropbox accounts can contain any kind of file - not only images - and Cloudinary's upload API and upload widget also support uploading any file type \(PDF documents, videos, Office documents, text files, ZIP files, and more\). After connecting to their Dropbox account, your users can browse through their Dropbox folders and select one or more files that can then be uploaded to your Cloudinary account and associated with the model of your dynamic web application.

![width: 700, height: 347](https://cloudinary-res.cloudinary.com/image/upload/w_700,dpr_2.0,q_auto,f_auto/upload_widget_dropbox_folder_browsing.jpg)

For a **full listing of all the JavaScript options and parameters** available for the upload widget, take a look at the [API reference table](https://cloudinary.com/documentation/upload_widget#upload_widget_options) on the upload widget's documentation page.

## Towards a better image upload user experience

In this article, we have highlighted the new media sources you can use with the upload widget. The widget supports many additional capabilities that you can mix and match: interactive cropping, client-side resizing, look & feel customization and more. Take a look at [our documentation](https://cloudinary.com/documentation/upload_widget) for more details.

Spoiler alert! We are already working on the next version of the upload widget, which should be released within the next few months. More media sources, such as additional social networks, cloud storage services and stock photography services will be supported. We are also redesigning the widget with a revamped look & feel, and we are developing the widget to be a centric uploader component for modern web applications.

The upload widget, including support for all-the new media sources described in this post, is available for free for all of Cloudinary's plans. You can [create your free account here](https://cloudinary.com/signup). We would of course appreciate any feedback you have!

