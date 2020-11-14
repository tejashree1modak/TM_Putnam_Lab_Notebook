---
layout: post
title: Modified pipeline for identification of clusters and cluster specific analysis
tags: [ ddRAD, epiRAD, Moorea, dDocent, cluster, SNP, filter ]
---

## Pipeline modificaitons

After reorganizing the entire pipeline from identification of clusters to individual cluster analysis, this post walks through all the steps performed per the changes.This analysis is housed in mod_pipeline/ on kitt.  
The steps refer to the step numbers in the pipeline figure generated for the MS.

## Estimating species diversity
KITT: mod_pipeline/species_diversity/

### Step1: This step uses all samples post demultiplexing and removal of clones and removal of samples with read count < 400K. 

### Step2: Generating a reference assembly  
KITT: mod_pipeline/species_diversity/reference_assembly/
Five samples per location were randomly chosen to generate the reference assembly. Parameter optimization was performed using 
Used [this](https://github.com/jpuritz/BIO_594_2019/blob/master/Exercises/Week05/Jon/Week5.md) as reference for parameter optimization for reference assembly.

1. ReferenceOpt.sh
`ReferenceOpt.sh 2 6 2 6 PE 20`

```shell

dDocent ReferenceOpt version 2.7.8
K1 is 2 K2 is 2 c is 0.80
K1 is 2 K2 is 2 c is 0.82
K1 is 2 K2 is 2 c is 0.84
K1 is 2 K2 is 2 c is 0.86
K1 is 2 K2 is 2 c is 0.88
K1 is 2 K2 is 2 c is 0.90
K1 is 2 K2 is 2 c is 0.92
K1 is 2 K2 is 2 c is 0.94
K1 is 2 K2 is 2 c is 0.96
K1 is 2 K2 is 2 c is 0.98
K1 is 2 K2 is 3 c is 0.80
K1 is 2 K2 is 3 c is 0.82
K1 is 2 K2 is 3 c is 0.84
K1 is 2 K2 is 3 c is 0.86
K1 is 2 K2 is 3 c is 0.88
K1 is 2 K2 is 3 c is 0.90
K1 is 2 K2 is 3 c is 0.92
K1 is 2 K2 is 3 c is 0.94
K1 is 2 K2 is 3 c is 0.96
K1 is 2 K2 is 3 c is 0.98
K1 is 2 K2 is 4 c is 0.80
K1 is 2 K2 is 4 c is 0.82
K1 is 2 K2 is 4 c is 0.84
K1 is 2 K2 is 4 c is 0.86
K1 is 2 K2 is 4 c is 0.88
K1 is 2 K2 is 4 c is 0.90
K1 is 2 K2 is 4 c is 0.92
K1 is 2 K2 is 4 c is 0.94
K1 is 2 K2 is 4 c is 0.96
K1 is 2 K2 is 4 c is 0.98
K1 is 2 K2 is 5 c is 0.80
K1 is 2 K2 is 5 c is 0.82
K1 is 2 K2 is 5 c is 0.84
K1 is 2 K2 is 5 c is 0.86
K1 is 2 K2 is 5 c is 0.88
K1 is 2 K2 is 5 c is 0.90
K1 is 2 K2 is 5 c is 0.92
K1 is 2 K2 is 5 c is 0.94
K1 is 2 K2 is 5 c is 0.96
K1 is 2 K2 is 5 c is 0.98
K1 is 2 K2 is 6 c is 0.80
K1 is 2 K2 is 6 c is 0.82
K1 is 2 K2 is 6 c is 0.84
K1 is 2 K2 is 6 c is 0.86
K1 is 2 K2 is 6 c is 0.88
K1 is 2 K2 is 6 c is 0.90
K1 is 2 K2 is 6 c is 0.92
K1 is 2 K2 is 6 c is 0.94
K1 is 2 K2 is 6 c is 0.96
K1 is 2 K2 is 6 c is 0.98
K1 is 3 K2 is 2 c is 0.80
K1 is 3 K2 is 2 c is 0.82
K1 is 3 K2 is 2 c is 0.84
K1 is 3 K2 is 2 c is 0.86
K1 is 2 K2 is 5 c is 0.88
K1 is 2 K2 is 5 c is 0.90
K1 is 2 K2 is 5 c is 0.92
K1 is 2 K2 is 5 c is 0.94
K1 is 2 K2 is 5 c is 0.96
K1 is 2 K2 is 5 c is 0.98
K1 is 2 K2 is 6 c is 0.80
K1 is 2 K2 is 6 c is 0.82
K1 is 2 K2 is 6 c is 0.84
K1 is 2 K2 is 6 c is 0.86
K1 is 2 K2 is 6 c is 0.88
K1 is 2 K2 is 6 c is 0.90
K1 is 2 K2 is 6 c is 0.92
K1 is 2 K2 is 6 c is 0.94
K1 is 2 K2 is 6 c is 0.96
K1 is 2 K2 is 6 c is 0.98
K1 is 3 K2 is 2 c is 0.80
K1 is 3 K2 is 2 c is 0.82
K1 is 3 K2 is 2 c is 0.84
K1 is 3 K2 is 2 c is 0.86
K1 is 3 K2 is 2 c is 0.88
K1 is 3 K2 is 2 c is 0.90
K1 is 3 K2 is 2 c is 0.92
K1 is 3 K2 is 2 c is 0.94
K1 is 3 K2 is 2 c is 0.96
K1 is 3 K2 is 2 c is 0.98
K1 is 3 K2 is 3 c is 0.80
K1 is 3 K2 is 3 c is 0.82
K1 is 3 K2 is 3 c is 0.84
K1 is 3 K2 is 3 c is 0.86
K1 is 3 K2 is 3 c is 0.88
K1 is 3 K2 is 3 c is 0.90
K1 is 3 K2 is 3 c is 0.92
K1 is 3 K2 is 3 c is 0.94
K1 is 3 K2 is 3 c is 0.96
K1 is 3 K2 is 3 c is 0.98
K1 is 3 K2 is 4 c is 0.80
K1 is 3 K2 is 4 c is 0.82
K1 is 3 K2 is 4 c is 0.84
K1 is 3 K2 is 4 c is 0.86
K1 is 3 K2 is 4 c is 0.88
K1 is 3 K2 is 4 c is 0.90
K1 is 3 K2 is 4 c is 0.92
K1 is 3 K2 is 4 c is 0.94
K1 is 3 K2 is 4 c is 0.96
K1 is 3 K2 is 4 c is 0.98
K1 is 3 K2 is 5 c is 0.80
K1 is 3 K2 is 5 c is 0.82
K1 is 3 K2 is 5 c is 0.84
K1 is 3 K2 is 5 c is 0.86
K1 is 3 K2 is 5 c is 0.88
K1 is 3 K2 is 5 c is 0.90
K1 is 3 K2 is 5 c is 0.92
K1 is 3 K2 is 5 c is 0.94
K1 is 3 K2 is 5 c is 0.96
K1 is 3 K2 is 5 c is 0.98
K1 is 3 K2 is 6 c is 0.80
K1 is 3 K2 is 6 c is 0.82
K1 is 3 K2 is 6 c is 0.84
K1 is 3 K2 is 6 c is 0.86
K1 is 3 K2 is 6 c is 0.88
K1 is 3 K2 is 6 c is 0.90
K1 is 3 K2 is 6 c is 0.92
K1 is 3 K2 is 6 c is 0.94
K1 is 3 K2 is 6 c is 0.96
K1 is 3 K2 is 6 c is 0.98
K1 is 4 K2 is 2 c is 0.80
K1 is 4 K2 is 2 c is 0.82
K1 is 4 K2 is 2 c is 0.84
K1 is 4 K2 is 2 c is 0.86
K1 is 4 K2 is 2 c is 0.88
K1 is 4 K2 is 2 c is 0.90
K1 is 4 K2 is 2 c is 0.92
K1 is 4 K2 is 2 c is 0.94
K1 is 4 K2 is 2 c is 0.96
K1 is 4 K2 is 2 c is 0.98
K1 is 4 K2 is 3 c is 0.80
K1 is 4 K2 is 3 c is 0.82
K1 is 4 K2 is 3 c is 0.84
K1 is 4 K2 is 3 c is 0.86
K1 is 4 K2 is 3 c is 0.88
K1 is 4 K2 is 3 c is 0.90
K1 is 4 K2 is 3 c is 0.92
K1 is 4 K2 is 3 c is 0.94
K1 is 4 K2 is 3 c is 0.96
K1 is 4 K2 is 3 c is 0.98
K1 is 4 K2 is 4 c is 0.80
K1 is 4 K2 is 4 c is 0.82
K1 is 4 K2 is 4 c is 0.84
K1 is 4 K2 is 4 c is 0.86
K1 is 4 K2 is 4 c is 0.88
K1 is 4 K2 is 4 c is 0.90
K1 is 4 K2 is 4 c is 0.92
K1 is 4 K2 is 4 c is 0.94
K1 is 4 K2 is 4 c is 0.96
K1 is 4 K2 is 4 c is 0.98
K1 is 4 K2 is 5 c is 0.80
K1 is 4 K2 is 5 c is 0.82
K1 is 4 K2 is 5 c is 0.84
K1 is 4 K2 is 5 c is 0.86
K1 is 4 K2 is 5 c is 0.88
K1 is 4 K2 is 5 c is 0.90
K1 is 4 K2 is 5 c is 0.92
K1 is 4 K2 is 5 c is 0.94
K1 is 4 K2 is 5 c is 0.96
K1 is 4 K2 is 5 c is 0.98
K1 is 4 K2 is 6 c is 0.80
K1 is 4 K2 is 6 c is 0.82
K1 is 4 K2 is 6 c is 0.84
K1 is 4 K2 is 6 c is 0.86
K1 is 4 K2 is 6 c is 0.88
K1 is 4 K2 is 6 c is 0.90
K1 is 4 K2 is 6 c is 0.92
K1 is 4 K2 is 6 c is 0.94
K1 is 4 K2 is 6 c is 0.96
K1 is 4 K2 is 6 c is 0.98
K1 is 5 K2 is 2 c is 0.80
K1 is 5 K2 is 2 c is 0.82
K1 is 5 K2 is 2 c is 0.84
K1 is 5 K2 is 2 c is 0.86
K1 is 5 K2 is 2 c is 0.88
K1 is 5 K2 is 2 c is 0.90
K1 is 5 K2 is 2 c is 0.92
K1 is 5 K2 is 2 c is 0.94
K1 is 5 K2 is 2 c is 0.96
K1 is 5 K2 is 2 c is 0.98
K1 is 5 K2 is 3 c is 0.80
K1 is 5 K2 is 3 c is 0.82
K1 is 5 K2 is 3 c is 0.84
K1 is 5 K2 is 3 c is 0.86
K1 is 5 K2 is 3 c is 0.88
K1 is 5 K2 is 3 c is 0.90
K1 is 5 K2 is 3 c is 0.92
K1 is 5 K2 is 3 c is 0.94
K1 is 5 K2 is 3 c is 0.96
K1 is 5 K2 is 3 c is 0.98
K1 is 5 K2 is 4 c is 0.80
K1 is 5 K2 is 4 c is 0.82
K1 is 5 K2 is 4 c is 0.84
K1 is 5 K2 is 4 c is 0.86
K1 is 5 K2 is 4 c is 0.88
K1 is 5 K2 is 4 c is 0.90
K1 is 5 K2 is 4 c is 0.92
K1 is 5 K2 is 4 c is 0.94
K1 is 5 K2 is 4 c is 0.96
K1 is 5 K2 is 4 c is 0.98
K1 is 5 K2 is 5 c is 0.80
K1 is 5 K2 is 5 c is 0.82
K1 is 5 K2 is 5 c is 0.84
K1 is 5 K2 is 5 c is 0.86
K1 is 5 K2 is 5 c is 0.88
K1 is 5 K2 is 5 c is 0.90
K1 is 5 K2 is 5 c is 0.92
K1 is 5 K2 is 5 c is 0.94
K1 is 5 K2 is 5 c is 0.96
K1 is 5 K2 is 5 c is 0.98
K1 is 5 K2 is 6 c is 0.80
K1 is 5 K2 is 6 c is 0.82
K1 is 5 K2 is 6 c is 0.84
K1 is 5 K2 is 6 c is 0.86
K1 is 5 K2 is 6 c is 0.88
K1 is 5 K2 is 6 c is 0.90
K1 is 5 K2 is 6 c is 0.92
K1 is 5 K2 is 6 c is 0.94
K1 is 5 K2 is 6 c is 0.96
K1 is 5 K2 is 6 c is 0.98
K1 is 6 K2 is 2 c is 0.80
K1 is 6 K2 is 2 c is 0.82
K1 is 6 K2 is 2 c is 0.84
K1 is 6 K2 is 2 c is 0.86
K1 is 6 K2 is 2 c is 0.88
K1 is 6 K2 is 2 c is 0.90
K1 is 6 K2 is 2 c is 0.92
K1 is 6 K2 is 2 c is 0.94
K1 is 6 K2 is 2 c is 0.96
K1 is 6 K2 is 2 c is 0.98
K1 is 6 K2 is 3 c is 0.80
K1 is 6 K2 is 3 c is 0.82
K1 is 6 K2 is 3 c is 0.84
K1 is 6 K2 is 3 c is 0.86
K1 is 6 K2 is 3 c is 0.88
K1 is 6 K2 is 3 c is 0.90
K1 is 6 K2 is 3 c is 0.92
K1 is 6 K2 is 3 c is 0.94
K1 is 6 K2 is 3 c is 0.96
K1 is 6 K2 is 3 c is 0.98
K1 is 6 K2 is 4 c is 0.80
K1 is 6 K2 is 4 c is 0.82
K1 is 6 K2 is 4 c is 0.84
K1 is 6 K2 is 4 c is 0.86
K1 is 6 K2 is 4 c is 0.88
K1 is 6 K2 is 4 c is 0.90
K1 is 6 K2 is 4 c is 0.92
K1 is 6 K2 is 4 c is 0.94
K1 is 6 K2 is 4 c is 0.96
K1 is 6 K2 is 4 c is 0.98
K1 is 6 K2 is 5 c is 0.80
K1 is 6 K2 is 5 c is 0.82
K1 is 6 K2 is 5 c is 0.84
K1 is 6 K2 is 5 c is 0.86
K1 is 6 K2 is 5 c is 0.88
K1 is 6 K2 is 5 c is 0.90
K1 is 6 K2 is 5 c is 0.92
K1 is 6 K2 is 5 c is 0.94
K1 is 6 K2 is 5 c is 0.96
K1 is 6 K2 is 5 c is 0.98
K1 is 6 K2 is 6 c is 0.80
K1 is 6 K2 is 6 c is 0.82
K1 is 6 K2 is 6 c is 0.84
K1 is 6 K2 is 6 c is 0.86
K1 is 6 K2 is 6 c is 0.88
K1 is 6 K2 is 6 c is 0.90
K1 is 6 K2 is 6 c is 0.92
K1 is 6 K2 is 6 c is 0.94
K1 is 6 K2 is 6 c is 0.96
K1 is 6 K2 is 6 c is 0.98


                                         Histogram of number of reference contigs

     8 +------------------------------------------------------------------------------------------------------------+
       |  *        * +            +             +             +            +             +            +             |
       |  *        *                                        'plot.kopt.data' using (bin($1,binwidth)):(1.0) ******* |
     7 |***       **                                                                                              +-|
       |***       **                                                                                                |
       |***       **                                                                                                |
     6 |*****     ** *                                                                                            +-|
       |*****     ** *                                                                                              |
       |*****     ** *                                                                                              |
     5 |*****  ***** *        *        * **                                                                       +-|
       |*****  ***** *        *        * **                                                                         |
     4 |*****  ***** *    *****        *****                                                                      +-|
       |*****  ***** *    *****        *****                                                                        |
       |*****  ***** *    *****        *****                                                                        |
     3 |****** *******    ********     *****               *** *  *                                               +-|
       |****** *******    ********     *****               *** *  *                                                 |
       |****** *******    ********     *****               *** *  *                                                 |
     2 |****** ********   **********  *********** **      ********* **                                            +-|
       |****** ********   **********  ********* * **      ********* **                                              |
       |****** ********   **********  ********* * **      ********* **                                              |
     1 |*************************************** ***********************************************************       +-|
       |*************************************** ***** * ******************          *         **** * *  * *         |
       |*************************************** ***** * ****************** +        *    +    **** * *+ * *         |
     0 +------------------------------------------------------------------------------------------------------------+
     15000         20000        25000         30000         35000        40000         45000        50000         55000
                                                Number of reference contigs
Average contig number = 25114
The top three most common number of contigs
X       Contig number
2       16127
2       15503
1       51276
The top three most common number of contigs (with values rounded)
X       Contig number
6       15800
5       16800
5       15200

```

![]({{site.baseurl}}/images/mod_pipeline/species_diversity/ReferenceOpt_sp_div.png)
The plot shows 0.9 as the optimal similarity threshold. 


2. RefMapOpt.sh

`RefMapOpt.sh 2 6 2 6 0.9 PE 20`

Used the mapping.results to compare values. We have to pick optimal k1,k2 cutoffs. Ideally, you want to maximize properly paired mappings and number of contigs while minimizing mismatched reads.

```shell
Cov      Non0Cov  Contigs  MeanContigsMapped  K1  K2  SUM Mapped  SUM Properly  Mean Mapped  Mean Properly  MisMatched
98.2696  155.183  47633    29719              2   2   70214603    63625835      4.68097e+06  4.24172e+06    164558
145.521  192.78   31099    23272.4            2   3   67885501    61904868      4.5257e+06   4.12699e+06    116478
175.186  212.939  24689    20193              2   4   64880128    59927449      4.32534e+06  3.99516e+06    77087.4
198.334  228.68   20280    17511.3            2   5   60336126    55456066      4.02241e+06  3.69707e+06    90376.3
218.948  243.525  16823    15074.7            2   6   55253611    51240341      3.68357e+06  3.41602e+06    45771.6
128.898  189.021  36511    24709              3   2   70595010    64493357      4706334      4.29956e+06    134345
159.81   207.222  28177    21605.6            3   3   67546809    61530161      4.50312e+06  4.10201e+06    119537
182.325  220.097  23429    19320.6            3   4   64078229    58592299      4.27188e+06  3.90615e+06    116625
205.33   235.896  19461    16877.4            3   5   59941970    55216232      3.99613e+06  3.68108e+06    81705.3
224.496  249.18   16198    14552.2            3   6   54549227    50362975      3.63662e+06  3.35753e+06    56075.1
132.589  193.627  35354    24042.6            4   2   70315301    64103940      4.68769e+06  4273596        138974
162.541  210.089  27562    21207.3            4   3   67201915    61276951      4.48013e+06  4.08513e+06    126061
186.141  224.259  22978    18988.8            4   4   64159865    58770869      4.27732e+06  3.91806e+06    111165
208.017  238.534  19067    16569.6            4   5   59496810    54478379      3966454      3.63189e+06    90448.1
227.155  251.868  15856    14261.7            4   6   54030051    49858645      3.602e+06    3.32391e+06    54826.3
134.182  195.396  34859    23774.8            5   2   70163844    63618028      4.67759e+06  4.2412e+06     146547
164.281  211.924  27162    20942.1            5   3   66935536    61025545      4.46237e+06  4.06837e+06    123960
188.826  226.936  22572    18700.7            5   4   63935453    58827777      4.26236e+06  3.92185e+06    94486.3
209.67   240.056  18738    16309.8            5   5   58935223    54142343      3.92901e+06  3.60949e+06    72980.3
230.211  254.952  15564    14015.5            5   6   53748447    49230968      3.58323e+06  3.28206e+06    54917.5
135.847  197.179  34379    23525.5            6   2   70056427    63833654      4.67043e+06  4.25558e+06    127198
166.401  213.862  26829    20762.7            6   3   66968079    61438385      4.46454e+06  4.09589e+06    111078
190.838  228.795  22231    18463.8            6   4   63640815    58681873      4242721      3.91212e+06    79363.3
212.021  242.331  18463    16098.6            6   5   58721215    53718516      3.91475e+06  3.58123e+06    87104.8
232.112  256.639  15250    13755.3            6   6   53099038    48668830      3.53994e+06  3.24459e+06    50503.3
❯ sort -k 10 -n -r  mapping.results | column -t -s $'\t'
132.589  193.627  35354    24042.6            4   2   70315301    64103940      4.68769e+06  4273596        138974
128.898  189.021  36511    24709              3   2   70595010    64493357      4706334      4.29956e+06    134345
135.847  197.179  34379    23525.5            6   2   70056427    63833654      4.67043e+06  4.25558e+06    127198
98.2696  155.183  47633    29719              2   2   70214603    63625835      4.68097e+06  4.24172e+06    164558
134.182  195.396  34859    23774.8            5   2   70163844    63618028      4.67759e+06  4.2412e+06     146547
145.521  192.78   31099    23272.4            2   3   67885501    61904868      4.5257e+06   4.12699e+06    116478
159.81   207.222  28177    21605.6            3   3   67546809    61530161      4.50312e+06  4.10201e+06    119537
166.401  213.862  26829    20762.7            6   3   66968079    61438385      4.46454e+06  4.09589e+06    111078
162.541  210.089  27562    21207.3            4   3   67201915    61276951      4.48013e+06  4.08513e+06    126061
164.281  211.924  27162    20942.1            5   3   66935536    61025545      4.46237e+06  4.06837e+06    123960
175.186  212.939  24689    20193              2   4   64880128    59927449      4.32534e+06  3.99516e+06    77087.4
188.826  226.936  22572    18700.7            5   4   63935453    58827777      4.26236e+06  3.92185e+06    94486.3
186.141  224.259  22978    18988.8            4   4   64159865    58770869      4.27732e+06  3.91806e+06    111165
190.838  228.795  22231    18463.8            6   4   63640815    58681873      4242721      3.91212e+06    79363.3
182.325  220.097  23429    19320.6            3   4   64078229    58592299      4.27188e+06  3.90615e+06    116625
198.334  228.68   20280    17511.3            2   5   60336126    55456066      4.02241e+06  3.69707e+06    90376.3
205.33   235.896  19461    16877.4            3   5   59941970    55216232      3.99613e+06  3.68108e+06    81705.3
208.017  238.534  19067    16569.6            4   5   59496810    54478379      3966454      3.63189e+06    90448.1
209.67   240.056  18738    16309.8            5   5   58935223    54142343      3.92901e+06  3.60949e+06    72980.3
212.021  242.331  18463    16098.6            6   5   58721215    53718516      3.91475e+06  3.58123e+06    87104.8
218.948  243.525  16823    15074.7            2   6   55253611    51240341      3.68357e+06  3.41602e+06    45771.6
224.496  249.18   16198    14552.2            3   6   54549227    50362975      3.63662e+06  3.35753e+06    56075.1
227.155  251.868  15856    14261.7            4   6   54030051    49858645      3.602e+06    3.32391e+06    54826.3
230.211  254.952  15564    14015.5            5   6   53748447    49230968      3.58323e+06  3.28206e+06    54917.5
232.112  256.639  15250    13755.3            6   6   53099038    48668830      3.53994e+06  3.24459e+06    50503.3
Cov      Non0Cov  Contigs  MeanContigsMapped  K1  K2  SUM Mapped  SUM Properly  Mean Mapped  Mean Properly  MisMatched

```
Comparing top choices: 

```shell
Cov      Non0Cov  Contigs  MeanContigsMapped  K1  K2  SUM Mapped  SUM Properly  Mean Mapped  Mean Properly  MisMatched
128.898  189.021  36511    24709              3   2   70595010    64493357      4706334      4.29956e+06    134345
135.847  197.179  34379    23525.5            6   2   70056427    63833654      4.67043e+06  4.25558e+06    127198
98.2696  155.183  47633    29719              2   2   70214603    63625835      4.68097e+06  4.24172e+06    164558
134.182  195.396  34859    23774.8            5   2   70163844    63618028      4.67759e+06  4.2412e+06     146547

```
With K1=3 and K2=2 we have the most mean properly paired mappings, second highest number of contigs and the fewer mismatched reads. 
**So K1 =3 and K2 = 2 were chosen for reference assembly.**
These parameters were used for the reference assembly that was built using dDocent.

```shell
cat config.file

Number of Processors                                                                                                                                                           [15/4491]
20
Maximum Memory
0
Trimming
no
Assembly?
yes
Type_of_Assembly
PE
Clustering_Similarity%
0.9
Minimum within individual coverage level to include a read for assembly (K1)
3
Minimum number of individuals a read must be present in to include for assembly (K2)
2
Mapping_Reads?
no
Mapping_Match_Value

Mapping_MisMatch_Value

Mapping_GapOpen_Penalty

Calling_SNPs?
no
Email
xx@uri.edu
```
####**Filtering reference assembly for coral contigs**

Blast the reference assembly with a database made from 3 coral genomes (Pocillopora acuta, P. verrucosa and P. damicornis).

`blastn -db /home/tejashree/Moorea/genomes/coral -query /home/tejashree/Moorea/ddocent/mod_pipeline/species_diversity/reference_assembly/reference.fasta  -evalue 0.001 -outfmt 6 -out /home/tejashree/Moorea/blast/mod_pipeline/species_diversity/coral_hits -num_threads 20`

Get unique hits 
`cut -f1 coral_hits| uniq > uniq_coral_hits.txt`

Filter reference assembly to keep only those contigs that mapped to atleast one coral genome. These are listed in the uniq_coral_hits.txt. I wrote a script subset_fasta.py to subset the reference assembly that is run as following:  

`python3 subset_fasta.py -i /home/tejashree/Moorea/ddocent/mod_pipeline/species_diversity/reference_assembly/reference.fasta -f /home/tejashree/Moorea/blast/mod_pipeline/species_diversity/uniq_coral_hits.txt -o /home/tejashree/Moorea/ddocent/mod_pipeline/species_diversity/reference_assembly/coral_reference.fasta`

This was moved to species_diversity and renamed as reference.fasta since dDocent will look for the specific file name. 

```shell
cp reference_assembly/coral_reference.fasta .
mv coral_reference.fasta reference.fasta
```

### Step3: Mapping reads to filtered reference:
I created symlinks for all samples to here and used dDocent for trimming and mapping to reference.

```shell
❯ cat config.file
Number of Processors
20
Maximum Memory
0
Trimming
yes
Assembly?
no
Type_of_Assembly
PE
Clustering_Similarity%
0.9
Minimum within individual coverage level to include a read for assembly (K1)
3
Minimum number of individuals a read must be present in to include for assembly (K2)
2
Mapping_Reads?
yes
Mapping_Match_Value
1
Mapping_MisMatch_Value
3
Mapping_GapOpen_Penalty
5
Calling_SNPs?
yes
Email
xxx@uri.edu

```
### Step4:SNP calling and filtering for ddRAD samples 

**SNP calling**
Housed in dir mod_pipeline/species_diversity/ddr_snp_calling
Created symlinks from mapping step for the the files required for SNP calling to avoid clutter.
Created a config.file to only call SNPs using dDocent. 

```shell
❯ cat config.file
Number of Processors
20
Maximum Memory
0
Trimming
no
Assembly?
no
Type_of_Assembly

Clustering_Similarity%

Minimum within individual coverage level to include a read for assembly (K1)

Minimum number of individuals a read must be present in to include for assembly (K2)

Mapping_Reads?
no
Mapping_Match_Value

Mapping_MisMatch_Value

Mapping_GapOpen_Penalty

Calling_SNPs?
yes
Email
xxx@uri.edu

```

**SNP filtering**

Housed in /home/tejashree/Moorea/ddocent/mod_pipeline/species_diversity/ddr_snp_calling/snp_filtering
Generated a symlink to the final vcf output from SNP calling:
`ln -s ../TotalRawSNPs.vcf`

1. **Step1: 50% of individuals, a minimum quality score of 30, and a minor allele count of 3**

```shell
vcftools --vcf TotalRawSNPs.vcf --max-missing 0.5 --mac 3 --minQ 30 --recode --recode-INFO-all --out raw.g5mac3

After filtering, kept 56 out of 56 Individuals
Outputting VCF file...
After filtering, kept 205536 out of a possible 625287 Sites

```

2. **Step2: Minimum mean depth: minDP 5**

```shell
vcftools --vcf raw.g5mac3.recode.vcf --minDP 5 --recode --recode-INFO-all --out raw.g5mac3dp5

After filtering, kept 56 out of 56 Individuals
Outputting VCF file...
After filtering, kept 205536 out of a possible 205536 Sites
```

3. **Step3: Filter missing indiv post minDP =5**

```shell
./filter_missing_ind.sh raw.g5mac3dp5.recode.vcf raw.g5mac3dplm
After filtering, kept 205536 out of a possible 205536 Sites
Run Time = 3.00 seconds


                                          Histogram of % missing data per individual

       14 +---------------------------------------------------------------------------------------------------------+
          |              +              +              +               +              +              +              |
          |                                     ********      'totalmissing' using (bin($1,binwidth)):(1.0) ******* |
       12 |-+                                   *      *                                                          +-|
          |                                     *      *                                                            |
          |                                     *      *                                                            |
          |                                     *      *                                                            |
       10 |-+                                   *      *                                                          +-|
          |                      ********       *      *                                                            |
          |                      *      *       *      *                                                            |
        8 |-+                    *      *       *      *                                                          +-|
          |                      *      *       *      *                                                            |
          |                      *      *       *      *                                                            |
        6 |-+            *********      *       *      *               ********                                   +-|
          |              *       *      *       *      *               *      *                                     |
          |              *       *      *       *      *********       *      *                                     |
        4 |-+            *       *      *********      *       *********      *                                   +-|
          |              *       *      *       *      *       *       *      *                                     |
          |       ********       *      *       *      *       *       *      *********                             |
          |       *      *       *      *       *      *       *       *      *       *                             |
        2 |-+     *      *       *      *       *      *       *       *      *       ************                +-|
          |       *      *       *      *       *      *       *       *      *       *          *********          |
          |       *      *       *      *       *      *       *       *      *       *          *   +   *          |
        0 +---------------------------------------------------------------------------------------------------------+
         0.12           0.14           0.16           0.18            0.2            0.22           0.24           0.26
                                                       % of missing data

The 85% cutoff would be 0.205789
Would you like to set a different cutoff, yes or no
yes
Please enter new cutoff
0.25
All individuals with more than 25.0% missing data will be removed.

After filtering, kept 56 out of 56 Individuals
Outputting VCF file...
After filtering, kept 205536 out of a possible 205536 Sites

mawk '$5 > 0.25' raw.g5mac3dplm.imiss | cut -f1 | less

INDV
```
4. **Step4: Restrict the data to variants called in a high percentage of individuals and filter by mean depth of genotypes**

This applied a genotype call rate (95%) across all individuals. Setting maf = 0.001

```shell
vcftools --vcf raw.g5mac3dplm.recode.vcf --max-missing 0.95 --maf 0.001 --recode --recode-INFO-all --out DP3g95maf001 --min-meanDP 20

After filtering, kept 56 out of 56 Individuals
Outputting VCF file...
After filtering, kept 90254 out of a possible 205536 Sites
```

5. **Step5: Filtering by population specific call rate when multiple localities are present**

```shell
ln -s ../popmap .
mawk '$2 == "EOB"' popmap > 1.keep && mawk '$2 == "PBF"' popmap > 2.keep && mawk '$2 == "WOB"' popmap > 3.keep && mawk '$2 == "WOF"' popmap > 4.keep
vcftools --vcf DP3g95maf001.recode.vcf --keep 1.keep --missing-site --out 1
vcftools --vcf DP3g95maf001.recode.vcf --keep 2.keep --missing-site --out 2
vcftools --vcf DP3g95maf001.recode.vcf --keep 3.keep --missing-site --out 3
vcftools --vcf DP3g95maf001.recode.vcf --keep 4.keep --missing-site --out 4
cat 1.lmiss 2.lmiss 3.lmiss 4.lmiss | mawk '!/CHR/' | mawk '$6 > 0.1' | cut -f1,2 >> badloci

fter filtering, kept 56 out of 56 Individuals
Outputting VCF file...
After filtering, kept 87616 out of a possible 90254 Sites

```

6. **Step6: Used dDocent_filters script**

```shell
./dDocent_filters DP3g95p5maf001.recode.vcf dDocent_filters_out
This script will automatically filter a FreeBayes generated VCF file using criteria related to site depth,
quality versus depth, strand representation, allelic balance at heterzygous individuals, and paired read representation.
The script assumes that loci and individuals with low call rates (or depth) have already been removed.

Contact Jon Puritz (jpuritz@gmail.com) for questions and see script comments for more details on particular filters

Number of sites filtered based on allele balance at heterozygous loci, locus quality, and mapping quality / Depth
 11141 of 87616

Are reads expected to overlap?  In other words, is fragment size less than 2X the read length?  Enter yes or no.
no
Number of additional sites filtered based on overlapping forward and reverse reads
 16957 of 76475

Is this from a mixture of SE and PE libraries? Enter yes or no.
no
Number of additional sites filtered based on properly paired status
 1507 of 59518

Number of sites filtered based on high depth and lower than 2*DEPTH quality score
 5618 of 58011

                                               Histogram of mean depth per site

      900 +---------------------------------------------------------------------------------------------------------+
          |+    +    +    +     +    +    +    +    +     +    +    +    +    +     +    +    +    +    +     +    +|
          |                                    **         'meandepthpersite' using (bin($1,binwidth)):(1.0) ******* |
      800 |-+                                 *** ***                                                             +-|
          |                                  ********                                                               |
      700 |-+                                ********* *                                                          +-|
          |                            **   ********** *                                                            |
          |                            ** **************                                                            |
      600 |-+                          ** **************                                                          +-|
          |                            ********************                                                         |
      500 |-+                        **********************                                                       +-|
          |                          **********************                                                         |
          |                          ************************                                                       |
      400 |-+                        ************************** **                                                +-|
          |                         ******************************  *                                               |
      300 |-+                      ************************************** **                                      +-|
          |                     *  ************************************** **                                        |
          |                    ********************************************* *     *                                |
      200 |-+                *************************************************** * *                              +-|
          |                  ***********************************************************                            |
      100 |-+               ************************************************************      **                  +-|
          |              ******************************************************************* ***** *     *    *   * |
          |+    +    + ************************************************************************************ ********|
        0 +---------------------------------------------------------------------------------------------------------+
           12   24   36   48    60   72   84   96  108   120  132  144  156  168   180  192  204  216  228   240  252
                                                          Mean Depth

If distrubtion looks normal, a 1.645 sigma cutoff (~90% of the data) would be 13239.1453
The 95% cutoff would be 232

Would you like to use a different maximum mean depth cutoff than 232, yes or no
no
Number of sites filtered based on maximum mean depth
 3520 of 58011

Number of sites filtered based on within locus depth mismatch
 26 of 54491

Total number of sites filtered
 33151 of 87616

Remaining sites
 54465

Filtered VCF file is called dDocent_filters_out.FIL.recode.vcf

Filter stats stored in dDocent_filters_out.filterstats

```

7. **Step7: Convert our variant calls to SNPs**

```shell
vcfallelicprimitives dDocent_filters_out.FIL.recode.vcf --keep-info --keep-geno > DP3g95p5maf001.prim.vcf

vcftools --vcf DP3g95p5maf001.prim.vcf --remove-indels --recode --recode-INFO-all --out SNP.DP3g95p5maf001

After filtering, kept 56 out of 56 Individuals
Outputting VCF file...
After filtering, kept 58541 out of a possible 61467 Sites

```

8. **Step8: HWE filter**

Setting -h 0.001

```shell
./filter_hwe_by_pop.pl -v SNP.DP3g95p5maf001.recode.vcf -p popmap -o SNP.DP3g95p5maf001.HWE -h 0.001

Processing population: EOB (17 inds)
Processing population: PBF (14 inds)
Processing population: WOB (11 inds)
Processing population: WOF (14 inds)
Outputting results of HWE test for filtered loci to 'filtered.hwe'
Kept 56824 of a possible 58541 loci (filtered 1717 loci)

```
9. **Haplotyping using rad_haplotyper**

Made symlinks for bam and their indexes from ddr_snp_calling to snpPfitlering since they are required by rad_haplotyper

```shell
rad_haplotyper.pl -v SNP.DP3g95p5maf001.HWE.recode.vcf -x 20 -mp 1 -u 20 -ml 4 -n -r reference.fasta
Removed 146 loci (3541 SNPs) with more than 20 SNPs at a locus
Building haplotypes for EOB_174_ddr
Building haplotypes for EOB_175_ddr
Building haplotypes for EOB_176_ddr
Building haplotypes for EOB_177_ddr
Building haplotypes for EOB_178_ddr
Building haplotypes for EOB_182_ddr
Building haplotypes for EOB_183_ddr
Building haplotypes for EOB_184_ddr
Building haplotypes for EOB_185_ddr
Building haplotypes for EOB_186_ddr
Building haplotypes for EOB_188_ddr
Building haplotypes for EOB_189_ddr
Building haplotypes for EOB_190_ddr
Building haplotypes for EOB_191_ddr
Building haplotypes for EOB_192_ddr
Building haplotypes for EOB_493_ddr
Building haplotypes for EOB_494_ddr
Building haplotypes for PBF_157_ddr
Building haplotypes for PBF_158_ddr
Building haplotypes for PBF_160_ddr
Building haplotypes for PBF_161_ddr
Building haplotypes for PBF_164_ddr
Building haplotypes for PBF_165_ddr
Building haplotypes for PBF_167_ddr
Building haplotypes for PBF_168_ddr
Building haplotypes for PBF_169_ddr
Building haplotypes for PBF_171_ddr
Building haplotypes for PBF_172_ddr
Building haplotypes for PBF_489_ddr
Building haplotypes for PBF_490_ddr
Building haplotypes for PBF_491_ddr
Building haplotypes for WOB_35_ddr
Building haplotypes for WOB_41_ddr
Building haplotypes for WOB_42_ddr
Building haplotypes for WOB_47_ddr
Building haplotypes for WOB_48_ddr
Building haplotypes for WOB_49_ddr
Building haplotypes for WOB_50_ddr
Building haplotypes for WOB_59_ddr
Building haplotypes for WOB_60_ddr
Building haplotypes for WOB_62_ddr
Building haplotypes for WOB_65_ddr
Building haplotypes for WOF_217_ddr
Building haplotypes for WOF_224_ddr
Building haplotypes for WOF_225_ddr
Building haplotypes for WOF_232_ddr
Building haplotypes for WOF_234_ddr
Building haplotypes for WOF_236_ddr
Building haplotypes for WOF_237_ddr
Building haplotypes for WOF_238_ddr
Building haplotypes for WOF_239_ddr
Building haplotypes for WOF_240_ddr
Building haplotypes for WOF_241_ddr
Building haplotypes for WOF_243_ddr
Building haplotypes for WOF_244_ddr
Building haplotypes for WOF_245_ddr
Filtered 11 loci below missing data cutoff
Filtered 913 possible paralogs
Filtered 417 loci with low coverage or genotyping errors
Filtered 0 loci with an excess of haplotypes

head stats.out
rad_haplotyper -v SNP.DP3g95p5maf001.HWE.recode.vcf -x 20 -mp 1 -u 20 -ml 4 -n -r reference.fasta
Locus   Sites   Haplotypes      Inds_Haplotyped Total_Inds      Prop_Haplotyped Status  Poss_Paralog    Low_Cov/Geno_Err        Miss_Geno       Comment
dDocent_Contig_10000    1       2       56      56      1.000   PASSED  0       0       0
dDocent_Contig_10002    11      6       55      56      0.982   PASSED  0       0       1
dDocent_Contig_10005    2       3       56      56      1.000   PASSED  0       0       0
dDocent_Contig_10008    4       5       56      56      1.000   PASSED  0       0       0
dDocent_Contig_10009    10      9       56      56      1.000   PASSED  0       0       0
dDocent_Contig_10011    4       5       56      56      1.000   PASSED  0       0       0
dDocent_Contig_10016    2       4       56      56      1.000   PASSED  0       0       0
dDocent_Contig_10017    10      14      36      56      0.643   FILTERED        18      0       2       Possible paralog

```
We can use this file to create a list of loci to filter

`grep FILTERED stats.out | mawk '!/Complex/' | cut -f1 > loci.to.remove`

Remove bad loci identified by rad_haplotyper
Now that we have the list we can parse through the VCF file and remove the bad RAD loci. Use script from dDocent to do this: remove.bad.hap.loci.sh

```shell
./remove.bad.hap.loci.sh loci.to.remove SNP.DP3g95p5maf001.HWE.recode.vcf
mawk '!/#/' SNP.DP3g95p5maf001.HWE.filtered.vcf | wc -l
40251

```
10. **Handling techinical replicates**
Used this markdown as [reference](https://github.com/amyzyck/RADseq_Uca-rapax_2016/blob/master/Scripts/Filtering/Filtering_UcaRapax.md)
This data set contains technical replicates. We will use a custom script dup_sample_filter.sh to automatically remove sites in VCF files that do not have congruent genotypes across duplicate individuals. It will only consider genotypes that have at least 5 reads.
The techinical reps are listed in file techinical_reps. EOB_492 had less than 400K reads and was filtered out so took that out of this list. 

```shell
./dup_sample_filter.sh SNP.DP3g95p5maf001.HWE.filtered.vcf technical_reps
head mismatched.loci
4       dDocent_Contig_5321     108
2       dDocent_Contig_8662     75
3       dDocent_Contig_20246    89
2       dDocent_Contig_2543     119
3       dDocent_Contig_17193    21
2       dDocent_Contig_25017    178
3       dDocent_Contig_4016     74
2       dDocent_Contig_22187    137
2       dDocent_Contig_7004     162
2       dDocent_Contig_8454     22

echo -e "Mismatches\tNumber_of_Loci" > mismatch.txt
for i in {2..20}
do
paste <(echo $i) <(mawk -v x=$i '$1 > x' mismatched.loci | wc -l) >> mismatch.txt
done

wc -l bad.loci*
  27 bad.loci.EOB_176_ddr.EOB_493_ddr
  31 bad.loci.EOB_176_ddr.EOB_494_ddr
  54 bad.loci.EOB_493_ddr.EOB_494_ddr
  76 bad.loci.PBF_157_ddr.PBF_489_ddr
  20 bad.loci.PBF_157_ddr.PBF_490_ddr
  14 bad.loci.PBF_157_ddr.PBF_491_ddr
  74 bad.loci.PBF_489_ddr.PBF_490_ddr
  76 bad.loci.PBF_489_ddr.PBF_491_ddr
  22 bad.loci.PBF_490_ddr.PBF_491_ddr
 394 total

cat mismatch.txt
Mismatches      Number_of_Loci
2       87
3       14
4       2
5       1
6       0
7       0
8       0
9       0
10      0
11      0
12      0
13      0
14      0
15      0
16      0
17      0
18      0
19      0
20      0

```
I chose a cut off of 4,to filter out loci with mismatched values > 4 to remove most affected loci.

```shell
mawk '$1 > 4' mismatched.loci | cut -f2,3 > mismatchedloci
vcftools --vcf SNP.DP3g95p5maf001.HWE.filtered.vcf --exclude-positions mismatchedloci --recode --recode-INFO-all --out SNP.DP3g95p5maf001.HWE.filtered.MM

After filtering, kept 56 out of 56 Individuals
Outputting VCF file...
After filtering, kept 40249 out of a possible 40251 Sites
``` 
### Step 5: Cluster identification
The final vcf file was used in script identify_clusters.R to identify putative species clusters using DAPC. 

```r
> grps <- find.clusters(SNPs) #45 PCs and k=5 clusters
Choose the number PCs to retain (>= 1): 
45
Choose the number of clusters (>=2: 
5
> names(grps)
[1] "Kstat" "stat"  "grp"   "size" 
> grps$Kstat
     K=1      K=2      K=3      K=4      K=5      K=6 
581.0997 571.7620 566.6947 564.7860 563.6012 564.6559 
> grps$grp
EOB_174_ddr EOB_175_ddr EOB_176_ddr EOB_177_ddr EOB_178_ddr EOB_182_ddr EOB_183_ddr EOB_184_ddr EOB_185_ddr EOB_186_ddr 
          1           1           2           3           3           3           3           3           1           3 
EOB_188_ddr EOB_189_ddr EOB_190_ddr EOB_191_ddr EOB_192_ddr EOB_493_ddr EOB_494_ddr PBF_157_ddr PBF_158_ddr PBF_160_ddr 
          3           1           1           3           1           2           2           4           1           3 
PBF_161_ddr PBF_164_ddr PBF_165_ddr PBF_167_ddr PBF_168_ddr PBF_169_ddr PBF_171_ddr PBF_172_ddr PBF_489_ddr PBF_490_ddr 
          1           1           5           5           5           1           1           1           4           4 
PBF_491_ddr  WOB_35_ddr  WOB_41_ddr  WOB_42_ddr  WOB_47_ddr  WOB_48_ddr  WOB_49_ddr  WOB_50_ddr  WOB_59_ddr  WOB_60_ddr 
          4           1           3           3           3           3           3           3           3           3 
 WOB_62_ddr  WOB_65_ddr WOF_217_ddr WOF_224_ddr WOF_225_ddr WOF_232_ddr WOF_234_ddr WOF_236_ddr WOF_237_ddr WOF_238_ddr 
          3           3           5           1           1           1           1           1           1           1 
WOF_239_ddr WOF_240_ddr WOF_241_ddr WOF_243_ddr WOF_244_ddr WOF_245_ddr 
          1           1           1           1           1           1 
Levels: 1 2 3 4 5

> dapc <- dapc(SNPs, grps$grp)# 20 PCs and 2 Discriminant functions to retain
Choose the number PCs to retain (>=1): 
20
Choose the number discrmod_pipeline/cluster_variation/iminant functions to retain (>=1): 
2

```

![]({{site.baseurl}}/images/mod_pipeline/species_diversity/Find_clusters_var_by_pca.png)
![]({{site.baseurl}}/images/mod_pipeline/species_diversity/ClustersvsBIC.png)
![]({{site.baseurl}}/images/mod_pipeline/species_diversity/dapc_variance_by_pca.png)
![]({{site.baseurl}}/images/mod_pipeline/species_diversity/dapc_eigen.png)
![]({{site.baseurl}}/images/mod_pipeline/species_diversity/dapc.png)

Thus according to the above DAPC result we have 5 clusters in total out of which clusters 1 and 3 have the highest membership. These will be further used to estimate genetic and epigenetic variation in STEP 6. Below are the compositions of the 2 clusters. Cluster 2 has only one PBF sample. To keep the comparison between east vs west back reef, fringe sample PBF160 will be removed from this cluster. 
Cluster 
- Cluster 1: EOB_174_ddr,EOB_175_ddr,EOB_185_ddr,EOB_189_ddr,EOB_190_ddr,EOB_192_ddr,PBF_158_ddr,PBF_161_ddr,PBF_164_ddr,PBF_169_ddr,PBF_171_ddr,PBF_172_ddr,WOB_35_ddr,WOF_224_ddr WOF_225_ddr,WOF_232_ddr,WOF_234_ddr,WOF_236_ddr,WOF_237_ddr,WOF_238_ddr,WOF_239_ddr,WOF_240_ddr,WOF_241_ddr,WOF_243_ddr,WOF_244_ddr,WOF_245_ddr. 
- Cluster 2: EOB_177_ddr EOB_178_ddr EOB_182_ddr EOB_183_ddr EOB_184_ddr,EOB_186_ddr,EOB_188_ddr,EOB_191_ddr,WOB_41_ddr,WOB_42_ddr,WOB_47_ddr,WOB_48_ddr,WOB_49_ddr,WOB_50_ddr,WOB_59_ddr,WOB_60_ddr,WOB_62_ddr,WOB_65_ddr. 

### Step 6: Determining genetic and epigenetic variation per species cluster
Housed in: mod_pipeline/cluster_variation/ 
Analysis for cluster1: mod_pipeline/cluster_variation/clust1
Analysis for cluster2: mod_pipeline/cluster_variation/clust2

### Step 7: Reference assembly per cluster
Housed in: 
Analysis for cluster1: mod_pipeline/cluster_variation/clust1/reference_assembly/
Analysis for cluster2: mod_pipeline/cluster_variation/clust2/reference_assembly/
A reference set of up to 5 samples per location were used to build the reference assembly. Parameter optimization was performed as before.  

#### Cluster 1: 

```shell

ReferenceOpt.sh 2 6 2 6 PE 20

All required software is installed!

dDocent ReferenceOpt version 2.7.8
K1 is 2 K2 is 2 c is 0.80
K1 is 2 K2 is 2 c is 0.82
K1 is 2 K2 is 2 c is 0.84
K1 is 2 K2 is 2 c is 0.86
K1 is 2 K2 is 2 c is 0.88
K1 is 2 K2 is 2 c is 0.90
K1 is 2 K2 is 2 c is 0.92
K1 is 2 K2 is 2 c is 0.94
K1 is 2 K2 is 2 c is 0.96
K1 is 2 K2 is 2 c is 0.98
K1 is 2 K2 is 3 c is 0.80
K1 is 2 K2 is 3 c is 0.82
K1 is 2 K2 is 3 c is 0.84
K1 is 2 K2 is 3 c is 0.86
K1 is 2 K2 is 3 c is 0.88
K1 is 2 K2 is 3 c is 0.90
K1 is 2 K2 is 3 c is 0.92
K1 is 2 K2 is 3 c is 0.94
K1 is 2 K2 is 3 c is 0.96
K1 is 2 K2 is 3 c is 0.98
K1 is 2 K2 is 4 c is 0.80
K1 is 2 K2 is 4 c is 0.82
K1 is 2 K2 is 4 c is 0.84
K1 is 2 K2 is 4 c is 0.86
K1 is 2 K2 is 4 c is 0.88
K1 is 2 K2 is 4 c is 0.90
K1 is 2 K2 is 4 c is 0.92
K1 is 2 K2 is 4 c is 0.94
K1 is 2 K2 is 4 c is 0.96
K1 is 2 K2 is 4 c is 0.98
K1 is 2 K2 is 5 c is 0.80
K1 is 2 K2 is 5 c is 0.82
K1 is 2 K2 is 5 c is 0.84
K1 is 2 K2 is 5 c is 0.86
K1 is 2 K2 is 5 c is 0.88
K1 is 2 K2 is 5 c is 0.90
K1 is 2 K2 is 5 c is 0.92
K1 is 2 K2 is 5 c is 0.94
K1 is 2 K2 is 5 c is 0.96
K1 is 2 K2 is 5 c is 0.98
K1 is 2 K2 is 6 c is 0.80
K1 is 2 K2 is 6 c is 0.82
K1 is 2 K2 is 6 c is 0.84
K1 is 2 K2 is 6 c is 0.86
K1 is 2 K2 is 6 c is 0.88
K1 is 2 K2 is 6 c is 0.90
K1 is 2 K2 is 6 c is 0.92
K1 is 2 K2 is 6 c is 0.94
K1 is 2 K2 is 6 c is 0.96
K1 is 2 K2 is 6 c is 0.98
K1 is 3 K2 is 2 c is 0.80
K1 is 3 K2 is 2 c is 0.82
K1 is 3 K2 is 2 c is 0.84
K1 is 3 K2 is 2 c is 0.86
K1 is 3 K2 is 2 c is 0.88
K1 is 3 K2 is 2 c is 0.90
K1 is 3 K2 is 2 c is 0.92
K1 is 3 K2 is 2 c is 0.94
K1 is 3 K2 is 2 c is 0.96
K1 is 3 K2 is 2 c is 0.98
K1 is 3 K2 is 3 c is 0.80
K1 is 3 K2 is 3 c is 0.82
K1 is 3 K2 is 3 c is 0.84
K1 is 3 K2 is 3 c is 0.86
K1 is 3 K2 is 3 c is 0.88
K1 is 3 K2 is 2 c is 0.90
K1 is 3 K2 is 2 c is 0.92
K1 is 3 K2 is 2 c is 0.94
K1 is 3 K2 is 2 c is 0.96
K1 is 3 K2 is 2 c is 0.98
K1 is 3 K2 is 3 c is 0.80
K1 is 3 K2 is 3 c is 0.82
K1 is 3 K2 is 3 c is 0.84
K1 is 3 K2 is 3 c is 0.86
K1 is 3 K2 is 3 c is 0.88
K1 is 3 K2 is 3 c is 0.90
K1 is 3 K2 is 3 c is 0.92
K1 is 3 K2 is 3 c is 0.94
K1 is 3 K2 is 3 c is 0.96
K1 is 3 K2 is 3 c is 0.98
K1 is 3 K2 is 4 c is 0.80
K1 is 3 K2 is 4 c is 0.82
K1 is 3 K2 is 4 c is 0.84
K1 is 3 K2 is 4 c is 0.86
K1 is 3 K2 is 4 c is 0.88
K1 is 3 K2 is 4 c is 0.90
K1 is 3 K2 is 4 c is 0.92
K1 is 3 K2 is 4 c is 0.94
K1 is 3 K2 is 4 c is 0.96
K1 is 3 K2 is 4 c is 0.98
K1 is 3 K2 is 5 c is 0.80
K1 is 3 K2 is 5 c is 0.82
K1 is 3 K2 is 5 c is 0.84
K1 is 3 K2 is 5 c is 0.86
K1 is 3 K2 is 5 c is 0.88
K1 is 3 K2 is 5 c is 0.90
K1 is 3 K2 is 5 c is 0.92
K1 is 3 K2 is 5 c is 0.94
K1 is 3 K2 is 5 c is 0.96
K1 is 3 K2 is 5 c is 0.98
K1 is 3 K2 is 6 c is 0.80
K1 is 3 K2 is 6 c is 0.82
K1 is 3 K2 is 6 c is 0.84
K1 is 3 K2 is 6 c is 0.86
K1 is 3 K2 is 6 c is 0.88
K1 is 3 K2 is 6 c is 0.90
K1 is 3 K2 is 6 c is 0.92
K1 is 3 K2 is 6 c is 0.94
K1 is 3 K2 is 6 c is 0.96
K1 is 3 K2 is 6 c is 0.98
K1 is 4 K2 is 2 c is 0.80
K1 is 4 K2 is 2 c is 0.82
K1 is 4 K2 is 2 c is 0.84
K1 is 4 K2 is 2 c is 0.86
K1 is 4 K2 is 2 c is 0.88
K1 is 4 K2 is 2 c is 0.90
K1 is 4 K2 is 2 c is 0.92
K1 is 4 K2 is 2 c is 0.94
K1 is 4 K2 is 2 c is 0.96
K1 is 4 K2 is 2 c is 0.98
K1 is 4 K2 is 3 c is 0.80
K1 is 4 K2 is 3 c is 0.82
K1 is 4 K2 is 3 c is 0.84
K1 is 4 K2 is 3 c is 0.86
K1 is 4 K2 is 3 c is 0.88
K1 is 4 K2 is 3 c is 0.90
K1 is 4 K2 is 3 c is 0.92
K1 is 4 K2 is 3 c is 0.94
K1 is 4 K2 is 3 c is 0.96
K1 is 4 K2 is 3 c is 0.98
K1 is 4 K2 is 4 c is 0.80
K1 is 4 K2 is 4 c is 0.82
K1 is 4 K2 is 4 c is 0.84
K1 is 4 K2 is 4 c is 0.86
K1 is 4 K2 is 4 c is 0.88
K1 is 4 K2 is 4 c is 0.90
K1 is 4 K2 is 4 c is 0.92
K1 is 4 K2 is 4 c is 0.94
K1 is 4 K2 is 4 c is 0.96
K1 is 4 K2 is 4 c is 0.98
K1 is 4 K2 is 5 c is 0.80
K1 is 4 K2 is 5 c is 0.82
K1 is 4 K2 is 5 c is 0.84
K1 is 4 K2 is 5 c is 0.86
K1 is 4 K2 is 5 c is 0.88
K1 is 4 K2 is 5 c is 0.90
K1 is 4 K2 is 5 c is 0.92
K1 is 4 K2 is 5 c is 0.94
K1 is 4 K2 is 5 c is 0.96
K1 is 4 K2 is 5 c is 0.98
K1 is 4 K2 is 6 c is 0.80
K1 is 4 K2 is 6 c is 0.82
K1 is 4 K2 is 6 c is 0.84
K1 is 4 K2 is 6 c is 0.86
K1 is 4 K2 is 6 c is 0.88
K1 is 4 K2 is 6 c is 0.90
K1 is 4 K2 is 6 c is 0.92
K1 is 4 K2 is 6 c is 0.94
K1 is 4 K2 is 6 c is 0.96
K1 is 4 K2 is 6 c is 0.98
K1 is 5 K2 is 2 c is 0.80
K1 is 5 K2 is 2 c is 0.82
K1 is 5 K2 is 2 c is 0.84
K1 is 5 K2 is 2 c is 0.86
K1 is 5 K2 is 2 c is 0.88
K1 is 5 K2 is 2 c is 0.90
K1 is 5 K2 is 2 c is 0.92
K1 is 5 K2 is 2 c is 0.94
K1 is 5 K2 is 2 c is 0.96
K1 is 5 K2 is 2 c is 0.98
K1 is 5 K2 is 3 c is 0.80
K1 is 5 K2 is 3 c is 0.82
K1 is 5 K2 is 3 c is 0.84
K1 is 5 K2 is 3 c is 0.86
K1 is 5 K2 is 3 c is 0.88
K1 is 5 K2 is 3 c is 0.90
K1 is 5 K2 is 3 c is 0.92
K1 is 5 K2 is 3 c is 0.94
K1 is 5 K2 is 3 c is 0.96
K1 is 5 K2 is 3 c is 0.98
K1 is 5 K2 is 4 c is 0.80
K1 is 5 K2 is 4 c is 0.82
K1 is 5 K2 is 4 c is 0.84
K1 is 5 K2 is 4 c is 0.86
K1 is 5 K2 is 4 c is 0.88
K1 is 5 K2 is 4 c is 0.90
K1 is 5 K2 is 4 c is 0.92
K1 is 5 K2 is 4 c is 0.94
K1 is 5 K2 is 4 c is 0.96
K1 is 5 K2 is 4 c is 0.98
K1 is 5 K2 is 5 c is 0.80
K1 is 5 K2 is 5 c is 0.82
K1 is 5 K2 is 5 c is 0.84
K1 is 5 K2 is 5 c is 0.86
K1 is 5 K2 is 5 c is 0.88
K1 is 5 K2 is 5 c is 0.90
K1 is 5 K2 is 5 c is 0.92
K1 is 5 K2 is 5 c is 0.94
K1 is 5 K2 is 5 c is 0.96
K1 is 5 K2 is 5 c is 0.98
K1 is 5 K2 is 6 c is 0.80
K1 is 5 K2 is 6 c is 0.82
K1 is 5 K2 is 6 c is 0.84
K1 is 5 K2 is 6 c is 0.86
K1 is 5 K2 is 6 c is 0.88
K1 is 5 K2 is 6 c is 0.90
K1 is 5 K2 is 6 c is 0.92
K1 is 5 K2 is 6 c is 0.94
K1 is 5 K2 is 6 c is 0.96
K1 is 5 K2 is 6 c is 0.98
K1 is 6 K2 is 2 c is 0.80
K1 is 6 K2 is 2 c is 0.82
K1 is 6 K2 is 2 c is 0.84
K1 is 6 K2 is 2 c is 0.86
K1 is 6 K2 is 2 c is 0.88
K1 is 6 K2 is 2 c is 0.90
K1 is 6 K2 is 2 c is 0.92
K1 is 6 K2 is 2 c is 0.94
K1 is 6 K2 is 2 c is 0.96
K1 is 6 K2 is 2 c is 0.98
K1 is 6 K2 is 3 c is 0.80
K1 is 6 K2 is 3 c is 0.82
K1 is 6 K2 is 3 c is 0.84
K1 is 6 K2 is 3 c is 0.86
K1 is 6 K2 is 3 c is 0.88
K1 is 6 K2 is 3 c is 0.90
K1 is 6 K2 is 3 c is 0.92
K1 is 6 K2 is 3 c is 0.94
K1 is 6 K2 is 3 c is 0.96
K1 is 6 K2 is 3 c is 0.98
K1 is 6 K2 is 4 c is 0.80
K1 is 6 K2 is 4 c is 0.82
K1 is 6 K2 is 4 c is 0.84
K1 is 6 K2 is 4 c is 0.86
K1 is 6 K2 is 4 c is 0.88
K1 is 6 K2 is 4 c is 0.90
K1 is 6 K2 is 4 c is 0.92
K1 is 6 K2 is 4 c is 0.94
K1 is 6 K2 is 4 c is 0.96
K1 is 6 K2 is 4 c is 0.98
K1 is 6 K2 is 5 c is 0.80
K1 is 6 K2 is 5 c is 0.82
K1 is 6 K2 is 5 c is 0.84
K1 is 6 K2 is 5 c is 0.86
K1 is 6 K2 is 5 c is 0.88
K1 is 6 K2 is 5 c is 0.90
K1 is 6 K2 is 5 c is 0.92
K1 is 6 K2 is 5 c is 0.94
K1 is 6 K2 is 5 c is 0.96
K1 is 6 K2 is 5 c is 0.98
K1 is 6 K2 is 6 c is 0.80
K1 is 6 K2 is 6 c is 0.82
K1 is 6 K2 is 6 c is 0.84
K1 is 6 K2 is 6 c is 0.86
K1 is 6 K2 is 6 c is 0.88
K1 is 6 K2 is 6 c is 0.90
K1 is 6 K2 is 6 c is 0.92
K1 is 6 K2 is 6 c is 0.94
K1 is 6 K2 is 6 c is 0.96
K1 is 6 K2 is 6 c is 0.98

                                         Histogram of number of reference contigs

     10 +-----------------------------------------------------------------------------------------------------------+
        |  *           +               +              +               +              +               +              |
        |  *                                                'plot.kopt.data' using (bin($1,binwidth)):(1.0) ******* |
        |  *                                                                                                        |
        |  *                                                                                                        |
      8 |-+*                                                                                                      +-|
        |  *                                                                                                        |
        | **      **                                                                                                |
        | **      **                                                                                                |
      6 |-** *  ****     ***                                                                                      +-|
        | ** *  ****     ***                                                                                        |
        |*** *  *******  *****                                                                                      |
        |*** *  *******  *****                                                                                      |
        |*** *  *******  *****                                                                                      |
      4 |*** *  *******  *****  *     ****              **                                                        +-|
        |*** *  *******  *****  *     ****              **                                                          |
        |*****  *******  ***** **    ******            **** *** **                                                  |
        |*****  *******  ***** **    ******            **** *** **                                                  |
      2 |**************  ********   *********** ****  ************                                  *             +-|
        |**************  ********   ********* * * **  ************                                  *               |
        |**************  ********   ********* * * **  ************                                  *               |
        |************************************ *** *************************************************************     |
        |************************************ * * ** **************** *              *             **+**  *  **     |
      0 +-----------------------------------------------------------------------------------------------------------+
      15000          20000           25000          30000           35000          40000           45000          50000
                                                 Number of reference contigs

Average contig number = 23432.5
The top three most common number of contigs
X       Contig number
2       18025
2       15972
1       48007
The top three most common number of contigs (with values rounded)
X       Contig number
7       15800
6       16000
5       18600

```

![]({{site.baseurl}}/images/mod_pipeline/cluster_variation/clust1/ReferenceOpt_clust_1.png)
The plot shows 0.9 as the optimal similarity threshold.


2. RefMapOpt.sh

`RefMapOpt.sh 2 6 2 6 0.9 PE 20`

#### Cluster 2: 

1. ReferenceOpt.sh

```shell
ReferenceOpt.sh 2 6 2 6 PE 20

All required software is installed!

dDocent ReferenceOpt version 2.7.8
K1 is 2 K2 is 2 c is 0.80
K1 is 2 K2 is 2 c is 0.82
K1 is 2 K2 is 2 c is 0.84
K1 is 2 K2 is 2 c is 0.86
K1 is 2 K2 is 2 c is 0.88
K1 is 2 K2 is 2 c is 0.90
K1 is 2 K2 is 2 c is 0.92
K1 is 2 K2 is 2 c is 0.94
K1 is 2 K2 is 2 c is 0.96
K1 is 2 K2 is 2 c is 0.98
K1 is 2 K2 is 3 c is 0.80
K1 is 2 K2 is 3 c is 0.82
K1 is 2 K2 is 3 c is 0.84
K1 is 2 K2 is 3 c is 0.86
K1 is 2 K2 is 3 c is 0.88
K1 is 2 K2 is 3 c is 0.90
K1 is 2 K2 is 3 c is 0.92
K1 is 2 K2 is 3 c is 0.94
K1 is 2 K2 is 3 c is 0.96
K1 is 2 K2 is 3 c is 0.98
K1 is 2 K2 is 4 c is 0.80
K1 is 2 K2 is 4 c is 0.82
K1 is 2 K2 is 4 c is 0.84
K1 is 2 K2 is 4 c is 0.86
K1 is 2 K2 is 4 c is 0.88
K1 is 2 K2 is 4 c is 0.90
K1 is 2 K2 is 4 c is 0.92
K1 is 2 K2 is 4 c is 0.94
K1 is 2 K2 is 4 c is 0.96
K1 is 2 K2 is 4 c is 0.98
K1 is 2 K2 is 5 c is 0.80
K1 is 2 K2 is 5 c is 0.82
K1 is 2 K2 is 5 c is 0.84
K1 is 2 K2 is 5 c is 0.86
K1 is 2 K2 is 5 c is 0.88
K1 is 2 K2 is 5 c is 0.90
K1 is 2 K2 is 5 c is 0.92
K1 is 2 K2 is 5 c is 0.94
K1 is 2 K2 is 5 c is 0.96
K1 is 2 K2 is 5 c is 0.98
K1 is 2 K2 is 6 c is 0.80
K1 is 2 K2 is 6 c is 0.82
K1 is 2 K2 is 6 c is 0.84
K1 is 2 K2 is 6 c is 0.86
K1 is 2 K2 is 6 c is 0.88
K1 is 2 K2 is 6 c is 0.90
K1 is 2 K2 is 6 c is 0.92
K1 is 2 K2 is 6 c is 0.94
K1 is 2 K2 is 6 c is 0.96
K1 is 2 K2 is 6 c is 0.98
K1 is 3 K2 is 2 c is 0.80
K1 is 3 K2 is 2 c is 0.82
K1 is 3 K2 is 2 c is 0.84
K1 is 3 K2 is 2 c is 0.86
K1 is 3 K2 is 2 c is 0.88
K1 is 3 K2 is 2 c is 0.90
K1 is 3 K2 is 2 c is 0.92
K1 is 3 K2 is 2 c is 0.94
K1 is 3 K2 is 2 c is 0.96
K1 is 3 K2 is 2 c is 0.98
K1 is 3 K2 is 3 c is 0.80
K1 is 3 K2 is 3 c is 0.82
K1 is 3 K2 is 3 c is 0.84
K1 is 3 K2 is 3 c is 0.86
K1 is 3 K2 is 3 c is 0.88
K1 is 3 K2 is 3 c is 0.90
K1 is 3 K2 is 3 c is 0.92
K1 is 3 K2 is 3 c is 0.94
K1 is 3 K2 is 3 c is 0.96
K1 is 3 K2 is 3 c is 0.98
K1 is 3 K2 is 4 c is 0.80
K1 is 3 K2 is 4 c is 0.82
K1 is 3 K2 is 4 c is 0.84
K1 is 3 K2 is 4 c is 0.86
K1 is 3 K2 is 4 c is 0.88
K1 is 3 K2 is 4 c is 0.90
K1 is 3 K2 is 4 c is 0.92
K1 is 3 K2 is 4 c is 0.94
K1 is 3 K2 is 4 c is 0.96
K1 is 3 K2 is 4 c is 0.98
K1 is 3 K2 is 5 c is 0.80
K1 is 3 K2 is 5 c is 0.82
K1 is 3 K2 is 5 c is 0.84
K1 is 3 K2 is 5 c is 0.86
K1 is 3 K2 is 5 c is 0.88
K1 is 3 K2 is 5 c is 0.90
K1 is 3 K2 is 5 c is 0.92
K1 is 3 K2 is 5 c is 0.94
K1 is 3 K2 is 5 c is 0.96
K1 is 3 K2 is 5 c is 0.98
K1 is 3 K2 is 6 c is 0.80
K1 is 3 K2 is 6 c is 0.82
K1 is 3 K2 is 6 c is 0.84
K1 is 3 K2 is 6 c is 0.86
K1 is 3 K2 is 6 c is 0.88
K1 is 3 K2 is 6 c is 0.90
K1 is 3 K2 is 6 c is 0.92
K1 is 3 K2 is 6 c is 0.94
K1 is 3 K2 is 6 c is 0.96
K1 is 3 K2 is 6 c is 0.98
K1 is 4 K2 is 2 c is 0.80
K1 is 4 K2 is 2 c is 0.82
K1 is 4 K2 is 2 c is 0.84
K1 is 4 K2 is 2 c is 0.86
K1 is 4 K2 is 2 c is 0.88
K1 is 4 K2 is 2 c is 0.90
K1 is 4 K2 is 2 c is 0.92
K1 is 4 K2 is 2 c is 0.94
K1 is 4 K2 is 2 c is 0.96
K1 is 4 K2 is 2 c is 0.98
K1 is 4 K2 is 3 c is 0.80
K1 is 4 K2 is 3 c is 0.82
K1 is 4 K2 is 3 c is 0.84
K1 is 4 K2 is 3 c is 0.86
K1 is 4 K2 is 3 c is 0.88
K1 is 4 K2 is 3 c is 0.90
K1 is 4 K2 is 3 c is 0.92
K1 is 4 K2 is 3 c is 0.94
K1 is 4 K2 is 3 c is 0.96
K1 is 4 K2 is 3 c is 0.98
K1 is 4 K2 is 4 c is 0.80
K1 is 4 K2 is 4 c is 0.82
K1 is 4 K2 is 4 c is 0.84
K1 is 4 K2 is 4 c is 0.86
K1 is 4 K2 is 4 c is 0.88
K1 is 4 K2 is 4 c is 0.90
K1 is 4 K2 is 4 c is 0.92
K1 is 4 K2 is 4 c is 0.94
K1 is 4 K2 is 4 c is 0.96
K1 is 4 K2 is 4 c is 0.98
K1 is 4 K2 is 5 c is 0.80
K1 is 4 K2 is 5 c is 0.82
K1 is 4 K2 is 5 c is 0.84
K1 is 4 K2 is 5 c is 0.86
K1 is 4 K2 is 5 c is 0.88
K1 is 4 K2 is 5 c is 0.90
K1 is 4 K2 is 5 c is 0.92
K1 is 4 K2 is 5 c is 0.94
K1 is 4 K2 is 5 c is 0.96
K1 is 4 K2 is 5 c is 0.98
K1 is 4 K2 is 6 c is 0.80
K1 is 4 K2 is 6 c is 0.82
K1 is 4 K2 is 6 c is 0.84
K1 is 4 K2 is 6 c is 0.86
K1 is 4 K2 is 6 c is 0.88
K1 is 4 K2 is 6 c is 0.90
K1 is 4 K2 is 6 c is 0.92
K1 is 4 K2 is 6 c is 0.94
K1 is 4 K2 is 6 c is 0.96
K1 is 4 K2 is 6 c is 0.98
K1 is 5 K2 is 2 c is 0.80
K1 is 5 K2 is 2 c is 0.82
K1 is 5 K2 is 2 c is 0.84
K1 is 5 K2 is 2 c is 0.86
K1 is 5 K2 is 2 c is 0.88
K1 is 5 K2 is 2 c is 0.90
K1 is 5 K2 is 2 c is 0.92
K1 is 5 K2 is 2 c is 0.94
K1 is 5 K2 is 2 c is 0.96
K1 is 5 K2 is 2 c is 0.98
K1 is 5 K2 is 3 c is 0.80
K1 is 5 K2 is 3 c is 0.82
K1 is 5 K2 is 3 c is 0.84
K1 is 5 K2 is 3 c is 0.86
K1 is 5 K2 is 3 c is 0.88
K1 is 5 K2 is 3 c is 0.90
K1 is 5 K2 is 3 c is 0.92
K1 is 5 K2 is 3 c is 0.94
K1 is 5 K2 is 3 c is 0.96
K1 is 5 K2 is 3 c is 0.98
K1 is 5 K2 is 4 c is 0.80
K1 is 5 K2 is 4 c is 0.82
K1 is 5 K2 is 4 c is 0.84
K1 is 5 K2 is 4 c is 0.86
K1 is 5 K2 is 4 c is 0.88
K1 is 5 K2 is 4 c is 0.90
K1 is 5 K2 is 4 c is 0.92
K1 is 5 K2 is 4 c is 0.94
K1 is 5 K2 is 4 c is 0.96
K1 is 5 K2 is 4 c is 0.98
K1 is 5 K2 is 5 c is 0.80
K1 is 5 K2 is 5 c is 0.82
K1 is 5 K2 is 5 c is 0.84
K1 is 5 K2 is 5 c is 0.86
K1 is 5 K2 is 5 c is 0.88
K1 is 5 K2 is 5 c is 0.90
K1 is 5 K2 is 5 c is 0.92
K1 is 5 K2 is 5 c is 0.94
K1 is 5 K2 is 5 c is 0.96
K1 is 5 K2 is 5 c is 0.98
K1 is 5 K2 is 6 c is 0.80
K1 is 5 K2 is 6 c is 0.82
K1 is 5 K2 is 6 c is 0.84
K1 is 5 K2 is 6 c is 0.86
K1 is 5 K2 is 6 c is 0.88
K1 is 5 K2 is 6 c is 0.90
K1 is 5 K2 is 6 c is 0.92
K1 is 5 K2 is 6 c is 0.94
K1 is 5 K2 is 6 c is 0.96
K1 is 5 K2 is 6 c is 0.98
K1 is 6 K2 is 2 c is 0.80
K1 is 6 K2 is 2 c is 0.82
K1 is 6 K2 is 2 c is 0.84
K1 is 6 K2 is 2 c is 0.86
K1 is 6 K2 is 2 c is 0.88
K1 is 6 K2 is 2 c is 0.90
K1 is 6 K2 is 2 c is 0.92
K1 is 6 K2 is 2 c is 0.94
K1 is 6 K2 is 2 c is 0.96
K1 is 6 K2 is 2 c is 0.98
K1 is 6 K2 is 3 c is 0.80
K1 is 6 K2 is 3 c is 0.82
K1 is 6 K2 is 3 c is 0.84
K1 is 6 K2 is 3 c is 0.86
K1 is 6 K2 is 3 c is 0.88
K1 is 6 K2 is 3 c is 0.90
K1 is 6 K2 is 3 c is 0.92
K1 is 6 K2 is 3 c is 0.94
K1 is 6 K2 is 3 c is 0.96
K1 is 6 K2 is 3 c is 0.98
K1 is 6 K2 is 4 c is 0.80
K1 is 6 K2 is 4 c is 0.82
K1 is 6 K2 is 4 c is 0.84
K1 is 6 K2 is 4 c is 0.86
K1 is 6 K2 is 4 c is 0.88
K1 is 6 K2 is 4 c is 0.90
K1 is 6 K2 is 4 c is 0.92
K1 is 6 K2 is 4 c is 0.94
K1 is 6 K2 is 4 c is 0.96
K1 is 6 K2 is 4 c is 0.98
K1 is 6 K2 is 5 c is 0.80
K1 is 6 K2 is 5 c is 0.82
K1 is 6 K2 is 5 c is 0.84
K1 is 6 K2 is 5 c is 0.86
K1 is 6 K2 is 5 c is 0.88
K1 is 6 K2 is 5 c is 0.90
K1 is 6 K2 is 5 c is 0.92
K1 is 6 K2 is 5 c is 0.94
K1 is 6 K2 is 5 c is 0.96
K1 is 6 K2 is 5 c is 0.98
K1 is 6 K2 is 6 c is 0.80
K1 is 6 K2 is 6 c is 0.82
K1 is 6 K2 is 6 c is 0.84
K1 is 6 K2 is 6 c is 0.86
K1 is 6 K2 is 6 c is 0.88
K1 is 6 K2 is 6 c is 0.90
K1 is 6 K2 is 6 c is 0.92
K1 is 6 K2 is 6 c is 0.94
K1 is 6 K2 is 6 c is 0.96
K1 is 6 K2 is 6 c is 0.98

                                         Histogram of number of reference contigs

     8 +------------------------------------------------------------------------------------------------------------+
       |     *               +                     +                    +                     +                     |
       |     *                                              'plot.kopt.data' using (bin($1,binwidth)):(1.0) ******* |
     7 |-+*****        ***                                                                                        +-|
       |  *****        ***                                                                                          |
       |  *****        ***                                                                                          |
     6 |-+*******      **** *                          **                                                         +-|
       |  *******      **** *                          **                                                           |
       |  *******      **** *                          **                                                           |
     5 |-+*******     ***** *        *** **            **                    **                                   +-|
       |  *******     ***** *        *** **            **                    **                                     |
     4 |-+*******     ***** *      ***** **         *****   **            ** **  **                               +-|
       |  *******     ***** *      ***** **         *****   **            ** **  **                                 |
       |  *******     ***** *      ***** **         *****   **            ** **  **                                 |
     3 |-+*******     *******      ********       ********  **            ****** **                               +-|
       |  *******     *******      ********       ********  **            ****** **                                 |
       |  *******     *******      ********       ********  **            ****** **                                 |
     2 |-+*******     *******   ************      ************            **********                     ***      +-|
       |  *******     *******   *  *********      ************            **********                     ***        |
       |  *******     *******   *  *********      ************            **********                     ***        |
     1 |-+***********************  *********************************************************************************|
       |  ******** *  ********* *  **********  *  ************** *   *   ************** *        *       *** * *  * |
       |  ******** *  ********* *  **********  *  ************** *   *  +************** *     +  *       *** * *  * |
     0 +------------------------------------------------------------------------------------------------------------+
     10000                 15000                 20000                25000                 30000                 35000
                                                Number of reference contigs

Average contig number = 18333.3
The top three most common number of contigs
X       Contig number
1       34817
1       34145
1       33632
The top three most common number of contigs (with values rounded)
X       Contig number
7       11600
7       11300
7       11000


```
![]({{site.baseurl}}/images/mod_pipeline/cluster_variation/clust2/ReferenceOpt_clust_2.png)
The plot shows 0.9 as the optimal similarity threshold.


2. RefMapOpt.sh

`RefMapOpt.sh 2 6 2 6 0.9 PE 20`

```shell
❯ column -t -s $'\t' mapping.results
Cov      Non0Cov  Contigs  MeanContigsMapped  K1  K2  SUM Mapped  SUM Properly  Mean Mapped  Mean Properly  MisMatched
136.944  185.375  32866    24160.7            2   2   31506644    29224835      4.50095e+06  4.17498e+06    94539.9
190.862  217.077  22239    19499              2   3   29713432    27847038      4244776      3.97815e+06    54490.1
218.583  234.285  17991    16752.1            2   4   27529237    25865733      3.93275e+06  3.6951e+06     37203.7
242.109  252.244  14812    14200.4            2   5   25104475    23604313      3.58635e+06  3.37204e+06    31076.9
262.57   269.217  11980    11673.6            2   6   22020948    20586322      3.14585e+06  2.9409e+06     26010.3
166.223  204.911  26999    21809.3            3   2   31416156    29208349      4.48802e+06  4.17262e+06    86443.6
200.035  224.409  21130    18784.4            3   3   29588554    27627641      4.22694e+06  3.94681e+06    64797.1
225.696  240.927  17433    16297.9            3   4   27543510    25895090      3.93479e+06  3.6993e+06     37901.9
246.189  255.928  14351    13788.6            3   5   24733147    23243978      3.53331e+06  3.32057e+06    32408.1
266.188  272.636  11592    11308.1            3   6   21601434    20224808      3.08592e+06  2.88926e+06    27398.9
170.772  208.716  26177    21325.7            4   2   31293296    29124020      4.47047e+06  4.16057e+06    86572.6
203.857  227.851  20693    18459.7            4   3   29530371    27602551      4.21862e+06  3.94322e+06    61493.1
229.289  244.259  17085    16003.9            4   4   27423400    25795048      3.91763e+06  3.68501e+06    35259.4
250.082  259.66   14047    13512              4   5   24592124    23115844      3.51316e+06  3.30226e+06    30427.6
269.912  276.206  11325    11056.4            4   6   21399183    19996565      3.05703e+06  2.85665e+06    26775.1
173.256  210.955  25796    21089.7            5   2   31286323    29015273      4.46947e+06  4145039        101309
205.16   228.747  20398    18238.9            5   3   29295390    27444116      4.18506e+06  3920588        56877.9
231.117  245.767  16776    15741.1            5   4   27142198    25538579      3.87746e+06  3.64837e+06    33773.6
253.216  262.57   13748    13239.9            5   5   24370302    22902690      3.48147e+06  3.27181e+06    29392.9
273.423  279.688  11029    10772.1            5   6   21111002    19724281      3.01586e+06  2.81775e+06    25454.4
175.59   212.935  25458    20890.4            6   2   31292522    28969496      4.47036e+06  4.1385e+06     104483
208.173  231.435  20092    18013.7            6   3   29279778    27382110      4.18283e+06  3911730        53734.1
233.964  248.522  16499    15497.1            6   4   27022859    25409205      3.86041e+06  3.62989e+06    31701.7
255.553  264.653  13462    12979.1            6   5   24083598    22583410      3440514      3.2262e+06     28968.3
276.529  282.736  10760    10513.9            6   6   20830094    19421794      2.97573e+06  2774542        28466.9

❯ sort -k 10 -n -r  mapping.results | column -t -s $'\t'
173.256  210.955  25796    21089.7            5   2   31286323    29015273      4.46947e+06  4145039        101309
205.16   228.747  20398    18238.9            5   3   29295390    27444116      4.18506e+06  3920588        56877.9
208.173  231.435  20092    18013.7            6   3   29279778    27382110      4.18283e+06  3911730        53734.1
276.529  282.736  10760    10513.9            6   6   20830094    19421794      2.97573e+06  2774542        28466.9
136.944  185.375  32866    24160.7            2   2   31506644    29224835      4.50095e+06  4.17498e+06    94539.9
166.223  204.911  26999    21809.3            3   2   31416156    29208349      4.48802e+06  4.17262e+06    86443.6
170.772  208.716  26177    21325.7            4   2   31293296    29124020      4.47047e+06  4.16057e+06    86572.6
175.59   212.935  25458    20890.4            6   2   31292522    28969496      4.47036e+06  4.1385e+06     104483
190.862  217.077  22239    19499              2   3   29713432    27847038      4244776      3.97815e+06    54490.1
200.035  224.409  21130    18784.4            3   3   29588554    27627641      4.22694e+06  3.94681e+06    64797.1
203.857  227.851  20693    18459.7            4   3   29530371    27602551      4.21862e+06  3.94322e+06    61493.1
225.696  240.927  17433    16297.9            3   4   27543510    25895090      3.93479e+06  3.6993e+06     37901.9
218.583  234.285  17991    16752.1            2   4   27529237    25865733      3.93275e+06  3.6951e+06     37203.7
229.289  244.259  17085    16003.9            4   4   27423400    25795048      3.91763e+06  3.68501e+06    35259.4
231.117  245.767  16776    15741.1            5   4   27142198    25538579      3.87746e+06  3.64837e+06    33773.6
233.964  248.522  16499    15497.1            6   4   27022859    25409205      3.86041e+06  3.62989e+06    31701.7
242.109  252.244  14812    14200.4            2   5   25104475    23604313      3.58635e+06  3.37204e+06    31076.9
246.189  255.928  14351    13788.6            3   5   24733147    23243978      3.53331e+06  3.32057e+06    32408.1
250.082  259.66   14047    13512              4   5   24592124    23115844      3.51316e+06  3.30226e+06    30427.6
253.216  262.57   13748    13239.9            5   5   24370302    22902690      3.48147e+06  3.27181e+06    29392.9
255.553  264.653  13462    12979.1            6   5   24083598    22583410      3440514      3.2262e+06     28968.3
262.57   269.217  11980    11673.6            2   6   22020948    20586322      3.14585e+06  2.9409e+06     26010.3
266.188  272.636  11592    11308.1            3   6   21601434    20224808      3.08592e+06  2.88926e+06    27398.9
269.912  276.206  11325    11056.4            4   6   21399183    19996565      3.05703e+06  2.85665e+06    26775.1
273.423  279.688  11029    10772.1            5   6   21111002    19724281      3.01586e+06  2.81775e+06    25454.4
Cov      Non0Cov  Contigs  MeanContigsMapped  K1  K2  SUM Mapped  SUM Properly  Mean Mapped  Mean Properly  MisMatched

Cov      Non0Cov  Contigs  MeanContigsMapped  K1  K2  SUM Mapped  SUM Properly  Mean Mapped  Mean Properly  MisMatched
136.944  185.375  32866    24160.7            2   2   31506644    29224835      4.50095e+06  4.17498e+06    94539.9
166.223  204.911  26999    21809.3            3   2   31416156    29208349      4.48802e+06  4.17262e+06    86443.6
170.772  208.716  26177    21325.7            4   2   31293296    29124020      4.47047e+06  4.16057e+06    86572.6
175.59   212.935  25458    20890.4            6   2   31292522    28969496      4.47036e+06  4.1385e+06     104483


```
**Top choice is K1=3 and K2=2 and used for assembly.** 
These parameters were used for the reference assembly that was built using dDocent.

### Step 7: Reference assembly per cluster

#### Cluster 1:

#### Cluster 2: 

```shell
Number of Processors
20
Maximum Memory
0
Trimming
no
Assembly?
yes
Type_of_Assembly
PE
Clustering_Similarity%
0.9
Minimum within individual coverage level to include a read for assembly (K1)
3
Minimum number of individuals a read must be present in to include for assembly (K2)
2
Mapping_Reads?
no
Mapping_Match_Value

Mapping_MisMatch_Value

Mapping_GapOpen_Penalty

Calling_SNPs?
no
Email
xxxx@uri.edu

```






