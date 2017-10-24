---
layout: default
title:  "Heavy batch operations on images"
date:   2017-10-24 08:08:26 +0100
categories: programming languages
---

# Imagicks
Convert all images from current folder proportionally.

for file in *.jpg; do convert $file -resize 1000x800 $file; done

for file in *.jpg; do convert $file -resize 1000x800 -quality 95 -rotate 180 -charcoal 4 $file-rotated; done
