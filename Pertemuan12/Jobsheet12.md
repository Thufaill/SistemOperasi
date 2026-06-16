<h1 align="center">JOBSHEET 12 - SISTEM OPERASI</h1>


**Nama**       : M. Javier Thufail  
**NIM**        : 254107020019  
**Kelas**      : TI 1-G  
**No. Absen**  : 18  

---
<h1 align="center"> Manajemen Service</h2>

## Praktek 10.1 — Amati Layanan Aktif Saat Boot
### 1. Lihat semua layanan yang sedang berjalan
```
vier@UBUNTU:~/lab-os/chapter10-services$ systemctl list-units --type=service --state=runing
  UNIT LOAD ACTIVE SUB DESCRIPTION

0 loaded units listed.
```
### 2. Lihat semua unit service yang ada (aktif maupun tidak)
```
vier@UBUNTU:~/lab-os/chapter10-services$ systemctl list-unit-fil
es --type=service | head -30
UNIT FILE                                    STATE           PRESET
apparmor.service                             enabled         enabled
apport-autoreport.service                    static          -
apport-coredump-hook@.service                static          -
apport-forward@.service                      static          -
apport.service                               enabled         enabled
apt-daily-upgrade.service                    static          -
apt-daily.service                            static          -
apt-news.service                             static          -
autovt@.service                              alias           -
blk-availability.service                     enabled         enabled
bolt.service                                 static          -
cloud-config.service                         enabled         enabled
cloud-final.service                          enabled         enabled
cloud-init-hotplugd.service                  static          -
cloud-init-local.service                     enabled         enabled
cloud-init.service                           enabled         enabled
console-getty.service                        disabled        disabled
console-setup.service                        enabled         enabled
container-getty@.service                     static          -
cron.service                                 enabled         enabled
cryptdisks-early.service                     masked          enabled
cryptdisks.service                           masked          enabled
dbus-org.freedesktop.hostname1.service       alias           -
dbus-org.freedesktop.locale1.service         alias           -
dbus-org.freedesktop.login1.service          alias           -
dbus-org.freedesktop.ModemManager1.service   alias           -
dbus-org.freedesktop.resolve1.service        alias           -
dbus-org.freedesktop.thermald.service        alias           -
dbus-org.freedesktop.timedate1.service       alias           -
```
### 3. Analisis waktu boot dan temukan layanan paling lambat
```
vier@UBUNTU:~/lab-os/chapter10-services$ systemd-analyze
Startup finished in 6.014s (kernel) + 1min 16.451s (userspace) = 1min 22.466s
graphical.target reached after 1min 15.684s in userspace.
praditadf@Ubuntu-Server:~/lab-os/chapter10-services$ systemd-analyze blame | head -15
1min 4.497s vboxadd.service
    12.982s apt-daily-upgrade.service
     4.607s cloud-config.service
     3.247s cloud-init.service
     3.104s pollinate.service
     2.735s cloud-init-local.service
     2.168s fwupd.service
     1.670s dev-sda2.device
     1.608s dpkg-db-backup.service
     1.446s apparmor.service
     1.259s apport.service
      741ms cloud-final.service
      682ms e2scrub_reap.service
      603ms fwupd-refresh.service
      580ms logrotate.service
```
### Tantangan
Identifikasi tiga layanan dengan waktu inisialisasi terlama menggunakan systemd-analyze blame. Gunakan pipeline dari Bab 3 (| sort rh | head-3) untuk mempercepat pencariannya. Untuk setiap layanan, cari tahu fungsinya dengan systemctl cat nama-layanan. Tuliskan nama layanan, waktu inisialisasinya, dan penjelasan singkat fungsinya.
```
vier@UBUNTU:~/lab-os/chapter10-services$ systemd-analyze blame | sort -rh | head -3
      741ms cloud-final.service  : Menjalankan skrip konfigurasi tahap akhir `cloud-init` saat server selesai *boot*.
      682ms e2scrub_reap.service : Membersihkan sisa *snapshot* LVM setelah proses pengecekan sistem file (ext4).
      653ms logrotate.service    : Mengunduh dan memperbarui metadata *firmware* dari internet di latar belakang.
vier@UBUNTU:
# /usr/lib/systemd/system/cloud-final.service
[Unit]
# https://docs.cloud-init.io/en/latest/explanation/boot.html
Description=Cloud-init: Final Stage
After=network-online.target time-sync.target cloud-config.service rc-local.service
After=multi-user.target
Before=apt-daily.service
Wants=network-online.target cloud-config.service
ConditionPathExists=!/etc/cloud/cloud-init.disabled
ConditionKernelCommandLine=!cloud-init=disabled
ConditionEnvironment=!KERNEL_CMDLINE=cloud-init=disabled


[Service]
Type=oneshot
ExecStart=/usr/bin/cloud-init modules --mode=final
RemainAfterExit=yes
TimeoutSec=0
KillMode=process
TasksMax=infinity

# Output needs to appear in instance console output
StandardOutput=journal+console

[Install]
WantedBy=cloud-init.target
vier@UBUNTU:~/lab-os/chapter10-services$ systemctl cat e2scrub_reap.service
# /usr/lib/systemd/system/e2scrub_reap.service
[Unit]
Description=Remove Stale Online ext4 Metadata Check Snapshots
ConditionCapability=CAP_SYS_ADMIN
ConditionCapability=CAP_SYS_RAWIO
Documentation=man:e2scrub_all(8)

[Service]
Type=oneshot
WorkingDirectory=/
PrivateNetwork=true
ProtectSystem=true
ProtectHome=read-only
PrivateTmp=yes
AmbientCapabilities=CAP_SYS_ADMIN CAP_SYS_RAWIO
NoNewPrivileges=yes
User=root
IOSchedulingClass=idle
CPUSchedulingPolicy=idle
Environment=SERVICE_MODE=1
ExecStart=/sbin/e2scrub_all -A -r
SyslogIdentifier=%N
RemainAfterExit=no

[Install]
WantedBy=multi-user.target
vier@UBUNTU:~/lab-os/chapter10-services$ systemctl cat logrotate.service
# /usr/lib/systemd/system/logrotate.service
[Unit]
Description=Rotate log files
Documentation=man:logrotate(8) man:logrotate.conf(5)
RequiresMountsFor=/var/log
ConditionACPower=true

[Service]
Type=oneshot
ExecStart=/usr/sbin/logrotate /etc/logrotate.conf

# performance options
Nice=19
IOSchedulingClass=best-effort
IOSchedulingPriority=7

# hardening options
#  details: https://www.freedesktop.org/software/systemd/man/systemd.exec.html
#  no ProtectHome for userdir logs
#  no PrivateNetwork for mail deliviery
#  no NoNewPrivileges for third party rotate scripts
#  no RestrictSUIDSGID for creating setgid directories
LockPersonality=true
MemoryDenyWriteExecute=true
PrivateDevices=true
PrivateTmp=true
ProtectClock=true
ProtectControlGroups=true
ProtectHostname=true
ProtectKernelLogs=true
ProtectKernelModules=true
ProtectKernelTunables=true
ProtectSystem=full
RestrictNamespaces=true
RestrictRealtime=true
```

