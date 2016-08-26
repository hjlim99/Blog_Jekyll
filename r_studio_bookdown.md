# R Studio와 bookdown.org를 이용한 Rmd 문서화 하기


###

### 1. 패키지 설치 

R 실행 

```R
install.packages("devtools")
devtools::install_github("rstudio/bookdown")
```


### 2. github 준비 
1. 새 Repository생성
2. https://github.com/rstudio/bookdown-demo 클론



### 3. RMD 파일 작성 

1. New Project로 "Version Control"-> git생성
2. 하기 index.Rmd파일 참고 하여 파일 작성/수정

> `#` 제목으로 각 챕터 구분 

```R
--- 
title: "A Minimal Book Example"
author: "Yihui Xie"
date: "`r Sys.Date()`"
site: bookdown::bookdown_site
output: bookdown::gitbook
documentclass: book
bibliography: [book.bib, packages.bib]
biblio-style: apalike
link-citations: yes
github-repo: rstudio/bookdown-demo
description: "This is a minimal example of using the bookdown package to write a book. The output format for this example is bookdown::gitbook."
---

# Prerequisites

This is a _sample_ book written in **Markdown**. You can use anything that Pandoc's Markdown supports, e.g., a math equation $a^2 + b^2 = c^2$.

For now, you have to install the development versions of **bookdown** from Github:

'''{r eval=FALSE}
devtools::install_github("rstudio/bookdown")
'''

Remember each Rmd file contains one and only one chapter, and a chapter is defined by the first-level heading `#`.

To compile this example to PDF, you need to install XeLaTeX.

''''{r include=FALSE}
# automatically create a bib database for R packages
knitr::write_bib(c(
  .packages(), 'bookdown', 'knitr', 'rmarkdown'
), 'packages.bib')
''''

```

### 4. 책 Build하기 
* Build 패널 클릭  (Environment, History 패널 옆)

### 5. bookdoc.org에 출판 

`bookdown::publish_book(render = "local")`


---

[1]: https://bookdown.org/
