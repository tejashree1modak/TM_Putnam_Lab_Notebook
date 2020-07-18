---
layout: post
title: Comparison of results for filtered epiRAD data without outliers  
tags: [ ddRAD, epiRAD, Moorea, methylation, filter, outliers ]
---

## Comparison of results for the following data after removing outlier samples
1. Filter4: Data obtained post BLAST filter, low read filter and low coverage filter 
2. Filter 5a: Data obtained post filter4 AND removing problematic loci identified by rad_haplotyper 
3. Filter 5b: Data obtained post filter4 AND keeping only those loci that remain after full SNP filtering pipeline

Outliers removed: PBF_158, WOF_232, WOF_236 and WOB_41.

| Filter#  | Number of loci| Methylation cutoff |
|----------|-------------|----------------------|
| 4        |  7006       | -2.822               |
| 5a       |  6101       |  -2.863801           |
| 5b       |  5579       | -2.870767            |

## Result1: MDS without outliers

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:------:
![]({{site.baseurl}}/images/epiRAD_analysis_out/minus_outliers/Filter4_mds.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/minus_outliers/Filter5a_mds.png) | ![]({{site.baseurl}}/images/epiRAD_analysis_out/minus_outliers/Filter5b_mds.png)

## Result2: Methylation heatmap clustered by rows and columns without outliers

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:------:
![]({{site.baseurl}}/images/epiRAD_analysis_out/minus_outliers/Filter4_MethylHeatMap_fil.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/minus_outliers/Filter5a_MethylHeatMap.png) | ![]({{site.baseurl}}/images/epiRAD_analysis_out/minus_outliers/Filter5b_MethylHeatMap.png)

## Result3: %Methylation without outliers

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:------:
![]({{site.baseurl}}/images/epiRAD_analysis_out/minus_outliers/Filter4_percnt_CpGmethyln_bysite.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/minus_outliers/Filter5a_percnt_CpGmethyln_bysite.png) | ![]({{site.baseurl}}/images/epiRAD_analysis_out/minus_outliers/Filter5b_percnt_CpGmethyln_bysite.png)

## Result5a: Pst 

|         | Filter4    | Filter5a | Filter5b  |
|---------|------------|----------|-----------|
Mean Pst| 0.054| 0.059|0.061|

Filter4             |  Filter5a                       | Filter5b
:-------------------------:|:-------------------------:|:----------:
![]({{site.baseurl}}/images/epiRAD_analysis_out/minus_outliers/Filter4_Pst.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/minus_outliers/Filter5a_Pst.png) | ![]({{site.baseurl}}/images/epiRAD_analysis_out/minus_outliers/Filter5b_Pst.png)

## Result5b: Pairwise Pst 

<table>
<tr><th>Table 1 Filter4</th><th>Table 2 Filter5a</th><th>Table3 Filter5b</th></tr>
<tr><td>

|     | EOB | PBF   | WOB   | WOF   |
|-----|-----|-------|-------|-------|
| EOB | x   | 0.046 | 0.077 | 0.03  |
| PBF |     | x     | 0.064 | 0.033 |
| WOB |     |       | x     | 0.079 |
| WOF |     |       |       | x     |

</td><td>

|     | EOB | PBF   | WOB   | WOF   |
|-----|-----|-------|-------|-------|
| EOB | x   | 0.046 | 0.083 | 0.028 |
| PBF |     | x     | 0.067 | 0.035 |
| WOB |     |       | x     | 0.085 |
| WOF |     |       |       | x     |

</td><td>

|     | EOB | PBF   | WOB   | WOF   |
|-----|-----|-------|-------|-------|
| EOB | x   | 0.047 | 0.085 | 0.029 |
| PBF |     | x     | 0.065 | 0.038 |
| WOB |     |       | x     | 0.085 |
| WOF |     |       |       | x     |

</td></tr> </table>

## Result5c: Pooled Back Reef vs Pooled Fringe Reef Pst

|         | Filter4    | Filter5a | Filter5b  |
|---------|------------|----------|-----------|
Mean Pst| 0.017| 0.017|0.016|

