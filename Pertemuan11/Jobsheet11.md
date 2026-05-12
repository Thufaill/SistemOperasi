<h1 align="center">JOBSHEET 11 - SISTEM OPERASI</h1>


**Nama**       : M. Javier Thufail  
**NIM**        : 254107020019  
**Kelas**      : TI 1-G  
**No. Absen**  : 18  

---
<h1 align="center">Manajemen File & User/Group</h2>



Praktikum 9.1 — Permissions

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