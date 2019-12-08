# Lietz's SNA data in Pajek format

SowiDataNet|datorium https://data.gesis.org/sharing/#!Home

https://data.gesis.org/sharing/#!Detail/10.7802/1437

Lietz, Haiko; GESIS - Leibniz Institute for the Social Sciences

https://www.gesis.org/institut/mitarbeiterverzeichnis/person/haiko.lietz

http://doi.org/10.7802/1437

Social Network Science (1916-2012):
Social Network Science (SNS) is the field concerned with studying social systems in a relational way from the perspectives of the social and natural sciences. This data set consists of 25,760 biographical records retrieved from the Web of Science, ranging from 1916 to 2012. Each publication belongs to one of five subfields. To facilitate analyses of the social aspect of SNS, the names of 45,580 distinct authors are provided, linked to the papers in 68,227 publication-author relations. Author names have been disambiguated semi-automatically. To enable analyses of the cultural aspect of SNS, 23,026 distinct linguistic concepts are provided. These concepts resemble words or word combinations extracted from titles (for all publication years) and from abstracts and author keywords (only for publications published after 1990/1991). They are linked to the papers in 202,181 publication-concept relations.

Lietz, Haiko. 2016. Scale-Free Identity: The Emergence of Social Network Science. Dissertation, University of Duisburg Essen, Faculty of Social Sciences.;


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

* a
* b
* c
