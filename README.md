jekyll blog openapc

## generate posts

Posts are written in `RMarkdown`. To generate posts, execute:

```
 R -e "knitr::knit('input.md', 'output.md')"
 ```

on the command line. You need to have R and the dependencies `knitr` and `ggplot2`installed.

## Example MPDL

```
 R -e "knitr::knit('_posts/mpdl_frontiers.Rmd', '_posts/2015-03-19-mpdl.md')"
```
