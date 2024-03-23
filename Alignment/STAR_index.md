## **STAR index**

**INDEXING:** it is a computational way to create a "data structure" for the reference genome, using indexes, so that we can access parts of it in a more efficient way by aligning. 

Indexing improves the speed and efficiency of these analyses by allowing the software to quickly locate and access relevant parts of the genome.

**Which files are required?**

        - Annotation file (GFF): is a standard file format used in bioinformatics to store and represent genomic and annotation information for various features within a genome, such as genes, transcripts, exons and other genomic elements.

          We use these files alongside the reference genome in order to find locations of genes, transcripts, etc.
          
        - Reference genome: serves as a template against which various genomic analyses are performed, such as read mapping, variant calling and gene expression quantification. 


#### **Fasta file and GFF**

To obtain the annotation file, we were able to download it from the GENCODE Project, available at https://www.gencodegenes.org/human/. 

To download the **General Feature File (GFF)**, we chose the `Basic gene annotation` option, left click on the `GFF3` option and copy the download link to have the file in the cluster.

```{bash download GFF3, eval=FALSE}
qlogin -N GFF3
cd /mnt/Guanina/bioinfo24/Equipo_rosa/alignment/
wget https://ftp.ebi.ac.uk/pub/databases/gencode/Gencode_human/release_45/gencode.v45.basic.annotation.gff3.gz
```


In addition, we obtained the **reference genome** from the path `/mnt/Archives/genome/human/GRCh38/UCSC/chromosomes/hg38.fa`

Once we have all the necessary files to perform the index of the readings, we perform the following scheduled job:

For the sake of efficiency, we have omitted the complete script structure from the report.

```{bash STAR index, eval=FALSE}
module load star/2.7.9a
cd /mnt/Guanina/bioinfo24/Equipo_rosa/STAR_index

# script index con STAR
STAR --runThreadN 12 \
--runMode genomeGenerate \
--genomeDir /mnt/Guanina/bioinfo24/Equipo_rosa/STAR_index \
--genomeFastaFiles /mnt/Archives/genome/human/GRCh38/UCSC/chromosomes/hg38.fa \
--sjdbGTFfile /mnt/Guanina/bioinfo24/Equipo_rosa/alignment/gencode.v45.basic.annotation.gff3 \
--sjdbOverhang 42

```


**Where:**

`STAR --runThreadN 12 \:` indicates that 12 processing threads should be used.

`--runMode genomeGenerate \:` specifies that a genomic index is being generated.

`--genomeDir /mnt/Guanina/bioinfo24/Equipo_rosa/STAR_index \:` specifies the directory where the genomic index files being generated will be stored.

`--genomeFastaFiles /mnt/Archives/genome/human/GRCh38/UCSC/chromosomes/hg38.fa \:` specifies the location of the human genome DNA sequence file (in FASTA format) that will be used to generate the genomic index.

`--sjdbGTFfile /mnt/Guanina/bioinfo24/Equipo_rosa/alignment/gencode.v45.basic.annotation.gff3 \:` specifies the location of the genome annotation file to be used to improve alignment accuracy.

`--sjdbOverhang 42:` specifies the size of the splice overhang (or overextension). In this case, it is set to 42, which refers to the size of the read fragment minus 1. 


This is how the following files were obtained as output:
