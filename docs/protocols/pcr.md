# PCR Protocol

## What is PCR?

**PCR (Polymerase Chain Reaction)** is a fundamental molecular biology technique used to amplify (make many copies of) specific DNA sequences. It's one of the most widely used methods in molecular biology, allowing researchers to produce millions of copies of a DNA fragment from a very small starting amount.

### Definition

PCR is an enzymatic reaction that:
1. **Denatures** double-stranded DNA into single strands (heating to ~95°C)
2. **Anneals** short DNA primers to complementary sequences on the template (cooling to ~50-65°C)
3. **Extends** the primers using DNA polymerase to synthesize new DNA strands (heating to ~72°C)

This cycle is repeated 25-35 times, resulting in exponential amplification of the target sequence.

### Why Do We Use PCR?

PCR is essential for many applications in molecular biology:

#### 1. **Amplification of DNA Sequences**
- Make many copies of a specific DNA fragment from a small amount of starting material
- Essential when you have limited template (e.g., from a single cell, ancient DNA, or low-abundance samples)
- Enables downstream applications that require larger amounts of DNA

#### 2. **DNA Cloning and Construction**
- Amplify DNA fragments for insertion into vectors
- Create DNA constructs for expression or analysis
- Generate templates for sequencing or other analyses

#### 3. **Detection and Identification**
- Detect the presence of specific DNA sequences
- Identify genes, mutations, or pathogens
- Verify constructs or transformations

#### 4. **Quantification**
- Quantitative PCR (qPCR) measures the amount of DNA/RNA in a sample
- Used for gene expression analysis, copy number variation, and more

#### 5. **Mutagenesis and Engineering**
- Introduce mutations, deletions, or insertions
- Create libraries of variants
- Engineer DNA sequences for specific purposes

#### 6. **Sequencing Preparation**
- Amplify regions of interest before sequencing
- Generate sufficient template for Sanger sequencing or next-generation sequencing

#### 7. **RNA Analysis (RT-PCR)**
- Reverse transcription PCR converts RNA to DNA, then amplifies it
- Enables analysis of RNA expression and structure

### When to Use PCR

**Use PCR when:**
- You need to amplify a specific DNA sequence
- You have limited starting material
- You need to detect the presence of a specific sequence
- You're preparing DNA for cloning, sequencing, or other applications
- You need to introduce mutations or modifications

**Consider alternatives when:**
- You already have sufficient DNA (may not need amplification)
- Working with very long sequences (>10-15 kb) - may need specialized polymerases or methods
- Need to amplify entire genomes (use whole genome amplification methods)

---

## Materials

### Reagents

- **Template DNA**: The DNA sequence you want to amplify (can be genomic DNA, plasmid, PCR product, etc.)
- **Forward Primer**: Short DNA oligonucleotide that binds to the 5' end of your target sequence
- **Reverse Primer**: Short DNA oligonucleotide that binds to the 3' end of your target sequence
- **DNA Polymerase**: Enzyme that synthesizes DNA (e.g., Taq, Q5, Phusion, Pfu)
- **dNTPs**: Deoxynucleotide triphosphates (dATP, dCTP, dGTP, dTTP) - building blocks for DNA synthesis
- **PCR Buffer**: 10x buffer provided with polymerase (contains salts, pH stabilizers)
- **Magnesium Chloride (MgCl₂)**: Often included separately, required for polymerase activity
- **Nuclease-free water**: For making up reaction volumes

### Equipment

- **Thermal cycler**: Programmable machine that cycles through temperatures
- **Micropipettes**: P2, P10, P20, P200, P1000
- **PCR tubes or 96-well plates**: For reactions
- **Ice bucket**: For keeping reagents cold
- **Centrifuge**: For spinning down reactions
- **Gel electrophoresis apparatus**: For analyzing products
- **UV transilluminator or gel imaging system**: For visualizing DNA

### Optional Reagents

- **DMSO**: Can help with difficult templates (secondary structures)
- **Betaine**: Can help with GC-rich sequences
- **BSA (Bovine Serum Albumin)**: Can stabilize reactions
- **Glycerol**: Sometimes included in reaction mixes

