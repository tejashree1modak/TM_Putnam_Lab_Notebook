---
layout: post
title: SNP filtering of clusters identified from full ddRAD data set
tags: [ ddRAD, epiRAD, Moorea, dDocent, SNP, filter ]
---

## Cluster 1: 

- EOB_175_ddr,EOB_185_ddr,EOB_189_ddr,EOB_190_ddr,EOB_192_ddr
- PBF_161_ddr,PBF_169_ddr,PBF_171_ddr,PBF_172_ddr
- WOB_35_ddr
- WOF_224_ddr,WOF_225_ddr,WOF_232_ddr,WOF_234_ddr,WOF_237_ddr,WOF_238_ddr,WOF_239_ddr,WOF_240_ddr,WOF_241_ddr,WOF_243_ddr,WOF_244_ddr,WOF_245_ddr,EOB_175_epi,EOB_185_epi,EOB_189_epi,EOB_190_epi,EOB_192_epi,PBF_161_epi,PBF_169_epi,PBF_171_epi,PBF_172_epi,WOB_35_epi,WOF_224_epi,WOF_225_epi,WOF_232_epi,WOF_234_epi,WOF_237_epi,WOF_238_epi,WOF_239_epi,WOF_240_epi,WOF_241_epi,WOF_243_epi,WOF_244_epi,WOF_245_epi

## Cluster 2: 
- EOB_177_ddr,EOB_178_ddr,EOB_182_ddr,EOB_183_ddr,EOB_184_ddr,EOB_186_ddr,EOB_188_ddr,EOB_191_ddr
- WOB_41_ddr,WOB_42_ddr,WOB_45_ddr,WOB_47_ddr,WOB_48_ddr,WOB_49_ddr,WOB_50_ddr,WOB_59_ddr,WOB_60_ddr,WOB_62_ddr,WOB_65_ddr,EOB_177_epi,EOB_178_epi,EOB_182_epi,EOB_183_epi,EOB_184_epi,EOB_186_epi,EOB_188_epi,EOB_191_epi,WOB_41_epi,WOB_42_epi,WOB_45_epi,WOB_47_epi,WOB_48_epi,WOB_49_epi,WOB_50_epi,WOB_59_epi,WOB_60_epi,WOB_62_epi,WOB_65_epi

## Step1: 50% of individuals, a minimum quality score of 30, and a minor allele count of 3

```
vcftools --vcf TotalRawSNPs.vcf --max-missing 0.5 --mac 3 --minQ 30 --recode --recode-INFO-all --out raw.g5mac3

```

## Step2: Minimum mean depth: minDP 5

```shell
vcftools --vcf raw.g5mac3.recode.vcf --minDP 5 --recode --recode-INFO-all --out raw.g5mac3dp5

```
## Step3: Filter missing indiv post minDP =5

```shell
./filter_missing_ind.sh raw.g5mac3dp5.recode.vcf raw.g5mac3dplm

```
### Cluster1

```
                                          Histogram of % missing data per individual

        9 +---------------------------------------------------------------------------------------------------------+
          |            +             +            +            +            *             +            *            |
          |                                                   'totalmissing'*using (bin($1,binwidth)):(*.0) ******* |
        8 |-+                                                               *                          *          +-|
          |                                                                 *                          *            |
        7 |-+                                                               *                          *          +-|
          |                                                                 *                          *            |
          |                                                                 *                          *            |
        6 |-+                                                               *                          *          +-|
          |                                                                 *                          *            |
        5 |-+          ****************************                         *                          *          +-|
          |            *                          *                         *                          *            |
          |            *                          *                         *                          *            |
        4 |-+          *                          *                         *                          *          +-|
          |            *                          *                         *                          *            |
        3 |*************                          ***************************                          *          +-|
          |            *                          *                         *                          *            |
          |            *                          *                         *                          *            |
        2 |-+          *                          *                         *                          *************|
          |            *                          *                         *                          *            |
        1 |-+          *                          *                         *                          *          +-|
          |            *                          *                         *                          *            |
          |            *             +            *            +            *             +            *            |
        0 +---------------------------------------------------------------------------------------------------------+
        0.125         0.13         0.135         0.14        0.145         0.15         0.155         0.16        0.165
                                                       % of missing data

The 85% cutoff would be 0.157016
Would you like to set a different cutoff, yes or no
yes
Please enter new cutoff
0.165
All individuals with more than 16.5% missing data will be removed.

After filtering, kept 21 out of 22 Individuals
Outputting VCF file...
After filtering, kept 123892 out of a possible 123892 Sites

mawk '$5 > 0.165' raw.g5mac3dplm.imiss | cut -f1 | less

INDV
PBF_169_ddr

```

