# Primer Assembly Protocol

## What is Primer Assembly?

**Primer assembly** (also known as **oligonucleotide assembly** or **gene synthesis by assembly**) is a molecular biology technique used to construct longer double-stranded DNA combining shorter synthetic oligonucleotides (primers) using PCR

### Definition

Primer assembly is the process of:
1. **Designing** overlapping oligonucleotide sequences that span the target DNA/RNA sequence
2. **Synthesizing** these short DNA fragments (typically 20-60 nucleotides each)
3. **Annealing** complementary overlapping regions between adjacent oligonucleotides
4. **Extending** the annealed fragments using DNA polymerase to create full-length double-stranded DNA
5. **Amplifying** the assembled product using PCR

### Why Do We Use Primer Assembly?

Primer assembly is used for several important reasons:

#### 1. **Cost-Effective Gene Construction**
- Synthesizing long DNA sequences (>200 bp) directly is expensive
- Short oligonucleotides (20-60 bp) are much cheaper to synthesize
- Assembly allows construction of genes, promoters, or regulatory elements at a fraction of the cost

#### 2. **Custom Sequence Design**
- Enables creation of sequences that don't exist in nature
- Allows introduction of specific mutations, deletions, or insertions
- Permits design of optimized sequences (codon optimization, regulatory elements)

#### 3. **Rapid Prototyping**
- Faster than traditional cloning methods for new constructs
- Can test multiple sequence variants quickly
- Enables iterative design and testing cycles

#### 4. **Precision and Control**
- Exact control over every nucleotide in the sequence
- Can introduce specific modifications (mutations, tags, linkers) precisely
- Avoids issues with restriction sites or unwanted sequences from traditional cloning

#### 5. **Building Complex Constructs**
- Assemble multiple functional elements (promoters, coding sequences, terminators)
- Create libraries of related sequences with systematic variations
- Construct chimeric sequences combining elements from different sources

#### 6. **RNA Structure Studies**
- For RNA research, primer assembly allows construction of RNA sequences with specific structural features
- Can introduce modified nucleotides or specific sequences for structure-function studies
- Enables creation of RNA libraries for high-throughput screening

### When to Use Primer Assembly

**Use primer assembly when:**
- Constructing sequences longer than ~200 bp
- Need precise control over sequence
- Creating sequences that don't exist naturally
- Building multiple related variants
- Cost is a consideration (cheaper than full gene synthesis)
- Need to introduce specific mutations or modifications

**Consider alternatives when:**
- Sequence already exists in a plasmid (use PCR or restriction cloning)
- Very short sequences (<100 bp) - direct synthesis may be simpler
- Need very long sequences (>3 kb) - may need hierarchical assembly or commercial synthesis

---

## Materials

### Reagents

- **Oligonucleotides**: Overlapping primers designed for assembly (typically 20-60 nucleotides each, 15-20 bp overlaps)
- **DNA Polymerase**: High-fidelity polymerase (e.g., Q5, Phusion, or Pfu)
- **dNTPs**: Deoxynucleotide triphosphates (dATP, dCTP, dGTP, dTTP)
- **PCR Buffer**: 10x buffer appropriate for your polymerase
- **Nuclease-free water**: For dilutions and reactions
- **Agarose**: For gel electrophoresis
- **DNA ladder**: Molecular weight marker
- **Gel loading dye**: 6x loading buffer
- **Ethidium bromide or alternative DNA stain**: For visualization

### Equipment

- **Thermal cycler**: For PCR reactions
- **Gel electrophoresis apparatus**: For analyzing products
- **UV transilluminator or gel imaging system**: For visualizing DNA
- **Micropipettes**: P10, P20, P200, P1000
- **PCR tubes or 96-well plates**: For reactions
- **Ice bucket**: For keeping reagents cold
- **Centrifuge**: For spinning down reactions

### Software/Tools

- **Primer design software**: 
  - NUPACK (for secondary structure prediction)
  - Primer3 (for primer design)
  - Custom scripts for overlap design
- **Sequence analysis tools**: 
  - BLAST (for checking sequences)
  - Sequence alignment tools

---

## Protocol

### Step 1: Design Overlapping Primers

#### 1.1 Determine Target Sequence

- Define the complete sequence you want to assemble
- Include any modifications, tags, or mutations
- Verify sequence is correct (check for errors, unwanted sequences)

#### 1.2 Design Overlapping Oligonucleotides

