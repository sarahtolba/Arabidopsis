Arabidopsis Variant Calling Pipeline
This pipeline performs quality control, trimming, alignment, and variant calling on Arabidopsis thaliana sequencing data.

Input Files
Reference Genome: ~/Arabidopsis/fasta/GCF_000001735.4_TAIR10.1_genomic.fna

Raw FASTQ Reads: ~/Arabidopsis/fastq.files/DRR659586.fastq

Tools Used
FastQC: Quality control of raw and trimmed reads

Fastp: Trimming low-quality reads

BWA: Alignment to the reference genome

Samtools: BAM file manipulation and statistics

BCFtools: Variant calling and filtering

Pipeline Steps
Set working directory

Quality control
Run FastQC on the raw FASTQ file.

Trimming
Use fastp to trim low-quality bases.

Post-trimming QC
Run FastQC on the cleaned FASTQ file.

Reference indexing
Index the reference genome using BWA.

Alignment
Align reads to the reference using BWA-MEM.

SAM/BAM Conversion and Sorting
Convert SAM to BAM, sort and index it using Samtools.

Alignment Statistics
Generate alignment statistics using Samtools flagstat.

Variant Calling
Use BCFtools mpileup and bcftools call to generate a compressed VCF file.

VCF Indexing and Viewing
Index and view called variants.

Output Files
results/fastq.fastp: Trimmed FASTQ file

results/*.html: FastQC reports

alignment/align.sam: Raw alignment file

alignment/align.sorted.bam: Sorted and indexed BAM

alignment/stat: Alignment statistics

variants/raw_variants.vcf.gz: Called variants in compressed VCF format

Notes
Ensure all required tools are installed and available in your $PATH.

Create the following directories before running: results/, alignment/, variants/

Modify paths as needed based on your system.

To Run the Pipeline

bash run_pipeline.sh
