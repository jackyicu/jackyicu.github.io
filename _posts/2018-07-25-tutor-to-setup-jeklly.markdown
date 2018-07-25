---
layout: post
title:  "Tutorial to setup jekyll"
date:   2018-07-25 12:39:10 +0800
categories: jekyll update
---

This tutorial is based on macOS High Sierra.

# Requirements
1. Homebrew
2. Ruby
3. Bundler
4. jekyll
5. Visual Studio Code

# Install jekyll
1. Open Visual Studio Code
2. Turn to terminal and type the following command:
```
brew install ruby
gem install bundler
```
3. Create a new file named Gemfile and add these lines
```
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```
4. Type the commands:
> `bundle install`
5. Create a new jekyll repo with commands:
> `bundle exec jekyll new username.github.io
cd username.github.io`
6. Edit Gemfile, put '#' before
> ` "jekyll", "3.3.0"`

7. Remove '#' before
> `gem "github-pages", group: :jekyll_plugins`

# Publish
1. Type the following commands to publish it on github page:
```
git init
git remote add origin https://github.com/username/username
git add .
git commit -m "update site"
git push -u origin master
```

2. Go to check your website at username.github.io

# Update
1. Simply type the command:
> `bundle update`
