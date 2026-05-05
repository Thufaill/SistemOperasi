<h1 align="center">JOBSHEET 7 - SISTEM OPERASI</h1>


**Nama**       : M. Javier Thufail  
**NIM**        : 254107020019  
**Kelas**      : TI 1-G  
**No. Absen**  : 18  

---
<h1 align="center">BASH SHELL dan SHELL BASIC</h2>

### Praktikum 6.1 — Mengenali Bash dan Menyiapkan Workspace
#### 1. Lihat shell login dan shell aktif saat ini
Perintah:
```bash
echo " Shell login : $SHELL "
echo " Shell aktif : $0"
bash --version | head -n 1
```
Output:
```bash
vier@UBUNTU:~/praktikum-os/week07$ echo " Shell login : $SHELL "
 Shell login : /bin/bash 
vier@UBUNTU:~/praktikum-os/week07$ echo " Shell aktif : $0"
 Shell aktif : bash
vier@UBUNTU:~/praktikum-os/week07$ bash --version | head -n 1
GNU bash, version 5.2.21(1)-release (x86_64-pc-linux-gnu)
```
#### 2. Lihat proses shell yang sedang berjalan
Perintah:
```bash
echo $$
ps -p $$ -o pid,ppid,args=
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07$ echo $$
2815

vier@UBUNTU:~/praktikum-os/week07$ ps -p $$ -o pid,ppid,args=
    PID    PPID 
   2815    2791 bash
```
#### 3. Buat workspace praktikum 
Perintah:
```bash
mkdir -p ~/praktikum-os/week07-bash/{bin,backup,logs,sampel,ruang-nama}
cd ~/praktikum-os/week07-bash
pwd
```
Outputnya
```bash
vier@UBUNTU:~$ mkdir -p ~/praktikum-os/week07-bash/{bin,backup,logs,sampel,ruang-nama}

vier@UBUNTU:~$ cd ~/praktikum-os/week07-bash

vier@UBUNTU:~/praktikum-os/week07-bash$ pwd
/home/vier/praktikum-os/week07-bash 
```
#### 4. Buat beberapa file contoh yang akan dipakai pada praktikum berikutnya:
Perintah:
```bash
touch sample-app.conf
touch logs/app-01.log logs/app-02.log logs/app-03.log
touch sampel/catatan-a.txt sampel/catatan-b.txt
touch sampel/backup-01.tar sampel/backup-02.tar
touch sampel/laporan-harian.log sampel/laporan-mingguan.log sampel/laporan-bulanan. log
touch "ruang-nama/laporan server april.txt"
touch "ruang-nama/backup [mingguan] server.conf"
ls -R
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash$ touch sample-app.conf

vier@UBUNTU:~/praktikum-os/week07-bash$ touch logs/app-01.log logs/app-02.log logs/app-03.log

vier@UBUNTU:~/praktikum-os/week07-bash$ touch sampel/catatan-a.txt sampel/catatan-b.txt

vier@UBUNTU:~/praktikum-os/week07-bash$ touch sampel/backup-01.tar sampel/backup-02.tar

vier@UBUNTU:~/praktikum-os/week07-bash$ touch sampel/laporan-harian.log sampel/laporan-mingguan.log sampel/laporan-bulanan. log

vier@UBUNTU:~/praktikum-os/week07-bash$ touch "ruang-nama/laporan server april.txt"

vier@UBUNTU:~/praktikum-os/week07-bash$ touch "ruang-nama/backup [mingguan] server.conf"

vier@UBUNTU:~/praktikum-os/week07-bash$ ls -R
.:
backup  bin  log  logs  ruang-nama  sampel  sample-app.conf

./backup:

./bin:

./logs:
app-01.log  app-02.log  app-03.log

./ruang-nama:
'backup [mingguan] server.conf'  'laporan server april.txt'

./sampel:
backup-01.tar  backup-02.tar  catatan-a.txt  catatan-b.txt  laporan-bulanan.  laporan-harian.log  laporan-mingguan.log
```
---

### Praktikum 6.2 — Membuat Ringkasan Sesi Terminal
#### 1. Masuk ke workspace praktikum:
Perintah:
```bash
cd ~/praktikum-os/week07-bash
```
Outputnya
```bash
cd ~/praktikum-os/week07-bash
vier@UBUNTU:~/praktikum-os/week07-bash$
```
#### 2. Simpan informasi sesi terminal ke file laporan:
Perintah:
```bash
{
echo "=== RINGKASAN SESI BASH ==="
date
echo "User : $(whoami)"
echo "Hostname : $(hostname)"
echo "Shell login : $SHELL"
echo "Shell aktif : $0"
echo "PID shell : $$"
echo "Direktori : $(pwd)"
} | tee session-info.txt
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash$ {
> echo "=== RINGKASAN SESI BASH ==="
date
echo "User : $(whoami)"
echo "Hostname : $(hostname)"
echo "Shell login : $SHELL"
echo "Shell aktif : $0"
echo "PID shell : $$"
echo "Direktori : $(pwd)"
} | tee session-info.txt
=== RINGKASAN SESI BASH ===
Sun Apr 12 06:04:35 AM UTC 2026
User : vier
Hostname : UBUNTU
Shell login : /bin/bash
Shell aktif : bash
PID shell : 2815
Direktori : /home/vier/praktikum-os/week07-bash
```
#### 3. Verifikasi isi file laporan:
Perintah:
```bash
cat session-info.txt

```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash$ cat session-info.txt
=== RINGKASAN SESI BASH ===
Sun Apr 12 06:04:35 AM UTC 2026
User : vier
Hostname : UBUNTU
Shell login : /bin/bash
Shell aktif : bash
PID shell : 2815
Direktori : /home/vier/praktikum-os/week07-bash
```
---

### Praktikum 6.3 — Menambahkan Konfigurasi Aman pada .bashrc
#### 1. Lihat file konfigurasi Bash pada home directory:
Perintah:
```bash
ls -la ~ | grep -E 'bashrc|bash_profile|profile'
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash$ ls -la ~ | grep -E 'bashrc|bash_profile|profile'
-rw-r--r--  1 vier vier 3771 Mar 31  2024 .bashrc
-rw-r--r--  1 vier vier  807 Mar 31  2024 .profile
```
#### 2. Lihat file konfigurasi Bash pada home directory:
Perintah:
```bash
cp ~/.bashrc ~/.bashrc.bak-praktikum
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash$ cp ~/.bashrc ~/.bashrc.bak-praktikum
```
#### 3. Tambahkan blok konfigurasi praktikum:
Perintah:
```bash
cat <<'EOF' >> ~/.bashrc
# --- Praktikum Bash Shell ---
export PRAKTIKUM_BASH_DIR="$HOME/praktikum-os/week04-bash"
export EDITOR = nano
# --- End Praktikum Bash Shell ---
EOF
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash$ cat <<'EOF' >> ~/.bashrc
> # --- Praktikum Bash Shell ---
> export PRAKTIKUM_BASH_DIR="$home/vier/praktikum-os/week07-bash"
> export EDITOR=nano
> # --- End Praktikum Bash Shell ---
> EOF
```
#### 4. Terapkan konfigurasi tanpa logout:
Perintah:
```bash
source ~/.bashrc
echo "$PRAKTIKUM_BASH_DIR"
echo "$EDITOR"
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash$ source ~/.bashrc
bash: export: `=': not a valid identifier
bash: export: `=': not a valid identifier

vier@UBUNTU:~/praktikum-os/week07-bash$ echo "$PRAKTIKUM_BASH_DIR"
/vier/praktikum-os/week07-bash

