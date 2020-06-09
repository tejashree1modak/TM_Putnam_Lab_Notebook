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
![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/epiRAD_analysis_out/Filter4_mds.png)  |  ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/epiRAD_analysis_out/Filter5a_mds.png) | ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/epiRAD_analysis_out/Filter5b_mds.png)

## Result2: MDS without outlier PBF_158

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:------:
![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/epiRAD_analysis_out/Filter4_mds_minus_outlier.png)  |  ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/epiRAD_analysis_out/Filter5a_mds_minus_outlier.png) | ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/epiRAD_analysis_out/Filter5b_mds_minus_outlier.png)

## Result3: Methylation heatmap clustered by column

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:------:
![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/epiRAD_analysis_out/Filter4_MethylHeatMap.png)  |  ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/epiRAD_analysis_out/Filter5a_MethylHeatMap.png) | ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/epiRAD_analysis_out/Filter5b_MethylHeatMap.png)

## Result4: % Methylation 

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:------:
![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/epiRAD_analysis_out/Filter4_percent_CpGmethyln.png)  |  ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/epiRAD_analysis_out/Filter5a_percent_CpGmethyln.png) | ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/epiRAD_analysis_out/Filter5b_percent_CpGmethyln.png)

## Result5: Pst

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:------:
![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/epiRAD_analysis_out/Filter4_Pst.png)  |  ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/epiRAD_analysis_out/Filter5a_Pst.png) | ![](https://github.com/tejashree1modak/TM_Putnam_Lab_Notebook/blob/master/images/epiRAD_analysis_out/Filter5b_Pst.png)
