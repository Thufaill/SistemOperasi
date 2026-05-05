<h1 align="center">JOBSHEET 9 - SISTEM OPERASI</h1>


**Nama**       : M. Javier Thufail  
**NIM**        : 254107020019  
**Kelas**      : TI 1-G  
**No. Absen**  : 18  

---
<h1 align="center">PEMOGRAMAN BASH</h2>

## Praktikum 7.1 Script Pertama: Laporan Sistem

### 1. Buat workspace praktikum
```bash
vier@UBUNTU:~/praktikum-os/week07-bash$ mkdir -p ~/praktikum-os/week09/{scripts,logs,data}

vier@UBUNTU:~/praktikum-os/week07-bash$ cd ~/praktikum-os/week09/scripts
vier@UBUNTU:~/praktikum-os/week09/scripts$
```
### 2. Buat script dengan nano
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ nano laporan-sistem.sh
```
### 3. Ketik isi berikut, simpan ( Ctrl+O Enter ), lalu keluar ( Ctrl+X )
```bash
#!/bin/bash
# Script: laporan-sistem.sh
echo " ================================"
echo "   LAPORAN SISTEM"
echo " ================================"
echo " Tanggal  : $(date '+%A, %d %B %Y')"
echo " Jam      : $(date '+%H:%M:%S')"
echo " Hostname : $(hostname)"
echo " User     : $(whoami)"
echo " CPU core : $(nproc)"
echo " RAM bebas: $(free -h | awk '/^Mem/ {print $4}')"
echo " Disk /   : $(df -h / | awk 'NR==2 {print $5}') terpakai "
echo " ================================"
```
### 4. Beri izin dan jalankan
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ chmod +x laporan-sistem.sh

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./laporan-sistem.sh
 ================================
   LAPORAN SISTEM
 ================================
 Tanggal  : Tuesday, 05 May 2026
 Jam      : 15:06:18
 Hostname : UBUNTU
 User     : vier
 CPU core : 4
 RAM bebas: 148Mi
 Disk /   : 33% terpakai 
 ================================
 ```
## Latihan 9.1

### Modifikasi laporan-sistem.sh agar menyimpan output ke file laporan-YYYY-MM-DD.txt sekaligus menampilkannya di terminal. Petunjuk: gunakan tee yang sudah dipelajari di bab sebelumnya
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ nano laporan-sistem.sh
#!/bin/bash
# Script: laporan-sistem.sh
{
echo " ================================"
echo "   LAPORAN SISTEM"
echo " ================================"
echo " Tanggal  : $(date '+%A, %d %B %Y')"
echo " Jam      : $(date '+%H:%M:%S')"
echo " Hostname : $(hostname)"
echo " User     : $(whoami)"
echo " CPU core : $(nproc)"
echo " RAM bebas: $(free -h | awk '/^Mem/ {print $4}')"
echo " Disk /   : $(df -h / | awk 'NR==2 {print $5}') terpakai "
echo " ================================"
} | tee "laporan-$(date +%F).txt"

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./laporan-sistem.sh
 ================================
   LAPORAN SISTEM
 ================================
 Tanggal  : Tuesday, 05 May 2026
 Jam      : 15:08:43
 Hostname : UBUNTU
 User     : vier
 CPU core : 4
 RAM bebas: 142Mi
 Disk /   : 33% terpakai 
 ================================
vier@UBUNTU:~/praktikum-os/week09/scripts$ ls
laporan-2026-05-05.txt  laporan-sistem.sh
vier@UBUNTU:~/praktikum-os/week09/scripts$ cat laporan-2026-05-05.txt
 ================================
   LAPORAN SISTEM
 ================================
 Tanggal  : Tuesday, 05 May 2026
 Jam      : 15:07:40
 Hostname : UBUNTU
 User     : vier
 CPU core : 4
 RAM bebas: 145Mi
 Disk /   : 33% terpakai 
 ================================
