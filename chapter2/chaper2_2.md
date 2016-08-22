> 출처 : http://www.jopenbusiness.com/wordpress/?p=114

### 1. 자주 사용하는 RStudio 단축키와 명령
* Console 화면에서 Ctrl_l (Ctrl_소문자L) : 화면을 깨끗하게 지웁니다.
* Crm(list=ls(all=TRUE)) : 작업 영역을 깨끗이 청소 합니다.
* C Ctrl_+ : 화면에 표시되는 문자의 크기를 크게 합니다.
* CCtrl_- : 화면에 표시되는 문자의 크기를 작게 합니다.
* C"Tools -> Global Options…" 메뉴를 선택한 후 "General" 메뉴에서	
	* "Default working directory (when not in a project):" : RStudio에서 사용할 작업용 폴더를 지정 합니다.
	* "Default text encoding: " : ~.R 파일의 인코딩을 지정 합니다.  저는 "UTF-8"을 지정하여 사용하고 있습니다.
 
* RScript 편집 화면에서 Ctrl_Enter : 커서가 있는 라인을 Console 화면에서 실행 합니다.
* ? ~ : help(~)와 동일한 기능으로 함수, 데이터셋 등에 대한 도움말을 표시 합니다.
> 사용 예 1)  ? iris                 : iris 데이터셋에 대한 도움말
> 사용 예 2)  ? summary         : summary 함수에 대한 도움말

* ??  ~ : help.search("~")와 동일한 기능으로 함수 등의 이름을 명확히 알지 못할 경우, 검색을 할 때 사용 합니다.
* help(package = "~"), library(help = "~") : 패키지(라이브러리) 도움말로 제공하는 함수 목록을 확인할 수 있습니다.
> 사용 예)  library(help = "stats") : stats 패키지의 도움말 화면을 표시 합니다.
* methods(~) : ~이 대표하는 함수들의 목록을 표시 합니다.
> 사용 예)  methods(plot) : 다양한 데이터 타입을 사용하여 챠트를 그려주는 함수명을 확인할 수 있습니다.
>  * 시계열 데이터를 그려주는 plot.ts(~) 대신에 
> * 대표 함수명인 plot(~)를 사용하면 내부적으로 plot.ts(~)가 실행이 됩니다.

* args(~) : ~ 함수의 인자 정보를 조회 합니다.
> 사용 예) args(lm) : 회귀분석에서 사용하는 lm 함수의 인자 정보를 확인 합니다.
* attributes(~) : 데이터셋의 인자 정보를 조회 합니다.
* TAB : 자동 완성 기능으로 console 창에서 몇글자를 입력한 후 TAB키를 누르면 입력한 글자로 시작되는 함수 목록을 보여 주어 자동 완성 기능을 사용할 수 있도록 합니다.
 
 
### 2.  문자셋 관련 사항
* UTF-8 문자셋으로 저장된 ~.R 파일을 사용할 경우
	* "Tools -> Global Options…" 메뉴를 선택한 후 "General" 메뉴에서
	* "Default text encoding: " : ~.R 파일의 인코딩을 지정 합니다.  "UTF-8"을 지정하세요.

* UTF-8 문자셋으로 저장된 데이터 (csv 파일 등)을 읽을 경우
> read.table(생략, encoding = "UTF-8")                            #— 문자셋 정보를 명시 합니다.
 
* R의 인코딩 정보 확인
> localeToCharset()
> Sys.getlocale()

* 오류 메시지를 영문으로 보기 (영문 오류 메시지가 명확하고 구글 등의 검색을 통해서 확인하기가 편리 합니다.)
> Sys.setlocale("LC_ALL", "English_United States.1252")  #— 영문 문자셋을 지정 합니다.
> Sys.setlocale()                        #— 원래 디폴트로 설정된 문자셋으로 복구 됩니다.

* 데이터의 인코딩 정보 확인
> Encoding(~)

* 문자열의 인코딩 변환
>  iconv(~, "CP949", "UTF-8) #— "CP949"로 인코딩된 ~라는 데이터에 저장된 문자열을 "UTF-8"로 인코딩된 문자열로 변환
 
* "Notepad++" 텍스트 편집기 : 오픈소스로 제공되는 편집기로 사용이 편리 합니다.
	* 다운로드 사이트 : http://notepad-plus-plus.org/
	* 파일의 문자셋 변경 방법
		* 편집기의 우측 하단 영역에 문자셋이 표시 됩니다.  (ANSI, ANSI as UTF-8 등)
		* 윈도우의 디폴드 문자셋인 CP949를 사용할 경우 ANSI로 표시됨
		* BOM이 없는 UTF-8 문자셋을 사용할 경우 ANSI as UTF-8로 표시됨
		* "인코딩" 메뉴에서 "ANSI로 변환" 메뉴 선택  : UTF-8 문자셋으로 저장된 파일을 CP949 문자셋으로 변환 
		* "UTF-8 (BOM 없음)로 변환" 메뉴 선택 : CP949 문자셋으로 저장된 파일을 UTF-8 문자셋으로 변환