---

## Protocol

### Step 1: Design Primers

#### 1.1 Primer Design Principles

**Key parameters:**
- **Length**: 18-25 nucleotides (optimal)
- **Melting temperature (Tm)**: 55-65°C (both primers should have similar Tm, within 2-3°C)
- **GC content**: 40-60% (avoid extremes)
- **Avoid**: Secondary structures, primer-dimers, repetitive sequences

**Primer binding:**
- Forward primer: Binds to the 5' end of the template (same strand as coding sequence)
- Reverse primer: Binds to the 3' end of the template (complementary strand)

#### 1.2 Verify Primer Design

- Check for secondary structures using NUPACK or similar tools
- Verify no primer-dimers will form
- BLAST primers to check for off-target binding
- Calculate melting temperatures

#### 1.3 Order Primers

- Order from commercial supplier (IDT, Sigma, etc.)
- Standard desalting purification is usually sufficient
- Typical scale: 25 nmol
- Verify sequences when received

### Step 2: Prepare Primer Stocks

#### 2.1 Resuspend Primers

```bash
# Typical resuspension
# For 25 nmol scale, add 250 μL nuclease-free water
# Final concentration: ~100 μM

# Calculate volume needed:
# Volume (μL) = (nmoles × 10^6) / (desired concentration in μM)
```

#### 2.2 Create Working Stocks

- Dilute to 10 μM working concentration
- Store at -20°C for long-term storage
- Keep on ice when working

### Step 3: Prepare Template DNA

#### 3.1 Template Types

- **Genomic DNA**: Extract from cells/tissue
- **Plasmid DNA**: Mini-prep or maxi-prep
- **PCR product**: From previous PCR
- **cDNA**: From reverse transcription

#### 3.2 Template Concentration

- **Typical range**: 1 pg - 100 ng per reaction
- **Plasmid**: 0.1-10 ng
- **Genomic DNA**: 10-100 ng
- **PCR product**: 0.1-1 ng
- **Too much template**: Can cause non-specific amplification
- **Too little template**: May not amplify or give low yield

### Step 4: Set Up PCR Reaction

#### 4.1 Standard Reaction Setup (50 μL)

```python
Component              Volume      Final Concentration
─────────────────────────────────────────────────────
Template DNA           1-5 μL      Variable
Forward primer (10 μM) 1 μL        0.2 μM
Reverse primer (10 μM) 1 μL        0.2 μM
10x PCR Buffer         5 μL        1x
dNTPs (10 mM each)     1 μL        200 μM each
Polymerase             0.25-1 μL   Per manufacturer
Water                  to 50 μL
─────────────────────────────────────────────────────
Total                  50 μL
```

#### 4.2 Master Mix (For Multiple Reactions)

When running multiple reactions, prepare a master mix:

```python
# For 10 reactions (add 10% extra for pipetting error = 11 reactions)

Component              Volume per rxn  Total (11 rxns)
─────────────────────────────────────────────────────
10x PCR Buffer         5 μL           55 μL
dNTPs (10 mM each)     1 μL            11 μL
Forward primer (10 μM) 1 μL            11 μL
Reverse primer (10 μM) 1 μL            11 μL
Polymerase             0.5 μL           5.5 μL
Water                  41.5 μL          456.5 μL
─────────────────────────────────────────────────────
Subtotal               50 μL           550 μL

# Then add template to each tube:
# 45 μL master mix + 5 μL template = 50 μL total
```

**Benefits of master mix:**
- Reduces pipetting errors
- Ensures consistency across reactions
- Faster setup

### Step 5: Thermal Cycling Program

#### 5.1 Standard PCR Program

```
Step 1: Initial Denaturation
  95-98°C for 30 seconds - 2 minutes
  (Depends on polymerase and template complexity)

Step 2: Cycling (25-35 cycles)
  Denaturation:  95-98°C for 10-30 seconds
  Annealing:      50-65°C for 15-60 seconds
  Extension:      72°C for 30 seconds - 2 minutes
                  (1 minute per kb of product)

Step 3: Final Extension
  72°C for 2-10 minutes
  (Ensures all products are fully extended)

Step 4: Hold
  4-10°C hold (indefinite)
```

