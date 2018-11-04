# Media Authentication

![with\_code: false, with\_url: false](https://res.cloudinary.com/demo/image/upload/cookie_authentication_header.jpg)

Controlling who can access your images and videos, and when, can be an important concern for your business and security workflow. You may have resources that you only want some of your users or employees to access, or you may need to make sure that your original resources are secure, and only transformed \(edited\) versions of your resources are delivered, e.g., with a watermark or logo displayed.

Cloudinary prides itself on the wide range of manipulations available via dynamic URLs, and there are huge benefits to using on-the-fly dynamic manipulations to deliver your public resources. But this flexibility for delivering resources may be too permissive in certain situations because simply changing or removing a dynamic Cloudinary URL parameter can deliver a new image on-the-fly. This can result in users tweaking a URL in order to access the original version of images, for example to view an image _without_ the added watermark, minus the cropping parameters that have isolated a specific face in the image, or without the `pixelate_faces` effect hiding people's identity, etc.

To provide more control over access to your images, Cloudinary offers out-of-the-box support for [uploading resources as authenticated](https://cloudinary.com/documentation/upload_images#authenticated_images). By default, these authenticated resources can only be accessed with a signed delivery URL: a dynamic URL with a signature that must be validated before the resource is delivered. The signature is based on all the dynamic parameters included in the URL, so changing any parameter or value in the URL will invalidate the signature and thus access to the requested resource will be denied.

An example of the single line of code needed for uploading an image as authenticated:

### ruby

```text
Cloudinary::Uploader.upload("bag.jpg", 
    :type => :authenticated)
```

### php

```text
\Cloudinary\Uploader::upload("bag.jpg", 
    array("type" => "authenticated"));
```

### python

```text
cloudinary.uploader.upload("bag.jpg", 
    type = "authenticated")
```

### nodejs

```text
cloudinary.v2.uploader.upload("bag.jpg", 
    { type: "authenticated" }, 
    function(error, result) {console.log(result); });
```

### java

```text
cloudinary.uploader().upload("bag.jpg", 
    ObjectUtils.asMap("type", "authenticated"));
```

An example of the single line of code needed to deliver an authenticated image \(also scaled to a width of 300 pixels\). Note the signature component in the resulting URL \(automatically added when using our SDKs\):

![with\_image: false](https://res.cloudinary.com/demo/image/authenticated/s--8_TXHRoM--/c_scale,w_300/bag.jpg)

The signed delivery method described above may meet your authentication needs in many cases, but what if you want to limit access to your resources to a particular IP address, or to specific users, or for a limited time until they are released? In order to support more advanced requirements for authentication, Cloudinary has added new authentication functionality:

* `Token-based` authentication, providing IP restrictions and time-limited URLs.
* `Cookie-based` authentication, restricting access to users with a valid cookie.

## Token-based authentication

When you need to control which devices have access to an image, the basic signed URL solution may not be enough.

Suppose you have images of products that have not been released yet, or user uploaded images that should not be publicly available \(e.g., signed contracts\). In this case, you would want to allow access only for your employees, or in effect, restrict requests to only those that have been initiated from within your network \(a static IP address\). That’s where token-based authentication comes in.

An authentication token is added as a set of query parameters to the image delivery URL, and is used for validation before delivering the image. Generating the token-based authentication URL is as simple as adding the `sign_url` parameter \(set to `true`\) and the `auth_token` parameter in your SDK resource delivery method. The `auth_token` parameter includes the details that limit access, which in our example would include values for the permitted `ip` and the encryption `key` you receive from Cloudinary.

For example, to deliver the "contract123" image only if the requesting IP address is 22.33.22.11:

### ruby

```text
cl_image_tag("contract123.jpg", :sign_url => true, :auth_token => { 
  :key => "MyKey", :ip => "22.33.22.11"}, :type => "authenticated")
```

### php

```text
cl_image_tag("contract123.jpg",  array("auth_token" => array(
  "key" => "MyKey",  "ip" => "22.33.22.11"), "type" => "authenticated",  
  "sign_url" => true));
```

### python

```text
cloudinary.CloudinaryImage("contract123.jpg").image(
  type = "authenticated", auth_token = dict(ip = "22.33.22.11", 
  key = "MyKey"), sign_url = true)
```

### nodejs

```text
cloudinary.image("contract123.jpg",  { type: "authenticated",  
  auth_token: {key: "MyKey", ip: "22.33.22.11" }, sign_url: true })
```

### java

```text
cloudinary.url().transformation(new Transformation().
  type("authenticated").authToken(new AuthToken("MyKey").
  ip("22.33.22.11").signed(true)).imageTag("contract123.jpg");
```

## Cookie-based authentication

What if you also need fine-grained control over not only the device accessing specific resources or when they are available, but also the specific person or people accessing them?

For example, let’s say you are developing a website that has a membership-only section for registered users. The registered users have access to images and videos that should not be available to your 'regular' visitors. You also want to grant access for up to 1 hour while ensuring that your registered users can't just share an image URL with non-members. In this case you will want to use the [cookie-based authentication](https://github.com/cloudinary-developers/canadian-music-week-hackathon-guide-/tree/39a9b1c59498323c6876cd302c24ff20894ab40f/documentation/image_transformations/README.md#cookie_based_authentication) feature, which expands on the functionality of token-based authentication, enabling you to limit the delivery of authenticated images only to users with a valid cookie. The validity of the cookie can be matched with the user's session expiration and can include an Access Control List \(ACL\) for configuring the URL path where the cookie can be used \(e.g., /image/authenticated/\*\). As with token-based authentication, you can also limit the cookie by IP address and/or time.

In the example above, when a user logs in to the membership section of your website, you would generate a cookie for the user that allows him to view your "authenticated" images. But if anyone without the cookie tried to open the same image URL they would get an error.

**Example**: To create a cookie that is valid for 60 minutes, allows access to all of your authenticated images, and is signed with MY\_KEY:

### ruby

```text
tokenOptions  =  { 
  :key => "MY_KEY", 
  :duration => 3600, 
  :acl => "/image/authenticated/*"
}
cookieToken = Cloudinary::Utils.generate_auth_token(tokenOptions)
```

## Cookies with transformations

The flexibility of cookie-based authentication also provides a means for customizing the access for every user that logs into your system. As Cloudinary uses dynamic URLs to deliver your resources, the Access Control List path in the cookie can include transformations that are custom-tailored with details specific to your company, for example, adding the company logo as an overlay on an image \(e.g., /image/authenticated/l\_logo.png/\*\). That means that the cookie can only be used to authenticate URLs that include the given transformation.

For example, you could set the ACL in the cookie so that it authorizes all images with a width of 700 pixels and a company logo in the top right corner:

### ruby

```text
:acl => "/image/authenticated/w_700/l_logo,g_north_east/*"
```

To simplify the effort, you can group any set of transformations as a [named transformation](https://github.com/cloudinary-developers/canadian-music-week-hackathon-guide-/tree/39a9b1c59498323c6876cd302c24ff20894ab40f/documentation/image_transformations/README.md#named_transformations) and then simply add the named transformation to the ACL. For example, adding a named transformation called "authorized" to the ACL, where "authorized" has been set to the transformations mentioned above: \(`w_700/l_logo,g_north_east`\).

### ruby

```text
:acl => "/image/authenticated/t_authorized/*"
```

## Cookies and user-specific transformations

One of the potential drawbacks of delivering even authenticated images is the ease with which the recipient can simply save the image to their computer and potentially pass it on to anyone else. This can be especially problematic if your company needs specific people to view your resources, but the resources also need to be kept private from others for a variety of reasons, for example, images of pre-released products. To help safeguard against any "leaks", you can provide a means of tracing where the image originated.

Let’s say that John Doe is a product design manager. He needs to have access to all the images being prepared for a planned product release. Here's an example that allows authentication for any image as long as that person's name is added as a semi-transparent text overlay, repeated over the entire image.

### ruby

```text
:acl => "/image/authenticated/a_-25,o_6,l_text:Arial_25_bold:" 
  + current_user + "/fl_tiled.layer_apply/*"
```

So the following image URL will be authenticated for John Doe, but not for any other user:

### html

```text
https://res.cloudinary.com/demo/image/authenticated/a_-25,l_text:Arial_25_bold:John%20Doe,o_6/fl_tiled.layer_apply/w_800/cookies.jpg
```

![with\_code: false, with\_url: false](https://res.cloudinary.com/demo/image/authenticated/s--s5XtdYrE--/a_-25,l_text:Arial_25_bold:John%20Doe,o_6/fl_tiled.layer_apply/c_scale,w_800/cookies.jpg)

![with\_image: false, with\_url: false](https://res.cloudinary.com/demo/image/authenticated/s--GOOo0vEj--/a_-25,l_text:Arial_25_bold:John%20Doe,o_6/fl_tiled.layer_apply/cookies.jpg)

This very identifying watermark can help ensure that John will not break company policy and share _his_ image with others.

## One tough cookie

Preventing unauthenticated access to your resources can be an important concern for a variety of reasons. With cookies you can take your authentication workflow to a whole new level of customizable access to your resources, including the flexibility to tailor the access on an individual basis for every authenticated user. For more detailed information on authenticating resources and implementing cookie-based authentication, see the documentation on [authenticated images](https://github.com/cloudinary-developers/canadian-music-week-hackathon-guide-/tree/39a9b1c59498323c6876cd302c24ff20894ab40f/documentation/image_transformations/README.md#authenticated_images).

The new authentication functionality is currently available for our [Enterprise](https://github.com/cloudinary-developers/canadian-music-week-hackathon-guide-/tree/39a9b1c59498323c6876cd302c24ff20894ab40f/pricing/README.md) customers and requires a small setup on Cloudinary's side. [Contact us](https://support.cloudinary.com/hc/en-us/requests/new) to enable these features for your account.

Cloudinary reduces the complexities of image manipulation, storage, administration and delivery and provides developers with an easy-to-use, end-to-end, cloud-based solution. Cloudinary enables developers to focus on creating their apps and presenting the best images possible. If you haven't tried Cloudinary yet, what are you waiting for? Visit our website to [sign up for a free account](https://cloudinary.com/users/register/free).