vier@UBUNTU:~/praktikum-os/week07-bash$ echo "$EDITOR"
nano
```
---

### Praktikum 6.4 — Menyiapkan .bash_profile untuk Shell Login
#### 1. Backup .bash_profile jika sudah ada:
Perintah:
```bash
[ -f ~/.bash_profile ] && cp ~/.bash_profile ~/.bach_profile.bak-praktikum
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash$ [ -f ~/.bash_profile ] && cp ~/.bash_profile ~/.bach_profile.bak-praktikum
```
#### 2. Tambahkan konfigurasi login shell:
Perintah:
```bash
cat <<'EOF' >> ~/.bash_profile
# --- Praktikum Bash Login Shell ---
if [ -f ~/.bashrc ]; then
. ~/.bashrc
fi
echo "Login Bash pada $(date '+%F %T' )" >> "$HOME/praktikum-os/week07-bash/login-audit.log"
# --- End Praktikum Bash Login Shell ---
EOF
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash$ cat <<'EOF' >> ~/.bash_profile
> # --- Praktikum Bash Login Shell ---
> if [ -f ~/.bashrc ]; then
> . ~/.bashrc
> fi
> echo "Login Bash pada $(date '+%F %T' )" >> "$HOME/praktikum-os/week07-bash/login-audit.log"
> # --- End Praktikum Bash Login Shell ---
> EOF
```
#### 3. Uji dengan membuka login shell baru:
Perintah:
```bash
bash -l
tail -n 3 ~/praktikum-os/week07-bash/login-audit.log
exit
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash$ bash -l
bash: export: `=': not a valid identifier
bash: export: `=': not a valid identifier

vier@UBUNTU:~/praktikum-os/week07-bash$ tail -n 3 ~/praktikum-os/week07-bash/login-audit.log
Login Bash pada 2026-04-12 06:45:25

vier@UBUNTU:~/praktikum-os/week07-bash$ exit
logout
```
---

### Praktikum 6.5 — Membedakan Variabel Shell dan Environment Variable
#### 1. Buat variabel lokal:
Perintah:
```bash
KELAS_OS="Sistem Operasi A"
echo "$KELAS_OS"
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash$ KELAS_OS="Sistem Operasi A"

vier@UBUNTU:~/praktikum-os/week07-bash$ echo "$KELAS_OS"
Sistem Operasi A
```
#### 2. Buka subshell dan cek apakah variabel masih ada:
Perintah:
```bash
bash
echo "$KELAS_OS"
exit
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash$ bash
bash: export: `=': not a valid identifier
bash: export: `=': not a valid identifier

vier@UBUNTU:~/praktikum-os/week07-bash$ echo "KELAS_OS"
KELAS_OS

vier@UBUNTU:~/praktikum-os/week07-bash$ exit
exit
```
#### 3. Sekarang ubah menjadi environment variable:
Perintah:
```bash
export KELAS_OS="Sistem Operasi A"
bash
echo "$KELAS_OS"
exit
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash$ export KELAS_OS="Sistem Operasi A"
vier@UBUNTU:~/praktikum-os/week07-bash$ bash

bash: export: `=': not a valid identifier
bash: export: `=': not a valid identifier

vier@UBUNTU:~/praktikum-os/week07-bash$ echo "KELAS_OS"
KELAS_OS

vier@UBUNTU:~/praktikum-os/week07-bash$ exit
exit
```
#### 4. Lihat isi PATH dan lokasi beberapa perintah:
Perintah:
```bash
echo "$PATH"
which bash
type ls
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash$ echo "$PATH"
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin

vier@UBUNTU:~/praktikum-os/week07-bash$ which bash
/usr/bin/bash

vier@UBUNTU:~/praktikum-os/week07-bash$ type ls
ls is aliased to `ls --color=auto'
```
---

### Praktikum 6.6 — Menambahkan Direktori Script Pribadi ke PATH
#### 1. Pastikan direktori bin praktikum tersedia:
Perintah:
```bash
mkdir -p ~/praktikum-os/week07-bash/bin
```
Outputnya
```bash
vier@UBUNTU:~$ mkdir -p ~/praktikum-os/week07-bash/bin
```
#### 2. Tambahkan direktori tersebut ke PATH melalui .bashrc:
Perintah:
```bash
cat <<'EOF ' >> ~/. bashrc
# --- Praktikum PATH ---
export PATH =" $HOME / praktikum -os/week07 - bash /bin : $PATH "
# --- End Praktikum PATH ---
EOF
source ~/. bashrc
echo " $PATH "
```
Outputnya
```bash
vier@UBUNTU:~$ cat <<'EOF' >> ~/.bashrc
>                       
> # --- Praktikum PATH ---
> export PATH="$HOME/praktikum-os/week07-bash/bin:$PATH"
> # --- End Praktikum PATH ---
> 
> EOF

vier@UBUNTU:~$ source ~/.bashrc

vier@UBUNTU:~$ echo "$PATH"
/home/vier/praktikum-os/week07-bash/bin:/home/vier/praktikum-os/week07-bash/bin:/home/vier/praktikum-os/week07-bash/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin
```
#### 3. Buat script ringkasan sistem:
Perintah:
```bash
cat <<'EOF ' > ~/ praktikum - os / week07 - bash / bin / ringkas -
sistem
#!/ usr/bin/env bash
echo " Hostname : $( hostname )"
echo " User : $( whoami )"
echo " Uptime : $( uptime -p)"
echo " Disk / :"
df -h /
EOF
chmod + x ~/ praktikum - os / week07 - bash / bin / ringkas - sistem
```
Outputnya
```bash
vier@UBUNTU:~$ cat <<'EOF' > ~/praktikum-os/week07-bash/bin/ringkas-sistem
> #!/usr/bin/env bash
> echo "Hostname  : $(hostname)"
> echo "User      : $(whoami)"
> echo "Uptime    : $(uptime -p)"
> echo "Disk /    :"
> df -h /
> EOF

vier@UBUNTU:~$ chmod +x ~/praktikum-os/week07-bash/bin/ringkas-sistem
```
#### 4. Jalankan script dari direktori yang berbeda:
Perintah:
```bash
cd ~
ringkas - sistem
```
Outputnya
```bash
vier@UBUNTU:~$ cd ~

vier@UBUNTU:~$ ringkas-sistem
Hostname  : UBUNTU
User      : vier
Uptime    : up 47 minutes
Disk /    :
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        30G  8.9G   20G  32% /
```
---

### Praktikum 6.7 — Membuat Alias Produktivitas Dasar
#### 1. Tambahkan alias ke .bashrc:
Perintah:
```bash
cat <<'EOF ' >> ~/. bashrc
# --- Praktikum Alias ---
alias ll ='ls -lah --color = auto '
alias hist10 ='history | tail -n 10 '
alias cdbashlab ='cd $HOME / praktikum -os/week04 - bash '
# --- End Praktikum Alias ---
EOF
source ~/. bashrc
```
Outputnya
```bash
vier@UBUNTU:~$ cat <<'EOF' >> ~/.bashrc
> 
> # --- Praktikum Alias ---
> alias ll='ls -lah --color=auto'
> alias hist10='history | tail -n 10'
> alias cdbashlab='cd $HOME/praktikum-os/week07-bash'
> # --- End Praktikum Alias ---
> 
> EOF

vier@UBUNTU:~$ source ~/.bashrc
```
#### 2. Uji alias:
Perintah:
```bash
ll
hist10
cdbashlab
pwd
type ll
```
Outputnya
```bash
vier@UBUNTU:~$ ll
total 108K
drwxr-x--- 17 vier vier 4.0K Apr 12 06:44 .
drwxr-xr-x  3 root root 4.0K Feb 15 15:34 ..
-rw-------  1 vier vier 8.0K Apr 12 07:03 .bash_history
-rw-r--r--  1 vier vier  220 Mar 31  2024 .bash_logout
-rw-rw-r--  1 vier vier  212 Apr 12 06:44 .bash_profile
-rw-r--r--  1 vier vier 5.0K May  2 17:48 .bashrc
-rw-r--r--  1 vier vier 4.4K Apr 12 06:29 .bashrc.bak-praktikum
drwx------ 10 vier vier 4.0K Feb 24 10:26 .cache
drwx------ 18 vier vier 4.0K Apr 11 18:19 .config
drwxr-xr-x  2 vier vier 4.0K Feb 15 15:34 Desktop
drwxr-xr-x  2 vier vier 4.0K Feb 15 15:34 Documents
drwxr-xr-x  2 vier vier 4.0K Feb 15 15:34 Downloads
drwx------  2 vier vier 4.0K May  2 16:58 .gnupg
-rw-------  1 vier vier   20 Feb 25 09:51 .lesshst
drwx------  4 vier vier 4.0K Feb 15 15:34 .local
drwxr-xr-x  2 vier vier 4.0K Feb 15 15:34 Music
drwxr-xr-x  2 vier vier 4.0K Feb 15 15:34 Pictures
drwxrwxr-x  8 vier vier 4.0K Apr 12 05:50 praktikum-os
-rw-r--r--  1 vier vier  807 Mar 31  2024 .profile
drwxr-xr-x  2 vier vier 4.0K Feb 15 15:34 Public
drwx------  5 vier vier 4.0K Feb 25 04:18 snap
drwx------  2 vier vier 4.0K Feb 15 15:34 .ssh
-rw-r--r--  1 vier vier    0 Feb 24 10:54 .sudo_as_admin_successful
drwxr-xr-x  2 vier vier 4.0K Feb 15 15:34 Templates
drwxr-xr-x  2 vier vier 4.0K Feb 15 15:34 Videos

vier@UBUNTU:~$ hist10
alias ll='ls -lah --color=auto'
alias hist10='history | tail -n 10'
alias cdbashlab='cd $HOME/praktikum-os/week07-bash'
# --- End Praktikum Alias ---

EOF

  305  source ~/.bashrc
  306  ll
  307  hist10

vier@UBUNTU:~$ cdbashlab

vier@UBUNTU:~/praktikum-os/week07-bash$ pwd
/home/vier/praktikum-os/week07-bash

vier@UBUNTU:~/praktikum-os/week07-bash$ type ll
ll is aliased to `ls -lah --color=auto'
```
---

### Praktikum 6.8 — Membuat Fungsi Backup Konfigurasi
#### 1. Siapkan file konfigurasi contoh:
Perintah:
```bash
echo " PORT =8080 " > ~/ praktikum - os / week07 - bash / sample -
app . conf
cat ~/ praktikum - os / week07 - bash / sample - app . conf
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash$ echo "PORT=8080" > ~/praktikum-os/week07-bash/sample-app.conf

