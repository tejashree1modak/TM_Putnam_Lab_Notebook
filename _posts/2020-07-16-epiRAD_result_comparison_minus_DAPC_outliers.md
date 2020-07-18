---
layout: post
title: Comparison of results for filtered epiRAD data without outliers identified by DAPC  
tags: [ ddRAD, epiRAD, Moorea, methylation, filter, outliers ]
---

## Comparison of results for the following data after adding an additional filter (Filter2b) for removing **outlier samples identified by DAPC** and rerunning the full epiRAD pipeline. 
**Number of individuals left after this additional filter is 33.**

1. Filter4: Data obtained post BLAST filter, low read filter and low coverage filter 
2. Filter 5a: Data obtained post filter4 AND removing problematic loci identified by rad_haplotyper 
3. Filter 5b: Data obtained post filter4 AND keeping only those loci that remain after full SNP filtering pipeline

| Filter#  | Number of loci| Methylation cutoff |
|----------|-------------|----------------------|
| 4        |  7795       | -2.848               |
| 5a       |  6809       |  -2.883959           |
| 5b       |  5912       |   -2.830382          |

## Result1: MDS without dapc outliers

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:------:
![]({{site.baseurl}}/images/epiRAD_analysis_out/post_fil2b/Filter4_mds2.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/post_fil2b/Filter5a_mds2.png) | ![]({{site.baseurl}}/images/epiRAD_analysis_out/post_fil2b/Filter5b_mds2.png)

## Result2: Methylation heatmap clustered by rows and columns without dapc outliers

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:------:
![]({{site.baseurl}}/images/epiRAD_analysis_out/post_fil2b/Filter4_MethylHeatMap.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/post_fil2b/Filter5a_MethylHeatMap.png) | ![]({{site.baseurl}}/images/epiRAD_analysis_out/post_fil2b/Filter5b_MethylHeatMap.png)

## Result3: %Methylation without dapc outliers
ANOVA for % methylation per site is not significant.

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:------:
![]({{site.baseurl}}/images/epiRAD_analysis_out/post_fil2b/Filter4_percnt_CpGmethyln_bysite.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/post_fil2b/Filter5a_percnt_CpGmethyln_bysite.png) | ![]({{site.baseurl}}/images/epiRAD_analysis_out/post_fil2b/Filter5b_percnt_CpGmethyln_bysite.png)

## Result5a: Pst 

|         | Filter4    | Filter5a | Filter5b  |
|---------|------------|----------|-----------|
Mean Pst| 0.127| 0.132|0.132|

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:----------:
![]({{site.baseurl}}/images/epiRAD_analysis_out/post_fil2b/Filter4_Pst.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/post_fil2b/Filter5a_Pst.png) | ![]({{site.baseurl}}/images/epiRAD_analysis_out/post_fil2b/Filter5b_Pst.png)

## Result5b: Pairwise Pst 

<table>
<tr><th>Table 1 Filter4</th><th>Table 2 Filter5a</th><th>Table3 Filter5b</th></tr>
<tr><td>

|     | EOB | PBF   | WOB   | WOF   |
|-----|-----|-------|-------|-------|
| EOB | x   | 0.217 | 0.053 | 0.02  |
| PBF |     | x     | 0.2 | 0.218 |
| WOB |     |       | x     | 0.072 |
| WOF |     |       |       | x     |

</td><td>

|     | EOB | PBF   | WOB   | WOF   |
|-----|-----|-------|-------|-------|
| EOB | x   | 0.22 | 0.055 | 0.018 |
| PBF |     | x     | 0.199 | 0.219 |
| WOB |     |       | x     | 0.075 |
| WOF |     |       |       | x     |

</td><td>

|     | EOB | PBF   | WOB   | WOF   |
|-----|-----|-------|-------|-------|
| EOB | x   | 0.22 | 0.055 | 0.018 |
| PBF |     | x     | 0.199 | 0.219 |
| WOB |     |       | x     | 0.075 |
| WOF |     |       |       | x     |

</td></tr> </table>

## Result5c: Pooled Back Reef vs Pooled Fringe Reef Pst

|         | Filter4    | Filter5a | Filter5b  |
|---------|------------|----------|-----------|
Mean Pst|0.053 | 0.053|0.053|


## find.clusters 

`find.clusters` identifies one cluster for data post Filter4,5a,5b.

## PERMANOVA

**by site**

|         | Filter4    | Filter5a | Filter5b  |
|---------|------------|----------|-----------|
R2|0.12809 | 0.12993|0.12993|
Pvalue|0.011 | 0.011|0.007|


**by loc**

|         | Filter4    | Filter5a | Filter5b  |
|---------|------------|----------|-----------|
R2|0.06397 | 0.06215|0.6215|
Pvalue|0.001 | 0.002|0.003|
