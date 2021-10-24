## Laporan Hasil Praktikum Sistem Adiministrasi server

------

#### Laporan Praktikum 1

Kelompok 11[IT 02-02]

Muhammad Iqbal Maulana (1202190023) || Grahito Ardani Bimanta (1202199006)

------

#### Langkah-langkah

1. Rename ubuntu_php5.6 menjadi ubuntu_landing, serta rubah IP mengikuti skema yang baru!!

   * cek status kontainer apakah masih  berjalan jika ya, maka kita harus menonaktifkan terlebih dahulu untuk memproses penggantian nama pada kontainer tersebut

   

   ```markdown
   sudo lxc-stop -n ubuntu_php5.6
   ```

   ![](C:\Users\grahi\Pictures\Saved Pictures\1.png)

   * setelah konatiner telah nonaktif maka kita dapat mengganti nama kontainer nya 

     ```markdown
     sudo lxc-copy -R -n ubuntu5.6 -N ubuntu_landing
     ```

   * kita dapat melihat nama apakah telah terganti

     ```markdown
     sudo lxc-ls -f
     ```

   ![](C:\Users\grahi\Pictures\Saved Pictures\2.png)

   2.  Install Lxc debian 9 dengan nama debian_php5.6

      Lakukan instalasi debian 9 yang tersedia pada template kontainer ubutnu untuk memporses php5.6

      Debian : Jenis Kontainer

      Stretch : versi Kontainer

      ```markdown
      Sudo-create -n Debian_php5.6 -t download -- --dist Debian –release stretch -h amd64 –force-cache –no-validate –server images.linuxcontainers.org
      ```

   ![](C:\Users\grahi\Pictures\Saved Pictures\3.PNG)

   3. Setup nginx pada debian_php5.6 untuk domain http://lxc_php5.dev , buat halaman index.html yang menerangkan informasi nama lxc

   * Jalankan lxc debian 5 dan lakukan installasi nginx

   ```markdown
   sudo lxc_start -n debian_php5.6
   sudo lxc-attach -n debian_5.6
   sudo apt install nginx nginx-extras
   ```

   ![image-20211024005217322](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024005217322.png)

   * Install net-tools curl yang berfungsi untuk Untuk memantau aktivitas jaringan komputer. Untuk melihat konektivitas dari suatu perangkat jaringan komputer dengan yang lain. Untuk melihat data atau file apa yang sedang ditransfer

     ```markdown
     apt install net-tools curl
     ```

     ![](C:\Users\grahi\Pictures\Saved Pictures\5.PNG)

   * Lakukan cek ip untuk mengetahui ip default yang dipakai, Lalu masuk dalam folder/ etc/network untuk melakukan Settings ip static

     ```
     ipconfig
     nano /etc/network/interfaces
     ```

     ![image-20211024010438436](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024010438436.png)

     

   * Lakukan setting ip sesuai dengan kebutuhan, lalu restart jaringan tersebut agar sistem pada jaringan dapat memperbarui ip yang baru dilakukan konfigurasi

     ```markdown
     systemctl restart networking.service
     ```

     ![image-20211024010651243](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024010651243.png)

   * cek ip apakah telah terganti. ternyata tidak berganti, hal ini kemungkinan setting ip gagal. jadi kita melakukan shutdown untuk merefresh sistem yang telah di konfigurasi ulang

     ```markdown
     shutdown now
     ```

     ![image-20211024011402166](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024011402166.png)

   * jalankan ulang lxc debian 9 nya dan coba ip apakah sudah berganti. ip telah terganti untuk memastikan kontainer lxc terhubung ke internet dengan melakukan ping ke google

     ```markdown
     ping google.com
     ```

     ![](C:\Users\grahi\Pictures\Saved Pictures\9.PNG)

   * setelah itu masuk ke folder sites avaible yang merupakan domain file nya dan membuat file dev

     ```markdown
     cd /etc/nginx/sites-avaible
     touch lxc-php5.dev
     ```

     ![image-20211024111903748](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024111903748.png)

     

   * melakukan konfigurasi pada file lxc_php5.dev
   
     ```
     nano lxc_php5/dev
     ```

     ![image-20211024012257516](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024012257516.png)

   * masuk ke folder sites-enabled dan melakukan penyambungan atau *lean* yang berfungsi untuk membuat tautan antar file dan cek apakah syntax file yang dibuat sudah benar dan menjalankan ulang nginx
   
     ```
     cd ../sites-enabled
     ln-s /etc/nginx/sites-available/lxc_php5.dev
     nginx -t
     nginx -s reload
     ```

     ![image-20211024111947569](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024111947569.png)

   * masuk ke host untuk melakukan konfigurasi menghubungkan lxc dengan domain yang telah di buat
   
     ```markdown
     nano /etc/host
     ```

     ![image-20211024012820109](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024012820109.png)

   * konfigurasi host pada ubuntu5.6, tambahkan ip dan nama file agar kedua nya akan saling terhubung

     ![image-20211024012957048](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024012957048.png)

   * masuk ke folder var/www/html lalu membuat sebuah folder yang nantinya akan diakses di browser. membuat file yang mengcopy dari file *index.nginx-debian.html*menjadi file baru *index.html*
   
     ```markdown
     cd var/www/html
     mkdir app
     cp index.nginx-debian.html_php5.6/index.html
     nano index.html
     ```

     ![image-20211024112058756](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024112058756.png)

   * editing file index yang nantinya ditampilkan pada browser

     ![image-20211024013345190](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024013345190.png)

   * memanggil domain yang sudah dibuat untuk memastikan container berjalan dengan baik yang dimana akan menampilkan file yang akan muncul pad web
   
     ```markdown
     curl -i http://lxc_php.dev
     ```

     ![image-20211024013516044](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024013516044.png)

   Ubuntu php 7

   * melakukan konfigurasi pada ubuntu php 7. berhubung sudah melakukan instalasi sebelumnya maka kita hanya menjalankan ubuntu php7
   
     ```markdown
     sudo lxc-attach -n ubuntu_php7.4
     sudo apt install nginx nginx-extras
     apt install net-tools curl
     ```

     ![image-20211024112144729](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024112144729.png)

   * konfigurasi ip menjadi ip statis
   
     ```markdown
     nano /etc/netplan/10-lxc.yaml
     ```

     ![image-20211024013930574](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024013930574.png)

   * restart sistem karena kita telah merubah konfigurasi ip. kita melakukan cek ip untuk memastikan ip telah terganti dan melakukan cek apakah terhubung dengan internet pada jaringan php 7 dapat berjalan
   
     ```markdown
     sudo netplan apply
     ifconfig
     ping google.com
     ```

     ![image-20211024014147026](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024014147026.png)

   * masuk pada folder /etc/nginx/sites-available dan membuat file dev. 
   
     ```markdown
     cd /etc/nginx/sites-available
     touch lxc-php5.dev
     ```

     !![image-20211024112223864](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024112223864.png)

   * setting konfigurasi pada nginx php7
   
     ```markdown
     nano lxc_php7.dev
     ```

     ![image-20211024014422106](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024014422106.png)

   * masuk ke folder sites-enabled dan melakukan penyambungan atau *lean* yang berfungsi untuk membuat tautan antar file dan cek apakah syntax file yang dibuat sudah benar dan menjalankan ulang nginx
   
     ```markdown
     cd ../sites-enabled
     ln -s /etc/nginx/sites-available/lxc_php7.dev
     nginx -t
     nginx -s reload
     ```

     ![image-20211024112253463](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024112253463.png)

   * konfigurasi host pada php7, tambahkan ip dan nama file agar keduanya saling terhubung
   
     ```markdown
     nano /etc/hosts
     ```

     ![image-20211024014901100](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024014901100.png)

   * masuk ke folder var/www/html lalu membuat sebuah folder yang nantinya akan diakses di browser. membuat file yang mengcopy dari file *index.nginx-debian.html* menjadi file baru *index.html*
   
     ```markdown
     cd /var/www/html
     mkdir blog
     cd index.nginx-debian.html blog/index.html
     nano index.html
     ```

     !![image-20211024112325625](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024112325625.png))

   * editing pada file blog/index.html dan beri menu untuk menuju ke halaman lain

     ![image-20211024015141088](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024015141088.png)

   * memanggil domain yang telah dibuat untuk memastikan file index yang kita buat dapat berjalan dengan baik dalam kontainer ubuntu 7.4
   
     ```markdown
     curl -i http://lxc-php7.dev
     ```

     ![image-20211024015254120](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024015254120.png)

   4.  Setup nginx pada ubuntu_landing untuk domain http://lxc_landing.dev , buat halaman index.html yang menerangkan informasi nama lxc	

   * masuk pada kontainer ubuntu_landing lalu cek ip apakah terdapat ip yang sama jika ya, kita dapat mengkonfigurasi ulang karena dapat menimbulkan conflik atau tabrakan antar ip
   
     ```markdown
     sudo lxc-ls -f
     sudo lxc-attach -n ubuntu_landing
     ```

     ![](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024112413656.png)

   * install net-tools pada ubuntu landing
   
     ```markdown
     apt install nano net-tools curl
     ```

     ![image-20211024112451260](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024112451260.png)

   * konfigurasi ip yang sebelumnya 10.0.3.10 menjadi 10.0.3.103
   
     ```markdown
     nano /etc/network/interfaces
     ```

     ![image-20211024020140599](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024020140599.png)

   * cek ip dan cek jaringan untuk memastikan terhubung ke internet
   
     ```markdown
     ifconfig
     ping google.com
     ```

     ![](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024112521646.png)

   * membuat file domain dengan cara masuk ke folder sites-available. karena kita sudah memiliki file domain pada folder tersebut maka kita dapat melakukan rename file menjadi lxc_landing.dev 
   
     ```markdown
     cd /etc/nginx/sites-available
     sudo mv lxc-php5.dev lxc-landing.dev
     ```

     ![](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024112609047.png)

   * konfigurasi pada file domain
   
     ```markdown
     nano lxc_landing.dev
     ```

     ![image-20211024020625649](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024020625649.png)

   * masuk ke folder sites-enabled dan melakukan penyambungan atau *lean* yang berfungsi untuk membuat tautan antar file dan cek apakah syntax file yang dibuat sudah benar dan menjalankan ulang nginx
   
     ```markdown
     cd ../sites-enabled
     ln -s/etc/nginx/sites-availble/lxc_php5.dev
     nginx -t
     sudo nginx service start
     nginx -s reload
     ```

     ![](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024112722289.png)

   * konfigurasi host, sesuaikan dengan penamaan file domain dan ip yang dipakai
   
     ```markdown
     nano /etc/host
     ```

     ![image-20211024021013082](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024021013082.png)

   * masuk ke folder var/www/html lalu membuat sebuah folder yang nantinya akan diakses di browser. membuat file yang mengcopy dari file *index.nginx-debian.html* menjadi file baru *index.html*
   
     ```markdown
     cd /var/www/html
     mkdir landing
     cp index.nginx-debiam.html landing/index.html
     nano index.html
     ```

     ![](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024112807399.png)

   * edit isi dalam file html sesuai apa yang ingin ditampilkan pada web

     ![image-20211024021222088](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024021222088.png)

   * Jalan kan curl untuk melihat data yang akan muncul pada web yang mesih menggunakan bahas html
   
     ```markdown
     curl -i http://lxc_landing.dev
     ```

     ![image-20211024021300889](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024021300889.png)

   5. Lxc ubuntu_landing harus auto start ketika vm dinyalakan, hal ini digunakan untuk menjaga agar website comapny profile tidak mengalami *downtime*

      mengatur konfigurasi auto start kontainer lxc dengan masuk sebagai user root
   
      ```markdown
      sudo su
      cd /var/lib/lxc/ubuntu_landing
      ```

      tambahkan konfigurasi pada kontainer server utama
   
      ```markdown
      lxc.start.auto = 1
      ```

      ![image-20211024021622847](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024021622847.png)

   6. setup nginx pada vm.local untuk mengatur *proxy_pass* dimana:

   * mengatur hosts dan menambah nama file domain serta ip yang digunakan pada masing-masing kontainer
   
   ```markdown
   sudo nano /etc/hosts
   ```

   ![image-20211024021814788](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024021814788.png)

   * Buat file vm.local di folder sites-available. Jika sudah memilik tidak perlu pakai tinggal lakukan konfigurasi
   
     ```markdown
     sudo /etc/nginx/sites-available/
     sudo touch vm.local
     ```

     ![image-20211024022052112](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024022052112.png)
   
     * mengakses http://vm.local akan diarahkan ke http://lxc_landing.dev
     * mengakses http://vm.local/blog akan diarahkan ke http://lxc_php7.dev
     * mengakses http://vm.local/app akan diarahkan ke http://lxc_php5.dev

   * konfigurasi vm.lokal dan tambahkan masing-masing nama file dan tempat folder domain
   
     ```markdown
     sudo nano vm.local
     ```

     ![image-20211024022724560](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024022724560.png)

   * memperbarui konfigurasi
   
     ```markdown
     cd ../sites-enabled
     nginx -t
     nginx -s reload
     ```

     ![](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024112956276.png)

   * menampilkan site utama atau site vm.local
   
     ```markdown
     curl -i http://vm.local
     ```

     ![image-20211024022914019](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024022914019.png)

   7. untuk kebutuhan presentasi mereka, browser di laptop mereka harus dapat mengakses ketiga url tersebut

   * web utama

     ![image-20211024022956628](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024022956628.png)
   
   * Membuka di dalam brwoser windows menggunakan url vm.local
      Web Blog

     ![image-20211024023027733](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024023027733.png)

   * web aplikasi

     ![image-20211024023045685](C:\Users\grahi\AppData\Roaming\Typora\typora-user-images\image-20211024023045685.png)

   ------

   #### Analisa

   1. - mengapa untuk kebutuhan php5.6 tidak bisa      menggunakan ubuntu 16.04, sehingga perlu diganti os ke debian 9?

        karena ubuntu 16.04 hanya tersedia untuk opsi yang berbayar yang hanya dapat diakses ubuntu estended security maintenance yang berarti ubuntu 16.04 akan dihapus karena adanya pembaruan fitur yang bernama Trusty EOL yang tidak support pada ubuntu 16.04

      - kenapa harus menggunakan virtualisasi LXC pada skema website yang akan didevelop?

        Karena LXC menggunakan file system yang netral, container dapat di fungsikan secara penuh oleh OS, data dapat disimpan di dalam maupun diluar container.

      - apa yang dimaksud dengan proxy server? kenapa vm.local bisa kita anggap sebagai proxy server?
   
        Proxy server bisa disebut computer sentral atau computer server yang bisa bertindak sebagai computer lainnya untuk yang dapat melakukan request content pada internet maupun intranet sama seperti vm.local. jadi vm.local bisa dikatakan juga sebagai proxy server

