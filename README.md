# reconstruct_sequences
Reconstructions of consensus fasta sequences; reconstructions of fasta sequences according to AF thresholds for specific genes.

# In this case, MSP2 haplotype reconstruction from targeted deep sequencing

This repository documents the workflow used to reconstruct MSP2 gene sequences
from Illumina targeted deep sequencing data of Plasmodium falciparum.

The approach generates sample-specific MSP2 sequences stratified by allele
frequency (AF) thresholds, enabling downstream phylogenetic and diversity
analyses (e.g. in MEGA).

## Data

- Input VCFs: Mutect2 post-filtered, bgzipped and indexed
- Reference genome: Pfalciparum.genome.fasta (3D7)

## Target gene

- Gene: msp2
- Gene ID: PF3D7_0206800
- Coordinates: Pf3D7_02_v3:271576–274917

## Overview of the workflow

1. Extract MSP2 variants from multiple VCF files
2. Group variants by sample
3. Apply allele-frequency thresholds
4. Reconstruct haplotype sequences per sample and AF cutoff
5. Export sequences in FASTA format
6. Append the MSP2 reference sequence

## Tools

- bcftools
- samtools
- Python 3
