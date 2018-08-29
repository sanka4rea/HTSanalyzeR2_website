+++
title = "Case Study 2: Time series analysis for CRISPR data"

date = 2016-04-20
lastmod = 2018-04-11
draft = false

tags = ["caseStudy"]

summary = "This case study uses a time series CRISPR genome-wide drop-out data as a demonstration to perform time series analysis."

[header]
image = "tutorials/case2.jpg"
caption = "[Image credit](https://positivepsychologylearning.com/case-study/)"
+++
---
<span id="top"></span>

{{% toc %}}

# Introduction

<p align="justify">This case study uses a time series CRISPR genome-wide drop-out data as a demonstration
to perform time series analysis. Data ‘d7’, ‘d13’ and ‘d25’ are three gRNA sequencing data
after transducting the CRISPR system into a human cancer cellline on day 7, day 13 and
day 25 separately (Tzelepis K (2016)), they are further preprocessed by [MAGeCK](https://sourceforge.net/p/mageck/wiki/Home/) to identify
significant essential genes from genome-scale CRISPR knockout screens. Again, here to simply
the compilation of this vignette, we skip the preprocessed steps and start from the results
gotten by MAGeCK.

---

# 1. Hypergeometric test and gene set enrichment analysis

## 1.1 Prepare the input data

<p align="justify">To perform analysis for time series data, one must prepare the following inputs:
<p align="justify">1. A character matrix contains experiment information with each experiment in row and
descriptions in column. Specifically, it should at least contain two columns named as
‘ID’ and ‘Description’.
<p align="justify">2. A list of phenotypes, each element of this list is a phenotype of that experiment. An
important thing here needs to be noted is the order of each element of this list
must match the order of ‘ID’ in the experiment information matrix.
<p align="justify">3. A list of gene set collections which can either be gotten by HTSanalyzeR2 or defined
by users using customized gene sets.

<p align="justify">To make it easy to compile this vignette, here we only use Biological Process (BP) in Gene
Ontology to make a demonstration.

```
data(d7, d13, d25)
expInfor <- matrix(c("d7", "d13", "d25"), nrow = 3, ncol = 2, byrow = FALSE,
                   dimnames = list(NULL, c("ID", "Description")))
datalist <- list(d7, d13, d25)

phenotypeTS <- lapply(datalist, function(x) {
  tmp <- as.vector(x$neg.lfc)
  names(tmp) <- x$id
  tmp
})

GO_BP <- GOGeneSets(species="Hs", ontologies=c("BP"))
ListGSC <- list(GO_BP=GO_BP)
```

<p align="justify">Similar as single dataset analysis, if you also want to do hypergeometric test, a list of hits
is needed. Here, each element of this list is a hits of that experiment. Also, **the order of each element of this list must match the order of ‘ID’ in the experiment information matrix.** Here, for each data set, we define genes with pvalue less than 0.01 as hits.

```
hitsTS <- lapply(datalist, function(x){
  tmp <- x[x$neg.p.value < 0.01, "id"]
  tmp
})
```

[<i class="fa fa-hand-o-up fa-1x "></i>Top](#top)

---

## 1.2 Initialize and preprocess

<p align="justify">To perform gene set enrichment analysis and hypermetric test for time-series data, an S4
class ‘GSCABatch’ which can pack the time series data to do further analysis is developed.
First, you need to create a new ‘GSCABatch’ object using the prepared inputs.


```
gscaTS <- GSCABatch(expInfor = expInfor,
                    phenotypeTS = phenotypeTS, listOfGeneSetCollections = ListGSC,
                    hitsTS = hitsTS)
```
<p align="justify">Then, the ‘GSCABatch’ object need to be preprocessed using preprocessGscaTS method. The
preprocess procedure here is the same as single data set. This step would return a list of
preprocessed ‘GSCA’ object.

```
gscaTS1 <- preprocessGscaTS(gscaTS, species="Hs", initialIDs="SYMBOL",
                            keepMultipleMappings=TRUE,
                            duplicateRemoverMethod="max",
                            orderAbsValue=FALSE)
```
[<i class="fa fa-hand-o-up fa-1x "></i>Top](#top)

---

## 1.3 Perform analysis

<p align="justify">After getting a list of preprocessed ‘GSCA’ object, you can use analyzeGscaTS to perform
hypergeometric test as well as GSEA on it. The parameters’ function here is the same as in
single data set. Similarly, to speed up you can use multiple cores via doParallel package. This
step would return a list of analyzed ‘GSCA’ object.

```
## analyze using 4 cores
if (requireNamespace("doParallel", quietly=TRUE)) {
    doParallel::registerDoParallel(cores=4)
} else {
}

gscaTS2 <- analyzeGscaTS(gscaTS1, para=list(pValueCutoff=0.05,
                                            pAdjustMethod="BH",
                                            nPermutations=100,
                                            minGeneSetSize=100,
                                            exponent=1),
                         doGSOA = TRUE, doGSEA = TRUE)
                         
## GSEA result of the first experiment usingBP gene sets
head(getResult(gscaTS2[[1]])$GSEA.results$GO_BP, 3)
```
<p align="justify">To make the result more understandable, users are highly recommended to annotate the gene
sets ID to names by function appendGSTermsTS. As a result, an additional column named
‘Gene.Set.Term’ would appear.

```
gscaTS3 <- appendGSTermsTS(gscaTS2, goGSCs=c("GO_BP"))
head(getResult(gscaTS3[[1]])$GSEA.results$GO_BP, 3)
##                    Gene.Set.Term         Observed.score  Pvalue
## GO:0006281          DNA repair             -0.6898409       0
## GO:0001525         angiogenesis            -0.1840823       0
## GO:0000398 mRNA splicing, via spliceosome  -0.8693455       0
##             Adjusted.Pvalue
## GO:0006281         0
## GO:0001525         0
## GO:0000398         0
```

<p align="justify">You can then use *reportAll* to generate an interactive Shiny report to visualize a union
enrichment map for this time series data. To put it more specific, a union enrichment map is
generated by taking the union of significant gene sets in each experiment and then form an
enrichment map as illustrated before. Thus there maybe be some gene sets not significant in
one time point but in others. More details please see Part4: An interactive Shiny report of
results.

[<i class="fa fa-hand-o-up fa-1x "></i>Top](#top)

---

# 2. Enriched subnetwork analysis

## 2.1 Prepare input, initialize and preprocess

<p align="justify">An S4 class named ‘NWABatch’ is developed to pack time series data for further subnetwork
analysis. You need first to create a new object of class ‘NWABatch’. To this end, a list of
pvalues is needed. Each element of this list is a vector of pvalues of that experiment. **Again, an important thing needs to be noted is the order of each element of this list must match the order of ‘ID’ in the experiment information matrix.** If a list of phenotypes
is also available, they can be inputted during the initialization stage and used to highlight
nodes with different colors in the identified subnetwork. Also, the order of each element of
this phenotypes list must match the order of ‘ID’ in the experiment information matrix.

```
pvalueTS <- lapply(datalist, function(x){
  tmp <- as.vector(x$neg.p.value)
  names(tmp) <- x$id
  tmp
})

## generate a new 'NWABatch' object for further analysis
nwaTS <- NWABatch(expInfor = expInfor,
                  pvalueTS = pvalueTS, phenotypeTS = phenotypeTS)
```

<p align="justify">After creating an object of ‘NWABatch’, a preprocessing step needs to be performed which
will return a list of preprocessed ‘NWA’ objects.


```
nwaTS1 <- preprocessNwaTS(nwaTS, species="Hs", initialIDs="SYMBOL",
                          keepMultipleMappings=TRUE,
                          duplicateRemoverMethod="max")
```

[<i class="fa fa-hand-o-up fa-1x "></i>Top](#top)

---

## 3.2 Perform analysis


<p align="justify">Similarly, an interactome needs to be created before performing subnetwork analysis using
*interactomeNwaTS* if you have not inputted your own interactome in the initial step. You can
either specify the species and fetch the corresponding network from BioGRID database, or input
an interaction matrix if it is in right format. More details please see *help(interactomeNwaTS)*.


<p align="justify">Then, *analyzeNwaTS* could perform the subnetwork analysis for a list of ‘NWA’ object, which
would take a few minutes. Finally, this step would return a list of analyzed ‘NWA’ objects.

```
nwaTS2 <- interactomeNwaTS(nwaTS1, species="Hs",
                           reportDir="HTSanalyzerReport", genetic=FALSE)
nwaTS3 <- analyzeNwaTS(nwaTS2, fdr=0.0001, species="Hs")
```
```
## get a general summary for the first experiment
summarize(nwaTS3[[1]])
```


<p align="justify">You can then use reportAll to generate an interactive Shiny report to visualize a union
subnetwork for this time series data. To put it more specific, a union subnetwork is generated
by taking the union of identified subnetwork in each experiment. Thus there maybe be some
genes not identified in the subnetwork of one time point but in others. More details please
see Part4: An interactive Shiny report of results.{to be modified}

[<i class="fa fa-hand-o-up fa-1x "></i>Top](#top)



---