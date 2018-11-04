# Artistic Filters

![artistic filters in poloroid frames](https://res.cloudinary.com/cloudinary/image/upload/w_700/blog_poloroid_filters_wide.jpg)

Every picture has a story to tell. But the story it tells can change when you change the color tone, saturation, contrast, or other elements of a photo.

A few years ago, post-processing a digital image generally required a high level of skill and expensive software such as PhotoShop. But in recent years, popular photo sharing apps such as Instagram, Flickr, and Snapchat started offering built-in filters. Professionals take advantage of filters to make subtle corrections or adjustments. Casual users often apply more prominent filters that add their own unique touch or just make their images more fun.

These easy-to-apply filters have made photo post-processing an almost integral and expected part of the process; so much so that people feel the need to make a point of noting when they've actually posted an unaltered photo: the **\#nofilter** hashtag.

But research shows that filtered photos increase engagement. According to a recent [study](http://comp.social.gatech.edu/papers/icwsm15.why.bakhshi.pdf) by _Yahoo Labs_ and _Georgia Tech_, filtered images are **21% more likely to be viewed** and **45% more likely to be commented on** than non-filtered counterparts.

So filters can be really valuable, both for your own site photos and to add value for your users, but developing a set of proprietary filters would be a hefty project. No worries. Cloudinary now offers 21 artistic filter transformations for Web and app developers to choose from. This makes it easy to adjust your photos on-the-fly to match the message and design of a particular page, or to pass them on as a feature to the users who upload photos to your site or app.

## How does it work?

Normally, generating these effects on your site or app would involve complex client-side CSS, javascript coding, and SVG rendering to achieve the desired combinations of blurring, sharpening, gradient overlays, recoloring, and blending effects.

But when you use Cloudinary's artistic filters, we handle all the image processing on the cloud. All you have to do is pick the filter you want, add it as an `e_art:<filter-name>` transformation in the image URL, or using any of our SDK framework languages, and deliver. For example:

![with\_image:false](https://res.cloudinary.com/demo/image/upload/e_art:red_rock/bicycle.jpg)

## Sandbox

OK, so you wanna play too? Here’s a sandbox where you can try out all the available filters on a few images with different kinds of content.

[View Sandbox Demo](https://codepen.io/cloudinary/live/EZYmgz/)

## Taking it up a notch

Above, you can see how simple it is to apply any of the available artistic filters to any photo, but you don’t have to stop there...

* **double the fun**: If no single artistic filter achieves exactly the effect or impact you are looking for, don’t limit yourself to one. If you want to increase the aggressiveness of a filter, simply chain the same filter in consecutive transformation components. For example, here’s the sandbox photo with no filter, a single `athena` filter, and a double `athena` \(**.../upload/e\_art:athena/e\_art:athena/sandbox.jpg**\) filter. Each application of the filter adds a bit more of a yellow sunny center and slightly more washed out color at the edges.  

![original image - no filter](https://res.cloudinary.com/demo/image/upload/w_200/sandbox.jpg) **Original** ![athena artistic filter](https://res.cloudinary.com/demo/image/upload/w_200/e_art:athena/sandbox.jpg) **Athena X 1** ![athena X 2](https://res.cloudinary.com/demo/image/upload/w_200/e_art:athena/e_art:athena/sandbox.jpg) **Athena X 2**

In the same way, you can also chain transformations to apply two \(or more\) different filters, making the possibilities endless. For example, below we take advantage of the telescopic effect of `zorro` along with the historical grays of `daguerre`.

![Two different filters applied](https://res.cloudinary.com/demo/image/upload/e_art:zorro/e_art:daguerre/w_300/sandbox.jpg)

Note that while you will get a similar result if you reverse the order of the chained artistic filters, it is not identical, so it’s always worth trying in both directions.

* **mix and match**: You can also achieve unique results by chaining an artistic filter before or after [other effects](https://github.com/cloudinary-developers/canadian-music-week-hackathon-guide-/tree/39a9b1c59498323c6876cd302c24ff20894ab40f/documentation/image_transformations/README.md#applying_image_effects_and_filters), such as `tint`, `blur`, `sharpen`, `pixelate`, `vignette`, `contrast`, `vibrance`, `oil paint` and more. Check out what happens when we decide to both `pixelate` and add the `red_rock` filter to this dog:

![with\_image: false](https://res.cloudinary.com/demo/image/upload/w_200/e_pixelate:3/e_art:red_rock/dog.jpg)

![original image](https://res.cloudinary.com/demo/image/upload/w_200/dog.jpg) **Original** ![pixelate effect](https://res.cloudinary.com/demo/image/upload/w_200/e_pixelate:3/dog.jpg) **Pixelate effect** ![pixelate + red\_rock filter effects](https://res.cloudinary.com/demo/image/upload/w_200/e_pixelate:3/e_art:red_rock/dog.jpg) **Pixelate + red\_rock filter**

* **on condition**: Different types of filters may be appropriate for different subject matter. Some are better for outdoors, some for inanimate objects, and so on. Consider using [conditions](https://cloudinary.com/documentation/image_transformations#specifying_conditions) in your transformation to apply a particular filter only for images with a particular tag. For example, the URL below applies the bright-day effect of the `peacock` filter only if the image has `nature` in it’s tag set:

  ![](https://res.cloudinary.com/demo/image/upload/if_!nature!_in_tags,c_fill,h_160,w_240,e_art:peacock/if_else,c_fill,h_400,w_600/sandbox.jpg)

  The `sandbox` image has the `nature` tag, so the `peacock` filter is applied, but if you use the exact same transformation for the

  [partners\_table.jpg](https://res.cloudinary.com/demo/image/upload/if_!nature!_in_tags,c_fill,h_160,w_240,e_art:peacock/if_else,c_fill,h_400,w_600/partners_table.jpg) image, it is not. You could of course add several `if` components to cover a number of different tags and corresponding filters to apply.

  **Note**: For the purposes of the above example, the two conditions also use different dimensions so that it's easy to see which condition was applied to each one.

## What’s in a name?

After having seen and experimented with our list of filters, maybe you are wondering where those names came from and what each one is good for? Like most photo filters available out there, our filter names have a variety of origins. And filters tend to have different impacts on different content, so there are no hard and fast rules. But below, we share a bit of background on some of the names and where they might come in handy.

In the monochrome family, we decided to name our sharp black and white filter after **Audrey** Hepburn, while the more fuzzy gray-toned filter is named for Louis-Jacques-Mandé **Daguerre** \(1787 - 1851\), inventor of the daguerreotype process of photography. On the other hand, **incognito** gives you a dark monochrome with a mysterious, subtle purplish tone.

For cooler colors, **primavera** \(meaning ‘spring’ in many romance languages\) gives a high contrast, blue-sky effect to your nature scenes. **Peacock** adds a bright blue tint with a high exposure that can brighten your outdoor shots, but may make people look slightly pale. **Eucalyptus**, not surprisingly, has a light green touch, which gives grass and trees a healthy look. Try **linen** for a crisp, clean feel, or **frost** for modern images and inanimate objects.

When you want to go for warmth, **athena**, the Greek goddess of arts and literature, and daughter of sun god, Zeus, can make almost any day look yellow and sunny. Or maybe you want to give your pictures a pinkish tone and the gentle spotlight effect of **aurora**, named for the polar light seen in arctic regions. If you are looking for a warm retro feel with a soft purple-pink hue, consider **fes** \(a Moroccan city\). Or perhaps go for a nostalgic faded look with **hokusai**, named for the Japanese artist who painted in that style.

Well, you get the idea. You’ll really have to play with them all to decide what’s best for your photos. But if you are not sure, do keep in mind that according to the [study](http://comp.social.gatech.edu/papers/icwsm15.why.bakhshi.pdf) mentioned above, filters that increase warmth, exposure, and contrast seem to boost views and comments.

## Now it’s your turn!

You’ve read how the right filter can increase user engagement, and you now know that all it takes to apply filters to your photos is a simple `e_art` transformation. Letting your users express their own personality with the photos they upload to your site or app is just as easy. You’ve had a chance to toy around with the filters on our `sandbox` photos. Now it’s time to let your creativity run wild on your own images.

The artistic filters, along with many other upload and manipulation features, are available with all of Cloudinary’s plans including the [free plan](https://cloudinary.com/signup).

We invite you to comment below to tell us your favorite filters and to share your unique ideas for combining them with other features.

