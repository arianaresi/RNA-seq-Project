### **FastQC raw data**

The next step is to evaluate the qualities of the downloaded sequences, this with the script that was run in a scheduled job:

```{bash fastqc raw data, eval=FALSE}
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
#You can edit the script since this line
#
# Your job name
$ -N fastqc
#
# Send an email after the job has finished
$ -m e
$ -M arianasilrgv@gmail.com
#
#
# If modules are needed, source modules environment (Do not delete the next line):
. /etc/profile.d/modules.sh
#
# Add any modules you might require:
#
module load fastqc/0.11.3
cd /mnt/Guanina/bioinfo24/Equipo_rosa/raw_data/fastq_files
#
# Write your commands in the next line

fastqc -o /mnt/Guanina/bioinfo24/Equipo_rosa/raw_data/fastq_files *.fastq
```

Since we have several samples, we prefer to evaluate the qualities in a multiqc. See file MultiQC_RawData.md
