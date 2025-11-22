# Vienna

**Category**: RNA Secondary Structure Prediction  
**Language**: Python  
**Version**: 0.8.0  
**Author**: Joe Yesselman

## Overview

Vienna is a Python wrapper for ViennaRNA tools, providing an easy-to-use interface for RNA secondary structure prediction, folding, and sequence design. This package simplifies working with ViennaRNA in Python and is particularly useful for RNA structure analysis in computational biology.

### Key Features

- **RNA Folding**: Predict secondary structures and minimum free energies
- **Base Pair Probabilities**: Calculate ensemble properties
- **Cofolding**: Predict interactions between two RNA sequences
- **Inverse Folding**: Design sequences that fold into specific structures
- **Structure Validation**: Check if sequences fold to target structures

---

## Installation

### Installation in Jupyter Notebooks

#### Method 1: Using Conda (Recommended for Jupyter)

The easiest way to install Vienna in a Jupyter environment is using conda, which handles both ViennaRNA and the Python package:

```bash
# Create a new conda environment with ViennaRNA
conda create -n vienna-env -c bioconda viennarna python=3.10 jupyter

# Activate the environment
conda activate vienna-env

# Install the vienna package
pip install vienna

# Install Jupyter if not already installed
conda install jupyter

# Launch Jupyter
jupyter notebook
# or
jupyter lab
```

#### Method 2: Install in Existing Jupyter Environment

If you already have a Jupyter environment set up:

```bash
# First, install ViennaRNA (required dependency)
conda install -c bioconda viennarna

# Then install the Python package
pip install vienna
```

#### Method 3: Using pip (Requires ViennaRNA Pre-installed)

```bash
# Install ViennaRNA first (using conda is recommended)
conda install -c bioconda viennarna

# Install the Python package
pip install vienna
```

#### Method 4: Install from Source

```bash
# Clone the repository
git clone https://github.com/jyesselm/vienna
cd vienna

# Install ViennaRNA first
conda install -c bioconda viennarna

# Install the package
pip install .
```

### Verify Installation in Jupyter

After installation, verify it works in a Jupyter notebook:

```python
import vienna

# Test basic folding
result = vienna.fold('GGGGAAAACCCC')
print(f"Structure: {result.dot_bracket}")
print(f"Energy: {result.mfe} kcal/mol")
```

---

## Basic Usage

### Importing the Package

```python
import vienna
```

### Simple RNA Folding

The most basic usage is folding a single RNA sequence:

```python
# Fold a simple hairpin sequence
sequence = "GGGGAAAACCCC"
result = vienna.fold(sequence)

# Access results
print(f"Sequence: {sequence}")
print(f"Structure: {result.dot_bracket}")      # Secondary structure in dot-bracket notation
print(f"Energy: {result.mfe} kcal/mol")        # Minimum free energy
print(f"Ensemble Diversity: {result.ens_defect}")  # Ensemble diversity metric
```

**Output:**
```
Sequence: GGGGAAAACCCC
Structure: ((((....))))
Energy: -5.40 kcal/mol
Ensemble Diversity: 1.62
```

### Getting Just the Structure

If you only need the secondary structure:

```python
structure = vienna.folded_structure('GGGGAAAACCCC')
print(structure)  # '((((....))))'
```

---

## Advanced Examples

### Example 1: Folding with Base Pair Probabilities

Calculate base pair probabilities for detailed structural analysis:

```python
# Fold with base pair probabilities
result = vienna.fold('GGGGAAAACCCC', bp_probs=True)

print(f"Structure: {result.dot_bracket}")
print(f"Energy: {result.mfe} kcal/mol")
print(f"\nBase Pair Probabilities:")
print(f"Total base pairs found: {len(result.bp_probs)}")

# Display high-probability base pairs
for bp in result.bp_probs:
    i, j, prob = bp
    if prob > 0.5:  # Only show pairs with >50% probability
        print(f"  Position {i}-{j}: probability = {prob:.3f}")
```

### Example 2: Analyzing Multiple Sequences

Compare folding of different sequences:

