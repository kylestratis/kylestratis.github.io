---
layout: post
title: Sublime Markdown
category: productivity
tags: [ editor, markdown, notes ] 
comments: true
---

I take a lot of notes. Obsessively. Any time I'm writing code, I'm also writing prose: documenting every train of thought, code snippet, and the structure of the program I'm working on. For me, it's almost a form of cartography, mapping both my mind and the code. Originally, I did this all in Notepad in Windows and nano in Ubuntu. This left much to be desired: I couldn't easily show dead-end paths, Notepad is just ugly, displaying code snippets was clunky, and other small annoyances piled up constantly over time. Enter [Sublime Text](https://www.sublimetext.com/).

### The Editor

Sublime Text is a powerful, highly extensible, and beautiful text editor available for Windows, OSX, and all flavors of Linux. Powerful on its own, its usefulness is multiplied by the plugins available to it. There are two versions available, ST2 and ST3, the latter of which is in beta. Sublime on its own didn't solve all the problems I was having with my note-taking, but this is where its extensibility comes into play. 
There is rich support (via plugins) for [Markdown](https://help.github.com/articles/markdown-basics/), which is a great way to introduce structure and rich content to your notes, while providing the ease of use of using a plaintext editor. Starting this site (which uses Markdown built by [Jekyll](http://jekyllrb.com) to format posts) really got me excited about using Markdown in my everyday work, despite having used forms of it for quite some time on Reddit and Github both. 

### The Plugins

* [Package Control](http://wbond.net/sublime_packages/package_control) - The Sublime Text package manager, which is the most convenient way to install plugins. Simply copy the python script appropriate to your version of Sublime Text. To do this, open Sublime Text and press <kbd>Ctrl</kbd> + <kbd>`</kbd> to open the built-in python console. Paste the script and press <kbd>Enter</kbd> to run it. You can now access Package Control with <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd>.

* [Markdown Editing](https://github.com/SublimeText-Markdown/MarkdownEditing) - The main Markdown editing plugin, this provides syntax highlighting, autoclosure of special characters like <kbd>`</kbd>, <kbd>_</kbd>, and <kbd>*</kbd>, a bevy of keyboard shortcuts, and much more. It supports Markdown, [Github-Flavored Markdown](https://help.github.com/articles/github-flavored-markdown/) (my personal preference), and [MultiMarkdown](http://en.wikipedia.org/wiki/MultiMarkdown) as well. 

* [SmartMarkdown](https://github.com/demon386/SmartMarkdown) - This enables even more keyboard shortcuts to make you more productive if you're the memorizing type, along with headline folding and unfolding. 

* [Markdown Preview](https://github.com/revolunet/sublimetext-markdown-preview) - Markdown Preview, true to its name, allows you to preview your Markdown built as an HTML file, and can also save your built HTML file. This is especially useful for your notes, and less necessary if you are using markdown for software like Jekyll which automatically builds your markdown file. You can use either [Python Markdown](https://pythonhosted.org/Markdown/) or the [Github Markdown API](https://developer.github.com/v3/markdown/) to build your files. 

### The Installation

Thanks to Sublime Text's excellent Package Control installing these plugins is a breeze. Launch Package control with <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> and type 'Install Package' and then <kbd>Enter</kbd>. Now start typing the plugin name you wish to install, <kbd>Enter</kbd> again, and that's it! Repeat this process for each plugin you wish to install. 

![Package Control in Sublime Text]({{ site.url }}/assets/sublime-text-package-control.png)

### The Customization

Sublime Text is already a beautiful editor, but there is a rich environment of themes and color schemes available for your tinkering. Across all my installations, I like to use [Monokai Extended](https://github.com/jonschlinkert/sublime-monokai-extended) for the Monokai-Bright color scheme. Install this as you would any other plugin. On Windows, I prefer the default Sublime Text theme, but on Linux I like to use the [Soda Dark theme](http://buymeasoda.github.io/soda-theme/). 

### The Configuration

To configure Sublime Text and your extensions, simply go to `Preferences > Settings - User` (for Sublime) or `Preferences > Package Settings` (for your plugins) and then pick the package you wish to configure. All settings files are in JSON, and the default settings (which you should never edit, as these will get overwritten with every update) show you all the options you have for configuration. Below are examples from my own configuration:

#### Sublime Settings:

```json
{
    "theme": "Soda Dark 3.sublime-theme",
    "font_face": "ubuntu mono", 
    "font_size": 11,
    "tab_size": 4, 
    "translate_tabs_to_spaces": true
}
```

Note: These are only additions. You may have other settings set here by previously installed plugins. 

#### MarkdownEditing Settings:

```json
{
    "color_scheme": "Packages/Monokai Extended/Monokai Extended Bright.tmTheme",
    "line_numbers": true
}
```
 
The `color_scheme` setting overrides the themes that come with MarkdownEditing. 

#### Markdown Preview:

```json
{
    "parser": "github", 
    "enable_uml": true 
}
```

The `parser` setting forces the Markdown Preview parser to use the Github API for markdown parsing, enabling extra features. 

### The Other Plugins

* [GitGutter](http://www.jisaacks.com/gitgutter) - This allows you to see changes to the file you are working on in the gutter as compared to the file on on git. You can configure it to compare against HEAD (default behavior), or a particular branch, tag, or commit. 

* [SublimeCodeIntel](http://sublimecodeintel.github.io/SublimeCodeIntel/) - SublimeCodeIntel brings code autocomplete for a number of languages to Sublime Text. 

And that's it! Happy note-taking, blog-building, app-building, and everything else you're now using Sublime Text for!