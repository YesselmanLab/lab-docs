# Jupyter Guide

Jupyter is an open-source web application for creating and sharing documents that contain live code, equations, visualizations, and narrative text. It's essential for data science, research, and interactive computing.

---

## What is Jupyter?

Jupyter provides:
- **Interactive notebooks**: Combine code, output, and documentation
- **Multiple languages**: Python, R, Julia, and more
- **Visualizations**: Inline plots and charts
- **Sharing**: Export to HTML, PDF, slides
- **Collaboration**: Share notebooks with others

### Jupyter Components

- **Jupyter Notebook**: Classic notebook interface
- **JupyterLab**: Next-generation interface with more features
- **Jupyter Notebook Server**: Backend that runs notebooks

---

## Installation

### Install Jupyter

```bash
# Activate your conda environment
conda activate lab-env

# Install Jupyter
pip install jupyter

# Or install via conda
conda install jupyter
```

### Install JupyterLab

```bash
# Install JupyterLab (recommended)
pip install jupyterlab

# Or via conda
conda install -c conda-forge jupyterlab
```

### Install Jupyter Extensions

```bash
# Install JupyterLab extensions manager
pip install jupyterlab-git
pip install jupyterlab-variableinspector
pip install jupyterlab-lsp
```

### Verify Installation

```bash
# Check Jupyter version
jupyter --version

# List installed kernels
jupyter kernelspec list
```

---

## Basic Usage

### Starting Jupyter

#### Jupyter Notebook (Classic)

```bash
# Start Jupyter Notebook
jupyter notebook

# Opens in browser at http://localhost:8888
```

#### JupyterLab (Recommended)

```bash
# Start JupyterLab
jupyter lab

# Opens in browser at http://localhost:8888
```

### Creating a New Notebook

1. Click "New" → "Python 3" (or your kernel)
2. Or use command line:
```bash
jupyter notebook new-notebook.ipynb
jupyter lab new-notebook.ipynb
```

### Notebook Interface

- **Cells**: Individual code or markdown blocks
- **Toolbar**: Run, save, add cells
- **Menu**: File, Edit, View, Insert, Cell, Kernel, Help

### Running Cells

- **Run cell**: `Shift+Enter`
- **Run and insert below**: `Option+Enter` (Mac) / `Alt+Enter` (Windows)
- **Run and stay**: `Ctrl+Enter`
- **Run all cells**: `Cell → Run All`
- **Run all above**: `Cell → Run All Above`

### Cell Types

- **Code**: Execute Python code
- **Markdown**: Write documentation
- **Raw**: Unformatted text

Switch cell type:
- `Y` → Code
- `M` → Markdown
- `R` → Raw

---

## Working with Notebooks

### Cell Operations

```bash
# Keyboard shortcuts (in command mode, press Esc first)
A              Insert cell above
B              Insert cell below
D D            Delete cell (press D twice)
Z              Undo cell deletion
X              Cut cell
C              Copy cell
V              Paste cell below
M              Convert to markdown
Y              Convert to code
L              Toggle line numbers
```

### Navigation

```bash
# Command mode (press Esc)
↑/↓            Navigate cells
Enter          Edit cell
Shift+Enter    Run cell and move to next
```

### Markdown Cells

Write documentation using Markdown:

```markdown
# Heading 1
## Heading 2

**Bold** and *italic* text

- Bullet point
- Another point

1. Numbered list
2. Second item

`code` inline

```python
# Code block
print("Hello")
```
```

### Magic Commands

Jupyter supports "magic" commands:

```python
# Line magics (single %)
%timeit sum(range(100))        # Time execution
%matplotlib inline             # Inline plots
%load_ext autoreload           # Auto-reload modules
%autoreload 2                  # Reload all modules

# Cell magics (double %%)
%%timeit
# Code here
sum(range(100))

%%writefile filename.py
# Write cell content to file
print("Hello")
```

### Common Magic Commands

```python
%lsmagic                       # List all magics
%pwd                           # Print working directory
%cd /path/to/dir               # Change directory
%ls                            # List files
%who                           # List variables
%whos                          # Detailed variable info
%reset                         # Reset namespace
%run script.py                 # Run Python script
%load script.py                # Load script into cell
```

