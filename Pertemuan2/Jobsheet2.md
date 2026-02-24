<h1 align="center">JOBSHEET 2 - SISTEM OPERASI</h1>


**Nama**       : M. Javier Thufail  
**NIM**        : 254107020019  
**Kelas**      : TI 1-G  
**No. Absen**  : 18  

---
## Praktikum 2.1 — Identifikasi CPU dan Memori
## 1. Tampilkan informasi CPU:
Perintah:

```bash
lscpu
```

📌 *Kode 1.1 – Melihat informasi CPU*

![Informasi CPU](Foto/lscpu.png)

Keterangan:
Perintah `lscpu` digunakan untuk menampilkan detail arsitektur CPU seperti jumlah core, thread, dan model prosesor.

## 2. Tampilkan ringkasan memori:
Perintah:

```bash
free -h
```

📌 *Kode 1.2 – Melihat penggunaan memori*

![Informasi Memori](Foto/free-h.png)

Keterangan:
Perintah `free -h` digunakan untuk melihat total RAM, memori yang terpakai, serta swap dalam format yang mudah dibaca (human-readable).

## 3. (Opsional) cek informasi hardware dari DMI/BIOS (butuh sudo):
Perintah:

```bash
sudo dmidecode -t system
```

📌 *Kode 1.3 – Informasi DMI (opsional)*

![Informasi DMI](Foto/sudoDmi.png)

Keterangan:
Perintah ini menampilkan informasi sistem dari BIOS/DMI seperti manufacturer, product name, dan versi sistem.

## 🔎 Latihan 2.1
Catat: (1) jumlah CPU(s), core/thread, (2) total RAM, (3) total swap. Jelaskan perbedaan RAM vs swap dalam 2–3 kalimat.
#### 📌 Data yang Diperoleh:

1. Jumlah CPU(s)        : (4 `lscpu`)
2. Core / Thread        : (1 `lscpu`)
3. Total RAM            : (3.8 `free -h`)
4. Total Swap           : (0B `free -h`)

#### ✍️ Penjelasan RAM vs Swap

RAM adalah memori utama yang digunakan sistem untuk menjalankan aplikasi secara aktif dan memiliki kecepatan sangat tinggi.  
Swap adalah ruang pada storage (HDD/SSD) yang digunakan sebagai memori cadangan ketika RAM hampir penuh, tetapi kecepatannya lebih lambat dibandingkan RAM.

---

## Praktikum 2.2 — Identifikasi Perangkat PCI/USB dan Driver