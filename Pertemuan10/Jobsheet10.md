<h1 align="center">JOBSHEET 10 - SISTEM OPERASI</h1>


**Nama**       : M. Javier Thufail  
**NIM**        : 254107020019  
**Kelas**      : TI 1-G  
**No. Absen**  : 18  

---
<h1 align="center">Manajemen Memori & System Call</h2>

## Praktikum 10.1 — Melihat Penggunaan Memori

#### 1. Jalankan free -h untuk melihat ringkasan RAM dan swap
```bash
vier@UBUNTU:~$ free -h
               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       1.7Gi       236Mi        71Mi       2.1Gi       2.1Gi
Swap:             0B          0B          0B
```
#### 2. Lihat detail memori dari kernel melalui /proc/meminfo
```bash
vier@UBUNTU:~$ cat /proc/meminfo | head -n 20
MemTotal:        4008056 kB
MemFree:          240328 kB
MemAvailable:    2232724 kB
Buffers:           20372 kB
Cached:          2153968 kB
SwapCached:            0 kB
Active:          2022224 kB
Inactive:        1369572 kB
Active(anon):    1070168 kB
Inactive(anon):   161232 kB
Active(file):     952056 kB
Inactive(file):  1208340 kB
Unevictable:          16 kB
Mlocked:              16 kB
SwapTotal:             0 kB
SwapFree:              0 kB
Zswap:                 0 kB
Zswapped:              0 kB
Dirty:              1780 kB
Writeback:             0 kB
```
### Analisis
##### 1. Hitung persentase memori tersedia: available / total × 100%. Jika hasilnya di bawah 10%, sistem mulai kekurangan memori.  
Rumus:

```text
available / total × 100%
```

Perhitungan:

```text
2.1 / 3.8 × 100% = 55.26%
```

Hasil menunjukkan bahwa memori tersedia sekitar **55%**.

Karena nilainya masih di atas **10%**, maka sistem masih memiliki memori yang cukup dan belum mengalami kekurangan RAM.

##### 2. Pada baris Swap, apakah kolom used bernilai 0? Jika lebih dari 0, kernel sudah pernah memindahkan data ke disk karena RAM tidak cukup.
Pada output `free -h`:

```bash
Swap: 0B  0B  0B
```

Kolom `used` bernilai **0B**, artinya:

- Sistem belum menggunakan swap
- Kernel belum memindahkan data dari RAM ke disk
- Penggunaan RAM masih dalam kondisi aman

Pada `/proc/meminfo` juga terlihat:

```bash
SwapTotal: 0 kB
SwapFree: 0 kB
```

Hal ini menunjukkan bahwa sistem tidak memiliki swap space aktif.
##### 3. Perhatikan field Cached dan Buffers di /proc/meminfo. Nilai ini sesuai dengan kolom buff/cache pada free -h.
Dari `/proc/meminfo`:

```bash
Buffers:   20372 kB
Cached:  2153968 kB
```

Perhitungan:

```text
20372 + 2153968 = 2174340 kB
```

Hasil tersebut sekitar **2.1 GiB**, sesuai dengan kolom:

```bash
buff/cache = 2.1Gi
```

pada output `free -h`.


## Studi Kasus 10.1 — Server Lambat karena Memori

#### 1. Periksa kondisi memori secara
```bash
vier@UBUNTU:~$ free -h
               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       1.8Gi       229Mi        64Mi       1.9Gi       2.0Gi
Swap:             0B          0B          0B
```
#### 2. Pantau proses secara real-time
```bash
vier@UBUNTU:~$ top

top - 07:50:16 up 12 min,  1 user,  load average: 0.25, 1.09, 1.00
Tasks: 215 total,   2 running, 213 sleeping,   0 stopped,   0 zombie
%Cpu(s): 12.3 us, 12.5 sy,  0.0 ni, 73.9 id,  0.1 wa,  0.0 hi,  1.1 si,  0.0 st 
MiB Mem : 48.0/3914.1   [|||||||||||||||||||||||||||||||||||||||||||||                                                ] 
MiB Swap:  0.0/0.0      [                                                                                             ] 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                                          
   2019 vier      20   0 4924108 398904 158692 R  70.5  10.0   4:11.14 gnome-shell                                      
   2892 vier      20   0   11.5g 580340 251048 S  21.2  14.5   2:55.97 firefox                                          
   3722 vier      20   0 2977688 378644 118572 S  13.2   9.4   0:44.89 Isolated Web Co                                  
   4139 vier      20   0  708412  58704  46648 S   9.3   1.5   0:13.96 gnome-terminal-                                  
   2138 vier      20   0  397512  12556   7248 S   3.3   0.3   0:02.27 ibus-daemon                                      
     47 root      20   0       0      0      0 I   3.0   0.0   0:05.28 kworker/u16:1-events_unbound                     
   3117 vier      20   0 2673412 146252  91488 S   2.6   3.6   0:09.38 Privileged Cont                                  
    595 root      20   0       0      0      0 I   1.3   0.0   0:04.18 kworker/u16:8-kvfree_rcu_reclaim                 
   2271 vier      20   0  430204  30208  18800 S   1.3   0.8   0:05.56 ibus-extension-                                  
     15 root      20   0       0      0      0 I   0.7   0.0   0:05.10 rcu_preempt                                      
   2470 vier      20   0  245444   7524   6820 S   0.7   0.2   0:00.49 ibus-engine-sim                                  
   4373 vier      20   0 2578672  71912  56876 S   0.7   1.8   0:01.51 Web Content                                      
     58 root      20   0       0      0      0 I   0.3   0.0   0:00.46 kworker/3:1-mm_percpu_wq                         
    498 root      20   0       0      0      0 I   0.3   0.0   0:01.84 kworker/0:3-events                               
   2550 vier      20   0  917836  40796  30608 S   0.3   1.0   0:00.68 xdg-desktop-por                                  
   3527 vier      20   0 2849100 280096  96216 S   0.3   7.0   0:43.39 Isolated Web Co                                  
   3724 vier      20   0 2578672  72096  57028 S   0.3   1.8   0:01.74 Web Content                                      
   3940 vier      20   0 2578672  72080  57028 S   0.3   1.8   0:01.80 Web Content                                      
   4864 vier      20   0   23192   6028   3804 R   0.3   0.2   0:02.27 top                                              
      1 root      20   0   23316  14752   9808 S   0.0   0.4   0:07.11 systemd                                          
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.05 kthreadd                                         
      3 root      20   0       0      0      0 S   0.0   0.0   0:00.00 pool_workqueue_release                           
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-rcu_gp                                 
      5 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-sync_wq                                
      6 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-kvfree_rcu_reclaim         
```
### Analisis
##### 1. Apakah nilai available sangat kecil (misalnya di bawah 200 MB pada server dengan RAM 2 GB)? Jika ya, server kemungkinan kekurangan memori.
Pada output `free -h`:

```bash
available = 2.0Gi
```

Nilai available masih cukup besar, yaitu sekitar **2.0 GiB**.

Artinya:

- Sistem masih memiliki banyak memori yang dapat digunakan
- Server belum mengalami kekurangan RAM
- Kondisi memori masih aman

Jika nilai available berada di bawah 200 MB pada sistem dengan RAM kecil, maka server dapat mengalami kekurangan memori dan performa menjadi lambat.

##### 2. Apakah kolom used pada baris Swap lebih dari 0? Jika ya, kernel sedang enggunakan swap, yang berarti performa menurun
Pada output:

```bash
Swap: 0B  0B  0B
```

Kolom `used` bernilai **0B**, artinya:

- Kernel tidak menggunakan swap
- RAM masih mencukupi
- Tidak terjadi penurunan performa akibat akses disk swap

Karena swap tidak digunakan, performa sistem masih tergolong baik.

##### 3. Di tampilan top, proses apa yang memiliki %MEM terbesar? Proses tersebut menjadi kandidat utama penyebab lambatnya server.
Pada tampilan `top`, proses dengan `%MEM` terbesar adalah:

```bash
firefox   %MEM = 14.5
```

Selain itu terdapat beberapa proses lain yang juga menggunakan memori cukup besar:

| Proses | %MEM |
|---|---|
| firefox | 14.5% |
| gnome-shell | 10.0% |
| Isolated Web Co | 9.4% |
| Isolated Web Co | 7.0% |

Dapat disimpulkan bahwa:

- `firefox` menjadi proses utama yang paling banyak menggunakan RAM
- Browser dan proses web content merupakan penyebab terbesar penggunaan memori
- Jika sistem terasa lambat, proses-proses browser tersebut menjadi kandidat utama penyebabnya

