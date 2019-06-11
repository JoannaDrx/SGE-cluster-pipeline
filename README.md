# RNA-Seq pipeline on SGE cluster - June 2016

A pipeline for RNA-Seq data processing using the UCSF qb3 cluster (SGE). 

# Tools
FASTQC - http://www.bioinformatics.babraham.ac.uk/projects/fastqc/

FASTx_toolkit - http://hannonlab.cshl.edu/fastx_toolkit/download.html

STAR - https://github.com/alexdobin/STAR

SAMtools - http://www.htslib.org/download/

HTSeq - http://www-huber.embl.de/HTSeq/doc/overview.html

Subread bioconductor package (featureCounts) - http://subread.sourceforge.net/ 

# Steps

* FASTQC - checks read quality with a variety of analyses. Output is a zip file and a HTML file. DOwnload HTML file locally to evaluate read quality visually.

* FASTQ trimmer (fastx_toolkit) - trim low quality bases. Input is raw FASTQ files, output is (hopefully cleaner) FASTQ files with the suffix _trimmed added.

* STAR aligner - Input is annotation file (I use GRCh38-Gencode24) and FASTQ files from step 1 or 2 Output is SAM file. The program will ask you if you have single or paired reads (2 files instead of one). If paired reads, it will detect pairs, confirm with the user for correct read pairing and save a reference table of the pairs and their assigned task ID. This small function is available as a standalone script under read_pairs.py in this repository.

* Convert the alignement sam file to a bam file, sort and index it using SAMTOOLS. Seldom use as STAR will directly convert to sorted BAM.

* Count the reads with HTSeq or featureCounts (faster). Input is a sorted BAM file.


In development: multi-threaded job submission support and more automated use of Bioconductor packages.
