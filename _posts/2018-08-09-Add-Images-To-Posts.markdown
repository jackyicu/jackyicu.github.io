---
layout: post
title:  "Add images to posts in jekyll"
date:   2018-08-09 10:10:00 +0800
categories: howto
---


If your jekyll website is hosted on github pages like mine, you may follow this tutorial to add photos to add images to your articles.

# Create folders for placing images

1. Create a new folder named `public` in  `root` folder.
2. Create a sub-folder named `img` in `public`.
3. Place the images in the `img` folder. Here I would place "addimage.jpg" in `img` folder.

# Refer to images in your markdown file

Link your images in your markdown file:

`![alt text for image](https://yourusername.github.io/public/img/imagelink.jpg)`

To show image in this post, the code should be:

`![add image](https://jackyicu.github.io/public/img/addimage.jpg)`

![add image](https://jackyicu.github.io/public/img/addimage.jpg)