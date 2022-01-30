## TUGAS AKHIR

#### Grahito Ardani B	(1202199007) || M. Iqbal Maulana	(1202190023)

#### IT 02-02

------

##### Membuat LXC

LXC yang kita perlukan adalah :

* 6 LXC ubuntu 20.04 PHP 7.4
* 2 LXC debian 10 PHP 5.6
* 1 LXC debian 10 mariadb server

kita buat dulu LXC php5 dengan nama lxc_php5.2_1 dan lxc_php5.2_2 dan set IP masing -  masing lxc.

![](C:\Users\grahi\Pictures\UAS\1.png)

set codeigniter

![](C:\Users\grahi\Pictures\UAS\2.png)

lalu kita buat Ansible codeiginiter dengan nama deploy-app.yml

![](C:\Users\grahi\Pictures\UAS\3.png)

jalankan Ansible nya

![](C:\Users\grahi\Pictures\UAS\4.png)

Setting app/hendlers

![](C:\Users\grahi\Pictures\UAS\5.png)

app/tasks

![](C:\Users\grahi\Pictures\UAS\6.png)

app/templates

![](C:\Users\grahi\Pictures\UAS\7.png)

lalu kita jalankan http://kelompok11.fpsas/app

![](C:\Users\grahi\Pictures\UAS\8.png)

kita buat 6 LXC php7 Laravel,YII dan Wordpress lalu set ip masing-masing LXC

![](C:\Users\grahi\Pictures\UAS\9.png)

sebelum melanjutkan cek dulu versi ubuntu dan debian yang kita gunakan

```markdown
lsb_release -a
```

![](C:\Users\grahi\Pictures\UAS\10.png)

###### Laravel

Set domain pada Laravel

![](C:\Users\grahi\Pictures\UAS\11.png)

kita lakukan set pada php tasks 

![](C:\Users\grahi\Pictures\UAS\12.png)

php handlers

![](C:\Users\grahi\Pictures\UAS\13.png)

lakukan juga pada Laravel

laravel handlers

![](C:\Users\grahi\Pictures\UAS\14.png)

laravel Tasks

![](C:\Users\grahi\Pictures\UAS\15.png)

laravel env.templates

![](C:\Users\grahi\Pictures\UAS\16.png)

laravel roles/lv/templates/lv.conf

![](C:\Users\grahi\Pictures\UAS\17.png)

laravel roles/lv/templates/php7.conf

![](C:\Users\grahi\Pictures\UAS\17.png)

lalu kita jalankan laravel nya http://kelompok11.fpas/

![](C:\Users\grahi\Pictures\UAS\18.png)

###### YII

set YII

Ansibel YII

![](C:\Users\grahi\Pictures\UAS\19.png)

YII Tasks

![](C:\Users\grahi\Pictures\UAS\20.png)

YII handlers

![](C:\Users\grahi\Pictures\UAS\21.png)

YII templates lv.conf

![](C:\Users\grahi\Pictures\UAS\22.png)

lalu kita set YII agar terkoneksi ke database

![](C:\Users\grahi\Pictures\UAS\23.png)

lalu kita jalankan YII

![](C:\Users\grahi\Pictures\UAS\24.png)

###### WordPress

Set Wordpress

Ansible Wordpres

![](C:\Users\grahi\Pictures\UAS\25.png)

Task Wordpress

![](C:\Users\grahi\Pictures\UAS\26.png)

Handlers Wordpress

![](C:\Users\grahi\Pictures\UAS\27.png)

Templates Wordpress(wp.conf)

![](C:\Users\grahi\Pictures\UAS\28.png)

Templates Wordpress(wordpress.conf)

![](C:\Users\grahi\Pictures\UAS\29.png)

kita juga set pada templates php7.conf

![](C:\Users\grahi\Pictures\UAS\30.png)

kita jalankan Wordpress

![](C:\Users\grahi\Pictures\UAS\31.png)

###### LXC Database

![](C:\Users\grahi\Pictures\UAS\32.png)

lalu kita set ansible pada database

Task DB

![](C:\Users\grahi\Pictures\UAS\33.png)

Handlres DB

![](C:\Users\grahi\Pictures\UAS\34.png)

Templates DB

![](C:\Users\grahi\Pictures\UAS\35.png)

lalu kita jalankan DB

![](C:\Users\grahi\Pictures\UAS\36.png)

###### Set Host Utama

kita tambahkan domain pada masing-masing container

