# 🖥️ Session 2B-ii: Assembly Quality Assessment

**🎯 Goal:** Evaluate your assembled genome for quality, completeness, and contamination  
**🛠️ Tools:** QUAST · BUSCO · RagTag

---

## 🧠 Concept: Why Assess Assembly Quality?

Assembling reads into contigs doesn't mean you're done. Your assembly could have:

- ❌ **Fragmentation** — the genome is broken into thousands of tiny pieces
- ❌ **Misassemblies** — contigs that join regions that shouldn't be joined
- ❌ **Incompleteness** — large parts of the genome are missing
- ❌ **Contamination** — sequences from other organisms (bacteria, human, etc.)

**Quality Assessment (QA)** checks all of these problems before you trust your assembly for downstream analyses like gene prediction or variant calling.

### The Pillars of Assembly QA

```
Assembly Quality

        Contiguity ──── QUAST  (how fragmented is it?)
        Completeness ── BUSCO  (are expected genes present?)
```

---

## 📁 Required Input Files

| File | Format | Description | From | Download command |
|------|--------|-------------|------|------------------|
| `contigs.fasta` | FASTA | Assembled genome | Download or Provided |```wget https://raw.githubusercontent.com/mukulverma22/ICMR_genome_assembly-/refs/heads/main/day2-genome-assembly/contigs.fasta``` |
| BUSCO lineage | Auto-downloaded | Gene database for completeness check | BUSCO downloads automatically |



---

## 🔧 Tool 1: QUAST

### What is QUAST?
**QUAST** (Quality Assessment Tool for Genome Assemblies) measures the **contiguity** of your assembly. It answers:
- How fragmented is the assembly? (fewer contigs = better)
- How long are the contigs? (longer = better)
- If given a reference: Where are the misassemblies?

### Verify installation of QUAST
```bash
# Verify
quast.py --version
```

### Understanding Key QUAST Metrics

#### N50 — The Most Important Metric

Imagine laying all your contigs end-to-end from longest to shortest. **N50 is the length of the contig where you've covered 50% of the total assembly.**

```
Contig lengths: [50000, 30000, 20000, 15000, 10000, 5000, 3000...]
Total assembly = 200,000 bp
50% of total  = 100,000 bp

Cumulative:
50000 bp ──── (25%)
50000 + 30000 = 80000 bp ──── (40%)
80000 + 20000 = 100000 bp ──── (50%) ← N50 = 20,000 bp ✅
```

| N50 Interpretation | Meaning |
|-------------------|---------|
| N50 = genome size | Perfect single contig assembly |

### Run QUAST

```bash
mkdir -p quast

quast.py \
    contigs.fasta \
    --output-dir quast \
    --threads 2
```

```
# Flag explanations:
# assembly.fasta      : Your assembled genome (from SPAdes)
# --output-dir        : Where to save results
# --threads           : CPU threads
```

### QUAST Output Files

```
quast/
├── report.html         ← ✅ Open this in your browser!
├── report.txt          ← Plain text summary
├── report.tsv          ← Tab-separated (import to Excel)
└── icarus.html         ← Interactive contig browser
```

### Reading the QUAST Report

Key metrics to check in `report.txt`:

```
# contigs (>= 0 bp)          ← Total contigs (lower = better)
# contigs (>= 1000 bp)       ← Contigs >1kb (more meaningful)
Total length                  ← Should match expected genome size
Largest contig                ← Longest single contig
N50                           ← Most important! (higher = better)
```
---


## 🔧 Tool 2: BUSCO

### What is BUSCO?
**BUSCO** (Benchmarking Universal Single-Copy Orthologs) assesses **genome completeness** by checking for the presence of genes that are expected to be present in **every species of a given lineage**.

The logic: If your genome assembly is complete, it should contain nearly all the genes that evolution has conserved across that group of organisms.

> 🔑 **Key Insight:** BUSCO doesn't just count how much sequence is assembled — it checks if biologically important genes are present and intact.

### BUSCO Categories

For each universal single-copy gene, BUSCO classifies it as:

| Category | Symbol | Meaning |
|----------|--------|---------|
| **Complete Single-Copy** | `C:S` | Present once ✅ |
| **Complete Duplicated** | `C:D` | Present, but duplicated (possible contamination or polyploidy) ⚠️ |
| **Fragmented** | `F` | Partially present (assembly gaps?) ⚠️ |
| **Missing** | `M` | Not found (incomplete assembly) ❌ |

**A good BUSCO result looks like:**
```
C:98.2% [S:97.8%, D:0.4%], F:0.5%, M:1.3%
```

**A poor BUSCO result looks like:**
```
C:45.3% [S:44.9%, D:0.4%], F:8.2%, M:46.5%
← Only 45% of expected genes found! Very incomplete assembly.
```

### Verify the installation of BUSCO
```bash
# Verify
busco --version
```

### Choose the Right BUSCO Lineage Database

BUSCO has different gene databases for different organism groups:

```bash
# List available lineages
busco --list-datasets

```
```
# Common lineages:
# bacteria_odb10    ← Bacterial genomes
# fungi_odb10       ← Fungal genomes
# metazoa_odb10     ← Animals (broad)
# viridiplantae_odb10 ← Plants
# eukaryota_odb10   ← All eukaryotes (broadest)
# NOTE: Viruses don't have a standard BUSCO lineage
#       BUSCO is mainly used for larger genomes
```

> ⚠️ **Note for today's viral assembly:** BUSCO is less applicable for viral genomes (too small, too variable). We're running it for training purposes. For viral completeness, QUAST's genome fraction metric is more meaningful.

### Run BUSCO

```bash
busco \
    --in contigs.fasta \
    --out busco_results \
    --mode genome \
    --lineage_dataset bacteria_odb10 \
    --cpu 2 \
    --download_path ./busco_downloads
```

```

# Flag explanations:
# --in              : Input assembly (FASTA)
# --out             : Output folder name (created inside --out_path)
# --out_path        : Parent directory for output
# --mode            : genome (assembly), transcriptome, or proteins
# --lineage_dataset : Which BUSCO database to use
# --cpu             : Number of CPU threads
# --download_path   : Where to cache downloaded databases
```

### BUSCO Output

```
busco_results/
├── short_summary.specific.bacteria_odb10.busco_results.txt  ← ✅ Key results
├── run_bacteria_odb10/
│   ├── full_table.tsv       ← Status of each individual BUSCO gene
│   └── missing_busco_list.tsv ← List of missing genes
└── logs/
    └── busco.log
```

---

## 🎉 Congratulations!

You've completed the full genome assembly pipeline:

```
Raw Reads (.fastq)
    ↓ FastQC → Fastp → MultiQC
Clean Reads
    ↓ SPAdes / Setu
Draft Assembly
    ↓ QUAST → BUSCO
Assembly Assessment

```

---

*See you at dinner! 🍽️*
