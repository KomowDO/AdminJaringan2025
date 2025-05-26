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
## Laporan Instalasi dan Konfigurasi Mail Server (Postfix, Dovecot, Mailutils)

### Pendahuluan: Pengenalan Email (Surat Elektronik)

Email atau surat elektronik adalah metode pertukaran pesan secara digital melalui jaringan internet. Beberapa komponen utama dalam sistem email meliputi:

- Alamat Email: Identitas unik pengguna, biasanya dalam format nama@domain.com.

- Email Client: Aplikasi untuk mengelola email, seperti Gmail, Outlook, atau Thunderbird.

- Email Server: Sistem yang menyimpan dan mendistribusikan email kepada penerima.

###  Cara Mengirim Email

- Buat pesan baru menggunakan email client.

- Isi alamat tujuan pada kolom "To".

- Tambahkan subjek untuk merangkum isi pesan.

- Tulis isi pesan.

- Lampirkan file jika diperlukan.

- Klik "Kirim" untuk mengirim pesan ke server tujuan.

### Fitur tambahan seperti CC, BCC, Reply, dan Forward juga tersedia untuk memudahkan komunikasi dengan banyak pihak.

## Konsep Sistem Email
Email adalah layanan internet yang memungkinkan pengguna mengirim pesan, baik teks maupun media (gambar, audio, video), ke pengguna lain di seluruh dunia. Konsep ini serupa dengan sistem pos konvensional: ada pengirim dan penerima.

### Komponen Utama Sistem Email:
User Agent (UA): Aplikasi yang digunakan untuk menyusun, membaca, dan mengelola email.

- Message Transfer Agent (MTA): Komponen yang memindahkan email antar server menggunakan protokol SMTP.

- Mailbox: Tempat penyimpanan email masuk milik pengguna di sistem.

- Spool File: Lokasi sementara untuk email yang akan dikirim. Email dari UA disimpan di sini sebelum diproses oleh MTA.

### Sistem email juga mendukung mailing list, yakni satu nama alias yang mewakili banyak alamat email.

- Layanan dalam Sistem Email
Komposisi: Proses membuat atau membalas email.

- Transfer: Pengiriman email dari pengirim ke penerima.

- Pelaporan: Memberikan status pengiriman (berhasil, gagal, ditolak).

- Tampilan: Menyajikan email dalam format yang bisa dibaca oleh pengguna.

- Disposition: Tindakan penerima setelah menerima email, seperti membaca, menyimpan, atau menghapus.

## Kelebihan dan Kekurangan Email

### Kelebihan:

- Komunikasi cepat dan efisien ke seluruh dunia.

- Dapat menyimpan dan mencari pesan lama dengan mudah.

- Mendukung lampiran file seperti dokumen dan media.

- Biaya murah dibandingkan surat atau faks.

- Tersedia setiap saat (24/7).

### Kekurangan:

- Rentan terhadap spam dan serangan phishing.

- Informasi dapat menumpuk dan membuat pengguna kewalahan.

- Mengurangi interaksi tatap muka.

- Risiko salah paham karena tidak adanya nada suara atau ekspresi.

- Tergantung pada kestabilan server.


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


### 19. Gunakan perintah `newaliases` dan `systemctl restart postfix` untuk restart

<img src="./img/p3.jpg" alt="gambar" width="800">


--------

## Instalasi Dovecot
### 1. Instalasi Dovecot menggunakan perintah `sudo apt -y install dovecot-core dovecot-pop3d dovecot-imapd` untuk mendownload dovecot

<img src="img/d1.jpg" alt="gambar" width="800">

### 2. Konfigurasi dovecot menggunakan perintah `sudo nano /etc/dovecot/conf.d/10-auth.conf` untuk membuka /etc/dovecot/conf.d/10-auth.conf, dan tambahkan `disable_plaintext_auth = no` di line 10


<img src="img/d2.jpg" alt="gambar" width="800">


### Tambahkan `auth_mechanisms = plain login` di line 100

<img src="img/d3.jpg" alt="gambar" width="800">

### 3. Gunakan perintah `sudo nano /etc/dovecot/conf.d/10-mail.conf` untuk membuka /etc/dovecot/conf.d/10-mail.conf, dan tambahkan `mail_location = maildir:~/Maildir` di line 30 

<img src="img/d5.jpg" alt="gambar" width="800">



### 4. Gunakan perintah `sudo nano /etc/dovecot/conf.d/10-master.conf` untuk membuka /etc/dovecot/conf.d/10-master.conf dan tambahkan konfigurasi dibawah ini di line 107-109

```bash
# Postfix smtp-auth
  unix_listener /var/spool/postfix/private/auth {
    mode = 0666
    user = postfix
    group = postfix
  }

```

<img src="img/d6.jpg" alt="gambar" width="800">

### 5. Gunakan perintah `systemctl restart dovecot` untuk restart dovecot

<img src="img/d7.jpg" alt="gambar" width="800">

--------

## Instalasi Maildir

### 1. Instalasi Maildir menggunakan perintah `sudo apt -y install mailutils` untuk mendownload mailutils

<img src="img/m1.jpg" alt="gambar" width="800">

### 2. Gunakan perintah `echo 'export MAIL=$HOME/Maildir/' >> /etc/profile.d/mail.sh` 

<img src="img/m2.jpg" alt="gambar" width="800">

#### Perintah ini mengatur variabel lingkungan MAIL agar menunjuk ke folder Maildir pengguna, dan menyimpannya di /etc/profile.d/mail.sh agar aktif otomatis saat login. 

### 3. Untuk menambahkan user baru menggunakan perintah `adduser "nama user"` seperti contoh dibawah : 

<img src="img/m3.jpg" alt="gambar" width="800">

### 4. Test mengirim pesan ke user lain dengan perintah `mail "nama user"@localhost"`

<img src="img/m4.jpg" alt="gambar" width="800">

### 5. untuk melihat pesan yang dikirim oleh user lain kita hanya perlu menggunakan perintah `mail`

<img src="img/m5.jpg" alt="gambar" width="800">