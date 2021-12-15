# DNS

#### Grahito Ardani B 1202199006 || M Iqbal Maulana 1202190023

------

Pertama, untuk membuat sebuah subdomain dev.vm.local. Edit vm.local tambahkan subdomain

```markdown
sudo nano vm.local
```

![1](https://user-images.githubusercontent.com/93030868/146196129-97318b04-4d1a-4a99-97b9-6e20a6286191.png)

Masuk kedalam Hosts tambahkan subdomain dev.vm.local, setelah itu jangan lupa lakukan restart nginx

```markdown
Sudo nano /etc/hosts
Sudo service nginx restart
```

![2](https://user-images.githubusercontent.com/93030868/146196137-1c815223-168a-4c75-9697-94824c7db50b.png)

Tambahkan Konfigurasi CNAME untuk memasukkan subdomain, CNAME digunakan untuk alias dari satu nama ke nama lain: pencarian DNS akan dilanjutkan dengan mencoba lagi pencarian dengan nama baru 

![3](https://user-images.githubusercontent.com/93030868/146196141-bc9b32e6-87e6-41e3-966c-b17461d4f6fc.png)

```markdown
sudo nano /etc/bind/vm/vm.local
```

Restart bind9 dan coba lakukan ping ke subdomain kita buat

```markdown
Sudo service bind9 restart
Ping dev.vm.local

```

![4](https://user-images.githubusercontent.com/93030868/146196143-a71dcc25-d31d-4210-85c7-23b1976c7b4e.png)

Disini kita lakukan curl untuk mengetahui isi dari subdomain itu

```markdown
Curl -i http://dev.vm.local 
```

![5](https://user-images.githubusercontent.com/93030868/146196149-12dde24a-b225-4e92-ae7a-3a5fd94817e4.png)

#### **Modifikasi directory /var/www/html menjadi /var/www/html/dev/{nama_app}**

Sebelum nya kita masuk kedalam directory cd /var/www/html, lalu buat directory baru sesuai ketentuan soal praktikum yakni /var/www/html/dev/{nama_app}. Setelah itu copykan file index.nginx-debian.html kedalam directory yang telah kita buat.

```markdown
Sudo cd /var/www/html
Sudo mkdir dev
Sudo mkdir dev/utama
Sudo cp index.nginx-debian.html dev/utama/index.html
```

![6](https://user-images.githubusercontent.com/93030868/146196153-8ea1f3e5-da0f-4a7a-9376-46f7afb6d951.png)

Nah Setelah itu Masuk kedalam vm.local kita, disini kita edit lokasi file html ke sebuah directory yang kita buat tadi. /var/www/html/dev/utama

![7](https://user-images.githubusercontent.com/93030868/146196156-1fd5e392-cd62-4095-aaae-c48bb30604ed.png)

jangan lupa setelah itu lakukan restart nginx serta lakukan cek apakah konfigurasi sudah benar.

```markdown
Cd  /etc/nginx/sites-available
Sudo service nginx restart
sudo nginx -t
Sudo nginx -s reload
```

![8](https://user-images.githubusercontent.com/93030868/146196158-0a33a837-00a8-46f6-8429-e74e6cbe207e.png)

Selamat, anda dapat mengakses laravel di subdomain kita buat

![9](https://user-images.githubusercontent.com/93030868/146196159-033974bc-1962-4433-ab0e-485c9dd70ed6.png)

Akses Codeigniter Dengan Subdomain

![10](https://user-images.githubusercontent.com/93030868/146196162-1270d5c1-73b9-4736-bd75-021daf33fa6f.png)

Akses Wordpress

![11](https://user-images.githubusercontent.com/93030868/146196164-e26fccdd-247c-4252-9172-a78a1abfb99d.png)

Akses Phpmyadmin

![12](https://user-images.githubusercontent.com/93030868/146196168-c1b4f68a-abd9-4898-bb78-992fb8cbadfd.png)
