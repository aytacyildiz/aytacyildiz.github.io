---
layout: article
title: Sublime Jekyll
categories: kodlama
description: A Sublime Text package for [Jekyll](http://jekyllrb.com/) static sites.
---

A Sublime Text package for [Jekyll](http://jekyllrb.com/) static sites. This began as a fork of the [liquid-syntax-mode](https://github.com/siteleaf/liquid-syntax-mode) repo from siteleaf. This package should help creating Jekyll sites and posts easier by providing access to key template tags and filters, as well as common completions and a current date/datetime command (for dating posts). Some of the concepts for the date commands were borrowed from the [sublime-insertdate](https://github.com/FichteFoll/sublimetext-insertdate) repo from FichteFoll.

## Installation

### Package Control

You can install this package using [Package Control](https://sublime.wbond.net/packages/Jekyll) from wbond.net.

* Press `ctrl+shift+p` (Windows/Linux) or `command+shift+p` (OS X) to bring up the Command Palette (or use _Tools > Command Palette_ menu)
* Type to search for the `Package Control: Install Package` command
* Search packages for **Jekyll** and hit `enter` to install
* You may need to restart in order to use this package

### Manual

[Clone](https://github.com/23maverick23/sublime-jekyll.git) or [download](https://github.com/23maverick23/sublime-jekyll/archive/master.zip) the contents of this repo into your Sublime Text `Packages` folder.

* OS X: `~/Library/Application\ Support/Sublime\ Text\ 3/Packages`
* Windows: `%APPDATA%\Sublime Text 3\Packages`
* Linux: `~/.config/sublime-text-3/Packages`

## Resim Denemeleri
![Kod](/images/header.png)
<img src="/images/header.png" alt="Kod" class="pure-img">
[<img src="/images/header.png" alt="Kod" class="pure-img">](/images/header.png)

## Kod örnekleri
{% highlight ruby %}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% endhighlight %}
{% highlight ruby %}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb show.html.erb show.html.erb show.html.erb show.html.erb show.html.erb show.html.erb show.html.erb show.html.erb show.html.erb
    format.json { render json: @widget }
  end
end
{% endhighlight %}