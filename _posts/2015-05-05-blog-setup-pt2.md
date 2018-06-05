---
layout: post
title: Setting Up an Elegant Blog with Github Pages, Jekyll, and Poole; Part II
comments: true
tags: [ web, tutorial, markdown  ]
---

I guess it's time to talk a little bit about the finishing touches I did to customize this site further beyond what Poole and Layon offer.  

## <a name="resources"></a>Resources

I used the following sites for help with these customizations, ideas, code, and more. Be sure to visit them and poke around a bit:

* [How I Created a Beautiful and Minimal Blog Using Jekyll, Github Pages, and poole](https://joshualande.com/jekyll-github-pages-poole/) - Joshua Lande discusses the route he took in setting up his blog with a detailed write-up of how he bootstrapped and customized his site. A very helpful guide.
* [Using Jekyll, Poole and Lanyon to Setup My Github User Page](https://patricksteadman.ca/2014/08/04/lanyonsetup/) - Patrick Steadman briefly lists the customizations on his Jekyll site and links to articles to read about them. I loved how he customized his sidebar, and used much of the same design. 
* [Github Help on Markdown Syntax](https://help.github.com/articles/markdown-basics/)
* [Liquid Markup Documentation](https://github.com/Shopify/liquid/wiki)
* [Jekyll Project Official Site](https://jekyllrb.com/)

## Enabling Disqus Comments

First, visit the [Disqus website](https://www.disqus.com), set up an account, and log in. Upon logging in you will be brought to your dashboard. Click the gear in the top right corner, and in the dropdown box select "Add Disqus to Site." Follow the commands until you get to the unique code for your disqus comments.

Now, shifting forcus to your site, you'll want to add the following line to `_layouts/default.html`:  

{% raw %}
`{% include comments.html %}`
{% endraw %}

If you take a look at my [default layout]({{ site.github.repo }}/_layouts/default.html) you will see that this is placed in the content container div underneath the liquid tag for the post's (or page's) content. The relevant code:

```html
<div class="container content">
  {% raw %}
  {{ content }}
  {% include comments.html %}
  {% endraw %}
</div>
```

The parent divs are wider than the content container, and so adding the `include` statement outside of this one will make the comments section (once you implement it in `comments.html`) stretch across the entire page, rather than being confined to the content's area. 

Now that you are armed with Disqus's universal code and you have set the location of your comments in the HTML, you can create `comments.html` in the `_includes` folder. Here's what my [comments.html]({{ site.github.repo }}/_includes/comments.html) looks like:

```html
{% raw %}
{% if page.comments %}
<div id="disqus_thread"></div>
<script type="text/javascript">
    /* * * CONFIGURATION VARIABLES * * */
    var disqus_shortname = %%%YOUR USER NAME HERE%%%;
    var disqus_identifier = "{{ site.disqusid }}{{ page.url | replace:'index.html','' }}";
    
    /* * * DON'T EDIT BELOW THIS LINE * * */
    (function() {
        var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
        dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
        (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
    })();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript" rel="nofollow">comments powered by Disqus.</a></noscript>
{% endif %}
{% endraw %}
```

The first thing you see is this liquid tag: {% highlight liquid %}{% raw %}{% if page.comments %}{% endraw %}{% endhighlight %} which is paired with {% highlight liquid %}{% raw %}{% endif %}{% endraw %}{% endhighlight %} at the end of the file. This will run all the code it encloses if the ```comments``` is set to true in the YAML frontmatter of whichever page or post is being generated. After that is the universal code (slightly modified) provided by Disqus, and the value of the `disqus_shortname` variable is provided by Disqus (and is simply your Disqus username). Don't forget to set `Comments` to `true` or `false` in your YAML frontmatter!

The `disqus_identifier` configuration variable does not come from the universal code, but it helps Disqus return the appropriate thread for your article. See more about Disqus configuration variables [here](https://help.disqus.com/customer/portal/articles/472098-javascript-configuration-variables).

This code was adapted from [Joshua Lande's excellent article](https://joshualande.com/jekyll-github-pages-poole/).

## Enabling Google Analytics

This is very straightforward and follows the same pattern as setting up the Disqus comments. Go to the [Google Analytics site](www.google.com/analytics/), sign up for an account if you don't have one already, use universal tracking and copy the code that they provide. Create a file in the `_includes` folder and name it something like `google_analytics.html`. Paste in the code Google gave you and save the file. Now all that's left is to open `layouts/default.html` and add the following line:
{% highlight liquid %}
{% raw %}
{% include google_analytics.html %}
{% endraw %}
{% endhighlight %}

## Favicon

A favicon can be built an an image editor like GIMP, and there are a number of sites that have pre-made designs you can choose from. Save your favicon.ico to the folder `public` (which should have a placeholder favicon already present), then head over to `_includes/head.html` and and verify that the reference to your favicon exists:
{% raw %}
```html
<link rel="shortcut icon" href="{{ site.baseurl }}public/favicon.ico">
```
{% endraw %}

## Tags Page

This page was modified from [Patrick Steadman's site](https://patricksteadman.ca/2014/08/04/lanyonsetup/) that I mentioned earlier. You can store this page in the root folder for your site as `tags.html`. A slight modification from his version was to comment out the code that displays the number of articles with a given tag, as you can see [in my repo](https://github.com/kylestratis/kylestratis.github.io/blob/master/tags.html). Feel free to copy and paste the code directly, and note how the YAML frontmatter declares it a `page` rather than a `post`. 

## Sidebar

I again drew inspiration from Patrick Steadman's design here, which is clean and balanced, and has some nice features not present in the default Lanyon sidebar. Let's first take a look at the sidebar and its structure. At the top I have a pretty picture of myself cropped as a circle, below which I have a some nice attractive icons that link to my various social networks. Below that still is a short tagline, then site navigation, version number, and a copyright notice (don't worry, this is just for the blog content, the actual code is available under MIT licensing). You can find the sidebar code in `_includes/sidebar.html`. All of the code in the following subsections will be within the first div of this file, aside from the CSS file:

```html
<div class="sidebar" id="sidebar">
```

### Custom CSS

First, though, we will want to apply some custom CSS for the sidebar to allow for a few aesthetic features like opacity. To do this, we will create a new file in `public/css/` called `custom.css`. Save the empty file as it is, then open `head.html` in `_includes` and add the following line under the CSS comment:

```html
<link rel="stylesheet" href="{{ site.baseurl }}public/css/custom.css">
```

Save that, now go back to your custom CSS file, and add the lines below. Feel free to play with the values to get the effect that is most pleasing to your eye, this is your site after all! Since you've got the CSS file linked, you can use `jekyll serve` in your terminal to test your changes to the CSS. 

```css
.sidebar {
       opacity: 0.8;
}
   
.sidebar:hover {
       opacity: 1.0;
}
```

This will simply set the default and hover opacities for the sidebar, tweak these to what looks pleasing to your eye. 

```css
.sidebar-logo {
      padding: 1.5rem;
}
  
.sidebar-logo img {
      border-radius: 50%;
      -moz-border-radius: 50%;
      -webkit-border-radius: 50%;
      width: 160px;
      margin: 0 auto;
}
```

The logo will be your gravatar (details below), and this sets the location (via `padding` and measured in rem units, for more about rem units [see this article](https://css-tricks.com/theres-more-to-the-css-rem-unit-than-font-sizing/)), shape (via `border-radius` which defines the *circularity*, if you will, of the image), size (via `width`), and again location (via `margin`). Now that we've done some setup, we can move on to the gravatar logo. 

### Gravatar

First, we will set up a gravatar. Go to [Gravatar's site](https://gravatar.com) and set up an account, if you don't have one already. Upload the image you wish to use, and follow all the instructions for setting up your gravatar. Eventually, you will be given an email hash, and you should add this to your `_config.yml` file, something like this (with other identifiers removed):

```yaml
author:
    gravatar_md5:     //your hash here
```

Then open up your sidebar HTML file and add this line right inside the first div: 

```html
 <div class="sidebar-logo" style="align:center">
      <img src="https://www.gravatar.com/avatar/{% raw %}{{ site.author.gravatar_md5 }}{% endraw %}?s=120" />
  </div>
```

This will allow the CSS to be applied to your gravatar properly. 

### Contact List

Below the logo, we have some stylish icons that link to various methods of contacting me. These icons are from the excellent (and free) [Font Awesome icon pack](https://fortawesome.github.io/Font-Awesome/), and are a breeze to install. The easiest way is to use their Bootstrap CDN: all you have to do is add the following line to your `_includes/head.html` with your other CSS links:

```html
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">
```

Now you have access to the icons, but how do you use them? I will show you some example code below, which works with your `_config.yml` file, but first take a look at the [519 icons included in the Font Awesome pack](https://fortawesome.github.io/Font-Awesome/icons/). Chances are you'll find some that you like better than the ones I use, or you'll find one for a social media account that I don't have linked, but that you do. 

On to the code: the first thing you'll want to do is set up a div container for your contact list, like so:

```html
<div id="contact-list" style="text-align:center">
<!-- contact icons go here --> 
</div>
```

You will want one of these div containers for each row of icons you want to use. Within these, you will add an if block that will display an icon and link if you have specified the site in your config. 

In the example below, your config is checked to see if you have defined an attribute named `github` under `author`, and if it is present a link to github is constructed with your github username (assuming that's what the `github` attribute is set to). Within that `a` tag is a `span` tag with a `class` attribute that tells it to stack the images within. We are stacking icons to allow for a border, which is defined by the first `i` tag and the enclosed icon in the second `i` tag. For more examples on what you can do with the Font Awesome CSS, see their [examples page](https://fortawesome.github.io/Font-Awesome/examples/).

{% raw %}
```html
{% if site.author.github %}
  <a href="https://github.com/{{ site.author.github }}">
    <span class="fa-stack fa-lg">
      <i class="fa fa-square-o fa-stack-2x"></i>
      <i class="fa fa-github-alt fa-stack-1x"></i>
    </span>
  </a>
{% endif %}
```
{% endraw %}

Your actual link will be different based on the contact method: LinkedIn will have a different way to get to a given profile than Github, as an example, and if you want to include an email you will instead have a `mailto:` link. Repeat this pattern (or one that you make with Font Awesome's many styling features) for each icon you want on each row, and don't forget that each row will have its own `contact-list` div! 

### Description and Navigation

These items are mostly unchanged from the original Lanyon sidebar, however I did remove the download link because it is mostly redundant with the link to the project and it doesn't work if you are primarily working on the master branch. If you do want the download link, change this:

```html
<a class="sidebar-nav-item" href="{% raw %}{{ site.github.repo }}{% endraw %}/archive/v{{ site.version }}.zip">Download</a>
```

to this:

```html
<a class="sidebar-nav-item" href="{% raw %}{{ site.github.repo }}{% endraw %}/archive/master.zip">Download</a>
```

## RSS

Lanyon comes with a generated RSS file, `atom.xml`. All you have left to do is link to it where necessary. As an example, I have added a link to the RSS feed on the second row of the contact list. 

## Closing Notes

I hope this gives a little insight into the use of Jekyll, Poole, and Lanyon in bootstrapping and customizing a personal site on Github Pages. For further reading, please refer to the [links at the top of this post](#resources).