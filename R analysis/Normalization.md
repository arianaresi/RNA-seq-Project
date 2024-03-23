## **Data normalization**

**Why is it necessary to normalization?**

Our data are subject to technical and biological biases that cause variability in the counts.

If we want to make comparisons of expression levels between samples it is necessary to adjust the data taking these biases into account.

  - Differential expression analysis

  - Data visualization

In general, whenever we are comparing expression between our data.


```{r normalization, eval=FALSE}

## ---------------- Normalizacion de los datos ----------------

# Opcion 2. regularized logarithm or rlog
# Normalizacion de las cuentas por logaritmo y podrias hacer el analisis usando$
ddslog <- rlog(dds, blind = F)

# Opcion 3. vsd
# Estima la tendencia de dispersion de los datos y calcula la varianza, hace un$
# cuentas con respecto al tamaño de la libreria
vsdata <- vst(dds, blind = F)

```