vier@UBUNTU:~/praktikum-os/week09/scripts$ 
```
## Praktikum 7.2 Script Info Sistem dengan Argumen

### 1. Buat script
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/info-sistem.sh
```
### 2. Ketik isi berikut
```bash
#!/bin/bash
# Script: laporan-sistem.sh
echo " ================================"
echo "   LAPORAN SISTEM"
echo " ================================"
echo " Tanggal  : $(date '+%A, %d %B %Y')"
echo " Jam      : $(date '+%H:%M:%S')"
echo " Hostname : $(hostname)"
echo " User     : $(whoami)"
echo " CPU core : $(nproc)"
echo " RAM bebas: $(free -h | awk '/^Mem/ {print $4}')"
echo " Disk /   : $(df -h / | awk 'NR==2 {print $5}') terpakai "
echo " ================================"
```
### 3. Simpan, beri izin, uji dengan berbagai kombinasi argumen
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ chmod +x info-sistem.sh

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./info-sistem.sh 
Admin   : Tidak dikenal 
Tanggal : 2026-05-05 15:20:22 
Disk /  : 33% terpakai
Batas   : 80% 
STATUS  : Normal ( sisa toleransi 47%) 

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./info-sistem.sh "Dian" 50
Admin   : Dian 
Tanggal : 2026-05-05 15:21:58 
Disk /  : 33% terpakai
Batas   : 50% 
STATUS  : Normal ( sisa toleransi 17%) 

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./info-sistem.sh "Dian" 10
Admin   : Dian 
Tanggal : 2026-05-05 15:22:09 
Disk /  : 33% terpakai
Batas   : 10% 
STATUS  : PERINGATAN - disk melebihi batas !
```
## Latihan 9.2

### Buat script kalkulator.sh yang menerima tiga argumen: <angka1> <operator> <angka2> dengan operator +, -, *, atau /. Contoh: ./kalkulator.sh 20 + 5 menghasilkan 25. Gunakan case untuk memilih operasi, dan validasi jika argumen tidak lengkap
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/kalkulator.sh
#!/bin/bash
# Penggunaan: ./info-sistem.sh [nama-admin] [batas-disk-persen]

ADMIN=${1:-"Tidak dikenal"}
BATAS=${2:-80}
TANGGAL=$(date '+%F %T')
DISK_PERSEN=$(df / | awk 'NR==2 {print $5}' | tr -d '%')

echo "Admin   : $ADMIN "
echo "Tanggal : $TANGGAL "
echo "Disk /  : ${DISK_PERSEN}% terpakai"
echo "Batas   : ${BATAS}% "

if [ "$DISK_PERSEN" -gt "$BATAS" ]; then
echo "STATUS  : PERINGATAN - disk melebihi batas !"
else
SISA=$((BATAS - DISK_PERSEN))
echo "STATUS  : Normal ( sisa toleransi ${SISA}%) "
fi

vier@UBUNTU:~/praktikum-os/week09/scripts$ chmod +x kalkulator.sh

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./kalkulator.sh 100 + 5
ANGKA1  : 100 
Operator: +
Angka 2 : 5 
Hasil : 100 + 5 = 105

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./kalkulator.sh 100 - 5
ANGKA1  : 100 
Operator: -
Angka 2 : 5 
Hasil : 100 - 5 = 95

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./kalkulator.sh 100 - 5
ANGKA1  : 100 
Operator: -
Angka 2 : 5 
Hasil : 100 - 5 = 95
v
ier@UBUNTU:~/praktikum-os/week09/scripts$ ./kalkulator.sh 10 / 0
ANGKA1  : 10 
Operator: /
Angka 2 : 0 
./kalkulator.sh: line 23: ANGKA1 / ANGKA2: division by 0 (error token is "ANGKA2")
vier@UBUNTU:~/praktikum-os/week09/scripts$ 
```
## Praktikum 7.3 Script Grading dan Menu Interaktif

