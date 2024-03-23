## **Analysis of Functional Terms (GOterms)**

GOterms allows us to describe the biological functions of genes and proteins in organisms. It works with standardized terms to describe biological functions, processes and the components of the cell where all of the above takes place. This allows us to better interpret genetic data.



```{r GOterms, eval=FALSE}
#######
# Script : Analisis de terminos GO
# Author: Sofia Salazar, Diego Ramirez y Evelia Coss
# Date: 01/03/2024
# Description: El siguiente script nos permite realiza la Determinacion funcional de los genes diferencialmente expresados
# a partir de los datos provenientes del alineamiento de STAR a R,
# Primero correr el script "load_data_inR.R"
# Usage: Correr las lineas en un nodo de prueba en el cluster.
# Arguments:
#   - Input: metadata.csv, cuentas de STAR (Terminacion ReadsPerGene.out.tab)
#   - Output: Matriz de cuentas (CSV y RData)
#######

# qlogin
# module load r/4.0.2
# R
# rm(list=ls())

# --- Load packages ----------
library(gprofiler2)
library(enrichplot)
library(DOSE)
library(clusterProfiler)
library(ggplot2)
library(tidyverse)
library(dplyr)

# --- Load data -----
# Cargar archivos
indir <- "/mnt/Guanina/bioinfo24/Equipo_rosa/DEG_results/"
outdir <- "/mnt/Guanina/bioinfo24/Equipo_rosa/DEG_results/"
figdir <- '/mnt/Guanina/bioinfo24/Equipo_rosa/DEG_results/figures/'


# ---- Analisis de terminos Go ----
# Seleccionar bases de datos
sources_db <- c("GO:BP", "KEGG", "REAC", "TF", "MIRNA", "CORUM", "HP", "HPA", "WP")

# Seleccionar solo archivos CSV
files <- dir(indir, pattern = "^DE_(.+)\\.csv$")


# ---- Ejemplo de UN SOLO ARCHIVO --------
# Extraer el nombre del primer archivo
plot_name <- gsub("^DE_(.+)\\.csv$", "\\1",  files[1]) #name

# Cargar archivo
df <- read.csv(file = paste0(indir, files[1]), row.names = 'X')
head(df)


# Agregar informacion sobre la expresion
abslogFC <- 2 # Corte de 2 log2FoldChange
df <- df %>%
  dplyr::mutate(Expression = case_when(log2FoldChange >= abslogFC & padj < 0.05 ~ "Up-regulated",
                                       log2FoldChange <= -(abslogFC) & padj < 0.05 ~ "Down-regulated",
                                       TRUE ~ "Unchanged"))

```



For genes upregulated:
```{r UPregulated, eval=FALSE}
#OBTENER LOS NOMBRES DE LOS GENES
# > UP
up_genes <- df %>% filter(Expression == 'Up-regulated') %>%
  arrange(padj, desc(abs(log2FoldChange)))
# Extraer solo el nombre de los genes
up_genes <- rownames(up_genes)
tmp <- as.vector(up_genes)
tmp <- gsub("\\.[0-9]*", ".", up_genes)
head(tmp)

```



For genes downregulated:
```{r DOWNregulated, eval=FALSE}

# > DOWN
down_genes <- df %>% filter(Expression == 'Down-regulated') %>%
  arrange(padj, desc(abs(log2FoldChange)))
# Extraer solo el nombre de los genes
down_genes <- rownames(down_genes)
tmp2 <- as.vector(down_genes)
tmp2 <- gsub("\\.[0-9]*", ".", down_genes)
head(tmp2)

```


continuing with GOterms:

```{r, eval=FALSE}
#multi_gp <- gost(list("Upregulated" = tmp,
#                      "Downregulated" = tmp2),
#                 organism = 'hsapiens',
#                 evcodes = TRUE)

## ---- colors ---
# paleta de colores
#Category_colors <- data.frame(
#  category = c("GO:BP", "GO:CC", "GO:MF", "KEGG",
#               'REAC', 'TF', 'MIRNA', 'HPA', 'CORUM', 'HP', 'WP'),
#  label = c('Biological Process', 'Cellular Component', 'Molecular Function',  "KEGG",
#            'REAC', 'TF', 'MIRNA', 'HPA', 'CORUM', 'HP', 'WP'),
#  colors =  c('#FF9900', '#109618','#DC3912', '#DD4477',
#              '#3366CC','#5574A6', '#22AA99', '#6633CC', '#66AA00', '#990099', '#0099C6'))


```



Then, we made a Manhattan plot:

```{r Manhattan plot, eval=FALSE}
gostp1 <- gostplot(multi_gp, interactive = FALSE)

# Guardar grafica
ggsave(paste0(figdir, "ManhattanGO_", plot_name, ".png"),
       plot = gostp1, dpi = 300)

## ----Dataframe de todos los datos --------
# Convertir a dataframe
gost_query <- as.data.frame(multi_gp$result)

# Extarer informacion en modo matriz de todos los resultados
bar_data <- data.frame("term" = as.factor(gost_query$term_name), "condition" = gost_query$query,
                       "count" = gost_query$term_size, "p.adjust" = gost_query$p_value,
                       'category' = as.factor(gost_query$source), "go_id" = as.factor(gost_query$term_id),
                       'geneNames' = gost_query$intersection)

```
