---
layout: page
title: Compressive Sensing
description: Compressively Sensed Ultrasound Radio-frequency Data Reconstruction
img: /assets/img/cs_cover.png
importance: 4
---

Ultrasound (US) imaging has become an essential part of clinical routine that produces real-time images of patient anatomy. As a non-ionizing and low-cost modality, US has a number of advantages over other medical imaging modalities like non-invasiveness, portability, and versatility. However, handling a large amount of US data during real-time imaging as well as its transmission at low bit rate (and without any perceived loss of image quality) in tele-medicine are considered limiting factors.

The recently introduced compressive sensing (CS) theory allows to recover a signal sampled below the Nyquist sampling limit under certain assumptions. CS provide optimized ultrasound imaging solutions that also has the potential to offer a coherent framework for image analysis, object detection, and information extraction. CS can also improve efficiency of triplex acquisitions for CFM/B-mode/Doppler or 3D imaging using matrix arrays. So far, a number of sparsifying bases for the reconstruction of compressively sensed US have been proposed in literature like the Fourier, wavelets, wave atoms, curvelets, and Bayesian bases. However, all of these bases have various limitations. In this project, we proposed a novel reconstruction method for the compressively sensed ultrasound RF data using the combined curvelets- and wave atoms-based (CCW) orthonormal basis. We exploit the merits of both the sparsifying orthonormal bases via concatenating them where RF data is reconstructed from the larger coefficients of the combined basis. 


<strong>CCW-based Reconstruction Method</strong>

The primary target of the CCW-based reconstruction method is to recover the original signal <i>F</i> using a combined orthonormal sparsifying domain that consists of curvelets and wave atoms coefficients. This equation is an under-determined inverse problem. The solution of this equation would be the model that agrees with incomplete data <i><b>b</b></i> after being restricted by restriction operator <i><b>R</b></i>. We reformulate the problem according to the compressive sampling theory as <i><b>b = A</b>x</i> with <i><b>A = RS</b><sup>H</sup></i>, where <i><b>S =</b>C||W</i> is the sparsifying transform that catenates two different sparsifying bases namely curvelets <i>C</i> and wave atoms <i>W</i>, <i>||</i> sign denotes catenation operator, and <i><b>S</b><sup>H</sup> = C<sup>H</sup>||W<sup>H</sup></i>. Finally, for randomized subsampling, we can write <i><b>A</b><sup>H</sup>(b) = <b>A</b><sup>H</sup><b>A</b>x ≈ x + n</i>, where <i>n</i> represent the approximated additive white Gaussian noise due to the spectral leakage. The curvelets and wave
atoms transforms give a compressible representation of <i>s</i>, where <i>s</i> is the number of non-zero element in the sparsifying domain
and therefore called <i>s</i>-sparse. It is shown in a previous article that for a matrix <i><b>b = A</b></i> with a specified isometry constant of the so-called restricted isometry property, optimization problem in the previous equation can be solved as: <i>x˜ = argmin<sub>x</sub>||x||<sub>1</sub> s.t. <b>RS</b><sup>H</sup>x = <b>b</b></i>.


<strong>Data</strong>

We use three sets of in vivo US data from patients undergoing open surgical RF thermal ablation for primary or secondary liver cancer and proper prior consent was obtained. US data were acquired using a RITA Model 1500 XRF generator (Rita Medical Systems, Fremont, CA) at a transducer center frequency, f0 = 7.27MHz and sampling frequency, fs = 40MHz. The study was approved by an institutional review board.

<strong>Results</strong>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/cs_fig1.png' | relative_url }}" alt="" title="example image"/>
    </div>
</div>
<div class="caption">
    Fig. 1: Illustration of the RF data reconstruction performance of different methods using 3 sets of in vivo data. (a)-(c) Actual and estimated B-mode images from the reconstructed RF data (80% subsampled), (d)-(f) NMSE of the reconstructed RF data, (g)-(i) NMSE of the estimated B-mode images from the reconstructed RF data, and (j)-(l) MSSIM of the estimated B-mode images from the reconstructed RF data.
</div>

<strong>For Details</strong>

Please read our paper for details [[1](https://ieeexplore.ieee.org/abstract/document/7428257?casa_token=XICEk4II6TIAAAAA:g1EyVRJBif0dyvwfNNe9xHFZZvjfLYcwee5A-FKCcQvPHnkxzFUwhTN5IcmZzRowekltrJs)].