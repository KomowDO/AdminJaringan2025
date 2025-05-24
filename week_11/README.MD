# Laporan Praktikum Workshop Administrasi Jaringan Week-11

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

## Instalasi POSTFIX
### 1. Instalasi Postfix menggunakan perintah `sudo apt-get install postfix`

<img src="./img/p1.jpg" alt="gambar" width="800">


### 2. Lalu gunakan perintah `sudo nano /etc/postfix/main.cf`

<img src="./img/p2.1.jpg" alt="gambar" width="800">

### 3. Tulis  `mail_owner = postfix` di line 86

<img src="./img/p2.2.jpg" alt="gambar" width="800">

### 4. Tulis `myhostname = mail.kelompok8.home` di line 98

<img src="./img/p2.3.jpg" alt="gambar" width="800">

### 5. Tulis `mydomain = kelompok8.home` di line 106


<img src="./img/p2.4.jpg" alt="gambar" width="800">

### 6. Tulis `myorigin = $mydomain` di line 127

<img src="./img/p2.5.jpg" alt="gambar" width="800">

### 7. Tulis `inet_interfaces = all`  di line 141

<img src="./img/p2.6.jpg" alt="gambar" width="800">

### 8. Tulis `mydestination = $myhostname, localhost.$mydomain, localhost, $mydomain` di line 189

<img src="./img/p2.7.jpg" alt="gambar" width="800">

### 9. Tulis `local_recipient_maps = unix:passwd.byname $alias_maps` di line 232

<img src="./img/p2.8.jpg" alt="gambar" width="800">

### 10. Tulis `mynetworks_style = subnet` di line 277

<img src="./img/p2.9.jpg" alt="gambar" width="800">

### 11. Tulis `mynetworks = 192.168.8.10/24` di line 294

<img src="./img/p2.10.jpg" alt="gambar" width="800">

### 12. Tulis `alias_maps = hash:/etc/aliases` di line 416

<img src="./img/p2.11.jpg" alt="gambar" width="800">

### 13. Tulis `alias_database = hash:/etc/aliases` di line 427

<img src="./img/p2.12.jpg" alt="gambar" width="800">

### 14. Tulis `home_mailbox = Maildir/` di line 449

<img src="./img/p2.13.jpg" alt="gambar" width="800">

### 15. Tulis `smtpd_banner = $myhostname ESMTP` seperti berikut:

<img src="./img/p2.14.jpg" alt="gambar" width="800">

### 16. Tulis `sendmail_path = /usr/sbin/postfix` di line 659. `newaliases_path = /usr/bin/newaliases` di line 664. `setgid_group = postdrop` di line 675.


<img src="./img/p2.15.jpg" alt="gambar" width="800">

### 17. Tulis `inet_protocols = ipv4` di line 692. `disable_vrfy_command = yes`. `smtpd_helo_required = yes`. `message_size_limit = 10240000`

<img src="./img/p2.16.jpg" alt="gambar" width="800">


### 18. Tulis ini seperti gambar dibawah : 

```bash
# SMTP-Auth settings
smtpd_sasl_type = dovecot
smtpd_sasl_path = private/auth
smtpd_sasl_auth_enable = yes
smtpd_sasl_security_options = noanonymous
smtpd_sasl_local_domain = $myhostname
smtpd_recipient_restrictions = 
  permit_mynetworks,
  permit_sasl_authenticated,
  reject_unauth_destination

```

<img src="./img/p2.17.jpg" alt="gambar" width="800">