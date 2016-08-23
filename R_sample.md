
```R 

install.packages("caret")
install.packages("sos")
install.packages("doParallel")
install.packages("sqldf")
install.packages("stringr")
install.packages("dplyr")
#install.packages("https://cran.r-project.org/src/contrib/DMwR_0.4.1.tar.gz", repos = NULL, type="source") #cran 외 소스로 설치 하기 
#install.packages("devtools") #devtools::install_github('rstudio/DT')


suppressPackageStartupMessages({  #warning메시지 미출력 
  library(caret)
  library(sos) #findFn("")
  library(doParallel)  # 병렬처리용 
  library(sqldf)
  library(stringr)
  require(dplyr)
})

#if (!require("R6")) {
#  install.packages("R6") 
#  library("R6")
#}


### Verteilung von Tasks auf mehrere Cores
detectCores()
registerDoParallel(cores=35)
cat(sprintf('Running with %d worker(s)\n', getDoParWorkers())) ## 이를 이용하면 멀티 프로세싱이 되고 있는지 확인앟 수 있음 
Sys.setenv(LANGUAGE='en')


#메모리 정리
rm(list=ls())
gc()
cat("\014")  # clear the screen

#작업환경 설정
setwd("/home/hunjung.lim/R/KR_RBEMS")
path <- getwd()

system("wget http://server.cyclogic.net/~sshome/dump/ko_kyonggi_25_2016-04-25~2016-05-03_All_1462335982.csv")

#파일 읽기 
system("ls") #list.files() 
raw<- read.table(paste0(path, "/ko_kyonggi_25_2016-04-25~2016-05-03_All_1462335982.csv"),header=TRUE, sep="," , fileEncoding = "CP949", encoding = "UTF-8") 
#test <- read.csv(paste0(path, "/test.csv"),header=TRUE, sep=",")   
raw <- read.table("./ko_kyonggi_25_2016-04-25~2016-05-03_All_1462335982.csv", header=T, sep=",")  # sep이용 csv 읽기 가능 
#raw <- read.table(file.choose(), header=T, sep=",")  # sep이용 csv 읽기 가능 
str(raw)

#컬럼 이름 입력 
colnames(raw) <-c("timestamp",  "siteID" ,  "outdoor_condition" ,  "outdoor_temp" ,  "outdoor_humidity"  ,  "indoor_temp"  ,  "indoor_humidity"  ,  "occupancy" ,  "power_realtime"  ,  "power_accumulated"  ,  "plug1_serial"  ,  "plug1_description",  "plug1_isRunning" ,  "plug1_power_realtime" ,  "plug2_serial"  ,  "plug2_description",  "plug2_isRunning" ,  "plug2_power_realtime" ,  "plug3_serial"  ,  "plug3_description",  "plug3_isRunning" ,  "plug3_power_realtime" ,  "plug4_serial"  ,  "plug4_description",  "plug4_isRunning" ,  "plug4_power_realtime" ,  "plug5_serial"  ,  "plug5_description",  "plug5_isRunning" ,  "plug5_power_realtime" ,  "plug6_serial"  ,  "plug6_description",  "plug6_isRunning" ,  "plug6_power_realtime" ,  "plug7_serial"  ,  "plug7_description",  "plug7_isRunning" ,  "plug7_power_realtime" ,  "plug8_serial"  ,  "plug8_description",  "plug8_isRunning" ,  "plug8_power_realtime" ,  "plug9_serial"  ,  "plug9_description",  "plug9_isRunning" ,  "plug9_power_realtime" ,  "plug10_serial"  ,  "plug10_description",  "plug10_isRunning" ,  "plug10_power_realtime")
t(raw)#switch row & columns  

attach(raw) #$로 호출 없이 바로 사용 가능 반대는 detach(raw)

#불필요 삭제 
str(raw)
raw<- select(raw, -(plug1_serial:plug10_power_realtime))

#NA / NULL handling
sum(is.na(raw))
raw <- na.omit(raw)  
#train[is.na(train)] <- 0

data <- raw #backup


#날짜 추출 ? 더 나은 방법은? 
data$timestamp <- as.character(data$timestamp)
data$year <- as.integer(str_sub(data$timestamp, 1,4))
data$month <- as.integer(str_sub(data$timestamp, 6,7))
data$day <- as.integer(str_sub(data$timestamp, 9,10))
data$hour <- as.integer(str_sub(data$timestamp, 12,13))
data$min <- as.integer(str_sub(data$timestamp, 15,16))
#r435$lecture[(r435$week =="수요일") & (r435$hour >=10) & (r435$hour <=11)& (r435$minu >=01) & (r435$minu <=50) ]  <- 1 
str(data)

#날짜 변환 / 요일 추가 
data$date <- as.Date(str_sub(data$timestamp, 1,10),"%Y-%m-%d") 
data$week <- weekdays(data$date)
#data$timestamp <- as.POSIXlt(data$timestamp, format="%Y-%m-%d %H:%M")  # xxx$hour 등 가능 , sqldf사용 불가 
#data$timestamp <- as.Date(data$timestamp, format="%Y-%m-%d %H:%M")
str(data)

#목적에 따라 파일 분리 하기 
for (i in 1:25)
{  
  command = sprintf("shome%02d <-  data[which(data$siteID==\"shome%02d\"),]",i,i)   #shome01 <-  data[which(data$siteID=="shome01"),]
  eval(parse( text=command ))
  message(command)
}

#Feature Extraction 
#r435$lecture[(r435$week =="목요일") & (r435$hour >=10) & (r435$hour <=15)& (r435$minu >=01) & (r435$minu <=50) ]  <- 1 
#r435$lecture[is.na(r435$lecture)] = 0 #r435$lecture <- sub("NULL","0",r435$lecture)


setseed(100)

write.csv(raw,file="mod_raw.csv")
```

