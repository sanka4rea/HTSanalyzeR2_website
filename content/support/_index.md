+++
title = "Support"
date = 2018-04-11
math = false
highlight = false

# Optional featured image (relative to `static/img/` folder).
[header]
image = ""
caption = ""

+++
---

<span id="top"></span>


{{%toc%}}

---

## **Supported Analysis:**


• Over-representation analysis<br>
• Gene set enrichment analysis<br>
• Enriched subnetwork analysis<br>
• Time series analysis<br>

---

## **Supported data types:**

• Gene list<br>
• Named phenotypes preprocessed from either [RNA-seq](https://en.wikipedia.org/wiki/RNA-Seq), [micro-array](https://en.wikipedia.org/wiki/Microarray), [RNAi](https://en.wikipedia.org/wiki/RNA_interference) or [CRISPR](https://en.wikipedia.org/wiki/CRISPR)<br>
• [‘Time Series’ data](https://en.wikipedia.org/wiki/Time_series)<br>

---

## **Supported ontologies/pathways:**

###  Gene Ontology: [GO](http://www.geneontology.org/)<br>

• Molecular function (MF)<br>
• Biological process (BP)<br>
• Cellular component (CC)<br>

###  Kyoto Encyclopedia of Genes and Genomes pathways: [KEGG](http://www.genome.jp/kegg/)

###  Molecular Signatures Database: [MSigDB v6.1](http://software.broadinstitute.org/gsea/msigdb/index.jsp)<br>

• h: hallmark gene sets<br>
• c1: positional gene sets<br>
• c2: curated gene sets<br>
• c3: motif gene sets<br>
• c4: computational gene sets<br>
• c5: GO gene sets<br>
• c6: oncogenic signatures<br>
• c7: immunologic signatures<br>

###  Customized gene sets<br><br>

---

## **Supported species:**

• Gene Ontology and KEGG gene sets support any species that have an **OrgDb** object in
[Bioconductor](http://bioconductor.org/packages/release/BiocViews.html#___OrgDb).<br>
• MSigDB gene sets only support all 8 gene set collections for [Homo Sapiens](https://en.wikipedia.org/wiki/Homo_sapiens) and three
gene set collections: ‘c2’, ‘c6’ and ‘c7’ for [Mus musculus](https://en.wikipedia.org/wiki/House_mouse).<br>

---

## **Visualization:**


• GSEA plot<br>
• Enrichment map<br>
• Enriched subnetwork<br>
• Interactive report for all results<br><br>
Before starting the demonstration, you need to install and load the following packages:<br>

> library(HTSanalyzeR2)<br>
> library(org.Hs.eg.db)<br>
> library(KEGGREST)<br>
> library(GO.db)<br>
> library(igraph)<br>
> library(TxDb.Hsapiens.UCSC.hg19.knownGene)<br>


[<i class="fa fa-hand-o-up fa-1x "></i>Top](#top)

