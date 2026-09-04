# Rabies virus Gene Annotator (RvGA)

A Bash script for annotating and retrieving the 5 individual genes of the rabies virus in nucleotides and amino acids.


# Important:

This pipeline works well with complete rabies virus (RABV) sequences, so it is important to note that if you want to annotate fragmented sequences, SamTools may fail when attempting to extract the gene sequences. This is because, when annotating genes using protein sequences as references, SamTools searches three bases beyond the position indicated by BLASTx to include the stop codon; thus, if the contig in which the gene was annotated is shorter, SamTools will not retrieve the gene’s sequence.

# Installation:

To clone the repository, run the following command:

```
 git clone https://github.com/Marcopterix/Rabies_virus_Gene_Annotator
```

Once you have cloned the repository, navigate to the ***Rabies_virus_Gene_Annotator/bin*** directory and grant the scripts execute permission:

```
chmod +x *sh
```
It's also important to add this folder to the PATH in your ***~/.bashrc***:
```
nano ~/.bashrc

# Once you are editing your ~/.bashrc, paste the following line into the section where your paths are listed,
# replacing “$HOME/PATH_TO/Rabies_virus_Gene_Annotator/bin” with the full path where you cloned your repository.
# To find this path, navigate to the bin directory, and once there, type the command pwd in the terminal.

export PATH="$HOME/PATH_TO/Rabies_virus_Gene_Annotator/bin:$PATH"

source ~/.bashrc

```

# Required dependencies:

You must have the following programs installed, and you ***must also add the binaries for these programs to your PATH***:


***---> BLAST+ to run BLASTx (https://blast.ncbi.nlm.nih.gov/doc/blast-help/downloadblastdata.html#blast-executables)  
---> Entrez Direct to download the database (https://www.ncbi.nlm.nih.gov/books/NBK179288/)  
---> samtools to run samtools faidx (https://www.htslib.org/) and  
---> seqkit (https://bioinf.shenwei.me/seqkit/download/)***

# Prepare the Database

Once you have installed the necessary dependencies, you must run the ***RGA_db_dwl.sh*** script as follows:

```
bash RGA_db_dwl.sh
```

This will download the databases to the $HOME/db/RGA folder. If you'd like, you can add the path to these generated files to your ~/.bashrc file as follows:

```
nano ~/.bashrc

export Bx_RABV_RGA_PATH="$HOME/db/RGA"

source ~/.bashrc
```

# Using and Running the Pipeline

Once you have all the requirements, you should run the pipeline as follows:


 Note: It is important to paste the full paths into the “-f” and “-o” options so that the pipeline can run correctly.
 
```
bash rabies_gene_annotator.sh -f FASTA file directory -o OUTPUT directory -p PATH to BLAST DB 

Options:
Usage: rabies_gene_annotator.sh -f FASTA file PATH -o OUTDIR PATH
 -h print help 
 -f FASTA file directory 
 -o OUTPUT directory 
 -p PATH to BLAST database. If you downloades the database by running the RGA_db_dwl.sh script, the path to your database is: $HOME/db/RGA 

```

# Output Files

At the end of the pipeline run, in the directory you specified with the ***-o*** option, you will find two folders: Nucleotides and Proteins, containing the nucleotide and amino acid sequences, respectively; you will also find the **Annotation_all.tsv** file, which contains the annotation information for your sequences.