```markdown
nano /etc/hosts
```

![](C:\Users\grahi\Pictures\UAS\37.png)

lalu kita buat semua container auto start

![](C:\Users\grahi\Pictures\UAS\38.png)

###### Host Grouping

lakukan grouping pada host

![](C:\Users\grahi\Pictures\UAS\39.png)

###### Load Balancer

lakukan load balancer pada YII, Laravel, dan Ci

```markdown
/etc/nginx/sites-available/kelompok11.fpsas
```

![](C:\Users\grahi\Pictures\UAS\40.png)

![](C:\Users\grahi\Pictures\UAS\41.png)

pada Wordpress

```markdown
/etc/nginx/sites-available/news.kelompok11.fpsas
```

![](C:\Users\grahi\Pictures\UAS\42.png)

###### Analisa JMeter

lalu kita gunakan app jmeter untuk load testing

* **50 Users**

  Summary report

  ![](C:\Users\grahi\Pictures\UAS\43.png)

  Details User Akses

  ![](C:\Users\grahi\Pictures\UAS\44.png)

  Grafik

  ![](C:\Users\grahi\Pictures\UAS\45.png)

* **150 Users**

  Summary report

  ![](C:\Users\grahi\Pictures\UAS\46.png)

  Details User Akses

  ![](C:\Users\grahi\Pictures\UAS\47.png)

  Grafik

  ![](C:\Users\grahi\Pictures\UAS\48.png)

* **300 Users**

  Summary Report

  ![](C:\Users\grahi\Pictures\UAS\49.png)

  Detail Users Akses

  ![](C:\Users\grahi\Pictures\UAS\50.png)

  Grafik

  ![](C:\Users\grahi\Pictures\UAS\51.png)

* **500 Users**

  Summary report

  ![](C:\Users\grahi\Pictures\UAS\52.png)

  Detail Users Akses

  ![](C:\Users\grahi\Pictures\UAS\53.png)

  Grafik

  ![](C:\Users\grahi\Pictures\UAS\54.png)

  ------

  #### Analisa

  ##### 1. Berapa nilai rata - rata througput untuk setiap website yang dihasilkan dari load testing?

  50 Users

  * Laravel			: 237,0/sec
  * Codeigneter   : 190,8/sec
  * YII                     : 198,4/sec
  * Wordpress      : 212,8/sec

  150 Users

  * Laravel			: 33,2/min
  * Codeigneter   : 33,2/min
  * YII                     : 33,2/min
  * Wordpress      : 33,2/min

  300 Users

  * Laravel			: 48,4/min
  * Codeigneter   : 48,4/min
  * YII                     : 48,4/min
  * Wordpress      : 48,4/min

  500 Users

  * Laravel			: 1,0/sec
  * Codeigneter   : 1,0/sec
  * YII                     : 1,0/sec
  * Wordpress      : 1,0/sec

  ##### 2. Berapa nilai rata - rata jumlah user yang dapat dilayani setiap detik untuk setiap website yang dihasilkan dari load testing?

  50 Users

  * Laravel			: 65 Users/sec
  * Codeigneter   : 37 Users/sec
  * YII                     : 33 Users/sec
  * Wordpress      : 86 Users/sec

  150 Users

  * Laravel			: 134 users/sec
  * Codeigneter   : 24 User/sec
  * YII                     : 22 Users/sec
  * Wordpress      : 211 Users/sec

  300 Users

  * Laravel			: 108 Users/sec
  * Codeigneter   : 18 Users/sec
  * YII                     : 17 Users/sec
  * Wordpress      : 158 Users/sec

  500 Users

  * Laravel			: 87 Users/sec
  * Codeigneter   : 25 Users/sec
  * YII                     : 23 Users/sec
  * Wordpress      : 150 Users/sec

  ##### 3. Bagaimana cara mengurangi nilai througput dan meningkatkan nilai jumlah user yang dapat dilayani setiap detik untuk skema yang telah dibuat ? Sebutkan faktor faktor yang mempengaruhi !

  Mengurangi Troughput dengan cara menambah bandwith yang kita gunakan dan untuk meningkatkan jumlah user yang dapat dilayani setiap detik dengan menambah load balance pada akses perdetik nya.

  faktor yang mempengaruhi

  * Topologi Jaringan
  * Banyak nya Pengguna
  * Spesifikasi Device User Dan Server
  * Tipe Data
  * Piranti Jaringan

  