
> R Studio 0.99.1251 이상 버젼 필요 (Build-Build Book 기능 포함)
> 
> Pandoc을 이용하여 Markdown 랜더링 

### 1. 패키지 설치 

```R
install.packages("devtools")
devtools::install_github("rstudio/bookdown")
```
> Devtools설치 에러시 : apt-get install libssl-dev
> xelatex 에러시 : apt-get install texlive-xetex

### 2. Rmd 문서 작성

###### 1. 설정 수정하기 
```r
site: bookdown::bookdown_site #고정값
output: bookdown::gitbook #고정값
```
>Tool-> Project Option -> Build tool -> Project build tools = website (확인, 필수??)

###### 2. index.Rmd 저장 

각 챕터는 하기 Naming 규칙으로 작성 
01-xxxx.Rmd (숫자로 order탐지)

챕터 Re-order하고 싶으면 _bookdown.yml 수정
* rmd_files: ["index.Rmd", 01-xxx.Rmd" ...]



### 3. RMD 파일 작성 

1. New Project로 "Version Control"-> git생성
2. 하기 index.Rmd파일 참고 하여 파일 작성/수정

> `#`(single sharp)제목으로 __각 챕터__ 구분 
 




### 4. 책 Build하기 
* Build 패널 클릭  (Environment, History 패널 옆)

> 해당 챕터만 수정 사항 보고 싶으면 `knitr` 이용하여 확인 

### 5. bookdoc.org에 출판 

`bookdown::publish_book()`


### [QnA]
###### 1. Python도 사용 가능한가?
*Rmarkdown이 기본적으로 다른 언어 지원, 하기 코드 정크로 사용 가능

\```{python}

print("hello world")

\```
###### 2. readthedown Rmd template(rmdformats package)과의 다른점은?
해당 패키지를 잘 안지 못하여 답변 불가 

###### 3. yaml 설정에 대한 추가 정보가 있는가?
https://bookdown.org/yihui/bookdown/yaml-options.html

###### 4. IEEE 저널 latex 템플릿과 연동 가능 한가?
* bookdown을 사용하는 것 보다 [rticles](https://github.com/rstudio/rticles) 패키지의 Template 사용 추천 

##### 5. sample code [4]
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
```
---

[1]: https://bookdown.org/
[2]: http://bookdown.io/
[3]: https://www.rstudio.com/resources/webinars/introducing-bookdown/
[4]: https://github.com/rstudio/bookdown-demo  (sample code)
[5]: https://bookdown.org/yihui/bookdown/