## Praktikum 10.2 — Mengamati Aktivitas Paging

#### 1. Jalankan vmstat dengan interval 1 detik, 5 sampel
```bash
vier@UBUNTU:~$ vmstat 1 5
procs -----------memory---------- ---swap-- -----io---- -system-- -------cpu-------
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st gu
 3  0      0 189560  20676 2034480    0    0  3392   465 2512    7 11 14 74  1  0  0
 0  0      0 189560  20676 2034532    0    0     0     0  898  737  1  2 97  0  0  0
 4  0      0 189560  20684 2034524    0    0     0   684 3835 5032 22 24 53  0  0  0
 0  0      0 189560  20684 2034532    0    0     0     0 2156 2093  6 10 84  0  0  0
 5  0      0 189608  20684 2034544    0    0     0     0 2658 3493 14 15 71  0  0  0
```

### Analisis
##### 1. Amati nilai si dan so pada kelima baris. Pada sistem normal dengan RAM cukup, kedua nilai ini selalu 0.
Kolom:

- `si` = swap in
- `so` = swap out

Pada seluruh sampel, nilai `si` dan `so` selalu:

```text
0
```

Artinya:

- Tidak ada aktivitas swap
- Sistem masih memiliki RAM yang cukup
- Kernel tidak perlu memindahkan data antara RAM dan disk

Kondisi ini menunjukkan sistem berjalan normal.

##### 2. Jika nilai si atau so sesekali muncul lebih dari 0, artinya pernah ada aktivitas swap. Ini masih wajar jika tidak terus-menerus.
Pada hasil pengamatan ini, tidak ditemukan nilai `si` maupun `so` lebih dari 0.

Jika suatu saat nilai tersebut muncul sesekali, maka artinya sistem pernah menggunakan swap sementara. Hal tersebut masih dianggap normal apabila tidak terjadi terus-menerus.

##### 3. Jika si dan so terus-menerus lebih dari 0, sistem dalam kondisi memory pressure serius — performa turun drastis karena akses disk jauh lebih lambat dari RAM.
Karena nilai `si` dan `so` tetap 0 pada seluruh sampel, maka sistem tidak mengalami memory pressure.

Jika nilai `si` dan `so` terus-menerus lebih dari 0, maka:

- RAM sudah tidak mencukupi
- Sistem mulai sering menggunakan swap
- Performa komputer dapat menurun drastis karena disk jauh lebih lambat dibanding RAM

Pada pengamatan ini kondisi tersebut tidak terjadi.

##### 4. Perhatikan juga kolom free (RAM kosong) dan buff (buffer) untuk memahami kondisi keseluruhan RAM saat itu.
- Kolom free

Nilai `free` berada di sekitar:

```text
189560 kB
```

Artinya masih ada RAM kosong yang tersedia.

- Kolom buff

Nilai `buff` berada di sekitar:

```text
20676 kB
```

Buffer digunakan kernel untuk membantu proses input/output data.

- Kolom cache

Nilai `cache` sangat besar, sekitar:

```text
2034xxx kB
```

Hal ini menunjukkan Linux menggunakan sebagian RAM sebagai cache untuk mempercepat akses file dan program.

Cache ini dapat dilepaskan kembali jika aplikasi membutuhkan RAM tambahan, sehingga kondisi sistem masih tergolong aman dan normal.

## Praktikum 10.3 — Membuat dan Mengonfigurasi Swap File

#### 1. Buat file berukuran 512 MB sebagai calon swap
```bash
vier@UBUNTU:~$ sudo fallocate -l 512M /swapfile-week10
[sudo] password for vier: 
```
#### 2. Atur permission file menjadi 600 — hanya root yang boleh membaca dan menulis
```bash
vier@UBUNTU:~$ sudo chmod 600 /swapfile-week10
```
#### 3. Format file sebagai area swap, lalu aktifkan
```bash
vier@UBUNTU:~$ sudo mkswap /swapfile-week10
Setting up swapspace version 1, size = 512 MiB (536866816 bytes)
no label, UUID=f17ff91e-5763-4531-a99e-f8c8c65321e2

vier@UBUNTU:~$ sudo swapon /swapfile-week10
```
#### 4. Verifikasi swap aktif. Anda akan melihat entri /swapfile-week10 dengan ukuran 512M, dan nilai total pada baris Swap di free -h bertambah 512M
```bash
vier@UBUNTU:~$ swapon --show
NAME             TYPE SIZE USED PRIO
/swapfile-week10 file 512M   0B   -2

vier@UBUNTU:~$ free -h
               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       1.8Gi       170Mi        67Mi       2.0Gi       2.0Gi
Swap:          511Mi          0B       511Mi
```
#### 5. Periksa nilai swappiness, ubah sementara, dan verifikasi perubahan
```bash
vier@UBUNTU:~$ cat /proc/sys/vm/swappiness
60

vier@UBUNTU:~$ sudo sysctl vm.swappiness=10
vm.swappiness = 10

vier@UBUNTU:~$ cat /proc/sys/vm/swappiness
10
```
### Analisis
##### 1. Berapa nilai swappiness default? Apa artinya bagi perilaku kernel dalam menggunakan swap?
Perintah:

```bash
cat /proc/sys/vm/swappiness
```

Output:

```bash
60
```

Nilai default swappiness adalah **60**.

Artinya:

- Kernel cukup aktif menggunakan swap
- Sistem akan mulai memindahkan data dari RAM ke swap ketika penggunaan RAM mulai meningkat
- Nilai ini merupakan konfigurasi standar Linux untuk menjaga keseimbangan antara RAM dan swap

##### 2. Setelah diubah ke 10, konfirmasi nilai berubah pada output cat kedua. Apa dampak nilai 10 terhadap penggunaan swap dibanding nilai 60?
Perintah:

```bash
sudo sysctl vm.swappiness=10
```

Verifikasi:

```bash
cat /proc/sys/vm/swappiness
```

Output:

```bash
10
```

Hal ini membuktikan bahwa nilai swappiness berhasil diubah dari 60 menjadi 10.

### Dampak Nilai 10

Nilai `10` membuat kernel:

- Lebih jarang menggunakan swap
- Lebih memprioritaskan penggunaan RAM
- Baru menggunakan swap ketika RAM benar-benar mulai penuh

Dibanding nilai `60`:

| Swappiness 60 | Swappiness 10 |
|---|---|
| Swap lebih sering digunakan | Swap lebih jarang digunakan |
| Lebih agresif memindahkan data ke swap | Lebih mempertahankan data di RAM |
| Cocok untuk sistem server tertentu | Cocok untuk desktop agar responsif |

Karena akses RAM jauh lebih cepat dibanding disk swap, nilai rendah biasanya membuat sistem desktop terasa lebih responsif.

##### 3. Apakah entri /swapfile-week10 muncul di swapon –show? Jika tidak, pastikan Langkah 2 (chmod 600) sudah dijalankan sebelum Langkah 3.
Pada output:

```bash
swapon --show
```

terlihat entri:

```bash
/swapfile-week10
```

Artinya:

- Swap file berhasil aktif
- Langkah konfigurasi sudah benar

Jika entri tersebut tidak muncul, biasanya penyebabnya:

- Permission file belum diatur ke `600`
- Langkah `chmod 600` belum dijalankan sebelum `mkswap` dan `swapon`
- Swap gagal diaktifkan karena alasan keamanan 

## Praktikum 10.4 — Monitoring Memory

