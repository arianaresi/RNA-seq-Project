## **R analysis**

### **Why do we want to do analysis in R?**

To be able to correct errors in sample preparation, library preparation and sequencing errors. It will also help us with differential expression analysis.

First, it is necessary to normalize the count data to account for differences in library size and RNA composition between samples. Next, we will use the normalized counts to make some plots for quality control at the gene and sample level. Finally, differential expression analysis is performed. 

### **Import data into R**

*All the code in the import data into R section is the same code, it is all run together, in this report it was separated into sections for visualization purposes.*

First of all, we must have our data (.out.tab) available for use in R, so we did de following script named `load_data_inR.txt`, avaiable in the path `/mnt/Guanina/bioinfo24/Equipo_rosa/scripts/scripts_R`:

```{r load_data_inR.txt, eval=FALSE}

# DE STAR A R

qlogin
cd /mnt/Guanina/bioinfo24/Equipo_rosa/STAR_output/STAR_output_R
module load r/4.0.2
R

# 1 Importar datos en R ___________________________________________________________________________________

indir <- "/mnt/Guanina/bioinfo24/Equipo_rosa/STAR_output/STAR_output_R"
outdir <- "/mnt/Guanina/bioinfo24/Equipo_rosa/results/"

files <- dir(pattern = "ReadsPerGene.out.tab")
files

counts <- c() # esta sera la matriz
for(i in seq_along(files)){
  x <- read.table(file = files[i], sep = "\t", header = F, as.is = T)
  # as.is para no convertir tipo de datos
  counts <- cbind(counts, x[,2])
}

head(counts)
dim(counts)

```


And it is visualized as follows:

### **Metadata**

This is how we obtained a new file called metadata.csv containing information about the columns/samples of our data. 

A metadata table can have, in addition to the sample names, clinical information, e.g. treatment, weight, type of feeding, disease (yes or no), etc.

These data are useful for further analysis, where we want to relate differential expression to a condition or conditions.


```{r load_data_inR.txt:metadata, eval=FALSE}
# Cargar Metadatos
metadata <- read.csv("/mnt/Guanina/bioinfo24/Equipo_rosa/scripts/scripts_R/metadata.csv", header = F)

# Renombrar columnas con el ID de los transcriptomas
metadata <- data.frame(sample_id = c("SRR15024190", "SRR15024191", "SRR15024192", "SRR15024193", "SRR15024194", "SRR15024195"),
                       type = c("control1", "control2", "control3", "trat1", "trat2", "trat3"))
colnames(metadata) <- c("sample_id", "type")
head(metadata)
```

It is visualized as follows:

```{r load_data_inR.txt:counts, eval=FALSE}
counts <- as.data.frame(counts)
rownames(counts) <- x[,1]
colnames(counts) <- sub("_ReadsPerGene.out.tab", "", files)
```


It is visualized as follows:


```{r eval=FALSE}
# Eliminar las 4 primeras filas ______________________________________________________________________________
counts <- counts[-c(1:4),]

#Guardar datos _______________________________________________________________________________________________

save(metadata, counts, file = paste0(outdir, "counts/raw_counts.RData"))
write.csv(counts, file = paste0(outdir,"counts/raw_counts.csv"))
```

It is visualized as follows:

The results of the command `write.csv(counts, file = paste0(outdir,"counts/raw_counts.csv"))` were saved in `/mnt/Guanina/bioinfo24/Equipo_rosa/results/counts`, with the following display if we do `less raw_counts.csv`: 

It is visualized as follows:

- Each row begins with the name of a gene, followed by a list of expression counts for that gene in each of the samples.

- Each column begins with the name of a sample, followed by the expression counts for each of the genes in that sample.

    For example, in the first row, the gene "ENSG00000290825.1" has an expression count of 0 in all samples ("SRR15024190",     "SRR15024191", ..., "SRR15024195").


<div class="alert alert-block alert-info">
***Important note: the DEG Analysis, normalization and batch effect sections go together, i.e. the parts of R code provided go in one code.***</div>
