# discoAnt: isoform identification and quantification from long-read amplicon sequencing

Discoant is a pipeline for the identification of known and novel isoforms from targeted amplicon sequencing data generated with Oxford Nanopore Technologies long-read sequencing. 

## Contents

- [Installation](#installation)
- [Dependencies](#dependencies)
- [General Usage](#General-Usage)
- [Output](#Output)
- [Visualisation](#Visualisation)
- [Troubleshooting](#Troubleshooting)

## Installation

Download the pipeline with Git:
```
git clone https://github.com/youyupei/discoAnt.git
```

Run the setup script:
```
cd discoAnt
bash scripts/discoAnt_setup
```
*Note*: depending on your operating system you may need to edit the setup script to either 'conda activate' or 'source activate'.

Test the installation:
```
cd discoAnt
conda activate discoAnt
./discoAnt_main sirv_test_data/sirv_params.ini
```
This should produce a folder called 'SIRV5_test' which contains the expected output of the pipeline.

## Dependencies
Dependencies are automatically built in a conda environment when the setup script is executed.

Required:
  - python >= 3.7.6
  - BBMap
  - bedtools
  - samtools
  - salmon == 0.14
  - gffread
  - gffcompare
  - minimap2

  R and R libraries:
  - R >= 4.3
  - Bioconductor
  - optparse
  - bambu >= 3.2.4

## General Usage
Run discoAnt with the following command after editing the parameters file:
```
./discoAnt_main parameters.ini
```

Parameters file with comments on usage:
```
## Experiment Info ##
# a folder will be created with OUTPUT_NAME and this is used as a prefix for files
OUTPUT_NAME=CLCN3
# the ENSEMBL ID is used to filter reference files to increase speed
ENSG_ID=ENSG00000109572
# chromosome is used to filter genome reference file to increase speed
chr=chr4
##

## Paths to data ##
# standard output for barcoded amplicon sequencing is multiple barcode/sample folers containing fastq or fasta files
# supports .fasta or .fastq
FASTA="path/to/sample/fa_folders"
# path to reference genome 
REF_GENOME_FN="path/to/hg38.fa"
# path to reference annotation
ANNA_GTF="path/to/gencode.v44.annotation.gtf"
##

## Minimum read count per isoform threshold ##
# these values can be left blank to use default values
read_count_minimum=5 # default is 5
samples_minimum=3 # default is half the total number of samples (rounded to integer)
##

## Downsampling to be set to TRUE or FALSE ##
# Downsampling results in the same number of reads for every sample, reducing inter-sample bias
downsampling=TRUE # default is TRUE
# below is checked only if downsampling is TRUE
# leave blank/delete for default value
number_reads_downsample=8000 # default is 8000
##

## Primer site filter to be set to TRUE or FALSE ##
# Recommended to increase accuracy and reduce isoforms to only those amplified with primers
# leave blank/delete for default values
primer_site_based_filter=TRUE # default is FALSE
# Primer coordinates for forward and reverse, as bed files
# Only checked if primer filtering is TRUE
forward_primers="path/to/forward.bed" # default is NULL
reverse_primers="path/to/reverse.bed" # default is NULL
##

## Optional arguments ##
# minimap2 typically only checks a distance of 200k, genes with long introns cause errors
# leave blank/delete lines for default value
max_intron_length=400 # default is 400
##
```
Basic parameters file:
```
OUTPUT_NAME=CLCN3
ENSG_ID=ENSG00000109572
chr=chr4
FASTA="path/to/sample/fa_folders"
REF_GENOME_FN="path/to/hg38.fa"
ANNA_GTF="path/to/gencode.v44.annotation.gtf"
```

## Output
The main output of discoAnt includes three files:
  - a basic text report
  - annotations of known and novel isoforms as a GTF
  - quantifications of known and novel isoforms as a CSV

## Visualisation

## Troubleshooting




