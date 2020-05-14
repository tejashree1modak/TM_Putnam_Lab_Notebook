---
layout: post
title: SNP filtering ddRAD data set post trimming, assembly and mapping
tags: [ ddRAD, epiRAD, Moorea, dDocent, SNP, filter ]
---

#Step1: 50% of individuals, a minimum quality score of 30, and a minor allele count of 3

vcftools --vcf TotalRawSNPs.vcf --max-missing 0.5 --mac 3 --minQ 30 --recode --recode-INFO-all --out raw.g5mac3

## Step2: Minimum mean depth Testing at 2 values
minDP 5

```shell
vcftools --vcf raw.g5mac3.recode.vcf --minDP 5 --recode --recode-INFO-all --out raw.g5mac3dp5

After filtering, kept 62 out of 62 Individuals
Outputting VCF file...
After filtering, kept 218805 out of a possible 218805 Sites
```
## Step3: Filter missing indiv post minDP =5

```shell
./filter_missing_ind.sh raw.g5mac3dp5.recode.vcf raw.g5mac3dplm


                                          Histogram of % missing data per individual

       12 +---------------------------------------------------------------------------------------------------------+
          |    **     +           +          +           +           +           +          +           +           |
          |    **                                             'totalmissing' using (bin($1,binwidth)):(1.0) ******* |
          |    **                                                                                                   |
       10 |-+  ****                                                                                               +-|
          |    ****                                                                                                 |
          |    *****                                                                                                |
          |    *****                                                                                                |
        8 |-+  *****                                                                                              +-|
          |    *****                                                                                                |
          |    *******                                                                                              |
        6 |-+  ***** *                                                                                            +-|
          |    ***** *                                                                                              |
          |    ***** *                                                                                              |
          |    ***** *                                                                                              |
        4 |-+  ***** **                                                                                           +-|
          |    ***** **                                                                                             |
          |    ***** **                                                                                             |
          |    ***** **                                                                                             |
        2 |-+ ****** **        *********                                                                          +-|
          |   ****** **        *       *                                                                            |
          | ******** ***********       **************************************************************************** |
          | * ****** *** *     *  +    *     +        *  +           +*          +          +  *        +         * |
        0 +---------------------------------------------------------------------------------------------------------+
         0.1         0.2         0.3        0.4         0.5         0.6         0.7        0.8         0.9          1
                                                       % of missing data

The 85% cutoff would be 0.205315
Would you like to set a different cutoff, yes or no
yes
0.35

After filtering, kept 58 out of 62 Individuals
Outputting VCF file...
After filtering, kept 218805 out of a possible 218805 Sites
```
Choosing 70% cutof

```shell
mawk '$5 > 0.35' raw.g5mac3dplm.imiss | cut -f1 | less
INDV
PBF_159_ddr
WOB_38_ddr
WOB_46_ddr
WOB_61_ddr
```
## Step4: Restrict the data to variants called in a high percentage of individuals and filter by mean depth of genotypes
This applied a genotype call rate (95%) across all individuals. Setting maf = 0.001

```shell
vcftools --vcf raw.g5mac3dplm.recode.vcf --max-missing 0.95 --maf 0.001 --recode --recode-INFO-all --out DP3g95maf001 --min-meanDP 20

After filtering, kept 58 out of 58 Individuals
Outputting VCF file...
After filtering, kept 94587 out of a possible 218805 Sites
```
## Step5: Filtering by population specific call rate when multiple localities are present

```shell
cut -f1 raw.g5mac3dplm.imiss|awk  -F "_" 'NR>1{print $1"_"$2"_"$3,$1}' > popmap
cat popmap
mawk '$2 == "EOB"' popmap > 1.keep && mawk '$2 == "PBF"' popmap > 2.keep && mawk '$2 == "WOB"' popmap > 3.keep && mawk '$2 == "WOF"' popmap > 4.keep
vcftools --vcf DP3g95maf001.recode.vcf --keep 1.keep --missing-site --out 1
vcftools --vcf DP3g95maf001.recode.vcf --keep 2.keep --missing-site --out 2
vcftools --vcf DP3g95maf001.recode.vcf --keep 3.keep --missing-site --out 3
vcftools --vcf DP3g95maf001.recode.vcf --keep 4.keep --missing-site --out 4
cat 1.lmiss 2.lmiss 3.lmiss 4.lmiss | mawk '!/CHR/' | mawk '$6 > 0.1' | cut -f1,2 >> badloci
vcftools --vcf DP3g95maf001.recode.vcf --exclude-positions badloci --recode --recode-INFO-all --out DP3g95p5maf001

After filtering, kept 58 out of 58 Individuals
Outputting VCF file...
After filtering, kept 91703 out of a possible 94587 Sites
```
## Step6: Used dDocent_filters script

