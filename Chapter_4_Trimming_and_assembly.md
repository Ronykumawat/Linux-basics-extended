# Chapter 4: Trimming and Genome Assembly
![DNA Icon](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/DNA_Icon.svg/100px-DNA_Icon.svg.png)

Trimming removes low-quality bases and adapters. Assembly reconstructs complete genomes from sequencing reads.

## Part 1: Quality Trimming

### fastp (Recommended - Fast & Simple)

```bash
mamba create -n trim -c bioconda fastp
mamba activate trim
```

**Single-end reads:**
```bash
fastp -i input.fastq -o output.fastq
```

**Paired-end reads:**
```bash
fastp -i read1.fastq -I read2.fastq -o out1.fastq -O out2.fastq
```

**Advanced with quality control:**
```bash
fastp -i read1.fastq -I read2.fastq \
      -o out1.fastq -O out2.fastq \
      -q 20 -l 50 -w 8 -h report.html
```

Parameters:
- `-q 20`: Quality threshold (Phred 20)
- `-l 50`: Minimum length to keep
- `-w 8`: 8 parallel threads
- `-h`: Generate HTML report

### Trim Galore! (Alternative)

```bash
mamba create -n trim -c bioconda trim-galore

# Single-end
trim_galore input.fastq

# Paired-end
trim_galore --paired read1.fastq read2.fastq
```

## Part 2: Genome Assembly

### SPAdes (Best for Bacterial Genomes)

```bash
mamba create -n spades -c bioconda spades
```

**Basic paired-end assembly:**
```bash
spades.py -1 read1.fastq -2 read2.fastq -t 8 -m 32 -o assembly_out/
```

**With quality control (recommended):**
```bash
spades.py -1 read1.fastq -2 read2.fastq \
          -t 16 -m 64 -o out/ --careful
```

Parameters:
- `-t 16`: Use 16 threads
- `-m 64`: Use 64GB memory
- `--careful`: Extra quality checks

### MEGAHIT (Large Genomes/Metagenomes)

```bash
mamba create -n megahit -c bioconda megahit
```

```bash
# Fast large genome assembly
megahit -1 read1.fastq -2 read2.fastq -o output/ -t 16 -m 0.9
```

## Part 3: Quality Assessment (QUAST)

```bash
mamba create -n quast -c bioconda quast
```

**Assess assembly quality:**
```bash
# Basic
quast.py assembly.fasta -o results/

# With reference
quast.py assembly.fasta -r reference.fasta -o results/

# Compare multiple assemblies
quast.py assembly1.fasta assembly2.fasta -o comparison/
```

## Key Assembly Metrics

| Metric | Meaning | Good Value |
|--------|---------|------------|
| **N50** | Length where 50% of assembly is in contigs ≥ N50 | Depends on genome |
| **Number of contigs** | Fragment count | Fewer = better |
| **Total length** | Assembled size | ~Expected genome size |
| **L50** | Number of contigs ≥ N50 | Lower = better |
| **GC %** | Guanine + Cytosine ratio | Match expected organism |

## Complete Pipeline Script

```bash
#!/bin/bash
SAMPLE="sample_name"
READ1="${SAMPLE}_R1.fastq"
READ2="${SAMPLE}_R2.fastq"
THREADS=8

echo "Starting assembly pipeline..."

# Step 1: Trim
echo "Step 1: Trimming with fastp..."
mkdir -p trimmed
fastp -i "$READ1" -I "$READ2" \
      -o trimmed/${SAMPLE}_R1_trimmed.fastq \
      -O trimmed/${SAMPLE}_R2_trimmed.fastq \
      -q 20 -l 50 -w $THREADS

# Step 2: Assemble
echo "Step 2: Assembling with SPAdes..."
mkdir -p assembly
spades.py -1 trimmed/${SAMPLE}_R1_trimmed.fastq \
          -2 trimmed/${SAMPLE}_R2_trimmed.fastq \
          -t $THREADS -m 64 -o assembly/${SAMPLE}/ --careful

# Step 3: QC
echo "Step 3: Quality assessment with QUAST..."
mkdir -p qc
quast.py assembly/${SAMPLE}/contigs.fasta -o qc/${SAMPLE}/

echo "Pipeline complete!"
echo "Assembly: assembly/${SAMPLE}/contigs.fasta"
echo "Report: qc/${SAMPLE}/report.html"
```

## Troubleshooting

**Not enough memory:**
```bash
# Reduce k-mer range
megahit -1 read1.fastq -2 read2.fastq -k 21,33,55 -o output/
```

**Too many contigs (fragmented):**
```bash
# Try more stringent parameters
spades.py -1 r1.fq -2 r2.fq -t 16 -m 128 --careful -k 21,33,55,77,99,127
```

**Low N50:**
- Check coverage depth
- Verify data quality with FastQC
- Try different assembler

You're ready to process and assemble genomes!