Praktek 10.2 — Kelola Layanan SSH
1. Periksa status SSH secara menyeluruh
2. Lakukan restart dan pantau perubahannya
3. Lihat dependensi SSH
4. Cek semua unit yang gagal di sistem
Tantangan
Buat skrip Bash (referensi Bab 7) bernama cek-layanan.sh yang memeriksa status daftar layanan dari sebuah berkas teks. Berkas teks daftar-layanan.txt berisi satu nama layanan per baris (isi minimal: ssh, cron, rsyslog). Skrip membaca setiap nama layanan, memeriksa statusnya dengan systemctl is-active, lalu menulis laporan ke berkas laporan-layanan.log dengan format: [TANGGAL] nama-layanan: ACTIVE/INACTIVE. Gunakan date untuk mendapatkan tanggal.

Praktek 10.3 — Buat Layanan Sederhana dari Skrip Bash
1. Siapkan konten yang akan dilayani   
2. Buat skrip wrapper untuk server HTTP
3. Buat berkas unit systemd untuk layanan ini
4. Jalankan layanan dan verifikasi
5. Uji fitur restart otomatis
6. Bersihkan layanan uji setelah selesai
Tantangan
Modifikasi berkas unit demo-web.service sebelum menghapusnya: tambahkan RestartSec=10s agar sistemmenunggu 10 detik sebelum mencoba restart, dan tambahkan Environment="PORT=9091" lalu ubah ExecStart agar menggunakan variabel tersebut. Aktifkan layanan dengan enable dan WantedBy=multi-user.target, lalu uji apakah layanan aktif setelah systemctl daemon-reload. Dokumentasikan perbedaan perilaku dibanding versi sebelumnya.

