+++
title = "Special Usage of HTSanalyzeR2"

date = 2016-04-20
lastmod = 2018-04-11
draft = false

tags = ["caseStudy"]

summary = "hi"

[header]
image = "tutorials/case3.jpg"
caption = "[Image credit](https://www.123rf.com/photo_57637487_stock-vector-gears-and-case-study-mechanism.html)"
+++
---
<span id="top"></span>

{{% toc %}}


# Hypergeometric test with no phenotype

<p align="justify">In case if you only have a list of genes and want to do hypergeometric test with gene sets
having known functions, **HTSanalyzeR2** provides an interface to realize it. Since phenotype
is only used as background genes in hypergeometric test, you can manually set all the genes
of that species as phenotype and give them a pseudo value to fit **HTSanalyzeR2** as below:

```
data(d7)
hits1 <- d7$id[1:200]
## set all the coding genes of Homo sapiens as phenotype
allgenes <- keys(TxDb.Hsapiens.UCSC.hg19.knownGene, keytype = "GENEID")
## change Entrez ID to gene name to keep consistent with hits
allgenes <- mapIds(org.Hs.eg.db, keys = allgenes,
                   keytype = "ENTREZID", column = "SYMBOL")
                   
## give phenotype a pseudo value to fit for HTSanalyzeR2
phenotype <- rep(1, length(allgenes))
names(phenotype) <- allgenes
```
<p align="justify">Then, you can use the artificial phenotype as gene background and your hits to perform
hypergeometric test.

```
gsca <- GSCA(listOfGeneSetCollections=ListGSC,
             geneList=phenotype, hits=hits1)
## the following analysis is the same as before
```

[<i class="fa fa-hand-o-up fa-1x "></i>Top](#top)

---

# Customized gene set


<p align="justify">When you have your own gene sets with specific functions and they do not belong to any GO
terms, KEGG or MSigDB. In that case, you can set your customized gene set collection and
follow the format of GO, KEGG and MSigDB gene set collections. An important thing here
you need pay attention to is the ID of genes in the gene set collection must be Entrez ID.

```
## Suppose your own gene sets is geneset1 and geneset2
allgenes <- keys(org.Hs.eg.db, "ENTREZID")
geneset1 <- allgenes[sample(length(allgenes), 100)]
geneset2 <- allgenes[sample(length(allgenes), 60)]

## Set your custom gene set collection and make the format to fit HTSanalyzeR2
CustomGS <- list("geneset1" = geneset1, "geneset2" = geneset2)
## then the gene set collections would be as below:
ListGSC <- list(CustomGS=CustomGS)
## other part is the same as before
```

[<i class="fa fa-hand-o-up fa-1x "></i>Top](#top)

---

# An interface to fgsea package

<p align="justify">HTSanalyzeR2 also provides an interface to [fgsea](http://bioconductor.org/packages/release/bioc/html/fgsea.html) package which proposes a novel algorithm
for fast preranked gene set enrichment analysis using cumulative statistic calculation. Details
please see [fgsea](http://bioconductor.org/packages/release/bioc/html/fgsea.html) (Sergushichev (2016)).
To perform GSEA by **fgsea** instead of HTSanlayzeR2, users need to specifiy the parameter
*GSEA*.by in analyze (for single data set) or analyzeGscaTS (for time series analysis) with
fgsea. Otherwise, it will use **HTSanalyzeR2** by default.

```
gsca4 <- analyze(gsca1,
                 para=list(pValueCutoff=0.05, pAdjustMethod="BH",
                           nPermutations=100, minGeneSetSize=150,
                           exponent=1),
                 doGSOA = TRUE, doGSEA = TRUE,
                 GSEA.by = "fgsea")
```

[<i class="fa fa-hand-o-up fa-1x "></i>Top](#top)

---

# Extract shared genes between enriched pathways and input gene list


<p align="justify">Once you’ve finished the GSEA or hypergeometric test, you may be interested in some
pathways and wonder which genes are shared by that pathway and you input gene list.

```
## Suppose you are interested in "growth factor activity" in 'Molecular Function',
## of Gene Ontology, We can retrieve the GO ID of this pathway:
GO_MFrslt <- getResult(gsca3)$HyperGeo.results$GO_MF
GOID <- rownames(GO_MFrslt[GO_MFrslt$Gene.Set.Term ==
                                             "growth factor activity", ])
                                             
## Then get the genes in this pathways
pathway_gene <- GO_MF[[GOID]]

## change Entrez ID to gene symbol
pathway_gene <- mapIds(org.Hs.eg.db, keys = pathway_gene,
                       keytype = "ENTREZID", column = "SYMBOL")
## 'select()' returned 1:1 mapping between keys and columns

## get the shared genes between this pathway and your input gene list
intersect(pathway_gene, hits)
## [1] "CTGF"    "EFEMP1" "FGF7"  "IGF1"  "INHBA" "NOV"  "OGN"
## [8] "CLEC11A" "CXCL12" "TGFB3" "THBS4" "VEGFC" "DKK1" "PDGFC"
```

[<i class="fa fa-hand-o-up fa-1x "></i>Top](#top)

---