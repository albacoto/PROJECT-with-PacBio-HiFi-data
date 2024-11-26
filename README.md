Pacbio HiFi data is very accurate except for homopolymers (starches of the same base pair). This means there will be many false insertions or deletions of single base pairs in a read. 
However, high-quality longer indels should generally be true. There are different possible types.

1.	Insertions and deletions larger than three base pairs and not homopolymers and not repeats of the same unit (microsatellites)
2.	Microsattelites
3.	Alu insertions
4.	Transposable elements

### The task is to develop software based on Pysam to detect a raw set of specific types of insertions and deletions and then filter these to get a highly confident set.

--> *Pysam is a Python package for reading, manipulating, and writing genomics data such as SAM/BAM/CRAM and VCF/BCF files*

You should use the human testis data set *“ob007_kinetics_diploid.bam”*.  You can subsequently also test your code on the *“carl_kinetics_diploid.bam”* data set to see if it is different between humans and chimpanzees.

We can find it in the directory: ```/home/albacoto/TopicsInBioinformatics/data ```

- The *ob007_kinetics_diploid.bam* is a HiFi data set from a human testis biopsi and includes both kinetics information and other tags such as the number of subreads supporting the called base pair for each position. It was aligned to the ob007_diploid.fa reference genome assmbled from the same data.
- The *carl_kinetics_diploid.bam* data file is HiFi data from a chimp testis biopsi that includes kinetics information. It is aligned to the reference genome carl_diploid.fa that was assembled from the same data.


### The output should be a Table with the position in the contig, quality of base pairs, and size of the event. 

I will develop the software based on Pysam through a jupyter notebook.


To use the module to read a file in BAM format, create a ```AlignmentFile``` object:
```
# read BAM file
import pysam
bam_file = pysam.AlignmentFile("/home/albacoto/TopicsInBioinformatics/data/ob007_kinetics_diploid.bam", "rb")
```
- The b qualifier indicates that this is a BAM file.




```cigar``` stands for Compact Idiosyncratic Gapped Alignment Report and represents a compressed (run-length encoded) pairwise alignment format.











NOT REQUIRED (OPTIONAL):
Quality scores in HiFi Pacbio data
The qualities are encoded as phred scaled qualities for each base pair in the consensus read. However, for each base pair, we also have the number of subreads supporting the consensus and the number not supporting the consensus. How do these two measures relate to each other?

Kinetics in Pacbio HiFi data
Pacbio HiFi data contains tags for the kinetics information for each strand of a read with both interpulse and pulse durations (in milliseconds, I believe) 
Characterise the kinetics of all three-mers, five-mers and seven-mers
