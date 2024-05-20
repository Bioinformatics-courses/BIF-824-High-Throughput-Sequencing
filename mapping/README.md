# Map reads on a reference genome
Sequence read mapping is  refer to the process to align the reads on a reference genomes. 
A  mapping  tool (mapper) required as input two set of files:
1. An indexed reference genome
2. A set of reads (Often fastq files). 

Mapper align each read in the set of reads on the reference genome. Some mappers perform exact matching, while others allow  mismatches, indels and clipping of some short fragments on the two ends of the reads.


# Software 
1. bwa
2. Bowtie2 

# Reference genome  
We will use hg38/GRCh38 human reference genome which   is the latest human reference genome as of today. hg38/GRCh38 was released December, 2013. There are multiple  versions hg38/GRCh38 human reference genome.
> sources for downloading: 

1.UCSC Genome Browser: http://hgdownload.soe.ucsc.edu/downloads.html#human
2. Ensembl: https://www.ensembl.org/info/data/ftp/index.html
3. NCBI: https://www.ncbi.nlm.nih.gov/genome/51

## FTP Download sections 
1. http://hgdownload.soe.ucsc.edu/goldenPath/hg38/bigZips/
2. ftp://ftp.ensembl.org/pub/release-92/fasta/homo_sapiens/dna/
3. https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/000/001/405/GCA_000001405.29_GRCh38.p14/

## Download  hg38/GRCh38 

### UCSC Genome Browser

> wget -c http://hgdownload.soe.ucsc.edu/goldenPath/hg38/bigZips/hg38.fa.gz
> gunzip hg38.fa.gz

or 

> wget --timestamping 'ftp://hgdownload.cse.ucsc.edu/goldenPath/hg38/bigZips/14/*'


### NCBI

> https://api.ncbi.nlm.nih.gov/datasets/v2alpha/genome/accession/GCF_000001405.40/download?include_annotation_type=GENOME_FASTA&include_annotation_type=GENOME_GFF&include_annotation_type=RNA_FASTA&include_annotation_type=CDS_FASTA&include_annotation_type=PROT_FASTA&include_annotation_type=SEQUENCE_REPORT&hydrated=FULLY_HYDRATED

or 

> datasets download genome accession GCF_000001405.40 --include gff3,rna,cds,protein,genome,seq-report

## Mapping 
1. [bwa]{./bwa.md}
2. [Bowtie2]{./bowtie2.md}














# References
Schbath S, Martin V, Zytnicki M, Fayolle J, Loux V, Gibrat JF. Mapping reads on a genomic sequence: an algorithmic overview and a practical comparative analysis. J Comput Biol. 2012 Jun;19(6):796-813. doi: 10.1089/cmb.2012.0022. Epub 2012 Apr 16. PMID: 22506536; PMCID: PMC3375638.

Chen, NC., Paulin, L.F., Sedlazeck, F.J. et al. Improved sequence mapping using a complete reference genome and lift-over. Nat Methods 21, 41–49 (2024). https://doi.org/10.1038/s41592-023-02069-6