### 1. Buat script grading (menggunakan if dan for)
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/grading-batch.sh
```
### 2. Ketik isi berikut
```bash
#!/bin/bash
# Script : grading-batch.sh
# Proses daftar nilai mahasiswa
MAHASISWA=("Andi:92" "Budi:73" "Citra:55" "Deni:80" "Eka:45")
echo "=== HASIL GRADING ==="
for ENTRI in "${MAHASISWA[@]}"; do
NAMA=$(echo "$ENTRI" | cut -d: -f1)
NILAI=$(echo "$ENTRI" | cut -d: -f2)
if [ "$NILAI" -ge 85 ]; then
GRADE="A"
elif [ "$NILAI" -ge 75 ]; then
GRADE="B"
elif [ "$NILAI" -ge 65 ]; then
GRADE="C"
elif [ "$NILAI" -ge 55 ]; then
GRADE="D"
else
GRADE="E"
fi
printf " %-10s %3d %s\n" "$NAMA" "$NILAI" "$GRADE"
done
echo "====================="
```
### 3. Simpan, beri izin, dan jalankan
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ chmod +x ~/praktikum-os/week09/scripts/grading-batch.sh
vier@UBUNTU:~/praktikum-os/week09/scripts$ ./grading-batch.sh
=== HASIL GRADING ===
 Andi        92 A
 Budi        73 C
 Citra       55 D
 Deni        80 B
 Eka         45 E
=====================
```
### 4. Buat script menu interaktif (while + case)
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/menu-sistem.sh
```
### 5. Ketik isi berikut
```bash
#!/bin/bash
# Menu interaktif pemantauan sistem
while true; do
echo ""
echo "===== MENU MONITOR ====="
echo "1) Info disk"
echo "2) Info memori"
echo "3) Proses teratas"
echo "4) Keluar"
echo -n "Pilih [1-4]: "
read PILIHAN
case $PILIHAN in
1) df -h ;;
2) free -h ;;
3) ps aux --sort=-%cpu | head -6 ;;
4) echo "Sampai jumpa!"; exit 0 ;;
*) echo "Pilihan tidak valid." ;;
esac
done
```
### 6. Beri izin dan jalankan, coba setiap opsi
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ chmod +x ~/praktikum-os/week09/scripts/menu-sistem.sh
vier@UBUNTU:~/praktikum-os/week09/scripts$ ./menu-sistem.sh

===== MENU MONITOR =====
1) Info disk
2) Info memori
3) Proses teratas
4) Keluar
Pilih [1-4]: 1
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           392M  2.1M  390M   1% /run
/dev/sda2        30G  9.2G   19G  33% /
tmpfs           2.0G     0  2.0G   0% /dev/shm
tmpfs           5.0M  8.0K  5.0M   1% /run/lock
tmpfs           392M  116K  392M   1% /run/user/1000

===== MENU MONITOR =====
1) Info disk
2) Info memori
3) Proses teratas
4) Keluar
Pilih [1-4]: 2
               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       2.5Gi       208Mi        73Mi       1.1Gi       1.3Gi
Swap:             0B          0B          0B

===== MENU MONITOR =====
1) Info disk
2) Info memori
3) Proses teratas
4) Keluar
Pilih [1-4]: 3
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
vier        5577 66.6  0.1  22424  4888 pts/0    R+   15:57   0:00 ps aux --sort=-%cpu
vier        1989 23.8  8.6 4983936 345468 ?      Ssl  14:56  14:43 /usr/bin/gnome-shell
vier        2671 19.2 17.2 12423964 690444 ?     Sl   14:56  11:48 /snap/firefox/8247/usr/lib/firefox/firefox
vier        3156  5.7 13.5 3735520 544484 ?      Sl   14:56   3:30 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:32095 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {933018c5-4b7d-4e78-96fc-ea401571801b} -parentPid 2671 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 6 tab
vier        3525  2.9 11.3 3097004 455812 ?      Sl   14:56   1:47 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:43483 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {640c1352-3e77-4aee-94eb-7853d1673376} -parentPid 2671 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 7 tab

===== MENU MONITOR =====
1) Info disk
2) Info memori
3) Proses teratas
4) Keluar
Pilih [1-4]: 4
Sampai jumpa!
```
## Latihan 9.3

### Tambahkan ke script grading-batch.sh sebuah ringkasan di bagian bawah yang menampilkan: jumlah mahasiswa per grade (A, B, C, D, E) menggunakan perulangan for kedua yang mengiterasi array MAHASISWA
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/grading-batch.sh
#!/bin/bash
# Script : grading-batch.sh
# Proses daftar nilai mahasiswa
MAHASISWA=("Andi:92" "Budi:73" "Citra:55" "Deni:80" "Eka:45")
echo "=== HASIL GRADING ==="
for ENTRI in "${MAHASISWA[@]}"; do
NAMA=$(echo "$ENTRI" | cut -d: -f1)
NILAI=$(echo "$ENTRI" | cut -d: -f2)
if [ "$NILAI" -ge 85 ]; then
GRADE="A"
elif [ "$NILAI" -ge 75 ]; then
GRADE="B"
elif [ "$NILAI" -ge 65 ]; then
GRADE="C"
elif [ "$NILAI" -ge 55 ]; then
GRADE="D"
else
GRADE="E"
fi
printf " %-10s %3d %s\n" "$NAMA" "$NILAI" "$GRADE"
done
echo "====================="

