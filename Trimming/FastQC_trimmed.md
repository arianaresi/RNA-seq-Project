### **FastQC trimmed files**

Once the adapters and sequences with low quality have been removed, we perform again a fastqc and a multiqc to analyze their updated qualities.

Again we perform a scheduled job to obtain the fastqc.

```{bash fastqc trimmed, eval=FALSE}
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
$ -N fastqc_C2_T2
#
# Send an email after the job has finished
$ -m e
$ -M paurodriguez760@gmail.com
#
#
# If modules are needed, source modules environment (Do not delete the next line):
. /etc/profile.d/modules.sh
#
# Add any modules you might require:
#
module load fastqc/0.11.3
module load multiqc/1.5
cd /mnt/Guanina/bioinfo24/Equipo_rosa/data_trimmed/

# Write your commands in the next line

fastqc C1_SRR15024190_1_trimmed.fq -o /mnt/Guanina/bioinfo24/Equipo_rosa/fastQC_trimmed
fastqc C1_SRR15024190_2_trimmed.fq -o /mnt/Guanina/bioinfo24/Equipo_rosa/fastQC_trimmed
fastqc T1_SRR15024193_1_trimmed.fq -o /mnt/Guanina/bioinfo24/Equipo_rosa/fastQC_trimmed
fastqc T1_SRR15024193_2_trimmed.fq -o /mnt/Guanina/bioinfo24/Equipo_rosa/fastQC_trimmed

fastqc C2_SRR15024191_1_trimmed.fq -o /mnt/Guanina/bioinfo24/Equipo_rosa/fastQC_trimmed
fastqc C2_SRR15024191_2_trimmed.fq -o /mnt/Guanina/bioinfo24/Equipo_rosa/fastQC_trimmed
fastqc T2_SRR15024194_1_trimmed.fq -o /mnt/Guanina/bioinfo24/Equipo_rosa/fastQC_trimmed
fastqc T2_SRR15024194_2_trimmed.fq -o /mnt/Guanina/bioinfo24/Equipo_rosa/fastQC_trimmed


fastqc C3_SRR15024192_1_trimmed.fq -o /mnt/Guanina/bioinfo24/Equipo_rosa/fastQC_trimmed
fastqc C3_SRR15024192_2_trimmed.fq -o /mnt/Guanina/bioinfo24/Equipo_rosa/fastQC_trimmed
fastqc T3_SRR15024195_1_trimmed.fq -o /mnt/Guanina/bioinfo24/Equipo_rosa/fastQC_trimmed
fastqc T3_SRR15024195_2_trimmed.fq -o /mnt/Guanina/bioinfo24/Equipo_rosa/fastQC_trimmed

```
