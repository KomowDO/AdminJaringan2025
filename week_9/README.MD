# Laporan Praktikum Workshop Administrasi Jaringan Week-9

<p align="center">
  <img src="./img/pens.png" alt="gambar" width="400">
</p>

## Dosen Pengampu  
**Dr. Ferry Astika Saputra, ST, M.Sc**  

## Disusun Oleh  
- **Nama**: Muhammad Arief Wicaksono Putra Santoso  
- **Kelas**: 2 D3 IT A  
- **NRP**: 3123500022  
- **Program Studi**: D3 Teknik Informatika  
- **Politeknik Elektronika Negeri Surabaya**  
- **Tahun Ajaran**: 2025/2026  

---

## Instalasi Apache2

### 1. Instalasi Apache2
Gunakan perintah `sudo apt -y install apache2` untuk menginstall apache2

<img src="./img/a1.jpg" alt="gambar" width="800">

### 2. Setting /etc/apache2/conf-enabled/security.conf
Gunakan perintah `sudo nano /etc/apache2/conf-enabled/security.conf` seperti gambar dibawah : 

<img src="./img/a2.jpg" alt="gambar" width="800">

Tambahkan dibawah ini sesuai foto yang saya berikan dibawah:
```bash

ServerTokens OS
ServerTokens Prod

```
<img src="./img/a2.1.jpg" alt="gambar" width="800">

### 3. Setting /etc/apache/mods-enabled/dir.conf
Gunakan perintah `sudo nano /etc/apache/mods-enabled/dir.conf` untuk membuka /etc/apache/mods-enabled/dir.conf

<img src="./img/a3.jpg" alt="gambar" width="800">

Lalu ketik sesuai gambar dibawah ini : 

<img src="./img/a3.1.jpg" alt="gambar" width="800">

### 4. Setting /etc/apache2/apache2.conf
Gunakan perintah `sudo nano /etc/apache2/apache2.conf` 

<img src="./img/a4.jpg" alt="gambar" width="800">

Lalu ketik seperti contoh dibawah sesuai contoh gambar : 

```bash

ServerName www.kelompok8.home

```

<img src="./img/a4.1.jpg" alt="gambar" width="800">


### 5. Setting /etc/apache2/sites-enabled/000-default.conf
Gunakan perintah `sudo nano /etc/apache2/sites-enabled/000-default.conf` untuk konfigurasi virtual host default Apache untuk port HTTP 

<img src="./img/a5.jpg" alt="gambar" width="800">

Lalu ketik perintah ini sesuai dari contoh gambar dibawah : 

```bash 

ServerAdmin webmaster@kelompok8.home
DocumentRoot /var/www/html

```
<img src="./img/a5.1.jpg" alt="gambar" width="800">


### 6. Reload apache2 service

Gunakan perintah `systemctl reload apache2.service`  untuk memuat ulang (reload) konfigurasi Apache tanpa menghentikan layanan Apache yang sedang berjalan 

<img src="./img/a6.jpg" alt="gambar" width="800">

### 7. Hasil dari Web Server
Gunakan IP `192.168.8.10` di browser untuk melihat apache2 web server sudah berfungsi atau belum. jika muncul seperti gambar dibawah maka web server-nya sudah aktif dan berjalan dengan baik.

<img src="./img/a7.jpg" alt="gambar" width="800">

----





`KomowDO`