```shell
./dDocent_filters DP3g95p5maf001.recode.vcf dDocent_filters_out

Number of sites filtered based on allele balance at heterozygous loci, locus quality, and mapping quality / Depth
 12289 of 91703

Are reads expected to overlap?  In other words, is fragment size less than 2X the read length?  Enter yes or no.
no

Number of additional sites filtered based on overlapping forward and reverse reads
 10242 of 79414

Is this from a mixture of SE and PE libraries? Enter yes or no.
no

Number of additional sites filtered based on properly paired status
 1445 of 69172

Number of sites filtered based on high depth and lower than 2*DEPTH quality score
 5730 of 67727


                                               Histogram of mean depth per site

     1000 +---------------------------------------------------------------------------------------------------------+
          |     +    +    +    +     +    +    +**  *     +    +    +     +    +    +    +     +    +    +    +     |
      900 |-+                                   *** * *** *meandepthpersite' using (bin($1,binwidth)):(1.0) *******-|
          |                                  ************ *                                                         |
          |                                  **************                                                         |
      800 |-+                                **************                                                       +-|
          |                                  **************                                                         |
      700 |-+                            ** ****************                                                      +-|
          |                              *******************                                                        |
      600 |-+                          ********************* *                                                    +-|
          |                            ***********************                                                      |
      500 |-+                        ***************************                                                  +-|
          |                          *************************** ***                                                |
          |                          ********************************                                               |
      400 |-+                      *********************************** **                                         +-|
          |                     ** ***************************************  *                                       |
      300 |-+                   ********************************************** *                                  +-|
          |                  *************************************************** *                                  |
      200 |-+                **********************************************************                           +-|
          |                *************************************************************  *                         |
          |              **********************************************************************     **              |
      100 |-+            **********************************************************************************       +*|
          |     +  *************************************************************************************************|
        0 +---------------------------------------------------------------------------------------------------------+
          11    22   33   44   55    66   77   88   99   110  121  132   143  154  165  176   187  198  209  220   231
                                                          Mean Depth

If distrubtion looks normal, a 1.645 sigma cutoff (~90% of the data) would be 13238.745
The 95% cutoff would be 211
Would you like to use a different maximum mean depth cutoff than 211, yes or no
no
Number of sites filtered based on maximum mean depth
 4055 of 67727

Number of sites filtered based on within locus depth mismatch
 14 of 63672

Total number of sites filtered
 28045 of 91703

Remaining sites
 63658

Filtered VCF file is called Output_prefix.FIL.recode.vcf

Filter stats stored in dDocent_filters_out.filterstats
```

## Step7: Convert our variant calls to SNPs

```shell

vcfallelicprimitives dDocent_filters_out.FIL.recode.vcf --keep-info --keep-geno > DP3g95p5maf001.prim.vcf
vcftools --vcf DP3g95p5maf001.prim.vcf --remove-indels --recode --recode-INFO-all --out SNP.DP3g95p5maf001

After filtering, kept 58 out of 58 Individuals
Outputting VCF file...
After filtering, kept 68799 out of a possible 72111 Sites
```

## Step8: HWE filter
Setting -h 0.001

```shell
./filter_hwe_by_pop.pl -v SNP.DP3g95p5maf001.recode.vcf -p popmap -o SNP.DP3g95p5maf001.HWE -h 0.001
Processing population: EOB (18 inds)
Processing population: PBF (15 inds)
Processing population: WOB (15 inds)
Processing population: WOF (14 inds)
Outputting results of HWE test for filtered loci to 'filtered.hwe'
Kept 66843 of a possible 68799 loci (filtered 1956 loci)
```
With minDP = 5, maf = 0.001 and h = 0.001 : 68799 loci kept with 58 indiv

