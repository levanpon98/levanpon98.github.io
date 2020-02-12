---
title: 'Image processing (part 1)'
date: 2020-02-12
permalink: /posts/2020/02/mage_processing_part_1/
tags:
  - computer vision
  - image processing
---

Wellcome to my "Image processing series", in this post, i will intoduce some image processing operators that map pixel values from one image to another. 
We begin with the simplest kind of image transforms, namely those that manipulate each pixel independently of its neighbors. Next, we examine *neighborhood* (area-based) operators, where each new pixel's value depends on a small number of neighboring input values. Another important class of global operators are *geometric transformations*, such as rotations, shears, and perspective deformations. Finally, i will introduce *global optimization* approaches to image processing, which involve the minimization of an energy functional or equivalently, optimal estimation using Bayesian Markov random field models

1. Point operatiors
The simplest kinds of image processing transforms are point operators, where each output pixel’s value depends on only the corresponding input pixel value (plus, potentially, some globally collected information or parameters)
