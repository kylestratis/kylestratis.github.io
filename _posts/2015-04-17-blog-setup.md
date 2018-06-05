---
layout: post
title: Setting Up an Elegant Blog with Github Pages, Jekyll, and Poole; Part I
comments: true
tags: [ web, tutorial, markdown  ]
---

Recently, as an extension of my [note-taking obsession]({% post_url 2015-04-06-sublime-markdown %}), I decided to start this blog, primarily to share what I've learned the hard way. I already had my domain name [registered via Namecheap](https://www.namecheap.com/?aff=84217) ([non-ref](https://www.namecheap.com)), so it was time to find hosting. Luckily, Github offers [free hosting](https://pages.github.com/) with support for [Jekyll](https://jekyllrb.com/). Jekyll is a Ruby-based static site generator that authoring easy by automatically building Markdown files, but remains powerful enough to create all sorts of site customizations.

In this tutorial, I will walk you through the steps I took and the resources I used to build this blog, the first undertaking of its kind for me. There were many tools that made setup easy, but it was still enough work that it was a fun and enlightening process. 

To begin with Github pages, you will have to create a repo on Github entitled _yourname_.github.io. This will be your URL if you don't register a custom domain, but having your own domain is always nice. It takes just a few extra steps, but is worth it for the professional look it offers your site.  

## Setting Up Poole

The first step is to get [Poole](https://getpoole.com/). This site uses the minimalist [Lanyon](https://github.com/poole/lanyon) theme, which keeps navigation in a collapsible sidebar. Poole on its own is described as a butler for Jekyll, which is really a great analogy: it provides a vanilla install of Jekyll, setting up many of the folders that Jekyll will use to generate your site. Follow the instructions at the Poole website to install the gemfile, then clone down the empty repository you made, go to the repo for the theme you want and download the provided archive. Extract that to your local repo and push it to your remote, and you're all set with Poole!

## Setting Up a Custom URL 

Github offers two sets of instructions for setting up your domain depending on whether you are using an [apex domain or subdomain](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/). To set up the appropriate records with Namecheap specifically, navigate to the Manage Domains page, select the domain you wish to set the record for, and click the 'Edit Selected' button. Now, on the left navigation pane, click the 'All Host Records' link. On this page, you will need to set two `A` records for hostname `@`, one to `192.30.252.153` and the other `192.30.252.154`. You will also need to set a `CNAME` record for hostname `www` to your Github Pages URL (in my case `kylestratis.github.io`). 

When you have done this, all that is left is to edit the CNAME file (a blank one comes with Poole) to have your custom URL. Save the file and push it to your remote, and navigating to your blog via a custom URL should work shortly. 

## Setting Up Your Configuration

The main way to do basic configuration on your site is to edit your `_config.yml` file in the root of your repo. Here, you can set the markdown engine, code highlighting engine, and more. These will allow you to leverage the liquid templating system and customize the sidebar later. For an example `_config.yml` file, see [my config](https://github.com/kylestratis/kylestratis.github.io/blob/master/_config.yml). 

## Setting Up Your About Page

Poole comes with an example `about.md` page that gives you a general idea of how to leverage Markdown for the content of your page. What you will also notice is some information at the top of the page. This is the YAML frontmatter, and gives Jekyll some important information about your page (or post) that it will use when generating your site. Here is the default frontmatter in `about.md`: 

```
---
layout: page
title: About
---
```

`Layout` specifies which specific layout to use (they are located in your `_layouts` folder), in this case we are using a page layout, as opposed to a post layout. We can also specify the `title`. I didn't make any additional changes to the frontmatter here, the frontmatter is much more powerful (and useful) in the context of a blog post. 

Open up your local `about.md` in [your favorite text editor](https://sublimetext.com) if you haven't already, and write something up! Now, I'm sure you don't want to push every minor change to Github just to preview your changes, so instead of that fire up your Terminal and run `jekyll serve`. This will allow you to access your generated website at `localhost:4000` and will rebuild your site when any file is changed so that you can quickly view any edits you make before publishing. Play around, and when you're satisfied with your page, push it to your remote repo. 

## <a name="firstpost"></a>Setting Up Your First Post

The primary difference between a post and a page is the location of a post (they will be put in your `_posts` folder) and the filename, which will be the date followed by the title, e.g. `2015-04-06-sublime-markdown.md` (for my excellent [previous post]({% post_url 2015-04-06-sublime-markdown %})). You can also take advantage of more YAML variables here, such as `tags` and `category`. Go ahead and write an introductory post and give it some tags! To preview your post, fire up your terminal, navigate to your local repo for the site, and run `jekyll serve`. Like above, this command will build and serve your site, allowing you to view it at `localhost:4000`. When you want to publish (you can go ahead and publish what you've written now, or write another post later), use git to `add` your files to the staging area, `commit` them, and then `push` them to your remote repo. 

## Setting Up Drafts and .gitignore

Another handy feature is the ability to save drafts. Instead of saving a dated markdown file to the `_posts` folder, save an undated markdown file (e.g. `ruby-blog-first-draft.md`) to the `_drafts` folder. In order to preview, run `jekyll serve --drafts`. When you are ready to publish the post, rename it according to the convention [above](#firstpost) and move it to your `_posts` folder. 

Before you push anything to your remote (and public) Github repo, it may be wise to create a `.gitignore` file. Like the filename says, this file tells git which files to ignore so that they don't show up in your public repo. Simply add the name of a specific file or files (by using asterisks as wildcards) to its own line. For a template, feel free to refer to [my own .gitignore file](https://github.com/kylestratis/kylestratis.github.io/blob/master/.gitignore). The most important thing for me was to not share my `_drafts` folder, so that I could both keep my commits clean (and not have dozens of draft edits being pushed along with a major page overhaul) and to keep post ideas private until they are finished, polished, and ready for the world to see. Read more about `.gitignore` [here](https://git-scm.com/docs/gitignore).

That is it for part 1 of this guide, please check back again soon for Part 2, where I will cover more customizations and other blogs that helped me set mine up. 