## Step2: Minimum mean depth Testing at 2 values
Minimum mean depth = 10

```shell
vcftools --vcf raw.g5mac3.recode.vcf --minDP 10 --recode --recode-INFO-all --out raw.g5mac3dp10

After filtering, kept 62 out of 62 Individuals
Outputting VCF file...
After filtering, kept 218805 out of a possible 218805 Sites
```
## Step3: Filter missing indiv post minDP = 10

```shell
./filter_missing_ind.sh raw.g5mac3dp10.recode.vcf raw.g5mac3dplm

After filtering, kept 62 out of 62 Individuals
Outputting Individual Missingness
After filtering, kept 218805 out of a possible 218805 Sites


                                          Histogram of % missing data per individual

       12 +---------------------------------------------------------------------------------------------------------+
          |     ****  +           +          +           +           +           +          +           +           |
          |     ****                                          'totalmissing' using (bin($1,binwidth)):(1.0) ******* |
          |     ****                                                                                                |
       10 |-+   ****                                                                                              +-|
          |     ****                                                                                                |
          |     ******                                                                                              |
          |     **** *                                                                                              |
        8 |-+   **** *                                                                                            +-|
          |     **** *                                                                                              |
          |     **** ****                                                                                           |
        6 |-+   **** ** *                                                                                         +-|
          |     **** ** *                                                                                           |
          |     **** ** *                                                                                           |
          |     **** ** *                                                                                           |
        4 |-+   **** ** *                                                                                         +-|
          |     **** ** *                                                                                           |
          |     **** ** ****                                                                                        |
          |     **** ** *  *                                                                                        |
        2 |-+  ***** ** *  *                                                                                      +-|
          |    ***** ** *  *                                                                                        |
          |   ****** ** *  *****************************************************************************************|
          |   ****** ** *  * * *  +*         +     *     +       *   *           + *        +       *   +     *    *|
        0 +---------------------------------------------------------------------------------------------------------+
         0.1         0.2         0.3        0.4         0.5         0.6         0.7        0.8         0.9          1
                                                       % of missing data

The 85% cutoff would be 0.268705
Would you like to set a different cutoff, yes or no
no
After filtering, kept 54 out of 62 Individuals
Outputting VCF file...
After filtering, kept 218805 out of a possible 218805 Sites
```

Choosing 85% cutof

```shell
mawk '$5 > 0.268' raw.g5mac3dplm.imiss | cut -f1 | less

INDV
EOB_178_ddr
EOB_184_ddr
EOB_492_ddr
PBF_159_ddr
PBF_168_ddr
WOB_38_ddr
WOB_45_ddr
WOB_46_ddr
WOB_61_ddr
```
## Step4: Restrict the data to variants called in a high percentage of individuals and filter by mean depth of genotypes
This applied a genotype call rate (95%) across all individuals. Setting maf = 0.001

```shell
vcftools --vcf raw.g5mac3dplm.recode.vcf --max-missing 0.95 --maf 0.001 --recode --recode-INFO-all --out DP3g95maf001 --min-meanDP 20
After filtering, kept 54 out of 54 Individuals
Outputting VCF file...
After filtering, kept 93250 out of a possible 218805 Sites
```
## Step5: Filtering by population specific call rate when multiple localities are present

```shell
cut -f1 raw.g5mac3dplm.imiss|awk  -F "_" 'NR>1{print $1"_"$2"_"$3,$1}' > popmap
cat popmap
mawk '$2 == "EOB"' popmap > 1.keep && mawk '$2 == "PBF"' popmap > 2.keep && mawk '$2 == "WOB"' popmap > 3.keep && mawk '$2 == "WOF"' popmap > 4.keep
vcftools --vcf DP3g95maf001.recode.vcf --keep 1.keep --missing-site --out 1
vcftools --vcf DP3g95maf001.recode.vcf --keep 2.keep --missing-site --out 2
vcftools --vcf DP3g95maf001.recode.vcf --keep 3.keep --missing-site --out 3
vcftools --vcf DP3g95maf001.recode.vcf --keep 4.keep --missing-site --out 4
cat 1.lmiss 2.lmiss 3.lmiss 4.lmiss | mawk '!/CHR/' | mawk '$6 > 0.1' | cut -f1,2 >> badloci
vcftools --vcf DP3g95maf001.recode.vcf --exclude-positions badloci --recode --recode-INFO-all --out DP3g95p5maf001

After filtering, kept 54 out of 54 Individuals
Outputting VCF file...
After filtering, kept 90731 out of a possible 93250 Sites
```
## Step6: Used dDocent_filters script

