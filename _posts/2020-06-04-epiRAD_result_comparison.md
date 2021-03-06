---
layout: post
title: Comparison of results for  epiRAD data filtered in three steps 
tags: [ ddRAD, epiRAD, Moorea, methylation, filter ]
---

## Comparison of results for 
1. Filter4: Data obtained post BLAST filter, low read filter and low coverage filter 
2. Filter 5a: Data obtained post filter4 AND removing problematic loci identified by rad_haplotyper 
3. Filter 5b: Data obtained post filter4 AND keeping only those loci that remain after full SNP filtering pipeline

| Filter#  | Number of loci| Methylation cutoff | MDS outlier |
|----------|-------------|----------------------|-------------|
| 4        |  7006       | -2.822               | PBF_158     |
| 5a       |  6101       |  -2.863801           | PBF_158     |
| 5b       |  5579       | -2.870767            | PBF_158     |

## Result1: MDS with all samples

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:------:
![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter4_mds.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter5a_mds.png) | ![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter5b_mds.png)

## Result2: MDS without outlier PBF_158

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:------:
![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter4_mds_minus_outlier.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter5a_mds_minus_outlier.png) | ![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter5b_mds_minus_outlier.png)

## Result3: Methylation heatmap clustered by column

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:------:
![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter4_MethylHeatMap.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter5a_MethylHeatMap.png) | ![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter5b_MethylHeatMap.png)

## Result4a: % Methylation 

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:------:
![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter4_percent_CpGmethyln.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter5a_percent_CpGmethyln.png) | ![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter5b_percent_CpGmethyln.png)

## Result4b: % Methylation per site
There is no significant difference between sites.

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:------:
![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter4_percnt_CpGmethyln_bysite.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter5a_percnt_CpGmethyln_bysite.png) | ![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter5b_percnt_CpGmethyln_bysite.png)

## Result5a: Pst 

|         | Filter4    | Filter5a | Filter5b  |
|---------|------------|----------|-----------|
| Mean Pst| 0.00440542 | 0.01522  | 0.01963305|

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:----------:
![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter4_Pst.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter5a_Pst.png) | ![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter5b_Pst.png)

## Result5b: Pst minus outliers 
Outliers removed include PBF_158, WOF_232, WOF_236 and WOB_41.

|         | Filter4    | Filter5a     | Filter5b  |
|---------|------------|--------------|-----------|
| Mean Pst| -0.01028157| 0.003816915  | 0.01479802|

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:----------:
![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter4_Pst_minus_outlier.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter5a_Pst_minus_outlier.png) | ![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter5b_Pst_minus_outlier.png)

## Result5c: Pairwise Pst 

|          | Filter4    | Filter5a     | Filter5b  |
|----------|------------|--------------|-----------|
| Mean Pst1|0.009522026 | 0.01080664   | 0.01420777|
| Mean Pst2| 0.01047574 | 0.02351662   |0.0313601 4|

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:----------:
![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter4_Pst_pair1.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter5a_Pst_pair1.png) | ![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter5b_Pst_pair1.png)
![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter4_Pst_pair2.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter5a_Pst_pair2.png) | ![]({{site.baseurl}}/images/epiRAD_analysis_out/Filter5b_Pst_pair2.png)

