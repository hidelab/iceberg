# Installing pathprint

pathprint can be installed from bioconductor.
 
GMAfunctions needs to be installed from Gabriel’s source code.
They are in /data/md4ga/fingerprint/package.

They can be installed using R CMD INSTALL in terminal or install.packages in R.

```
module load apps/R/3.3.1
R
```

```{r}
source("https://bioconductor.org/biocLite.R")
biocLite("pathprint")
biocLite("pathprintGEOData")
 
setwd("/data/md4ga/fingerprint/package")
install.packages("GMAfunctions_1.2.3.tar.gz")
```
