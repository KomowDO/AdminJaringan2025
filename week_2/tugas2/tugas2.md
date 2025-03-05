# Laporan Praktikum Workshop Administrasi Jaringan

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

## Daftar Isi
- [Laporan Praktikum Workshop Administrasi Jaringan](#laporan-praktikum-workshop-administrasi-jaringan)
  - [Dosen Pengampu](#dosen-pengampu)
  - [Disusun Oleh](#disusun-oleh)
  - [Daftar Isi](#daftar-isi)
  - [Bab 4: Kontrol Proses](#bab-4-kontrol-proses)
    - [Komponen Proses](#komponen-proses)
    - [PID: Process ID](#pid-process-id)
    - [PPID: Parent Process ID](#ppid-parent-process-id)
    - [UID dan EUID: User ID dan Effective User ID](#uid-dan-euid-user-id-dan-effective-user-id)
    - [Siklus Hidup Proses](#siklus-hidup-proses)
    - [Signals](#signals)
    - [Perintah `kill`: Mengirim Signal](#perintah-kill-mengirim-signal)
    - [Perintah `ps`: Memantau Proses](#perintah-ps-memantau-proses)
    - [Perintah `top` dan `htop`: Pemantauan Real-Time](#perintah-top-dan-htop-pemantauan-real-time)
    - [Perintah `nice` dan `renice`: Mengubah Prioritas Proses](#perintah-nice-dan-renice-mengubah-prioritas-proses)
    - [Sistem File `/proc`](#sistem-file-proc)
    - [Perintah `strace` dan `truss`](#perintah-strace-dan-truss)
    - [Runaway Process](#runaway-process)
    - [Proses Periodik](#proses-periodik)
    - [Kegunaan Umum Tugas Terjadwal](#kegunaan-umum-tugas-terjadwal)

---

## Bab 4: Kontrol Proses

### Komponen Proses
Sebuah proses terdiri dari ruang alamat dan sejumlah struktur data dalam kernel. Ruang alamat adalah kumpulan halaman memori yang dialokasikan oleh kernel untuk proses tersebut. Halaman-halaman ini digunakan untuk menyimpan kode, data, dan stack proses. Struktur data dalam kernel mencatat status proses, prioritas, parameter penjadwalan, dan informasi lainnya.

Struktur data kernel menyimpan berbagai informasi untuk setiap proses, seperti:
- Pemetaan ruang alamat
- Status proses saat ini (misalnya, Running, Sleeping)
- Prioritas proses
- Sumber daya yang digunakan (CPU, memori, dll.)
- File dan port jaringan yang dibuka
- Masker sinyal (sinyal yang diblokir)
- Pemilik proses

**Thread** adalah unit eksekusi dalam sebuah proses. Sebuah proses dapat memiliki beberapa thread yang berbagi ruang alamat dan sumber daya yang sama. Thread digunakan untuk mencapai paralelisme dalam proses, memungkinkan beberapa tugas berjalan bersamaan. Thread sering disebut sebagai "proses ringan" karena lebih mudah dibuat dan dihancurkan dibandingkan proses.

[⬆ Kembali ke Daftar Isi](#daftar-isi)

---

### PID: Process ID
Setiap proses diidentifikasi oleh Process ID (PID) yang unik. PID adalah bilangan bulat yang diberikan oleh kernel saat proses dibuat. PID digunakan untuk merujuk proses dalam berbagai pemanggilan sistem.

[⬆ Kembali ke Daftar Isi](#daftar-isi)

---

### PPID: Parent Process ID
Setiap proses juga memiliki Parent Process ID (PPID), yaitu PID dari proses yang menciptakannya. PPID digunakan untuk merujuk proses induk dalam pemanggilan sistem.

[⬆ Kembali ke Daftar Isi](#daftar-isi)

---

### UID dan EUID: User ID dan Effective User ID
User ID (UID) adalah ID pengguna yang menjalankan proses. Effective User ID (EUID) adalah UID yang digunakan proses untuk menentukan akses ke sumber daya seperti file dan port jaringan. EUID mengontrol akses ke berbagai sumber daya sistem.

[⬆ Kembali ke Daftar Isi](#daftar-isi)

---

### Siklus Hidup Proses
Proses baru dibuat dengan menggunakan system call `fork`, yang membuat salinan dari proses yang ada. Proses baru memiliki PID yang berbeda dan informasi perhitungan sendiri.

Saat sistem boot, kernel membuat beberapa proses, termasuk `init` atau `systemd`, yang selalu memiliki PID 1. Proses ini menjalankan skrip startup sistem.

[⬆ Kembali ke Daftar Isi](#daftar-isi)

---

### Signals
Signal adalah notifikasi yang dikirim ke proses. Ada lebih dari 30 jenis signal yang digunakan untuk berbagai tujuan, seperti:
- Komunikasi antar proses
- Interupsi dari driver terminal
- Pengiriman oleh administrator menggunakan `kill`
- Notifikasi kesalahan fatal dari kernel
- Pemberitahuan kondisi khusus oleh kernel

[⬆ Kembali ke Daftar Isi](#daftar-isi)

---

### Perintah `kill`: Mengirim Signal
- **kill**: Mengirim sinyal ke proses berdasarkan PID. Secara default, sinyal `TERM` dikirim untuk meminta proses berhenti. Sinyal `KILL` (kill -9) tidak dapat diabaikan atau ditangkap.
  ```bash
  kill [-signal] pid

- **killall**: Menghentikan proses berdasarkan nama.
  ```bash
  killall [nama-proses]
  ```

- **pkill**: Menghentikan proses berdasarkan pola atau pengguna.
  ```bash
  pkill [opsi] <pola>
  ```

### Perintah `ps`: Memantau Proses
Perintah `ps` digunakan untuk memantau proses, menampilkan informasi seperti PID, UID, prioritas, dan penggunaan sumber daya.
  ```bash
  ps [opsi]
  ```

### Perintah `top` dan `htop`: Pemantauan Real-Time
- **top**: Menampilkan informasi sistem dan proses secara real-time.
  ```bash
  top
  ```

- **htop**: Versi interaktif dari `top` dengan antarmuka yang lebih baik.
  ```bash
  htop
  ```

### Perintah `nice` dan `renice`: Mengubah Prioritas Proses
- **nice**: Memulai proses dengan nilai niceness tertentu.
  ```bash
  nice -n nice_val [perintah]
  ```

- **renice**: Mengubah nilai niceness proses yang sedang berjalan.
  ```bash
  renice -n nice_val -p pid
  ```

### Sistem File `/proc`
Direktori `/proc` adalah sistem file semu yang mengekspos informasi tentang proses dan status sistem. Setiap proses memiliki subdirektori di `/proc` yang berisi detail seperti status, penggunaan memori, dan file yang dibuka.

### Perintah `strace` dan `truss`
- **strace** (Linux) dan **truss** (FreeBSD): Melacak system calls dan sinyal yang dilakukan oleh proses.
  ```bash
  strace -p pid
  ```

### Runaway Process
Runaway process adalah proses yang tidak merespons dan menggunakan 100% CPU. Untuk menghentikannya, gunakan perintah `kill`. Untuk investigasi, gunakan `strace` atau `truss`.

### Proses Periodik
Proses periodik adalah tugas yang dijalankan secara terjadwal. Alat utama untuk ini adalah `cron` dan `systemd timer`.

- **Cron**: Menjadwalkan perintah berdasarkan waktu.
  ```bash
  * * * * * command
  ```

- **Systemd Timer**: Alternatif modern untuk cron dengan fleksibilitas lebih.
  ```bash
  systemctl list-timers
  ```

### Kegunaan Umum Tugas Terjadwal
- Mengirim email otomatis
- Membersihkan file sistem
- Rotasi file log
- Menjalankan batch jobs
- Backup dan mirroring data

Dengan memahami kontrol proses, administrator sistem dapat mengelola sumber daya secara efisien dan memastikan sistem berjalan lancar.
```

Anda bisa menyalin dan menempelkan teks di atas ke dalam file Markdown (`.md`) untuk mendapatkan format yang rapi dan terstruktur.


