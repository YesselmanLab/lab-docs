# Working with HCC Clusters

The Holland Computing Center (HCC) provides high-performance computing (HPC) resources for research at the University of Nebraska. This guide will help you get started using HCC clusters for computational work.

---

## What is HCC?

**HCC (Holland Computing Center)** is a computing facility that provides:

- **High-performance computing clusters**: Powerful computers for running large computational jobs
- **Cloud computing resources**: Virtual machines for various computing needs
- **Storage**: Large amounts of data storage for research projects
- **Specialized software**: Pre-installed scientific and research software

### Why Use HCC Clusters?

- **More computing power**: Run jobs that need more resources than your laptop
- **Parallel processing**: Run many tasks simultaneously
- **Long-running jobs**: Jobs can run for days or weeks without interruption
- **Specialized software**: Access to software that's difficult to install locally
- **Large storage**: Store and process large datasets

### When to Use HCC vs. Your Computer

**Use HCC when:**
- Your job needs more memory than your computer has
- Your job will run for hours or days
- You need to run many jobs in parallel
- You need specialized scientific software
- You're working with very large datasets

**Use your local computer when:**
- Quick tests or small jobs
- Interactive development
- Jobs that finish in minutes
- Working with small datasets

---

## Getting Started

### Step 1: Create an HCC Account

1. **Apply for an account** at the HCC website, join group `yesselmanlab`
2. **Wait for approval** (usually quick for University of Nebraska affiliates)
3. **Set up your password** when you receive account information
4. **Set up Duo two-factor authentication** (required for security)

### Step 2: Connect to a Cluster

Once you have an account, you can connect to HCC clusters using SSH (Secure Shell).

**Basic connection command:**
```bash
ssh your-username@login.swan.unl.edu
```

Replace `your-username` with your HCC username.


**First time connecting:**
- You'll be asked to accept the host key (type `yes`)
- Enter your password
- Complete Duo authentication

### Step 3: Understand the Cluster Structure

When you connect, you're on a **login node**. This is NOT for running jobs - it's only for:
- Managing files
- Editing scripts
- Submitting jobs
- Light testing

**Important:** Never run heavy computations on login nodes! Always submit jobs to compute nodes.

---

## Basic Linux Commands

Since HCC clusters run Linux, you'll need to know basic Linux/Unix commands to navigate and work with files.

!!! tip "Learn Linux Commands"
    For a comprehensive guide to Linux/Unix commands, see the **[Command Line Guide](../command-line-guide.md)**. This guide covers all the essential commands you'll need for working on HCC clusters, including:
    - Navigation commands (`cd`, `ls`, `pwd`)
    - File management (`cp`, `mv`, `rm`, `mkdir`)
    - Text editing (`nano`, `vim`)
    - Viewing files (`cat`, `less`, `head`, `tail`)
    - Getting help (`man`, `--help`)
    - And much more!

---

## File Storage on HCC

### Home Directory (`~`)

- **Location:** `/home/your-username`
- **Size limit:** Usually 10-50GB
- **Backed up:** Yes
- **Best for:** Scripts, configuration files, small data

### Work Directory (`/work`)

- **Location:** `/work/your-username`
- **Size limit:** Much larger (check current limits)
- **Backed up:** No (be careful!)
- **Best for:** Large datasets, job outputs, temporary files

### Scratch Space

- **Location:** `/scratch/your-username` or node-specific
- **Size:** Very large but temporary
- **Backed up:** No
- **Best for:** Temporary files during job execution
- **Important:** Files may be deleted after a period of inactivity

### Storage Best Practices

1. **Keep scripts in home directory** (backed up)
2. **Use work directory for large data** (not backed up, but persistent)
3. **Use scratch for temporary job files** (may be deleted)
4. **Transfer important results back to your computer** regularly
5  **Back stuff up on $NRDSTOR** which is free storage that everyone has access to.

---

## Transferring Files

### Using SCP (Command Line)

SCP (Secure Copy Protocol) allows you to transfer files from the command line. For detailed SCP usage and examples, see the **[Command Line Guide](../command-line-guide.md)**.

**Basic usage:**
- Upload: `scp filename.txt your-username@login.swan.unl.edu:~/`
- Download: `scp your-username@login.swan.unl.edu:~/filename.txt ./`
- Transfer directory: `scp -r directoryname your-username@login.swan.unl.edu:~/`

