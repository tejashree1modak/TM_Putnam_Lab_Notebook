---
layout: post
title: SNP filtering full data set
tags: [ ddRAD, epiRAD, Moorea, dDocent, SNP, filter ]
---

## Step2: Minimum mean depth Testing at 2 values
With the full dataset testing 2 values of minDP 

## Minimum mean depth = 5

```shell
vcftools --vcf raw.g5mac3.recode.vcf --minDP 5 --recode --recode-INFO-all --out raw.g5mac3dp5

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
mawk '$5 > 0.3' out.imiss | cut -f1 | less
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
```
Choosing 25% cutoff

```shell
vcftools --vcf raw.g5mac3dp5.recode.vcf --remove lowDP.indv --recode --recode-INFO-all --out raw.g5mac3dplm
After filtering, kept 113 out of 124 Individuals
Outputting VCF file...
After filtering, kept 288777 out of a possible 288777 Sites
```
### Step4: Restrict the data to variants called in a high percentage of individuals and filter by mean depth of genotypes

This applied a genotype call rate (95%) across all individuals.
**Setting maf = 0.001**

```shell
vcftools --vcf raw.g5mac3dplm.recode.vcf --max-missing 0.95 --maf 0.001 --recode --recode-INFO-all --out DP3g95maf001 --min-meanDP 20
After filtering, kept 113 out of 113 Individuals
Outputting VCF file...
After filtering, kept 126456 out of a possible 288777 Sites
```

### Step5: Filtering by population specific call rate when multiple localities are present

```shell
cut -f1 out.imiss|awk  -F "_" 'NR>1{print $1"_"$2"_"$3,$1}' > popmap
cat popmap
mawk '$2 == "EOB"' popmap > 1.keep && mawk '$2 == "PBF"' popmap > 2.keep && mawk '$2 == "WOB"' popmap > 3.keep && mawk '$2 == "WOF"' popmap > 4.keep
vcftools --vcf DP3g95maf001.recode.vcf --keep 1.keep --missing-site --out 1
vcftools --vcf DP3g95maf001.recode.vcf --keep 2.keep --missing-site --out 2
vcftools --vcf DP3g95maf001.recode.vcf --keep 3.keep --missing-site --out 3
vcftools --vcf DP3g95maf001.recode.vcf --keep 4.keep --missing-site --out 4
cat 1.lmiss 2.lmiss 3.lmiss 4.lmiss | mawk '!/CHR/' | mawk '$6 > 0.1' | cut -f1,2 >> badloci
vcftools --vcf DP3g95maf001.recode.vcf --exclude-positions badloci --recode --recode-INFO-all --out DP3g95p5maf001
After filtering, kept 113 out of 113 Individuals
Outputting VCF file...
After filtering, kept 121233 out of a possible 126456 Sites
```

### Step6: Used dDocent_filters script

```shell
./dDocent_filters DP3g95p5maf001.recode.vcf dDocent_filters_out

Number of sites filtered based on allele balance at heterozygous loci, locus quality, and mapping quality / Depth
 18603 of 121233

Are reads expected to overlap?  In other words, is fragment size less than 2X the read length?  Enter yes or no.
no
Number of additional sites filtered based on overlapping forward and reverse reads
12091 of 102630

Is this from a mixture of SE and PE libraries? Enter yes or no.
no
Number of additional sites filtered based on properly paired status
1815 of 90539

Number of sites filtered based on high depth and lower than 2*DEPTH quality score
 7746 of 88724

                                               Histogram of mean depth per site

     1200 +---------------------------------------------------------------------------------------------------------+
          |     +    +    +    +     +    +    +    +     +    +    +     +    +    +    +     +    +    +    +     |
          |                                               'meandepthpersite' using (bin($1,binwidth)):(1.0) ******* |
          |                                                 * *                                                     |
     1000 |-+                                     *** ** ** * *                                                   +-|
          |                                     * *** **********                                                    |
          |                                     * **************                                                    |
          |                            *     **********************                                                 |
      800 |-+                          *    ************************                                              +-|
          |                            *  * **************************                                              |
          |                          *** ****************************** **                                          |
      600 |-+                        *** *********************************                                        +-|
          |                          **************************************                                         |
          |                         **************************************** ***                                    |
          |                       ********************************************** **                                 |
      400 |-+                     *************************************************                               +-|
          |                     ***************************************************                                 |
          |                    **********************************************************                           |
          |                 ***************************************************************                         |
      200 |-+             ******************************************************************                      +-|
          |           *************************************************************************  *                  |
          |         ********************************************************************************   ***** **     |
          |     +  *************************************************************************************************|
        0 +---------------------------------------------------------------------------------------------------------+
          11    22   33   44   55    66   77   88   99   110  121  132   143  154  165  176   187  198  209  220   231
                                                          Mean Depth

If distrubtion looks normal, a 1.645 sigma cutoff (~90% of the data) would be 25233.65575
The 95% cutoff would be 211
Would you like to use a different maximum mean depth cutoff than 211, yes or no
no
Number of sites filtered based on maximum mean depth
 5198 of 88724

Number of sites filtered based on within locus depth mismatch
 26 of 83526

Total number of sites filtered
 37733 of 121233

Remaining sites
 83500

```