echo "=== JUMLAH MAHASISWA PER GRADE ==="
for G in A B C D E; do
COUNT=0
for ENTRI in "${MAHASISWA[@]}"; do
NILAI=$(echo "$ENTRI" | cut -d: -f2)
if [ "$NILAI" -ge 85 ]; then
GRADE="A"
elif [ "$NILAI" -ge 75 ]; then
GRADE="B"
elif [ "$NILAI" -ge 65 ]; then
GRADE="C"
elif [ "$NILAI" -ge 55 ]; then
GRADE="D"
else
GRADE="E";
fi
if [ "$GRADE" == "$G" ]; then
((COUNT++))
fi
done
echo "Grade $G: $COUNT"
done

praditadf@praditadf-VirtualBox:~/praktikum-os/week09/scripts$ ./grading-batch.sh 
=== HASIL GRADING ===
 Andi        92 A
 Budi        73 C
 Citra       55 D
 Deni        80 B
 Eka         45 E
=====================
=== JUMLAH MAHASISWA PER GRADE ===
Grade A: 1
Grade B: 1
Grade C: 1
Grade D: 1
Grade E: 1

vier@UBUNTU:~/praktikum-os/week09/scripts$ chmod +x ~/praktikum-os/week09/scripts/grading-batch.sh

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./grading-batch.sh
=== HASIL GRADING ===
 Andi        92 A
 Budi        73 C
 Citra       55 D
 Deni        80 B
 Eka         45 E
=====================
=== JUMLAH MAHASISWA PER GRADE ===
Grade A: 1
Grade B: 1
Grade C: 1
Grade D: 1
Grade E: 1
vier@UBUNTU:~/praktikum-os/week09/scripts$ 
```
## Praktikum 7.4 Library Fungsi Validasi

### 1. Buat file library
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/lib-validasi.sh
```
### 2. Ketik isi berikut
```bash
#!/bin/bash
# lib-validasi.sh - Library fungsi validasi

adalah_angka() {
[[ "$1" =~ ^[0-9]+$ ]]
}
file_bisa_dibaca() {
[ -f  "$1" ] && [ -r "$1" ]
}
error_exit() {
echo "ERROR: $1" >&2
exit 1
}
info() { echo "[ INFO ] $1"; }
sukses() { echo "[ OK ] $1"; }
```
### 3. Buat script yang menggunakan library
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/pakai-library.sh
```
### 4. Ketik isi berikut
```bash
#!/bin/bash
# Muat library (seperti import di Java)
source ~/praktikum-os/week09/scripts/lib-validasi.sh
ANGKA=$1
FILE=$2
[ -z "$ANGKA" ] || [ -z "$FILE" ] && \
error_exit "Penggunaan: $0 <angka> <path-file>"
if adalah_angka "$ANGKA"; then
sukses "Input '$ANGKA' adalah angka valid"
else
error_exit "'$ANGKA' bukan angka"
fi
if file_bisa_dibaca "$FILE"; then
sukses "File '$FILE' bisa dibaca"
info "Jumlah baris: $(wc -l < "$FILE")"
else
error_exit "File '$FILE' tidak ada atau tidak bisa dibaca "
fi
```
### 5. Beri izin dan uji semua skenario
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ chmod +x ~/praktikum-os/week09/scripts/pakai-library.sh

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./pakai-library.sh 42 /etc/hostname
[ OK ] Input '42' adalah angka valid
[ OK ] File '/etc/hostname' bisa dibaca
[ INFO ] Jumlah baris: 1

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./pakai-library.sh abc /etc/hostname
ERROR: 'abc' bukan angka

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./pakai-library.sh 42 /tidak-ada.txt
[ OK ] Input '42' adalah angka valid
ERROR: File '/tidak-ada.txt' tidak ada atau tidak bisa dibaca 

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./pakai-library.sh
ERROR: Penggunaan: ./pakai-library.sh <angka> <path-file>
```
## Latihan 9.4

### Tambahkan fungsi konfirmasi() ke lib-validasi.sh. Fungsi ini menampilkan pertanyaan, membaca input Y/N dari user, mengembalikan 0 jika Y dan 1 jika N. Buat script demo yang memanggil fungsi ini sebelum menghapus sebuah file
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/lib-validasi.sh