vier@UBUNTU:~/praktikum-os/week07-bash$ cat ~/praktikum-os/week07-bash/sample-app.conf
PORT=8080
```
#### 2. Tambahkan fungsi ke .bashrc:
Perintah:
```bash
cat <<'EOF ' >> ~/. bashrc
# --- Praktikum Fungsi Shell ---
backup_conf () {
if [ $# -ne 1 ]; then
echo " Usage : backup_conf <file >"
return 1
fi
local src ="$1"
local dst =" $HOME / praktikum -os/week07 - bash / backup "
if [ ! -f " $src " ]; then
echo " File tidak ditemukan : $src "
return 2
fi
mkdir -p " $dst "
cp -- " $src " " $dst /$( basename " $src ").$( date +%F -%H%
M%S).bak"
echo " Backup selesai di $dst "
}
# --- End Praktikum Fungsi Shell ---
EOF
source ~/. bashrc
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash$ cat <<'EOF' >> ~/.bashrc
> 
> # --- Praktikum Fungsi Shell ---
> backup_conf () {
> if [ $# -ne 1 ]; then
> echo " Usage : backup_conf <file>"
> return 1
> fi
> local src="$1"
> local dst="$HOME/praktikum-os/week07-bash/backup"
> if [ ! -f "$src" ]; then
> echo "File tidak ditemukan: $src"
> return 2
> fi
> mkdir -p "$dst"
> cp -- "$src" "$dst/$(basename "$src").$(date +%F-%H%M%S).bak"
> echo "Backup selesai di $dst"
> }
> # --- End Praktikum Fungsi Shell ---
> EOF

vier@UBUNTU:~/praktikum-os/week07-bash$ source ~/.bashrc
```
#### 3. Uji fungsi:
Perintah:
```bash
backup_conf ~/ praktikum - os / week07 - bash / sample - app . conf
ls - lah ~/ praktikum - os / week07 - bash / backup
type backup_conf
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash$ backup_conf ~/praktikum-os/week07-bash/sample-app.conf
Backup selesai di /home/vier/praktikum-os/week07-bash/backup

vier@UBUNTU:~/praktikum-os/week07-bash$ ls -lah ~/praktikum-os/week07-bash/backup
total 12K
drwxrwxr-x 2 vier vier 4.0K May  2 17:57 .
drwxrwxr-x 7 vier vier 4.0K Apr 12 06:45 ..
-rw-rw-r-- 1 vier vier   10 May  2 17:57 sample-app.conf.2026-05-02-175705.bak

vier@UBUNTU:~/praktikum-os/week07-bash$ type backup_conf
backup_conf is a function
backup_conf () 
{ 
    if [ $# -ne 1 ]; then
        echo " Usage : backup_conf <file>";
        return 1;
    fi;
    local src="$1";
    local dst="$HOME/praktikum-os/week07-bash/backup";
    if [ ! -f "$src" ]; then
        echo "File tidak ditemukan: $src";
        return 2;
    fi;
    mkdir -p "$dst";
    cp -- "$src" "$dst/$(basename "$src").$(date +%F-%H%M%S).bak";
    echo "Backup selesai di $dst"
}
```
---

### Praktikum 6.9 — Menggunakan Completion Dasar dan Melihat History
#### 1. Pastikan file contoh tersedia:
Perintah:
```bash
cd ~/ praktikum - os / week07 - bash / sampel
touch laporan - harian . log laporan - mingguan . log laporan -
bulanan . log
ls
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash$ cd ~/praktikum-os/week07-bash/sampel

vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ touch laporan-harian.log laporan-mingguan.log laporan-bulanan.log

vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ ls
backup-01.tar  catatan-a.txt  laporan-bulanan.     laporan-harian.log
backup-02.tar  catatan-b.txt  laporan-bulanan.log  laporan-mingguan.log
```
#### 2. Uji completion file:
Perintah:
```bash
a) Ketik cat lap lalu tekan Tab dua kali.
b) Amati daftar file yang memiliki prefix lap.
c) Ketik lebih spesifik, misalnya cat laporan-h lalu tekan Tab.
```
Outputnya
```bash
```
#### 3. Jalankan beberapa perintah sederhana:
Perintah:
```bash
pwd
ls - lah
date
whoami
history | tail -n 10
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ pwd
/home/vier/praktikum-os/week07-bash/sampel

vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ ls -lah
total 8.0K
drwxrwxr-x 2 vier vier 4.0K May  2 18:02 .
drwxrwxr-x 7 vier vier 4.0K Apr 12 06:45 ..
-rw-rw-r-- 1 vier vier    0 Apr 12 05:54 backup-01.tar
-rw-rw-r-- 1 vier vier    0 Apr 12 05:54 backup-02.tar
-rw-rw-r-- 1 vier vier    0 Apr 12 05:54 catatan-a.txt
-rw-rw-r-- 1 vier vier    0 Apr 12 05:54 catatan-b.txt
-rw-rw-r-- 1 vier vier    0 Apr 12 05:54 laporan-bulanan.
-rw-rw-r-- 1 vier vier    0 May  2 18:02 laporan-bulanan.log
-rw-rw-r-- 1 vier vier    0 May  2 18:02 laporan-harian.log
-rw-rw-r-- 1 vier vier    0 May  2 18:02 laporan-mingguan.log

vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ date
Sat May  2 06:03:04 PM UTC 2026

vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ whoami
vier

vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ history | tail -n 10 
  316  ls -lah ~/praktikum-os/week07-bash/backup
  317  type backup_conf
  318  cd ~/praktikum-os/week07-bash/sampel
  319  touch laporan-harian.log laporan-mingguan.log laporan-bulanan.log
  320  ls
  321  pwd
  322  ls -lah
  323  date
  324  whoami
  325  history | tail -n 10 
