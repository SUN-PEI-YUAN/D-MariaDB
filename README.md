# D-MariaDB

啟用Mariadb說明書

先下載dockerfile

```shell
git clone https://github.com/SUN-PEI-YUAN/D-MariaDB.git
```

由於[airlines.csv](https://drive.google.com/file/d/1vfpf2iSvG12BKp8qfs0YukMVEC2E_lNB/view?usp=sharing)檔案過大，所以請至下載資料並放入D-MariaDB資料夾中

進入資料夾後

```shell
docker build -t webserver-mariadb .
```

接下來啟用MariaDB與phpmyadmin以管理資料庫
```shell
docker-compose -f docker-compose.yml up 
```

確認一下container是否成功建立

![]('pic1.png')

成功後，進入`0.0.0.0:8080`，並在 `rbase` 中建立 `airlines` table

```shell
use rbase;
create table airlines (
  Year int,
  Month int,
  DayofMonth int,
  DayOfWeek int,
  DepTime  int,
  CRSDepTime int,
  ArrTime int,
  CRSArrTime int,
  UniqueCarrier varchar(5),
  FlightNum int,
  TailNum varchar(8),
  ActualElapsedTime int,
  CRSElapsedTime int,
  AirTime int,
  ArrDelay int,
  DepDelay int,
  Origin varchar(3),
  Dest varchar(3),
  Distance int,
  TaxiIn int,
  TaxiOut int,
  Cancelled int,
  CancellationCode varchar(1),
  Diverted varchar(1),
  CarrierDelay int,
  WeatherDelay int,
  NASDelay int,
  SecurityDelay int,
  LateAircraftDelay int
);
```


進入MariaDB中將csv匯入資料庫

```shell
sudo docker exec -it tku-mariadb bash
mysql -uroot -p123456
LOAD DATA LOCAL INFILE '/tmp/airlines.csv' 
INTO TABLE airlines
FIELDS TERMINATED BY ','
ENCLOSED BY '\"' 
LINES TERMINATED BY '\n' 
IGNORE 1 LINES
(
  Year, 
  Month, 
  DayofMonth, 
  DayOfWeek, 
  DepTime, 
  CRSDepTime, 
  ArrTime, 
  CRSArrTime, 
  UniqueCarrier, 
  FlightNum, 
  TailNum, 
  ActualElapsedTime, 
  CRSElapsedTime, 
  AirTime, 
  ArrDelay, 
  DepDelay, 
  Origin, 
  Dest, 
  Distance, 
  TaxiIn, 
  TaxiOut, 
  Cancelled, 
  CancellationCode, 
  Diverted, 
  CarrierDelay, 
  WeatherDelay, 
  NASDelay, 
  SecurityDelay, 
  LateAircraftDelay
);
```