# 🌍 Chapter 6: Metagenomics - Classification & Visualization

![Metagenomics](https://img.shields.io/badge/Metagenomics-Community%20Analysis-orange?style=for-the-badge&logo=network&logoColor=white)

Metagenomics analyzes genetic material from environmental samples to understand microbial communities.

> 🔬 **Explore:** Discover hidden microbes in environmental samples!

---

## 📚 What is Metagenomics?

Metagenomics studies:
- **Community Composition**: Which organisms are present?
- **Functional Genes**: What metabolic capabilities exist?
- **Diversity**: How many different species?
- **Assembly**: Reconstructing genomes from mixed samples

---

## 🏷️ Classification with Kraken2

### 📥 Installation & Setup

```bash
mamba create -n kraken -c bioconda kraken2
mamba activate kraken

# Download standard database (8GB)
kraken2-build --standard --db kraken_db/
```

### 🔍 Taxonomic Classification

**Single file:**
```bash
kraken2 --db kraken_db/ reads.fastq --output output.kraken
```

**Paired-end with reporting:**
```bash
kraken2 --db kraken_db/ --paired read1.fastq read2.fastq \
         --output sample.kraken --report sample.kreport
```

**With threading:**
```bash
kraken2 --db kraken_db/ sample.fastq \
         --threads 8 --output output.kraken --report report.txt
```

---

## 📊 Visualization with Krona

### 📦 Installation

```bash
mamba create -n krona -c bioconda krona
```

### 🎨 Create Interactive Charts

```bash
# Convert and visualize
kraken-translate sample.kraken | \
ktImportTaxonomy /dev/stdin -o interactive.html

# View in browser
open interactive.html        # macOS
xdg-open interactive.html    # Linux
```

---

## 🚀 Assembly with MEGAHIT

```bash
mamba create -n megahit -c bioconda megahit

# Metagenomic assembly
megahit -1 read1.fastq -2 read2.fastq \
        -o megahit_output/ -t 16 -m 0.9
```

---

## 📦 Binning with MetaBAT2

```bash
mamba create -n metabat -c bioconda metabat2

# Generate coverage and bin
jgi_summarize_bam_contig_depths --outputDepth depth.txt *.bam
metabat2 -i assembly.fasta -a depth.txt -o bins/bin -t 16
```

## Complete Pipeline

```bash
#!/bin/bash
READ1="reads_R1.fastq"
READ2="reads_R2.fastq"
SAMPLE="sample"
THREADS=16

echo "Metagenomic analysis pipeline"

# Classification
echo "Classifying with Kraken2..."
mkdir -p classification
kraken2 --db kraken_db/ --paired "$READ1" "$READ2" \
         --threads $THREADS --output classification/${SAMPLE}.kraken \
         --report classification/${SAMPLE}.kreport

# Visualization
echo "Creating Krona visualization..."
kraken-translate classification/${SAMPLE}.kraken | \
ktImportTaxonomy /dev/stdin -o classification/${SAMPLE}_krona.html

# Assembly
echo "Assembling metagenome..."
mkdir -p assembly
megahit -1 "$READ1" -2 "$READ2" -o assembly/${SAMPLE}/ -t $THREADS -m 0.9

echo "Pipeline complete!"
echo "Results: classification/, assembly/"
```

## Interpreting Results

| Metric | Interpretation |
|--------|-----------------|
| % classified | % of reads assigned (higher = better) |
| Dominant taxa | Most abundant organisms |
| Diversity | Number of different taxa |
| Assembly N50 | Contig quality |

## Best Practices

✓ **Do:**
- Quality trim data first
- Classify before assembly
- Use appropriate databases
- Document parameters

✗ **Don't:**
- Over-interpret rare taxa
- Skip QC steps
- Assume assembly = real genomes

---

## 🎓 Congratulations!

✅ You've completed the full bioinformatics training!

**You now know:**
- ✅ Linux command line fundamentals
- ✅ File manipulation & organization
- ✅ Quality control (FastQC)
- ✅ Read trimming & assembly
- ✅ Genome annotation
- ✅ Metagenomics & analysis

**Ready for real projects? Start analyzing your own data! 🚀**

**Congratulations! You're now a Bioinformatician! 🧬🎉**