#### 1. Ambil snapshot proses diurutkan dari penggunaan memori terbesar
```bash
vier@UBUNTU:~$ ps aux --sort=-%mem | head
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
vier        2892 30.0 15.1 12118084 606604 ?     Sl   07:39   5:10 /snap/firefox/8247/usr/lib/firefox/firefox
vier        3722  7.7 10.2 2982020 411352 ?      Sl   07:39   1:17 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:44410 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {1a871799-e0f4-4acc-8b4f-44d156bb2eb5} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 8 tab
vier        2019 42.8  9.9 4925136 399916 ?      Ssl  07:38   7:36 /usr/bin/gnome-shell
vier        3527  6.4  6.9 2847036 278768 ?      Sl   07:39   1:05 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:43483 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {148bd2f8-d0fe-4d53-898b-b035eefba6bb} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 6 tab
vier        3117  1.0  3.6 2673396 146940 ?      Sl   07:39   0:10 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:38076 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {979fe0d7-130e-4460-8e71-2fb30b7e12b8} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 3 tab
vier        2861  0.0  2.5 1423280 102192 ?      Sl   07:39   0:00 /usr/libexec/mutter-x11-frames
vier        3353  0.1  2.4 2617460 99476 ?       Sl   07:39   0:01 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:38198 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {1dc83fe5-bb44-4a7c-8596-c64ae13209bd} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 5 tab
vier        2806  0.0  2.0 650952 83360 ?        Ssl  07:39   0:00 /usr/libexec/gsd-xsettings
vier        3724  0.2  1.7 2578672 72100 ?       Sl   07:39   0:02 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:44410 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {853a7ae0-6970-4e67-8380-07bd73bdcacc} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 9 tab
```
#### 2. Pantau secara real-time dengan top
```bash
vier@UBUNTU:~$ top

top - 07:58:23 up 20 min,  1 user,  load average: 0.50, 0.95, 0.98
Tasks: 215 total,   1 running, 214 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.3 us,  0.6 sy,  0.0 ni, 98.8 id,  0.0 wa,  0.0 hi,  0.3 si,  0.0 st 
MiB Mem : 49.1/3914.1   [                                                                                             ] 
MiB Swap:  0.0/512.0    [                                                                                             ] 

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND                                          
   2892 vier      20   0   11.6g 605316 255240 S   2.3  15.1   5:16.21 firefox                                          
   2019 vier      20   0 4925136 399872 158692 S   1.3  10.0   7:55.47 gnome-shell                                      
   3722 vier      20   0 2970216 404900 107264 S   1.3  10.1   1:18.36 Isolated Web Co                                  
     76 root      20   0       0      0      0 I   0.3   0.0   0:10.56 kworker/u16:3-kvfree_rcu_reclaim                 
    498 root      20   0       0      0      0 I   0.3   0.0   0:02.40 kworker/0:3-mm_percpu_wq                         
    500 systemd+  20   0   21728  13880  11368 S   0.3   0.3   0:01.14 systemd-resolve                                  
   3117 vier      20   0 2673412 146956  91488 S   0.3   3.7   0:11.25 Privileged Cont                                  
   3724 vier      20   0 2578672  72100  57028 S   0.3   1.8   0:02.71 Web Content                                      
   3968 vier      20   0  503680  32408  24776 S   0.3   0.8   0:00.81 update-notifier                                  
   5035 vier      20   0   23192   6012   3792 R   0.3   0.1   0:00.77 top                                              
      1 root      20   0   23316  14756   9808 S   0.0   0.4   0:07.15 systemd                                          
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.05 kthreadd                                         
      3 root      20   0       0      0      0 S   0.0   0.0   0:00.00 pool_workqueue_release                           
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-rcu_gp                                 
      5 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-sync_wq                                
      6 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-kvfree_rcu_reclaim                     
      7 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-slub_flushwq                           
      8 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-netns                                  
     11 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/0:0H-events_highpri                      
     13 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-mm_percpu_wq                           
     14 root      20   0       0      0      0 S   0.0   0.0   0:01.05 ksoftirqd/0                                      
     15 root      20   0       0      0      0 I   0.0   0.0   0:06.43 rcu_preempt                                      
     16 root      20   0       0      0      0 S   0.0   0.0   0:00.00 rcu_exp_par_gp_kthread_worker/0                  
     17 root      20   0       0      0      0 S   0.0   0.0   0:00.37 rcu_exp_gp_kthread_worker                        
     18 root      rt   0       0      0      0 S   0.0   0.0   0:00.25 migration/0                                      
```
### Analisis
##### 1. Proses apa yang berada di urutan pertama? Catat nilai %MEM dan RSS-nya.
Pada output `ps`, proses di urutan pertama adalah:

```bash
firefox
```

Detail:

| Parameter | Nilai |
|---|---|
| %MEM | 15.1% |
| RSS | 606604 KB |
| VSZ | 12118084 KB |

Pada tampilan `top`, proses yang berada di urutan pertama juga:

```bash
firefox
```

dengan:

| Parameter | Nilai |
|---|---|
| %MEM | 15.1% |
| RES (RSS) | 605316 KB |

Hal ini menunjukkan bahwa Firefox menjadi proses yang paling banyak menggunakan RAM.

##### 2. Konversikan RSS dari KB ke MB (bagi 1024). Misalnya, RSS=524288 berarti proses menggunakan 512 MB RAM. Apakah wajar untuk jenis program tersebut?
Rumus:

```text
MB = KB / 1024
```

Perhitungan:

```text
606604 / 1024 = 592.39 MB
```

Jadi Firefox menggunakan sekitar:

```text
592 MB RAM
```

Penggunaan tersebut masih tergolong wajar karena:

- Browser modern membutuhkan memori besar
- Banyak tab dan proses web aktif
- Firefox menggunakan arsitektur multi-process untuk stabilitas dan keamanan

Selain Firefox utama, terdapat beberapa proses `contentproc` yang juga memakai RAM cukup besar.

##### 3. Mengapa VSZ selalu lebih besar dari RSS pada proses yang sama?
*a.* VSZ (Virtual Size)

VSZ menunjukkan total memori virtual yang dialokasikan proses, termasuk:

- Library
- Shared memory
- Memory mapping
- Swap
- Area memori yang belum benar-benar digunakan

*b.* RSS (Resident Set Size)

RSS menunjukkan jumlah RAM fisik yang benar-benar sedang digunakan proses.

Karena VSZ mencakup seluruh memori virtual, maka nilainya hampir selalu lebih besar dibanding RSS.

Contoh pada Firefox:

| Jenis | Nilai |
|---|---|
| VSZ | 12118084 KB |
| RSS | 606604 KB |

Artinya Firefox memesan memori virtual sangat besar, tetapi yang benar-benar digunakan di RAM hanya sekitar 592 MB.

##### 4. Apakah urutan proses di ps konsisten dengan tampilan top saat diurutkan berdasarkan %MEM?
Urutan proses pada `ps` konsisten dengan tampilan `top`.

Pada kedua output:

1. `firefox` berada di posisi pertama
2. `gnome-shell` berada di posisi berikutnya
3. Proses `Isolated Web Co` juga muncul dengan penggunaan memori tinggi

Hal ini menunjukkan bahwa kedua tools memberikan hasil yang sesuai dalam pengurutan berdasarkan penggunaan memori (`%MEM`).

## Praktikum 10.5 — Script Monitor Memori

