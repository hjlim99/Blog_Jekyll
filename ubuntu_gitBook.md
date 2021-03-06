# gitBook 설치 및 사용하기


### 0. Node.JS(npm) 사전 설치
```
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
apt-get install -y nodejs
apt-get install nodejs-legacy
npm install -g n --stable
node -v
> 에러시 : ln -s /usr/bin/nodejs /usr/bin/node
```
소스로 설치 
```
git clone http://github.com/isaacs/npm.git
cd npm
make install
```
### 1. 설치하기


터미널에서 다음 명령어로 프로젝트를 clone 한다.

```bash 
npm install -g gitbook-cli
gitbook build
gitbook serve
```
웹페이지를 통해 문서 확인 `http://localhost:4000`


> 샘플 문서 파일 : $ git clone https://github.com/umanji/umanji-docs.git

> 한글 메뉴얼 : [bluekms21](https://bluekms21.gitbooks.io/gitbookhelp_kr/content/)

### 2. 플러그인 적용

https://joygram.info/wp/?tag=gitbook

> 추천 플러그인 :  [mathjax](https://plugins.gitbook.com/plugin/mathjax), [code-highlighter](https://plugins.gitbook.com/plugin/code-highlighter), 

### 3. Rmarkdown 연계

R Studio에서 실행 
```
devtools::install_github("jbryer/Rgitbook")
require(Rgitbook)
installGitbook()
```

(옵션) 설치 실패시 Ubuntu 콘솔에서 `root`로 설치 
```bash
npm install gitbook -g
npm install gitbook-pdf -g
npm install gitbook-plugin
```

> 참고 : http://jason.bryer.org/Rgitbook/

> http://www.bookdown.org 