### Cluster2

```
                                          Histogram of % missing data per individual

        5 +---------------------------------------------------------------------------------------------------------+
          |     *     *           +          +           +           +           +          +           +           |
          |     *     *                                       'totalmissing' using (bin($1,binwidth)):(1.0) ******* |
          |     *     *                                                                                             |
          |     *     *                                                                                             |
        4 |-+   *     *     ***************                                                                       +-|
          |     *     *     *     *       *                                                                         |
          |     *     *     *     *       *                                                                         |
          |     *     *     *     *       *                                                                         |
        3 |-+   *     *******     *       *                                                                       +-|
          |     *     *     *     *       *                                                                         |
          |     *     *     *     *       *                                                                         |
          |     *     *     *     *       *                                                                         |
          |     *     *     *     *       *                                                                         |
        2 |-+   *     *     *     *       *                                                                       +-|
          |     *     *     *     *       *                                                                         |
          |     *     *     *     *       *                                                                         |
          |     *     *     *     *       *                                                                         |
        1 |-+   *     *     *     *       ******************************************************************      +-|
          |     *     *     *     *       *        *                             *                         *        |
          |     *     *     *     *       *        *                             *                         *        |
          |     *     *     *     *       *        *                             *                         *        |
          |     *     *     *     *       *  +     *     +           +           *          +           +  *        |
        0 +---------------------------------------------------------------------------------------------------------+
         0.1         0.12        0.14       0.16        0.18        0.2         0.22       0.24        0.26        0.28
                                                       % of missing data

The 85% cutoff would be 0.160448
Would you like to set a different cutoff, yes or no
yes
Please enter new cutoff
0.26
All individuals with more than 26.0% missing data will be removed.

After filtering, kept 18 out of 19 Individuals
Outputting VCF file...
After filtering, kept 106595 out of a possible 106595 Sites

```

## Step4: Restrict the data to variants called in a high percentage of individuals and filter by mean depth of genotypes
This applied a genotype call rate (95%) across all individuals. Setting maf = 0.001

```shell
vcftools --vcf raw.g5mac3dplm.recode.vcf --max-missing 0.95 --maf 0.001 --recode --recode-INFO-all --out DP3g95maf001 --min-meanDP 20

```
### Cluster1

```
After filtering, kept 21 out of 21 Individuals
Outputting VCF file...
After filtering, kept 71466 out of a possible 123892 Sites

```

### Cluster2

```
After filtering, kept 18 out of 18 Individuals
Outputting VCF file...
After filtering, kept 53836 out of a possible 106595 Sites

```

## Step5: Filtering by population specific call rate when multiple localities are present

### Cluster1

```shell
mawk '$2 == "EOB"' popmap > 1.keep && mawk '$2 == "PBF"' popmap > 2.keep && mawk '$2 == "WOF"' popmap > 3.keep
vcftools --vcf DP3g95maf001.recode.vcf --keep 1.keep --missing-site --out 1
vcftools --vcf DP3g95maf001.recode.vcf --keep 2.keep --missing-site --out 2
vcftools --vcf DP3g95maf001.recode.vcf --keep 3.keep --missing-site --out 3
cat 1.lmiss 2.lmiss 3.lmiss | mawk '!/CHR/' | mawk '$6 > 0.1' | cut -f1,2 >> badloci
vcftools --vcf DP3g95maf001.recode.vcf --exclude-positions badloci --recode --recode-INFO-all --out DP3g95p5maf001

After filtering, kept 21 out of 21 Individuals
Outputting VCF file...
After filtering, kept 67166 out of a possible 71466 Sites

```

### Cluster2

```
mawk '$2 == "EOB"' popmap > 1.keep && mawk '$2 == "WOB"' popmap > 2.keep
vcftools --vcf DP3g95maf001.recode.vcf --keep 1.keep --missing-site --out 1
vcftools --vcf DP3g95maf001.recode.vcf --keep 2.keep --missing-site --out 2
cat 1.lmiss 2.lmiss | mawk '!/CHR/' | mawk '$6 > 0.1' | cut -f1,2 >> badloci

After filtering, kept 18 out of 18 Individuals
Outputting VCF file...
After filtering, kept 53836 out of a possible 53836 Sites

```
## Step6: Used dDocent_filters script

