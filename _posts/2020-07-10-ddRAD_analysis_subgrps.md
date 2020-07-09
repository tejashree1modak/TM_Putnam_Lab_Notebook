---
layout: post
title:  ddRAD data analysis for filtered SNPs in sample subgroups
tags: [ ddRAD, Moorea, SNP ]
---

## Comparison of results for subgroups of samples identified from DAPC analysis of full dataset 
1. Subgroup1 (30): EOB_174,EOB_175,EOB_185,EOB_189,EOB_190,EOB_192, PBF_157,PBF_158,PBF_161,PBF_164,PBF_169,PBF_171,PBF_172,PBF_489,PBF_490,PBF_491, WOB_35, WOF_224,WOF_225,WOF_232, WOF_234,WOF_236,WOF_237,WOF_238,WOF_239,WOF_240,WOF_241,WOF_243,WOF_244,WOF_245.  
2. Subgroup2 (20): EOB_177,EOB_178,EOB_182,EOB_183,EOB_184,EOB_186,EOB_188,EOB_191, PBF_160, WOB_41,WOB_42,WOB_45,WOB_47,WOB_48,WOB_49,WOB_50,WOB_59,WOB_60,WOB_62,WOB_65.

## Outlier detection: 

## 1. Choosing the number of principal components:

full data | subgrp1| subgrp2 
:-------------------------:|:-------------------------:|:------:
![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/screeplot.png)  |  ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/screeplot_subgrp1.png) | ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/screeplot_subgrp2.png)

## 2. PCA based on scores: 

full data | subgrp1| subgrp2 
:-------------------------:|:-------------------------:|:------:
![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/pca.png)  |  ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/pca_subgrp1.png) | ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/pca_subgrp2.png)

## 3. SNP distribution:

full data | subgrp1| subgrp2 
:-------------------------:|:-------------------------:|:------:
![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/manhattan.png)  |  ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/manhattan_subgrp1.png) | ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/manhattan_subgrp2.png)

## 4. Distribution of pvalues:

full data | subgrp1| subgrp2 
:-------------------------:|:-------------------------:|:------:
![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/Q-Qplot.png)  |  ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/Q-Qplot_subgrp1.png) | ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/Q-Qplot_subgrp2.png)

## 5. Histogram of pvalues:

full data | subgrp1| subgrp2 
:-------------------------:|:-------------------------:|:------:
![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/hist.png)  |  ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/hist_subgrp1.png) | ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/hist_subgrp2.png)

## 6. Histogram of the Mahalanobis distance:

full data | subgrp1| subgrp2 
:-------------------------:|:-------------------------:|:------:
![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/statdist.png)  |  ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/statdist_subgrp1.png) | ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/statdist_subgrp2.png)

## MDS

full data | subgrp1| subgrp2 
:-------------------------:|:-------------------------:|:------:
![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/MDS.png)  |  ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/MDS_subgrp1.png) | ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/MDS_subgrp2.png)
