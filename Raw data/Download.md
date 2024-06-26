### **Download of raw data**

To download the sequences of the samples of the paper `Susceptibility of pediatric acute lymphoblastic leukemia to STAT3 inhibition depends on p53 induction`, we visited Gene Expression Omnibus web, where we found the title `Gene expression changes in REH following STAT3 pharmacological inhibition`, avaiable in: https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE179333.

Thus, we search with the ID of each sample in the ENA Browser, avaiable in: https://www.ebi.ac.uk/ena/browser/home.

Select the study where it says `Nucleotide sequences`, and in the lower table, in the column `Generated FASTQ files:FTP`, select the samples you want and left click on `Get download script`.

After obtaining the script to download the samples, we perform a scheduled job on the cluster, with the following script:


```{bash download raw data, eval=FALSE}
#!/bin/bash
# Use current working directory
#$ -cwd
#
# Join stdout and stderr
#$ -j y
#
# Run job through bash shell
#$ -S /bin/bash
#
#You can edit the scriptsince this line
#
# Your job name
#$ -N download_1
#
# Send an email after the job has finished
#$ -m e
#$ -M valeriacr1804@gmail.com
#
# If modules are needed, source modules environment (Do not delete the next line):
. /etc/profile.d/modules.sh
#
# Add any modules you might require:
# Write your commands in the next line
cd /mnt/Guanina/bioinfo24/Equipo_rosa/RNA_Seq_Proyecto/fastq_files/

# Control 1
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR150/090/SRR15024190/SRR15024190_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR150/090/SRR15024190/SRR15024190_2.fastq.gz

# Sample 1
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR150/093/SRR15024193/SRR15024193_1.fastq.gz
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR150/093/SRR15024193/SRR15024193_2.fastq.gz

# Control 2
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR150/091/SRR15024191/SRR15024191_2.fastq.gz \
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR150/094/SRR15024194/SRR15024194_2.fastq.gz \

# Sample 2
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR150/094/SRR15024194/SRR15024194_1.fastq.gz \
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR150/091/SRR15024191/SRR15024191_1.fastq.gz \

# Control 3
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR150/092/SRR15024192/SRR15024192_2.fastq.gz \
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR150/092/SRR15024192/SRR15024192_1.fastq.gz \

# Sample 3
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR150/095/SRR15024195/SRR15024195_1.fastq.gz \
wget -nc ftp://ftp.sra.ebi.ac.uk/vol1/fastq/SRR150/095/SRR15024195/SRR15024195_2.fastq.gz \

```
