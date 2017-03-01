---
layout:     post
author:     Christoph Broschinski
author_lnk: https://github.com/cbroschinski
title:      Analysing hybrid Elsevier articles for correct access rights
date:       2017-02-23 06:00:00
summary:    
categories: [general, openAPC]
comments: true
---


Having read Ross Mounce's interesting [article](http://rossmounce.co.uk/2017/02/20/hybrid-open-access-is-unreliable/) on wrongly paywalled Open Access articles in hybrid Elsevier journals, 
I came up with the idea of throwing a bit more data at the issue. We have a lot of those articles in our OpenAPC data collection ([2630 articles in 670 different journals, to be precise](https://treemaps.intact-project.org/apcdata/openapc/#publisher/Elsevier%20BV/is_hybrid=TRUE)),
and since the contributing institutions reported their APC costs for all of them, we can be pretty confident that they were all paid for and none should be paywalled at the moment.

So, after fiddling around with some regular expressions and the structure of the landing pages at sciencedirect.com, I came up with a small [python script](https://github.com/OpenAPC/openapc-de/blob/master/python/sciencedirect_check_oa.py) which does the following:

* Extract all hybrid Elsevier articles from our collection
* Resolve the DOI for every article (will lead to a landing page at sciencedirect.com)
* Scrape the page content
* Use regexes to search for a PDF download link

Resolving and obtaining the page contents is quite time consuming, so the whole process took some hours. Here is a screenshot of the script's output while being busy:

![screenshot of the test script while running](/figure/elsevier_oa_check_running.png)

All green at the University of Bristol - but Elsevier is not off the hook yet. :-)
The script collects all negative results and prints out a concise summary after finishing. So let's have a look at the bottom line:

![screenshot of the test script after finishing](/figure/elsevier_oa_check_finished.png)

Surprise - 6 articles out of 2630 (or about 0.23%) were still hidden behind a paywall where it should not be the case according to our data. 

Here is a detailed overview of the articles in question:

|institution               | period | APCs paid (€)| DOI                                                                          | journal                                |
|:-------------------------|--------|--------------|------------------------------------------------------------------------------|----------------------------------------|
|~~Wellcome Trust~~            | ~~2015~~   | ~~1829.97~~      | ~~[10.1016/j.jth.2015.04.502](https://doi.org/10.1016/j.jth.2015.04.502)~~ [10.1016/j.jth.2015.06.005](https://doi.org/10.1016/j.jth.2015.06.005)       | ~~Journal of Transport & Health~~          |
|~~University College London~~ | ~~2014~~   | ~~822.53~~       | ~~[10.1016/j.jns.2013.01.022](https://doi.org/10.1016/j.jns.2013.01.022)~~       | ~~Journal of the Neurological Sciences~~   |
|University College London (_confirmed case_) | 2014   | 2257.64      | [10.1378/chest.13-0179](https://doi.org/10.1378/chest.13-0179)               | Chest                                  |
|University of Glasgow     | 2014   | 1882.5       | [10.1016/j.renene.2014.11.024](https://doi.org/10.1016/j.renene.2014.11.024) | Renewable Energy                       |
|~~University of Cambridge~~   | ~~2015~~   | ~~2294.44~~      | ~~[10.1016/j.epsl.2014.11.034](https://doi.org/10.1016/j.epsl.2014.11.034)~~     | ~~Earth and Planetary Science Letters~~    |
|University of Milan       | 2016   | 400          | [10.1016/j.puhe.2016.10.024](https://doi.org/10.1016/j.puhe.2016.10.024)     | Public Health                          |

&nbsp; 


To be fair, while we can clearly tell that something is wrong here, it's too early to lay the blame on Elsevier yet. 
Five of the items in question were part of aggregated data sets (The first one is from the [Wellcome Trust open data](https://github.com/OpenAPC/openapc-de/tree/master/data/wellcome), the next 4 articles from British universities were contained in the [JISC collections data](https://github.com/OpenAPC/openapc-de/tree/master/data/jisc_collections)), so it is quite possible that something went wrong during the aggregation process.
The article from Milan University has only been published this month, so maybe the transaction has not been fully processed yet and the full text will become available in the near future.

Nonetheless, this issue seems worth to investigate further. We will try to contact the involved institutions and see if we can shed some light upon this.

_Update, Mar 1, 2017:_

We have now cleared up 4 of the 6 cases:

* Number 1 turned out to be a false positive: Instead of the article DOI, a DOI belonging to the article abstract had been reported. The article itself is not paywalled. (Thanks to Ross Mounce for pointing this out)
* Number 2 remains somewhat unclear, but the UCL is positive that no APC has been paid for this article and there's also no UCL affiliated author on it. In any case the data is clearly incorrect and we have removed this entry from our collection.
* Number 5 is also a false positive: Cambridge had erroneously reported a page/colour charge as APC (Again, thanks to Ross for looking into this).

We have [corrected](https://github.com/OpenAPC/openapc-de/pull/232/commits/0079dd20) all of the entries mentioned above in our data collection.

* Number 3, however, turned out to be a true positive. The institution had paid an APC for this article in March 2014, so it is clearly incorrectly paywalled. The UCL will contact Elsevier and ask them to correct this case. 

As a side note, according to UCL's records the original payment was not payable to Elsevier, but to the [ACCP](https://www.accp.com/), and it seems the journal has moved to Elsevier since then. This is interesting as it identifies changes in journal ownership as another possible source of such mistakes.


