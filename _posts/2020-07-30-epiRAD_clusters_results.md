---
layout: post
title: Comparison of results for epiRAD data per cluster, post removal of problematic loci from technical reps.  
tags: [ ddRAD, epiRAD, Moorea, methylation, filter, cluster]
---

## Cluster composition post all filters: 
1. CLUSTER1:
- EOB_175_epi, EOB_185_epi, EOB_189_epi, EOB_190_epi, EOB_192_epi
- PBF_169_epi, PBF_171_epi, PBF_172_epi
- WOF_224_epi, WOF_225_epi, WOF_234_epi, WOF_237_epi, WOF_238_epi, WOF_239_epi, WOF_240_epi, WOF_241_epi, WOF_243_epi, WOF_244_epi, WOF_245_epi
2. CLUSTER2: 
- EOB_177_epi, EOB_183_epi, EOB_184_epi, EOB_186_epi, EOB_188_epi, EOB_191_epi
- WOB_42_epi, WOB_47_epi, WOB_48_epi, WOB_49_epi, WOB_50_epi, WOB_59_epi, WOB_60_epi, WOB_62_epi

1. Filter4: Data obtained post BLAST filter, low read filter and low coverage filter 
2. Filter 5a: Data obtained post filter4 AND removing problematic loci identified by rad_haplotyper AND technical reps
3. Filter 5b: Data obtained post filter4 AND keeping only those loci that remain after full SNP filtering pipeline

|Cluster#| Filter#  | Number of loci| Methylation cutoff |
|--------|----------|-------------|----------------------|
|1| 4        |  7795       | -2.848               |
|2|4         |              |                       |
|1| 5a       |  6809       |  -2.883959           |
|1| 5b       |  5912       |   -2.830382          |

## Result1: MDS 

Cluster1             | cluster2 
:-------------------------:|:------:
![]({{site.baseurl}}/images/epiRAD_analysis_out/minus_outliers/Filter4_clust1_mds.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/minus_outliers/Filter4_clust2_mds.png)

## Result2: Methylation heatmap clustered by rows and columns 

Cluter1             | cluster2 
:-------------------------:|:------:
![]({{site.baseurl}}/images/epiRAD_analysis_out/post_fil2b/Filter4_clust1_MethylHeatMap.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/post_fil2b/Filter4_clust2_MethylHeatMap.png)

## Result3: %Methylation by site
ANOVA for % methylation per site is not significant.

Cluster1             |  Cluster2
:-------------------------:|:------:
![]({{site.baseurl}}/images/epiRAD_analysis_out/post_fil2b/Filter4_clust1_percnt_CpGmethyln_bysite.png)  |  ![]({{site.baseurl}}/images/epiRAD_analysis_out/post_fil2b/Filter4_clust2_percnt_CpGmethyln_bysite.png) 

## Result: Pst 

|         |Cluster1|Cluster2 
|---------|------------|---------|
Mean Pst| 0.1701| 0.05|

## Result: Pairwise Pst 

Cluster1 only
- EOB vs PBF: 0.118 
- PBF vs WOF: 0.211
- EOB vs WOF: 0.127