konfirmasi() {
read -rp "$1 (Y/N): " hasil
case "$hasil" in
[Yy]) return 0 ;;
[Nn]) return 1 ;;
*) echo "Masukkan Y atau N." ;;
esac
}

vier@UBUNTU:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/hapus-file.sh

#!/bin/bash
# Load library
source ./lib-validasi.sh
file="$1"
[ -z "$file" ] && error_exit "Nama file harus diberikan."
file_bisa_dibaca "$file" || error_exit "File tidak ditemukan atau tidak bisa dibaca."
if konfirmasi "Apakah Anda yakin ingin menghapus file '$file'?"; then
    rm "$file" && sukses "File berhasil dihapus."
else
    info "Penghapusan dibatalkan."
fi

vier@UBUNTU:~/praktikum-os/week09/scripts$ chmod +x hapus-file.sh

vier@UBUNTU:~/praktikum-os/week09/scripts$ touch a.txt

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./hapus-file.sh a.txt
Apakah Anda yakin ingin menghapus file 'a.txt'? (Y/N): n
[ INFO ] Penghapusan dibatalkan.

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./hapus-file.sh a.txt
Apakah Anda yakin ingin menghapus file 'a.txt'? (Y/N): y
[ OK ] File berhasil dihapus.
vier@UBUNTU:~/praktikum-os/week09/scripts$
```
## Praktikum 7.5 Script Backup dengan Opsi

### 1. Buat script
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/backup-data.sh
```
### 2. Ketik isi berikut
```bash
#!/bin/bash
# Penggunaan: ./backup-data.sh [-v] [-c] [-l logfile] <sumber> <tujuan>

VERBOSE=false
COMPRESS=false
LOG_FILE=""

while getopts "vcl:" OPSI; do
case $OPSI in
v) VERBOSE=true ;;
c) COMPRESS=true ;;
l) LOG_FILE="$OPTARG" ;;
*) echo "Penggunaan: $0 [-v] [-c] [-l logfile] <sumber> <tujuan>"
exit 1 ;;
esac
done

shift $((OPTIND - 1))

SUMBER=$1
TUJUAN=$2

log() {
local MSG="[$(date '+%T')] $1"
echo "$MSG"
[ -n "$LOG_FILE" ] && echo "$MSG" >> "$LOG_FILE"
}

[ -z "$SUMBER" ] || [ -z "$TUJUAN" ] && {
echo "ERROR: sumber dan tujuan wajib diisi"; exit 1; }

[ ! -d "$SUMBER" ] && { log "ERROR: $SUMBER tidak ada"; exit 2; }

mkdir -p "$TUJUAN"

TANGGAL=$(date '+%F-%H%M%S')

[ "$VERBOSE" = true ] && log "Sumber: $SUMBER | Tujuan: $TUJUAN"

if [ "$COMPRESS" = true ]; then
ARSIP="$TUJUAN/backup-$(basename "$SUMBER")-$TANGGAL.tar.gz"
tar -czf "$ARSIP" -C "$(dirname "$SUMBER")" "$(basename "$SUMBER")"
log "Arsip: $ARSIP ($(du -sh "$ARSIP" | cut -f1))"
else
cp -r "$SUMBER" "$TUJUAN/backup-$(basename "$SUMBER")-$TANGGAL"
log "Backup selesai."
fi
```
### 3. Beri izin dan uji
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ chmod +x ~/praktikum-os/week09/scripts/backup-data.sh

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./backup-data.sh ~/praktikum-os/week09/data ~/praktikum-os/week09/logs
[16:43:42] Backup selesai.

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./backup-data.sh -v -c -l ../logs/backup.log ~/praktikum-os/week09/data ~/praktikum-os/week09/logs
[16:59:00] Sumber: /home/vier/praktikum-os/week09/data | Tujuan: /home/vier/praktikum-os/week09/logs
[16:59:00] Arsip: /home/vier/praktikum-os/week09/logs/backup-data-2026-05-05-165900.tar.gz (4.0K)

