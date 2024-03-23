## **Multiqc raw data**

Given that we have several samples, it is easy to analyze the qualities by performing a multiqc, a tool which aggregates results from bioinformatics analyses across many samples into a single report. Thus, we made the following scheduled job:

```{bash multiqc raw data, eval=FALSE}
# Use current working directory
#$ -cwd
#
# Join stdout and stderr
#$ -j y
#
# Run job through bash shell
#$ -S /bin/bash
#
#You can edit the script since this line
#
# Your job name
$ -N multiqc
#
# Send an email after the job has finished
#$ -m e
$ -M arianasilrgv@gmail.com
#
#
# If modules are needed, source modules environment (Do not delete the next line):
. /etc/profile.d/modules.sh
#
# Add any modules you might require:
#
module load multiqc/1.5
cd /mnt/Guanina/bioinfo24/Equipo_rosa/fastQC_rawData/
#
# Write your commands in the next line
multiqc /mnt/Guanina/bioinfo24/Equipo_rosa/raw_data/fastQC_rawData/quality_fastqc/

```

As **output** we obtained different files when running the scheduled job, such as:

- `multiqc_data.json`
- `multiqc_fastqc.txt`
- `multiqc_general_stats.txt` 
- `multiqc.log` 
- `multiqc_report.html` 
- `multiqc_sources.txt`

We will focus on the file with the .html ending, which contains a detailed quality report summarizing all the results of the analyses performed. 

**This file contains the following sections:**

- Sequence Quality Histograms
- Per Sequence Quality Scores
- Per Base Sequence Content
- Per Sequence GC Content
- Per Base N Content
- Sequence Length Distribution
- Sequence Duplication Levels
- Overrepresented sequences
- Adapter Content

To sum up, we had no major problems with the qualities of the RNA-seq samples, they came in a range of sequence lengths from 35 to 43 bp, and 12/12 samples had less than 1% of reads made up of overrepresented sequences. 
Now, we will concentrate on the specific analyses where we are interested in pointing out a few points. In Per Sequence Quality Scores, there is a call accuracy base of 99.2% to 99.9%, which is a satisfactory level of sequence quality.


### **Per Base Sequence Content**

Per Base Sequence Content plots out the proportion of each base position in a file for which each of the four normal DNA bases has been called. 
This module issues a warning if the difference between A and T, or G and C is greater than 10% in any position.  
Some of the reasons why this may occur include overrepresented sequences, biased fragmentation or biased composition libraries.

![](https://github.com/arianaresi/RNA-seq-Project/blob/main/Raw%20data/Images_RawData/per_base_content.png?raw=true)

### **Sequence Duplication Levels**

In this item, there are 9 samples with a failure and 3 with a warning.

According to Babraham Bioinformatics, in RNA-Seq libraries sequences from different transcripts will be present at wildly different levels in the starting population. In order to be able to observe lowly expressed transcripts it is therefore common to greatly over-sequence high expressed transcripts, and this will potentially create large set of duplicates. This will result in high overall duplication in this test, and will often produce peaks in the higher duplication bins. This duplication will come from physically connected regions, and an examination of the distribution of duplicates in a specific genomic region will allow the distinction between over-sequencing and general technical duplication, but these distinctions are not possible from raw fastq files. 

![](https://github.com/arianaresi/RNA-seq-Project/blob/main/Raw%20data/Images_RawData/fastqc_sequence_duplication_levels_plot.png)

### **Adapter Content**

In this section, 12/12 samples passed the indicated standards, where the proportions of adapters range from 0.1% to 3.15%.

![](https://github.com/arianaresi/RNA-seq-Project/blob/main/Raw%20data/Images_RawData/fastqc_adapter_content_plot.png)
