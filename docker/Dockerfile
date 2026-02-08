# 1. Imagen base (R con Bioconductor ya listo)
FROM bioconductor/bioconductor_docker:RELEASE_3_18

# 2. Instalamos las herramientas de análisis que usarás
RUN R -e "BiocManager::install(c('DESeq2', 'ggplot2'))"

# 3. Indicamos donde trabajaremos
WORKDIR /data