#### 1. Masuk ke direktori kerja dan buat file scrip
```bash
vier@UBUNTU:~$ mkdir -p ~/praktikum-os/week10-memory

vier@UBUNTU:~$ cd ~/praktikum-os/week10-memory

vier@UBUNTU:~/praktikum-os/week10-memory$ nano monitor-memori.sh
```
#### 2. Ketik isi script berikut
```bash
#!/bin/bash
set -euo pipefail

THRESHOLD=20
echo "=== Monitor Memori ==="
date
echo

free -h
echo

AVAIL=$(free | awk '/Mem/ {printf "%d", $7/$2*100}')
if [ "$AVAIL" -lt "$THRESHOLD" ]; then
echo "PERINGATAN: Memori tersedia hanya ${AVAIL}%!"
else
echo "Status: Memori tersedia ${AVAIL}% (normal)"
fi
echo
echo "--- 5 Proses Memori Tertinggi ---"
ps aux --sort=-%mem | head -n 6 | tail -n 5
```
#### 3. Beri izin eksekusi dan jalankan script
```bash
vier@UBUNTU:~/praktikum-os/week10-memory$ chmod +x monitor-memori.sh 
vier@UBUNTU:~/praktikum-os/week10-memory$ bash monitor-memori.sh 
=== Monitor Memori ===
Fri May 15 08:17:21 AM UTC 2026

               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       1.9Gi       232Mi        67Mi       1.9Gi       2.0Gi
Swap:          511Mi       316Ki       511Mi

Status: Memori tersedia 51% (normal)

--- 5 Proses Memori Tertinggi ---
vier        2892 22.8 14.9 12137816 598344 ?     Sl   07:47   6:50 /snap/firefox/8247/usr/lib/firefox/firefox
vier        3722  6.2  9.6 3010152 388116 ?      Sl   07:47   1:51 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:44410 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {1a871799-e0f4-4acc-8b4f-44d156bb2eb5} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 8 tab
vier        2019 34.2  9.2 4926160 371664 ?      Ssl  07:46  10:27 /usr/bin/gnome-shell
vier        3527  4.5  6.5 2847672 261628 ?      Sl   07:47   1:21 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:43483 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {148bd2f8-d0fe-4d53-898b-b035eefba6bb} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 6 tab
vier        3117  0.7  3.6 2673412 146016 ?      Sl   07:47   0:13 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:38076 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {979fe0d7-130e-4460-8e71-2fb30b7e12b8} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 3 tab
```
### Analisis
##### 1. Variabel THRESHOLD=20 menetapkan batas persentase. Perintah free | awk ’/Mem/ {printf "%d", $7/$2*100}’ mengambil kolom ke-7 (available) dibagi kolom ke-2 (total) dari baris Mem, lalu dikalikan 100 untuk menghasilkan persentase bilangan bulat.
```text
Available / total x 100
    2.0Gi / 3.8Gi x 100
  =  52.63%
```
##### 2. Kondisi if [ "$AVAIL" -lt "$THRESHOLD" ] bernilai benar jika persentase memori tersedia di bawah 20.
```
Memori tersedia 51% lebih besar dari THRESHOLD=20, sehingga outputnya adalah echo "Status: Memori tersedia ${AVAIL}% (normal)"
```
##### 3. Ubah THRESHOLD menjadi 90 dan jalankan ulang. Apa yang berubah pada output? Mengapa demikian?
Perintah:
```bash
vier@UBUNTU:~/praktikum-os/week10-memory$ nano monitor-memori.sh
#!/bin/bash
set -euo pipefail

THRESHOLD=90
echo "=== Monitor Memori ==="
date
echo

free -h
echo

AVAIL=$(free | awk '/Mem/ {printf "%d", $7/$2*100}')
if [ "$AVAIL" -lt "$THRESHOLD" ]; then
echo "PERINGATAN: Memori tersedia hanya ${AVAIL}%!"
else
echo "Status: Memori tersedia ${AVAIL}% (normal)"
fi
echo
echo "--- 5 Proses Memori Tertinggi ---"
ps aux --sort=-%mem | head -n 6 | tail -n 5

vier@UBUNTU:~/praktikum-os/week10-memory$ ./monitor-memori.sh 
```
Outputnya:
```bash
=== Monitor Memori ===
Fri May 15 08:38:50 AM UTC 2026

               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       1.9Gi       104Mi        79Mi       1.9Gi       1.9Gi
Swap:          511Mi       1.0Mi       510Mi

PERINGATAN: Memori tersedia hanya 49%!

--- 5 Proses Memori Tertinggi ---
vier        2892 23.6 15.9 12219640 640208 ?     Sl   07:47  12:10 /snap/firefox/8247/usr/lib/firefox/firefox
vier        3722  5.6 10.9 3015900 438152 ?      Sl   07:47   2:54 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:44410 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {1a871799-e0f4-4acc-8b4f-44d156bb2eb5} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 8 tab
vier        2019 37.8 10.0 4947420 401220 ?      Ssl  07:46  19:40 /usr/bin/gnome-shell
vier        3527  4.3  6.6 2849720 266856 ?      Sl   07:47   2:13 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:43483 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {148bd2f8-d0fe-4d53-898b-b035eefba6bb} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 6 tab
vier        3117  0.5  4.1 2689952 167020 ?      Sl   07:47   0:17 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:38076 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {979fe0d7-130e-4460-8e71-2fb30b7e12b8} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 3 tab
```
Output berubah yang awalnya status aman menjadi muncul PERINGATAN: Memori tersedia hanya 49%! karena memori tersedia(49%) lebih kecil dari TRESHOLD(90).

## Studi Kasus 10.2 — Gagal Akses File

#### 1. Buat direktori dan file konfigurasi contoh
```bash
vier@UBUNTU:~/praktikum-os/week10-memory$ mkdir -p ~/praktikum-os/week10-memory/syscall-case

vier@UBUNTU:~/praktikum-os/week10-memory$ cd ~/praktikum-os/week10-memory/syscall-case

vier@UBUNTU:~/praktikum-os/week10-memory/syscall-case$ echo "PORT=8080" > app.conf

vier@UBUNTU:~/praktikum-os/week10-memory/syscall-case$ ls -l app.conf 
-rw-rw-r-- 1 vier vier 10 May 15 08:42 app.conf

vier@UBUNTU:~/praktikum-os/week10-memory/syscall-case$ cat app.conf
PORT=8080
```
#### 2. Simulasikan permission bermasalah
```bash
vier@UBUNTU:~/praktikum-os/week10-memory/syscall-case$ chmod 000 app.conf

vier@UBUNTU:~/praktikum-os/week10-memory/syscall-case$ cat app.conf 
cat: app.conf: Permission denied
```
#### 3. Kembalikan permission dan verifikasi
```bash
vier@UBUNTU:~/praktikum-os/week10-memory/syscall-case$ chmod 644 app.conf
vier@UBUNTU:~/praktikum-os/week10-memory/syscall-case$ cat app.conf 
PORT=8080
```

### Analisis
##### 1. Mengapa cat menghasilkan Permission denied setelah chmod 000? System call apa yang gagal?
Setelah menjalankan:

```bash
chmod 000 app.conf
```

semua izin akses file dihapus, sehingga file tidak bisa dibaca, ditulis, maupun dijalankan.

Saat `cat app.conf` dijalankan, system call `open()` gagal karena tidak memiliki izin akses, sehingga muncul pesan:

```bash
Permission denied
```
##### 2. Apa perbedaan pesan error Permission denied vs No such file or directory? Coba rm app.conf lalu cat app.conf untuk melihat perbedaannya.
| Error | Arti |
|---|---|
| Permission denied | File ada tetapi tidak punya izin akses |
| No such file or directory | File tidak ada atau sudah dihapus |
##### 3. Permission 644 berarti apa untuk owner, group, dan others?
Permission `644` berarti:

| User | Izin |
|---|---|
| Owner | read dan write |
| Group | read |
| Others | read |

Jadi owner bisa membaca dan mengubah file, sedangkan user lain hanya bisa membaca.

## Praktikum 10.6 — Mengamati System Call dengan strace