```
---

### Praktikum 6.10 — Menelusuri Perintah Diagnostik dengan History
#### 1. Jalankan beberapa perintah diagnostik:
Perintah:
```bash
df -h
free -h
uptime
ps aux | head
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ df -h
Filesystem      Size  Used Avail Use% Mounted on
tmpfs           392M  1.9M  390M   1% /run
/dev/sda2        30G  8.9G   20G  32% /
tmpfs           2.0G     0  2.0G   0% /dev/shm
tmpfs           5.0M  8.0K  5.0M   1% /run/lock
tmpfs           392M  132K  392M   1% /run/user/1000

vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ free -h 
               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       2.0Gi       109Mi        87Mi       1.8Gi       1.8Gi
Swap:             0B          0B          0B

vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ uptime
 18:06:15 up  1:08,  1 user,  load average: 1.11, 1.44, 1.22

vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ ps aux | head 
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.1  0.3  23324 14716 ?        Ss   16:57   0:06 /sbin/init splash
root           2  0.0  0.0      0     0 ?        S    16:57   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        S    16:57   0:00 [pool_workqueue_release]
root           4  0.0  0.0      0     0 ?        I<   16:57   0:00 [kworker/R-rcu_gp]
root           5  0.0  0.0      0     0 ?        I<   16:57   0:00 [kworker/R-sync_wq]
root           6  0.0  0.0      0     0 ?        I<   16:57   0:00 [kworker/R-kvfree_rcu_reclaim]
root           7  0.0  0.0      0     0 ?        I<   16:57   0:00 [kworker/R-slub_flushwq]
root           8  0.0  0.0      0     0 ?        I<   16:57   0:00 [kworker/R-netns]
root          10  0.0  0.0      0     0 ?        I    16:57   0:00 [kworker/0:1-events]
```
#### 2. Cari ulang perintah diagnostik dari history:
Perintah:
```bash
history | grep -E 'df -h| free -h| uptime |ps aux '
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ history | grep -E 'df -h | free -h | uptime | ps aux'
   57  df -h | awk 'NR==1 {print $1, $5, $6} NR>1 {print $1, $5, $6}'
   58  df -h | awk 'NR==1 || ($5+0) > 80 {print $1, $5, $6}'
   59  ps aux | head
   60  ps aux | grep -i sshd
  147  ps aux | grep sleep | grep -v grep
  149  ps aux | grep sleep | grep -v grep
  161  ps aux | grep sleep | grep -v grep
  164  df -h | tee laporan.text
  165  free -h | -a tee laporan.text
  166  free -h | tee -a laporan.text
  167  ps aux | grep -v grep | head -10
  193  ps aux
  195  ps aux -L
  201  ps aux | grep sleep
  203  ps aux | grep sleep
  209  ps aux | grep sleep
  237  ps aux | grep sleep
  260  ps aux | grep -v grep | grep sleep
  262  ps aux | grep -v grep | grep sleep
  263  ps aux | grep sleep
  265  ps aux | grep sleep
  267  ps aux | grep sleep
  271  ps aux | grep sleep
  273  ps aux | grep sleep
  275  ps aux | grep sleep
df -h /
  327  free -h 
  329  ps aux | head 
  330  history | grep -E 'df -h | free -h | uptime | ps aux'
```
#### 3. Jalankan ulang salah satu perintah berdasarkan nomor history:
Perintah:
```bash
! < NOMOR_HISTORY_ANDA >
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ !275
ps aux | grep sleep
vier        5333  0.0  0.0  17820  2372 pts/0    S+   18:09   0:00 grep --color=auto sleep
```
#### 4. Simpan potongan history ke file dokumentasi:
Perintah:
```bash
history | tail -n 20 > ~/ praktikum - os / week07 - bash / diag
- history . txt
cat ~/ praktikum - os / week07 - bash / diag - history . txt
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ history | tail -n 20 > ~/praktikum-os/week07-bash/diag-history.txt

vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ cat ~/praktikum-os/week07-bash/diag-history.txt

  314  source ~/.bashrc
  315  backup_conf ~/praktikum-os/week07-bash/sample-app.conf
  316  ls -lah ~/praktikum-os/week07-bash/backup
  317  type backup_conf
  318  cd ~/praktikum-os/week07-bash/sampel
  319  touch laporan-harian.log laporan-mingguan.log laporan-bulanan.log
  320  ls
  321  pwd
  322  ls -lah
  323  date
  324  whoami
  325  history | tail -n 10 
  326  df -h
  327  free -h 
  328  uptime
  329  ps aux | head 
  330  history | grep -E 'df -h | free -h | uptime | ps aux'
  331  ps aux | grep sleep
  332  history | tail -n 20 > ~/praktikum-os/week07-bash/diag-history.txt
```
--- 

### Praktikum 6.11 — Mencoba Wildcard Dasar
#### 1. Masuk ke direktori sampel:
Perintah:
```bash
cd ~/ praktikum - os / week07 - bash / sampel
ls
```
Outputnya
```bash
vier@UBUNTU:~$ cd ~/praktikum-os//week07-bash//sampel

vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ ls
backup-01.tar  catatan-a.txt  laporan-bulanan.     laporan-harian.log
backup-02.tar  catatan-b.txt  laporan-bulanan.log  laporan-mingguan.log
```
#### 2. Coba beberapa pola wildcard:
Perintah:
```bash
ls *. log
ls catatan -?. txt
ls backup -0[12]. tar
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ ls *.log
laporan-bulanan.log  laporan-harian.log  laporan-mingguan.log

vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ ls catatan-?.txt
catatan-a.txt  catatan-b.txt

vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ ls backup-0[12].tar
backup-01.tar  backup-02.tar
```
#### 3. Coba beberapa ekspansi lain:
Perintah:
```bash
echo log -{ pagi , siang , malam }. txt
echo ~
echo ~/ praktikum - os / week04 - bash
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ echo log-{pagi,siang,malam}.txt
log-pagi.txt log-siang.txt log-malam.txt

vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ echo ~
/home/vier

vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ echo ~/praktikum-os/week07-bash
/home/vier/praktikum-os/week07-bash
```
---

### Praktikum 6.12 — Mengarsipkan Banyak Log Sekaligus
#### 1. Siapkan file log tambahan:
Perintah:
```bash
cd ~/ praktikum - os / week07 - bash / logs
touch access -01. log access -02. log access -03. log
ls
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash/sampel$ cd ~/praktikum-os/week07-bash/logs

vier@UBUNTU:~/praktikum-os/week07-bash/logs$ touch acces-01.log acces-02.log acces-03.log

vier@UBUNTU:~/praktikum-os/week07-bash/logs$ ls
acces-01.log  acces-02.log  acces-03.log  app-01.log  app-02.log  app-03.log
```
#### 2. Preview file yang akan diproses:
Perintah:
```bash
echo *. log
echo access -0?. log
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash/logs$ echo *.log
acces-01.log acces-02.log acces-03.log app-01.log app-02.log app-03.log

vier@UBUNTU:~/praktikum-os/week07-bash/logs$ echo acces-0?.log
acces-01.log acces-02.log acces-03.log
```
#### 3. Pindahkan semua file log ke folder arsip:
Perintah:
```bash
mkdir -p arsip - log
mv *. log arsip - log /
ls arsip - log
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash/logs$ mkdir -p arsip-log

vier@UBUNTU:~/praktikum-os/week07-bash/logs$ mv *.log arsip-log/

vier@UBUNTU:~/praktikum-os/week07-bash/logs$ ls arsip-log
acces-01.log  acces-02.log  acces-03.log  app-01.log  app-02.log  app-03.log
```
#### 4. Kompres folder arsip:
Perintah:
```bash
tar - czf arsip - log - $ ( date +% F ) . tar . gz arsip - log
ls - la
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash/logs$ tar -czf arsip-log-$(date +%F).tar.gz arsip-log

vier@UBUNTU:~/praktikum-os/week07-bash/logs$ ls -lah
total 16K
drwxrwxr-x 3 vier vier 4.0K May  5 11:46 .
drwxrwxr-x 7 vier vier 4.0K May  2 18:10 ..
drwxrwxr-x 2 vier vier 4.0K May  5 11:45 arsip-log
-rw-rw-r-- 1 vier vier  214 May  5 11:46 arsip-log-2026-05-05.tar.gz
```
---

### Praktikum 6.13 — Membedakan Single Quote, Double Quote, dan Escape
#### 1. Uji single quote dan double quote:
Perintah:
```bash
echo '$USER bekerja di $HOME '
echo " $USER bekerja di $HOME "
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash/logs$ echo '$USER bekerja di $HOME'
$USER bekerja di $HOME

