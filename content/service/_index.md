+++
title = "Service"
date = 2018-04-11
math = false
highlight = false

# Optional featured image (relative to `static/img/` folder).
[header]
image = ""
caption = ""

+++
---
{{% alert note %}}
[**Session info:**]
{{% /alert %}}

>\## R version 3.5.1 (2018-07-02)<br>
>\## Platform: x86_64-pc-linux-gnu (64-bit)<br>
>\## Running under: Ubuntu 18.04 LTS<br>
>\##
>\## Matrix products: default<br>
>\## BLAS: /usr/lib/x86_64-linux-gnu/openblas/libblas.so.3<br>
>\## LAPACK: /usr/lib/x86_64-linux-gnu/libopenblasp-r0.2.20.so<br>
>\##<br>
>\## locale:<br>
>\## [1] LC_CTYPE=en_US.UTF-8 LC_NUMERIC=C<br>
>\## [3] LC_TIME=en_US.UTF-8 LC_COLLATE=en_US.UTF-8<br>
>\## [5] LC_MONETARY=en_US.UTF-8 LC_MESSAGES=en_US.UTF-8<br>
>\## [7] LC_PAPER=en_US.UTF-8 LC_NAME=C<br>
>\## [9] LC_ADDRESS=C LC_TELEPHONE=C<br>
>\## [11] LC_MEASUREMENT=en_US.UTF-8 LC_IDENTIFICATION=C<br>
>\##<br>
>\## attached base packages:<br>
>\## [1] parallel stats4 stats graphics grDevices utils datasets<br>
>\## [8] methods base<br>
>\##<br>
>\## other attached packages:<br>
>\## [1] TxDb.Hsapiens.UCSC.hg19.knownGene_3.2.2<br>
>\## [2] GenomicFeatures_1.32.0<br>
>\## [3] GenomicRanges_1.32.3<br>
>\## [4] GenomeInfoDb_1.16.0<br>
>\## [5] igraph_1.2.1<br>
>\## [6] GO.db_3.6.0<br>
>\## [7] KEGGREST_1.20.0<br>
>\## [8] org.Hs.eg.db_3.6.0<br>
>\## [9] AnnotationDbi_1.42.1<br>
>\## [10] IRanges_2.14.10<br>
>\## [11] S4Vectors_0.18.3<br>
>\## [12] Biobase_2.40.0<br>
>\## [13] BiocGenerics_0.26.0<br>
>\## [14] HTSanalyzeR2_0.99.15<br>
>\## [15] BiocStyle_2.8.2<br>
>\##<br>
>\## loaded via a namespace (and not attached):<br>
>\## [1] fgsea_1.6.0 colorspace_1.3-2<br>
>\## [3] hwriter_1.3.2 rprojroot_1.3-2<br>
>\## [5] XVector_0.20.0 affyio_1.50.0<br>
>\## [7] DT_0.4 bit64_0.9-7<br>
>\## [9] mvtnorm_1.0-8 codetools_0.2-15<br>
>\## [11] splines_3.5.1 doParallel_1.0.11<br>
>\## [13] robustbase_0.93-1.1 knitr_1.20<br>
>\## [15] splots_1.46.0 Rsamtools_1.32.0<br>
>\## [17] prada_1.56.0 annotate_1.58.0<br>
>\## [19] cluster_2.0.7-1 Rmpfr_0.7-0<br>
>\## [21] vsn_3.48.1 png_0.1-7<br>
>\## [23] shinydashboard_0.7.0 graph_1.58.0<br>
>\## [25] shiny_1.1.0 rrcov_1.4-4<br>
>\## [27] compiler_3.5.1 httr_1.3.1<br>
>\## [29] backports_1.1.2 assertthat_0.2.0<br>
>\## [31] Matrix_1.2-14 lazyeval_0.2.1<br>
>\## [33] limma_3.36.2 later_0.7.3<br>
>\## [35] prettyunits_1.0.2 htmltools_0.3.6<br>
>\## [37] tools_3.5.1 gmp_0.5-13.2<br>
>\## [39] bindrcpp_0.2.2 GenomeInfoDbData_1.1.0<br>
>\## [41] gtable_0.2.0 glue_1.3.0<br>
>\## [43] affy_1.58.0 Category_2.46.0<br>
>\## [45] dplyr_0.7.6 fastmatch_1.1-0<br>
>\## [47] Rcpp_0.12.17 Biostrings_2.48.0<br>
>\## [49] preprocessCore_1.42.0 rtracklayer_1.40.3<br>
>\## [51] iterators_1.0.10 xfun_0.3<br>
>\## [53] stringr_1.3.1 mime_0.5<br>
>\## [55] miniUI_0.1.1.1 XML_3.98-1.12<br>
>\## [57] BioNet_1.40.0 DEoptimR_1.0-8<br>
>\## [59] zlibbioc_1.26.0 MASS_7.3-50<br>
>\## [61] scales_0.5.0 RankProd_3.6.0<br>
>\## [63] BiocInstaller_1.30.0 colourpicker_1.0<br>
>\## [65] hms_0.4.2 promises_1.0.1<br>
>\## [67] SummarizedExperiment_1.10.1 RBGL_1.56.0<br>
>\## [69] RColorBrewer_1.1-2 curl_3.2<br>
>\## [71] yaml_2.1.19 memoise_1.1.0<br>
>\## [73] gridExtra_2.3 ggplot2_3.0.0<br>
>\## [75] biomaRt_2.36.1 stringi_1.2.3<br>
>\## [77] RSQLite_2.1.1 genefilter_1.62.0<br>
>\## [79] cellHTS2_2.44.0 pcaPP_1.9-73<br>
>\## [81] foreach_1.4.4 BiocParallel_1.14.1<br>
>\## [83] matrixStats_0.53.1 rlang_0.2.1<br>
>\## [85] pkgconfig_2.0.1 bitops_1.0-6<br>
>\## [87] evaluate_0.11 lattice_0.20-35<br>
>\## [89] purrr_0.2.5 bindr_0.1.1<br>
>\## [91] GenomicAlignments_1.16.0 htmlwidgets_1.2<br>
>\## [93] bit_1.1-14 tidyselect_0.2.4<br>
>\## [95] GSEABase_1.42.0 plyr_1.8.4<br>
>\## [97] magrittr_1.5 bookdown_0.7<br>
>\## [99] R6_2.2.2 DelayedArray_0.6.1<br>
>\## [101] DBI_1.0.0 pillar_1.3.0<br>
>\## [103] survival_2.42-3 RCurl_1.95-4.11<br>
>\## [105] tibble_1.4.2 crayon_1.3.4<br>
>\## [107] rmarkdown_1.10 progress_1.2.0<br>
>\## [109] locfit_1.5-9.1 grid_3.5.1<br>
>\## [111] data.table_1.11.4 blob_1.1.1<br>
>\## [113] digest_0.6.15 xtable_1.8-2<br>
>\## [115] httpuv_1.4.5 munsell_0.5.0<br>


