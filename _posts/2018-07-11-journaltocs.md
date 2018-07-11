---
layout:     post
author:     Christoph Broschinski
author_lnk: https://github.com/cbroschinski
title:      Analysing JournalTOCs as a possible source of journal hybrid status
date:       2018-07-11 08:00:00
summary:    
categories: [general, openAPC]
comments: true
---





One of OpenAPC's key features is the usage of many external information providers for automated metadata enrichment, both to improve efficiency and to relieve our participating institutions from having to compile large sets of bibliographical data along with their reported articles.
Here's an overview of the whole process:

![openapc enrichment overview](/figure/openapc_enrichment_overview.svg)

Naturally we are always keeping a lookout for additional sources to simplify the ingestion process even more, and the most obvious candidate to be switched to an external import is the *is_hybrid* field. It is a simple boolean indicator which describes if the journal the article was published in is either Gold/Fully OA (*FALSE*) or hybrid (*TRUE*). 
Given that a classification scheme of journal OA types is a complex bibliometrical question, our distinction is necessarily very rough and the value *TRUE* should more or less be interpreted as "anything else than Gold OA" (It also includes journals with a delayed OA/moving wall policy, for example).

There are many approaches to create listings of gold OA journals (Most notably the [DOAJ](https://doaj.org) or [ROAD](http://road.issn.org/), but also compiled reports like the [ISSN Gold OA list](https://pub.uni-bielefeld.de/data/2906347) created by our colleagues at the INTACT OA analytics group) and there's some inclination to use those compilations as "inverted classifiers" ("If it's not on the list, it's not fully OA."), but in our experience this is no valid approach - in our daily work at OpenAPC we often stumble upon journals which are clearly OA but not part of any known list.
Our conclusion is that a source of journal OA types should go beyond a one-sided list and report explictly both on fully and hybrid OA status. 
Unfortunately, a service which holds the desired information (and offers a public API) seems hard to come by. 

At our OpenAPC workshop held on the German Librarians’ Day this year the [JournalTOCs](http://www.journaltocs.hw.ac.uk/) site was brought to our attention. As the name implies, the scope of this service is to provide metadata on journal contents (TOCs), but it also features a classification of journal types and it offers an API (free after registration).
Since this sounded promising, we went ahead and conducted an analysis of the API and data quality.

## Technical details

Out of the four different calls the [JournalTOCs API](http://www.journaltocs.ac.uk/develop.php) offers, the "Search for Journals" is what we are looking for. 
It accepts both journal titles and ISSNs and returns a list of possible matches along with some metadata.
The construction of queries is straightforward and the results are easy to parse and seem appropiate in terms of precision. However, there are two problems:

- At times the system fails to answer at all, leading to socket timeouts. This is no dealbreaker, but it requires careful monitoring and event handling when processing large batches of journals. 
- Unfortunately, the API does not return the journal type, which is the only piece of information we are interested in - the type can only be found on a journal's [individual landing page](http://www.journaltocs.ac.uk/index.php?journalID=11218). This forced us to construct a complicated workaround:
    - Search for a journal using a title string or ISSN
    - obtain the according journaltocID (an internal identifier)
    - Use the journaltocID to naviagte to the journal's landing page
    - Extract the journal type from HTML via web scraping

We wrote a small [python script](https://github.com/OpenAPC/openapc-de/blob/master/python/analysis/journaltocs/journaltoc_analysis.py) which implements this heuristic. As with all OpenAPC software it's placed under an MIT license, so feel free to reuse and adapt it.

## Analysis



When our analysis took place, the OpenAPC and offsetting data sets combined contained 6,210 unique journal titles. The _journal_full_title_ is not a perfect identifier since there are cases of titles belonging to different journals (For example there are two journals named "Medicine", one published by Elsevier and one by Wolters Kluwer), but those are so rare that we can ignore them.
In a preprocessing step, our script searched through the data and created a mapping table of all journal titles, associated ISSNs and hybrid status. 18 journals were identified as "flipped" (They were both TRUE and FALSE in the _is_hybrid_ column) and excluded from the data. For every journal, all ISSNs where looked up in JournalTOCs until the first hit.

### Coverage

Our first step was to determine the share of OpenAPC journals covered by JournalTOCs. 
We found that out of the 1629 fully OA journals in OpenAPC 1372 were also listed in JournalTOCs (84.22%), while the coverage of hybrid journals was 4376 out of 4563 (95.9%):



![](/figure/journaltocs_coverage.png)

These results were a bit surprising, as we would have expected OA journals being easier to discover and ingest. 
The following table lists the 15 OA journals occuring most often in OpenAPC which are not covered by JournalTOCs. There does not seem to be a distinctive pattern, so the reason for this phenomenon remains unclear.


|Title                                                     | Count|Publisher                                     |
|:---------------------------------------------------------|-----:|:---------------------------------------------|
|OncoTarget                                                |   216|Impact Journals, LLC                          |
|Genome Announcements                                      |    46|American Society for Microbiology             |
|Acta Crystallographica Section E Structure Reports Online |    42|International Union of Crystallography (IUCr) |
|Geoscientific Model Development Discussions               |    27|Copernicus GmbH                               |
|ACS Omega                                                 |    20|American Chemical Society (ACS)               |
|Natural Hazards and Earth System Sciences Discussions     |    16|Copernicus GmbH                               |
|Aging                                                     |    15|Impact Journals, LLC                          |
|Journal of new frontiers in spatial concepts              |    10|KIT Scientific Publishing                     |
|Annals of Transplantation                                 |     9|International Scientific Literature           |
|BioResources                                              |     9|BioResources                                  |
|International Journal of Electrochemical Science          |     9|ESG                                           |
|Journal of Psychiatry & Neuroscience                      |     9|Joule Inc.                                    |
|International Journal of Clinical & Medical Imaging       |     7|OMICS Publishing Group                        |
|Microbial Cell                                            |     7|Shared Science Publishers OG                  |
|British Journal of Psychiatry Open                        |     6|Royal College of Psychiatrists                |

### Journal status

The second part of our analysis focussed on the journal type as reported by JournalTOCs and if it's consistent with the classification in OpenAPC.

#### Hybrid journals

Ignoring all titles not listed in JournalTOCs, we get the following results for the 4376 journals categorized as hybrid in our data set:



![](/figure/hybrid_jtocs_type.png)

We listed a journal in the ERROR category when JournalTOCs failed to display an article list, because in that case a journal type indicator isn't shown as well.
As discussed before, out notion of a "hybrid" journal is fairly broad, so we can safely assume that the HYBRID, SUBSCRIPTION and PARTIALLY_FREE categories match our definition (They are clearly not Gold OA), so only the journals marked OA and FREE represent clear mismatches (40 cases, or 0.91% of our sample).
Again, here's a table of the 15 journals in question appearing most often in our data sets. To get a clearer picture on the situation, we performed a manual lookup of the journals to determine their real status:


|Title                                           | Count|JTOCs type |Real status              |
|:-----------------------------------------------|-----:|:----------|:------------------------|
|Semiconductor Science and Technology            |    12|OA         |Hybrid                   |
|Health Expectations                             |    10|OA         |OA                       |
|Journal of Leukocyte Biology                    |    10|OA         |Hybrid                   |
|Catalysis Science & Technology                  |     6|FREE       |Hybrid                   |
|Nucleus                                         |     6|OA         |OA                       |
|Bulletin of the American Meteorological Society |     5|OA         |status unclear           |
|Zeitschrift für Naturforschung B                |     3|OA         |Hybrid (flipped in 2015) |
|Annals of Pure and Applied Logic                |     2|OA         |Delayed OA (48 months)   |
|Big Data                                        |     2|OA         |Hybrid                   |
|Healthcare Technology Letters                   |     2|OA         |OA (flipped in 2017)     |
|Reproductive Medicine and Biology               |     2|OA         |OA (flipped in 2017)     |
|Research in the Mathematical Sciences           |     2|OA         |Hybrid (flipped in 2018) |
|Tumor Biology                                   |     2|OA         |OA (flipped in 2017)     |
|BioMolecular Concepts                           |     1|OA         |OA (flipped in 2018)     |
|Bulletin of the Veterinary Institute in Pulawy  |     1|OA         |OA                       |

#### Fully OA journals

We conducted the same kind of analysis for the journals classified as fully OA in OpenAPC (1372 titles, again ignoring those not listed in JournalTOCs):



![](/figure/oa_jtocs_type.png)

Here we focussed on the JournalTOCs types SUBSCRIPTION, HYBRID and PARTIALLY_FREE which indicate a mismatch. Again we did a manual lookup for the 15 titles appearing most often:



|Title                                             | Count|JTOCs type   |Real status            |
|:-------------------------------------------------|-----:|:------------|:----------------------|
|Journal of High Energy Physics                    |    31|HYBRID       |OA (flipped in 2014)   |
|Meteorologische Zeitschrift                       |    31|SUBSCRIPTION |OA (flipped in 2014)   |
|Clinical Epigenetics                              |    24|HYBRID       |OA                     |
|Journal of Clinical Investigation                 |    23|SUBSCRIPTION |status unclear         |
|Journal of Cancer                                 |     9|SUBSCRIPTION |OA                     |
|Microbiome                                        |     9|HYBRID       |OA                     |
|Gut Pathogens                                     |     8|SUBSCRIPTION |OA                     |
|Nanophotonics                                     |     5|HYBRID       |OA                     |
|The European Physical Journal C                   |     5|HYBRID       |OA (flipped in 2014)   |
|EPJ Techniques and Instrumentation                |     4|SUBSCRIPTION |OA                     |
|Geophysical & Astrophysical Fluid Dynamics        |     4|HYBRID       |Hybrid                 |
|International Journal of Advanced Robotic Systems |     4|SUBSCRIPTION |OA                     |
|Climate Research                                  |     3|HYBRID       |Delayed OA (48 months) |
|Health Education Research                         |     3|HYBRID       |Delayed OA (12 months) |
|Solid State Nuclear Magnetic Resonance            |     3|HYBRID       |Hybrid                 |

### Conclusion



Putting all our results together, we get the following chart:

![](/figure/jtoc_total_results.png)

To our mind we can draw the following conclusions:

- In general, JournalTOCs offers good data quality regarding journal types. Most classifications are in line with OpenAPC, and when there's a mismatch, our manual lookups show that errors are evenly spread between both collections. We can also see that many mismatches seem to be based on journals having recently flipped in their OA policy, so these cases might be more related to information being outdated than to initial misclassification.
- From an OpenAPC perspective, completeness is an issue. Out of 6192 OpenAPC journal titles, 482 (7.8%) were not listed in JournalTOCs. While this not a bad result in general, it would be a problem when trying to use JournaTOCs as source for the OpenAPC hybrid status in automated metadata enrichment (Our content policy requires each journal to be classified as hybrid or OA).
- Both completeness and classification quality in JournalTOCs seem to be a bit worse on OA journals.

The bottom line is that JournalTOCs is probably not a candidate for automated metadata enrichment of the journal hybrid status in OpenAPC, at least not on it's own. On the other hand it is clearly useful as an additional corrective, and it might still be useful as a source of the _is_hybrid_ status when combined with other sources (like the DOAJ or the ISSN Gold OA list). 

