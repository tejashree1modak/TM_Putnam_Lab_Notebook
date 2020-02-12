---
layout: post
title: Pipeline for clean up of data
tags: [ EpiRAD, ddRAD, Moorea,Pipeline] 
---

### Getting the data
 - Data was copied from Hollie's disk to KITT  /RAID_STORAGE2/Shared_Data/20190819_RAD_EPIRAD/30-233732769/
 - I copied it from here to my dir tejashree/Moorea/raw_data/
 
### Barcode files
1. Barcode files were made from the csv file on google drive [Moorea_2018_Sampling Adapter/Index Map](https://docs.google.com/spreadsheets/d/16-kpj1MxpjoXOS4QKDRDBEfBdi5EjDHvGYgChyr6y6A/edit#gid=214392799)

2. Barcode files for renaming STACKS output files for dDocent: dDocent requires barcodes file to rename .fq.gz files as it wants loc_sample.fq.gz.These were generated as before but adding the location name from the shared google drive csv [Moorea_2018_Sampling](https://docs.google.com/spreadsheets/d/16-kpj1MxpjoXOS4QKDRDBEfBdi5EjDHvGYgChyr6y6A/edit#gid=0). An acronym for each location was made as follows: 

- West Opunohu Backreef : WOB
- East Opunohu Backreef : EOB
- Public Beach Fringe: PBF
- West Opunohu Fringe: WOF

### STACKS
Script used: [GitHub](https://github.com/tejashree1modak/EPIRAD_Moorea/blob/master/stacks.sh) 
`stacks.sh`
1. Clone filter: This step will reduce each set of identical oligos to a single representative in the output. 
2. Process_radtags: This program examines raw reads from an Illumina sequencing run and first, checks that the barcode and the RAD cutsite are intact, and demultiplexes the data. 

### Ddocent 
#### Renaming output files from Stacks [GitHub](https://github.com/tejashree1modak/EPIRAD_Moorea/blob/master/Rename_for_dDocent.sh)
`Rename_for_dDocent.sh`
Edited the script to handle paired-end barcodes

