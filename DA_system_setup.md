## Windows 기반

### R

* R Core 설치 : [https:\/\/cloud.r-project.org\/bin\/windows\/base\/](https://cloud.r-project.org/bin/windows/base/)
* R Studio 설치 : [https:\/\/www.rstudio.com\/products\/rstudio\/download\/](https://www.rstudio.com/products/rstudio/download/)

### Python

* Anaconda 설치 : [https:\/\/www.continuum.io\/downloads](https://www.continuum.io/downloads)

## Linux 기반

### R 분석환경

#### 1. R 설치

```bash
 sudo apt-get update
 sudo apt-get install r-base
```

#### 2. R-Studio 설치

```bash
$ sudo apt-get install gdebi-core
$ wget https://download2.rstudio.org/rstudio-server-1.0.136-amd64.deb
$ sudo gdebi rstudio-server-1.0.136-amd64.deb
```

> 접속 확인 `http://localhost:8787/`

### Python\/Jupyter 설치

#### 1. Python설치

```bash
wget https://repo.continuum.io/archive/Anaconda3-4.3.0-Linux-x86_64.sh
bash Anaconda3-4.3.0-Linux-x86_64.sh
export PATH="/home/username/anaconda/bin:$PATH"  OR 설치 설정시 pretend하기
```

> [https://www.continuum.io/downloads](https://www.continuum.io/downloads) 에서 최신 버전 확인 가능


기본 패키지 설치 
```
sudo apt-get install python3 python3-pip python3-dev python-virtualenv
```

Virtualenv 설치/업그레이트 
```
sudo pip install --upgrade virtualenv
```





#### 2. Python 용 R 설치

```bash
conda install -c r r-irkernel
conda install -c r r-essentials
```

> “R Essentials” bundle with the IRKernel native R language kernel and over 80 of the most used R language packages for data science, including dplyr, shiny, ggplot2, tidyr,caret and nnet.
>
> ipython에서 R 패지키 설치 방법 \(R 콘솔에서 실행??\)  
> $ R   
> `install.packages(c('rzmq','repr','IRkernel','IRdisplay'), repos = 'http://irkernel.github.io/', type = 'source')`
>
> `IRkernel::installspec()`

#### 3. OpenCV 설치

`conda install -c https://conda.binstar.org/menpo opencv3`

> import cv2 \(!!!IMPORTANT it’s still cv2 not cv3\).   
> `To check the version print(cv2.__version__)`

###### 3.1 Jupyter 설정하기

```
$ sudo pip3 install jupyter
$ jupyter notebook --generate-config
$ vi /root/.jupyter/jupyter_notebook_config.py
$ nohup jupyter notebook &
```

> 설정 파일 # /home/(username)/.jupyter/jupyter_notebook_config.py
> c = get_config()
> c.NotebookApp.ip = '123.456.789.123' # 공인ip를 적어주었다.
> c.NotebookApp.open_browser = False # 원격접속으로 활용할 것이기 때문에 비활성화 시켰다.
> c.NotebookApp.port = 8017 # 포트를 설정해준다. 기본포트로 8888이 자동 배정된다.
> c.NotebookApp.password = '....' 
> * #python 실행후 from notebook.auth import passwd; passwd()
> c.NotebookApp.notebook_dir = '/home/winterj/notebook' # 기본 디렉터리를 지정시켜준다.
> c.NotebookApp.base_url = 'notebook' #외부 접근을 위한 필수 작업
> 참고 : http://b.winterj.me/220858584491


[http:\/\/localhost:8888\/](http://localhost:8888/)

> [Jupyter 공식홈페이지](http://jupyter-notebook.readthedocs.io/en/latest/public_server.html)

#### 4. Tensorflow 설치

가상환경 구축 
```
$ mkdir tensorflow
$ virtualenv --system-site-packages ~/tensorflow 
```

가상환경 활성화
```
$ source ~/tensorflow/bin/activate
```

텐서플로우 설치
```
$ export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-0.12.1-cp34-cp34m-linux_x86_64.whl
$ sudo pip install --upgrade $TF_BINARY_URL
```

설치 확인
```
$python 
>>>> import tensorflow as tf
```

가상환경 종료 
```
$ deactive
```


> 공식 TensorFlow 설치 [메뉴얼](https://www.tensorflow.org/versions/master/get_started/os_setup)

#### 5. Python IDE(Pycharm)설치 

https://www.jetbrains.com/pycharm/download/#section=linux 에서 Community 버전을 다운로드 받았습니다.

압축을 풀은 후, /usr/local/ 아래로 옮긴 후..
```
$ tar xvzf pycharm-community-2016.2.3.tar.gz 
$ sudo mv pycharm-community-2016.2.3 /usr/local/pycharm
$ rm pycharm-community-2016.2.3.tar.gz
```

.bashrc에 PATH를 추가해주었습니다.
```
export PATH=$PATH:/usr/local/pycharm/bin/
```

path 추가한 것을 적용하고 
```
$ source ~/.bashrc
```


pyCharm을 실행시켜 봅니다.
```
$ pycharm.sh 
```