```python
sequences = [
    "GGGGAAAACCCC",                    # Simple hairpin
    "AUGCGUACGUACGUACGUA",            # Random sequence
    "GGGGAAAACCCC" * 2,                # Longer hairpin
]

results = []
for seq in sequences:
    result = vienna.fold(seq)
    results.append({
        'sequence': seq,
        'structure': result.dot_bracket,
        'energy': result.mfe,
        'diversity': result.ens_defect
    })
    print(f"\nSequence: {seq[:30]}..." if len(seq) > 30 else f"\nSequence: {seq}")
    print(f"  Structure: {result.dot_bracket}")
    print(f"  Energy: {result.mfe:.2f} kcal/mol")
    print(f"  Ensemble Diversity: {result.ens_defect:.2f}")
```

### Example 3: Cofolding Two Sequences

Predict how two RNA sequences interact:

```python
# Separate sequences with '&'
seq1 = "GGGG"
seq2 = "CCCC"
combined = f"{seq1}&{seq2}"

result = vienna.cofold(combined)

print(f"Sequence 1: {seq1}")
print(f"Sequence 2: {seq2}")
print(f"Combined structure: {result.dot_bracket}")
print(f"Combined energy: {result.mfe} kcal/mol")
print(f"Ensemble diversity: {result.ens_defect}")
```

**Output:**
```
Sequence 1: GGGG
Sequence 2: CCCC
Combined structure: ((((&))))
Combined energy: -4.40 kcal/mol
Ensemble diversity: 0.00
```

### Example 4: Inverse Folding - Design Sequences

Design RNA sequences that fold into a specific structure:

```python
# Target structure
target_structure = "(((.(((....))).)))"

# Sequence constraints (N = any nucleotide, lowercase = specific base)
constraint = "NNNgNNNNNNNNNNaNNN"

# Generate multiple solutions
results = vienna.inverse_fold(target_structure, constraint, n_sol=10)

print(f"Target structure: {target_structure}")
print(f"Found {len(results)} sequences:\n")

for i, seq_score in enumerate(results, 1):
    print(f"{i}. Sequence: {seq_score.seq}")
    print(f"   Score (MFE): {seq_score.score:.2f} kcal/mol")
    
    # Verify it folds to target
    actual = vienna.folded_structure(seq_score.seq)
    matches = "✓" if actual == target_structure else "✗"
    print(f"   Folds to target: {matches} ({actual})")
    print()
```

### Example 5: Validating Structure Folding

Check if a sequence folds into a desired structure:

```python
sequence = 'GGGGAAAACCCC'
target = '((((....))))'

if vienna.does_sequence_fold_to(sequence, target):
    print("✓ Sequence folds to target structure!")
    result = vienna.fold(sequence)
    print(f"  Structure: {result.dot_bracket}")
    print(f"  Energy: {result.mfe} kcal/mol")
else:
    print("✗ Sequence does not fold to target structure")
    actual = vienna.folded_structure(sequence)
    print(f"  Actual structure: {actual}")
    print(f"  Target structure: {target}")
```

### Example 6: Analyzing tRNA-like Sequences

Work with longer, more complex sequences:

```python
# tRNA-like sequence
tRNA_seq = 'GGGGAUAUAGCUCAGUUGGUAGAGCGCUGCCUUUGCACGGCAGAUGUCAGAGGUUCGAUUCUCUGUUAUCCCC'

result = vienna.fold(tRNA_seq, bp_probs=True)

print(f"Sequence length: {len(tRNA_seq)} nucleotides")
print(f"Structure:\n{result.dot_bracket}")
print(f"Energy: {result.mfe:.2f} kcal/mol")
print(f"Ensemble diversity: {result.ens_defect:.2f}")

# Find highly probable base pairs
high_prob_pairs = [bp for bp in result.bp_probs if bp[2] > 0.9]
print(f"\nHighly probable base pairs (>90%): {len(high_prob_pairs)}")

for bp in high_prob_pairs[:10]:  # Show first 10
    i, j, prob = bp
    print(f"  {i}-{j}: {prob:.3f}")
```

### Example 7: Batch Processing Multiple Sequences

Process multiple sequences efficiently:

