---
layout:     post
author:     Christoph Broschinski
author_lnk: https://github.com/cbroschinski
title:      Analysing JournalTOCs as a possible source of journal hybrid status
date:       2018-06-28 08:00:00
summary:    
categories: [general, openAPC]
comments: true
---





One of OpenAPC's key features is the heavy usage of external information providers for automated metadata enrichment, both to improve efficiency and to relieve our participating institutions from having to compile large sets of bibliographical data along with their reported articles.
Here's an overview of the whole process:

![openapc enrichment overview](/figure/openapc_enrichment_overview.svg)

Naturally we are always keeping a lookout for additional sources to simplify the ingestion process even more, and the most obvious candidate to be switched to an external import is the *is_hybrid* field. It is a simple boolean indicator which describes if the journal the article was published in is either Gold/Fully OA (*FALSE*) or hybrid (*TRUE*). 
Given that a classification scheme of journal OA types is a complex bibliometrical question, our distinction is necessarily very rough and the value *TRUE* should more or less be interpreted as "anything else than Gold OA" (It also includes journals with a delayed OA/moving wall policy, for example).

There are many approaches to create listings of gold OA journals (Most notably the [DOAJ](https://doaj.org) or [ROAD](http://road.issn.org/), but also compiled reports like the [ISSN Gold OA list](https://pub.uni-bielefeld.de/data/2906347) created by our colleagues at the INTACT OA analytics group) and there's some inclination to use those compilations as "inverted classifiers" ("If it's not on the list, it can't be fully OA"), but in our experience this is no valid approach - in our daily work at OpenAPC we often stumble upon journals which are clearly OA but not part of any known list.
Our conclusion is that a source of journal OA types should go beyond a one-sided list and report explictly both on fully and hybrid OA status. 
Unfortunately, a service which holds the desired information (and offers a public API) seems hard to come by. 

At our OpenAPC workshop held on the German Librarians’ Day this year the [JournalTOCs](http://www.journaltocs.hw.ac.uk/) site was brought to our attention. As the name implies, the scope of this service is to provide metadata on journal contents (TOCs), but it also features a classficiation of journal types and it offers an API (free after registration).
Since this sounded promising, we went ahead and conducted an analysis of the API and data quality.



## 1. Analysis


|is_hybrid (OpenAPC) |jtocs status   | count|
|:-------------------|:--------------|-----:|
|FALSE               |ERROR          |    21|
|FALSE               |FREE           |     1|
|FALSE               |HYBRID         |    28|
|FALSE               |OA             |  1274|
|FALSE               |PARTIALLY_FREE |     2|
|FALSE               |SUBSCRIPTION   |    10|
|FALSE               |NA             |   250|
|TRUE                |ERROR          |    12|
|TRUE                |FREE           |     1|
|TRUE                |HYBRID         |  2754|
|TRUE                |OA             |    28|
|TRUE                |PARTIALLY_FREE |    37|
|TRUE                |SUBSCRIPTION   |   485|
|TRUE                |NA             |    82|

![plot of chunk unnamed-chunk-4](/figure/unnamed-chunk-4-1.png)![plot of chunk unnamed-chunk-4](/figure/unnamed-chunk-4-2.png)