vier@UBUNTU:~/praktikum-os/week09/scripts$ cat ../logs/backup.log
[16:59:00] Sumber: /home/vier/praktikum-os/week09/data | Tujuan: /home/vier/praktikum-os/week09/logs
[16:59:00] Arsip: /home/vier/praktikum-os/week09/logs/backup-data-2026-05-05-165900.tar.gz (4.0K)
vier@UBUNTU:~/praktikum-os/week09/scripts$
```
## Praktikum 7.6 Debugging Script

### 1. Buat script untuk dianalisis
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/debug-latihan.sh
```
### 2. Ketik isi berikut
```bash
#!/bin/bash
# Script: debug-latihan.sh
# Penggunaan: ./debug-latihan.sh <direktori> <batas-MB>

DIREKTORI=$1
BATAS=$2

if [ $# -ne 2 ]; then
    echo "Penggunaan: $0 <direktori> <batas-MB>"
    exit 1
fi

UKURAN=$(du -sm "$DIREKTORI" | cut -f1)

echo "Direktori: $DIREKTORI"
echo "Ukuran: ${UKURAN} MB"
echo "Batas: ${BATAS} MB"

if [ "$UKURAN" -gt "$BATAS" ]; then
    echo "PERINGATAN: Ukuran melebihi batas!"
    echo "Kelebihan: $((UKURAN - BATAS)) MB"
else
    echo "Status: Normal (sisa: $((BATAS - UKURAN)) MB)"
fi
```
### 3. Cek sintaks, lalu jalankan dengan tracing
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ chmod +x ~/praktikum-os/week09/scripts/debug-latihan.sh

vier@UBUNTU:~/praktikum-os/week09/scripts$ bash -n debug-latihan.sh && echo "Sintaks OK"
Sintaks OK

vier@UBUNTU:~/praktikum-os/week09/scripts$ bash -x debug-latihan.sh /etc 10
+ DIREKTORI=/etc
+ BATAS=10
+ '[' 2 -ne 2 ']'
++ du -sm /etc
++ cut -f1
du: cannot read directory '/etc/credstore': Permission denied
du: cannot read directory '/etc/ppp/peers': Permission denied
du: cannot read directory '/etc/sssd': Permission denied
du: cannot read directory '/etc/chatscripts': Permission denied
du: cannot read directory '/etc/ssl/private': Permission denied
du: cannot read directory '/etc/polkit-1/rules.d': Permission denied
du: cannot read directory '/etc/credstore.encrypted': Permission denied
du: cannot read directory '/etc/cups/ssl': Permission denied
+ UKURAN=12
+ echo 'Direktori: /etc'
Direktori: /etc
+ echo 'Ukuran: 12 MB'
Ukuran: 12 MB
+ echo 'Batas: 10 MB'
Batas: 10 MB
+ '[' 12 -gt 10 ']'
+ echo 'PERINGATAN: Ukuran melebihi batas!'
PERINGATAN: Ukuran melebihi batas!
+ echo 'Kelebihan: 2 MB'
Kelebihan: 2 MB

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./debug-latihan.sh /vat 50
du: cannot access '/vat': No such file or directory
Direktori: /vat
Ukuran:  MB
Batas: 50 MB
./debug-latihan.sh: line 19: [: : integer expression expected
Status: Normal (sisa: 50 MB)

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./debug-latihan.sh
Penggunaan: ./debug-latihan.sh <direktori> <batas-MB>
```
## Latihan 9.5

### Script debug-latihan.sh tidak menangani direktori yang tidak ada. Perbaiki dengan menambahkan
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/debug-latihan.sh

#!/bin/bash
set -e
# Script: debug-latihan.sh
# Penggunaan: ./debug-latihan.sh <direktori> <batas-MB>

DIREKTORI=$1
BATAS=$2

# Validasi jumlah argumen
if [ $# -ne 2 ]; then
    echo "Penggunaan: $0 <direktori> <batas-MB>"
    exit 1
fi

# Cek apakah direktori ada
if [ ! -d "$DIREKTORI" ]; then
    echo "ERROR: Direktori '$DIREKTORI' tidak ditemukan."
    exit 1
fi

# Ambil ukuran direktori
UKURAN=$(du -sm "$DIREKTORI" | cut -f1)

echo "Direktori: $DIREKTORI"
echo "Ukuran: ${UKURAN} MB"
echo "Batas: ${BATAS} MB"

# Bandingkan ukuran
if [ "$UKURAN" -gt "$BATAS" ]; then
    echo "PERINGATAN: Ukuran melebihi batas!"
    echo "Kelebihan: $((UKURAN - BATAS)) MB"
else
    echo "Status: Normal (sisa: $((BATAS - UKURAN)) MB)"
fi

vier@UBUNTU:~/praktikum-os/week09/scripts$ chmod +x ~/praktikum-os/week09/scripts/debug-latihan.sh

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./debug-latihan.sh /folder-tidak-ada 10
ERROR: Direktori '/folder-tidak-ada' tidak ditemukan.

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./debug-latihan.sh ~/praktikum-os 100
Direktori: /home/vier/praktikum-os
Ukuran: 1 MB
Batas: 100 MB
Status: Normal (sisa: 99 MB)
vier@UBUNTU:~/praktikum-os/week09/scripts$ 
```
## Tugas Praktikum

### Tugas 1 Script Absensi Kelas

#### Konteks: instruktur mencatat kehadiran mahasiswa dari command line
Instruksi:

1. Buat script absensi.sh yang:
- Menerima argumen nama mahasiswa dan status (hadir/izin/alpha)
- Menyimpan entri ke absensi-YYYY-MM-DD.txt dengan format [HH:MM] NAMA - STATUS
- Opsi -r: tampilkan rekapitulasi (jumlah per status)
- Opsi -h: tampilkan bantuan
2. Rekam minimal 5 entri dan tampilkan rekapitulasinya. Konsep wajib: variabel, parameter posisional, getopts, if, for, fungsi, dan redirection ke file.
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/absensi.sh

#!/usr/bin/env bash
# Script: absensi.sh
# Versi: Javier

FILE="$HOME/praktikum-os/week09/logs/absensi-$(date +%F).txt"
mkdir -p "$(dirname "$FILE")"

# ===== Fungsi Bantuan =====
bantuan() {
    echo "Penggunaan:"
    echo "  $0 NAMA STATUS"
    echo "  $0 -r   (lihat rekap)"
    echo "  $0 -h   (bantuan)"
    echo ""
    echo "STATUS: hadir | izin | alpha"
    exit 0
}

# ===== Fungsi Rekap =====
rekap() {
    echo "=== REKAP ABSENSI ==="
    for S in hadir izin alpha; do
        JUMLAH=$(grep -ic "\- $S" "$FILE" 2>/dev/null || echo 0)
        echo "$S : $JUMLAH"
    done
    exit 0
}

# ===== Parsing Opsi =====
while getopts "hr" OPSI; do
    case $OPSI in
        h) bantuan ;;
        r) rekap ;;
        *) exit 1 ;;
    esac