#### 1. Lihat 30 baris pertama system call dari perintah ls
```bash
vier@UBUNTU:~/praktikum-os/week10-memory/syscall-case$ strace ls 2>&1 \ head -n 30
execve("/usr/bin/ls", ["ls", " head", "-n", "30"], 0x7ffef76cc258 /* 51 vars */) = 0
brk(NULL)                               = 0x55db59743000
mmap(NULL, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x79f3894ce000
access("/etc/ld.so.preload", R_OK)      = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/etc/ld.so.cache", O_RDONLY|O_CLOEXEC) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=57483, ...}) = 0
mmap(NULL, 57483, PROT_READ, MAP_PRIVATE, 3, 0) = 0x79f3894bf000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libselinux.so.1", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\0\0\0\0\0\0\0\0"..., 832) = 832
fstat(3, {st_mode=S_IFREG|0644, st_size=174472, ...}) = 0
mmap(NULL, 181960, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x79f389492000
mmap(0x79f389498000, 118784, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x6000) = 0x79f389498000
mmap(0x79f3894b5000, 24576, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x23000) = 0x79f3894b5000
mmap(0x79f3894bb000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x29000) = 0x79f3894bb000
mmap(0x79f3894bd000, 5832, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x79f3894bd000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libc.so.6", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\3\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\220\243\2\0\0\0\0\0"..., 832) = 832
pread64(3, "\6\0\0\0\4\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0"..., 784, 64) = 784
fstat(3, {st_mode=S_IFREG|0755, st_size=2125328, ...}) = 0
pread64(3, "\6\0\0\0\4\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0@\0\0\0\0\0\0\0"..., 784, 64) = 784
mmap(NULL, 2170256, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x79f389200000
mmap(0x79f389228000, 1605632, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x28000) = 0x79f389228000
mmap(0x79f3893b0000, 323584, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1b0000) = 0x79f3893b0000
mmap(0x79f3893ff000, 24576, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x1fe000) = 0x79f3893ff000
mmap(0x79f389405000, 52624, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_ANONYMOUS, -1, 0) = 0x79f389405000
close(3)                                = 0
openat(AT_FDCWD, "/lib/x86_64-linux-gnu/libpcre2-8.so.0", O_RDONLY|O_CLOEXEC) = 3
read(3, "\177ELF\2\1\1\0\0\0\0\0\0\0\0\0\3\0>\0\1\0\0\0\0\0\0\0\0\0\0\0"..., 832) = 832
fstat(3, {st_mode=S_IFREG|0644, st_size=625344, ...}) = 0
mmap(NULL, 627472, PROT_READ, MAP_PRIVATE|MAP_DENYWRITE, 3, 0) = 0x79f389166000
mmap(0x79f389168000, 450560, PROT_READ|PROT_EXEC, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x2000) = 0x79f389168000
mmap(0x79f3891d6000, 163840, PROT_READ, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x70000) = 0x79f3891d6000
mmap(0x79f3891fe000, 8192, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_FIXED|MAP_DENYWRITE, 3, 0x97000) = 0x79f3891fe000
close(3)                                = 0
mmap(NULL, 12288, PROT_READ|PROT_WRITE, MAP_PRIVATE|MAP_ANONYMOUS, -1, 0) = 0x79f38948f000
arch_prctl(ARCH_SET_FS, 0x79f38948f800) = 0
set_tid_address(0x79f38948fad0)         = 5712
set_robust_list(0x79f38948fae0, 24)     = 0
rseq(0x79f389490120, 0x20, 0, 0x53053053) = 0
mprotect(0x79f3893ff000, 16384, PROT_READ) = 0
mprotect(0x79f3891fe000, 4096, PROT_READ) = 0
mprotect(0x79f3894bb000, 4096, PROT_READ) = 0
mprotect(0x55db45ca5000, 8192, PROT_READ) = 0
mprotect(0x79f38950e000, 8192, PROT_READ) = 0
prlimit64(0, RLIMIT_STACK, NULL, {rlim_cur=8192*1024, rlim_max=RLIM64_INFINITY}) = 0
munmap(0x79f3894bf000, 57483)           = 0
statfs("/sys/fs/selinux", 0x7ffe94d15660) = -1 ENOENT (No such file or directory)
statfs("/selinux", 0x7ffe94d15660)      = -1 ENOENT (No such file or directory)
getrandom("\x92\x83\x00\xc3\xe3\xc4\x6b\x13", 8, GRND_NONBLOCK) = 8
brk(NULL)                               = 0x55db59743000
brk(0x55db59764000)                     = 0x55db59764000
openat(AT_FDCWD, "/proc/filesystems", O_RDONLY|O_CLOEXEC) = 3
fstat(3, {st_mode=S_IFREG|0444, st_size=0, ...}) = 0
read(3, "nodev\tsysfs\nnodev\ttmpfs\nnodev\tbd"..., 1024) = 393
read(3, "", 1024)                       = 0
close(3)                                = 0
access("/etc/selinux/config", F_OK)     = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/lib/locale/locale-archive", O_RDONLY|O_CLOEXEC) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=14596880, ...}) = 0
mmap(NULL, 14596880, PROT_READ, MAP_PRIVATE, 3, 0) = 0x79f388200000
close(3)                                = 0
ioctl(1, TCGETS, {c_iflag=ICRNL|IXON|IUTF8, c_oflag=NL0|CR0|TAB0|BS0|VT0|FF0|OPOST|ONLCR, c_cflag=B38400|CS8|CREAD, c_lflag=ISIG|ICANON|ECHO|ECHOE|ECHOK|IEXTEN|ECHOCTL|ECHOKE, ...}) = 0
openat(AT_FDCWD, "/usr/share/locale/locale.alias", O_RDONLY|O_CLOEXEC) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=2996, ...}) = 0
read(3, "# Locale name alias data base.\n#"..., 4096) = 2996
read(3, "", 4096)                       = 0
close(3)                                = 0
openat(AT_FDCWD, "/usr/share/locale/en_US.UTF-8/LC_TIME/coreutils.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale/en_US.utf8/LC_TIME/coreutils.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale/en_US/LC_TIME/coreutils.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale/en.UTF-8/LC_TIME/coreutils.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale/en.utf8/LC_TIME/coreutils.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale/en/LC_TIME/coreutils.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/lib/x86_64-linux-gnu/gconv/gconv-modules.cache", O_RDONLY|O_CLOEXEC) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=27028, ...}) = 0
mmap(NULL, 27028, PROT_READ, MAP_SHARED, 3, 0) = 0x79f3894c7000
close(3)                                = 0
futex(0x79f38940472c, FUTEX_WAKE_PRIVATE, 2147483647) = 0
statx(AT_FDCWD, " head", AT_STATX_SYNC_AS_STAT|AT_SYMLINK_NOFOLLOW|AT_NO_AUTOMOUNT, STATX_MODE|STATX_NLINK|STATX_UID|STATX_GID|STATX_MTIME|STATX_SIZE, 0x7ffe94d15140) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale/en_US.UTF-8/LC_MESSAGES/coreutils.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale/en_US.utf8/LC_MESSAGES/coreutils.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale/en_US/LC_MESSAGES/coreutils.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale/en.UTF-8/LC_MESSAGES/coreutils.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale/en.utf8/LC_MESSAGES/coreutils.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale/en/LC_MESSAGES/coreutils.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale-langpack/en_US.UTF-8/LC_MESSAGES/coreutils.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale-langpack/en_US.utf8/LC_MESSAGES/coreutils.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale-langpack/en_US/LC_MESSAGES/coreutils.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale-langpack/en.UTF-8/LC_MESSAGES/coreutils.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale-langpack/en.utf8/LC_MESSAGES/coreutils.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale-langpack/en/LC_MESSAGES/coreutils.mo", O_RDONLY) = 3
fstat(3, {st_mode=S_IFREG|0644, st_size=613, ...}) = 0
mmap(NULL, 613, PROT_READ, MAP_PRIVATE, 3, 0) = 0x79f3894c6000
close(3)                                = 0
write(2, "ls: ", 4ls: )                     = 4
write(2, "cannot access ' head'", 21cannot access ' head')   = 21
openat(AT_FDCWD, "/usr/share/locale/en_US.UTF-8/LC_MESSAGES/libc.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale/en_US.utf8/LC_MESSAGES/libc.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale/en_US/LC_MESSAGES/libc.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale/en.UTF-8/LC_MESSAGES/libc.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale/en.utf8/LC_MESSAGES/libc.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale/en/LC_MESSAGES/libc.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale-langpack/en_US.UTF-8/LC_MESSAGES/libc.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale-langpack/en_US.utf8/LC_MESSAGES/libc.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale-langpack/en_US/LC_MESSAGES/libc.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale-langpack/en.UTF-8/LC_MESSAGES/libc.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale-langpack/en.utf8/LC_MESSAGES/libc.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
openat(AT_FDCWD, "/usr/share/locale-langpack/en/LC_MESSAGES/libc.mo", O_RDONLY) = -1 ENOENT (No such file or directory)
write(2, ": No such file or directory", 27: No such file or directory) = 27
write(2, "\n", 1
)                       = 1
statx(AT_FDCWD, "30", AT_STATX_SYNC_AS_STAT|AT_SYMLINK_NOFOLLOW|AT_NO_AUTOMOUNT, STATX_MODE|STATX_NLINK|STATX_UID|STATX_GID|STATX_MTIME|STATX_SIZE, 0x7ffe94d15140) = -1 ENOENT (No such file or directory)
write(2, "ls: ", 4ls: )                     = 4
write(2, "cannot access '30'", 18cannot access '30')      = 18
write(2, ": No such file or directory", 27: No such file or directory) = 27
write(2, "\n", 1
)                       = 1
close(1)                                = 0
close(2)                                = 0
exit_group(2)                           = ?
+++ exited with 2 +++
```
#### 2. Lihat ringkasan statistik dan bandingkan dua direktori berbeda
```bash
vier@UBUNTU:~/praktikum-os/week10-memory/syscall-case$ strace -c ls
app.conf
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 16.74    0.001668          92        18           mmap
 16.74    0.001668        1668         1           execve
 11.54    0.001150         127         9           close
  8.72    0.000869         173         5           mprotect
  7.95    0.000792          99         8           fstat
  4.70    0.000468          66         7           openat
  4.53    0.000451         225         2           getdents64
  4.38    0.000437         218         2           ioctl
  3.72    0.000371         371         1           arch_prctl
  3.11    0.000310         310         1           set_tid_address
  2.84    0.000283          94         3           brk
  2.67    0.000266         133         2         2 statfs
  2.64    0.000263         263         1           write
  2.33    0.000232          46         5           read
  2.07    0.000206         206         1           getrandom
  1.75    0.000174         174         1           set_robust_list
  1.72    0.000171         171         1           munmap
  1.13    0.000113         113         1           rseq
  0.49    0.000049          24         2         2 access
  0.15    0.000015           7         2           pread64
  0.10    0.000010          10         1           prlimit64
------ ----------- ----------- --------- --------- ----------------
100.00    0.009966         134        74         4 total

vier@UBUNTU:~/praktikum-os/week10-memory/syscall-case$ strace -c ls /etc 2>&1 | tail -5
  0.36    0.000060          60         1           munmap
  0.13    0.000021          21         1           write
  0.05    0.000008           8         1           getrandom
------ ----------- ----------- --------- --------- ----------------
100.00    0.016742         220        76         5 total
```
### Analisis
##### 1. Dari output Langkah 1, identifikasi minimal 4 system call berbeda. Jelaskan fungsi singkat masing-masing berdasarkan argumen yang terlihat.
Beberapa system call yang muncul:

