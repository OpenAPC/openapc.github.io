---
layout:     post
author:     Christoph Broschinski
author_lnk: https://github.com/cbroschinski
title:      Data from Open APC Sweden included
date:       2017-09-18 08:00:00
summary:    
categories: [general, openAPC]
comments: true
---




In May 2016 the [National Library of Sweden](http://www.kb.se/Innovation/hjalp/english/) started their own [OpenAPC project](https://github.com/Kungbib/openapc-se) to collect cost data from Swedish HEIs. This data has now also been integrated into the original OpenAPC collection.

## Cost data



The ingested data covers publication fees for 1,550 articles published by Swedish institutions. Total expenditure amounts to 2 627 985€ and the average fee is 1 695€.

Note that OpenAPC did neither include articles already present in its [offsetting data collection](https://github.com/OpenAPC/openapc-de/tree/master/data/offsetting) nor articles with a cost of 0€, so the net intake is lower than what might be expected.

The following table and plots show a breakdown of the payments.

### Overview


|                                                              | Articles| Fees paid in EURO| Mean Fee paid|
|:-------------------------------------------------------------|--------:|-----------------:|-------------:|
|Springer Nature                                               |      300|            525237|          1751|
|Informa UK Limited                                            |      237|            382910|          1616|
|Elsevier BV                                                   |      189|            398022|          2106|
|Public Library of Science (PLoS)                              |      170|            229168|          1348|
|Wiley-Blackwell                                               |      154|            365093|          2371|
|MDPI AG                                                       |       89|             93635|          1052|
|Frontiers Media SA                                            |       66|            105230|          1594|
|Springer Science + Business Media                             |       58|             98118|          1692|
|Hindawi Publishing Corporation                                |       39|             17668|           453|
|Oxford University Press (OUP)                                 |       34|             69090|          2032|
|Royal Society of Chemistry (RSC)                              |       22|             37489|          1704|
|Copernicus GmbH                                               |       20|             25688|          1284|
|S. Karger AG                                                  |       16|             12042|           753|
|American Chemical Society (ACS)                               |       15|             22109|          1474|
|SAGE Publications                                             |       12|             17235|          1436|
|IOP Publishing                                                |       10|             21181|          2118|
|BMJ                                                           |        9|             18307|          2034|
|Institute of Electrical & Electronics Engineers (IEEE)        |        9|             11990|          1332|
|Resilience Alliance, Inc.                                     |        8|              8290|          1036|
|Cambridge University Press (CUP)                              |        6|             14592|          2432|
|Dove Medical Press Ltd.                                       |        6|             11450|          1908|
|Proceedings of the National Academy of Sciences               |        5|             11117|          2223|
|American Society of Plant Biologists (ASPB)                   |        4|              8485|          2121|
|OMICS Publishing Group                                        |        4|              3407|           852|
|Ovid Technologies (Wolters Kluwer Health)                     |        4|              6236|          1559|
|The Company of Biologists                                     |        4|             10936|          2734|
|The Royal Society                                             |        4|              7372|          1843|
|American Association for the Advancement of Science (AAAS)    |        3|              7288|          2429|
|American Dairy Science Association                            |        3|              7284|          2428|
|Geological Society of London                                  |        3|              5319|          1773|
|Impact Journals, LLC                                          |        3|              8193|          2731|
|AIP Publishing                                                |        2|              3138|          1569|
|Genetics Society of America                                   |        2|              3571|          1785|
|Scandinavian Journal of Work, Environment and Health          |        2|              3500|          1750|
|Scientific Research Publishing, Inc,                          |        2|              1939|           970|
|Wageningen Academic Publishers                                |        2|              3600|          1800|
|Academic Journals                                             |        1|               124|           124|
|American Association for Cancer Research (AACR)               |        1|              2641|          2641|
|American Meteorological Society                               |        1|              3500|          3500|
|American Society for Biochemistry & Molecular Biology (ASBMB) |        1|              3404|          3404|
|American Society for Clinical Investigation                   |        1|              2629|          2629|
|American Society for Microbiology                             |        1|              2314|          2314|
|American Society of Animal Science (ASAS)                     |        1|              2668|          2668|
|American Speech Language Hearing Association                  |        1|              2174|          2174|
|Bentham Science Publishers Ltd.                               |        1|               747|           747|
|BioResources                                                  |        1|               931|           931|
|Brill Academic Publishers                                     |        1|              1330|          1330|
|Canadian Center of Science and Education                      |        1|               265|           265|
|Canadian Science Publishing                                   |        1|              2833|          2833|
|Cappelen Damm AS - Cappelen Damm Akademisk                    |        1|               668|           668|
|CSIRO Publishing                                              |        1|              2488|          2488|
|e-Century Publishing Corporation                              |        1|              1017|          1017|
|Emerald                                                       |        1|              1138|          1138|
|Informa Healthcare                                            |        1|              3040|          3040|
|Inter-Research Science Center                                 |        1|              1550|          1550|
|International Union of Crystallography (IUCr)                 |        1|               907|           907|
|JMIR Publications Inc.                                        |        1|              2174|          2174|
|Mary Ann Liebert Inc                                          |        1|              2437|          2437|
|MyJove Corporation                                            |        1|              1578|          1578|
|Nature Publishing Group                                       |        1|              2400|          2400|
|Optical Society of America (OSA)                              |        1|              1757|          1757|
|Pensoft Publishers                                            |        1|               450|           450|
|Portland Press Ltd.                                           |        1|               652|           652|
|Sciedu Press                                                  |        1|               283|           283|
|Scientific Research Publishing                                |        1|                95|            95|
|Society for Sociological Science                              |        1|               590|           590|
|Symbiosis Group                                               |        1|               646|           646|
|The Endocrine Society                                         |        1|              1009|          1009|
|Trans Tech Publications                                       |        1|               239|           239|
|World Scientific Pub Co Pte Lt                                |        1|              1379|          1379|

### Fees paid per publisher (in EURO)

![plot of chunk tree_openapc_se_2017_09_18_full](/figure/tree_openapc_se_2017_09_18_full-1.png)

###  Average costs per year (in EURO)

![plot of chunk box_openapc_se_2017_09_18_year_full](/figure/box_openapc_se_2017_09_18_year_full-1.png)
