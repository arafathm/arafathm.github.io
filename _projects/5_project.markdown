---
layout: page
title: '<font style="color:blue;">Deep/Machine Learning</font> for Organ Functionality Assessment'
description: Segmentation-free Kidney Volume Estimation
img: /assets/img/r5_cover.png
importance: 3
---

The economic burden of chronic kidney disease (CKD) is significant, estimated in Canada in 2007 at $1.9 Billion just for patients with end-stage renal disease (ESRD). In 2011, about 620,000 patients in United States received treatment for ESRD either by receiving dialysis or by receiving kidney transplantation. ESRD is the final stage of different CKDs, e.g., Autosomal dominant polycystic kidney disease (ADPKD), renal artery atherosclerosis (RAS), which are associated with the change of kidney volume. However, detection of CKDs are complicated; multiple tests such as the estimated glomerular filtration rate (eGFR) and serum albumin-to-creatinine ratio may not detect early disease and may be poor at tracking progression of disease. Recent works have suggested kidney volume as the potential surrogate marker for renal function and is thus useful for predicting and tracking the progression of different CKDs. In fact, the total kidney volume has become the gold-standard image biomarker for the ADPKD and RAS progression at early stages of this disease. In addition, the renal volumetry has recently emerged as the most suitable alternative to renal scintigraphy in evaluating the split renal function in kidney donors as well as the best biomarker in follow-up evaluation of kidney transplants. Consequently, estimation of the ‘volume’ of a kidney has become the primary objective in various clinical analyses of kidney. Traditionally, the kidney volume is estimated by means of segmentation. However, existing kidney segmentation algorithms have various limitations (e.g., requiring user interaction, sensitivity to parameter setting, heavy computation). Therefore, in this project, primarily, we proposed a segmentation-free, supervised learning approach that addresses the challenges of accurate kidney volume estimation caused by extensive variations in kidney shape, size and orientation across subjects. We develop dual regression forests to simultaneously predict the kidney area per image slice, and kidney span per image volume. In our subsequent work, we further improved the segmentation-free volume estimation performance by incorporating deep CNN that skips the segmentation procedure. To the best of our knowledge, our segmentation-free method is the first that uses deep CNN for
kidney volume estimation. We estimate slice-based cross-sectional kidney areas followed by integration over these values across axial kidney span to produce the volume estimate. We also shoed that FCN performs better than a CNN of equivalent number of parameters in regression-based organ area estimation. 

<strong>Segmentation-Free Estimation of Kidney Volumes using Dual Regression Forests</strong>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/r5_fig1.png' | relative_url }}" alt="" title="example image"/>
    </div>
</div>
<div class="caption">
    Fig. 1: Flowchart and associated schematic diagrams showing different components of the proposed dual regression-forests method.
</div>
Regression forest 1 (Fig. 1) learns the correspondence between input features and kidney areas for training subpatches, and then predicts kidney areas in unseen subpatches. The distribution of estimated kidney area values vs. subpatches for a kidney sample is shown at the bottom in Fig. 1 (left most). However, due to extensive variation in kidney shapes, sizes and orientations across subjects, we observed that non-zero volumes are predicted for areas devoid of kidney tissue. These false positives are removed using a spatial filter (Fig. 1, second from the left at the bottom) having an extent (or bandwidth) equal to a spatial kidney span measure (along superior-inferior direction). This important span parameter is learnt by forest 2. For training forest 2, we use the same features. We define a unit step function whose spatial bandwidth is equivalent to the span predicted by forest 2 for a particular kidney sample. We approximate the most probable kidney span in the false positives-corrupted distribution by calculating the cross-correlation between distribution and span filter. Finally, we estimate the volume of a kidney by integrating the areas in the axial direction.


<strong>Segmentation-Free Estimation of Kidney Volumes using Deep Learning</strong>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/r5_fig2.png' | relative_url }}" alt="" title="example image"/>
    </div>
