## bwa mapping tools

### Index hg38 reference geenome
```bash

bwa index -a bwtsw  hg38.fa

## ---> -a bwtsw	Algorithm implemented in BWT-SW. This method works with the whole human genome.
## ---> -a is	IS linear-time algorithm for constructing suffix array. It requires 5.37N memory where N is the size of the database. IS is moderately fast, but does not #work with database larger than 2GB.

```