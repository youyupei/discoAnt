# discoAnt: isoform identification and quantification from long-read amplicon sequencing

Discoant is a pipeline for the identification of known and novel isoforms from targeted amplicon sequencing data generated with Oxford Nanopore Technologies long-read sequencing. 

## Contents

- [Installation](#installation)
- [Output](#Output)
- [Visualization](#Visualization)
- [General Usage](#General-Usage)

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
bash discoAnt_main sirv_test_data/sirv_params.txt
```
This should produce a folder called 'SIRV5_test' which contains the output of the pipeline.

## Dependencies

## General Usage

Parameters file with comments on usage:
```
## Experiment Info ##
OUTPUT_NAME=CLCN3
ENSG_ID=ENSG00000109572
# chr is used to filter reference files to increase speed
chr=chr4
##

## Paths to data ##
FASTA="path/to/sample/fasta_folders"
REF_GENOME_FN="path/to/hg38.fa"
ANNA_GTF="path/to/gencode.v44.annotation.gtf"
##

## Minimum read count per isoform threshold ##
# leave blank/delete for default value
read_count_minimum=5
samples_minimum=3
##

## Downsampling to be set to TRUE or FALSE ##
downsampling=TRUE
# below is checked only if downsampling is TRUE
# leave blank/delete for default value
number_reads_downsample=8000
##

## Primer site filter to be set to TRUE or FALSE ##
primer_site_based_filter=TRUE
# Primer coordinates for forward and reverse, as bed files
# Only checked if primer filtering is TRUE
forward_primers="path/to/forward.bed"
reverse_primers="path/to/reverse.bed"
##

## Optional arguments ##
# leave blank/delete lines for default value
max_intron_length=400
##
```
## Output

## Troubleshooting




