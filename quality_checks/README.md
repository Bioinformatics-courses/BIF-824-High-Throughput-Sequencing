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




































References
1. Matlock, B. & Scientific, T. F. Assessment of nucleic acid purity. https://assets.thermofisher.com/TFS-Assets/CAD/Product-Bulletins/TN52646-E-0215M-NucleicAcid.pdf. 

2. Mueller, O., Lightfoot, S. & Schroeder, A. RNA integrity number (RIN) -standardization of RNA quality control. https://www.agilent.com/cs/library/applications/5989-1165EN.pdf (2006). 

3. Illumina Inc. Optimizing cluster density on illumina sequencing systems. https://www.illumina.com/content/dam/illumina-marketing/documents/products/other/miseq-overclustering-primer-770-2014-038.pdf (2016). 

4. Hosseini M, Pratas D and Pinho AJ (2016) A Survey on Data Compression Methods for Biological Sequences. Information. An International Interdisciplinary Journal 7(4). Multidisciplinary Digital Publishing Institute: 56.

5. Andrews S (n.d.) Babraham Bioinformatics – FastQC A Quality Control tool for High Throughput Sequence Data. Available at: https://www.bioinformatics.babraham.ac.uk/projects/fastqc/ (accessed 13 October 2023).