---
{{% alert note %}}
[**References:**]
{{% /alert %}}

Arthur Liberzon, Reid Pinchback, Aravind Subramanian. 2011. “Molecular Signatures
Database (Msigdb) 3.0.” Bioinformatics 27 (12): 1739–40. doi:[10.1093/bioinformatics/btr260](https://doi.org/10.1093/bioinformatics/btr260).<br>

Beisser, Klau, D. 2010. “BioNet: An R-Package for the Functional Analysis of Biological
Networks.” Bioinformatics 26 (8): 1129–30. doi:[10.1093/bioinformatics/btq089](https://doi.org/10.1093/bioinformatics/btq089).<br>

Dittrich MT, Rosenwald A, Klau GW. 2008. “Identifying Functional Modules in Protein–
Protein Interaction Networks: An Integrated Exact Approach.” Bioinformatics 24 (13):
i223–i231. doi:[10.1093/bioinformatics/btn161](https://academic.oup.com/bioinformatics/article/24/13/i223/231653).<br>

Guinney J, Wang X, Dienstmann R. 2015. “The Consensus Molecular Subtypes of Colorectal
Cancer.” Nature Medicine 21 (11): 1350–6. doi:[10.1038/nm.3967](https://www.nature.com/articles/nm.3967).<br>

Merico D, Stueker O, Isserlin R. 2010. “Enrichment Map: A Network-Based Method
for Gene-Set Enrichment Visualization and Interpretation.” PLoS ONE 5 (11): e13984.
doi:[10.1371/journal.pone.0013984](http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0013984).<br>

Sergushichev, Alexey. 2016. “An Algorithm for Fast Preranked Gene Set Enrichment Analysis
Using Cumulative Statistic Calculation.” bioRxiv. doi:[10.1101.060012](https://doi.org/10.1101/060012).<br>

Subramanian A, Mootha VK, Tamayo P. 2005. “Gene Set Enrichment Analysis: A
Knowledge-Based Approach for Interpreting Genome-Wide Expression Profiles.” Proceedings
of the National Academy of Sciences of the United States of America 102 (43): 15545–50.
doi:[10.1073/pnas.0506580102](https://doi.org/10.1073/pnas.0506580102). <br>

Tzelepis K, De Braekeleer E, Koike-Yusa H. 2016. “A Crispr Dropout Screen Identifies Genetic
Vulnerabilities and Therapeutic Targets in Acute Myeloid Leukemia.” Cell Reports 17 (4):
1193–1205. doi:[10.1016/j.celrep.2016.09.079](https://doi.org/10.1016/j.celrep.2016.09.079).<br>

