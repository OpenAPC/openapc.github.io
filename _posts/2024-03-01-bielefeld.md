---
layout:     post
author:     Christoph Bartlewski
author_lnk: https://github.com/cbroschinski
title:      New APC data harvested from Bielefeld University using the openCost data format
date:       2024-03-01 14:00:00
summary:    
categories: [general, openAPC]
comments: true
---



New APC data has been harvested from the [institutional repository](https://pub.uni-bielefeld.de) of Bielefeld University, which had shifted to APC data provision via OAI-PMH. The data has been delivered in the [openCost format](https://github.com/opencost-de) for publication cost data.

[Bielefeld University Library](http://www.ub.uni-bielefeld.de/english/) is in charge of [Bielefeld University's Open Access Publishing Fund](http://oa.uni-bielefeld.de/en/publikationsfonds.html), which receives support by the Deutsche Forschungsgemeinschaft (DFG) under its [Open-Access Publication Funding Programme](https://www.dfg.de/en/research_funding/programmes/infrastructure/lis/open_access/infrastructure_funding/).

Contact person is [Dirk Pieper](<mailto:oa.ub@uni-bielefeld.de>).

## Cost data



The data ingestion covers publication fees for 1,294 articles, replacing the old harvest data for Bielefeld University. Total expenditure amounts to 2 220 862€ and the average fee is 1 716€.



|                                                            | Articles| Fees paid in EURO| Mean Fee paid|
|:-----------------------------------------------------------|--------:|-----------------:|-------------:|
|Springer Nature                                             |      365|            599209|          1642|
|Frontiers Media SA                                          |      311|            623571|          2005|
|MDPI AG                                                     |      262|            449764|          1717|
|Public Library of Science (PLoS)                            |      134|            203076|          1515|
|Wiley-Blackwell                                             |       51|             90324|          1771|
|Informa UK Limited                                          |       26|             41295|          1588|
|American Society for Microbiology                           |       14|             11677|           834|
|BMJ                                                         |       11|             24385|          2217|
|Cogitatio                                                   |       10|              3360|           336|
|Elsevier BV                                                 |       10|             19661|          1966|
|Oxford University Press (OUP)                               |        9|             19556|          2173|
|Association for Research in Vision and Ophthalmology (ARVO) |        8|             12294|          1537|
|Scientific Research Publishing, Inc.                        |        7|              7721|          1103|
|IOP Publishing                                              |        5|              6444|          1289|
|SAGE Publications                                           |        5|              5755|          1151|
|JMIR Publications Inc.                                      |        4|             10964|          2741|
|American Association for the Advancement of Science (AAAS)  |        3|             10382|          3461|
|Hindawi Publishing Corporation                              |        3|              3263|          1088|
|OMICS Publishing Group                                      |        3|              4107|          1369|
|Optica Publishing Group                                     |        3|              6415|          2138|
|PeerJ                                                       |        3|              3118|          1039|
|Syncsci Publishing Pte., Ltd.                               |        3|              1807|           602|
|The Royal Society                                           |        3|              3823|          1274|
|Ubiquity Press, Ltd.                                        |        3|              2258|           753|
|AIP Publishing                                              |        2|              2970|          1485|
|American Chemical Society (ACS)                             |        2|              2673|          1336|
|American Physical Society (APS)                             |        2|              4231|          2116|
|Cambridge University Press (CUP)                            |        2|              3879|          1940|
|Copernicus GmbH                                             |        2|              3641|          1820|
|eLife Sciences Publications, Ltd                            |        2|              5653|          2826|
|Eurasian Society of Educational Research                    |        2|              1245|           622|
|Hogrefe Publishing Group                                    |        2|              3480|          1740|
|Royal Society of Chemistry (RSC)                            |        2|              2402|          1201|
|University of Bern                                          |        2|               785|           392|
|American Medical Association (AMA)                          |        1|              3284|          3284|
|Brill                                                       |        1|               744|           744|
|Crimson Publishers                                          |        1|               424|           424|
|E.U. European Publishing                                    |        1|              1184|          1184|
|EMBO                                                        |        1|              4284|          4284|
|F1000 Research, Ltd.                                        |        1|               530|           530|
|Institute of Electrical & Electronics Engineers (IEEE)      |        1|              1732|          1732|
|Korean Society for Microbiology and Biotechnology           |        1|              1026|          1026|
|Life Science Alliance, LLC                                  |        1|              2313|          2313|
|MIT Press - Journals                                        |        1|               845|           845|
|Optical Society of America (OSA)                            |        1|              2045|          2045|
|Österreichische Akademie der Wissenschaften                 |        1|              1011|          1011|
|Science Publishing Group                                    |        1|              1250|          1250|
|Scientific & Academic Publishing                            |        1|               139|           139|
|SEAS - Society for South East Asian Studies                 |        1|               714|           714|
|The Company of Biologists                                   |        1|              2380|          2380|
|Vilnius Gediminas Technical University                      |        1|              1531|          1531|
|Walter de Gruyter GmbH                                      |        1|               238|           238|



## Overview

The overall APC data for Bielefeld now looks as follows:

### Fees paid per publisher (in EURO)

![plot of chunk tree_bielefeld_2024_03_01_full](/figure/tree_bielefeld_2024_03_01_full-1.png)

###  Average costs per year (in EURO)

![plot of chunk box_bielefeld_2024_03_01_year_full](/figure/box_bielefeld_2024_03_01_year_full-1.png)

###  Average costs per publisher (in EURO)

![plot of chunk box_bielefeld_2024_03_01_publisher_full](/figure/box_bielefeld_2024_03_01_publisher_full-1.png)