### Step7: Convert our variant calls to SNPs

```shell

vcfallelicprimitives dDocent_filters_out.FIL.recode.vcf --keep-info --keep-geno > DP3g95p5maf001.prim.vcf
vcftools --vcf DP3g95p5maf001.prim.vcf --remove-indels --recode --recode-INFO-all --out SNP.DP3g95p5maf001

After filtering, kept 113 out of 113 Individuals
Outputting VCF file...
After filtering, kept 90992 out of a possible 95915 Sites
```
### Step8: HWE filter
**Setting -h 0.001**
```shell
 .././filter_hwe_by_pop.pl -v SNP.DP3g95p5maf001.recode.vcf -p popmap -o SNP.DP3g95p5maf001.HWE -h 0.001
Processing population: EOB (36 inds)
Processing population: PBF (30 inds)
Processing population: WOB (30 inds)
Processing population: WOF (28 inds)
Outputting results of HWE test for filtered loci to 'filtered.hwe'
Kept 87172 of a possible 90992 loci (filtered 3820 loci)
```
## With minDP = 5, maf = 0.001 and h = 0.001 : 87172 loci kept with 113 indiv

## Step2: Minimum mean depth Testing at 2 values

## Minimum mean depth = 10

```shell
vcftools --vcf raw.g5mac3.recode.vcf --minDP 10 --recode --recode-INFO-all --out raw.g5mac3dp10

After filtering, kept 124 out of 124 Individuals
Outputting VCF file...
After filtering, kept 288777 out of a possible 288777 Sites`
```

### Step3: Filter missing indiv post minDP=10

```shell
vcftools --vcf raw.g5mac3dp10.recode.vcf --missing-indv
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

### Step4: Restrict the data to variants called in a high percentage of individuals and filter by mean depth of genotypes

This applied a genotype call rate (95%) across all individuals. **Setting maf = 0.001**

```shell
vcftools --vcf raw.g5mac3dplm.recode.vcf --max-missing 0.95 --maf 0.001 --recode --recode-INFO-all --out DP3g95maf001 --min-meanDP 20
fter filtering, kept 112 out of 112 Individuals
Outputting VCF file...
After filtering, kept 117809 out of a possible 288777 Sites
```
### Step5: Filtering by population specific call rate when multiple localities are present

```shell
cut -f1 out.imiss|awk  -F "_" 'NR>1{print $1"_"$2"_"$3,$1}' > popmap
cat popmap
mawk '$2 == "EOB"' popmap > 1.keep && mawk '$2 == "PBF"' popmap > 2.keep && mawk '$2 == "WOB"' popmap > 3.keep && mawk '$2 == "WOF"' popmap > 4.keep
vcftools --vcf DP3g95maf001.recode.vcf --keep 1.keep --missing-site --out 1
vcftools --vcf DP3g95maf001.recode.vcf --keep 2.keep --missing-site --out 2
vcftools --vcf DP3g95maf001.recode.vcf --keep 3.keep --missing-site --out 3
vcftools --vcf DP3g95maf001.recode.vcf --keep 4.keep --missing-site --out 4
cat 1.lmiss 2.lmiss 3.lmiss 4.lmiss | mawk '!/CHR/' | mawk '$6 > 0.1' | cut -f1,2 >> badloci
vcftools --vcf DP3g95maf001.recode.vcf --exclude-positions badloci --recode --recode-INFO-all --out DP3g95p5maf001
After filtering, kept 112 out of 112 Individuals
Outputting VCF file...
After filtering, kept 112668 out of a possible 117809 Sites
```
### Step6: dDocent_filters script

