# Lietz's SNA data in Pajek format

At [SowiDataNet|datorium](https://data.gesis.org/sharing/#!Home), GESIS - Leibniz Institute for the Social Sciences, [Haiko Lietz](https://www.gesis.org/institut/mitarbeiterverzeichnis/person/haiko.lietz) provided his network data set [Social Network Science (1916-2012)](https://data.gesis.org/sharing/#!Detail/10.7802/1437) / [http://doi.org/10.7802/1437](http://doi.org/10.7802/1437).

Social Network Science (SNS) is the field concerned with studying social systems in a relational way from the perspectives of the social and natural sciences. This data set consists of 25,760 biographical records retrieved from the Web of Science, ranging from 1916 to 2012. Each publication belongs to one of five subfields. To facilitate analyses of the social aspect of SNS, the names of 45,580 distinct authors are provided, linked to the papers in 68,227 publication-author relations. Author names have been disambiguated semi-automatically. To enable analyses of the cultural aspect of SNS, 23,026 distinct linguistic concepts are provided. These concepts resemble words or word combinations extracted from titles (for all publication years) and from abstracts and author keywords (only for publications published after 1990/1991). They are linked to the papers in 202,181 publication-concept relations.

The data set was used in:

Lietz, Haiko. 2016. Scale-Free Identity: The Emergence of Social Network Science. Dissertation, University of Duisburg Essen, Faculty of Social Sciences.

We transformed the data into Pajek format files using the following R code:
```
> wdir <- "C:/Users/batagelj/Downloads/data/leitz/SN"
> setwd(wdir)
> source("C:\\Users\\batagelj\\work\\projects\\BM\\indirect\\Pajek.R")

> fp <- c(rep("character",2),rep("integer",2))
> T <- read.table("publications.txt",colClasses=fp,header=TRUE)
> W <- T[,1] 
> vector2clu(T$domain,Clu="domain.clu")
> vector2clu(T$year,Clu="year.clu")
> vector2clu(as.integer(factor(T$type)),Clu="type.clu")

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
The set of functions `Pajek.R` is available [here](https://raw.githubusercontent.com/bavla/Rnet/master/R/Pajek.R). We added a new function `uv2net`.

Pajek files are available in [`LietzSN.zip`](https://github.com/bavla/SocNet/raw/master/Lietz/LietzSN.zip). It contains the following files
* `WA.net` - authorship network: |W| = 25760,  |A| = 45580.
* `WK.net` - keywords network: |W| = 25760,  |K| = 23027; works without keywords are linked to the keyword `""`.
* `domain.clu` - domain partition of W;
* `year.clu` - year partition of W
* `type.clu` - type partition of W;  1-article,  2-book,  3-chapter.

The information on domain encoding is missing. Probably it is:
1. Social Psychology & Epidemiology
2. Economic Sociology
3. Social Network Analysis
4. Network Science
5. Computational Social Science

The plan is:
* WK: compare the results obtained for our data up to 2012 and this data + split phrases in this data and compare it as well 
* WA: compare the results obtained for our data up to 2012 and this data
