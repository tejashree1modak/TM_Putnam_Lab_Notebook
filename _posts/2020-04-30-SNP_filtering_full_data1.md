---
layout: post
title: SNP filtering full data set
tags: [ ddRAD, epiRAD, Moorea, dDocent, SNP, filter ]
---

# SNP filtering 
This filtering was performed on full data set per the [ SNP filtering tutorial ] (http://www.ddocent.com/filtering/) in dDocent.
The filtration is housed in /home/tejashree/Moorea/ddocent/final/snp_filtering/.

## Step1: 50% of individuals, a minimum quality score of 30, and a minor allele count of 3

Filter genotypes called below 50% (across all individuals) the --mac 3 flag tells it to filter SNPs that have a minor allele count less than 3.
This is relative to genotypes, so it has to be called in at least 1 homozygote and 1 heterozygote or 3 heterozygotes.

```shell
vcftools --vcf TotalRawSNPs.vcf --max-missing 0.5 --mac 3 --minQ 30 --recode --recode-INFO-all --out raw.g5mac3

After filtering, kept 124 out of 124 Individuals
Outputting VCF file...
After filtering, kept 288777 out of a possible 773896 Sites
```

## Step2: Minimum mean depth

This command will recode genotypes that have less than 3 reads.Sophisticated multisample variant callers like FreeBayes and GATK can confidently call genotypes with few reads because variants are assessed across all samples simultaneously. So, the genotype is based on three reads AND prior information from all reads from all individuals. 

```shell
vcftools --vcf raw.g5mac3.recode.vcf --minDP 3 --recode --recode-INFO-all --out raw.g5mac3dp3`

After filtering, kept 124 out of 124 Individuals
Outputting VCF file...
After filtering, kept 288777 out of a possible 288777 Sites`
```

## Step3: Filter missing indiv 

The next step is to get rid of individuals that did not sequence well.

```shell
vcftools --vcf raw.g5mac3dp3.recode.vcf --missing-indv
cat out.imiss
mawk '!/IN/' out.imiss | cut -f5 > totalmissing
gnuplot << \EOF 
set terminal dumb size 120, 30
set autoscale 
unset label
set title "Histogram of % missing data per individual"
set ylabel "Number of Occurrences"
set xlabel "% of missing data"
#set yr [0:100000]
binwidth=0.01
bin(x,width)=width*floor(x/width) + binwidth/2.0
plot 'totalmissing' using (bin($1,binwidth)):(1.0) smooth freq with boxes
pause -1
EOF

                                         Histogram of % missing data per individual

     25 +-----------------------------------------------------------------------------------------------------------+
        |     *** * +           +           +           +           +           +           +           +           |
        |     *** *                                           'totalmissing' using (bin($1,binwidth)):(1.0) ******* |
        |     *** *                                                                                                 |
        |     *** *                                                                                                 |
     20 |-+  **** *                                                                                               +-|
        |    **** *                                                                                                 |
        |    **** *                                                                                                 |
        |    **** *                                                                                                 |
     15 |-+  **** *                                                                                               +-|
        |    **** *                                                                                                 |
        |    **** *                                                                                                 |
        |    **** *                                                                                                 |
        |    **** *                                                                                                 |
     10 |-+  **** *                                                                                               +-|
        |    **** *                                                                                                 |
        |    **** ***                                                                                               |
        |    **** ***                                                                                               |
      5 |-+  **** ***                                                                                             +-|
        |    **** ***                                                                                               |
        | ******* *** *****                                                                                         |
        | * ***** *****   *                                                                                         |
        |** ***** *****   ******************************************************************************************|
      0 +-----------------------------------------------------------------------------------------------------------+
       0.1         0.2         0.3         0.4         0.5         0.6         0.7         0.8         0.9          1
                                                      % of missing data

```

Most of the individuals have less than 0.3 missing data. Created a list of individuals with more than 30% missing data.

```shell
mawk '$5 > 0.3' out.imiss | cut -f1 > lowDP.indv
vcftools --vcf raw.g5mac3dp3.recode.vcf --remove lowDP.indv --recode --recode-INFO-all --out raw.g5mac3dplm`

After filtering, kept 117 out of 124 Individuals
Outputting VCF file...
After filtering, kept 288777 out of a possible 288777 Sites
```

## Step4: Restrict the data to variants called in a high percentage of individuals and filter by mean depth of genotypes 

This applied a genotype call rate (95%) across all individuals. 

```shell
vcftools --vcf raw.g5mac3dplm.recode.vcf --max-missing 0.95 --maf 0.05 --recode --recode-INFO-all --out DP3g95maf05 --min-meanDP 20
After filtering, kept 117 out of 117 Individuals
Outputting VCF file...
After filtering, kept 51772 out of a possible 288777 Sites
```

## Step5: Filtering by population specific call rate when multiple localities are present

We  want to filter by a population specific call rate.First we need a file to define localities (populations). This is called popmap. Use VCFtools to estimate missing data for loci in each population. Combine the two files and make a list of loci about the threshold of 10% missing data to remove. 

```shell
cut -f1 out.imiss|awk  -F "_" 'NR>1{print $1"_"$2"_"$3,$1}' > popmap
cat popmap
mawk '$2 == "EOB"' popmap > 1.keep && mawk '$2 == "PBF"' popmap > 2.keep && mawk '$2 == "WOB"' popmap > 3.keep && mawk '$2 == "WOF"' popmap > 4.keep                                         

vcftools --vcf DP3g95maf05.recode.vcf --keep 1.keep --missing-site --out 1
vcftools --vcf DP3g95maf05.recode.vcf --keep 2.keep --missing-site --out 2                                                                                                                     
vcftools --vcf DP3g95maf05.recode.vcf --keep 3.keep --missing-site --out 3
vcftools --vcf DP3g95maf05.recode.vcf --keep 4.keep --missing-site --out 4                                                                                                                     
cat 1.lmiss 2.lmiss 3.lmiss 4.lmiss | mawk '!/CHR/' | mawk '$6 > 0.1' | cut -f1,2 >> badloci
vcftools --vcf DP3g95maf05.recode.vcf --exclude-positions badloci --recode --recode-INFO-all --out DP3g95p5maf05

After filtering, kept 117 out of 117 Individuals
Outputting VCF file...
After filtering, kept 49453 out of a possible 51772 Sites
```

## Step6: Used dDocent_filters script 

```shell
./dDocent_filters DP3g95p5maf05.recode.vcf dDocent_filters_out

Number of sites filtered based on allele balance at heterozygous loci, locus quality, and mapping quality / Depth
 4058 of 49453

Are reads expected to overlap?  In other words, is fragment size less than 2X the read length? 
no
Number of additional sites filtered based on overlapping forward and reverse reads
5570 of 45395

Is this from a mixture of SE and PE libraries? Enter yes or no.
no
Number of additional sites filtered based on properly paired status
939 of 39825

Number of sites filtered based on high depth and lower than 2*DEPTH quality score
2470 of 38886

                                               Histogram of mean depth per site

      500 +---------------------------------------------------------------------------------------------------------+
          |+    +    +     +    +    +    +     +    +    +    +    +     +    +    +    +     +    +    +    +     |
      450 |-+                                      ** *   'meandepthpersite' using (bin($1,binwidth)):(1.0) *******-|
          |                                        ** *                                                             |
          |                                  **  ****** *                                                           |
      400 |-+                             ** *************                                                        +-|
          |                              *******************                                                        |
      350 |-+                          ***********************                                                    +-|
          |                        **  ***********************                                                      |
      300 |-+                      **  ************************ **                                                +-|
          |                       ********************************                                                  |
      250 |-+                     ********************************    **                                          +-|
          |                      ***********************************  **                                            |
          |                      *************************************** *                                          |
      200 |-+                  ***************************************** *                                        +-|
          |                  *********************************************                                          |
      150 |-+               **************************************************                                    +-|
          |               *******************************************************                                   |
      100 |-+          *  *********************************************************                               +-|
          |         ** **************************************************************                               |
          |         *****************************************************************  ***  * **                    |
       50 |-+    ******************************************************************************** *** **    ***  **-|
          |+    +***************************************************************************************************|
        0 +---------------------------------------------------------------------------------------------------------+
           12   24   36    48   60   72   84    96  108  120  132  144   156  168  180  192   204  216  228  240   252
                                                          Mean Depth

If distrubtion looks normal, a 1.645 sigma cutoff (~90% of the data) would be 29166.52005
The 95% cutoff would be 230
Would you like to use a different maximum mean depth cutoff than 230, yes or no 
no
Number of sites filtered based on maximum mean depth
 2370 of 38886

Number of sites filtered based on within locus depth mismatch
 23 of 36516

Total number of sites filtered
 12960 of 49453

Remaining sites
 36493

Filtered VCF file is called Output_prefix.FIL.recode.vcf

Filter stats stored in dDocent_filters_out.filterstats
```

## Step7: Convert our variant calls to SNPs

`vcfallelicprimitives dDocent_filters_out.FIL.recode.vcf --keep-info --keep-geno > DP3g95p5maf05.prim.vcf`

Feed this VCF file into VCFtools to remove indels

```shell
vcftools --vcf DP3g95p5maf05.prim.vcf --remove-indels --recode --recode-INFO-all --out SNP.DP3g95p5maf05

After filtering, kept 38619 out of a possible 40143 Sites
```

## Step8: HWE filter 

```shell
./filter_hwe_by_pop.pl -v SNP.DP3g95p5maf05.recode.vcf -p popmap -o SNP.DP3g95p5maf05.HWE -h 0.01
Processing population: EOB (36 inds)
Processing population: PBF (30 inds)
Processing population: WOB (30 inds)
Processing population: WOF (28 inds)
Outputting results of HWE test for filtered loci to 'filtered.hwe'
Kept 31009 of a possible 38619 loci (filtered 7610 loci)
```
