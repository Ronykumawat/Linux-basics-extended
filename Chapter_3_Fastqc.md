# Chapter 3: FastQC - Quality Control Analysis
![FastQC Logo](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_icon.png)

FastQC analyzes raw sequencing data to identify quality issues before downstream analysis.

## What is FastQC?

Identifies potential problems in FASTQ files:
- Low-quality bases at sequence ends
- Adapter contamination
- Sequence biases
- GC content anomalies
- High duplication levels

## Installation

```bash
mamba create -n qc -c bioconda fastqc
mamba activate qc
fastqc --version
```

## Basic Usage

```bash
# Analyze single file
fastqc sample.fastq

# Multiple files
fastqc *.fastq

# Specify output directory
fastqc -o results/ sample.fastq

# With threading (faster)
fastqc -t 4 -o results/ *.fastq

# Quiet mode for batch processing
fastqc --quiet -o results/ *.fastq
```

## Report Contents

| Module | What It Shows |
|--------|---------------|
| Per Base Quality | Phred score at each position (Green=Good, Red=Bad) |
| Sequence Quality | Overall quality score distribution |
| Per Base Content | A/C/G/T distribution at each position |
| Adapter Content | Detects leftover sequencing adapters |
| GC Content | Overall GC percentage |
| N Content | Uncalled bases (N's) percentage |
| Duplication | Sequence duplication levels |

## Interpreting Results

```bash
# View HTML report
open sample_fastqc.html        # macOS
xdg-open sample_fastqc.html    # Linux
firefox sample_fastqc.html     # Alternative
```

Quality scoring:
- **Green (PASS)**: Good quality
- **Orange (WARN)**: May need attention
- **Red (FAIL)**: Potential problems

## Batch Processing

```bash
# Process all files with reports
for file in *.fastq; do
  fastqc -o results/ "$file"
done

# Extract summary
grep ">>.*pass" results/*/summary.txt | wc -l
```

## Next Steps

If quality is poor:
```bash
# Install trimming tool
mamba create -n trim -c bioconda fastp

# Trim low-quality sequences
fastp -i sample.fastq -o trimmed.fastq -q 20 -l 50
```

After trimming, re-run FastQC to verify improvements!

You're ready to assess sequencing quality!