# Build a Cover Image

In this example we'll take a performance image and create a cover image. Here we have the amazing artist, Wiz Khalifa - image copyright and courtesy of Ardentes Music Festival.

![](http://res.cloudinary.com/tamas-demo/image/upload/c_scale,w_300,dpr_2.0/wallifornia/wiz-khalifa.jpg.png)

Beautifully cropped square image, but to make it a cover image we need the image to fit into a 16:9 aspect ratio. We will need to pad the image to make up the image fit into the new aspect ratio. First step is to example the direction the performer's eyes are gazing. Wayne is looking to the left so let's add lead space and pad the image to the left.

![](http://res.cloudinary.com/tamas-demo/image/upload/c_scale,w_600,ar_16:9,c_lpad,g_west,dpr_2.0/wallifornia/wiz-khalifa.jpg.png)

`http://res.cloudinary.com/tamas-demo/image/upload/ar_16:9,c_lpad,g_west/v1530016018/wallifornia/wiz-khalifa.jpg`

We added aspect ratio of 16:9, cropping of lpad and gravity west to create the image and move it to the right. This done simply by adding the params into the url as follows:

```text
ar_16:9,c_lpad,g_west
```

Nice but would it be better if the background color matched the exact same color as the backgound in our original? Easy! Just add background auto to our url:

```text
b_auto
```

![](http://res.cloudinary.com/tamas-demo/image/upload/c_scale,w_600,ar_16:9,c_lpad,g_west,b_auto,dpr_2.0/wallifornia/wiz-khalifa.jpg.png)

`http://res.cloudinary.com/tamas-demo/image/upload/ar_16:9,c_lpad,g_west,b_auto/v1530016018/wallifornia/wiz-khalifa.jpg`

Looking good! Now let's optimize this for performance and quality.

![](http://res.cloudinary.com/tamas-demo/image/upload/ar_16:9,c_lpad,g_west,b_auto,dpr_2.0/wallifornia/wiz-khalifa.jpg.png)

We can optimize the dpi, format, and quality with a few additional params in our url:

```text
dpr_auto,f_auto,q_auto:best
```

The addition of these params will improve performance and delivery of the final image tremendously, In general you should always use them.

`http://res.cloudinary.com/tamas-demo/image/upload/w_1600,ar_16:9,c_lpad,g_west,b_auto,dpr_auto,f_auto,q_auto:best/v1530016018/wallifornia/wiz-khalifa.jpg`

You'll notice we also added a width param: **w\_1600** - You'd set this to fit the image into a explicit layout size, if you omit it you'll get the original image size. The example here were set at a width of 600 to fit nicely in the layout.

Our cover image allready looks awesome, but let add a artistic filter to enhance the black and white image. Adding the effect param with a named filter is how we do it.

```text
e_art:zorro
```

![](http://res.cloudinary.com/tamas-demo/image/upload/c_scale,w_600,ar_16:9,dpr_2.0,c_lpad,g_west,b_auto,dpr_auto,f_auto,q_auto:best,e_art:zorro/wallifornia/wiz-khalifa.jpg.png)

Nice vibe! You can almost hear Wiz's heavy rapping beats. We have dozens of artistic filters, text and image overlays to experiment with and make that cover image pop.

This looks great so far however the background colour that we have generated stands out a little bit as there’s a seam between the original image and the generated background. We can very easily fix this visual defect by adding a gradient fade to ease the background colour to the main image.

We can achieve that by adding these parameters to the image:

`e_gradient_fade:symmetric_pad,x_50/e_art:zorro/`

![](http://res.cloudinary.com/tamas-demo/image/upload/c_scale,w_600,ar_16:9,dpr_2.0,c_lpad,g_west,b_auto,dpr_auto,f_auto,q_auto:best,e_gradient_fade:symmetric_pad,x_50/e_art:zorro/wallifornia/wiz-khalifa.jpg.png)

Notice how the previously added artistic filter is added as a different layer. We are required to specify it this way since the gradient fade will now occupy a layer and we need the artistic filter to be on a different layer in order for it to be visible.

Finally, we are also going to place the logo of the festival in the middle of our newly generated image - this would make a great addition to the image itself.

This is the logo that we’ll be using - it is also loaded as an asset to Cloudinary:

![](https://res.cloudinary.com/tamas-demo/image/upload/v1530018414/wallifornia/logo20182x.jpg)

Notice that this logo has a white background and a certain size as well, which is a tad too large for our scenario. So it’s not only enough to place the image as an overlay but we need to apply some transformation to this image before we add it as a new layer. We can achieve this by adding the following options:

`/e_make_transparent:10,l_wallifornia:logo20182x.jpg,w_140/`

And here is the final result:

![](http://res.cloudinary.com/tamas-demo/image/upload/c_scale,,dpr_2.0,w_600,ar_16:9,c_lpad,g_west,b_auto,dpr_auto,f_auto,q_auto:best,e_gradient_fade:symmetric_pad,x_50/e_make_transparent:10,l_wallifornia:logo20182x.jpg,w_140/e_art:zorro/v1530016018/wallifornia/wiz-khalifa.jpg.png)

Let's also add some text to this image to display the name of the artist. We can very easily achieve that by adding yet another layer and specify some options \(such as the font family, font size and additional options\):

`/l_text:roboto_45:Wiz%20Khalifa,co_black,g_south_east,x_30,y_10,w_600,c_fit/`

This is how the final result looks like:

![](http://res.cloudinary.com/tamas-demo/image/upload/ar_16:9,,dpr_2.0,c_lpad,g_west,b_auto/e_gradient_fade:symmetric_pad,x_50/e_art:zorro//e_make_transparent:10,l_wallifornia:logo20182x.jpg,w_140/l_text:roboto_45:Wiz%20Khalifa,co_black,g_south_east,x_30,y_10,w_600,c_fit/v1530016018/wallifornia/wiz-khalifa.jpg.png)

