# 🔍 Chapter 3: FastQC - Quality Control Analysis

> **Understand your sequencing data before analysis!**

---

## 📊 What is FastQC?

FastQC analyzes raw sequencing data (FASTQ files) to identify potential quality issues:

| Issue | Impact | Severity |
|-------|--------|----------|
| 🔴 Low-quality bases | Assembly errors | High |
| 🟡 Adapter contamination | False sequences | Medium |
| 🟡 Sequence biases | Assembly bias | Medium |
| 🟢 GC anomalies | May be biological | Low |
| 🟢 High duplication | PCR artifacts | Low |

---

## 🚀 Installation

```bash
# Using Mamba (recommended)
mamba create -n qc -c bioconda fastqc
mamba activate qc

# Verify
fastqc --version
```

---

## 💻 Basic Usage

### Single File
```bash
fastqc sample.fastq
```

### Multiple Files
```bash
fastqc *.fastq
```

### With Output Directory
```bash
fastqc -o results/ sample.fastq
```

### Parallel Processing (4 threads)
```bash
fastqc -t 4 -o results/ *.fastq
```

### Quiet Mode (for scripts)
```bash
fastqc --quiet -o results/ *.fastq
```

---

## 📈 Understanding Reports

### Report Modules

| Module | What It Measures | Pass Criteria |
|--------|------------------|---------------|
| **Per Base Quality** | Phred score at each position | Q > 28 across genome |
| **Per Sequence Quality** | Overall read quality | Peak at Q > 30 |
| **Per Base Content** | A/C/G/T distribution | Even distribution |
| **Adapter Content** | Leftover adapters | < 5% |
| **GC Content** | % of G+C bases | Matches expected |
| **N Content** | Uncalled bases (N) | < 0.1% |
| **Duplication Levels** | Repeated sequences | < 50% |

### Traffic Light System

🟢 **PASS** - Good quality, no action needed  
🟡 **WARN** - Possible issue, may need attention  
🔴 **FAIL** - Likely problem, investigate  

---

## 📖 Viewing Reports

```bash
# HTML reports generated automatically
open sample_fastqc.html        # macOS
xdg-open sample_fastqc.html    # Linux
firefox sample_fastqc.html     # Alternative
```

---

## 🔄 Batch Processing

### Process All Files
```bash
for file in *.fastq; do
  echo "Processing: $file"
  fastqc -o results/ "$file"
done
```

### Count Results
```bash
# How many files passed QC?
grep ">>.*PASS" results/*/summary.txt | wc -l

# Which files failed?
grep FAIL results/*/summary.txt
```

---

## ⚠️ Common Issues & Solutions

### ❌ Low Quality at 3' End
**Cause:** Sequencing degradation  
**Solution:** Trim 3' ends
```bash
fastp -i input.fastq -o output.fastq --length_required 50
```

### ❌ High Adapter Content
**Cause:** Incomplete adapter removal  
**Solution:** Re-trim with adapters
```bash
trim_galore --adapter AGATCGGAAGAGC input.fastq
```

### ❌ High N Content
**Cause:** Sequencing errors  
**Solution:** Filter low-quality reads
```bash
fastp -i input.fastq -o output.fastq -q 20
```

### ✅ GC Bias (FAIL)
**Note:** May be biological! Don't always trim  
**Action:** Document and proceed carefully

---

## 🔧 Advanced Options

```bash
# Extract results only (no HTML)
fastqc --noextract sample.fastq

# Specific format
fastqc --format bam input.bam

# No group bases by position (fine resolution)
fastqc --nogroup sample.fastq
```

---

## 📋 Quality Control Checklist

- [ ] Run FastQC on raw data
- [ ] Check all reports
- [ ] Identify problem samples
- [ ] Decide: trim or filter?
- [ ] Re-run FastQC after trimming
- [ ] Verify improvements
- [ ] Document decisions

---

## 🎯 Next Steps

If quality is **POOR**:
```bash
mamba create -n trim -c bioconda fastp
fastp -i sample.fastq -o trimmed.fastq -q 20 -l 50
```

If quality is **GOOD**:
```bash
# Proceed to assembly!
cd ../Chapter_4_Trimming_and_assembly.md
```

---

## 📚 Resources

- [FastQC Official](https://www.bioinformatics.babraham.ac.uk/projects/fastqc/)
- [Phred Quality Scores](https://en.wikipedia.org/wiki/Phred_quality_score)
- [NGS Best Practices](https://www.illumina.com/)

---

**Ready to QC your data? Let's assess! 📊**