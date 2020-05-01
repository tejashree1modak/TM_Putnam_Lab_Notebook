---
layout: post
title: SNP filtering full data set
tags: [ ddRAD, epiRAD, Moorea, dDocent, SNP, filter ]
---

# SNP filtering 
This filtering was performed on full data set per the [SNP filtering tutorial] (http://www.ddocent.com/filtering/) in dDocent.
The filtration is housed in /home/tejashree/Moorea/ddocent/final/snp_filtering/.

## Step1: 50% of individuals, a minimum quality score of 30, and a minor allele count of 3

```shell
vcftools --vcf TotalRawSNPs.vcf --max-missing 0.5 --mac 3 --minQ 30 --recode --recode-INFO-all --out raw.g5mac3

After filtering, kept 124 out of 124 Individuals
Outputting VCF file...
After filtering, kept 288777 out of a possible 773896 Sites
```

## Step2: Minimum mean depth

```shell
vcftools --vcf raw.g5mac3.recode.vcf --minDP 3 --recode --recode-INFO-all --out raw.g5mac3dp3`

After filtering, kept 124 out of 124 Individuals
Outputting VCF file...
After filtering, kept 288777 out of a possible 288777 Sites`
```

## Step3: Filter missing indiv 

```shell
vcftools --vcf raw.g5mac3dp3.recode.vcf --missing-indv
cat out.imiss
mawk '$5 > 0.3' out.imiss | cut -f1 > lowDP.indv
vcftools --vcf raw.g5mac3dp3.recode.vcf --remove lowDP.indv --recode --recode-INFO-all --out raw.g5mac3dplm`

After filtering, kept 117 out of 124 Individuals
Outputting VCF file...
After filtering, kept 288777 out of a possible 288777 Sites
```

## Step4: Restrict the data to variants called in a high percentage of individuals and filter by mean depth of genotypes 

```shell
vcftools --vcf raw.g5mac3dplm.recode.vcf --max-missing 0.95 --maf 0.05 --recode --recode-INFO-all --out DP3g95maf05 --min-meanDP 20
After filtering, kept 117 out of 117 Individuals
Outputting VCF file...
After filtering, kept 51772 out of a possible 288777 Sites
```

## Step5: Filtering by population specific call rate when multiple localities are present

```shell
cut -f1 out.imiss|awk  -F "_" 'NR>1{print $1"_"$2"_"$3,$1}' > popmap
cat popmap
mawk '$2 == "EOB"' popmap > 1.keep && mawk '$2 == "PBF"' popmap > 2.keep && mawk '$2 == "WOB"' popmap > 3.keep && mawk '$2 == "WOF"' popmap > 4.keep                                                        vcftools --vcf DP3g95maf05.recode.vcf --keep 1.keep --missing-site --out 1
vcftools --vcf DP3g95maf05.recode.vcf --keep 2.keep --missing-site --out 2                                                                                                                                  vcftools --vcf DP3g95maf05.recode.vcf --keep 3.keep --missing-site --out 3
vcftools --vcf DP3g95maf05.recode.vcf --keep 4.keep --missing-site --out 4                                                                                                                                  cat 1.lmiss 2.lmiss 3.lmiss 4.lmiss | mawk '!/CHR/' | mawk '$6 > 0.1' | cut -f1,2 >> badloci
vcftools --vcf DP3g95maf05.recode.vcf --exclude-positions badloci --recode --recode-INFO-all --out DP3g95p5maf05

After filtering, kept 117 out of 117 Individuals
Outputting VCF file...
After filtering, kept 49453 out of a possible 51772 Sites
```

## Step6: Used dDocent_filters script 

```shell
./dDocent_filters DP3g95p5maf05.recode.vcf dDocent_filters_out

Total number of sites filtered
 12960 of 49453

 Remaining sites
  36493
```

# Step7: Convert our variant calls to SNPs

`vcfallelicprimitives dDocent_filters_out.FIL.recode.vcf --keep-info --keep-geno > DP3g95p5maf05.prim.vcf`

#feed this VCF file into VCFtools to remove indels

```shell
vcftools --vcf DP3g95p5maf05.prim.vcf --remove-indels --recode --recode-INFO-all --out SNP.DP3g95p5maf05

After filtering, kept 38619 out of a possible 40143 Sites
```

# Step8: HWE filter 

```shell
./filter_hwe_by_pop.pl -v SNP.DP3g95p5maf05.recode.vcf -p popmap -o SNP.DP3g95p5maf05.HWE -h 0.01
Processing population: EOB (36 inds)
Processing population: PBF (30 inds)
Processing population: WOB (30 inds)
Processing population: WOF (28 inds)
Outputting results of HWE test for filtered loci to 'filtered.hwe'
Kept 31009 of a possible 38619 loci (filtered 7610 loci)
```
