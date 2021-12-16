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

lalu kita masuk ke

```markdown
cd main.yml
```

lalu kita membuat direktori baru dan copy ke dalam direktori baru

![](C:\Users\grahi\Pictures\Camera Roll\7.png)

![](C:\Users\grahi\Pictures\Camera Roll\8.png)

lalu kita masuk ke

```markdown
cd roles/lv/templates
nano 43.168.192.in-addr.arpa
nano named.conf.local
nano named.conf.options
nano  resolv.conf
nano vm.local
```

![](C:\Users\grahi\Pictures\Camera Roll\10.png)

![](C:\Users\grahi\Pictures\Camera Roll\11.png)

![](C:\Users\grahi\Pictures\Camera Roll\12.png)

![](C:\Users\grahi\Pictures\Camera Roll\13.png)

![](C:\Users\grahi\Pictures\Camera Roll\14.png)

lalu jalankan ansible playbook

```markdown
ansible-playbook -i hosts install-laravel.yml -k
```

![](C:\Users\grahi\Pictures\Camera Roll\15.png)

lalu lanjut keluar dari direktori dan masuk ke hosts dan tambahkan domain baru

```markdown
sudo nano /etc/hosts
```

![](C:\Users\grahi\Pictures\Camera Roll\16.png)

lalu masuk ke dalam lxc_landing dan tambahkan subdomain

```markdown
sudo lxc-attach -n ubuntu_php7.4 
sudo nano /etc/hosts
```

![](C:\Users\grahi\Pictures\Camera Roll\17.png)

tambahkan juga subdomain kita ke dalam name server lxc_landing.dev lalu restart nginx

```markdown
cd /etc/nginx/sites-available
sudo service nginx restart
sudo nginx -t
sudo nginx -s reload
```

![](C:\Users\grahi\Pictures\Camera Roll\18.png)

lakukan Cname dan ping pada subdomain didalam lxc_landing

![](C:\Users\grahi\Pictures\Camera Roll\19.png)

lalu kita akses laravel

![](C:\Users\grahi\Pictures\Camera Roll\22.png)

akses Cl

![](C:\Users\grahi\Pictures\Camera Roll\23.png)

akses wordpress

![](C:\Users\grahi\Pictures\Camera Roll\24.png)

akses phpMyAdmin

![](C:\Users\grahi\Pictures\Camera Roll\25.png)