**Design parameters:**
- **Length**: 40-60 nucleotides per oligonucleotide (optimal)
- **Overlap**: 15-20 base pairs between adjacent oligonucleotides
- **Melting temperature (Tm)**: Aim for 55-65°C for overlaps
- **Avoid**: Secondary structures, repetitive sequences, homopolymers

**Example design:**
```
Target: 200 bp sequence

Oligo 1:  [1-50]     (50 bp)
Oligo 2:  [35-85]    (50 bp, overlaps oligo 1 by 15 bp)
Oligo 3:  [70-120]   (50 bp, overlaps oligo 2 by 15 bp)
Oligo 4:  [105-155]  (50 bp, overlaps oligo 3 by 15 bp)
Oligo 5:  [140-190]  (50 bp, overlaps oligo 4 by 15 bp)
Oligo 6:  [175-200]  (25 bp, overlaps oligo 5 by 15 bp)
```

#### 1.3 Add Outer Primers

- Design forward and reverse primers that bind to the 5' and 3' ends
- These will be used for final PCR amplification
- Include restriction sites, tags, or other modifications if needed

#### 1.4 Verify Primer Design

- Check for secondary structures using NUPACK or similar
- Verify no primer-dimers will form
- BLAST primers to check for off-target binding
- Calculate melting temperatures

### Step 2: Order Oligonucleotides

- Order from commercial supplier (IDT, Sigma, etc.)
- Specify synthesis scale (typically 25 nmol is sufficient)
- Request standard desalting purification (usually sufficient)
- Verify sequences when received

### Step 3: Prepare Oligonucleotide Stocks

#### 3.1 Resuspend Oligonucleotides

```bash
# Typical resuspension
# For 25 nmol scale, add 250 μL nuclease-free water
# Final concentration: ~100 μM

# Calculate volume needed:
# Volume (μL) = (nmoles × 10^6) / (desired concentration in μM)
```

#### 3.2 Dilute to Working Concentration

- Create 10 μM working stocks for assembly reactions
- Store at -20°C for long-term storage
- Keep on ice when working

### Step 4: Assembly PCR

#### 4.1 Set Up Assembly Reaction

**Reaction setup (50 μL total volume):**

```python
# Typical reaction mix:
# - 1-2 μL of each oligonucleotide (10 μM stock)
# - 1x PCR buffer
# - 200 μM each dNTP
# - 0.02 U/μL DNA polymerase
# - Nuclease-free water to 50 μL

# Example for 6 oligonucleotides:
Component              Volume
─────────────────────────────────
Oligo 1 (10 μM)        1 μL
Oligo 2 (10 μM)        1 μL
Oligo 3 (10 μM)        1 μL
Oligo 4 (10 μM)        1 μL
Oligo 5 (10 μM)        1 μL
Oligo 6 (10 μM)        1 μL
10x PCR Buffer         5 μL
dNTPs (10 mM each)     1 μL
Polymerase             0.1 μL (or per manufacturer)
Water                  38.9 μL
─────────────────────────────────
Total                  50 μL
```

#### 4.2 Thermal Cycling Program

**Typical program:**

```
Step 1: Initial denaturation
  98°C for 30 seconds

Step 2: Annealing and extension (5-10 cycles)
  98°C for 10 seconds    (denaturation)
  55-60°C for 30 seconds (annealing - adjust based on Tm)
  72°C for 30-60 seconds (extension - 1 min per kb)

Step 3: Final extension
  72°C for 2-5 minutes

Step 4: Hold
  4°C hold
```

**Notes:**
- Annealing temperature should be 5-10°C below lowest overlap Tm
- Extension time: ~30 seconds per 500 bp
- Number of cycles: Start with 5-10, can increase if needed

### Step 5: Amplification PCR

#### 5.1 Set Up Amplification Reaction

Use outer primers to amplify the assembled product:

```python
Component              Volume
─────────────────────────────────
Assembly product       1-5 μL (from Step 4)
Forward primer (10 μM)  1 μL
Reverse primer (10 μM)  1 μL
10x PCR Buffer          5 μL
dNTPs (10 mM each)      1 μL
Polymerase             0.1 μL
Water                  to 50 μL
─────────────────────────────────
Total                  50 μL
```

#### 5.2 Thermal Cycling Program

```
Step 1: Initial denaturation
  98°C for 30 seconds

Step 2: Amplification (25-35 cycles)
  98°C for 10 seconds
  55-65°C for 20 seconds (primer Tm - 5°C)
  72°C for 30-60 seconds (1 min per kb)

Step 3: Final extension
  72°C for 2-5 minutes

Step 4: Hold
  4°C hold
```

### Step 6: Analyze Products