done
shift $((OPTIND - 1))

# ===== Validasi Input =====
if [ $# -lt 2 ]; then
    bantuan
fi

NAMA="$1"
STATUS="${2,,}"   # ubah ke lowercase

# validasi status
if [[ ! "$STATUS" =~ ^(hadir|izin|alpha)$ ]]; then
    echo "Error: Status harus hadir/izin/alpha"
    exit 1
fi

# ===== Simpan Data =====
echo "[$(date +%H:%M)] $NAMA - $STATUS" >> "$FILE"
echo "Tercatat: $NAMA - $STATUS"

vier@UBUNTU:~/praktikum-os/week09/scripts$ chmod +x ~/praktikum-os/week09/scripts/absensi.sh

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./absensi.sh "Javier" hadir
./absensi.sh "Ibni" izin
./absensi.sh "Lindhu" alpha
./absensi.sh "Yedid" hadir
./absensi.sh "Adjie" izin
Tercatat: Javier - hadir
Tercatat: Ibni - izin
Tercatat: Lindhu - alpha
Tercatat: Yedid - hadir
Tercatat: Adjie - izin

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./absensi.sh -r
=== REKAP ABSENSI ===
hadir : 2
izin : 2
alpha : 1

vier@UBUNTU:~/praktikum-os/week09/scripts$ cat ~/praktikum-os/week09/logs/absensi-$(date +%F).txt
[17:35] Javier - hadir
[17:35] Ibni - izin
[17:35] Lindhu - alpha
[17:35] Yedid - hadir
[17:35] Adjie - izin
vier@UBUNTU:~/praktikum-os/week09/scripts$ 
```
### Tugas 2 Script Health Check Sistem

#### Konteks: administrator membuat pemeriksaan kondisi server sebelum maintenance
Instruksi

1. Buat script healthcheck.sh menggunakan template profesional dari bagian Best Practices.
2. Script menampilkan: tanggal/waktu, hostname, uptime, penggunaan CPU, memori, dan disk untuk setiap filesystem yang terpasang.
3. Jika penggunaan disk mana pun melebihi 80%, tampilkan peringatan.
4. Simpan hasil ke healthcheck-YYYY-MM-DD.log dan tampilkan ke terminal sekaligus menggunakan tee.
5. Opsi -t mengubah batas peringatan disk (default 80). Konsep wajib: set -euo pipefail, trap, getopts, fungsi dengan local, for, if, dan tee.
```bash
vier@UBUNTU:~/praktikum-os/week09/scripts$ nano ~/praktikum-os/week09/scripts/healthcheck.sh

#!/usr/bin/env bash

set -euo pipefail

# ===== Default =====
BATAS=80
LOG="$HOME/praktikum-os/week09/logs/healthcheck-$(date +%F).log"
mkdir -p "$(dirname "$LOG")"

# ===== Trap =====
trap 'echo "[INFO] Selesai."' EXIT

# ===== Bantuan =====
bantuan() {
    echo "Penggunaan:"
    echo "  $0 [-t batas_persen]"
    echo ""
    echo "Contoh:"
    echo "  $0"
    echo "  $0 -t 70"
    exit 0
}

# ===== Parsing opsi =====
while getopts "t:h" opt; do
    case "$opt" in
        t) BATAS="$OPTARG" ;;
        h) bantuan ;;
        *) exit 1 ;;
    esac