</div>
<div class="caption">
    Fig. 2: Segmentation-free kidney volume estimation using deep CNN (top) and FCN (bottom).
</div>
<b>CNN-based Approach:</b> We estimate the cross-sectional area of a kidney in each slice using a deep CNN shown in Fig. 2(top). The CNN performs regression and has seven layers excluding the input. It has four convolutional layers, three fully connected layers, and one Euclidean loss layer. We also use dropout layers along with the first two fully connected layers in order to avoid over-fitting. As mentioned earlier, the input is a 120×120 pixel image patch and the output is the ratio of kidney pixels to the total image size. The CNN is trained by minimizing the Euclidean loss between the desired and predicted values. Once the CNN model is trained, we deploy the model to predict the kidney area in a particular image patch. Finally, the volume of a particular kidney is estimated by integrating the predicted areas in all of its image patches in the axial direction.

<b>FCN-based Approach:</b> We use an FCN (Fig. 2, bottom) to predict the crosssectional area of a kidney in each patch. Our FCN is a regression network consisting of six layers, excluding the input. It has five convolutional layers, one fully connected layer (only to generate a single activation), and one Euclidean loss layer. To avoid overfitting, we use the dropout in the last convolution layer. During inference, the FCN predicts the kidney area in a particular image patch. Finally, we calculate a particular kidney’s volume by adding the FCN-predicted areas for all of its axial image patches and multiplying by the voxel dimensions.

<strong>Data</strong>

We used 100 patients’ CT scans accessed from the Vancouver General Hospital (VGH) records with required ethics approvals by the UBC Clinical Research Ethics Board (CREB), certificate number: H15-00237. There were a total of 200 kidney samples, and we used 130 samples (from 65 randomly chosen patients) for training, 20 samples (from 10 randomly chosen patients) for validation, and the remaining 50 samples for testing. Our dataset included 12 pathological
kidney samples (with endo- and exophytic tumors), and our training and test data contained six pathological cases each. We made sure that kidneys from the same patient were not split across the training, validation, and test cases. These data were acquired using a Siemens SOMATOM Definition Flash
(Siemens Healthcare GmbH, Erlangen, Germany) CT scanner. Ground truth kidney bounding boxes were calculated from manual kidney delineation performed by an expert radiologist.

We also used 210 patients’ CT scans from the 2019 Kidney Tumor Segmentation (KiTS) Challenge database. This database contains patients’ scans accessed from the University of Minnesota Medical Center records. These patients underwent partial or radical nephrectomy for one or more kidney tumors between 2010 and 2018. We used 160 randomly chosen patients’ data for training, 15 randomly chosen patients’ data for validation, and the remaining 35 patients data (70 kidney samples) for testing. Here also, we made sure that kidneys from the same patient were not split into the training, validation, and test cases. We also collected the kidney segmentation data from the same database.

<strong>Results</strong>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        <img class="img-fluid rounded z-depth-1" src="{{ '/assets/img/r5_fig3.png' | relative_url }}" alt="" title="example image"/>
    </div>
</div>
<div class="caption">
    Fig. 3: Kidney volume estimation performance by different methods. The result for our dual regression-forests method (published in 2016) is shown with Red box. The result for our CNN-based method (published in 2017) is shown with Green box. The results by our latest FCN-based work (accepted in 2021) are indicated with Blue box.
</div>

<strong>For Details</strong>

Please read our papers [[1](https://ieeexplore.ieee.org/abstract/document/9358223?casa_token=rxZNi4GaP-YAAAAA:vlaAvOf6J1pKBT9goM4k0cCgPyJQ9NgOg_SSzt4iAFwHINOSelv-LsPXU44-XYmkME_wsI8)], [[2](https://link.springer.com/chapter/10.1007/978-3-319-66179-7_70)], [[3](https://link.springer.com/chapter/10.1007/978-3-319-47157-0_19)].