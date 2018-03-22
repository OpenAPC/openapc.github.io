---
layout:     post
author:     Christoph Broschinski and Dirk Pieper
title:      Analysing the article coverage of offsetting contracts
date:       2018-03-21 08:00:00
summary:    
categories: [general, ESAC]
comments: true
---

## Introduction

As a result of the first [ESAC Offsetting Workshop 2016](http://esac-initiative.org/activities/offsetting-workshop-2016/), the [collection of articles](https://github.com/OpenAPC/openapc-de/tree/master/data/offsetting) published under offsetting contracts like the Springer Compact agreements has been established as a side project of OpenAPC. Data providers include the Austrian Academic Library Consortium (KEMÖ), the Max Planck Digital Library, VSNU / UKB for all Dutch universities, the Bibsam Consortium for Sweden and JISC Collections for the UK. The data collection starts with the first data from 2015, the years 2016 and 2017 are now completely available.

While those articles are not associated with cost data in the sense of APCs, they can still be aggregated and visualised with [treemaps](https://treemaps.intact-project.org/apcdata/offsetting/), using a simple numerical count as measurement. With the offsetting collection now covering more than 13,000 articles from 3 years, it became feasible to attempt measuring the coverage of offsetting contracts by answering 3 questions:

For every hybrid journal appearing in the offsetting data set:

1. How many articles have been published in a distinct period (usually a calendar year)?
2. How many of those were published Open Access?
3. How many of those were published under offsetting contracts?

The analysis is especially appealing for the Springer Compact agreements: Since all current project members are reporting their data to OpenAPC, the article base should be (almost) complete.
This would provide important insights up to which scope the articles financed through the mentioned offsetting contracts have increased the open access shares in Springer Compact journals and how offsetting is contributing to the goal of the OA2020 initiative to flip journals from the subscription system into open access.


## Method

While the idea itself is straightforward, obtaining the required data on journal publication numbers turned out to be tricky. Our first approach, inspired by the [Hybrid OA Monitor](https://najkoja.shinyapps.io/hybridoa/) of our former colleague Najko Jahn, was to make use of the [Crossref API](https://github.com/CrossRef/rest-api-doc). As an example, [this query](https://api.crossref.org/works?filter=issn:0938-7994,from-pub-date:2015-01-01,type:journal-article&facet=license:*) obtains journal metrics on one of the largest journals (in terms of offsetting articles) in our collection, [European Radiology](https://link.springer.com/journal/330), from 2015 up to now. Digging through the returned JSON structure manually is cumbersome, but the relevant information can be found quite easily:

```json
"license": {
    "value-count": 3,
        "values": {
            "http:\/\/www.springer.com\/tdm": 1263,
            "http:\/\/creativecommons.org\/licenses\/by\/4.0": 171,
            "http:\/\/creativecommons.org\/licenses\/by-nc\/4.0": 43
        }
    }
},
```

and

```json
"total-results": 1772,
```

So, according to Crossref 1,772 articles have been published in *European Radiology* from 2015 until the current date (March 21, 2018), with 214 of them being Open Access (indicated by the sum of all CC license occurences). While these results do not seem to be implausible, let's verify them by consulting a second source: SpringerLink, the publisher's own web portal which also features a journal search function. Using the same parameters, we get [this results page](https://link.springer.com/search?date-facet-mode=between&facet-journal-id=330&facet-end-year=2018&query=&facet-start-year=2015) for the total number of articles and [this one](https://link.springer.com/search?facet-journal-id=330&package=openaccessarticles&search-within=Journal&query=&date-facet-mode=between&facet-start-year=2015&facet-end-year=2018) for the number of OA articles. As of today we end up with 1,956 total articles and 272 of them being OA. So there's quite a spread in numbers, and unfortunately this is no exceptional case. Here are some more results for the 5 journals occuring most often in the offsetting dataset, also received on 2018-03-21:

| Journal                                   | # Articles (Crossref)| # Articles (SpringerLink)| # OA Articles (Crossref) | # OA Articles (SpringerLink) |
|:------------------------------------------|---------------------:|-------------------------:|-------------------------:|-----------------------------:|
| European Radiology                        |             1772     |           1956           |           214            |       272                    |
| Synthese                                  |             1117     |           1242           |           176            |       187                    |
| Diabetologia                              |             1098     |           1185           |           241            |       321                    |      
| J. of Autism and Developmental Disorders  |             1180     |           1371           |           132            |       174                    | 
| J. of Business Ethics                     |             1316     |           1859           |           119            |       142                    |


The results are clear: When it comes to journal metrics (both OA and total), Crossref data is too sketchy to rely on.

This brought us directly to our second approach: Using the statistics from SpringerLink instead of Crossref. Technically there are two ways to do this: The first is one is to download search result files from SpringerLink in CSV format and count the the number of entries within, the second one is to make use of [web scraping](https://en.wikipedia.org/wiki/Web_scraping) to directly read the results count from the search page. While this approach lead to an accurate count of articles, it had an unforseen drawback which rendered it unsuable in the end: The time frame of the articles on SpringerLink is not identical to the one in our collection. While the "period" field in the offsetting dataset relates to the acceptance date of an article, the date filter on SpringerLink relates to the print publication date, which usually occurs significantly later, often not until the next calendar year. In our experience there is no possibility to use another type of date as filter on SpringerLink, so simple usage of these numbers would lead to incorrect comparisons and thus is not an option.

In the end we had to include an additional normalisation step to make the dates compatible: This would include downloading the aforementioned CSV lists for every journal present in our dataset from SpringerLink, looking up every single offsetting article in those lists (via the DOI) and retreiving the print publication date. This would effectively convert our offsetting data to "Springer print publication time" and make it comparable to the SpringerLink journal metrics. We would then aggregate the articles into journals and years and create an [OLAP cube](https://olap.intact-project.org/cube/offsetting_coverage/aggregate) and a [treemap visualisation](https://treemaps.intact-project.org/apcdata/offsetting-coverage/#publisher/Springer%20Nature/). 

While this approach proved successful and made an analysis of offsetting coverage possible, there are 2 potential problems:

- Since the time frame of the *offsetting_coverage* dataset has been altered, it is no longer comparable to the [original offsetting collection](https://treemaps.intact-project.org/apcdata/offsetting/) in terms of years (for instance, *offsetting* lists 6,892 articles for the 2016 period in contrast to 5,113 articles in *offsetting_coverage*).
- It's not a catch-all solution, since it relies on Springer's web portal and search engine. A long-term approach should be based on a public, publisher-independent data source like Crossref, but as we saw this would likely require improvements in data comprehension and quality.

## Results

The following brief presentation of the results relates to the publication years 2016 and 2017, as the data for the above-mentioned facilities are completely available for these two years. In total, 13,941 items were placed in open access through the offsetting contracts mentioned above. This corresponds to 4.28% of the total number of articles in the Springer Compact Journals (326,008) during this period. We were able to find a total of 27,622 open access articles in the Springer Compact journals, which corresponds to a share of 8,47%. Thus, offsetting was responsible for just over half of all open access articles in the hybrid Springer Compact journals.

In a total of 500 Springer Compact journals, the open access articles were even financed exclusively by offsetting, but very few of these journals achieved ever higher open access shares. Only two journals from this group have an open access percentage greater than or equal to 50% (*Cambridge Journal of Evidence-Based Policing* with 66.67% and *The Astronomy and Astrophysics Review* with exactly 50%).

The following figure shows all hybrid Springer Compact journals with open access shares greater than or equal to 50%.

![table top offsetting journals](/figure/top_oa_journals_springer_compact.png) 

In 2017, at least one offsetting article was published in a total of 1,311 Springer Compact journals, of which only 13 journals achieved an open access share of greater than or equal to 50%. If one assumes 1,700 Springer Compact journals altogether (https://www.springer.com/en/open-access/springer-open-choice/springer-compact), no offsetting articles have been published in around 400 titles. Based on 1,700 Springer Compact journals in 2017, only 0.76% of the journals have achieved an open access share of greater than or equal to 50%.

Furthermore, we observe strong fluctuations within individual journals, especially when the open access shares are overall low. In 2017, for example, the journal *Psychotherapy Forum* had an open acces share of 95%. Of these, only 5.26% were caused by offsetting. In 2016, the same journal had an open access share of 10.71%, of which 100% was financed by offsetting.

The first interim conclusion is that offsetting has contributed to a significant increase in open access articles in some of the hybrid Springer Compact journals from 2016 to 2017. Around 24% of all Springer Compact journals do not appear to be relevant as publication sites for the scientific institutions involved in the offsetting contracts. So far, additional open access articles generated by offsetting are not enough to completely juggle individual journals into open access.
