## **Differential gene expression (DGE) analysis**

The goal of differential expression testing is to determine which genes are expressed at different levels between conditions. These genes can offer biological insight into the processes affected by the condition(s) of interest.


```{r DEG analysis, eval=FALSE}
# Script : Analisis de expresion diferencial
# Author: Sofia Salazar, Diego Ramirez y Evelia Coss
# Date: 27/02/2024
# Description: El siguiente script nos permite realiza el Analisis de expresion Diferencial
# a partir de los datos provenientes del alineamiento de STAR a R,
# Primero correr el script "load_data_inR.R"
# Usage: Correr las lineas en un nodo de prueba en el cluster.
# Arguments:
#   - Input: Cargar la variable raw_counts.RData que contiene la matriz de cuentas y la metadata
#   - Output: DEG
#######

# qlogin
# module load r/4.0.2
# R

# --- Load packages ----------
library(DESeq2)

# --------------------- Load data ---------------------
# Cargar archivos
outdir <- "/mnt/Guanina/bioinfo24/Equipo_rosa/DEG_results"
figdir <- "/mnt/Guanina/bioinfo24/Equipo_rosa/DEG_results/figures/"

#Cargar variable "counts", proveniente del script "load_data_inR.R"
load("/mnt/Guanina/bioinfo24/Equipo_rosa/results/counts/raw_counts.RData")
samples <- Metadata$sample_id # Extraer los nombres de los Transcriptomas
metadata$type <- as.factor(Metadata$type) # convertir a factor


metadata$type <- as.factor(Metadata$type) # convertir a factor

counts <- counts[which(rowSums(counts) > 10),] #Seleccionamos genes con mas de $

# --------------------- DEG Analysis ---------------------

# Convertir al formato dds
dds <- DESeqDataSetFromMatrix(countData =  counts,
            colData = metadata, design = ~type)
dim(dds) # checar las dimensiones
```

It is visualized as follows:


```{r DEG dds, eval=FALSE}
#Asignar referencia:
dds$type <- relevel(dds$type, ref = "control")

## --- Obtener archivo dds ----
dds <- DESeq(dds)

# Obtener la lista de coeficientes o contrastes
resultsNames(dds)

# Guardar la salida del diseno
save(metadata, dds, file = paste0(outdir, 'dds_Treatment_vs_control.RData'))
```


It is visualized as follows:
