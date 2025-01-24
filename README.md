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

