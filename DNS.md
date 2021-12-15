# DNS

#### Grahito Ardani B 1202199006 || M Iqbal Maulana 1202190023

------

Pertama, untuk membuat sebuah subdomain dev.vm.local. Edit vm.local tambahkan subdomain

```markdown
sudo nano vm.local
```

![](D:\Semester5\administrasi Server\Modul5\1.png)

Masuk kedalam Hosts tambahkan subdomain dev.vm.local, setelah itu jangan lupa lakukan restart nginx

```markdown
Sudo nano /etc/hosts
Sudo service nginx restart
```

![](D:\Semester5\administrasi Server\Modul5\2.png)

Tambahkan Konfigurasi CNAME untuk memasukkan subdomain, CNAME digunakan untuk alias dari satu nama ke nama lain: pencarian DNS akan dilanjutkan dengan mencoba lagi pencarian dengan nama baru 

![](D:\Semester5\administrasi Server\Modul5\3.png)

```markdown
sudo nano /etc/bind/vm/vm.local
```

Restart bind9 dan coba lakukan ping ke subdomain kita buat

```markdown
Sudo service bind9 restart
Ping dev.vm.local

```

![](D:\Semester5\administrasi Server\Modul5\4.png)

Disini kita lakukan curl untuk mengetahui isi dari subdomain itu

```markdown
Curl -i http://dev.vm.local 
```

![](D:\Semester5\administrasi Server\Modul5\5.png)

#### **Modifikasi directory /var/www/html menjadi /var/www/html/dev/{nama_app}**

Sebelum nya kita masuk kedalam directory cd /var/www/html, lalu buat directory baru sesuai ketentuan soal praktikum yakni /var/www/html/dev/{nama_app}. Setelah itu copykan file index.nginx-debian.html kedalam directory yang telah kita buat.

```markdown
Sudo cd /var/www/html
Sudo mkdir dev
Sudo mkdir dev/utama
Sudo cp index.nginx-debian.html dev/utama/index.html
```

![](D:\Semester5\administrasi Server\Modul5\6.png)

Nah Setelah itu Masuk kedalam vm.local kita, disini kita edit lokasi file html ke sebuah directory yang kita buat tadi. /var/www/html/dev/utama

![](D:\Semester5\administrasi Server\Modul5\7.png)

jangan lupa setelah itu lakukan restart nginx serta lakukan cek apakah konfigurasi sudah benar.

```markdown
Cd  /etc/nginx/sites-available
Sudo service nginx restart
sudo nginx -t
Sudo nginx -s reload
```

![](D:\Semester5\administrasi Server\Modul5\8.png)

Selamat, anda dapat mengakses laravel di subdomain kita buat

![](D:\Semester5\administrasi Server\Modul5\9.png)

Akses Codeigniter Dengan Subdomain

![](D:\Semester5\administrasi Server\Modul5\10.png)

Akses Wordpress

![](D:\Semester5\administrasi Server\Modul5\11.png)

Akses Phpmyadmin

![](D:\Semester5\administrasi Server\Modul5\12.png)