Praktek 10.4 — Filter dan Analisis Log Layanan
1. Lihat log SSH dari satu jam terakhir
2. Filter log berprioritas error ke atas
3. Ikuti log secara real-time sambil memicu aktivitas
4. Ekstrak log ke berkas untuk analisis
Tantangan
Ekstrak semua log dengan prioritas error (-p err) dari 24 jam terakhir untuk layanan SSH, simpan ke berkas error-ssh-24jam.txt. Gunakan pipeline dari Bab 3 untuk menghitung total jumlah baris error dengan wc-1, lalu tampilkan 10 pesan error yang paling sering muncul menggunakan sort | uniq -c | sort -rn | head -10. Tuliskan perintah lengkap yang kamu gunakan.

Praktek 10.5 — Konfigurasi SSH Server
1. Periksa konfigurasi SSH saat ini
2. Buat backup dan ubah port SSH
3. Validasi konfigurasi dan restart layanan
4. Verifikasi port baru dengan ss
5. Kembalikan port SSH ke 22 setelah praktek
Tantangan
Ubah konfigurasi SSH untuk menambahkan dua pengaturan keamanan: PermitRootLogin no (larang login root langsung) dan MaxAuthTries 3 (maksimal tiga kali percobaan). Lakukan dengan urutan yang aman: backup, edit, validasi dengan sshd -t, reload. Verifikasi perubahan dengan grep -E "PermitRoot|MaxAuth" /etc/ssh/sshd_config. Kemudian periksa log SSH untuk memastikan tidak ada error setelah perubahan dengan journalctl -u ssh -n 20. Referensi Bab 2 untuk penggunaan ss dan Bab 9 untuk keamanan pengguna.


Latihan
Latihan 10.1 — Audit Layanan dan Analisis Boot
1. Jalankan systemctl list-units -type=service -state running dan catat semua layanan aktif. Pilih tiga layanan yang kamu kenal, periksa status masing-masing dengan systemctl status, dan jelaskan fungsinya.
2. Jalankan systemd-analyze blame dan identifikasi lima layanan dengan waktu inisialisasi terlama. Tampilkan hasilnya menggunakan pipeline: systemd-analyze blame | head -5.
3. Jalankan systemctl -failed dan dokumentasikan hasilnya. Jika ada layanan yang gagal, cari tahu penyebabnya dengan journalctl -u nama-layanan -n 30.

Latihan 10.2 — Layanan Kustom dengan Restart Otomatis
1. Buat skrip Bash (referensi Bab 7) bernama monitor-disk. sh yang setiap 30 detik menuliskan penggunaan disk ke berkas log. Gunakan df -h dan date.
2. Buat berkas unit /etc/systemd/system/monitor-disk. service untuk menjalankan skrip tersebut dengan konfigurasi: Restart=always, RestartSec = 5 s, dan berjalan sebagai pengguna kamu sendiri.
3. Aktifkan dan jalankan layanan. Verifikasi dengan systemctl status dan pastikan log masuk ke journal.
4. Simulasikan crash dengan membunuh proses secara paksa (kill -9), tunggu 10 detik, dan verifikasi bahwa layanan hidup kembali secara otomatis.
5. Bersihkan: nonaktifkan layanan dan hapus berkas unit setelah selesai.

Latihan 10.3 — Investigasi Log dan Keamanan SSH
1. Gunakan journalctl -b-perr untuk menemukan semua error sejak boot terakhir. Simpan hasilnya ke berkas dan hitung jumlah baris dengan wc -1.
2. Lakukan tiga perubahan keamanan pada /etc/ssh/sshd_config: tambahkan PermitRootLogin no, MaxAuthTries 3, dan LoginGraceTime 30. Ikuti alur aman: backup, edit, validasi sshd -t, reload.
3. Setelah reload, verifikasi tiga hal: layanan masih berjalan (systemctl status ssh), port masih mendengarkan (ss -tlnp | grep ssh), dan konfigurasi baru terbaca (grep -Е "PermitRoot | MaxAuth | GraceTime" /etc/ssh/sshd_config).
4. Kembalikan konfigurasi SSH ke kondisi semula menggunakan berkas backup.

---
*Jobsheet 12 - Sistem Operasi*