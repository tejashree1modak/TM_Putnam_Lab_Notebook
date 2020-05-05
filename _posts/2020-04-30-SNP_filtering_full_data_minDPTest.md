---
layout: post
title: SNP filtering full data set
tags: [ ddRAD, epiRAD, Moorea, dDocent, SNP, filter ]
---

## Step2: Minimum mean depth Testing at 2 values
With the full dataset testing 2 values of minDP 
##Minimum mean depth = 5

```shell
vcftools --vcf raw.g5mac3.recode.vcf --minDP 5 --recode --recode-INFO-all --out raw.g5mac3dp10

After filtering, kept 124 out of 124 Individuals
Outputting VCF file...
After filtering, kept 288777 out of a possible 288777 Sites`
```

### Step3: Filter missing indiv post minDP =5 

```shell
vcftools --vcf raw.g5mac3dp5.recode.vcf --missing-indv
cat out.imiss
mawk '!/IN/' out.imiss | cut -f5 > totalmissing
gnuplot << \EOF
set terminal dumb size 120, 30
set autoscale
unset label
set title "Histogram of % missing data per individual"
set ylabel "Number of Occurrences"
set xlabel "% of missing data"
set yr [0:100000]
binwidth=0.01
bin(x,width)=width*floor(x/width) + binwidth/2.0
plot 'totalmissing' using (bin($1,binwidth)):(1.0) smooth freq with boxes
pause -1
EOF
                                         Histogram of % missing data per individual

     25 +-----------------------------------------------------------------------------------------------------------+
        |       * * +           +           +           +           +           +           +           +           |
        |       * *                                           'totalmissing' using (bin($1,binwidth)):(1.0) ******* |
        |       * *                                                                                                 |
        |       * *                                                                                                 |
     20 |-+     * *                                                                                               +-|
        |      ** **                                                                                                |
        |      ** **                                                                                                |
        |      ** **                                                                                                |
     15 |-+    ** **                                                                                              +-|
        |      ** **                                                                                                |
        |      ** ***                                                                                               |
        |      ** ***                                                                                               |
        |    **** ***                                                                                               |
     10 |-+  **** ***                                                                                             +-|
        |    **** ***                                                                                               |
        |    **** ***                                                                                               |
        |    **** ***                                                                                               |
      5 |-+  **** ****                                                                                            +-|
        |    **** ****                                                                                              |
        |   ***** *****                                                                                             |
        |   ***** ********                                                                                         *|
        |   ***** ***** ********************************************************************************************|
      0 +-----------------------------------------------------------------------------------------------------------+
       0.1         0.2         0.3         0.4         0.5         0.6         0.7         0.8         0.9          1
                                                      % of missing data
```


With cutoff at 25%, the number of lowDP individuals are 11. 

```shell
mawk '$5 > 0.25' out.imiss | cut -f1 | less
INDV
EOB_182_epi
EOB_492_ddr
PBF_159_ddr
PBF_161_epi
WOB_35_epi
WOB_38_ddr
WOB_45_ddr
WOB_46_ddr
WOB_61_ddr
WOB_65_epi
WOF_232_epi
```

With cutoff at 30%, the number of lowDP indiv are 10

```shell
mawk '$5 > 0.25' out.imiss | cut -f1 | less
EOB_182_epi
EOB_492_ddr
PBF_159_ddr
PBF_161_epi
WOB_35_epi
WOB_38_ddr
WOB_45_ddr
WOB_46_ddr
WOB_61_ddr
WOB_65_epi

vcftools --vcf raw.g5mac3dp5.recode.vcf --remove lowDP.indv --recode --recode-INFO-all --out raw.g5mac3dplm
After filtering, kept 114 out of 124 Individuals
Outputting VCF file...
After filtering, kept 288777 out of a possible 288777 Sites
```
## Step2: Minimum mean depth Testing at 2 values
##Minimum mean depth = 10

```shell
vcftools --vcf raw.g5mac3.recode.vcf --minDP 10 --recode --recode-INFO-all --out raw.g5mac3dp10

After filtering, kept 124 out of 124 Individuals
Outputting VCF file...
After filtering, kept 288777 out of a possible 288777 Sites`
```

### Step3: Filter missing indiv post minDP=10

```shell
vcftools --vcf raw.g5mac3dp5.recode.vcf --missing-indv
cat out.imiss
mawk '!/IN/' out.imiss | cut -f5 > totalmissing
gnuplot << \EOF
set terminal dumb size 120, 30
set autoscale
unset label
set title "Histogram of % missing data per individual"
set ylabel "Number of Occurrences"
set xlabel "% of missing data"
set yr [0:100000]
binwidth=0.01
bin(x,width)=width*floor(x/width) + binwidth/2.0
plot 'totalmissing' using (bin($1,binwidth)):(1.0) smooth freq with boxes
pause -1
EOF

                                         Histogram of % missing data per individual

     18 +-----------------------------------------------------------------------------------------------------------+
        |       ****          +         +          +          +          +          +         +          +          |
        |       ****                                          'totalmissing' using (bin($1,binwidth)):(1.0) ******* |
     16 |-+     ****                                                                                              +-|
        |       ****                                                                                                |
     14 |-+     ****                                                                                              +-|
        |    ** *****                                                                                               |
        |    ** *****                                                                                               |
     12 |-+  ** *******                                                                                           +-|
        |    ** ***** *                                                                                             |
     10 |-+  ** ***** *                                                                                           +-|
        |    ** ***** *                                                                                             |
        |    ** ***** *                                                                                             |
      8 |-+  ** ***** *                                                                                           +-|
        |    ** ***** *                                                                                             |
      6 |-+  ******** ***                                                                                         +-|
        |    ** ***** * *                                                                                           |
        |    ** ***** * *                                                                                           |
      4 |-+  ** ***** * *                                                                                         +-|
        |    ** ***** * ** ***                                                                                      |
      2 |-+ *** ***** * ** * *                                                                         ***        +-|
        |   *** ***** * ** * *                                                                         * *          |
        |   *** ***** * **** *************************************************************************** **         |
      0 +-----------------------------------------------------------------------------------------------------------+
       0.1        0.2        0.3       0.4        0.5        0.6        0.7        0.8       0.9         1         1.1
                                                      % of missing data
```

With cut of 25%, number of lowDP indiv = 20

```
mawk '$5 > 0.25' out.imiss | cut -f1 | wc -l
INDV
EOB_175_ddr
EOB_178_ddr
EOB_182_epi
EOB_184_ddr
EOB_184_epi
EOB_492_ddr
PBF_158_epi
PBF_159_ddr
PBF_159_epi
PBF_161_epi
PBF_168_ddr
WOB_35_epi
WOB_38_ddr
WOB_45_ddr
WOB_46_ddr
WOB_49_epi
WOB_59_epi
WOB_61_ddr
WOB_65_epi
WOF_232_epi
```

With cutoff of 30%, number of lowDP indiv = 12

```
mawk '$5 > 0.3' out.imiss | cut -f1 | less
INDV
EOB_182_epi
EOB_184_ddr
EOB_492_ddr
PBF_159_ddr
PBF_161_epi
WOB_35_epi
WOB_38_ddr
WOB_45_ddr
WOB_46_ddr
WOB_61_ddr
WOB_65_epi
WOF_232_epi

vcftools --vcf raw.g5mac3dp10.recode.vcf --remove lowDP.indv --recode --recode-INFO-all --out raw.g5mac3dplm
After filtering, kept 112 out of 124 Individuals
Outputting VCF file...
After filtering, kept 288777 out of a possible 288777 Sites
```

























