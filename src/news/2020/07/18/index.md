---
title: Responsive Images and Cloudinary
date: 2020-06-18T13:58:04+00:00
---

Responsive images are hard. This template uses [eleventy-plugin-images-responsiver](https://nhoizey.github.io/eleventy-plugin-images-responsiver) which was developed by the creator of this blog template, [Nicolas Hoizey](https://github.com/nhoizey).
His solution is very good for this blog, but I wanted to have responsive images served to everyone, but also newer image formats( webp, and [JPEG XL](https://nicolas-hoizey.com/links/2020/05/27/how-jpeg-xl-compares-to-other-image-codecs) if their browser supported them.
[Cloudinary](https://cloudinary.com) has been my go-to image management company for a few years. One reason I am a loyal user is their image transformation capability. You can take an image and transform it just by using a URL. For example, let's say they host a cat image for me. If I wanted to make that image available to web browsers that accept the [webp](https://developers.google.com/speed/webp) then I would just have to change the URL and like magic and browser will get that new webp formatted image. Everyone else will get a plain jpeg.
Here is a made-up URL as an example:

https://res.cloudinary.com/demo/image/fetch/v15854736092/11ty/nice_city-desert-pic.jpg

To transform this URL to a magic one you just need to adjust the URL like so:

https://res.cloudinary.com/demo/image/fetch/f_auto/v1589736092/11ty/nice_city-desert-pic.jpg

f_auto tells Cloudinary to serve the smallest image in a format the browser can accept, in this case, Google Chrome, Opera browser, Firefox will get a smaller picture (webp), while others might get nothing, so a jpeg should be served. This is based on Cloudinary detecting which browser you are using, and they use your browser headers to find out.
Here is an example of what my browser told a web site that I just Googled.
ACCEPT text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
ACCEPT-ENCODING gzip, deflate, br
ACCEPT-LANGUAGE en-us
HOST www.whatismybrowser.com
REFERER https://www.google.com/
**USER-AGENT** Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_4) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/13.1 Safari/605.1.15
The user agent is most important since it tells what browser I am using, and Cloudinary which image format I can receive.

So that is how Cloudinary sends reduced images when it can tell which browser is being used.

Now for the even better part. If you use Cloudinary's javascript library and change the src to data-src those images will get magically transformed to match your website size requirements. Check out their [webpage](https://cloudinary.com/documentation/responsive_images#automating_responsive_images_with_javascript) for more about it.
So now let's say I have a 3MB image that is crazy large 4000x2500 pixels. On a desktop that will display as a 1.5MB image but still 4000x2500 pixels. If an iPhone visits your site it is fine to serve a smaller pic at 500KB but not cool to send it with the same dimensions as the desktop, 4000x2500. 
Using javascript Cloudinary can see the exact dimensions or limits you want the image to conform to and adjusts the image to fit exactly how you wanted it. You can even rotate your iPhone and a larger picture will update to your larger screen size.

Here is an example 3MB image of a Ferrari. It is 4961x3605, way too large to consider sending to a phone even if the file size is smaller after Cloudinary does it's thing.
<img
   data-src="https://res.cloudinary.com/paulportfolio/image/upload/w_auto,c_scale,q_auto,f_auto,dpr_auto/v1592493970/11ty/ferrari-pista-3.jpg"
alt=""
class="cld-responsive" />

<img
   data-src="https://res.cloudinary.com/paulportfolio/image/upload/w_auto,c_scale,q_auto,f_auto,dpr_auto/v1592494095/11ty/ImageInfo.png"
alt=""
class="cld-responsive" />

Next is the same picture sent to an iPhone.

<img
   data-src="https://res.cloudinary.com/paulportfolio/image/upload/w_auto,c_scale,q_auto,f_auto,dpr_auto/v1592495043/11ty/IMG_1115.png"
alt=""
class="cld-responsive" />

It is still a little large, 1200x872, but not too bad. So you see how this works and without saving multiple versions of the file at different sizes.



Now, this is all for nothing if the user turns off javascript. Thankfully most users keep it turned on. My site is not prepared for that scenario, because that requires me to think more, and deep down I think you're an animal for not leaving javascript on, haha
