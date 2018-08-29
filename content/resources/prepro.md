+++
# Date this page was created.
date = "2018-04-11"

# Project title.
title = "Preprocessing"

weight = 10
# Project summary to display on homepage.
summary = "a preprocess step including invalid input data removing, duplication removing, initial gene identifiers converting to Entrez ID and phenotype ordering."

# Optional image to display on homepage (relative to `static/img/` folder).
image_preview = "resources/preprocessing.png"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning"]`
tags = ["preprocessing"]

# Optional external URL for project (replaces project detail page).
#external_link = "https://cityu-bioinformatics.netlify.com/tools/seq_new/sequence alignment/"


# Does the project detail page use math formatting?
math = false

# Optional featured image (relative to `static/img/` folder).
#[header]
#image = "headers/bubbles-wide.jpg"
#caption = "My caption :smile:"

#*[citation:](http://www.sequence-alignment.com/)*

+++
---

<span id="top"></span>

{{%toc%}}

### Prepare the input data

<p align="justify">To perform gene set enrichment analysis for single dataset, you must preprare the following inputs:<br>
1. a named numeric vector of phenotypes (normally this would be a vector of genes with
log2 fold change).<br>
2. a list of gene set collections (could be generated by HTSanalyzeR2 or use customized
gene sets).<br>
First you need to prepare a named phenotype.

```python
data(GSE33113_limma)
phenotype <- as.vector(GSE33113_limma$logFC)
names(phenotype) <- rownames(GSE33113_limma)
```
<p align="justify">Then, if you want to do hypergeometric test on a list of interested genes simultaneously, you need to define the ‘hits’ as your interested genes. For example, here we define the hits as genes with absolute log2 fold change greater than 1 and adjust p value less than 0.05. In this case, the names of phenotype, namely all the input genes, would be taken as the background gene list to perform hypergeometric test.

<p align="justify">Note:In cases if you want to do hypergeometric test with only a list of hits and no phenotype, **HTSanalyzeR2** can also realize it. For details please go to Part5: Special usage of HTSanalyzeR2.

```python
## define hits if you want to do hypergeometric test
hits <- rownames(GSE33113_limma[abs(GSE33113_limma$logFC) > 1 &
GSE33113_limma$adj.P.Val < 0.05, ])
```

<p align="justify">Then we must define the gene set collections. A gene set collection is a list of gene sets, each of which consists of a group of genes with a similar known function. **HTSanalyzeR2** provides facilities which greatly simplify the creation of up-to-date gene set collections including three Gene Ontology terms: Molecular Function (MF), Biological Process (BP), Cellular Component (CC) and KEGG pathways. Gene sets in a comprehensive molecular signatures database,MSigDB([Arthur Liberzon (2011)](https://doi.org/10.1093/bioinformatics/btr260)), for Homo Sapiens and Mus musculus are also provided. Here to simplify the demonstration, we will only use one GO, KEGG and one MSigDB gene set collection. To work properly, you need to choose the right species for your input genes. Besides, these gene set collections must be provided as a named list as below:

```python
## generate gene set collection
GO_MF <- GOGeneSets(species="Hs", ontologies=c("MF"))
PW_KEGG <- KeggGeneSets(species="Hs")
MSig_C2 <- MSigDBGeneSets(collection = "c2", species = "Hs")

## combine all needed gene set collections into a named list for further analysis
ListGSC <- list(GO_MF=GO_MF, PW_KEGG=PW_KEGG, MSig_C2=MSig_C2)
```

### Initialize and preprocess

<p align="justify">An S4 class named ‘GSCA’ is developed to perform hypergeometric test in order to find the gene sets sharing significant overlapping with hits. Gene set enrichment analysis, as described by Subramanian et al. ([Subramanian A (2005)](https://doi.org/10.1073/pnas.0506580102)), can also be conducted.

<p align="justify">To initialize a new ‘GSCA’ object, the previous prepared phenotype and a named list of gene sets collections are needed. In addition, as said before, if you also want to do hypergeometric test, ‘hits’ is needed.

```python
gsca <- GSCA(listOfGeneSetCollections=ListGSC,
            geneList=phenotype, hits=hits)
```

<p align="justify">Then a preprocess step including invalid input data removing, duplication removing by different methods, initial gene identifiers converting to Entrez ID and phenotype ordering needs to be performed to fit for the next analysis. See the help documentation of funciton preprocess for more details.

```python
gsca1 <- preprocess(gsca, species="Hs", initialIDs="SYMBOL",
keepMultipleMappings=TRUE, duplicateRemoverMethod="max",
orderAbsValue=FALSE)
```

[<i class="fa fa-hand-o-up fa-1x "></i>Top](#top)

---