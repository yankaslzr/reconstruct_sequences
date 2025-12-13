# reconstruct_sequences

Reconstruction of FASTA sequences from Illumina targeted deep sequencing data, including
consensus-like reconstructions stratified by allele frequency (AF) thresholds for specific genes. It can be adapted to other targets, in this case it was used for pfmsp2.

## MSP2 haplotype reconstruction from targeted deep sequencing

This repository documents a workflow to reconstruct *Plasmodium falciparum* **MSP2**
gene sequences from Illumina targeted deep sequencing data.

Instead of generating a single consensus sequence per sample, this approach reconstructs
**sample-specific MSP2 haplotypes stratified by allele frequency (AF) thresholds**, allowing
the exploration of within-host diversity and minority variants.  
The resulting FASTA files are suitable for downstream analyses such as phylogenetics,
haplotype comparison, and diversity analyses (e.g. using MEGA).

---

## Data requirements

### Input files

- **VCF files**
  - Variant caller: Mutect2
  - Post-filtered
  - Compressed with `bgzip` and indexed (`.vcf.gz` + `.tbi`)
  - One VCF per sample

- **Reference genome**
  - *Plasmodium falciparum* 3D7 reference genome  
  - `Pfalciparum.genome.fasta` (indexed with `samtools faidx`)

---

## Target gene

- Gene name: **msp2**
- Gene ID: **PF3D7_0206800**
- Chromosome: **Pf3D7_02_v3**
- Coordinates (1-based, inclusive): **271576–274917**
- Gene length: **3342 bp**

---

## Workflow overview

1. Extract MSP2 variants from multiple VCF files using `bcftools`
2. Aggregate variants across samples into a single TSV file
3. Load the MSP2 reference sequence from the genome FASTA
4. Reconstruct haplotype sequences per sample using different AF cutoffs
5. Export reconstructed haplotypes in FASTA format
6. Append the MSP2 reference sequence to the final FASTA file

---

## Allele frequency thresholds

Haplotype sequences are reconstructed using the following minimum AF cutoffs:

- AF ≥ 0.01  
- AF ≥ 0.05  
- AF ≥ 0.10  
- AF ≥ 0.20  
- AF ≥ 0.50  
- AF ≥ 0.90  

For each sample, one MSP2 sequence is generated per AF threshold.