```python
# List of sequences to analyze
sequences = [
    "GGGGAAAACCCC",
    "AUGCGUACGUACGUACGUA",
    "UUUAAAAGGGCCC",
    "CCCCGGGGAAAATTTT",
]

# Process all sequences
results = []
for seq in sequences:
    result = vienna.fold(seq, bp_probs=True)
    results.append({
        'sequence': seq,
        'structure': result.dot_bracket,
        'energy': result.mfe,
        'diversity': result.ens_defect,
        'num_bp': len([bp for bp in result.bp_probs if bp[2] > 0.5])
    })

# Display summary
print("Folding Results Summary:")
print("-" * 60)
for r in results:
    print(f"\nSequence: {r['sequence']}")
    print(f"  Structure: {r['structure']}")
    print(f"  Energy: {r['energy']:.2f} kcal/mol")
    print(f"  High-probability base pairs: {r['num_bp']}")
```

### Example 8: Energy vs Sequence Length Analysis

Analyze how folding energy changes with sequence length:

```python
import matplotlib.pyplot as plt
import numpy as np

# Generate sequences of different lengths
lengths = [10, 20, 30, 40, 50, 60]
energies = []
diversities = []

for length in lengths:
    # Create a simple repeating sequence
    seq = "GGGGAAAACCCC" * (length // 12 + 1)
    seq = seq[:length]
    
    result = vienna.fold(seq)
    energies.append(result.mfe)
    diversities.append(result.ens_defect)
    print(f"Length {length:2d}: Energy = {result.mfe:.2f} kcal/mol, Diversity = {result.ens_defect:.2f}")

# Plot results
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(12, 4))

ax1.plot(lengths, energies, 'o-', linewidth=2, markersize=8)
ax1.set_xlabel('Sequence Length (nt)')
ax1.set_ylabel('Minimum Free Energy (kcal/mol)')
ax1.set_title('Folding Energy vs Sequence Length')
ax1.grid(True, alpha=0.3)

ax2.plot(lengths, diversities, 's-', linewidth=2, markersize=8, color='orange')
ax2.set_xlabel('Sequence Length (nt)')
ax2.set_ylabel('Ensemble Diversity')
ax2.set_title('Ensemble Diversity vs Sequence Length')
ax2.grid(True, alpha=0.3)

plt.tight_layout()
plt.show()
```

### Example 9: Structure Visualization Helper

Create a helper function to visualize structures:

```python
def visualize_structure(sequence, structure):
    """Visualize RNA structure with base pairing information"""
    print("Sequence:", sequence)
    print("Structure:", structure)
    print("\nBase Pairing:")
    
    # Find base pairs from dot-bracket notation
    pairs = []
    stack = []
    for i, char in enumerate(structure):
        if char == "(":
            stack.append(i)
        elif char == ")":
            if stack:
                j = stack.pop()
                pairs.append((j, i))
    
    # Sort pairs by position
    pairs.sort()
    
    for i, j in pairs:
        print(f"  {sequence[i]} (pos {i+1}) pairs with {sequence[j]} (pos {j+1})")
    
    return pairs

# Example usage
seq = "GGGGAAAACCCC"
result = vienna.fold(seq)
pairs = visualize_structure(seq, result.dot_bracket)
```

### Example 10: Comparing Structures

Compare predicted structures for similar sequences:

```python
# Similar sequences with slight variations
sequences = {
    "Original": "GGGGAAAACCCC",
    "Mutated 1": "GGGGAAGACCCC",  # Single mutation
    "Mutated 2": "GGGGAAACCCCC",  # Different mutation
}

results = {}
for name, seq in sequences.items():
    result = vienna.fold(seq)
    results[name] = {
        'sequence': seq,
        'structure': result.dot_bracket,
        'energy': result.mfe
    }

# Compare
print("Structure Comparison:")
print("=" * 60)
for name, data in results.items():
    print(f"\n{name}:")
    print(f"  Sequence: {data['sequence']}")
    print(f"  Structure: {data['structure']}")
    print(f"  Energy: {data['energy']:.2f} kcal/mol")

# Check if structures are the same
structures = [r['structure'] for r in results.values()]
if len(set(structures)) == 1:
    print("\n✓ All sequences fold to the same structure")
else:
    print("\n✗ Sequences fold to different structures")
```

