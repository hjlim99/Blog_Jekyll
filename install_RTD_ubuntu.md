## Linux 서버에 Read the docs 설치하기

### 1. root 계정으로 변경
```bash
su 
```
### 2. Sphynx-python 설치 

(참고 : http://sphinx-doc.org/latest/install.html#debian-ubuntu-install-sphinx-using-packaging-system)
```bash
apt-get install python-sphinx
```
### 3. python pip 설치
```bash
apt-get install phython-pip
```
### 4. Sphynx 자동 설치 
```bash
pip install sphinx sphinx-autobuild
```
### 5. Sphynx 퀵 설치
```bash
cd /path/to/project (프로젝트 생성 경로)
mkdir docs
cd docs
sphinx-quickstart #(설명에 따라서 project create 및 settings.)
```

### 6. Markdown 설치

```bash
pip install mkdocs
```

### 7. MD Directory 생성
```bash
cd /path/to/project (생성한 프로젝트 경로)
mkdocs new docs (md directory 생성)
```
### 8. build
```bash
mkdocs build
```
auto reload 필요 시 mkdocs serve 실행

### 9. virtualenv 사용하기 위해 설치
```bash
apt-get install python-virtualenv
```
### 10. read the docs 설치
```bash
virtualenv rtd
cd rtd
source bin/activate
pip --version
pip install --upgrade pip
mkdir checkouts
cd checkouts
git clone https://github.com/rtfd/readthedocs.org.git
```
-- pip 버전 확인(1.5이상)
### 11. pip를 사용하기 위한 기능 추가 인스톨(included with virtualenv)
```bash
cd readthedocs.org 
pip install -r requirements.txt
pip install -r requirements.txt 
```


	*** Error: command python setup.py egg_info failed with error code 1 in
	apt-get install build-essential
	apt-get install python-dev
	apt-get install libxml2-dev libxslt1-dev zlib1g-dev

### 12. Database 설정
```bash
cd readthedocs 
./manage.py syncdb
```

### 13. super user 계정 생성

```bash
./manage.py migrate`
```
### 14. 몇명의 user와 test project load

```bash
./manage.py loaddata test_data
```
### 15. Server Run!

```bash
./manage.py runserver
```



	*** Error
	1. http://localhost:8000/api/v1/project/25/ Error 발생
	--> Port를 8000으로 사용.
	--> ./manage.py runserver ip:8000 

	2. redis connection.py error 발생 (redis/connection.py line 436 incorrect raise connection error)
	--> sudo apt-get install redis-server 