done

# ===== Fungsi utama =====
cek_sistem() {
    local WAKTU
    local HOST
    local UPTIME
    local CPU
    local RAM

    WAKTU=$(date '+%F %T')
    HOST=$(hostname)
    UPTIME=$(uptime -p)

    # CPU usage sederhana
    CPU=$(top -bn1 | awk '/Cpu\(s\)/ {print $2+$4}')

    # RAM tersedia
    RAM=$(free -h | awk '/^Mem/ {print $7}')

    echo "=== HEALTH CHECK SYSTEM ==="
    echo "Waktu    : $WAKTU"
    echo "Hostname : $HOST"
    echo "Uptime   : $UPTIME"
    echo "CPU      : $CPU%"
    echo "Available RAM : $RAM"
    echo "---------------------------"
    echo "Disk Usage:"

    # Loop semua filesystem
    df -h | awk 'NR>1 {print $5","$6}' | while IFS=, read -r PERSEN MOUNT; do
        local NILAI=${PERSEN%\%}

        if [ "$NILAI" -ge "$BATAS" ]; then
            echo "[PERINGATAN] $MOUNT terpakai $NILAI% (Batas: $BATAS%)"
        else
            echo "[OK] $MOUNT terpakai $NILAI%"
        fi
    done
}

# ===== Jalankan + simpan log =====
cek_sistem | tee -a "$LOG"

vier@UBUNTU:~/praktikum-os/week09/scripts$ chmod +x ~/praktikum-os/week09/scripts/healthcheck.sh

vier@UBUNTU:~/praktikum-os/week09/scripts$ ./healthcheck.sh
=== HEALTH CHECK SYSTEM ===
Waktu    : 2026-05-05 17:46:29
Hostname : UBUNTU
Uptime   : up 2 hours, 24 minutes
CPU      : 0%
Available RAM : 1.2Gi
---------------------------
Disk Usage:
[OK] /run terpakai 1%
[OK] / terpakai 33%
[OK] /dev/shm terpakai 0%
[OK] /run/lock terpakai 1%
[OK] /run/user/1000 terpakai 1%
[INFO] Selesai.

vier@UBUNTU:~/praktikum-os/week09/scripts$ cat ~/praktikum-os/week09/logs/healthcheck-$(date +%F).log
=== HEALTH CHECK SYSTEM ===
Waktu    : 2026-05-05 17:46:29
Hostname : UBUNTU
Uptime   : up 2 hours, 24 minutes
CPU      : 0%
Available RAM : 1.2Gi
---------------------------
Disk Usage:
[OK] /run terpakai 1%
[OK] / terpakai 33%
[OK] /dev/shm terpakai 0%
[OK] /run/lock terpakai 1%
[OK] /run/user/1000 terpakai 1%
vier@UBUNTU:~/praktikum-os/week09/scripts$ 
```

*Jobsheet 9 - Sistem Operasi*
