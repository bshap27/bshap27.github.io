---
layout: post
title: Custom Fonts in Rails
---

Including a custom font in my Rails app was trickier than I expected it to be. Specifically, I wanted to include <a href="http://www.entypo.com/">Entypo</a> so that I could use its fun social icons. The Entypo website provides a downloadable zipfile of individual svg files, which isn't what I wanted. I was eventually able to find, via the Google machine, the set of eot, svg, ttf, woff and css files that are generally needed in order to require the font in your app. In Rails 4, copying the 4 font files directly into your assets/fonts folder should automatically require them in your app. I placed my CSS file into the stylesheets folder and refreshed my app. I had added an icon to a view, and in its place was appearing a small rectangle. So the view knew to look for an icon, but it wasn't finding the character. Something about the way I had copied in the font files was not correct.

In your font's CSS file, you'll need to specify the file path to the eot/svg/ttf/woff font files. The default will look something like this:

{% highlight css %}
@font-face {
  font-family: 'entypo';
  src: url('/assets/entypo.eot?71205724');
  src: url('/assets/entypo.eot?71205724#iefix') format('embedded-opentype'),
       url('/assets/entypo.woff?71205724') format('woff'),
       url('/assets/entypo.ttf?71205724') format('truetype'),
       url('/assets/entypo.svg?71205724#entypo') format('svg');
  font-weight: normal;
  font-style: normal;
}
{% endhighlight %}


Since the characters weren't loading, I figured there was something up with the relative path for each of these files. I played with the path for some time and wasn't able to find the combination of folders that would get the files to load. While researching alternatives to abstract out the literal paths of the files, I discovered the rails helper <b>asset_path</b>. It's used via ERB, like so:

{% highlight css %}
@font-face {
	font-family: 'entypo';
	src:url(<%= asset_path 'entypo.eot?-pco6za' %>);
	src:url(<%= asset_path 'entypo.eot?#iefix-pco6za' %>) format('embedded-opentype'),
		url(<%= asset_path 'entypo.woff?-pco6za' %>) format('woff'),
		url(<%= asset_path 'entypo.ttf?-pco6za' %>) format('truetype'),
		url(<%= asset_path 'entypo.svg?-pco6za#entypo' %>) format('svg');
	font-weight: normal;
	font-style: normal;
}
{% endhighlight %}

Essentially this helper "computes the path to an asset in a public directory" (per Rails documentation). Using this helper will also allow any file references within these files to be processed by the Asset Pipeline. <b>NOTE: It's imperative that you also change the file extension of the css file to .css.erb, otherwise your stylesheet will not be processed.</b>

<u>A few choice words on IcoMoon</u>

I watched a great CSS-Tricks screencast called <a href="https://css-tricks.com/video-screencasts/113-creating-and-using-a-custom-icon-font/">Creating and Using a Custom Icon Font</a>. To quote this reference, "To be the most efficient with your icon font, you should only load the characters that you need to load. And to be flexible, it's nice to be able to add to a single icon font from multiple sets or from any vector/SVG anywhere at all. The IcoMoon app lets you do all of this from it's super simple interface. You choose the icons you want, map them to whatever characters you want, then export the HTML/CSS/Web Fonts in a ready to use format."

I found <a href="https://icomoon.io/app">IcoMoon</a> to be extremely easy to use and to require in my app, so I thought I'd share it with you all. Enjoy :)