---

## Understanding the Results

### FoldResults Object

The `fold()` function returns a `FoldResults` object with the following attributes:

- **`dot_bracket`** (str): Secondary structure in dot-bracket notation
  - `(` = opening base pair
  - `)` = closing base pair
  - `.` = unpaired base
  - `&` = separator (in cofolding results)

- **`mfe`** (float): Minimum free energy in kcal/mol (more negative = more stable)

- **`ens_defect`** (float): Ensemble diversity metric (mean pairwise Hamming distance)

- **`bp_probs`** (list): List of base pair probabilities `[i, j, probability]`
  - Only populated if `bp_probs=True` in `fold()`
  - `i, j` are 1-indexed positions
  - `probability` ranges from 0.0 to 1.0

### InverseResults Object

The `inverse_fold()` function returns an `InverseResults` object containing:

- **`seq_scores`** (list): List of `SeqScore` objects, each with:
  - `seq` (str): Generated sequence
  - `score` (float): Minimum free energy of the sequence

---

## Best Practices

### 1. Use Base Pair Probabilities for Detailed Analysis

```python
# For detailed structural analysis, always use bp_probs=True
result = vienna.fold(sequence, bp_probs=True)

# Filter for high-confidence base pairs
high_confidence = [bp for bp in result.bp_probs if bp[2] > 0.8]
```

### 2. Validate Inverse Folding Results

```python
# Always verify that designed sequences fold to target
target = "((((....))))"
results = vienna.inverse_fold(target, "NNNNNNNNNNNN", n_sol=5)

for seq_score in results:
    actual = vienna.folded_structure(seq_score.seq)
    if actual == target:
        print(f"✓ {seq_score.seq} folds correctly")
    else:
        print(f"✗ {seq_score.seq} folds to {actual} instead")
```

### 3. Handle Long Sequences Efficiently

```python
# For very long sequences, base pair probabilities can be slow
# Only use if needed
long_seq = "A" * 1000

# Fast: just get structure and energy
result_fast = vienna.fold(long_seq)

# Slower: includes base pair probabilities
result_slow = vienna.fold(long_seq, bp_probs=True)
```

### 4. Error Handling

```python
try:
    result = vienna.fold(sequence)
except ValueError as e:
    print(f"Error: {e}")
    # Handle empty sequences, invalid characters, etc.
```

---

## Common Issues and Solutions

### Issue 1: ViennaRNA Not Found

**Problem**: `ImportError` or `RuntimeError` about ViennaRNA not being available

**Solution**:
```bash
# Install ViennaRNA using conda
conda install -c bioconda viennarna
```

### Issue 2: RNAinverse Not Available

**Problem**: `RuntimeError: RNAinverse command-line tool not available in PATH`

**Solution**:
```bash
# Ensure ViennaRNA is properly installed
conda install -c bioconda viennarna

# Verify RNAinverse is available
which RNAinverse
```

### Issue 3: Empty Sequence Error

**Problem**: `ValueError: Must supply a sequence longer than 0`

**Solution**: Always check sequence length before folding:
```python
if len(sequence) > 0:
    result = vienna.fold(sequence)
else:
    print("Error: Empty sequence")
```

### Issue 4: Invalid Characters in Sequence

**Problem**: Sequences should only contain A, U, G, C (or T for DNA)

**Solution**: Clean sequences before folding:
```python
# Remove invalid characters
valid_bases = set('AUCG')
cleaned = ''.join(c for c in sequence.upper() if c in valid_bases)
result = vienna.fold(cleaned)
```

---

## Resources

- **GitHub Repository**: [https://github.com/jyesselm/vienna](https://github.com/jyesselm/vienna)
- **PyPI Package**: [https://pypi.org/project/vienna/](https://pypi.org/project/vienna/)
- **ViennaRNA Documentation**: [https://www.tbi.univie.ac.at/RNA/](https://www.tbi.univie.ac.at/RNA/)
- **Example Notebooks**: See the `notebooks/` directory in the repository

## Related Software

- [Other Lab Software](index.md)

---

*Last updated: {{ git_revision_date_localized }}*