### Cluster1

```shell
./dDocent_filters DP3g95p5maf001.recode.vcf dDocent_filters_out

Number of sites filtered based on allele balance at heterozygous loci, locus quality, and mapping quality / Depth
 9094 of 67166

Are reads expected to overlap?  In other words, is fragment size less than 2X the read length?  Enter yes or no.
no
Number of additional sites filtered based on overlapping forward and reverse reads
 13577 of 58072

Is this from a mixture of SE and PE libraries? Enter yes or no.
no
Number of additional sites filtered based on properly paired status
 1701 of 44495

Number of sites filtered based on high depth and lower than 2*DEPTH quality score
 3491 of 42794

                                               Histogram of mean depth per site

      700 +---------------------------------------------------------------------------------------------------------+
          | +    +     +    +    +     +    +    +     +    +     +    +    +     +    +    +     +    +    +     + |
          |                            **                 'meandepthpersite' using (bin($1,binwidth)):(1.0) ******* |
      600 |-+                          **                                                                         +-|
          |                            ****                                                                         |
          |                            ****                                                                         |
          |                            ******                                                                       |
      500 |-+                          ********                                                                   +-|
          |                          ***********                                                                    |
          |                        *************                                                                    |
      400 |-+                      **************                                                                 +-|
          |                      * ****************                                                                 |
          |                      ******************                                                                 |
      300 |-+                  ********************* *                                                            +-|
          |                    *********************** *                                                            |
          |                    ************************* **  *                                                      |
      200 |-+               *******************************  **                                                   +-|
          |               * ************************************                                                    |
          |              *********************************************                                              |
          |            *************************************************                                            |
      100 |-+        ****************************************************     *                                   +-|
          |         ***************************************************************** * ***** **                    |
          | +   *+**************************************************************************************************|
        0 +---------------------------------------------------------------------------------------------------------+
            15   30    45   60   75    90  105  120   135  150   165  180  195   210  225  240   255  270  285   300
                                                          Mean Depth

If distrubtion looks normal, a 1.645 sigma cutoff (~90% of the data) would be 6383.247
The 95% cutoff would be 279
Would you like to use a different maximum mean depth cutoff than 279, yes or no
no
Number of sites filtered based on maximum mean depth
 2313 of 42794

Number of sites filtered based on within locus depth mismatch
 60 of 40481

Total number of sites filtered
 26745 of 67166

Remaining sites
 40421

Filtered VCF file is called Output_prefix.FIL.recode.vcf

Filter stats stored in dDocent_filters_out.filterstats

```
### Cluster2

```
 ./dDocent_filters DP3g95p5maf001.recode.vcf dDocent_filters_out

Number of sites filtered based on allele balance at heterozygous loci, locus quality, and mapping quality / Depth
 6215 of 53836

Are reads expected to overlap?  In other words, is fragment size less than 2X the read length?  Enter yes or no.
no
Number of additional sites filtered based on overlapping forward and reverse reads
 11214 of 47621

Is this from a mixture of SE and PE libraries? Enter yes or no.
no
Number of additional sites filtered based on properly paired status
 1512 of 36407

Number of sites filtered based on high depth and lower than 2*DEPTH quality score
 2552 of 34895

                                               Histogram of mean depth per site

      500 +---------------------------------------------------------------------------------------------------------+
          | +    +     +    +    +     +    +  **+     +    +     +    +    +     +    +    +     +    +    +     + |
      450 |-+                              **  **         'meandepthpersite' using (bin($1,binwidth)):(1.0) *******-|
          |                                ******                                                                   |
          |                             *  ******                                                                   |
      400 |-+                           *********                                                                 +-|
          |                           ************                                                                  |
      350 |-+                         **************                                                              +-|
          |                           **************                                                                |
      300 |-+                      * ****************                                                             +-|
          |                        ****************** **                                                            |
      250 |-+                    ******************** **                                                          +-|
          |                      ******************** **** *                                                        |
          |                    * ************************* *                                                        |
      200 |-+                  *************************** * **                                                   +-|
          |                  ************************************                                                   |
      150 |-+                ************************************  *                                              +-|
          |                 ************************************** **                                               |
      100 |-+             **********************************************                                          +-|
          |               **********************************************       **                                   |
          |               **************************************************   **   *   * *    *                    |
       50 |-+          ************************************************************** *************   **          +-|
          | +    +  **********************************************************************************************+*|
        0 +---------------------------------------------------------------------------------------------------------+
            15   30    45   60   75    90  105  120   135  150   165  180  195   210  225  240   255  270  285   300
                                                          Mean Depth

If distrubtion looks normal, a 1.645 sigma cutoff (~90% of the data) would be 5441.5459
The 95% cutoff would be 279
Would you like to use a different maximum mean depth cutoff than 279, yes or no
no
Number of sites filtered based on maximum mean depth
 1874 of 34895

Number of sites filtered based on within locus depth mismatch
 34 of 33021

Total number of sites filtered
 20849 of 53836

Remaining sites
 32987

Filtered VCF file is called Output_prefix.FIL.recode.vcf

Filter stats stored in dDocent_filters_out.filterstats

```
## Step7: Convert our variant calls to SNPs