| System Call | Fungsi |
|---|---|
| `execve()` | Menjalankan program `ls` |
| `openat()` | Membuka file atau direktori |
| `read()` | Membaca isi file |
| `close()` | Menutup file yang sudah dibuka |
| `mmap()` | Memetakan file/library ke memori |
| `write()` | Menampilkan output ke terminal |

##### 2. Dari ringkasan strace -c, system call mana yang paling sering dipanggil? Mengapa?
Dari output `strace -c`, system call yang paling sering dipanggil adalah:

```bash
mmap
```

karena program `ls` perlu memuat library dan data ke memori saat dijalankan.

Selain itu `openat()` dan `fstat()` juga sering dipanggil untuk membaca file dan direktori.

##### 3. Apakah ada system call dengan errors lebih dari 0? Apakah itu berarti program bermasalah, ataukah bagian normal dari logika program?
Ada beberapa system call dengan error, contohnya:

```bash
ENOENT (No such file or directory)
```

Hal ini tidak selalu berarti program bermasalah.

Sering kali program memang mencoba mencari file tertentu terlebih dahulu. Jika file tidak ada, program akan lanjut menggunakan alternatif lain. Jadi kondisi ini masih normal.

##### 4. Apakah jumlah system call berbeda antara ls dan ls /etc? Faktor apa yang menyebabkan perbedaan tersebut?
Jumlah system call pada:

```bash
ls
```

dan:

```bash
ls /etc
```

sedikit berbeda.

Hal ini terjadi karena:

- isi direktori berbeda
- jumlah file berbeda
- proses pembacaan direktori `/etc` lebih banyak

Semakin banyak file atau proses yang dilakukan, semakin banyak system call yang dipanggil.

## Tugas Praktikum

### 1. Tugas 10.1 Audit Penggunaan Memori Sistem
Instruksi: Buat script memory-audit.sh yang menghasilkan laporan kondisi memori sistem secara otomatis
```bash
vier@UBUNTU:~/praktikum-os/week10-memory$ nano ~/praktikum-os/week10-memory/memory-audit.sh
#!/bin/bash
set - euo pipefail
LAPORAN="memory-report.txt"
{
echo "=== LAPORAN MEMORI SISTEM ==="
date
echo
echo "--- Ringkasan free -h ---"
free -h
echo
echo "--- /proc/meminfo ---"
cat /proc/meminfo | head -n 20
} > "$LAPORAN"
echo "Laporan disimpan ke: $LAPORAN"
cat "$LAPORAN"

vier@UBUNTU:~/praktikum-os/week10-memory$ chmod +x ~/praktikum-os/week10-memory/memory-audit.sh

vier@UBUNTU:~/praktikum-os/week10-memory$ bash memory-audit.sh
Laporan disimpan ke: memory-report.txt
=== LAPORAN MEMORI SISTEM ===
Fri May 15 06:43:33 PM UTC 2026

--- Ringkasan free -h ---
               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       1.9Gi       200Mi        64Mi       1.8Gi       1.9Gi
Swap:          511Mi       1.1Mi       510Mi

--- /proc/meminfo ---
MemTotal:        4008056 kB
MemFree:          205196 kB
MemAvailable:    2042920 kB
Buffers:           22160 kB
Cached:          1830804 kB
SwapCached:          756 kB
Active:           424604 kB
Inactive:        2989116 kB
Active(anon):     212584 kB
Inactive(anon):  1198312 kB
Active(file):     212020 kB
Inactive(file):  1790804 kB
Unevictable:          16 kB
Mlocked:              16 kB
SwapTotal:        524284 kB
SwapFree:         523176 kB
Zswap:                 0 kB
Zswapped:              0 kB
Dirty:               336 kB
Writeback:             0 kB
```
#### Analisis
##### 1. Hitung persentase memori tersedia (available / total × 100%). Apakah sistem dalam kondisi normal?
Perhitungan:

```text
1.9 / 3.8 × 100% = 50%
```

Artinya sekitar 50% memori masih tersedia, sehingga sistem masih dalam kondisi normal dan tidak mengalami kekurangan RAM.

##### 2. Mengapa buff/cache tidak dihitung sebagai memori yang terpakai dari sudut pandang ketersediaan untuk aplikasi?
`buff/cache` digunakan Linux untuk menyimpan cache dan buffer agar akses file lebih cepat.

Memori ini bisa dilepaskan kembali kapan saja jika aplikasi membutuhkan RAM tambahan, sehingga tetap dianggap tersedia untuk sistem.

##### 3. Dari /proc/meminfo, apakah SwapTotal lebih besar dari 0? Berapa nilai SwapFree?
Dari `/proc/meminfo`:

```bash
SwapTotal: 524284 kB
SwapFree: 523176 kB
```

Artinya:

- `SwapTotal` lebih besar dari 0, sehingga sistem memiliki swap aktif
- `SwapFree` sebesar 523176 kB, berarti hampir seluruh swap masih kosong dan belum banyak digunakan

### 2. Tugas 10.2 Identifikasi Proses dengan Memori Tertinggi
Instruksi: Simpan daftar 10 proses pengguna memori terbesar ke file
```bash
vier@UBUNTU:~/praktikum-os/week10-memory$ ps aux --sort=-%mem | head -n 10 > top-memory-process.txt

vier@UBUNTU:~/praktikum-os/week10-memory$ cat top-memory-process.txt 
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
vier        2892 23.6 15.6 12201308 626056 ?     Sl   17:36  15:59 /snap/firefox/8247/usr/lib/firefox/firefox
vier        3722  5.6 10.9 3117520 439560 ?      Sl   17:37   3:48 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:44410 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {1a871799-e0f4-4acc-8b4f-44d156bb2eb5} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 8 tab
vier        2019 37.5 10.0 4947436 401176 ?      Ssl  17:36  25:37 /usr/bin/gnome-shell
vier        3527  4.4  6.7 2849720 269500 ?      Sl   17:37   3:01 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:43483 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {148bd2f8-d0fe-4d53-898b-b035eefba6bb} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 6 tab
vier        3117  0.5  3.8 2673432 153532 ?      Sl   17:37   0:21 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:38076 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {979fe0d7-130e-4460-8e71-2fb30b7e12b8} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 3 tab
vier        3353  0.0  2.4 2617460 98360 ?       Sl   17:37   0:01 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:38198 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {1dc83fe5-bb44-4a7c-8596-c64ae13209bd} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 5 tab
vier        2861  0.0  2.3 1423280 94484 ?       Sl   17:36   0:00 /usr/libexec/mutter-x11-frames
vier        2806  0.0  2.0 650952 82616 ?        Ssl  17:36   0:00 /usr/libexec/gsd-xsettings
vier        3724  0.2  1.7 2578672 72112 ?       Sl   17:37   0:08 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:44410 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {853a7ae0-6970-4e67-8380-07bd73bdcacc} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 9 tab
```
#### Analisis
##### 1. Proses apa di urutan pertama? Catat nilai %MEM dan RSS.
Proses dengan penggunaan memori terbesar adalah:

```bash
firefox
```

Nilainya:

- `%MEM` = 15.6%
- `RSS` = 626056 KB

##### 2. Konversikan RSS ke MB (bagi 1024). Apakah wajar?
Perhitungan:

```text
626056 ÷ 1024 = ±611 MB
```

Jadi Firefox menggunakan sekitar 611 MB RAM.

Nilai ini masih wajar karena browser modern menggunakan banyak memori, terutama saat membuka banyak tab.

##### 3. Jumlahkan %MEM dari 5 proses teratas. Berapa persen RAM yang mereka gunakan bersama?
Perhitungan:

```text
15.6 + 10.9 + 10.0 + 6.7 + 3.8 = 47%
```

Jadi 5 proses teratas menggunakan sekitar 47% RAM sistem secara bersama-sama.