---

## Python Kernels

### Using Conda Environments

Create a kernel from a conda environment:

```bash
# Activate environment
conda activate lab-env

# Install ipykernel
conda install ipykernel

# Create kernel
python -m ipykernel install --user --name lab-env --display-name "Python (lab-env)"
```

### Switch Kernels

1. In notebook: `Kernel → Change Kernel → Select kernel`
2. Or when creating: `New → Select kernel`

### List Kernels

```bash
# List all kernels
jupyter kernelspec list

# Remove kernel
jupyter kernelspec remove kernel-name
```

---

## Installing Packages

### In Notebook

```python
# Install package (use with caution)
!pip install package-name

# Or use conda
!conda install package-name

# Better: install in environment, then restart kernel
```

### Best Practice

Install packages in your conda environment, then restart kernel:

```bash
# In terminal
conda activate lab-env
pip install numpy pandas matplotlib
```

Then in notebook:
```python
# Restart kernel: Kernel → Restart
import numpy as np
import pandas as pd
```

---

## Data Visualization

### Matplotlib

```python
%matplotlib inline
import matplotlib.pyplot as plt
import numpy as np

x = np.linspace(0, 10, 100)
y = np.sin(x)

plt.figure(figsize=(10, 6))
plt.plot(x, y)
plt.xlabel('X axis')
plt.ylabel('Y axis')
plt.title('Sine Wave')
plt.show()
```

### Seaborn

```python
import seaborn as sns
import pandas as pd

# Load data
df = pd.read_csv('data.csv')

# Create plot
sns.scatterplot(data=df, x='x', y='y', hue='category')
plt.show()
```

### Plotly (Interactive)

```python
import plotly.express as px

df = pd.read_csv('data.csv')
fig = px.scatter(df, x='x', y='y', color='category')
fig.show()
```

---

## Working with Data

### Loading Data

```python
import pandas as pd

# CSV
df = pd.read_csv('data.csv')

# Excel
df = pd.read_excel('data.xlsx')

# JSON
df = pd.read_json('data.json')

# From URL
df = pd.read_csv('https://example.com/data.csv')
```

### Displaying Data

```python
# Display DataFrame
df

# First few rows
df.head()

# Last few rows
df.tail()

# Summary statistics
df.describe()

# Data types
df.dtypes

# Info
df.info()
```

---

## Best Practices

### 1. Organize Your Notebooks

Structure your notebook:

```markdown
# Title
## Introduction
## Data Loading
## Data Cleaning
## Analysis
## Results
## Conclusion
```

### 2. Use Markdown Cells

Document your work:
- Explain what each section does
- Add context and reasoning
- Include references

### 3. Keep Cells Focused

Each cell should do one thing:
```python
# Good: Focused cell
data = load_data('file.csv')
data.head()
```

```python
# Bad: Too much in one cell
data = load_data('file.csv')
data = clean_data(data)
data = process_data(data)
results = analyze(data)
plot_results(results)
```

### 4. Restart and Run All

Before sharing:
1. `Kernel → Restart & Clear Output`
2. `Cell → Run All`
3. Verify everything works

### 5. Don't Store Large Data

```python
# Bad: Store large arrays in notebook
large_array = np.random.rand(1000000)

# Good: Load when needed
# Or use data files
```

### 6. Use Version Control

Add to `.gitignore`:
```
.ipynb_checkpoints/
*.ipynb
```

Or use `nbstripout` to remove outputs:
```bash
pip install nbstripout
nbstripout --install
```

### 7. Export Important Results

```python
# Save plots
plt.savefig('figure.png', dpi=300, bbox_inches='tight')

# Save data
df.to_csv('results.csv', index=False)
```

---

## JupyterLab Features

### File Browser

- Navigate files and folders
- Create, rename, delete files
- Upload files

### Terminal

- Access terminal within JupyterLab
- Run command-line tools
- Install packages

### Text Editor

- Edit Python scripts
- Edit configuration files
- Syntax highlighting

### Extensions

Install extensions:
```bash
# Install extension manager
pip install jupyterlab-git

# Enable extension
jupyter labextension list
```

