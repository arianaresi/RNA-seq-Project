## **MultiQC trimmed files**

And to speed up the analysis of the qualities, we perform the multiqc with a scheduled job.

```{bash multiqc trimmed, eval=FALSE}
module load multiqc/1.5
cd /mnt/Guanina/bioinfo24/Equipo_rosa/fastQC_trimmed
#
# Write your commands in the next line
multiqc /mnt/Guanina/bioinfo24/Equipo_rosa/fastQC_trimmed
multiqc /mnt/Guanina/bioinfo24/Equipo_rosa/raw_data/quality_fastqc/
```

For the sake of efficiency, we have omitted the complete script structure from the report.

### **Per Base Sequence Quality Scores - trimmed**

The graph shows that there is a call accuracy base of 99.9%, which is a satisfactory level of sequence quality.
![](https://github.com/arianaresi/RNA-seq-Project/blob/main/Trimming/Images/fastqc_per_base_sequence_quality_trimmed.png)


### **Sequence Length Distribution - trimmed**

After trimming, since the minimum length is specified as 40 bp, now the read length range is between 40bp to 43 bp.
![](https://github.com/arianaresi/RNA-seq-Project/blob/main/Trimming/Images/fastqc_sequence_length_distribution_trimmed.png)


### **Sequence Duplication Levels - trimmed**

The level of duplication was found to be maintained, this compared to the quality analysis of the raw data.
![](https://github.com/arianaresi/RNA-seq-Project/blob/main/Trimming/Images/fastqc_sequence_duplication_levels_trimmed.png)