```shell

vcfallelicprimitives dDocent_filters_out.FIL.recode.vcf --keep-info --keep-geno > DP3g95p5maf001.prim.vcf
vcftools --vcf DP3g95p5maf001.prim.vcf --remove-indels --recode --recode-INFO-all --out SNP.DP3g95p5maf001

```
### Cluster1

```
After filtering, kept 21 out of 21 Individuals
Outputting VCF file...
After filtering, kept 43341 out of a possible 46010 Sites
```
### Cluster2

```
After filtering, kept 18 out of 18 Individuals
Outputting VCF file...
After filtering, kept 35575 out of a possible 37810 Sites
```
## Step8: HWE filter
Setting -h 0.001

```shell
./filter_hwe_by_pop.pl -v SNP.DP3g95p5maf001.recode.vcf -p popmap -o SNP.DP3g95p5maf001.HWE -h 0.001
```
### Cluster1

```
Processing population: EOB (5 inds)
Processing population: PBF (4 inds)
Processing population: WOB (1 inds)
Processing population: WOF (12 inds)
Outputting results of HWE test for filtered loci to 'filtered.hwe'
Kept 43341 of a possible 43341 loci (filtered 0 loci)

```

### Cluster2

```
Processing population: EOB (8 inds)
Processing population: WOB (11 inds)
Outputting results of HWE test for filtered loci to 'filtered.hwe'
Kept 35575 of a possible 35575 loci (filtered 0 loci)
```

## rad_haplotyper

```shell
rad_haplotyper.pl -v SNP.DP3g95p5maf001.HWE.recode.vcf -x 20 -mp 1 -u 20 -ml 4 -n -r reference.fasta
```

### Cluster1

The script found 1592 loci to remove.
```
Removed 70 loci (1737 SNPs) with more than 20 SNPs at a locus
Filtered 165 loci below missing data cutoff
Filtered 1189 possible paralogs
Filtered 238 loci with low coverage or genotyping errors
Filtered 0 loci with an excess of haplotypes
```

### Cluster2

The script found another 1148 loci to remove.

```
Removed 65 loci (1553 SNPs) with more than 20 SNPs at a locus

Filtered 168 loci below missing data cutoff
Filtered 825 possible paralogs
Filtered 155 loci with low coverage or genotyping errors
Filtered 0 loci with an excess of haplotypes
```


We can use stats.out to create a list of loci to filter

```shell
grep FILTERED stats.out | mawk '!/Complex/' | cut -f1 > loci.to.remove
```

## Remove bad loci identified by rad_haplotyper
Now that we have the list we can parse through the VCF file and remove the bad RAD loci. Use script from dDocent to do this: remove.bad.hap.loci.sh

```shell
./remove.bad.hap.loci.sh loci.to.remove SNP.DP3g95p5maf001.HWE.recode.vcf
mawk '!/#/' SNP.DP3g95p5maf001.HWE.filtered.vcf | wc -l
```

### Total loci in Cluster1 post SNP filtering: 29332
### Total individuals in Cluster1 post SNP filtering: 21

### Total loci in Cluster2 post SNP filtering: 24927
### Total individuals in Cluster2 post SNP filtering: 19