Popular extensions:
- **jupyterlab-git**: Git integration
- **jupyterlab-variableinspector**: Variable inspector
- **jupyterlab-lsp**: Language server protocol
- **jupyterlab-drawio**: Draw.io integration

---

## VS Code/Cursor Integration

### Open Notebook in VS Code/Cursor

1. Install Jupyter extension
2. Open `.ipynb` file
3. Select kernel
4. Run cells with `Shift+Enter`

### Benefits

- Better Git integration
- Integrated terminal
- Code navigation
- Debugging support

---

## Sharing Notebooks

### Export Formats

```bash
# HTML
jupyter nbconvert notebook.ipynb --to html

# PDF (requires LaTeX)
jupyter nbconvert notebook.ipynb --to pdf

# Python script
jupyter nbconvert notebook.ipynb --to python

# Markdown
jupyter nbconvert notebook.ipynb --to markdown
```

### Jupyter Notebook Viewer

Upload to:
- **nbviewer**: https://nbviewer.org/
- **GitHub**: View `.ipynb` files directly
- **Google Colab**: Import from GitHub

### Binder

Create interactive notebooks:
1. Push to GitHub
2. Create `requirements.txt`
3. Link to: https://mybinder.org/

---

## Troubleshooting

### Issue: Kernel Not Starting

**Problem**: Kernel won't start

**Solution**:
```bash
# Check kernel installation
jupyter kernelspec list

# Reinstall kernel
python -m ipykernel install --user --name kernel-name
```

### Issue: Import Errors

**Problem**: Can't import packages

**Solution**:
1. Check you're using correct kernel
2. Install packages in environment:
```bash
conda activate lab-env
pip install package-name
```
3. Restart kernel: `Kernel → Restart`

### Issue: Plots Not Showing

**Problem**: Matplotlib plots not displaying

**Solution**:
```python
%matplotlib inline
# Or
%matplotlib notebook  # For interactive plots
```

### Issue: Notebook Too Large

**Problem**: Notebook file is huge

**Solution**:
```bash
# Clear outputs
jupyter nbconvert --ClearOutputPreprocessor.enabled=True --inplace notebook.ipynb

# Or use nbstripout
nbstripout notebook.ipynb
```

### Issue: Can't Connect to Server

**Problem**: Can't access Jupyter

**Solution**:
```bash
# Check if server is running
jupyter notebook list

# Start with specific port
jupyter notebook --port 8889

# Generate new token
jupyter notebook --generate-config
```

---

## Advanced Usage

### Custom CSS

Create custom CSS for notebooks:

```python
from IPython.core.display import HTML
HTML("""
<style>
.container { width: 90% !important; }
</style>
""")
```

### Widgets

Interactive widgets:

```python
from ipywidgets import interact

@interact(x=(0, 10), y=(0, 10))
def plot(x, y):
    plt.scatter(x, y)
    plt.show()
```

### Parallel Processing

```python
from ipyparallel import Client

# Start cluster
# ipcluster start -n 4

rc = Client()
view = rc[:]

# Parallel execution
results = view.map(lambda x: x**2, range(10))
```

---

## Quick Reference

### Essential Commands

```bash
# Start Jupyter
jupyter notebook
jupyter lab

# Create kernel from environment
python -m ipykernel install --user --name env-name

# List kernels
jupyter kernelspec list

# Convert notebook
jupyter nbconvert notebook.ipynb --to html
```

### Keyboard Shortcuts

```
Shift+Enter        Run cell
Esc                Command mode
A                  Insert cell above
B                  Insert cell below
D D                Delete cell
M                  Markdown mode
Y                  Code mode
```

### Magic Commands

```python
%matplotlib inline     # Inline plots
%timeit               # Time execution
%load_ext autoreload  # Auto-reload
%autoreload 2         # Reload all
%pwd                   # Current directory
%who                   # List variables
```

---

## Related Guides

- **[Conda Guide](conda.md)** - Manage Python environments for Jupyter
- **[VS Code/Cursor Guide](vscode-cursor.md)** - Use Jupyter in VS Code/Cursor
- **[Python Development](../development-environment.md)** - Set up Python environment
- **[Development Tools Overview](index.md)** - All development tools guides

---

*Last updated: {{ git_revision_date_localized }}*

