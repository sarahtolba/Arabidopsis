# Arabidopsis Variant Calling Pipeline

This pipeline performs quality control, trimming, alignment, and variant calling on *Arabidopsis thaliana* sequencing data.



## Input Files

 **Reference Genome:**  
  `~/Arabidopsis/fasta/GCF_000001735.4_TAIR10.1_genomic.fna`

 **Raw FASTQ Reads:**  
  `~/Arabidopsis/fastq.files/DRR659586.fastq`

 **Chromosome Rename Map (`chr.txt`):**
  
NC_003070.9   Chr1
NC_003071.7   Chr2
NC_003074.8   Chr3
NC_003075.7   Chr4
NC_003076.8   Chr5


---

## Tools Used

- **FastQC:** Quality control of raw and trimmed reads  
- **Fastp:** Trimming low-quality reads  
- **BWA:** Alignment to the reference genome  
- **Samtools:** BAM file manipulation and statistics  
- **BCFtools:** Variant calling and filtering  
- **snpEff:** Variant annotation  

---

## Pipeline Steps

1. **Set working directory**

2. **Quality control**  
 Run FastQC on the raw FASTQ file.

3. **Trimming**  
 Use fastp to trim low-quality bases.

4. **Post-trimming QC**  
 Run FastQC on the trimmed FASTQ file.

5. **Reference indexing**  
 Index the reference genome using BWA.

6. **Alignment**  
 Align reads to the reference using BWA-MEM.

7. **SAM/BAM Conversion and Sorting**  
 Convert SAM to BAM, sort, and index with samtools.

8. **Alignment Statistics**  
 Generate alignment statistics using `samtools flagstat`.

9. **Variant Calling**  
 Use bcftools mpileup and call to generate a compressed VCF.

10. **VCF Indexing and Viewing**  
  Index and view variants.

11. **Variant Filtering**  
  Filter variants by quality and depth (QUAL < 30 or DP < 10).

12. **Chromosome Renaming**  
  Rename chromosome names in the VCF using `chr.txt` to match annotation database.

13. **Variant Annotation**  
  Annotate filtered variants with snpEff (download *Arabidopsis thaliana* database if needed).

14. **Get Annotation Summary**  
  Extract summary info from annotated VCF.

---

## Output Files

- `results/fastq.fastp` — Trimmed FASTQ file  
- `results/*.html` — FastQC reports  
- `alignment/align.sam` — Raw alignment file  
- `alignment/align.sorted.bam` — Sorted and indexed BAM  
- `alignment/stat` — Alignment statistics  
- `variants/raw_variants.vcf.gz` — Raw called variants (compressed)  
- `variants/filtered_variants.vcf.gz` — Filtered variants  
- `variants/renamed_variants.vcf.gz` — Chromosome-renamed variants  
- `variants/annotated.vcf` — Annotated variants  
- `variants/annotated_variants.tsv` — Annotation summary table  


## Important Notes

- Make sure all required tools are installed and available in your `$PATH`.
- Create the following directories **before** running the script:  
`results/`, `alignment/`, `variants/`
- Ensure `chr.txt` contains the chromosome mapping shown above.
- Modify file paths in the script as needed depending on your system.
- The snpEff database for *Arabidopsis thaliana* will be downloaded automatically by the script (or can be downloaded manually beforehand).
- 

## How to Run

bash run_pipeline.sh
