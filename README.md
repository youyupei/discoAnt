# IsoLamp: isoform identification and quantification from long-read amplicon sequencing data

IsoLamp is a bash pipeline for the identification of known and novel isoforms from targeted amplicon long-read sequencing data generated with Oxford Nanopore Technologies. 

<img src="https://github.com/youyupei/discoAnt/assets/30969357/aa0684e7-4878-4440-a41a-2e2b121fe0c4" width="440" height="600">

## Contents

- [Installation](#installation)
- [Usage](#usage)
- [SIRV Test Dataset](#SIRV-test-dataset)
- [Dependencies](#dependencies)
- [Input Data](#input-data)
- [Parameters](#parameters)
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
cd IsoLamp
bash scripts/IsoLamp_setup
```
**Note:** depending on your operating system you may need to edit the setup script to either 'conda activate' or 'source activate'.

## Usage

We suggest adding IsoLamp to your PATH so it can be run from any directory:
```
echo 'export PATH=~/path/to/IsoLamp:$PATH' >> ~/.bash_profile
source ~/.bash_profile
```

Run IsoLamp (after editing the parameters file):
```
conda activate IsoLamp

IsoLamp parameters.ini 

# alternatively, if not in PATH:
./IsoLamp parameters.ini # if running from same directory
~/path/to/IsoLamp/IsoLamp parameters.ini # provide full path when running from other directories
```

## SIRV test dataset
Test the installation on the provided SIRV data:
```
conda activate IsoLamp
IsoLamp sirv_test_data/sirv_params.ini
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

## Input data
The pipeline is designed to run on barcoded data produced by Oxford Nanopore Technologies. This is typically a directory containing subdirectories titled 'barcode01', 'barcode02' etc. Each barcode directory contains either single or multiple FASTA or FASTQ files of reads.

Please see the sirv_test_data/test_fasta directory for an example of the structure required. If you don't have barcoded data, please create a subdirectory with your single sample name and place all read FASTA or FASTQ files inside this directory (nanopore_data/sample_name/all_reads.fastq).

**Note:** the 'barcode' name is arbitrary, your subdirectories can be renamed to sample names or any identifiers.

## Parameters
Parameters file with comments on usage:
```
## Experiment Info ##
# a folder will be created with OUTPUT_NAME and this is used as a prefix for files
OUTPUT_NAME=CLCN3
# the ENSEMBL ID is used to filter reference files to increase speed
ENSG_ID=ENSG00000109572
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
# bambu parameters, leave blank for defaults
bambu_ndr=1
bambu_min_gene_fraction=0.005
##
```
Basic parameters file:
```
OUTPUT_NAME=CLCN3
ENSG_ID=ENSG00000109572
FASTA="path/to/sample/fa_folders"
REF_GENOME_FN="path/to/hg38.fa"
ANNA_GTF="path/to/gencode.v44.annotation.gtf"
```

## Output
The main output of IsoLamp includes three files:
  - a basic text report
  - annotations of known and novel isoforms as a GTF
  - quantifications of known and novel isoforms as a CSV

## Visualisation

## Troubleshooting




