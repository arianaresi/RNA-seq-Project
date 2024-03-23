## **Batch effect correction**

Batch effects are technical, non-biological factors that also affect variation in the resulting data, but they occur in batches of samples. A “batch” refers to an individual group of samples that are processed differently relative to other samples in the experiment.

This can often be prevented with good experimental design. When it cannot, there are computational approaches that can help.


```{r batch effect, eval=FALSE}
## ---------------- Deteccion de batch effect ----------------
# Almacenar la grafica
png(file = paste0(figdir, "PCA_rlog.png"))
plt <- plotPCA(ddslog, intgroup = "type")
print(plt)
dev.off()
```

It is a PCA with the data normalized with rlog and it looks like this:



```{r vsd, eval=FALSE}
# Almacenar la grafica
png(file = paste0(figdir, "PCA_vsd.png"))
plt <- plotPCA(vsdata, intgroup = "type")
print(plt)
dev.off()
```

It is a PCA with the data normalized with rlog and it looks like this:



```{r vsdata, eval=FALSE}
# Guardar la salida del diseno (vsdata)
save(metadata, vsdata, file = paste0(outdir, 'vst_treatment_vs_control.RData'))
```

We save the output of the vsdata design (normalized data with vst) and perform the data retrieval:


```{r res, eval=FALSE}
## ---------------- Obtener informacion Tratamiento/Control ----------------
# results(dds, contrast=c("condition","treated","untreated"))
res <- results(dds, name = "type_tratamiento_vs_control")
res
summary(res)

# Guardar los resultados
write.csv(res, file=paste0(outdir, 'DE_T_vs_C.csv'))
```

In addition, by summarizing res, we obtain the following:

Thus we combine normalization, DEG Analysis and batch effect correction in a single script named `DEG_analysis.R` avaiable in the path `/mnt/Guanina/bioinfo24/Equipo_rosa/scripts/scripts_R`.
