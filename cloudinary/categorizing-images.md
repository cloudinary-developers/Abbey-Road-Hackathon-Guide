# Categorizing Images

![Auto tagging images](https://res.cloudinary.com/cloudinary/image/upload/w_500/imagga_auto_tagging_post.jpg)

If you have an application that allows users to upload their own photos, it can be very useful to be able to organize these photos according to their content. This will allow you to categorize the content for displaying to all your users and make your image library searchable. Furthermore, you can also learn more about your users according to the content they upload and find different trends of what people care about. Other added benefits can also include the ability to display matching content to your users according to their interests or even match them with other users that share similar interests.

Identifying images and their content is a process that would take huge amounts of time and resources if performed manually for many images. On the other hand, unlike text with words, images are data files with no meaning for simple software based filtering and require a deeper analysis of the actual meaning of the pixel colors in the image in order to automate the categorization and tagging process.

[Imagga](http://imagga.com/) is a prominent company that develops and offers technologies, services, and online tools for visual image recognition, with technology that includes state-of-the-art machine learning approaches that allow it to be trained in the identification of various visual objects and concepts. **In this post we would like to introduce you to a new add-on for Imagga's automatic image tagging capabilities, fully integrated into Cloudinary's** [**image manipulation**](http://cloudinary.com/documentation/image_transformation_reference) **and management pipeline**.

## The Imagga Auto Tagging add-on

The Imagga add-on can automatically tell you what's in a photo by returning a list of detected tags and the confidence score of each tag.

The Imagga add-on is very simple to use: just set the `categorization` parameter of Cloudinary's image upload API to `imagga_tagging` while uploading an image and the response will include a list of suitable tags for the image.

For example, uploading the following picture of a koala to Cloudinary and requesting Imagga categorization:

![thumb: w\_400, with\_code: false](https://res.cloudinary.com/demo/image/upload/koala.jpg)

### ruby

```text
Cloudinary::Uploader.upload("koala.jpg",   
  :categorization => "imagga_tagging")
```

### php

```text
\Cloudinary\Uploader::upload("koala.jpg",   
  array("categorization" => "imagga_tagging"));
```

### python

```text
cloudinary.uploader.upload("koala.jpg",  
  categorization = "imagga_tagging")
```

### nodejs

```text
cloudinary.uploader.upload("koala.jpg",   
  function(result) { console.log(result); },   
  { categorization: "imagga_tagging" });
```

### java

```text
cloudinary.uploader().upload("koala.jpg", ObjectUtils.asMap(  
  "categorization", "imagga_tagging"));
```

The response will include the automatic categorization identified by the Imagga add-on. As can be seen in the response snippet below, various categories were automatically detected in the uploaded photo. The confidence score is a numerical value that represents the confidence level of the detected category, where 1.0 means 100% confidence. So Imagga is 100% sure that the picture contains a koala and only 8.5% sure that the picture contains a baboon.

```javascript
…
"info"=>{
  "categorization"=>{
    "imagga_tagging"=>{
      "status"=>"complete", 
      "data"=>[
        {"tag"=>"koala", "confidence"=>1.0}, 
        {"tag"=>"mammal", "confidence"=>0.3151}, 
        {"tag"=>"monkey", "confidence"=>0.0882}
        {"tag"=>"baboon", "confidence"=>0.0853}
```

You can also get a list of tags from an already uploaded image by using the `update` method in Cloudinary's Admin API together with the image's public ID. For example, requesting Imagga categorization for the already uploaded image with a public ID of `landscape`:

![thumb: w\_400, with\_code: false](https://res.cloudinary.com/demo/image/upload/landscape.jpg)

### ruby

```text
Cloudinary::Api.update("landscape",   
  :categorization => "imagga_tagging")
```

### php

```text
\Cloudinary\Api::update("landscape",   
  array("categorization" => "imagga_tagging"));
```

### python

```text
cloudinary.api.update("landscape",  
  categorization = "imagga_tagging")
```

### nodejs

```text
cloudinary.api.update("landscape",   
  function(result) { console.log(result); },   
  { categorization: "imagga_tagging"});
```

### java

```text
cloudinary.api().update("landscape", ObjectUtils.asMap(  
  "categorization", "imagga_tagging"));
```

As with the upload API, the response includes the automatic categorization identified by Imagga shown in the response snippet below, where, for example, "landscape" is identified with 54% confidence, "grass" is identified with 44% confidence, along with a variety of other categories that may be relevant depending on your categorization scheme.

```javascript
…
"info"=>{
  "categorization"=>{
    "imagga_tagging"=>{
      "status"=>"complete", 
      "data"=>[
        {"tag"=>"landscape", "confidence"=>0.5475}, 
        {"tag"=>"grass", "confidence"=>0.4414}, 
        {"tag"=>"field", "confidence"=>0.4121}, 
        {"tag"=>"sky", "confidence"=>0.394}, 
        {"tag"=>"land", "confidence"=>0.3514}, 
        {"tag"=>"rural", "confidence"=>0.3498}, 
        {"tag"=>"grassland", "confidence"=>0.3464}, 
        {"tag"=>"meadow", "confidence"=>0.3403}
```

## Automatic tagging

If you want to organize, browse and manage your images based on the categories identified by Imagga, you can also automatically assign Cloudinary's resource tags to uploaded images.

Add the `auto_tagging` API parameter and set it to a minimum confidence level threshold, where all detected categories with a confidence level above this value will be automatically assigned that category as a resource tag.

For example, to automatically add tags to the `landscape` image with all detected categories that have a score higher than 0.4.

### ruby

```text
Cloudinary::Uploader.upload("landscape.jpg", 
  :categorization => "imagga_tagging", :auto_tagging => 0.4)
```

### php

```text
\Cloudinary\Uploader::upload("landscape.jpg", 
  array("categorization" => "imagga_tagging", "auto_tagging" => 0.4));
```

### python

```text
cloudinary.uploader.upload("landscape.jpg",
  categorization = "imagga_tagging", auto_tagging = 0.4)
```

### nodejs

```text
cloudinary.uploader.upload("landscape.jpg", 
  function(result) { console.log(result); }, 
  { categorization: "imagga_tagging", auto_tagging: 0.4 });
```

### java

```text
cloudinary.uploader().upload("landscape.jpg", ObjectUtils.asMap(
  "categorization", "imagga_tagging", "auto_tagging", "0.4"));
```

The response of the upload API call above returns the detected categories as well as the assigned tags. In this case, only the 'landscape', 'grass' and 'field' categories have a high enough score to be used as tags.

```javascript
{ 
  ...    
  "tags" => [ "landscape", "grass", "field" ]   
  ...  
}
```

You can also use the `update` method to apply Imagga auto tagging to already uploaded images, based on their public IDs, and then automatically tag them according to the detected categories. See the [Imagga add-on documentation](https://cloudinary.com/documentation/imagga_auto_tagging_addon) for more information.

## Categorization of images made easy

Categorizing photos can be a very useful and powerful tool that you can utilize to understand and organize the images that are uploaded by your users. Using the Imagga add-on as part of Cloudinary's service is simple and streamlined: you just need to add a parameter as part of the Cloudinary image upload and manipulation process.

![with\_url: false, with\_code: false](https://res.cloudinary.com/demo/image/upload/w_600/imagga_addon_screenshot.png)

The Imagga Auto Tagging add-on is available now and all Cloudinary plans can try it out with the [add-on’s free tier](https://cloudinary.com/addons#imagga_tagging). If you don't have a Cloudinary account yet, you can easily [sign up for a free account](https://cloudinary.com/signup).