#### 5.2 Temperature Guidelines

**Denaturation:**
- Standard: 95°C
- High-fidelity polymerases: 98°C
- Time: 10-30 seconds (longer for complex templates)

**Annealing:**
- Start with primer Tm - 5°C
- Typical range: 55-65°C
- Can optimize by testing 2-3°C increments
- Time: 15-60 seconds

**Extension:**
- Standard: 72°C (optimal for most polymerases)
- Time: 30 seconds per 500 bp - 1 kb
- For products >1 kb: 1 minute per kb

**Number of cycles:**
- Standard: 25-35 cycles
- Fewer cycles: Less product, fewer errors
- More cycles: More product, but more errors and background

#### 5.3 Touchdown PCR (Optional)

For difficult amplifications:

```
Initial annealing: 65°C
Decrease by 0.5-1°C per cycle for 10 cycles
Then continue at final temperature for remaining cycles
```

### Step 6: Analyze Results

#### 6.1 Gel Electrophoresis

- Run 5-10 μL of PCR product on 1-2% agarose gel
- Include DNA ladder (size marker)
- Run at 5-10 V/cm
- Visualize under UV light

#### 6.2 Expected Results

- **Single band at expected size**: Success!
- **Multiple bands**: Non-specific amplification (optimize conditions)
- **No band**: No amplification (check primers, template, conditions)
- **Smear**: Degraded template or too many cycles
- **Primer dimers**: Small bands (~50-100 bp), usually at bottom of gel

#### 6.3 Quantification

- Estimate concentration by comparing to DNA ladder
- Use Nanodrop or similar for precise quantification
- Typical yields: 10-200 ng/μL

### Step 7: Purify Product (If Needed)

#### 7.1 When to Purify

- Before cloning
- Before sequencing
- Before restriction digestion
- To remove primers, dNTPs, or other reaction components

#### 7.2 Purification Methods

**PCR purification kit:**
- Removes primers, dNTPs, enzymes
- Fast and easy
- Good for most applications

**Gel extraction:**
- Removes non-specific products
- Use when you have multiple bands
- More time-consuming but higher purity

**Enzymatic cleanup:**
- Exonuclease I + Shrimp Alkaline Phosphatase
- Removes primers and dNTPs
- Fast and cheap

---

## Troubleshooting

| Issue | Possible Causes | Solutions |
|-------|----------------|----------|
| **No product** | • Wrong primers<br>• No template<br>• Wrong annealing temperature<br>• Polymerase inactive<br>• Inhibitors in template | • Check primer sequences<br>• Verify template is present<br>• Lower annealing temperature by 2-5°C<br>• Use fresh polymerase<br>• Dilute template or purify |
| **Multiple bands** | • Non-specific primer binding<br>• Too low annealing temperature<br>• Too many cycles<br>• Contaminated template | • Increase annealing temperature<br>• Redesign primers<br>• Reduce cycles<br>• Use touchdown PCR<br>• Purify template |
| **Wrong size product** | • Wrong primers<br>• Primer binding to wrong location<br>• Contamination | • Verify primer sequences<br>• BLAST primers<br>• Use fresh reagents |
| **Weak/smeared band** | • Too few cycles<br>• Degraded template<br>• Too much template<br>• Poor primer quality | • Increase cycles<br>• Use fresh template<br>• Reduce template amount<br>• Order new primers |
| **Primer dimers** | • Primers binding to each other<br>• Too much primer<br>• Too low annealing temperature | • Redesign primers<br>• Reduce primer concentration<br>• Increase annealing temperature |
| **High background** | • Too many cycles<br>• Too low annealing temperature<br>• Non-specific binding | • Reduce cycles<br>• Increase annealing temperature<br>• Use hot-start polymerase |
| **Product shorter than expected** | • Secondary structures<br>• Premature termination<br>• Degraded template | • Add DMSO (2-5%)<br>• Increase extension time<br>• Use fresh template |
| **Inconsistent results** | • Pipetting errors<br>• Temperature variations<br>• Old reagents | • Use master mix<br>• Check thermal cycler calibration<br>• Use fresh reagents |