```shell
.././dDocent_filters DP3g95p5maf001.recode.vcf dDocent_filters_out
Number of sites filtered based on allele balance at heterozygous loci, locus quality, and mapping quality / Depth
 17462 of 112668

Are reads expected to overlap?  In other words, is fragment size less than 2X the read length?  Enter yes or no.
no
Number of additional sites filtered based on overlapping forward and reverse reads
 11477 of 95206

Is this from a mixture of SE and PE libraries? Enter yes or no.
no
Number of additional sites filtered based on properly paired status
 1725 of 83729

Number of sites filtered based on high depth and lower than 2*DEPTH quality score
 7395 of 82004


                                               Histogram of mean depth per site

     1200 +---------------------------------------------------------------------------------------------------------+
          |     +    +    +    +    +    +    +    +    +    +    +     +    +    +    +    +    +    +    +    +   |
          |                                               'meandepthpersite' using (bin($1,binwidth)):(1.0) ******* |
          |                                            **   **                                                      |
     1000 |-+                                          **  ***                                                    +-|
          |                                      * ** **** ****                                                     |
          |                                    * ********* ****                                                     |
          |                                    *****************                                                    |
      800 |-+                               ***********************                                               +-|
          |                                *************************                                                |
          |                               ***************************  *                                            |
      600 |-+                         * ********************************                                          +-|
          |                          ** **********************************                                          |
          |                          *************************************                                          |
          |                          ********************************************                                   |
      400 |-+                      **********************************************                                 +-|
          |                        ***********************************************                                  |
          |                    ** *****************************************************                             |
          |                    ** ********************************************************                          |
      200 |-+                 ************************************************************                        +-|
          |                   **************************************************************   *                    |
          |                 **********************************************************************  ****** **       |
          |     +    +  ********************************************************************************************|
        0 +---------------------------------------------------------------------------------------------------------+
          11    22   33   44   55   66   77   88   99  110  121  132   143  154  165  176  187  198  209  220  231
                                                          Mean Depth
If distrubtion looks normal, a 1.645 sigma cutoff (~90% of the data) would be 25723.2027
The 95% cutoff would be 218
Would you like to use a different maximum mean depth cutoff than 218, yes or no
no
Number of sites filtered based on maximum mean depth
 4794 of 82004

Number of sites filtered based on within locus depth mismatch
 12 of 77210

Total number of sites filtered
 35470 of 112668

Remaining sites
 77198
```
### Step7: Convert our variant calls to SNPs

```shell
vcfallelicprimitives dDocent_filters_out.FIL.recode.vcf --keep-info --keep-geno > DP3g95p5maf001.prim.vcf
vcftools --vcf DP3g95p5maf001.prim.vcf --remove-indels --recode --recode-INFO-all --out SNP.DP3g95p5maf001
After filtering, kept 112 out of 112 Individuals
Outputting VCF file...
After filtering, kept 84068 out of a possible 88583 Sites
```
### Step8: HWE filter
**Setting -h 0.001**

```shell
 .././filter_hwe_by_pop.pl -v SNP.DP3g95p5maf001.recode.vcf -p popmap -o SNP.DP3g95p5maf001.HWE -h 0.001
Processing population: EOB (36 inds)
Processing population: PBF (30 inds)
Processing population: WOB (30 inds)
Processing population: WOF (28 inds)
Outputting results of HWE test for filtered loci to 'filtered.hwe'
Kept 80692 of a possible 84068 loci (filtered 3376 loci)
```

## With minDP = 10, maf = 0.001 and h = 0.001 : 80692 loci kept with 112 indiv



