vier@UBUNTU:~/praktikum-os/week07-bash/logs$ echo "$USER bekerja di $HOME"
vier bekerja di /home/vier
```
#### 2. Uji escape karakter spasi:
Perintah:
```bash
cd ~/ praktikum - os / week07 - bash / ruang - nama
ls laporan \ server \ april . txt
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash/logs$ cd ~/praktikum-os/week07-bash/ruang-nama

vier@UBUNTU:~/praktikum-os/week07-bash/ruang-nama$ ls laporan\ server\ april.txt
'laporan server april.txt'
```
#### 3. Uji akses file yang sama dengan double quote:
Perintah:
```bash
cat " laporan server april .txt"
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash/ruang-nama$ cat "laporan server april.txt"
```
---

### Praktikum 6.14 — Menangani File dengan Nama Sulit Secara Aman
#### 1. Pastikan file target tersedia:
Perintah:
```bash
cd ~/ praktikum - os / week07 - bash / ruang - nama
ls - lah
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash/ruang-nama$ cd ~/praktikum-os/week07-bash/ruang-nama

vier@UBUNTU:~/praktikum-os/week07-bash/ruang-nama$ ls -lah
total 8.0K
drwxrwxr-x 2 vier vier 4.0K Apr 12 05:55  .
drwxrwxr-x 7 vier vier 4.0K May  2 18:10  ..
-rw-rw-r-- 1 vier vier    0 Apr 12 05:55 'backup [mingguan] server.conf'
-rw-rw-r-- 1 vier vier    0 Apr 12 05:55 'laporan server april.txt'
```
#### 2. Salin file dengan nama kompleks ke folder backup:
Perintah:
```bash
cp -- " backup [ mingguan ] server . conf " \
" $HOME / praktikum -os/week07 - bash / backup /backup -
mingguan - server . conf "
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash/ruang-nama$ cp -- "backup [mingguan] server.conf" \
> "$HOME/praktikum-os/week07-bash/backup/backup-mingguan-server.conf"
```
#### 3. Gunakan variabel untuk memproses path dengan aman:
Perintah:
```bash
file_asli =" $HOME / praktikum -os/week07 - bash /ruang - nama /
backup [ mingguan ] server . conf "
file_salinan =" $HOME / praktikum -os/week07 - bash / backup /
backup - mingguan -server -v2. conf "
cp -- " $file_asli " " $file_salinan "
ls - lah " $HOME / praktikum -os/week07 - bash / backup "
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash/ruang-nama$ file_asli="$HOME/praktikum-os/week07-bash/ruang-nama/backup [mingguan] server.conf"

vier@UBUNTU:~/praktikum-os/week07-bash/ruang-nama$ file_salinan="$HOME/praktikum-os/week07-bash/backup/backup-mingguan-server-v2.conf"

vier@UBUNTU:~/praktikum-os/week07-bash/ruang-nama$ cp -- "$file_asli" "$file_salinan"