### 3. Tugas 10.3 Membuat dan Memverifikasi Swap File
Instruksi: Buat swap file khusus tugas sebesar 256 MB dan verifikasi
```bash
vier@UBUNTU:~/praktikum-os/week10-memory$ sudo fallocate -l 256M /swapfile-tugas-week10
[sudo] password for vier: 
vier@UBUNTU:~/praktikum-os/week10-memory$ sudo chmod 600 /swapfile-tugas-week10
vier@UBUNTU:~/praktikum-os/week10-memory$ sudo mkswap /swapfile-tugas-week10 
Setting up swapspace version 1, size = 256 MiB (268431360 bytes)
no label, UUID=ab2d5399-a4f9-4380-bbef-e49ef1c71aea
vier@UBUNTU:~/praktikum-os/week10-memory$ sudo swapon /swapfile-tugas-week10
vier@UBUNTU:~/praktikum-os/week10-memory$ {
> echo "=== VERIFIKASI SWAP ==="
> swapon --show
> echo
> free -h
> }
=== VERIFIKASI SWAP ===
NAME                   TYPE SIZE USED PRIO
/swapfile-week10       file 512M 1.1M   -2
/swapfile-tugas-week10 file 256M   0B   -3

               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       1.9Gi       160Mi        69Mi       1.9Gi       1.9Gi
Swap:          767Mi       1.1Mi       766Mi
vier@UBUNTU:~/praktikum-os/week10-memory$ cat swap-check.txt
cat: swap-check.txt: No such file or directory
vier@UBUNTU:~/praktikum-os/week10-memory$ { echo "=== VERIFIKASI SWAP ==="; swapon --show; echo; free -h; } >swap-check.txt
vier@UBUNTU:~/praktikum-os/week10-memory$ cat swap-check.txt
=== VERIFIKASI SWAP ===
NAME                   TYPE SIZE USED PRIO
/swapfile-week10       file 512M 1.1M   -2
/swapfile-tugas-week10 file 256M   0B   -3

               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       1.9Gi       158Mi        68Mi       1.9Gi       1.9Gi
Swap:          767Mi       1.1Mi       766Mi
```
#### Analisis
##### 1. Identifikasi kolom NAME, TYPE, SIZE, dan USED pada output swapon –show.
| Kolom | Arti |
|---|---|
| `NAME` | Nama file swap |
| `TYPE` | Jenis swap (file atau partition) |
| `SIZE` | Ukuran swap |
| `USED` | Jumlah swap yang sedang digunakan |

##### 2. Apakah nilai total pada baris Swap di free -h bertambah 256 MB?
Ya, total swap bertambah sekitar 256 MB.

Sebelumnya:

```text
512Mi
```

Setelah menambah swap baru:

```text
767Mi
```

Artinya swap file baru berhasil ditambahkan.
##### 3. Mengapa permission 600 penting? Apa risiko jika diatur ke 644?
Permission `600` membuat hanya root yang dapat membaca dan menulis file swap.

Hal ini penting untuk keamanan karena swap bisa menyimpan data sementara dari RAM, termasuk data sensitif.

Jika menggunakan `644`, user lain dapat membaca isi swap sehingga berisiko terjadi kebocoran data.

### 4. Tugas 10.4 Analisis System Call dengan strace
Instruksi: Analisis system call yang dipanggil perintah ls
```bash
vier@UBUNTU:~/praktikum-os/week10-memory$ strace -c ls 2> strace-summary.txt
memory-audit.sh    monitor-memori.sh   swap-check.txt  top-memory-process.txt
memory-report.txt  strace-summary.txt  syscall-case
vier@UBUNTU:~/praktikum-os/week10-memory$ strace ls /etc 2> strace-ls-etc.txt
adduser.conf        dictionaries-common   issue.net           os-release      speech-dispatcher
alsa            dpkg              kernel           PackageKit      ssh
alternatives        e2scrub.conf          kerneloops.conf       pam.conf      ssl
anacrontab        emacs              krb5.conf.d       pam.d      sssd
apg.conf        environment          ldap           papersize      subgid
apm            environment.d          ld.so.cache       passwd      subgid-
apparmor        ethertypes          ld.so.conf       passwd-      subuid
apparmor.d        fonts              ld.so.conf.d       pcmcia      subuid-
apport            fprintd.conf          legal           perl          sudo.conf
apt            fstab              libao.conf       pki          sudoers
avahi            fuse.conf          libaudit.conf       plymouth      sudoers.d
bash.bashrc        fwupd              libblockdev       pm          sudo_logsrvd.conf
bash_completion        gai.conf          libibverbs.d       pnm2ppa.conf   supercat
bindresvport.blacklist    gdb              libnl-3           polkit-1      sysctl.conf
binfmt.d        gdm3              libpaper.d       ppp          sysctl.d
bluetooth        geoclue              locale.alias       profile      sysstat
brlapi.key        ghostscript          locale.conf       profile.d      systemd
brltty            glvnd              locale.gen       protocols      terminfo
brltty.conf        gnome              localtime           pulse      thermald
ca-certificates        gnome-remote-desktop  logcheck           python3      timezone
ca-certificates.conf    gnutls              login.defs       python3.12      tmpfiles.d
chatscripts        groff              logrotate.conf       rc0.d      ubuntu-advantage
cloud            group              logrotate.d       rc1.d      ucf.conf
colord            group-              lsb-release       rc2.d      udev
console-setup        grub.d              machine-id       rc3.d      udisks2
cracklib        gshadow              magic           rc4.d      ufw
credstore        gshadow-          magic.mime       rc5.d      update-manager
credstore.encrypted    gss              manpath.config       rc6.d      update-motd.d
cron.d            gtk-2.0              mime.types       rcS.d      update-notifier
cron.daily        gtk-3.0              mke2fs.conf       resolv.conf      UPower
cron.hourly        hdparm.conf          ModemManager       rmt          usb_modeswitch.conf
cron.monthly        host.conf          modprobe.d       rpc          usb_modeswitch.d
crontab            hostname          modules           rsyslog.conf   vconsole.conf
cron.weekly        hosts              modules-load.d       rsyslog.d      vim
cron.yearly        hosts.allow          mtab           rygel.conf      vtrgb
cups            hosts.deny          nanorc           sane.d      vulkan
cupshelpers        hp              netconfig           security      w3m
dbus-1            ifplugd              netplan           selinux      wgetrc
dconf            ImageMagick-6          network           sensors3.conf  wpa_supplicant
debconf.conf        init              networkd-dispatcher  sensors.d      X11
debian_version        init.d              NetworkManager       services      xattr.conf
debuginfod        initramfs-tools       networks           sgml          xdg
default            inputrc              newt           shadow      xml
deluser.conf        insserv.conf.d          nftables.conf       shadow-      zsh_command_not_found
depmod.d        ipp-usb              nsswitch.conf       shells
dhcp            iproute2          openvpn           skel
dhcpcd.conf        issue              opt           snmp
vier@UBUNTU:~/praktikum-os/week10-memory$ cat strace-summary.txt 
% time     seconds  usecs/call     calls    errors syscall
------ ----------- ----------- --------- --------- ----------------
 16.64    0.001532         306         5           read
 14.70    0.001353         270         5           mprotect
 13.51    0.001244         155         8           fstat
 11.22    0.001033         147         7           openat
  7.73    0.000712         712         1           execve
  5.31    0.000489         244         2           getdents64
  5.28    0.000486          54         9           close
  4.70    0.000433          24        18           mmap
  4.50    0.000414         207         2           write
  3.47    0.000319         159         2         2 statfs
  3.24    0.000298         298         1           getrandom
  3.18    0.000293          97         3           brk
  2.16    0.000199          99         2           ioctl
  1.85    0.000170         170         1           munmap
  1.18    0.000109         109         1           prlimit64
  1.05    0.000097          48         2         2 access
  0.11    0.000010           5         2           pread64
  0.04    0.000004           4         1           arch_prctl
  0.04    0.000004           4         1           set_tid_address
  0.04    0.000004           4         1           rseq
  0.03    0.000003           3         1           set_robust_list
------ ----------- ----------- --------- --------- ----------------
100.00    0.009206         122        75         4 total
```
#### Analisis
##### 1. Sebutkan minimal 5 system call dari strace-summary.txt beserta fungsi singkatnya.
| System Call | Fungsi |
|---|---|
| `read` | Membaca isi file |
| `openat` | Membuka file atau direktori |
| `close` | Menutup file |
| `mmap` | Memetakan file/library ke memori |
| `write` | Menulis output ke terminal |
| `execve` | Menjalankan program `ls` |

##### 2. System call mana yang paling sering dipanggil? Mengapa?
System call yang paling sering dipanggil adalah:

```bash
mmap
```

dengan 18 kali pemanggilan.

Hal ini karena program `ls` perlu memuat library dan data ke memori saat dijalankan.

##### 3. Apakah ada errors lebih dari 0? Apakah program tetap berjalan normal meskipun ada kegagalan tersebut?
Ada beberapa error pada:

