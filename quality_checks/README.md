#  quality control (QC) metrics
## Yield
Yield is the number of bases generated in the run. Yield is important to all users, but is usually something your service provider will guarantee so you don't need to worry about it.
Error rate
Refers to the percentage of bases called incorrectly at any one cycle. It is calculated from the reads that are aligned to Illumina's PhiX control. If this was not used then %>=Q30 is your best tool to check base quality. Error rate increases along the length of the read.
## %Q30
The percentage of bases with a quality score of 30 or higher, respectively (see "Quality Scores Explained" below). Most Illumina runs will generate >70-80% Q30 data. This value is an average across the whole read length, and error rate increases towards the end of the reads. Because of this a run can "fail" at the end of a long-read, but pass Illumina's specs for the run with respect to Q30 - if a read is Q40 for bases 1-100, and Q10 for bases 101-150 it will pass the Q30 spec, but if you need the ends of the reads to be high quality, you may be disappointed.
## Density (K/mm2)
The density of clusters on the flow cell (in thousands per mm2). On MiniSeq, MiSeq, NextSeq and HiSeq 2500 this is an important metric to evaluate if the data are low-quality. It should be assessed in tandem with %PF as the two together can diagnose problems with over- or under-loading your library. On HiSeq 4000 and X density is a fixed value and diagnosing issues with library loading are much more difficult to fix.
## Cluster PF (%)
In Illumina clustering a single-molecule should generate a single cluster with a clear signal in the base being sequenced. The %PF is the number of clusters that passed Illumina's "Chastity filter". The clusters that do not pass this filter are generally removed from downstream analysis.

The Chastity filter works by calculating the ratio of the highest base intensity to the sum of the 1st and 2nd highest, anything less than 0.6 is filtered out. If a cluster was formed from a single-molecule then the chastity score will be 1; if it were formed from two molecules the signal would be equal and the chastity score will be 0.5.
## Phas/Prephas (%)
This is an important metric to pay attention to - low numbers are what you want to see e.g. 0.1/0.1. Phasing is the rate at which individual molecules in a cluster become out of sync with each other, with some falling behind (phasing), and others jumping ahead (pre-phasing). The value given is the percentage of true signal being lost in each cycle, so after 150 cycles 15% of the data is now noise. Phasing is why long-reads are difficult!

>>> ## Download data sets

We will download 4 fastq files of 1000 genomes data sets using the link below:
>https://www.ebi.ac.uk/ena/browser/view/PRJEB3366

>https://www.ebi.ac.uk/biostudies/arrayexpress/studies/E-GEUV-1

>https://github.com/nellore/rail/blob/master/eval/E-GEUV-3.sdrf.txt


>> commandline to download 
```bash
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/ERR188/ERR188027/ERR188027_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/ERR188/ERR188026/ERR188026_2.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/ERR188/ERR188030/ERR188030_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/ERR188/ERR188030/ERR188030_2.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/ERR188/ERR188026/ERR188026_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/ERR188/ERR188027/ERR188027_2.fastq.gz
```

>>> ## Tools for quality control assessment 
1. fastqc https://www.bioinformatics.babraham.ac.uk/projects/fastqc/
2. multiqc  https://multiqc.info/
3. picard https://broadinstitute.github.io/picard/

>>> ## checking quality control of fastq files. 
```bash
#---->  fastqc 1.fastq.gz  2.fastq.gz 
fastqc ERR188026_1.fastq.gz  ERR188026_2.fastq.gz 
fastqc ERR188027_1.fastq.gz  ERR188027_2.fastq.gz
fastqc ERR188030_1.fastq.gz  ERR188030_2.fastq.gz
```
>>> ## fastqc report 
1. Summary
1. Basic Statistics
2. Per base sequence quality
3. Per tile sequence quality
4 Per sequence quality scores
5. Per base sequence content
6. Per sequence GC content
7. Per base N content
8. Sequence Length Distribution
9. Sequence Duplication Levels
10. Overrepresented sequences
12. Adapter Content

