---
layout: post
title: Running dDocent with a subsample
tags: [ ddRAD, Moorea, dDocent, assembly ]
---

# Running a test assembly on a subset of data

## Choosing a subset 
We decided to choose 5 individuals from each of the four locations and start the test assemblywith 20 individuals. The selected individuals can be found in Assembly_subset_round1.csv uploaded separately. 

## dDocent Assembly 
The files for the chosen subset was copied into a new dir called round1/RefOpt housed in the /home/tejashree/Moorea/ddocent/ dir. 
dDocent was run allowing trimming, type of assembly PE, clustering similarity 0.85%, Minimum within individaul coverage level to include a read for assembly (K1) = 3, Minimum number of individuals a read must be present in to include for assembly (K2) also as 3 since this was the value right before the asympote for both plots. The rest of the parameters were chosen as defaults. The log file round1/ReOpt/dDocent.runs has all the chosen parameters for this run. 

'dDocent assembled 76568 sequences (after cutoffs) into 26666 contigs'