---

## Best Practices

### Primer Design

1. **Design carefully**: Use primer design software, check for secondary structures
2. **Verify sequences**: Always double-check primer sequences before ordering
3. **Test primers**: If possible, test new primers on a known template first
4. **Keep records**: Document primer sequences and conditions that work

### Experimental Setup

1. **Use master mix**: Reduces errors and ensures consistency
2. **Keep reagents cold**: Store on ice, work quickly
3. **Use nuclease-free water**: Prevents degradation
4. **Include controls**: 
   - Positive control (known template)
   - Negative control (no template)
   - No primer control (if troubleshooting)

### Optimization

1. **Start with standard conditions**: Then optimize if needed
2. **Optimize one variable at a time**: Temperature, primer concentration, etc.
3. **Test annealing temperature**: Gradient PCR can help find optimal temperature
4. **Document conditions**: Keep notes on what works

### Quality Control

1. **Always run a gel**: Verify product size and purity
2. **Sequence verify**: For important products, always sequence
3. **Check multiple clones**: If cloning, sequence 2-3 colonies
4. **Keep records**: Document all conditions and results

### Safety

1. **Wear PPE**: Gloves, lab coat, safety glasses
2. **Handle ethidium bromide carefully**: Use alternatives when possible
3. **UV protection**: Use shield when viewing gels
4. **Dispose properly**: Follow lab waste disposal protocols

---

## Specialized PCR Types

### High-Fidelity PCR

**Use when:** Need accurate amplification (cloning, sequencing)

**Features:**
- Uses proofreading polymerases (Q5, Phusion, Pfu)
- Lower error rate
- Higher extension temperature (72°C)
- May require optimization

### Hot-Start PCR

**Use when:** Want to reduce non-specific amplification

**Features:**
- Polymerase inactive until heated
- Reduces primer-dimers and background
- Better for difficult templates

### Touchdown PCR

**Use when:** Unsure of optimal annealing temperature

**Features:**
- Starts high, decreases each cycle
- Finds optimal temperature automatically
- Good for difficult amplifications

### Quantitative PCR (qPCR)

**Use when:** Need to quantify DNA/RNA

**Features:**
- Real-time detection
- Measures fluorescence
- Requires special equipment and reagents
- Used for gene expression, copy number, etc.

### Reverse Transcription PCR (RT-PCR)

**Use when:** Working with RNA

**Features:**
- First converts RNA to DNA (reverse transcription)
- Then amplifies DNA
- Used for gene expression analysis
- Requires reverse transcriptase enzyme

---

## Applications in the Lab

PCR is used for:

1. **Amplifying DNA fragments** for cloning or analysis
2. **Verifying constructs** after cloning or assembly
3. **Preparing sequencing templates** for Sanger or NGS
4. **Introducing mutations** via site-directed mutagenesis
5. **Detecting specific sequences** in samples
6. **Quantifying gene expression** via qPCR
7. **Creating DNA libraries** for screening

---

## Expected Results

### Successful PCR

- Single, bright band at expected size on gel
- High yield (>50 ng/μL typical)
- Ready for downstream applications
- Sequence matches expected (if verified)

### Typical Yields

- **Standard PCR**: 20-200 ng/μL
- **High-fidelity PCR**: 10-100 ng/μL (may be lower)
- **Long PCR**: Variable, often lower

### Time Required

- **Reaction setup**: 15-30 minutes
- **Thermal cycling**: 1-3 hours (depending on program)
- **Gel analysis**: 30-60 minutes
- **Purification**: 15-30 minutes
- **Total**: ~2-4 hours

---

## Related Protocols

- [Primer Assembly](primer-assembly.md) - Uses PCR for assembly
- [Sample Preparation](sample-preparation.md) - Template preparation
- [Data Collection](data-collection.md) - Recording results

---

## References

- Mullis, K. B. (1990). "The unusual origin of the polymerase chain reaction." *Scientific American*.
- Saiki, R. K. et al. (1988). "Primer-directed enzymatic amplification of DNA with a thermostable DNA polymerase." *Science*.

---

*Last updated: {{ git_revision_date_localized }}*