#### 6.1 Gel Electrophoresis

- Run 5-10 μL of PCR product on 1-2% agarose gel
- Include DNA ladder
- Run at appropriate voltage (5-10 V/cm)
- Visualize under UV light

#### 6.2 Expected Results

- **Assembly PCR**: May show faint or multiple bands
- **Amplification PCR**: Should show single band at expected size
- If multiple bands: Optimize conditions or gel-purify correct band

### Step 7: Purify and Verify

#### 7.1 Purify PCR Product

- Use PCR purification kit or gel extraction
- Elute in appropriate volume (typically 30-50 μL)
- Quantify using Nanodrop or similar

#### 7.2 Verify Sequence

- **Option 1**: Sanger sequencing
  - Send purified product for sequencing
  - Verify sequence matches design
  
- **Option 2**: Restriction digest
  - If designed with restriction sites, digest and check on gel
  
- **Option 3**: Clone and sequence
  - Clone into vector, pick colonies, sequence

---

## Troubleshooting

| Issue | Possible Causes | Solutions |
|-------|----------------|----------|
| No product in assembly PCR | • Oligonucleotides not annealing<br>• Too few cycles<br>• Wrong annealing temperature | • Check primer design and overlaps<br>• Increase cycles to 10-15<br>• Lower annealing temperature by 2-5°C |
| Multiple bands in amplification | • Non-specific amplification<br>• Primer dimers<br>• Contamination | • Increase annealing temperature<br>• Redesign primers<br>• Use touchdown PCR<br>• Gel-purify correct band |
| Product shorter than expected | • Incomplete assembly<br>• Secondary structures blocking extension | • Increase extension time<br>• Add DMSO (2-5%) or betaine<br>• Redesign primers to avoid secondary structures |
| Product longer than expected | • Primer dimers<br>• Non-specific amplification | • Increase annealing temperature<br>• Redesign primers<br>• Use hot-start polymerase |
| Low yield | • Too few cycles<br>• Suboptimal conditions<br>• Degraded reagents | • Increase cycles<br>• Optimize temperature<br>• Use fresh reagents |
| Sequence errors | • Synthesis errors in oligonucleotides<br>• Polymerase errors | • Order from reputable supplier<br>• Use high-fidelity polymerase<br>• Sequence multiple clones |

---

## Best Practices

### Design

1. **Verify sequences carefully** before ordering oligonucleotides
2. **Check for secondary structures** that might interfere with assembly
3. **Design overlaps** with appropriate Tm (55-65°C)
4. **Avoid repetitive sequences** or homopolymers in overlap regions

### Experimental

1. **Use high-fidelity polymerase** to minimize errors
2. **Keep oligonucleotides on ice** when working
3. **Use nuclease-free water** and clean pipettes
4. **Include negative controls** (no template, no polymerase)
5. **Optimize conditions** for your specific sequence

### Quality Control

1. **Always sequence verify** the final product
2. **Check multiple clones** if cloning (at least 2-3)
3. **Document all modifications** and deviations from protocol
4. **Keep records** of primer sequences and conditions used

---

## Expected Results

### Successful Assembly

- Single band of correct size on gel
- Sequence matches design (100% identity)
- High yield (>100 ng/μL after purification)
- Ready for downstream applications (cloning, etc.)

### Typical Yields

- Assembly PCR: Variable, often low yield
- Amplification PCR: 50-200 ng/μL typical
- After purification: 20-100 ng/μL

### Time Required

- Primer design: 1-2 hours
- Oligonucleotide ordering: 1-3 days (shipping)
- Assembly and amplification: 1 day
- Verification: 1-3 days (sequencing)
- **Total: ~1 week** (depending on sequencing turnaround)

---

## Applications in the Lab

Primer assembly is commonly used for:

1. **RNA Construct Design**: Creating RNA sequences with specific structural features
2. **Mutagenesis**: Introducing specific mutations for structure-function studies
3. **Library Construction**: Building libraries of related sequences
4. **Chimeric Constructs**: Combining elements from different RNAs
5. **Optimization**: Creating codon-optimized or structure-optimized sequences

---

## Related Protocols

- [Sample Preparation](sample-preparation.md)
- [Data Collection](data-collection.md)

## References

- Gibson et al. (2009). "Enzymatic assembly of DNA molecules up to several hundred kilobases." *Nature Methods*.
- Stemmer et al. (1995). "Single-step assembly of a gene and entire plasmid from large numbers of oligodeoxyribonucleotides." *Gene*.

---

*Last updated: {{ git_revision_date_localized }}*

