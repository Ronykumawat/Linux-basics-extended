# Chapter 5: Genome Annotation
![Gene Icon](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9e/Gene_icon.svg/100px-Gene_icon.svg.png)

Annotation identifies and labels genes and functional regions in genome sequences.

## What is Annotation?

Annotation involves:
- **Gene Prediction**: Finding open reading frames (ORFs)
- **Functional Assignment**: Determining what genes do
- **Feature Detection**: Identifying promoters, tRNA, rRNA
- **Quality Assessment**: Validating predictions

## Tool: Prokka (Best for Bacteria)

Prokka is the fastest and most reliable prokaryotic genome annotator.

### Installation

```bash
mamba create -n prokka -c bioconda prokka
mamba activate prokka
prokka --version
```

### Basic Annotation

**Simple command:**
```bash
prokka assembly.fasta --outdir results/
```

**With organism information:**
```bash
prokka assembly.fasta --outdir results/ \
       --organism "Escherichia coli" \
       --strain K-12 \
       --cpus 8
```

**Full parameters:**
```bash
prokka assembly.fasta \
  --outdir results/ \
  --kingdom Bacteria \
  --genus Salmonella \
  --species enterica \
  --strain LT2 \
  --cpus 8 \
  --usegenus  # Use genus-specific databases
```

### Understanding Output Files

| File Extension | Content |
|---|---|
| `.gff` | General Feature Format (all genomic features) |
| `.gbk` | GenBank format (for NCBI submission) |
| `.faa` | FASTA protein sequences |
| `.fna` | FASTA nucleotide gene sequences |
| `.txt` | Statistics summary |
| `.tsv` | Tab-separated values (features) |

## Extracting Gene Information

```bash
# Count total genes
grep "CDS" prokka.gff | wc -l

# Extract tRNA genes
grep "tRNA" prokka.gff | wc -l

# Extract rRNA genes
grep "rRNA" prokka.gff | wc -l

# Count hypothetical proteins
grep "hypothetical" prokka.gff | wc -l

# Calculate percentage hypothetical
HYP=$(grep -c "hypothetical" prokka.gff)
TOT=$(grep -c "CDS" prokka.gff)
echo "scale=2; $HYP * 100 / $TOT" | bc
```

## Tool: AMRFinder (Antimicrobial Resistance)

Identify antimicrobial resistance genes.

```bash
mamba create -n amr -c bioconda ncbi-amrfinderplus
mamba activate amr
amrfinder --update  # Download latest databases

# Find AMR genes in proteins
amrfinder --protein prokka_out/PROKKA_*.faa \
          --output amr_results.tsv

# Or in nucleotides
amrfinder --nucleotide assembly.fasta \
          --output amr_nucleotide.tsv
```

## Complete Pipeline

```bash
#!/bin/bash
ASSEMBLY="assembly.fasta"
SAMPLE="sample_name"
THREADS=8

echo "Starting annotation pipeline..."

# Step 1: Annotate with Prokka
echo "Annotating with Prokka..."
mkdir -p annotation
prokka "$ASSEMBLY" \
  --outdir annotation/prokka_${SAMPLE}/ \
  --organism "Unknown bacterium" \
  --cpus $THREADS

# Step 2: Find AMR genes
echo "Finding AMR genes..."
mkdir -p amr
PROTEINS="annotation/prokka_${SAMPLE}/PROKKA_*.faa"
amrfinder --protein $PROTEINS \
          --output amr/${SAMPLE}_amr.tsv

# Step 3: Generate report
echo "Generating summary..."
echo "Annotation Summary for $SAMPLE" > ${SAMPLE}_summary.txt
echo "=============================" >> ${SAMPLE}_summary.txt
echo "" >> ${SAMPLE}_summary.txt
cat annotation/prokka_${SAMPLE}/PROKKA_*.txt >> ${SAMPLE}_summary.txt

echo "Pipeline complete!"
echo "Results in annotation/ and amr/ directories"
```

## Interpreting Results

Expected values:
- Bacterial genome: 1,500-5,000 genes
- Hypothetical proteins: 20-40%
- GC%: 30-70% (species dependent)

| Finding | Interpretation |
|---------|-----------------|
| Few genes (<500) | Check assembly quality, may be contaminated |
| High hypothetical (>60%) | Common for novel species |
| No rRNA/tRNA | May be filtered during assembly |
| AMR genes present | Antibiotic resistance identified |

## Best Practices

✓ **Do:**
- Use high-quality assemblies
- Provide organism info if known
- Check for contamination
- Validate with reference if available

✗ **Don't:**
- Annotate low-quality assemblies
- Ignore hypothetical proteins
- Skip manual validation

You're ready to annotate genomes!