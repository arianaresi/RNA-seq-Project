## **Alignment**


### **What is an alignment?**

Genome alignment is a bioinformatics process that involves aligning the DNA or RNA sequences of one or more genomes. 

The main goal of genome alignment is to identify regions of similarity or homology between sequences, which can provide valuable information about various biological processes, such as gene identification, evolutionary analysis and functional annotation.


#### **RNA-seq**

Reference genome alignment involves mapping RNA-Seq reads to a known reference genome.

**Requirements for alignment:**

- A GFF (annotation file)
- The species must have a good quality genome
- Normally employed in a model organism


### **Alignment procedure**

Is based on a two-step approach:

1. Indexing the reference genome by creating a STAR index

2. Align and count with STAR

Now, we will go step by step in the alignment of our readings.
