---
layout:     post
author:     Julia Bartlewski
author_lnk: https://github.com/jbartlewski
title:      GFZ Potsdam 2023 OAPK data integrated
date:       2025-02-25 10:00:00
summary:    
categories: [general, openAPC]
comments: true
---




The Forschungszentrum Jülich collects publication cost data from German institutions as part of the DFG programme "[Open Access Publication Funding](https://www.fz-juelich.de/en/zb/open-science/open-access/monitoring-dfg-oa-publication-funding)".

When reporting their publication costs, the [GFZ](https://www.gfz.de/en/) (German Research Centre for Geosciences) had agreed to share the data with OpenAPC as well. This data has now been transferred and integrated.


## Cost data



The new data set covers publication fees for 94 articles, total expenditure amounts to 177 271€ and the average fee is 1 886€. Please note that articles published in **hybrid** journals under the DEAL agreements are not included in this list, as they are aggregated in OpenAPC's [transformative agreements](https://github.com/OpenAPC/openapc-de/tree/master/data/transformative_agreements) data set.

The following table provides an overview of the reported APCs: 




|                                           | Articles| Fees paid in EURO| Mean Fee paid|
|:------------------------------------------|--------:|-----------------:|-------------:|
|Copernicus GmbH                            |       22|             23405|          1064|
|Springer Nature                            |       15|             25706|          1714|
|Elsevier BV                                |       14|             40370|          2884|
|Frontiers Media SA                         |       10|             22373|          2237|
|MDPI AG                                    |        8|             15384|          1923|
|American Geophysical Union (AGU)           |        7|             12165|          1738|
|Wiley-Blackwell                            |        4|             10748|          2687|
|Seismological Society of America (SSA)     |        3|              4561|          1520|
|Oxford University Press (OUP)              |        2|              6090|          3045|
|Ubiquity Press, Ltd.                       |        2|              1146|           573|
|American Astronomical Society              |        1|              2423|          2423|
|American Society for Microbiology          |        1|              1111|          1111|
|American Society of Civil Engineers (ASCE) |        1|              2378|          2378|
|Cambridge University Press (CUP)           |        1|              3029|          3029|
|eLife Sciences Publications, Ltd           |        1|              1870|          1870|
|Informa UK Limited                         |        1|              2180|          2180|
|Society of Economic Geologists             |        1|              2333|          2333|



### Additional Costs



The new data also contained additional cost information for 2 publications. The following plot shows the distribution between APCs and additional costs for these 2 articles:


![plot of chunk additional_costs_gfz_2025_02_25_full](/figure/additional_costs_gfz_2025_02_25_full-1.png)


## Overview

With the recent contribution included, the overall APC data for the GFZ now looks as follows:

### Fees paid per publisher (in EURO)

![plot of chunk tree_gfz_2025_02_25_full](/figure/tree_gfz_2025_02_25_full-1.png)

###  Average costs per year (in EURO)

![plot of chunk box_gfz_2025_02_25_year_full](/figure/box_gfz_2025_02_25_year_full-1.png)

###  Average costs per publisher (in EURO)

![plot of chunk box_gfz_2025_02_25_publisher_full](/figure/box_gfz_2025_02_25_publisher_full-1.png)
