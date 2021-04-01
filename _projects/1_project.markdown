---
layout: page
title: Radiomics with Deep Learning
description: Learnable Image Histogram for Cancer Analysis
img: /assets/img/r1_cover.png
importance: 1
---

Fuhrman cancer grading and tumor-node-metastasis (TNM) cancer staging systems are typically used by clinicians in the treatment planning of renal cell carcinoma (RCC), a common cancer in men and women worldwide. Pathologists typically use percutaneous renal biopsy for RCC grading, while staging is performed by volumetric medical image analysis before renal surgery. Recent studies suggest that clinicians can effectively perform these classification tasks non-invasively by analysing image texture features of RCC from computed tomography (CT) data. However, image feature identification for RCC grading and staging often relies on laborious manual processes, which is error prone and time-intensive. To address this challenge, this paper proposes a learnable image histogram in the deep neural network framework, named "ImHistNet", that can learn task-specific image histograms with variable bin centers and widths. The proposed approach enables learning statistical context features from raw medical data, which cannot be performed by a conventional convolutional neural network (CNN). The linear basis function of our learnable image histogram is piece-wise differentiable, enabling back-propagating errors to update the variable bin centers and widths during training. This novel approach can segregate the CT textures of an RCC in different intensity spectra, which enables efficient Fuhrman low (I/II) and high (III/IV) grading as well as RCC low (I/II) and high (III/IV) staging. 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/r1_fig1.png' | relative_url }}" alt="" title="example image"/>
    </div>
</div>
<div class="caption">
    The graphical representation of the architecture of our learnable image histogram using CNN layers. We also break down our piece-wise linear basis function <b>H<sub>b</sub><sup>x</sup></b> on top of the figure in relation to different parts of the learnable image histogram architecture.
</div>

<strong>Learnable Image Histogram</strong>\
Our proposed learnable image histogram (LIH) stratifies the pixel values in an image <b>x</b> into different learnable and possibly overlapping intervals (bins of width <b>w<sub>b</sub></b>) with arbitrary learnable means (bin centers <b>β<sub>b</sub></b>). Given a 2D image (or a 2D region of interest or patch) <b>x: R<sup>2</sup>→R</b>, the feature value <b>h<sub>b</sub><sup>x</sup>: b ∈ B→R</b>, corresponding to the number of pixels in <b>x</b> whose values fall within the <b>b<sup>th</sup></b> bin, is estimated as:

<b>h<sub>b</sub><sup>x</sup> = Φ{H<sup>x</sup><sub>b</sub>} = Φ{max(0, 1−|x−β<sub>b</sub>| × w<sub>b</sub>)}</b>,

where <b>B</b> is the set of all bins, <b>Φ</b> is the global pooling operator, <b>H<sub>b</sub><sup>x</sup></b> is the piece-wise linear basis function that accumulates positive votes from the pixels in $x$ that fall in the b>b<sup>th</sup></b> bin of interval <b>[β<sub>b</sub>-w<sub>b</sub>/2,β<sub>b</sub>+w<sub>b</sub>/2]</b>, and <b>w<sub>b</sub></b> is the width of the <b>b<sup>th</sup></b> bin. Any pixel may vote for multiple bins with different <b>H<sub>b</sub><sup>x</sup></b> since there could be an overlap between adjacent bins in our learnable histogram. The final <b>|B|×1</b> feature values from the learned image histogram are obtained using a global pooling <b>Φ</b> over each <b>H<sub>b</sub><sup>x</sup></b> separately.


<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/r1_fig2.png' | relative_url }}" alt="" title="example image"/>
    </div>
</div>
<div class="caption">
    Multiple instance decisions aggregated ImHistNet for RCC grade and stage classification. The light green block represents the proposed LIH layer shown in the previous figure.
</div>

<strong>ImHistNet Classifier Architecture</strong>\
The classification network comprises ten layers: the LIH layer, five (F1-F5) fully connected layers (FCLs), one softmax layer, one average pooling (AP) layer, and two thresholding layers. The first seven layers contain trainable weights. The input is a 64×64 pixel image patch extracted from the kidney+RCC slices. During training, we fed randomly shuffled image patches individually to the network. The LIH layer learns the variables <b>β<sub>b</sub></b> and <b>w<sub>b</sub></b> to extract characteristic textural features from image patches. In implementing the proposed ImHistNet, we chose <b>B = 128</b> and "average" pooling at <b>H<sub>b</sub><sup>x</sup></b>. We set subsequent FCL (F1-F5) size to 4096×1. The number of FCLs plays a vital role as the model's overall depth is important for good performance. Empirically, we achieved good performance with five FCL layers. Layers 8, 9, and 10 of the ImHistNet are used during the testing phase and do not contain any trainable weights.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/1.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/3.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/5.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/5.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
</div>
<div class="caption">
    This image can also have a caption. It's like magic.
</div>

You can also put regular text between your rows of images.
Say you wanted to write a little bit about your project before you posted the rest of the images.
You describe how you toiled, sweated, *bled* for your project, and then... you reveal it's glory in the next row of images.


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/6.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/11.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>


The code is simple.
Just wrap your images with `<div class="col-sm">` and place them inside `<div class="row">` (read more about the <a href="https://getbootstrap.com/docs/4.4/layout/grid/" target="_blank">Bootstrap Grid</a> system).
To make images responsive, add `img-fluid` class to each; for rounded corners and shadows use `rounded` and `z-depth-1` classes.
Here's the code for the last row of images above:

```html
<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/6.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/11.jpg' | relative_url }}" alt="" title="example image"/>
    </div>
</div>
```
