---
layout:     post
author:     Christoph Broschinski
author_lnk: https://github.com/cbroschinski
title:      APC data harvested from Bielefeld University using the openCost format
date:       2025-09-03 07:00:00
summary:    
categories: [general, openAPC]
comments: true
---




New APC data has been harvested from the [institutional repository](https://pub.uni-bielefeld.de) of Bielefeld University. For the first time, the data has been transfered using the new [openCost](https://github.com/opencost-de/opencost/tree/main/doc) format.

[Bielefeld University Library](http://www.ub.uni-bielefeld.de/english/) is in charge of [Bielefeld University's Open Access Publishing Fund](http://oa.uni-bielefeld.de/en/publikationsfonds.html), which receives support by the Deutsche Forschungsgemeinschaft (DFG) under its [Open-Access Publication Funding Programme](https://www.dfg.de/en/research_funding/programmes/infrastructure/lis/open_access/infrastructure_funding/).

Contact person is [Dirk Pieper](<mailto:oa.ub@uni-bielefeld.de>).

## Cost data



The new data set covers publication fees for 91 articles, total expenditure amounts to 253 214€ and the average fee is 2 783€. Please note that harvested BPCs are not included in this list, as they are aggregated in OpenAPC's [BPC](https://github.com/OpenAPC/openapc-de/blob/master/data/bpc.csv) data set.



|                                                       | Articles| Fees paid in EURO| Mean Fee paid|
|:------------------------------------------------------|--------:|-----------------:|-------------:|
|Frontiers Media SA                                     |       20|             61076|          3054|
|Springer Nature                                        |       17|             42764|          2516|
|MDPI AG                                                |       11|             28291|          2572|
|Oxford University Press (OUP)                          |        9|             36380|          4042|
|Elsevier BV                                            |        8|             15174|          1897|
|Wiley-Blackwell                                        |        8|             17426|          2178|
|Informa UK Limited                                     |        3|             11602|          3868|
|JMIR Publications Inc.                                 |        2|              5413|          2706|
|Optica Publishing Group                                |        2|              4674|          2337|
|AIP Publishing                                         |        1|              3136|          3136|
|American Chemical Society (ACS)                        |        1|              4866|          4866|
|American Physical Society (APS)                        |        1|              3221|          3221|
|American Psychological Association (APA)               |        1|              3422|          3422|
|American Society for Microbiology                      |        1|              1597|          1597|
|BMJ                                                    |        1|              3390|          3390|
|Institute of Electrical & Electronics Engineers (IEEE) |        1|              2111|          2111|
|International Union of Crystallography (IUCr)          |        1|               647|           647|
|Society for Neuroscience                               |        1|              3029|          3029|
|Ubiquity Press, Ltd.                                   |        1|               603|           603|
|World Scientific Pub Co Pte Ltd                        |        1|              4392|          4392|



## Overview

The overall APC data for Bielefeld now looks as follows:

### Fees paid per publisher (in EURO)

![plot of chunk tree_bielefeld_2025_09_03_full](/figure/tree_bielefeld_2025_09_03_full-1.png)

###  Average costs per year (in EURO)

![plot of chunk box_bielefeld_2025_09_03_year_full](/figure/box_bielefeld_2025_09_03_year_full-1.png)

###  Average costs per publisher (in EURO)

![plot of chunk box_bielefeld_2025_09_03_publisher_full](/figure/box_bielefeld_2025_09_03_publisher_full-1.png)

