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

![1](https://user-images.githubusercontent.com/93030868/151694474-87271093-f9a0-4b44-86c8-3cde519a00e3.png)

lalu kita set codeigniter untuk lxc_php5_1 dan lxc_php5_2 dengan ip yang telah kita atur

![2](https://user-images.githubusercontent.com/93030868/151694475-2eab748b-623a-47e8-864c-d6fd178ba2ae.png)

lalu kita buat Ansible codeiginiter dengan nama deploy-app.yml yang berisi domain container yang kita gunakan

![3](https://user-images.githubusercontent.com/93030868/151694476-f6a99c8e-25ea-4d8f-ba72-58da3ebfc4e4.png)

jalankan Ansible nya

![4](https://user-images.githubusercontent.com/93030868/151694478-d84201d4-75ec-4c21-9c55-c110577d8ae3.png)

Buat direktori Handlers, tasks dan templates
Setting app/hendlers yang berfungsi untuk restart

![5](https://user-images.githubusercontent.com/93030868/151694479-f67f565d-3662-4f2c-b139-459481e1a842.png)

app/tasks

![6](https://user-images.githubusercontent.com/93030868/151694480-2fe2ff58-5fda-496d-9690-97ff31a1db65.png)

app/templates

![7](https://user-images.githubusercontent.com/93030868/151694481-c132947b-b206-4e1e-a974-0c3b77667b31.png)

lalu kita jalankan http://kelompok11.fpsas/app

![8](https://user-images.githubusercontent.com/93030868/151694482-a4bba7ca-4916-4440-a9bf-e858d864fbbc.png)

kita buat 6 LXC php7 yang berisi Laravel,YII dan Wordpress lalu set ip masing-masing LXC

![9](https://user-images.githubusercontent.com/93030868/151694483-56d273a2-6061-4669-b2e1-fe871c9264a7.png)

sebelum melanjutkan cek dulu versi ubuntu dan debian yang kita gunakan apakah sesuai yang diminta yaitu menggunakan ubuntu 20 dan debian 10.

```markdown
lsb_release -a
```

![10](https://user-images.githubusercontent.com/93030868/151694485-ca9b812e-63d7-449c-a286-1aba20c62abe.png))

###### Laravel

Set domain pada Laravel dengan membuat install-laravel.yml

![11](https://user-images.githubusercontent.com/93030868/151694486-f45ea359-dc5f-4c0d-81a4-7b4c6298f5ae.png)

kita lakukan set pada php tasks 

![12](https://user-images.githubusercontent.com/93030868/151694487-c81c3cdf-7419-4cd3-9b60-e57fe92baca3.png)

php handlers

![13](https://user-images.githubusercontent.com/93030868/151694489-c7c72a90-2303-4f92-aa72-601ad7e4452f.png)

lakukan juga pada Laravel

laravel handlers

![14](https://user-images.githubusercontent.com/93030868/151694490-93d227ad-0984-4cf4-b9b2-fbd5dfbe9578.png)

laravel Tasks

![15](https://user-images.githubusercontent.com/93030868/151694491-fc350a6c-d5a2-4c4d-81de-642d3ba88852.png)

laravel env.templates

![16](https://user-images.githubusercontent.com/93030868/151694492-bf585ef3-2dec-4793-9f42-c32342d41a3f.png)

laravel roles/lv/templates/php7.conf

![17](https://user-images.githubusercontent.com/93030868/151694493-15eba12c-267c-41f6-91e6-af9b8c5f469b.png)

lalu kita jalankan laravel nya http://kelompok11.fpas/ dan laravel dapat digunakan

![18](https://user-images.githubusercontent.com/93030868/151694494-ee15b6e2-4c3a-4fa1-8287-8fa39e8a78c6.png)

###### YII

selanjut nya kita setting YII untuk kelompok11.fpsas/product

Ansibel YII

![19](https://user-images.githubusercontent.com/93030868/151694495-7b397b6b-3934-4ae6-837a-05e11501822a.png)

YII Tasks

![20](https://user-images.githubusercontent.com/93030868/151694496-6ff9f3ea-f313-49ff-ae69-e70df3c47c06.png)

YII handlers

![21](https://user-images.githubusercontent.com/93030868/151694497-43acfc80-6bf6-42a6-a820-2a3d9b471803.png)

YII templates lv.conf

![22](https://user-images.githubusercontent.com/93030868/151694498-a3f9bb6b-8a8d-4950-850c-7d7ce5d229fd.png)

lalu kita set YII agar terkoneksi ke database

![23](https://user-images.githubusercontent.com/93030868/151694499-3da42120-ab74-4c8c-b094-dd4e5be3ebfb.png)

lalu kita jalankan YII

![24](https://user-images.githubusercontent.com/93030868/151694500-0b6726a3-bd8b-4843-b06f-6f7c444b0ed0.png)

###### WordPress

Set Wordpress

Ansible Wordpres

![25](https://user-images.githubusercontent.com/93030868/151694501-da4c88ac-e3d2-4221-bdff-cdf1c7ef2375.png)

Task Wordpress

![26](https://user-images.githubusercontent.com/93030868/151694502-dd52c522-b6d2-4156-b962-b713e4e11b0f.png)

Handlers Wordpress

![27](https://user-images.githubusercontent.com/93030868/151694504-a6e5fd63-ecc7-414d-9f67-a34c73a1b3b2.png)

Templates Wordpress(wp.conf)

![28](https://user-images.githubusercontent.com/93030868/151694505-fd226289-c581-4bff-a3e6-38cbfe9b386d.png)

Templates Wordpress(wordpress.conf)

![29](https://user-images.githubusercontent.com/93030868/151694506-e77e6d6a-25fc-4a1a-8119-3f52a838de8e.png)

kita juga set pada templates php7.conf

![30](https://user-images.githubusercontent.com/93030868/151694507-f940b707-9f2e-47d4-8b55-93960f227c13.png))

kita jalankan Wordpress

![31](https://user-images.githubusercontent.com/93030868/151694508-3797759f-0085-49be-a39b-45724ecf3dce.png)

###### LXC Database

![32](https://user-images.githubusercontent.com/93030868/151694509-4615f4c0-2e49-4ae8-a786-928cc167fc35.png)

lalu kita set ansible pada database

Task DB

![33](https://user-images.githubusercontent.com/93030868/151694510-cc47a6f1-2f94-4be2-8160-07192359bc67.png)

Handlres DB

![34](https://user-images.githubusercontent.com/93030868/151694511-4183e32f-6bf0-4ef1-be6c-2f7d59fe9fd0.png)

Templates DB

![35](https://user-images.githubusercontent.com/93030868/151694512-49fa2526-c6b4-4eb9-bd95-941f9ba1b78b.png)

lalu kita jalankan DB dan database dapat dijalankan dan tersambung denagan YII

![36](https://user-images.githubusercontent.com/93030868/151694513-1c26f633-8de4-4751-baf2-c23d544eb418.png)

###### Set Host Utama

kita tambahkan domain pada masing-masing container dan sesuai ip yang telah kita setting pada awal instalasi

```markdown
nano /etc/hosts
```

![37](https://user-images.githubusercontent.com/93030868/151694452-11a27576-e963-43a5-8d39-7111fb2adf52.png)

lalu kita buat semua container auto start

![38](https://user-images.githubusercontent.com/93030868/151694455-a77e7122-d3ee-4f41-980b-0b39ef2ecf91.png)

###### Host Grouping

lakukan grouping pada host untuk memfokuskan lxc sesuai yang diperlukan

![39](https://user-images.githubusercontent.com/93030868/151694456-8768c5c6-641e-48c4-a94c-1c77aa7b25a8.png)

###### Load Balancer

lakukan load balancer pada YII, Laravel, dan Ci

Least Connection

* LXC_PHP7_1
* LXC_PHP7_2
* LXC_PHP7_4
* LXC_PHP7_6

Ip Hash

* LXC_PHP7_2
* LXC_PHP7_3
* LXC_PHP7_4
* LXC_PHP7_5

Weighted Load Balancing

* LXC_PHP7_1 (Weight=3)
* LXC_PHP7_2 (Weight=2)
* LXC_PHP7_4 (Weight=4)
* LXC_PHP7_5 (Weight=1)
* LXC_PHP7_6 (Weight=6)

Round Robin

* LXC_PHP5_1
* LXC_PHP5_2

```markdown
/etc/nginx/sites-available/kelompok11.fpsas
```

![40](https://user-images.githubusercontent.com/93030868/151694457-f8aaff84-7d0d-4251-8391-c73fd15798e4.png)

![41](https://user-images.githubusercontent.com/93030868/151694458-55e3dd5e-a0ca-45b8-916d-1c73c0af8537.png)

pada Wordpress

```markdown
/etc/nginx/sites-available/news.kelompok11.fpsas
```

![42](https://user-images.githubusercontent.com/93030868/151694460-f407b5ba-8b8d-4bf5-a423-ba88bc13f682.png)

###### Analisa JMeter

lalu kita gunakan app jmeter untuk load testing

* **50 Users**

  Summary report

  ![43](https://user-images.githubusercontent.com/93030868/151694461-4a2f13d5-238b-44d5-8558-49a4b7bae87e.png)

  Details User Akses

  ![44](https://user-images.githubusercontent.com/93030868/151694462-9f481612-e0f0-4534-9a22-7ed74222be8b.png)

  Grafik

  ![45](https://user-images.githubusercontent.com/93030868/151694463-c0816ae6-12e3-4d71-a009-c13cf0464283.png)

* **150 Users**

  Summary report

  ![46](https://user-images.githubusercontent.com/93030868/151694464-a3da57ba-a9cc-47ae-a169-9762b2998804.png)

  Details User Akses

  ![47](https://user-images.githubusercontent.com/93030868/151694465-8b9de199-1295-4ada-9624-c454d81849c1.png)

  Grafik

  ![48](https://user-images.githubusercontent.com/93030868/151694466-ebf5e453-25ce-4da1-ac3a-cb84a33f837f.png)

* **300 Users**

  Summary Report

  ![49](https://user-images.githubusercontent.com/93030868/151694467-c0888acb-1637-473e-acac-aa2a84b9793b.png)

  Detail Users Akses

  ![50](https://user-images.githubusercontent.com/93030868/151694469-796aedbb-4d4e-4427-bd96-a7d9a3c453c3.png)

  Grafik

  ![51](https://user-images.githubusercontent.com/93030868/151694470-eab4362f-5969-45c8-941f-2bc451cc4dcb.png)

* **500 Users**

  Summary report

  ![52](https://user-images.githubusercontent.com/93030868/151694471-3d0ddcbc-bfc6-4f62-bd01-086ac7346184.png)

  Detail Users Akses

  ![53](https://user-images.githubusercontent.com/93030868/151694472-fc79348d-80d3-48fb-8abd-19c23cb54fc6.png)

  Grafik

  ![54](https://user-images.githubusercontent.com/93030868/151694473-1f87dd55-65cb-4555-8cce-80ef94e09b54.png)

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

  
