# Metagenomics_WW



## Centrifuge : novel microbial classification engine that enables rapid, accurate, and sensitive labeling of reads and quantification of species
https://www.ccb.jhu.edu/software/centrifuge/manual.shtml#what-is-centrifuge



Create conda environment
```
conda create -n centrifuge -c bioconda centrifuge
conda activate centrifuge
```


Download reference index

```
mkdir indices
cd indices
centrifuge-download -o taxonomy taxonomy
centrifuge-download -o library -m -d "bacteria" refseq > seqid2taxid.map
```

dustmasker was missing in the environment
dustmasker is part of NCBI BLAST+ and is used for low-complexity filtering
need to install NCBI BLAST+, which includes dustmasker.

First SLURM job created

```
nano centrifuge_download.sh
```

Write the .sh script to run with sbatch

```
#!/bin/bash
#SBATCH --job-name=centrifuge_download
#SBATCH --output=centrifuge_download.log
#SBATCH --error=centrifuge_download.err
#SBATCH --time=2-00:00:00  # 2 days runtime
#SBATCH --mem=32G          # 32GB RAM
#SBATCH --cpus-per-task=4  # 4 CPU cores
#SBATCH --ntasks=1
#SBATCH --partition=default  # Change this if needed

# Load necessary modules
module load blast+/2.14.1

# Run Centrifuge Download
centrifuge-download -o taxonomy taxonomy
centrifuge-download -o library -m -d "bacteria" refseq > seqid2taxid.map
```

Submit the Job to SLURM

```
sbatch centrifuge_download.sh
```

