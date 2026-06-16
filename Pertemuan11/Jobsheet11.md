<h1 align="center">JOBSHEET 11 - SISTEM OPERASI</h1>


**Nama**       : M. Javier Thufail  
**NIM**        : 254107020019  
**Kelas**      : TI 1-G  
**No. Absen**  : 18  

---
<h1 align="center">Manajemen File & User/Group</h2>



Praktikum 9.1 — Permissions
### Langkah 1: Buat direktori kerja dan dua file uji
```
vier@UBUNTU:~$ mkdir ~/lab-permissions && cd ~/lab-permissions
vier@UBUNTU:~/lab-permissions$ echo "data rahasia" > secret.txt
vier@UBUNTU:~/lab-permissions$ echo '#!/bin/bash' > myscript.sh
vier@UBUNTU:~/lab-permissions$ echo 'echo Hello' >> myscript.sh
vier@UBUNTU:~/lab-permissions$ ls -la
total 16
drwxrwxr-x  2 vier vier 4096 May  6 10:51 .
drwxr-x--- 30 vier vier 4096 May  6 10:50 ..
-rw-rw-r--  1 vier vier   23 May  6 10:51 myscript.sh
-rw-rw-r--  1 vier vier   13 May  6 10:50 secret.txt
```
### Langkah 2: Jadikan secret.txt privat hanya untuk owner
```
vier@UBUNTU:~/lab-permissions$ chmod 600 secret.txt
vier@UBUNTU:~/lab-permissions$ ls -l secret.txt
-rw------- 1 vier vier 13 May  6 10:50 secret.txt
```
### Langkah 3: Jadikan myscript.sh dapat dijalankan
```
vier@UBUNTU:~/lab-permissions$ chmod 755 myscript.sh
vier@UBUNTU:~/lab-permissions$ ls -l myscript.sh
-rwxr-xr-x 1 vier vier 23 May  6 10:51 myscript.sh
vier@UBUNTU:~/lab-permissions$ ./myscript.sh
Hello
```
### Langkah 4: Buat direktori bersama dan amati efek SGID sederhana
vier@UBUNTU::~/lab-permissions$ mkdir shared-dir
vier@UBUNTU:~/lab-permissions$ chmod g+s shared-dir
vier@UBUNTU:~/lab-permissions$ ls -ld shared-dir
drwxrwsr-x 2 vier vier 4096 May  6 10:55 shared-dir
```
### Langkah 5: Uji efek umask pada file baru
```
vier@UBUNTU:~/lab-permissions$ umask
vier@UBUNTU::~/lab-permissions$ umask 027
vier@UBUNTU:~/lab-permissions$ touch testfile-027
vier@UBUNTU:~/lab-permissions$ ls -l testfile-027
-rw-r----- 1 vier vier 0 May  6 10:56 testfile-02
```
### Analisis

1. Mengapa secret.txt tidak dapat dibaca oleh group dan others setelah chmod 600?
```
Karena chmod 600 hanya memberikan akses membaca dan menulis isi file ke user, dan untuk group dan other tidak diberikan izin apapun dengan pemberian angka 0 pada group dan other
```
2. Apa perbedaan arti 600 dan 755 terhadap file yang diuji?
```
600 : hanya user yang dapat membaca dan menulis isi file
755 : user dapat membaca, menulis, mengeksekusi file, group dapat membaca dan mengeksekusi, dan other dapat menbaca dan mengeksekusi
```
3. Setelah umask 027, permission apa yang dihasilkan untuk file baru, dan mengapa bukan 777?
```
permission yang dihasilkan untuk file baru yaitu 640
```

### Tantangan

Ubah owner atau group salah satu file uji ke akun atau group lain yang tersedia di sistem, kemudian jelaskan
perubahan output ls -l sebelum dan sesudahnya.

```
vier@UBUNTU:~/lab-permissions$ ls -l
total 12
-rwxr-xr-x 1 vier vier   23 May  6 10:51 myscript.sh
-rw------- 1 vier vier   13 May  6 10:50 secret.txt
drwxrwsr-x 2 vier vier 4096 May  6 10:55 shared-dir
-rw-r----- 1 vier vier    0 May  6 10:56 testfile-027
vier@UBUNTU:~/lab-permissions$ chmod 640 secret.txt
vier@UBUNTU:~/lab-permissions$ ls -l
total 12
-rwxr-xr-x 1 vier vier   23 May  6 10:51 myscript.sh
-rw-r----- 1 vier vier   13 May  6 10:50 secret.txt
drwxrwsr-x 2 vier vier 4096 May  6 10:55 shared-dir
-rw-r----- 1 vier vier    0 May  6 10:56 testfile-027
```
perintah chmod 640 secret.txt, mengubah permission file yang awalnya hanya user yang dapat membaca dan menulis isi file(-rw-------), menjadi user membaca dan menulis isi file, dan group dapat membaca (-rw-r-----)


Praktikum 9.2 — ACL

Praktikum 9.3A — Membuat dan Mengelola User

Praktikum 9.3B — Group Management

Praktikum 9.3C — Password Aging Policy

Praktikum 9.4 — Konfigurasi sudo

Praktikum 9.5 — Disk Quota

1.7 Latihan

Latihan Latihan 9.A — Audit dan Kolaborasi
1. Temukan file SUID aktif dengan find / -perm -4000 -type f 2>/dev/null, lalu jelaskan
tiga file yang Anda kenali beserta alasannya.
2. Cari direktori world-writable dan tentukan mana yang valid dan mana yang berisiko.
3. Rancang konfigurasi permission standar dan ACL untuk direktori proyek /srv/webapp/ agar
group webapp-team dapat menulis, user deploy hanya membaca, dan file baru selalu mewarisi
group proyek.

Latihan Latihan 9.B — Kebijakan Akun dan Quota
Tuliskan langkah untuk membuat user intern, menambahkannya ke group labgroup, memaksa pergantian password tiap 45 hari (warning 7 hari), memberi izin sudo hanya untuk systemctl status, dan
menetapkan quota ruang serta inode sederhana pada /home/
---
*Jobsheet 11 - Sistem Operasi*