```shell
./dDocent_filters DP3g95p5maf001.recode.vcf dDocent_filters_out

Number of sites filtered based on allele balance at heterozygous loci, locus quality, and mapping quality / Depth
 12037 of 90731

Are reads expected to overlap?  In other words, is fragment size less than 2X the read length?  Enter yes or no.
no
Number of additional sites filtered based on overlapping forward and reverse reads
 10193 of 78694

Is this from a mixture of SE and PE libraries? Enter yes or no.
no
Number of additional sites filtered based on properly paired status
 1472 of 68501
Number of sites filtered based on high depth and lower than 2*DEPTH quality score
 5719 of 67029



                                               Histogram of mean depth per site

     1200 +---------------------------------------------------------------------------------------------------------+
          |+    +     +    +    +     +    +    +     +    +    +     +    +    +     +    +    +     +    +    +   |
          |                                               'meandepthpersite' using (bin($1,binwidth)):(1.0) ******* |
          |                                                                                                         |
     1000 |-+                                   *                                                                 +-|
          |                                     ***  ***                                                            |
          |                                    **** ****                                                            |
          |                                  ***********                                                            |
      800 |-+                            **  **************                                                       +-|
          |                              ** ***************                                                         |
          |                              ** ***************                                                         |
      600 |-+                            ** ****************                                                      +-|
          |                            ***********************                                                      |
          |                            ***********************                                                      |
          |                          *****************************                                                  |
      400 |-+                       *********************************  **                                         +-|
          |                       ***************************************                                           |
          |                       ***************************************  **                                       |
          |                       ************************************************                                  |
      200 |-+                  ******************************************************                             +-|
          |                  ************************************************************    *                      |
          |                * ***************************************************************** *   *** *            |
          |+    +     +  *******************************************************************************************|
        0 +---------------------------------------------------------------------------------------------------------+
           12   24    36   48   60    72   84   96   108  120  132   144  156  168   180  192  204   216  228  240
                                                          Mean Depth
If distrubtion looks normal, a 1.645 sigma cutoff (~90% of the data) would be 13160.9314
The 95% cutoff would be 226
Would you like to use a different maximum mean depth cutoff than 226, yes or no
no
Number of sites filtered based on maximum mean depth
 4013 of 67029
Number of sites filtered based on within locus depth mismatch
 14 of 63016

Total number of sites filtered
 27729 of 90731

Remaining sites
 63002

Filtered VCF file is called Output_prefix.FIL.recode.vcf
```
## Step7: Convert our variant calls to SNPs

```shell
vcfallelicprimitives dDocent_filters_out.FIL.recode.vcf --keep-info --keep-geno > DP3g95p5maf001.prim.vcf
vcftools --vcf DP3g95p5maf001.prim.vcf --remove-indels --recode --recode-INFO-all --out SNP.DP3g95p5maf001

After filtering, kept 54 out of 54 Individuals
Outputting VCF file...
After filtering, kept 68115 out of a possible 71423 Sites
```
## Step8: HWE filter
Setting -h 0.001

```shell
./filter_hwe_by_pop.pl -v SNP.DP3g95p5maf001.recode.vcf -p popmap -o SNP.DP3g95p5maf001.HWE -h 0.001
Processing population: EOB (18 inds)
Processing population: PBF (15 inds)
Processing population: WOB (15 inds)
Processing population: WOF (14 inds)
Outputting results of HWE test for filtered loci to 'filtered.hwe'
Kept 66406 of a possible 68115 loci (filtered 1709 loci)
```

With minDP = 10, maf = 0.001 and h = 0.001 : 66406 loci kept with 54 indiv
