## **Trimming**

The process relies in removing adapter sequences and low-sequencing-quality bases. In this case, we use a tool called Trimmomatic.

Trimmomatic multithreaded command line tool that can be used to trim and crop Illumina (FASTQ) data as well as to remove adapters. 
There are two major modes of the program: Paired end mode and Single end mode. The paired end mode will maintain correspondence of read pairs and also use the additional information contained in paired reads to better find adapter or PCR primer fragments introduced by the library preparation process. For this practice we make use of the Paired end mode.

```{bash trimming, eval=FALSE}
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
#$ -N trimming
#
# Send an email after the job has finished
#$ -m e
#$ -M arianasilrgv@gmail.com
#
# If modules are needed, source modules environment (Do not delete the next line):
. /etc/profile.d/modules.sh
#
# Add any modules you might require:
module load trimmomatic/0.33
cd /mnt/Guanina/bioinfo24/Equipo_rosa/raw_data/fastq_files/
#
# Write your commands in the next line
for i in *_1.fastq;
do echo
trimmomatic PE -threads 8 -phred33 $i "${i%_1.fastq}_2.fastq" \
/mnt/Guanina/bioinfo24/Equipo_rosa/data_trimmed/"${i%_1.fastq}_1_trimmed.fq" \
/mnt/Guanina/bioinfo24/Equipo_rosa/data_trimmed/"${i%_1.fastq}_1_unpaired.fq" \
/mnt/Guanina/bioinfo24/Equipo_rosa/data_trimmed/"${i%_1.fastq}_2_trimmed.fq" \
ILLUMINACLIP:/mnt/Guanina/bioinfo24/Equipo_rosa/data_trimmed/TruSeq3-PE-2.fa:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:20 MINLEN:40 \

done
```


This is a job that is dedicated to perform the trimming of each of the two paired end reads, with a specific line of code that we highlight and explain the values of each parameter.

**ILLUMINACLIP:/mnt/Guanina/bioinfo24/Equipo_rosa/data_trimmed/TruSeq3-PE-2.fa:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:20 MINLEN:40**

**Where:**

***ILLUMINACLIP:*** allows to cut adapters

***/mnt/Guanina/bioinfo24/Equipo_rosa/data_trimmed/TruSeq3-PE-2.fa:***  file containing the adapter sequences to be used for trimming the reads.

***TruSeq3-PE-2.fa:2:30:10***

**2:** represents the maximum number of differences allowed between the adapter sequence and the input readout. If the difference is greater than this value, the adapter will not be clipped.

**30:** indicates the palindromic clipping, which refers to the removal of adapters that are in the palindromic part of the sequence read.

**10:** specifies the allowed error rate for base matching between the adapter and the sequence read. If the error rate is greater than this value, the adapter will not be trimmed.

**LEADING:3** removes bases of quality less than 3 phred score from the 5' (start) of the read.

**TRAILING:3** removes bases of quality less than 3 prhed score from the 3' (end) of the read.

**SLIDINGWINDOW:4:20** performs a sliding window based trimming along the readout. Bases at the 3' end of the reading will be removed if the average quality of the window falls below the specified value. In this case, the window has a size of 4 and the minimum allowed average window quality is 20.

**MINLEN:40** specifies the minimum length of the reading after all trimming and cleaning operations have been applied. If a reading has a length less than this value, it will be discarded.


### **Trimming results**

To contextualize the trimming results, in order to have a better organization of the samples, we divided controls and treatments with the following names:

|        Control        |      Treatment     |
|-----------------------|--------------------|
|    C1_SRR15024190_1   |  T1_SRR15024193_1  |
|    C1_SRR15024190_2   |  T1_SRR15024193_2  |
|    C2_SRR15024191_1   |  T2_SRR15024194_1  |
|    C2_SRR15024191_2   |  T2_SRR15024194_2  |
|    C3_SRR15024192_1   |  T3_SRR15024195_1  |
|    C3_SRR15024192_2   |  T3_SRR15024195_2  |

After running the job, the following files were obtained as output:
![](https://github.com/arianaresi/RNA-seq-Project/blob/main/Trimming/Images/trimming_files.png)