### Using Cyberduck (GUI - Mac/Windows)

1. **Download Cyberduck** from [cyberduck.io](https://cyberduck.io)
2. **Open Cyberduck** and click "Open Connection"
3. **Select "SFTP (SSH File Transfer Protocol)"**
4. **Enter connection details:**
   - Server: `login.swan.unl.edu`
   - Username: Your HCC username
   - Password: Your HCC password
5. **Click "Connect"**

### Using WinSCP (Windows)

1. **Download WinSCP** from [winscp.net](https://winscp.net)
2. **Open WinSCP** and enter connection details:
   - File protocol: SFTP
   - Host name: `login.swan.unl.edu`
   - Username: Your HCC username
   - Password: Your HCC password
3. **Click "Login"**

### Using Globus (Large Files)

For very large files or many files, use Globus:

1. **Go to** [globus.org](https://www.globus.org)
2. **Sign in** with your university credentials
3. **Set up endpoints** for HCC and your computer
4. **Transfer files** through the web interface

---

## Running Jobs on HCC

HCC uses **SLURM** (Simple Linux Utility for Resource Management) to manage jobs. You don't run jobs directly - you submit them to a queue, and SLURM runs them when resources are available.

### Understanding Job Submission

1. **Create a job script** (tells SLURM what to run)
2. **Submit the job** to the queue
3. **SLURM schedules** your job when resources are available
4. **Your job runs** on compute nodes
5. **Results are saved** to output files

### Basic Job Script Example

Create a file called `myjob.sh`:

```bash
#!/bin/bash
#SBATCH --job-name=myjob          # Job name
#SBATCH --output=myjob.out        # Output file
#SBATCH --error=myjob.err         # Error file
#SBATCH --time=01:00:00           # Time limit (1 hour)
#SBATCH --nodes=1                 # Number of nodes
#SBATCH --ntasks-per-node=1       # Tasks per node
#SBATCH --mem=4G                  # Memory needed

# Your commands here
echo "Hello from HCC!"
python myscript.py
```

### Submitting a Job

```bash
# Submit your job
sbatch myjob.sh

# Check job status
squeue -u your-username

# Cancel a job
scancel jobid
```

### Monitoring Jobs

```bash
# See your jobs
squeue -u your-username

# See detailed job information
scontrol show job jobid

# See job history
sacct -u your-username
```

### Interactive Jobs

Sometimes you want to interact with a job directly:

```bash
# Request an interactive session
srun --pty bash

# Request with specific resources
srun --time=01:00:00 --mem=8G --pty bash
```

**Use interactive jobs for:**
- Testing code
- Debugging
- Exploring data
- Running interactive software

---

## Using Software on HCC

### Module System

HCC uses a **module system** to manage software. Instead of installing software yourself, you load pre-installed modules.

**Common module commands:**
```bash
# See available software
module avail

# Search for software
module avail python

# Load a module
module load python/3.9

# See loaded modules
module list

# Unload a module
module unload python/3.9

# Unload all modules
module purge
```

### Example: Using Python

```bash
# Load Python module
module load python/3.9

# Check Python version
python --version

# Run Python script
python myscript.py
```

### Example: Using Conda

```bash
# Load conda module
module load anaconda

# Create environment
conda create -n myenv python=3.9

# Activate environment
conda activate myenv

# Install packages
conda install numpy pandas
```

### Finding Software

1. **Check available modules:**
   ```bash
   module avail
   ```

2. **Check HCC documentation** for specific software guides

3. **Ask HCC support** if software isn't available

---

## Common Workflows

### Workflow 1: Running a Python Script

1. **Transfer your script to HCC** using SCP or a GUI tool (see [Transferring Files](#transferring-files) section)

2. **Connect to HCC:**
   ```bash
   ssh your-username@login.swan.unl.edu
   ```

3. **Create job script** (`run_python.sh`) with a text editor:
   ```bash
   #!/bin/bash
   #SBATCH --job-name=python_job
   #SBATCH --output=python_job.out
   #SBATCH --time=02:00:00
   #SBATCH --mem=8G
   
   module load python/3.9
   python myscript.py
   ```

4. **Submit job:**
   ```bash
   sbatch run_python.sh
   ```

5. **Check status:**
   ```bash
   squeue -u your-username
   ```

6. **View results** using text viewing commands (see [Command Line Guide](../command-line-guide.md))

### Workflow 2: Running Multiple Jobs (Job Arrays)

If you need to run the same job with different parameters:

```bash
#!/bin/bash
#SBATCH --job-name=array_job
#SBATCH --output=array_%A_%a.out
#SBATCH --array=1-10
#SBATCH --time=01:00:00

# SLURM_ARRAY_TASK_ID will be 1, 2, 3, ..., 10
python myscript.py --input data_${SLURM_ARRAY_TASK_ID}.txt
```

### Workflow 3: Using Jupyter Notebooks

HCC supports running Jupyter notebooks on compute nodes:

1. **Submit interactive job with Jupyter:**
   ```bash
   srun --time=02:00:00 --mem=8G --pty bash
   ```

2. **Load Python module:**
   ```bash
   module load python/3.9
   ```

3. **Start Jupyter:**
   ```bash
   jupyter notebook --no-browser --port=8888
   ```

4. **Set up SSH tunnel** from your computer:
   ```bash
   ssh -L 8888:localhost:8888 your-username@login.swan.unl.edu
   ```

5. **Open browser** to `localhost:8888`

---

## Best Practices

### Do's

✅ **Do submit jobs instead of running on login nodes**
- Login nodes are shared - heavy computation slows things down for everyone

✅ **Do request appropriate resources**
- Request enough time, memory, and CPUs for your job
- Requesting too much wastes resources; too little causes job failures

✅ **Do test with small jobs first**
- Make sure your code works before submitting large jobs

✅ **Do clean up temporary files**
- Delete files you don't need to save storage space

✅ **Do use work directory for large files**
- Home directory has size limits

✅ **Do check job output files**
- Look at `.out` and `.err` files to see what happened

### Don'ts

❌ **Don't run heavy computations on login nodes**
- Always submit jobs to compute nodes

❌ **Don't request excessive resources**
- Request what you need, not everything available

❌ **Don't store large files in home directory**
- Use work or scratch directories

❌ **Don't submit thousands of tiny jobs**
- Batch similar jobs together when possible

❌ **Don't ignore error messages**
- Check `.err` files to understand failures

---

## Getting Help

### HCC Documentation

- **Main documentation:** [https://hcc.unl.edu/docs/](https://hcc.unl.edu/docs/)
- **Software guides:** Check the "Running Applications" section
- **Job submission:** Check the "Submitting Jobs" section

### HCC Support

- **Email:** [hcc-support@unl.edu](mailto:hcc-support@unl.edu)
- **Help tickets:** Submit through HCC website
- **Office hours:** Check HCC website for current hours

### Common Issues

**Problem: Job won't start**
- Check if you requested too many resources
- Check partition availability
- Check job script for errors

**Problem: Job runs out of memory**
- Increase `--mem` in your job script
- Check if your code has memory leaks

**Problem: Job takes too long**
- Increase `--time` in your job script
- Optimize your code if possible

**Problem: Can't connect to cluster**
- Check your internet connection
- Verify your username and password
- Check if Duo authentication is working

---

## Quick Reference

### Connection Commands

```bash
# Connect to Swan login node
ssh your-username@login.swan.unl.edu
```

### Job Management

```bash
# Submit job
sbatch jobscript.sh

# Check job status
squeue -u your-username

# Cancel job
scancel jobid

# See job details
scontrol show job jobid
```

### File Transfer

For detailed file transfer commands, see the **[Command Line Guide](../command-line-guide.md)**.

**Basic SCP commands:**
- Upload: `scp file.txt your-username@login.swan.unl.edu:~/`
- Download: `scp your-username@login.swan.unl.edu:~/file.txt ./`
- Upload directory: `scp -r directory your-username@login.swan.unl.edu:~/`

### Module Commands

```bash
# List available
module avail

# Load module
module load software/version

# List loaded
module list

# Unload all
module purge
```

---

## Next Steps

1. **Get an HCC account** if you don't have one
2. **Connect to Swan cluster** and explore
3. **Try a simple job** to get familiar with SLURM
4. **Read HCC documentation** for your specific software needs
5. **Ask for help** if you get stuck

---

## Related Guides

- **[Command Line Guide](../command-line-guide.md)** - Learn terminal basics (essential before using HCC)
- **[Development Tools Overview](index.md)** - Other development tools
- **[HCC Official Documentation](https://hcc.unl.edu/docs/)** - Complete HCC documentation

---

*Last updated: {{ git_revision_date_localized }}*