>>> ## quality assessment status  
PASS: <img src="./images/pass.png">

FAIL: <img src="./images/fail.png">

WARNING:<img src="./images/warning.png">

## fastqc report: Basic statistics 
1. Filename:  The original filename of the file which was analysed	
2. File type:  Whether the file appeared to contain actual base calls or colorspace data which had to be converted to base calls	 
3. Encoding: ASCII encoding of quality values 	 
4. Total Sequences:  A count of the total number of sequences processed.  In future will be two values : actual and estimated	 
5. Total Bases	 
6. Sequences flagged as poor quality: If running in Casava mode sequences flagged to be filtered will be removed from all analyses 
7. Sequence length: Provides the length of the shortest and longest sequence in the set. If all sequences are the same length only one value is reported.	 
7. %GC: he overall %GC of all bases in all sequences	 

 <img src="./images/basic_statistics.png">

> Warning
Basic Statistics never raises a warning.


> Failure
Basic Statistics never raises an error.

## fastqc report: Per base sequence quality
1. A	box-and-whisker	plot	showing	aggregated	quality	score	
statistics	at	each	position	along	all	reads	in	the	file.	
2. Note	that	the	X-axis	is	not	uniform.
3. the	X-axis	 starts	out	with	bases	1-10	being	reported	individually,	after	that, it	will	bin	bases	across	a
window	a	certain	number	of	positions	wide.	
4. The	number	of	base	positions	binned	 together	depends	on	the	length	of	the	reads, i.e, 	Shorter	reads	will	have	
smaller	windows	and	longer	reads	larger	windows. 
4. The	blue	line	is	the	mean	quality	score	at	each	base	position/window.
5. The	red	line	within	each	yellow	box	represents	the	median	quality	score	at	that	position/window.
6. Yellow	box	is	the	inner-quartile	range	for	25th to	75th percentile.
7. The	upper	and	lower	whiskers	represent	the	10th and	90th percentile	scores.
8. The y-axis on the graph shows the quality scores. The higher the score the better the
base call. 
9. The background of the graph divides the y axis into very good quality calls
(green), calls of reasonable quality (orange), and calls of poor quality (red). 

> `#40E0D0 Note that The quality of calls on most platforms will degrade as the run progresses, so it is common to see base`
calls falling into the orange area towards the end of a read.

> `#40E0D Note that FastQC attempts to automatically determine which encoding method was in any fastq file.`

 <img src="./images/per_base_qc.png">

> Warning
A warning will be issued if the lower quartile for any base is less than 10, or if the median
for any base is less than 25.

> Failure
This module will raise a failure if the lower quartile for any base is less than 5 or if the
median for any base is less than 20.

























# References
1. Matlock, B. & Scientific, T. F. Assessment of nucleic acid purity. https://assets.thermofisher.com/TFS-Assets/CAD/Product-Bulletins/TN52646-E-0215M-NucleicAcid.pdf. 

2. Mueller, O., Lightfoot, S. & Schroeder, A. RNA integrity number (RIN) -standardization of RNA quality control. https://www.agilent.com/cs/library/applications/5989-1165EN.pdf (2006). 

3. Illumina Inc. Optimizing cluster density on illumina sequencing systems. https://www.illumina.com/content/dam/illumina-marketing/documents/products/other/miseq-overclustering-primer-770-2014-038.pdf (2016). 

4. Hosseini M, Pratas D and Pinho AJ (2016) A Survey on Data Compression Methods for Biological Sequences. Information. An International Interdisciplinary Journal 7(4). Multidisciplinary Digital Publishing Institute: 56.

5. Andrews S (n.d.) Babraham Bioinformatics – FastQC A Quality Control tool for High Throughput Sequence Data. Available at: https://www.bioinformatics.babraham.ac.uk/projects/fastqc/ (accessed 13 October 2023).