vier@UBUNTU:~/praktikum-os/week07-bash/ruang-nama$ ls -lah "$HOME/praktikum-os/week07-bash/backup"
total 12K
drwxrwxr-x 2 vier vier 4.0K May  5 11:51 .
drwxrwxr-x 7 vier vier 4.0K May  2 18:10 ..
-rw-rw-r-- 1 vier vier    0 May  5 11:50 backup-mingguan-server.conf
-rw-rw-r-- 1 vier vier    0 May  5 11:51 backup-mingguan-server-v2.conf
-rw-rw-r-- 1 vier vier   10 May  2 17:57 sample-app.conf.2026-05-02-175705.bak
```
#### 4. Tampilkan daftar file hasil backup
Perintah:
```bash
for file in " $HOME "/ praktikum - os / week07 - bash / backup /*;
do
printf 'Hasil backup : %s\n' " $file "
done
```
Outputnya
```bash
vier@UBUNTU:~/praktikum-os/week07-bash/ruang-nama$ for file in "$HOME/praktikum-os/week07-bash/backup/*;
> do
> printf 'Hasil backup: %s\n' "$file'
> done
```
---

## TUGAS PRAKTIKUM
#### Tugas Praktikum 1 — Toolkit Bash Administrator Pribadi
Konteks riil: seorang administrator sering mengulang perintah yang sama setiap hari. Agar pekerjaan lebih efisien dan konsisten, ia perlu memiliki toolkit Bash pribadi yang otomatis aktif setiap login.
Instruksi tugas:

1. Tambahkan konfigurasi pada .bashrc untuk:
   - menambahkan direktori bin pribadi ke PATH,
   - membuat minimal 2 alias yang membantu kerja harian,
   - membuat minimal 1 fungsi shell yang berguna untuk administrasi.
2. Pastikan konfigurasi tersebut aktif kembali saat membuka shell login.
3. Buat satu script sederhana di direktori bin pribadi, misalnya script untuk menampilkan ringkasan sistem.
4. Uji dari direktori yang berbeda untuk memastikan script dapat dipanggil tanpa menuliskan path lengkap.
5. Simpan bukti pengujian ke file toolkit-bash-report.txt.
Minimal luaran:

- isi blok konfigurasi yang ditambahkan ke .bashrc,
- output echo $PATH,
- output type untuk alias, fungsi, dan script,
- file laporan toolkit-bash-report.txt.
```bash
===============================
TOOLKIT BASH ADMINISTRATOR
===============================

1. BLOK KONFIGURASI .bashrc

# --- Tugas Praktikum 1- Toolkit Bash Administrator Pribadi ---
export PATH="$HOME/praktikum-os/week07-bash/bin:$PATH"

alias ll='ls -lah --color=auto'
alias hist10='history | tail -n 10'
alias ringkas-sistem='free -h && uptime -p'

backup_conf () {
    if [ $# -ne 1 ]; then
        echo " Usage : backup_conf <file>"
        return 1
    fi

    local src="$1"
    local dst="$HOME/praktikum-os/week07-bash/backup"

    if [ ! -f "$src" ]; then
        echo "File tidak ditemukan: $src"
        return 2
    fi

    mkdir -p "$dst"
    cp -- "$src" "$dst/$(basename "$src").$(date +%F-%H%M%S).bak"
    echo "Backup selesai di $dst"
}
# --- End Praktikum Bash Administrator ---


2. OUTPUT ECHO PATH

/home/vier/praktikum-os/week07-bash/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin


3. OUTPUT TYPE

ll is aliased to `ls -lah --color=auto'
hist10 is aliased to `history | tail -n 10'
backup_conf is a function
backup_conf () 
{ 
    if [ $# -ne 1 ]; then
        echo " Usage : backup_conf <file>";
        return 1;
    fi;
    local src="$1";
    local dst="$HOME/praktikum-os/week07-bash/backup";
    if [ ! -f "$src" ]; then
        echo "File tidak ditemukan: $src";
        return 2;
    fi;
    mkdir -p "$dst";
    cp -- "$src" "$dst/$(basename "$src").$(date +%F-%H%M%S).bak";
    echo "Backup selesai di $dst"
}
ringkas-sistem is hashed (/home/vier/praktikum-os/week07-bash/bin/ringkas-sistem)


4. HASIL EKSEKUSI

Output ringkas-sistem:

Hostname  : UBUNTU
User      : vier
Uptime    : up 41 minutes
Disk /    :
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        30G  9.0G   19G  33% /
               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       2.4Gi       258Mi        74Mi       1.2Gi       1.4Gi
Swap:             0B          0B          0B
up 41 minutes


Output backup_conf:

Backup selesai di /home/vier/praktikum-os/week07-bash/backup


===============================
SELESAI
===============================

```
#### Tugas Praktikum 2 — Audit File Konfigurasi dan Logging Aman
Konteks riil: saat troubleshooting, administrator sering perlu menginventarisasi file konfigurasi dan memisahkan output normal dari pesan error.
Instruksi tugas:

1. Buat file laporan bernama audit-konfigurasi-$(date +%F).txt.
2. Cari file *.conf di dalam /etc dan simpan hasilnya ke file laporan.
3. Catat jumlah total file konfigurasi yang ditemukan.
4. Jika ada pesan error, simpan ke file terpisah, misalnya audit-error.log.
5. Tampilkan isi laporan ke terminal dan sekaligus simpan menggunakan tee.
6. Tambahkan ringkasan singkat 3–5 baris yang menjelaskan mengapa pemisahan stdout dan stderr penting dalam audit sistem.
Syarat konsep yang harus muncul:

- redirection >, 2>, atau &>,
- pipeline,
- tee,
- penggunaan variabel atau command substitution.  
Minimal luaran:
- file laporan audit,
- file log error,
- perintah yang digunakan,
- analisis singkat hasil audit.  
Perintah yang digunakan:
```bash
===============================
Audit File dan Logging
===============================

vier@UBUNTU:~/praktikum-os/week07-bash$ {
echo "=== LAPORAN AUDIT FILE KONFIGURASI ===";
echo "Tanggal Audit: $(date)"; 
echo "Daftar file .conf di /etc :"; find /etc -type f -name "conf" 2> audit-error.log;
JUMLAH=$(find /etc -type f -name "*.conf" 2>/dev/null | wc -l);
echo "Total file konfigurasi .conf: $JUMLAH file"; 
echo "=== RINGKASAN STDOUT & STDERR ===";
echo "stdout dan stderr sangat penting dalam audit sistem";
echo "Karena leporan dapat menjadi lebih rapi dan mudah dibaca";
echo "tanpa ada pesan 'permission denied'"; 
} | tee "audit-konfigurasi-$(date +%F).txt"
```
Outputnya:
```bash
=== LAPORAN AUDIT FILE KONFIGURASI ===
Tanggal Audit: Tue May  5 01:20:03 PM UTC 2026
Daftar file .conf di /etc :
/etc/depmod.d/ubuntu.conf
/etc/modprobe.d/blacklist-firewire.conf
/etc/modprobe.d/iwlwifi.conf
/etc/modprobe.d/amd64-microcode-blacklist.conf
/etc/modprobe.d/intel-microcode-blacklist.conf
/etc/modprobe.d/blacklist.conf
/etc/modprobe.d/blacklist-modem.conf
/etc/modprobe.d/blacklist-rare-network.conf
/etc/modprobe.d/blacklist-framebuffer.conf
/etc/modprobe.d/blacklist-ath_pci.conf
/etc/modprobe.d/alsa-base.conf
/etc/ca-certificates.conf
/etc/apparmor/parser.conf
/etc/selinux/semanage.conf
/etc/environment.d/90qt-a11y.conf
/etc/environment.d/90atk-adaptor.conf
/etc/sensors3.conf
/etc/ubuntu-advantage/uaclient.conf
/etc/ufw/ufw.conf
/etc/ufw/sysctl.conf
/etc/sysctl.conf
/etc/brltty.conf
/etc/bluetooth/main.conf
/etc/bluetooth/network.conf
/etc/bluetooth/input.conf
/etc/UPower/UPower.conf
/etc/usb_modeswitch.conf
/etc/ghostscript/fontmap.d/10fonts-urw-base35.conf
/etc/ghostscript/cidfmap.d/90gs-cjk-resource-japan2.conf
/etc/ghostscript/cidfmap.d/90gs-cjk-resource-gb1.conf
/etc/ghostscript/cidfmap.d/90gs-cjk-resource-korea1.conf
/etc/ghostscript/cidfmap.d/90gs-cjk-resource-cns1.conf
/etc/ghostscript/cidfmap.d/90gs-cjk-resource-japan1.conf
/etc/rygel.conf
/etc/PackageKit/PackageKit.conf
/etc/PackageKit/Vendor.conf
/etc/hdparm.conf
/etc/snmp/snmp.conf
/etc/avahi/avahi-daemon.conf
/etc/host.conf
/etc/geoclue/geoclue.conf
/etc/nsswitch.conf
/etc/mke2fs.conf
/etc/fonts/fonts.conf
/etc/fonts/snap-override/10-prefer-noto.conf
/etc/fonts/conf.avail/58-dejavu-lgc-sans.conf
/etc/fonts/conf.avail/57-dejavu-serif.conf
/etc/fonts/conf.avail/20-unhint-small-dejavu-lgc-serif.conf
/etc/fonts/conf.avail/20-unhint-small-dejavu-serif.conf
/etc/fonts/conf.avail/30-droid-noto-mono.conf
/etc/fonts/conf.avail/65-droid-sans-fallback.conf
/etc/fonts/conf.avail/57-dejavu-sans.conf
/etc/fonts/conf.avail/58-dejavu-lgc-sans-mono.conf
/etc/fonts/conf.avail/20-unhint-small-dejavu-sans.conf
/etc/fonts/conf.avail/58-dejavu-lgc-serif.conf
/etc/fonts/conf.avail/57-dejavu-sans-mono.conf
/etc/fonts/conf.avail/20-unhint-small-dejavu-sans-mono.conf
/etc/fonts/conf.avail/20-unhint-small-dejavu-lgc-sans.conf
/etc/fonts/conf.avail/30-droid-noto.conf
/etc/fonts/conf.avail/20-unhint-small-dejavu-lgc-sans-mono.conf
/etc/ld.so.conf
/etc/systemd/pstore.conf
/etc/systemd/logind.conf
/etc/systemd/timesyncd.conf
/etc/systemd/journald.conf
/etc/systemd/sleep.conf
/etc/systemd/timesyncd.conf.d/cloud-init.conf
/etc/systemd/oomd.conf
/etc/systemd/user.conf
/etc/systemd/resolved.conf
/etc/systemd/networkd.conf
/etc/systemd/system.conf
/etc/e2scrub.conf
/etc/initramfs-tools/initramfs.conf
/etc/initramfs-tools/update-initramfs.conf
/etc/locale.conf
/etc/pnm2ppa.conf
/etc/sudo_logsrvd.conf
/etc/sysctl.d/10-zeropage.conf
/etc/sysctl.d/10-console-messages.conf
/etc/sysctl.d/10-ptrace.conf
/etc/sysctl.d/10-bufferbloat.conf
/etc/sysctl.d/10-magic-sysrq.conf
/etc/sysctl.d/10-map-count.conf
/etc/sysctl.d/10-ipv6-privacy.conf
/etc/sysctl.d/10-kernel-hardening.conf
/etc/sysctl.d/10-network-security.conf
/etc/nftables.conf
/etc/sudo.conf
/etc/apt/apt.conf.d/20apt-esm-hook.conf
/etc/apt/apt.conf.d/20snapd.conf
/etc/ld.so.conf.d/x86_64-linux-gnu.conf
/etc/ld.so.conf.d/libc.conf
/etc/udisks2/udisks2.conf
/etc/cracklib/cracklib.conf
/etc/NetworkManager/conf.d/default-wifi-powersave-on.conf
/etc/NetworkManager/NetworkManager.conf
/etc/dbus-1/system.d/com.redhat.PrinterDriversInstaller.conf
/etc/dbus-1/system.d/com.redhat.NewPrinterNotification.conf
/etc/dbus-1/system.d/org.debian.apt.conf
/etc/dbus-1/system.d/com.hp.hplip.conf
/etc/dbus-1/system.d/com.ubuntu.WhoopsiePreferences.conf
/etc/dbus-1/system.d/com.ubuntu.LanguageSelector.conf
/etc/dbus-1/system.d/com.ubuntu.SoftwareProperties.conf
/etc/dbus-1/system.d/org.opensuse.CupsPkHelper.Mechanism.conf
/etc/dbus-1/system.d/kerneloops.conf
/etc/rsyslog.conf
/etc/debconf.conf
/etc/logrotate.conf
/etc/ldap/ldap.conf
/etc/fprintd.conf
/etc/fwupd/fwupd.conf
/etc/fwupd/remotes.d/vendor-directory.conf
/etc/fwupd/remotes.d/lvfs-testing.conf
/etc/fwupd/remotes.d/lvfs.conf
/etc/libao.conf
/etc/adduser.conf
/etc/xattr.conf
/etc/apg.conf
/etc/sane.d/st400.conf
/etc/sane.d/epsonds.conf
/etc/sane.d/saned.conf
/etc/sane.d/epson.conf
/etc/sane.d/matsushita.conf
/etc/sane.d/lexmark.conf
/etc/sane.d/canon_pp.conf
/etc/sane.d/genesys.conf
/etc/sane.d/xerox_mfp.conf
/etc/sane.d/hp5400.conf
/etc/sane.d/mustek.conf
/etc/sane.d/apple.conf
/etc/sane.d/canon_dr.conf
/etc/sane.d/escl.conf
/etc/sane.d/mustek_usb.conf
/etc/sane.d/test.conf
/etc/sane.d/canon_lide70.conf
/etc/sane.d/hp3900.conf
/etc/sane.d/nec.conf
/etc/sane.d/coolscan.conf
/etc/sane.d/teco3.conf
/etc/sane.d/hs2p.conf
/etc/sane.d/leo.conf
/etc/sane.d/rts8891.conf
/etc/sane.d/microtek2.conf
/etc/sane.d/sp15c.conf
/etc/sane.d/plustek.conf
/etc/sane.d/sm3840.conf
/etc/sane.d/net.conf
/etc/sane.d/ibm.conf
/etc/sane.d/ma1509.conf
/etc/sane.d/dc210.conf
/etc/sane.d/gt68xx.conf
/etc/sane.d/gphoto2.conf
/etc/sane.d/dll.conf
/etc/sane.d/abaton.conf
/etc/sane.d/p5.conf
/etc/sane.d/pie.conf
/etc/sane.d/microtek.conf
/etc/sane.d/kvs1025.conf
/etc/sane.d/coolscan2.conf
/etc/sane.d/sceptre.conf
/etc/sane.d/teco2.conf
/etc/sane.d/kodakaio.conf
/etc/sane.d/dmc.conf
/etc/sane.d/cardscan.conf
/etc/sane.d/tamarack.conf
/etc/sane.d/qcam.conf
/etc/sane.d/sharp.conf
/etc/sane.d/magicolor.conf
/etc/sane.d/pieusb.conf
/etc/sane.d/fujitsu.conf
/etc/sane.d/dc25.conf
/etc/sane.d/umax.conf
/etc/sane.d/bh.conf
/etc/sane.d/stv680.conf
/etc/sane.d/avision.conf
/etc/sane.d/s9036.conf
/etc/sane.d/hp4200.conf
/etc/sane.d/dell1600n_net.conf
/etc/sane.d/artec.conf
/etc/sane.d/kodak.conf
/etc/sane.d/umax1220u.conf
/etc/sane.d/hpsj5s.conf
/etc/sane.d/plustek_pp.conf
/etc/sane.d/u12.conf
/etc/sane.d/airscan.conf
/etc/sane.d/snapscan.conf
/etc/sane.d/epjitsu.conf
/etc/sane.d/hp.conf
/etc/sane.d/mustek_pp.conf
/etc/sane.d/pixma.conf
/etc/sane.d/canon.conf
/etc/sane.d/artec_eplus48u.conf
/etc/sane.d/umax_pp.conf
/etc/sane.d/dc240.conf
/etc/sane.d/ricoh.conf
/etc/sane.d/epson2.conf
/etc/sane.d/agfafocus.conf
/etc/sane.d/coolscan3.conf
/etc/sane.d/teco1.conf
/etc/sane.d/canon630u.conf
/etc/udev/iocost.conf
/etc/udev/udev.conf
/etc/pam.conf
/etc/rsyslog.d/50-default.conf
/etc/rsyslog.d/20-ufw.conf
/etc/rsyslog.d/21-cloudinit.conf
/etc/init/whoopsie.conf
/etc/ipp-usb/ipp-usb.conf
/etc/dhcpcd.conf
/etc/kerneloops.conf
/etc/speech-dispatcher/speechd.conf
/etc/speech-dispatcher/modules/espeak-ng-mbrola.conf
/etc/speech-dispatcher/modules/llia_phon-generic.conf
/etc/speech-dispatcher/modules/dtk-generic.conf
/etc/speech-dispatcher/modules/espeak-ng.conf
/etc/speech-dispatcher/modules/espeak-ng-mbrola-generic.conf
/etc/speech-dispatcher/modules/festival.conf
/etc/speech-dispatcher/modules/flite.conf
/etc/speech-dispatcher/modules/mary-generic.conf
/etc/speech-dispatcher/modules/openjtalk.conf
/etc/speech-dispatcher/modules/swift-generic.conf
/etc/speech-dispatcher/modules/epos-generic.conf
/etc/speech-dispatcher/modules/mimic3-generic.conf
/etc/speech-dispatcher/modules/espeak-mbrola-generic.conf
/etc/speech-dispatcher/modules/espeak.conf
/etc/speech-dispatcher/modules/cicero.conf
/etc/speech-dispatcher/clients/emacs.conf
/etc/gdm3/custom.conf
/etc/deluser.conf
/etc/modules-load.d/loop.conf
/etc/modules-load.d/cups-filters.conf
/etc/xdg/user-dirs.conf
/etc/ucf.conf
/etc/gai.conf
/etc/fuse.conf
/etc/gtk-3.0/im-multipress.conf
/etc/apport/crashdb.conf
/etc/gtk-2.0/im-multipress.conf
/etc/security/access.conf
/etc/security/pwquality.conf
/etc/security/namespace.conf
/etc/security/pam_env.conf
/etc/security/capability.conf
/etc/security/limits.conf
/etc/security/time.conf
/etc/security/faillock.conf
/etc/security/limits.d/10-gamemode.conf
/etc/security/limits.d/25-pw-rlimits.conf
/etc/security/sepermit.conf
/etc/security/group.conf
/etc/security/pwhistory.conf
/etc/hp/hplip.conf
/etc/pulse/client.conf
/etc/libaudit.conf
/etc/cups/subscriptions.conf
/etc/cups/snmp.conf
/etc/cups/cups-browsed.conf
/etc/cups/cups-files.conf
/etc/cups/cupsd.conf
Total file konfigurasi .conf: 260 file
=== RINGKASAN STDOUT & STDERR ===
stdout dan stderr sangat penting dalam audit sistem
Karena leporan dapat menjadi lebih rapi dan mudah dibaca
tanpa ada pesan 'permission denied'

===============================
SELESAI
===============================
```
#### Tugas Praktikum 3 — Mini Health Check Harian Server
Konteks riil: administrator perlu membuat pemeriksaan cepat (health check) untuk mengetahui kondisi dasar server sebelum dan sesudah maintenance.
Instruksi tugas:

1. Buat script Bash bernama daily-healthcheck pada direktori bin pribadi.
2. Script minimal harus menampilkan:

- tanggal dan waktu,
- hostname,
- user aktif,
- shell aktif,
- uptime,
- penggunaan memori,
- penggunaan filesystem root,
- 10 baris terakhir history command yang relevan dengan pengecekan.

1. Simpan hasil ke file log harian, misalnya healthcheck-$(date +%F).log.
2. Tampilkan hasil ke terminal dan ke file secara bersamaan.
3. Jika Anda menggunakan pipeline dengan tee, cek juga status exit command utama.
Syarat konsep yang harus muncul:

- environment variable,
- PATH,
- alias atau fungsi pendukung,
- history,
- tee,
- penanganan error dasar.
Minimal luaran:
- file script yang executable,
- contoh isi file log hasil eksekusi,
- penjelasan singkat fungsi tiap bagian script.
```bash
========================================
MINI HEALTH CHECK HARIAN SERVER
========================================

1. SCRIPT DAILY-HEALTHCHECK

Lokasi:
~/praktikum-os/week07-bash/bin/daily-healthcheck

Status:
Executable (sudah menggunakan chmod +x)


2. OUTPUT ECHO PATH

/home/vier/praktikum-os/week07-bash/bin:/home/vier/praktikum-os/week07-bash/bin:/home/vier/praktikum-os/week07-bash/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin


3. HASIL EKSEKUSI SCRIPT

Perintah:
daily-healthcheck

Output:

 === MINI HEALTH CHECK HARIAN === 
Tanggal & Waktu : Tue May  5 02:39:00 PM UTC 2026
Hostname        : UBUNTU
User Aktif      : vier
Shell Aktif     : /bin/bash
Uptime          : up 3 minutes

[1] Penggunaan Memori:
               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       1.8Gi       113Mi        69Mi       2.1Gi       2.0Gi
Swap:             0B          0B          0B

[2] Penggunaan Filesystem Root (/):
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        30G  9.1G   19G  33% /

[3] 10 Baris History Terakhir:
cd ~/praktikum-os/week07-bash
{     echo "=== LAPORAN AUDIT FILE KONFIGURASI ===";     echo "Tanggal Audit: $(date)";      echo "Daftar file .conf di /etc :"; find /etc -type f -name "*.conf" 2> audit-error.log;     JUMLAH=$(find /etc -type f -name "*.conf" 2>/dev/null | wc -l);     echo "Total file konfigurasi .conf: $JUMLAH file";      echo "=== RINGKASAN STDOUT & STDERR ===";     echo "stdout dan stderr sangat penting dalam audit sistem";     echo "Karena leporan dapat menjadi lebih rapi dan mudah dibaca";     echo "tanpa ada pesan 'permission denied'";      } | tee "audit-konfigurasi-$(date +%F).txt"
mkdir -p logs
nano ~/praktikum-os/week07-bash/bin/daily-healthcheck
echo $PATH
daily-healthcheck
ls logs
cat logs/healthcheck-$(date +%F).log
cd ~
daily-healthcheck

Health check berhasil


4. HASIL FILE LOG

Perintah:
ls logs

Output:
arsip-log  
arsip-log-2026-05-05.tar.gz  
healthcheck-2026-05-05.log


Isi file log:

cat logs/healthcheck-$(date +%F).log

 === MINI HEALTH CHECK HARIAN === 
Tanggal & Waktu : Tue May  5 02:39:00 PM UTC 2026
Hostname        : UBUNTU
User Aktif      : vier
Shell Aktif     : /bin/bash
Uptime          : up 3 minutes

[1] Penggunaan Memori:
               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       1.8Gi       113Mi        69Mi       2.1Gi       2.0Gi
Swap:             0B          0B          0B

[2] Penggunaan Filesystem Root (/):
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda2        30G  9.1G   19G  33% /

[3] 10 Baris History Terakhir:
cd ~/praktikum-os/week07-bash
{     echo "=== LAPORAN AUDIT FILE KONFIGURASI ===";     echo "Tanggal Audit: $(date)";      echo "Daftar file .conf di /etc :"; find /etc -type f -name "*.conf" 2> audit-error.log;     JUMLAH=$(find /etc -type f -name "*.conf" 2>/dev/null | wc -l);     echo "Total file konfigurasi .conf: $JUMLAH file";      echo "=== RINGKASAN STDOUT & STDERR ===";     echo "stdout dan stderr sangat penting dalam audit sistem";     echo "Karena leporan dapat menjadi lebih rapi dan mudah dibaca";     echo "tanpa ada pesan 'permission denied'";      } | tee "audit-konfigurasi-$(date +%F).txt"
mkdir -p logs
nano ~/praktikum-os/week07-bash/bin/daily-healthcheck
echo $PATH
daily-healthcheck
ls logs
cat logs/healthcheck-$(date +%F).log
cd ~
daily-healthcheck


5. PENGUJIAN DARI DIREKTORI LAIN

Perintah:
cd ~
daily-healthcheck

Status:
Berhasil dijalankan tanpa path lengkap (PATH berfungsi dengan baik)


========================================
SELESAI
========================================

```
#### Tugas Praktikum 4 — Penanganan File dengan Nama Kompleks dan Arsip Aman
Konteks riil: file hasil backup, ekspor, atau laporan sering memiliki nama yang mengandung spasi atau karakter khusus. Administrator harus tetap dapat memproses file-file tersebut tanpa salah target.
Instruksi tugas:

1. Buat minimal 4 file contoh dengan nama yang bervariasi, termasuk:

- nama file yang mengandung spasi,
- nama file yang mengandung tanda kurung siku atau karakter khusus,
- file dengan pola nama serupa untuk diuji dengan wildcard.

1. Tunjukkan perbedaan hasil jika file diakses tanpa quoting dan dengan quoting yang benar.
2. Lakukan preview wildcard dengan echo sebelum dipakai untuk operasi nyata.
3. Salin file-file tersebut ke direktori backup dengan nama yang aman.
4. Buat arsip tar.gz dari hasil backup.
5. Simpan riwayat perintah yang Anda gunakan ke file riwayat-arsip.txt. Syarat konsep yang harus muncul:

- single quote, double quote, dan escaping,
- wildcard,
- variabel path,
- history,
- operasi file lanjutan yang aman.
Minimal luaran:
- daftar file awal,
- daftar file hasil backup,
- file arsip tar.gz,
- file riwayat-arsip.txt,
- refleksi singkat tentang pentingnya quoting di Bash.
```bash
========================================
PENANGANAN FILE NAMA KOMPLEKS & ARSIP AMAN
========================================

1. DAFTAR FILE AWAL

Perintah:
ls

Output:

audit-error.log
audit-konfigurasi-2026-05-05.txt
backup
bin
diag-history.txt
laporan bulanan.txt
laporan [harian].conf
log-01.txt
log-02.txt
log-03.txt
logs
login-audit.log
ruang-nama
sampel
sample-app.conf
session-info.txt


2. UJI AKSES FILE TANPA QUOTING

Perintah:
ls laporan bulanan.txt

Output:
ls: cannot access 'laporan': No such file or directory
ls: cannot access 'bulanan.txt': No such file or directory

Kesimpulan:
Gagal karena nama file mengandung spasi.


3. UJI AKSES FILE DENGAN QUOTING

Perintah:
ls "laporan bulanan.txt"

Output:
laporan bulanan.txt

Perintah (escaping):
ls laporan\ bulanan.txt

Output:
laporan bulanan.txt

Kesimpulan:
Berhasil karena menggunakan quoting/escaping.


4. PREVIEW WILDCARD

Perintah:
echo log-*.txt

Output:
log-01.txt log-02.txt log-03.txt

Kesimpulan:
Wildcard bekerja untuk memilih file dengan pola tertentu.


5. PROSES BACKUP DENGAN VARIABEL PATH

Perintah:
DIR_BACKUP="$HOME/praktikum-os/week07-bash/backup"
mkdir -p "$DIR_BACKUP"

cp "laporan bulanan.txt" "$DIR_BACKUP/laporan-bulanan-aman.txt"
cp "laporan [harian].conf" "$DIR_BACKUP/laporan-harian-aman.conf"
cp log-*.txt "$DIR_BACKUP/"


6. DAFTAR FILE HASIL BACKUP

Perintah:
ls -lah "$DIR_BACKUP"

Output:

backup-mingguan-server.conf
backup-mingguan-server-v2.conf
.bashrc.2026-05-05-122108.bak
laporan-bulanan-aman.txt
laporan-harian-aman.conf
log-01.txt
log-02.txt
log-03.txt
sample-app.conf.2026-05-02-175705.bak


7. PEMBUATAN ARSIP

Perintah:
tar -czf arsip-backup-$(date +%F).tar.gz backup/


8. FILE ARSIP

Perintah:
ls -lah *.tar.gz

Output:

-rw-rw-r-- 1 vier vier 2.6K May  5 14:49 arsip-backup-2026-05-05.tar.gz


9. RIWAYAT PERINTAH

Perintah:
history | tail -n 25 > riwayat-arsip.txt

Catatan:
Terjadi kesalahan penamaan file:
riwayat-arsip.tx (seharusnya riwayat-arsip.txt)

========================================
SELESAI
========================================
```
---  

*Jobsheet 7 - Sistem Operasi*