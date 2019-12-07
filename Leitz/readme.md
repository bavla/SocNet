# Lietz's SNA data in Pajek format

https://www.gesis.org/institut/mitarbeiterverzeichnis/person/haiko.lietz

https://data.gesis.org/sharing/#!Detail/10.7802/1437

```
> wdir <- "C:/Users/batagelj/Downloads/data/leitz/SN"
> setwd(wdir)
> source("C:\\Users\\batagelj\\work\\projects\\BM\\indirect\\Pajek.R")

> fp <- c(rep("character",2),rep("integer",2))
> T <- read.table("publications.txt",colClasses=fp,header=TRUE)
> W <- T[,1] 
> vector2clu(T$domain,Clu="domain.clu")
> vector2clu(T$year,Clu="year.clu")
> vector2clu(as.integer(factor(T$type),Clu="type.clu")

> fp <- c(rep("integer",2),rep("character",2))
> T <- read.table("authorships.txt",colClasses=fp,header=TRUE)
> u <- factor(T$publication,levels=W)
> v <- factor(T$author)
> uv2net(u,v,Net="WA.net",twomode=TRUE)

> fp <- c(rep("integer",2),rep("character",2))
> T <- read.table("conceptUsages.txt",colClasses=fp,header=TRUE,fill=TRUE)
> u <- factor(T$publication,levels=W)
> v <- factor(T$concept)
> uv2net(u,v,Net="WK.net",twomode=TRUE)
```