```bash
statfs
access
```

tetapi program tetap berjalan normal.

Error tersebut biasanya terjadi karena program mencoba mengecek file atau direktori tertentu yang memang tidak ada. Ini merupakan bagian normal dari proses kerja program Linux.

### 5. Tugas 10.5 Studi Kasus Diagnosa Server Lambat
Skenario: Server terasa lambat. Buat script diagnosa yang menggabungkan semua pemeriksaan dari bab ini menggunakan fungsi Bash
```bash
vier@UBUNTU:~/praktikum-os/week10-memory$ nano ~/praktikum-os/week10-memory/diagnosa-server.sh
#!/bin/bash
set -euo pipefail
LAPORAN="diagnosa-server-lambat.txt"
WARN_MEM=false
WARN_SWAP=0
cek_memori() {
echo "--- Kondisi Memori ---"
free -h
echo
AVAIL_PCT=$(free | awk '/Mem/ {printf "%d", $7/$2*100}
')
if [ "$AVAIL_PCT" -lt 20 ]; then
echo "PERINGATAN : Memori tersedia hanya ${AVAIL_PCT}% "
WARN_MEM=true
fi
}
cek_swap() {
echo "--- Penggunaan Swap ---"
swapon --show 2>/dev/null || echo "Tidak ada swap aktif "
echo
WARN_SWAP=$(free | awk '/Swap/ {print $3}')
if [ "$WARN_SWAP" -gt 0 ]; then
echo "INFO: Swap digunakan (${WARN_SWAP} kB)"
fi
}
cek_proses() {
echo "--- 10 Proses Memori Tertinggi ---"
ps aux --sort=-%mem | head -n 11
echo
}
cek_paging() {
echo "--- Aktivitas Paging (5 sampel ) ---"
vmstat 1 5
echo
}
ringkasan() {
echo "=== RINGKASAN === "
if [ "$WARN_MEM" = true ]; then
echo "- Memori: KRITIS - perlu tindakan segera"
else
echo "- Memori : normal"
fi
if [ "$WARN_SWAP" -gt 0 ]; then
echo "- Swap: aktif - pantau aktivitas paging"
else
echo "- Swap: tidak digunakan"
fi
}
{
echo "=== LAPORAN DIAGNOSA SERVER === "
date
echo
cek_memori
cek_swap
cek_proses
cek_paging
ringkasan
} | tee "$LAPORAN"
echo
echo "Laporan disimpan ke : $LAPORAN"

vier@UBUNTU:~/praktikum-os/week10-memory$ chmod +x ~/praktikum-os/week10-memory/diagnosa-server.sh

vier@UBUNTU:~/praktikum-os/week10-memory$ bash diagnosa-server.sh 
=== LAPORAN DIAGNOSA SERVER === 
Fri May 15 06:54:07 PM UTC 2026

--- Kondisi Memori ---
               total        used        free      shared  buff/cache   available
Mem:           3.8Gi       1.9Gi       143Mi        68Mi       1.9Gi       1.9Gi
Swap:          767Mi       1.1Mi       766Mi

--- Penggunaan Swap ---
NAME                   TYPE SIZE USED PRIO
/swapfile-week10       file 512M 1.1M   -2
/swapfile-tugas-week10 file 256M   0B   -3

INFO: Swap digunakan (1108 kB)
--- 10 Proses Memori Tertinggi ---
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
vier        2892 23.8 15.9 12217116 638248 ?     Sl   17:39  17:51 /snap/firefox/8247/usr/lib/firefox/firefox
vier        3722  5.4 11.2 3120988 451752 ?      Sl   17:39   4:05 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:44410 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {1a871799-e0f4-4acc-8b4f-44d156bb2eb5} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 8 tab
vier        2019 38.2 10.0 4943260 401208 ?      Ssl  17:38  28:48 /usr/bin/gnome-shell
vier        3527  4.6  6.8 2849704 273256 ?      Sl   17:39   3:29 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:43483 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {148bd2f8-d0fe-4d53-898b-b035eefba6bb} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 6 tab
vier        3117  0.5  3.8 2673432 154120 ?      Sl   17:39   0:22 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:38076 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {979fe0d7-130e-4460-8e71-2fb30b7e12b8} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 3 tab
vier        3353  0.0  2.4 2617460 98360 ?       Sl   17:39   0:02 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:38198 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {1dc83fe5-bb44-4a7c-8596-c64ae13209bd} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 5 tab
vier        2861  0.0  2.3 1423280 94484 ?       Sl   17:39   0:01 /usr/libexec/mutter-x11-frames
vier        2806  0.0  2.0 650952 82616 ?        Ssl  17:39   0:00 /usr/libexec/gsd-xsettings
vier        3724  0.2  1.7 2578672 72112 ?       Sl   17:39   0:09 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:44410 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {853a7ae0-6970-4e67-8380-07bd73bdcacc} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 9 tab
vier        3940  0.2  1.7 2578672 72096 ?       Sl   17:39   0:09 /snap/firefox/8247/usr/lib/firefox/firefox -contentproc -isForBrowser -prefsHandle 0:44597 -prefMapHandle 1:285632 -jsInitHandle 2:156120 -parentBuildID 20260427221700 -sandboxReporter 3 -chrootClient 4 -ipcHandle 5 -initialChannelId {0fbf4e50-8513-42d2-9c21-61d240f4e5aa} -parentPid 2892 -crashReporter 6 -crashHelper 7 -greomni /snap/firefox/8247/usr/lib/firefox/omni.ja -appomni /snap/firefox/8247/usr/lib/firefox/browser/omni.ja -appDir /snap/firefox/8247/usr/lib/firefox/browser 10 tab

--- Aktivitas Paging (5 sampel ) ---
procs -----------memory---------- ---swap-- -----io---- -system-- -------cpu-------
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st gu
 3  0   1108 146440  23184 1918404    0    0   672   125 2074    6  7  9 83  0  0  0
 2  0   1108 146172  23184 1918532    0    0     0     0  771  665  1  2 98  0  0  0
 7  0   1108 146172  23184 1918532    0    0     0     0 1463 1386  1  3 96  0  0  0
 0  0   1108 146172  23192 1918552    0    0     0   648 3161 3530 13 14 73  0  0  0
 0  0   1108 146172  23192 1918552    0    0     0     0 3509 3915 16 15 68  0  0  0

=== RINGKASAN === 
- Memori : normal
- Swap: aktif - pantau aktivitas paging

Laporan disimpan ke : diagnosa-server-lambat.txt

```
#### Analisis
##### 1. Jelaskan peran masing-masing fungsi: cek_memori, cek_swap, cek_proses, cek_paging, dan ringkasan. Mengapa diagnosa dipecah menjadi fungsi terpisah?
| Fungsi | Peran |
|---|---|
| `cek_memori` | Mengecek kondisi RAM dan persentase memori tersedia |
| `cek_swap` | Mengecek penggunaan swap |
| `cek_proses` | Menampilkan proses dengan penggunaan memori terbesar |
| `cek_paging` | Memantau aktivitas paging menggunakan `vmstat` |
| `ringkasan` | Menampilkan kesimpulan kondisi server |

Diagnosa dipisah menjadi beberapa fungsi agar script lebih rapi, mudah dibaca, dan mudah dikembangkan.

##### 2. Berdasarkan bagian RINGKASAN, apakah kondisi sistem normal atau kritis? Jelaskan berdasarkan nilai threshold yang digunakan script.
Berdasarkan bagian:

```bash
- Memori : normal
- Swap: aktif - pantau aktivitas paging
```

kondisi sistem masih normal.

Karena script menggunakan threshold 20%, sedangkan memori tersedia masih di atas 20%, maka tidak dianggap kritis.

##### 3. Mengapa script menggunakan tee "$LAPORAN" bukan redirection biasa > "$LAPORAN"? Apa keuntungannya?
Perintah:

```bash
tee "$LAPORAN"
```

digunakan agar output:

- tampil di terminal
- sekaligus disimpan ke file laporan

Jika menggunakan:

```bash
> "$LAPORAN"
```

output hanya masuk ke file dan tidak tampil di layar.

##### 4. Dari output cek_paging, apakah ada aktivitas si atau so? Jika ada, apa implikasinya terhadap performa server?#### 
Nilai `si` dan `so` pada output `vmstat` semuanya:

```bash
0
```

Artinya tidak ada aktivitas swap masuk atau keluar.

Ini menunjukkan RAM masih cukup dan performa server masih stabil.

---
*Jobsheet 10 - Sistem Operasi*