---
layout: post
title:  ddRAD data analysis for filtered SNPs  
tags: [ ddRAD, Moorea, SNP ]
---

## Pop Gen Analysis
dDocent was used for QC, assembly, mapping and SNP calls on raw ddRAD data. 
dDocent SNP filtering pipeline plus rad haplotyper was used for filtering SNPs. 
Input file: SNP.DP3g95p5maf001.HWE.filtered.vcf.gz

## Outlier detection
[pcadapt](https://bcm-uga.github.io/pcadapt/articles/pcadapt.html) provides statistical tools for outlier detection based on Principal Component Analysis (PCA)

1. Choosing the number of principal components:
The ideal pattern in a scree plot is a steep curve followed by a bend and a straight line. Eigenvalues corresponding to population structure lie on the steep curve. By Cattell's rule it is recommended to keep PCs that correspond to eigenvalues to the left of the straight line. K=2 was the choice made. 
![Percentage of variance explaned by each PC](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/screeplot.png
)

2. PCA based on scores
![pca](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/pca.png)
 Looking at scores the outliers are: WOF217, PBF165, PBF167, PBF168
 Generally PC1 splits samples by back and fringe reef but some EOB/WOB samples wind up in fringe and one PBF160 sample in the back reef group.

3. SNP distribution
![Manhattan plot](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/manhattan.png)

4. Distribution of pvalues
![Expected vs Observed pvalues](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/Q-Qplot.png)

5. Histogram of pvalues
Excess small pvalues indicates presence of outliers
![Histogram of pvalues](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/hist.png)

6. Histogram of the Mahalanobis distance
This is a test statistic for detecting outlier SNPs that uses a multi-dimensional approach that measures how distant is a point from the mean.
![Statistic distribution](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/statdist.png)

## Fst

1. fst for all individuals together
fstat function from hierfstat R package was used to calculate Fst of all the data 
```shell
           pop       Ind
     Total 0.1675746 0.3774758
     pop   0.0000000 0.2521562
```

2. Pairwise Fst by location
This was calculated using the Nie method. All four locations were compared to each other. 
![Pairwise Fst by location](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/ddRAD_analysis_out/PairwiseFst_Nei.png)
