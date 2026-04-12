<h1 align="center">JOBSHEET 4 - SISTEM OPERASI</h1>


**Nama**       : M. Javier Thufail  
**NIM**        : 254107020019  
**Kelas**      : TI 1-G  
**No. Absen**  : 18  

---

## TUGAS PENDAHULUAN

Jawablah pertanyaan-pertanyaan di bawah ini:


#### 1. Apa yang dimaksud perintah-perintah direktori: `pwd`, `cd`, `mkdir`, `rmdir`?

- **pwd (Print Working Directory)**  
  Digunakan untuk menampilkan lokasi direktori kerja saat ini.

- **cd (Change Directory)**  
  Digunakan untuk berpindah atau mengubah direktori kerja.

- **mkdir (Make Directory)**  
  Digunakan untuk membuat direktori atau folder baru.

- **rmdir (Remove Directory)**  
  Digunakan untuk menghapus direktori yang kosong.


#### 2. Apa yang dimaksud perintah manipulasi file: `cp`, `mv`, dan `rm` (sertakan formatnya)

- **cp (Copy)**  
  Digunakan untuk menyalin file atau direktori ke lokasi lain.  

  Format:
  ```bash
  cp [opsi] sumber tujuan
  ```

- **mv (Move)**  
  Digunakan untuk memindahkan atau mengganti nama file/direktori.  

  Format:
  ```bash
  mv [opsi] sumber tujuan
  ```

- **rm (Remove)**  
  Digunakan untuk menghapus file atau direktori.  

  Format:
  ```bash
  rm [opsi] nama_file
  ```


#### 3. Jelaskan perbedaan Symbolic Link menggunakan Hard Link dan Soft Link

- **Hard Link (Direct Link)**  
  Hard link membuat dua nama file yang menunjuk ke data yang sama pada disk. Jika salah satu file diubah, perubahan juga terlihat pada file lainnya karena keduanya menunjuk ke inode yang sama.

- **Soft Link / Symbolic Link (Indirect Link)**  
  Soft link adalah file yang berisi referensi atau alamat ke file asli. Jika file asli dihapus, maka link tersebut menjadi rusak (broken link).


#### 4. Tuliskan maksud perintah-perintah: `file`, `find`, `which`, `locate`, dan `grep`

- **file**  
  Digunakan untuk mengetahui jenis atau tipe suatu file.

- **find**  
  Digunakan untuk mencari file atau direktori dalam sistem berdasarkan nama, ukuran, tipe, dan kriteria lainnya.

- **which**  
  Digunakan untuk mengetahui lokasi atau path dari suatu program yang dapat dijalankan.

- **locate**  
  Digunakan untuk mencari file dengan cepat menggunakan database indeks sistem.

- **grep**  
  Digunakan untuk mencari baris teks dalam file yang sesuai dengan pola (pattern) tertentu.

---

### Percobaan 1 : Direktori

---

#### 1. Melihat direktori HOME

Perintah:

```bash
pwd
echo $HOME
```

Output:

```
vier@UBUNTU:~/praktikum-os/week04$ pwd
/home/vier/praktikum-os/week04

vier@UBUNTU:~/praktikum-os/week04$ echo $home

vier@UBUNTU:~/praktikum-os/week04$ echo $HOME
/home/vier
```

Penjelasan:  
Perintah `pwd` menampilkan direktori kerja saat ini. Variabel lingkungan `$HOME` menunjukkan direktori home pengguna. Variabel bersifat **case sensitive**, sehingga `$home` tidak menghasilkan output.

---

#### 2. Melihat direktori aktual dan parent direktori

Perintah:

```bash
pwd
cd .
pwd
cd ..
pwd
cd
```

Output:

```
vier@UBUNTU:~/praktikum-os/week04$ pwd
/home/vier/praktikum-os/week04

vier@UBUNTU:~/praktikum-os/week04$ cd .

vier@UBUNTU:~/praktikum-os/week04$ pwd
/home/vier/praktikum-os/week04

vier@UBUNTU:~/praktikum-os/week04$ cd ..
vier@UBUNTU:~/praktikum-os$ pwd
/home/vier/praktikum-os

vier@UBUNTU:~/praktikum-os$ cd
vier@UBUNTU:~$
```

Penjelasan:  
- `cd .` tetap berada di direktori saat ini.  
- `cd ..` berpindah ke direktori **parent**.  
- `cd` tanpa argumen akan kembali ke **home directory**.

---

#### 3. Membuat satu atau lebih direktori serta subdirektori

Perintah:

```bash
pwd
mkdir A B C A/D A/E B/F A/D/A
ls -1
ls -1 A
ls -1 A/D
```

Output:
```
vier@UBUNTU:~/praktikum-os/week04$ pwd
/home/vier/praktikum-os/week04

vier@UBUNTU:~/praktikum-os/week04$ mkdir A B C A/D A/E B/F A/D/A

vier@UBUNTU:~/praktikum-os/week04$ ls -l
total 12
drwxrwxr-x 4 vier vier 4096 Mar 11 09:24 A
drwxrwxr-x 3 vier vier 4096 Mar 11 09:24 B
drwxrwxr-x 2 vier vier 4096 Mar 11 09:24 C

vier@UBUNTU:~/praktikum-os/week04$ ls -l A
total 8
drwxrwxr-x 3 vier vier 4096 Mar 11 09:24 D
drwxrwxr-x 2 vier vier 4096 Mar 11 09:24 E

vier@UBUNTU:~/praktikum-os/week04$ ls -l A/D
total 4
drwxrwxr-x 2 vier vier 4096 Mar 11 09:24 A
```

Penjelasan:  
Perintah `mkdir` digunakan untuk membuat direktori baru. Dalam satu perintah dapat dibuat beberapa direktori sekaligus termasuk **subdirektori**.  
Perintah `ls -l` digunakan untuk menampilkan daftar file atau direktori dalam format **long listing**, yang menampilkan informasi seperti **permission, jumlah link, pemilik, ukuran file, dan waktu modifikasi**.

---

#### 4. Menghapus direktori

Perintah:

```bash
rmdir B
ls -l B
rmdir B/F B
ls -l B
```

Output:

```
vier@UBUNTU:~/praktikum-os/week04$ rmdir B
rmdir: failed to remove 'B': Directory not empty

vier@UBUNTU:~/praktikum-os/week04$ ls -l B
total 4
drwxrwxr-x 2 vier vier 4096 Mar 11 10:13 F

vier@UBUNTU:~/praktikum-os/week04$ rmdir B/F B

vier@UBUNTU:~/praktikum-os/week04$ ls -l B
ls: cannot access 'B': No such file or directory
```

Penjelasan:  
Perintah `rmdir` digunakan untuk menghapus direktori **yang kosong**.  
Ketika menjalankan `rmdir B`, sistem menampilkan pesan **Directory not empty** karena direktori **B** masih berisi subdirektori **F**. Setelah subdirektori **F** dihapus menggunakan `rmdir B/F`, maka direktori **B** menjadi kosong dan dapat dihapus dengan perintah `rmdir B`. Saat dilakukan `ls -l B`, muncul pesan **No such file or directory** yang menandakan bahwa direktori **B** sudah berhasil dihapus.

---

#### 5. Navigasi direktori menggunakan `cd`

Perintah:

```bash
pwd
ls -l
cd A
pwd
cd ..
pwd
cd /home/vier/praktikum-os/week04/C
pwd
cd /vier/c
pwd
```

Output:

```
vier@UBUNTU:~/praktikum-os/week04$ pwd
/home/vier/praktikum-os/week04

vier@UBUNTU:~/praktikum-os/week04$ ls -l
total 8
drwxrwxr-x 4 vier vier 4096 Mar 11 09:24 A
drwxrwxr-x 2 vier vier 4096 Mar 11 09:24 C

vier@UBUNTU:~/praktikum-os/week04$ cd A
vier@UBUNTU:~/praktikum-os/week04/A$ pwd
/home/vier/praktikum-os/week04/A

vier@UBUNTU:~/praktikum-os/week04/A$ cd ..
vier@UBUNTU:~/praktikum-os/week04$ pwd
/home/vier/praktikum-os/week04

vier@UBUNTU:~/praktikum-os/week04$ cd /home/vier/praktikum-os/week04/C
vier@UBUNTU:~/praktikum-os/week04/C$ pwd
/home/vier/praktikum-os/week04/C

vier@UBUNTU:~/praktikum-os/week04/C$ cd /vier/C
bash: cd: /vier/C: No such file or directory

vier@UBUNTU:~/praktikum-os/week04/C$ pwd
/home/vier/praktikum-os/week04/C
```

Penjelasan:  
Perintah `cd` digunakan untuk berpindah dari satu direktori ke direktori lain.  
- `cd A` berpindah ke direktori **A**.  
- `cd ..` kembali ke **direktori parent**.  
- `cd /home/vier/praktikum-os/week04/C` berpindah menggunakan **path absolut**.  

Error terjadi karena direktori `/vier/C` **tidak ada**. Direktori pengguna sebenarnya berada pada `/home/vier`, sehingga path yang benar harus dimulai dari `/home/vier`.

---

### Percobaan 2 : Manipulasi File

---

#### 1. Perintah `cp` untuk mengkopi file atau seluruh direktori

Perintah:

```bash
cat > contoh
Membuat sebuah file
[Ctrl+D]

cp contoh contoh1
ls -l
cp contoh A
ls -l A
cp contoh contoh1 A/D
ls -l A/D
```

Output:

```
vier@UBUNTU:~/praktikum-os/week04$ cat > contoh
Membuat sebuah file

vier@UBUNTU:~/praktikum-os/week04$ cp contoh contoh1

vier@UBUNTU:~/praktikum-os/week04$ ls -l
total 16
drwxrwxr-x 4 vier vier 4096 Mar 11 09:24 A
drwxrwxr-x 2 vier vier 4096 Mar 11 09:34 C
-rw-rw-r-- 1 vier vier   20 Mar 11 09:35 contoh
-rw-rw-r-- 1 vier vier   20 Mar 11 09:36 contoh1

vier@UBUNTU:~/praktikum-os/week04$ cp contoh A

vier@UBUNTU:~/praktikum-os/week04$ ls -l A
total 12
-rw-rw-r-- 1 vier vier   20 Mar 11 09:36 contoh
drwxrwxr-x 3 vier vier 4096 Mar 11 09:24 D
drwxrwxr-x 2 vier vier 4096 Mar 11 09:24 E

vier@UBUNTU:~/praktikum-os/week04$ cp contoh contoh1 A/D

vier@UBUNTU:~/praktikum-os/week04$ ls -l A/D
total 12
drwxrwxr-x 2 vier vier 4096 Mar 11 09:24 A
-rw-rw-r-- 1 vier vier   20 Mar 11 09:37 contoh
-rw-rw-r-- 1 vier vier   20 Mar 11 09:37 contoh1
```

Penjelasan:  
Perintah `cp` digunakan untuk menyalin file. File `contoh` disalin menjadi `contoh1`, kemudian disalin ke direktori `A`, dan selanjutnya kedua file disalin ke subdirektori `A/D`.

---

#### 2. Perintah `mv` untuk memindahkan file

Perintah:

```bash
mv contoh contoh2
ls -l
mv contoh1 contoh2 A/D
ls -l A/D
mv contoh contoh1 C
ls -l C
```

Output:

```
vier@UBUNTU:~/praktikum-os/week04$ mv contoh contoh2

vier@UBUNTU:~/praktikum-os/week04$ ls -l
total 12
drwxrwxr-x 4 vier vier 4096 Mar 11 09:45 A
drwxrwxr-x 2 vier vier 4096 Mar 11 09:45 C
-rw-rw-r-- 1 vier vier   20 Mar 11 09:48 contoh1
-rw-rw-r-- 1 vier vier   20 Mar 11 09:48 contoh2

vier@UBUNTU:~/praktikum-os/week04$ mv contoh1 contoh2 A/D

vier@UBUNTU:~/praktikum-os/week04$ ls -l A/D
total 16
drwxrwxr-x 2 vier vier 4096 Mar 11 09:45 A
-rw-rw-r-- 1 vier vier   20 Mar 11 09:48 contoh
-rw-rw-r-- 1 vier vier   20 Mar 11 09:48 contoh1
-rw-rw-r-- 1 vier vier   20 Mar 11 09:48 contoh2

vier@UBUNTU:~/praktikum-os/week04$ mv contoh contoh1 C
mv: cannot stat 'contoh': No such file or directory
mv: cannot stat 'contoh1': No such file or directory

vier@UBUNTU:~/praktikum-os/week04$ ls -l C
total 0
```

Penjelasan:  
Perintah `mv` digunakan untuk memindahkan atau mengganti nama file. Error terjadi karena file `contoh` dan `contoh1` sudah tidak berada di direktori saat ini karena telah dipindahkan ke direktori lain.

---

#### 3. Perintah `rm` untuk menghapus file

Perintah:

```bash
rm contoh2
ls -l
rm -i contoh
rm -rf A C
ls -l
```

Output:

```
vier@UBUNTU:~/praktikum-os/week04$ rm contoh2
rm: cannot remove 'contoh2': No such file or directory

vier@UBUNTU:~/praktikum-os/week04$ ls -l
total 8
drwxrwxr-x 4 vier vier 4096 Mar 11 09:48 A
drwxrwxr-x 2 vier vier 4096 Mar 11 09:45 C

vier@UBUNTU:~/praktikum-os/week04$ rm -i contoh
rm: cannot remove 'contoh': No such file or directory

vier@UBUNTU:~/praktikum-os/week04$ rm -rf A C

vier@UBUNTU:~/praktikum-os/week04$ ls -l
total 0
```

Penjelasan:  
Perintah `rm` digunakan untuk menghapus file atau direktori.  
`rm contoh2` gagal karena file tidak ditemukan.  
`rm -i` digunakan untuk menghapus file dengan konfirmasi.  
`rm -rf` digunakan untuk menghapus direktori beserta seluruh isinya secara rekursif.

---

### Percobaan 3 : Symbolic Link

---

#### 1. Membuat shortcut (file link)

Perintah:

```bash
echo "haloo apa khabar" > halo.txt
ls -l
ln halo.txt z
ls -l
cat z
mkdir mydir
ln z mydir/halo.juga
cat mydir/halo.juga
ln -s z bye.txt
ls -l bye.txt
cat bye.txt
```

Output:

```
vier@UBUNTU:~/praktikum-os/week04$ echo "haloo apa khabar" > halo.txt

vier@UBUNTU:~/praktikum-os/week04$ ls -l
total 12
drwxrwxr-x 4 vier vier 4096 Mar 11 10:13 A
drwxrwxr-x 2 vier vier 4096 Mar 11 10:13 C
-rw-rw-r-- 1 vier vier   17 Mar 15 06:09 halo.txt

vier@UBUNTU:~/praktikum-os/week04$ ln halo.txt z

vier@UBUNTU:~/praktikum-os/week04$ ls -l
total 16
drwxrwxr-x 4 vier vier 4096 Mar 11 10:13 A
drwxrwxr-x 2 vier vier 4096 Mar 11 10:13 C
-rw-rw-r-- 2 vier vier   17 Mar 15 06:09 halo.txt
-rw-rw-r-- 2 vier vier   17 Mar 15 06:09 z

vier@UBUNTU:~/praktikum-os/week04$ cat z
haloo apa khabar

vier@UBUNTU:~/praktikum-os/week04$ mkdir mydir

vier@UBUNTU:~/praktikum-os/week04$ ln z mydir/halo.juga

vier@UBUNTU:~/praktikum-os/week04$ cat mydir/halo.juga
haloo apa khabar

vier@UBUNTU:~/praktikum-os/week04$ ln -s z bye.txt

vier@UBUNTU:~/praktikum-os/week04$ ls -l bye.txt
lrwxrwxrwx 1 vier vier 1 Mar 15 06:12 bye.txt -> z

vier@UBUNTU:~/praktikum-os/week04$ cat bye.txt
haloo apa khabar
```

Penjelasan:

- `ln halo.txt z` membuat **hard link** bernama `z` yang menunjuk ke file `halo.txt`.  
- Hard link memiliki **inode yang sama**, sehingga perubahan pada salah satu file akan mempengaruhi file lainnya.  
- `ln z mydir/halo.juga` membuat hard link lain di dalam direktori `mydir`.  
- `ln -s z bye.txt` membuat **symbolic link (soft link)** bernama `bye.txt` yang menunjuk ke file `z`.  
- Symbolic link hanya berupa **referensi ke file asli**, sehingga jika file asli dihapus maka link akan menjadi rusak (broken link).

---

### Percobaan 4 : Melihat Isi File

---

Perintah:

```bash
ls -l
file halo.txt
file bye.txt
```

Output:

```
vier@UBUNTU:~/praktikum-os/week04$ ls -l
total 20
drwxrwxr-x 4 vier vier 4096 Mar 11 10:13 A
lrwxrwxrwx 1 vier vier    1 Mar 15 06:12 bye.txt -> z
drwxrwxr-x 2 vier vier 4096 Mar 11 10:13 C
-rw-rw-r-- 3 vier vier   17 Mar 15 06:09 halo.txt
drwxrwxr-x 2 vier vier 4096 Mar 15 06:12 mydir
-rw-rw-r-- 3 vier vier   17 Mar 15 06:09 z

vier@UBUNTU:~/praktikum-os/week04$ file halo.txt
halo.txt: ASCII text

vier@UBUNTU:~/praktikum-os/week04$ file bye.txt
bye.txt: symbolic link to z
```

Penjelasan:

- Perintah `ls -l` digunakan untuk menampilkan daftar file dan direktori beserta informasi detail seperti permission, jumlah link, pemilik, ukuran, dan waktu modifikasi.
- Perintah `file` digunakan untuk mengetahui jenis atau tipe dari suatu file.
- `halo.txt` dikenali sebagai **ASCII text**, artinya file tersebut berisi teks biasa.
- `bye.txt` dikenali sebagai **symbolic link** yang menunjuk ke file `z`.

---

### Percobaan 5 : Mencari File

---

#### 1. Perintah `find`

Perintah:

```bash
find /home/vier/praktikum-os -name "*.txt" -print > myerror.txt
cat myerror.txt
find . -name "*.txt" -exec wc -l {} \;
```

Output:

```
vier@UBUNTU:~/praktikum-os/week04$ find /home/vier/praktikum-os -name "*.txt" -print > myerror.txt
vier@UBUNTU:~/praktikum-os/week04$ cat myerror.txt

/home/vier/praktikum-os
/home/vier/praktikum-os/week01
/home/vier/praktikum-os/week03
/home/vier/praktikum-os/week03/error.log
/home/vier/praktikum-os/week03/backup-error.log
/home/vier/praktikum-os/week03/backup-20260303-134315.tar.gz
/home/vier/praktikum-os/week03/backup-success.log
/home/vier/praktikum-os/week03/large-logs.txt
/home/vier/praktikum-os/week03/conf-files.txt
/home/vier/praktikum-os/week03/sorted-users.txt
/home/vier/praktikum-os/week03/monitoring.log
/home/vier/praktikum-os/week02
/home/vier/praktikum-os/week02/config.txt
/home/vier/praktikum-os/week02/server.log
/home/vier/praktikum-os/week02/latihan.txt
/home/vier/praktikum-os/week02/data.log
/home/vier/praktikum-os/week02/notes.txt
/home/vier/praktikum-os/week04
/home/vier/praktikum-os/week04/C
/home/vier/praktikum-os/week04/A
/home/vier/praktikum-os/week04/A/D
/home/vier/praktikum-os/week04/A/D/A
/home/vier/praktikum-os/week04/A/E
/home/vier/praktikum-os/week04/halo.txt
/home/vier/praktikum-os/week04/myerror.txt
/home/vier/praktikum-os/week04/bye.txt
/home/vier/praktikum-os/week04/z
/home/vier/praktikum-os/week04/mydir
/home/vier/praktikum-os/week04/mydir/halo.juga
/home/vier/praktikum-os/data.log
```

Penjelasan:

- `find` digunakan untuk mencari file atau direktori dalam suatu path tertentu.
- Opsi `-name "*.txt"` digunakan untuk mencari file dengan ekstensi `.txt`.
- `-print` menampilkan hasil pencarian.
- `>` digunakan untuk menyimpan hasil ke file `myerror.txt`.
- `-exec wc -l {} \;` digunakan untuk menghitung jumlah baris pada setiap file yang ditemukan.

---

#### 2. Perintah `which`

Perintah:

```bash
which ls
```

Penjelasan:

- Perintah `which` digunakan untuk mengetahui lokasi program atau command yang dijalankan di sistem.
- Contoh `which ls` akan menampilkan lokasi dari perintah `ls`, biasanya berada di `/usr/bin/ls`.

---

#### 3. Perintah `locate`

Perintah:

```bash
locate "*.txt"
```

Penjelasan:

- Perintah `locate` digunakan untuk mencari file dengan cepat berdasarkan database yang telah diindeks sebelumnya.
- Hasil yang ditampilkan berupa path lengkap dari file yang sesuai dengan pola pencarian.

---

### Percobaan 6 : Mencari Text pada File

---

Perintah:

```bash
grep haloo *.txt
```

Output:

```
vier@UBUNTU:~/praktikum-os/week04$ grep haloo *.txt
bye.txt:haloo apa khabar
halo.txt:haloo apa khabar
```

Penjelasan:

- `grep` digunakan untuk mencari teks atau pola tertentu di dalam file.
- `haloo` adalah kata yang dicari.
- `*.txt` berarti pencarian dilakukan pada semua file dengan ekstensi `.txt`.
- Output menampilkan **nama file dan baris yang mengandung kata tersebut**.

---

## LATIHAN

### 1. Urutan Perintah Navigasi Direktori

Perintah yang dijalankan:

```bash
cd
pwd
ls -al
cd .
pwd
cd ..
pwd
ls -al
cd ..
pwd
ls -al
cd /etc
ls -al | more
cat passwd
cd -
pwd
```

Output:

```
vier@UBUNTU:~$ cd ~/praktikum-os/week04
vier@UBUNTU:~/praktikum-os/week04$ pwd
/home/vier/praktikum-os/week04

vier@UBUNTU:~/praktikum-os/week04$ ls -al
total 32
drwxrwxr-x 5 vier vier 4096 Mar 15 06:19 . 
drwxrwxr-x 6 vier vier 4096 Mar 4 04:01 .. 
drwxrwxr-x 4 vier vier 4096 Mar 11 10:13 A 
lrwxrwxrwx 1 vier vier 1 Mar 15 06:12 bye.txt -> z 
drwxrwxr-x 2 vier vier 4096 Mar 11 10:13 C 
-rw-rw-r-- 3 vier vier 17 Mar 15 06:09 halo.txt 
drwxrwxr-x 2 vier vier 4096 Mar 15 06:12 mydir 
-rw-rw-r-- 1 vier vier 1187 Mar 15 06:44 myerror.txt 
-rw-rw-r-- 3 vier vier 17 Mar 15 06:09 z

vier@UBUNTU:~/praktikum-os/week04$ cd .
vier@UBUNTU:~/praktikum-os/week04$ pwd
/home/vier/praktikum-os/week04

vier@UBUNTU:~/praktikum-os/week04$ cd ..
vier@UBUNTU:~/praktikum-os$ ls -al
total 28 
drwxrwxr-x 6 vier vier 4096 Mar 4 04:01 . 
drwxr-x--- 17 vier vier 4096 Mar 11 14:21 .. 
-rw-rw-r-- 1 vier vier 22 Feb 25 03:40 data.log 
drwxrwxr-x 2 vier vier 4096 Feb 25 03:35 week01 
drwxrwxr-x 2 vier vier 4096 Feb 25 09:23 week02 
drwxrwxr-x 2 vier vier 4096 Mar 3 13:43 week03 
drwxrwxr-x 5 vier vier 4096 Mar 15 06:19 week04

vier@UBUNTU:~/praktikum-os$ cd ..
vier@UBUNTU:~$ pwd
/home/vier

vier@UBUNTU:~$ ls -al
drwxr-x--- 17 vier vier 4096 Mar 11 14:21 .
drwxr-xr-x  3 root root 4096 Feb 15 15:34 ..
-rw-------  1 vier vier 5846 Apr  4 13:19 .bash_history
-rw-r--r--  1 vier vier  220 Mar 31  2024 .bash_logout
-rw-r--r--  1 vier vier 3771 Mar 31  2024 .bashrc
drwx------ 10 vier vier 4096 Feb 24 10:26 .cache
drwx------ 16 vier vier 4096 Feb 25 05:19 .config
drwxr-xr-x  2 vier vier 4096 Feb 15 15:34 Desktop
drwxr-xr-x  2 vier vier 4096 Feb 15 15:34 Documents
drwxr-xr-x  2 vier vier 4096 Feb 15 15:34 Downloads
drwx------  2 vier vier 4096 Apr  4 12:57 .gnupg
-rw-------  1 vier vier   20 Feb 25 09:51 .lesshst
drwx------  4 vier vier 4096 Feb 15 15:34 .local
drwxr-xr-x  2 vier vier 4096 Feb 15 15:34 Music
drwxr-xr-x  2 vier vier 4096 Feb 15 15:34 Pictures
drwxrwxr-x  6 vier vier 4096 Mar  4 04:01 praktikum-os
-rw-r--r--  1 vier vier  807 Mar 31  2024 .profile
drwxr-xr-x  2 vier vier 4096 Feb 15 15:34 Public
drwx------  5 vier vier 4096 Feb 25 04:18 snap
drwx------  2 vier vier 4096 Feb 15 15:34 .ssh
-rw-r--r--  1 vier vier    0 Feb 24 10:54 .sudo_as_admin_successful
drwxr-xr-x  2 vier vier 4096 Feb 15 15:34 Templates
drwxr-xr-x  2 vier vier 4096 Feb 15 15:34 Videos

vier@UBUNTU:~$ cd /etc
vier@UBUNTU:/etc$ ls -al | more
total 1156
drwxr-xr-x 140 root                 root                 12288 Feb 24 11:03 .
drwxr-xr-x  23 root                 root                  4096 Feb 15 15:25 ..
-rw-r--r--   1 root                 root                  3444 Jul  5  2023 adduser.conf
drwxr-xr-x   3 root                 root                  4096 Feb 10 00:28 alsa
drwxr-xr-x   2 root                 root                  4096 Feb 24 11:03 alternatives
-rw-r--r--   1 root                 root                   335 Apr  8  2024 anacrontab
-rw-r--r--   1 root                 root                   433 Apr  8  2024 apg.conf
drwxr-xr-x   5 root                 root                  4096 Feb 10 00:27 apm
drwxr-xr-x   2 root                 root                  4096 Feb 10 00:27 apparmor
drwxr-xr-x   9 root                 root                  4096 Feb 10 00:31 apparmor.d
drwxr-xr-x   3 root                 root                  4096 Feb 10 00:29 apport
drwxr-xr-x   9 root                 root                  4096 Feb 15 15:25 apt
drwxr-xr-x   3 root                 root                  4096 Feb 10 00:29 avahi
-rw-r--r--   1 root                 root                  2319 Mar 31  2024 bash.bashrc
-rw-r--r--   1 root                 root                    45 Jan 24  2020 bash_completion
-rw-r--r--   1 root                 root                   367 Aug  2  2022 bindresvport.blacklist
drwxr-xr-x   2 root                 root                  4096 Apr 19  2024 binfmt.d
drwxr-xr-x   2 root                 root                  4096 Feb 10 00:29 bluetooth
-rw-r-----   1 root                 root                    33 Feb 10 00:31 brlapi.key
drwxr-xr-x   7 root                 root                  4096 Feb 10 00:28 brltty
-rw-r--r--   1 root                 root                 30571 Mar 31  2024 brltty.conf
drwxr-xr-x   3 root                 root                  4096 Feb 10 00:19 ca-certificates
-rw-r--r--   1 root                 root                  6288 Feb 10 00:20 ca-certificates.conf
drwxr-s---   2 root                 dip                   4096 Feb 10 00:29 chatscripts
drwxr-xr-x   5 root                 root                  4096 Feb 15 15:34 cloud
drwxr-xr-x   2 colord               colord                4096 Feb 15 15:34 colord
drwxr-xr-x   2 root                 root                  4096 Feb 15 15:30 console-setup
drwxr-xr-x   2 root                 root                  4096 Feb 10 00:29 cracklib
drwx------   2 root                 root                  4096 Apr 19  2024 credstore
drwx------   2 root                 root                  4096 Apr 19  2024 credstore.encrypted
drwxr-xr-x   2 root                 root                  4096 Feb 10 00:29 cron.d
drwxr-xr-x   2 root                 root                  4096 Feb 10 00:29 cron.daily

vier@UBUNTU:/etc$ cat passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin
_apt:x:42:65534::/nonexistent:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:998:998:systemd Network Management:/:/usr/sbin/nologin
systemd-timesync:x:996:996:systemd Time Synchronization:/:/usr/sbin/nologin
dhcpcd:x:100:65534:DHCP Client Daemon,,,:/usr/lib/dhcpcd:/bin/false
messagebus:x:101:101::/nonexistent:/usr/sbin/nologin
syslog:x:102:102::/nonexistent:/usr/sbin/nologin
systemd-resolve:x:991:991:systemd Resolver:/:/usr/sbin/nologin
uuidd:x:103:103::/run/uuidd:/usr/sbin/nologin
usbmux:x:104:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
tss:x:105:105:TPM software stack,,,:/var/lib/tpm:/bin/false
systemd-oom:x:990:990:systemd Userspace OOM Killer:/:/usr/sbin/nologin
kernoops:x:106:65534:Kernel Oops Tracking Daemon,,,:/:/usr/sbin/nologin
whoopsie:x:107:109::/nonexistent:/bin/false
dnsmasq:x:999:65534:dnsmasq:/var/lib/misc:/usr/sbin/nologin
avahi:x:108:111:Avahi mDNS daemon,,,:/run/avahi-daemon:/usr/sbin/nologin
tcpdump:x:109:112::/nonexistent:/usr/sbin/nologin
sssd:x:110:113:SSSD system user,,,:/var/lib/sss:/usr/sbin/nologin
speech-dispatcher:x:111:29:Speech Dispatcher,,,:/run/speech-dispatcher:/bin/false
cups-pk-helper:x:112:114:user for cups-pk-helper service,,,:/nonexistent:/usr/sbin/nologin
fwupd-refresh:x:989:989:Firmware update daemon:/var/lib/fwupd:/usr/sbin/nologin
saned:x:113:116::/var/lib/saned:/usr/sbin/nologin
geoclue:x:114:117::/var/lib/geoclue:/usr/sbin/nologin
cups-browsed:x:115:114::/nonexistent:/usr/sbin/nologin
hplip:x:116:7:HPLIP system user,,,:/run/hplip:/bin/false
gnome-remote-desktop:x:988:988:GNOME Remote Desktop:/var/lib/gnome-remote-desktop:/usr/sbin/nologin
polkitd:x:987:987:User for polkitd:/:/usr/sbin/nologin
rtkit:x:117:119:RealtimeKit,,,:/proc:/usr/sbin/nologin
colord:x:118:120:colord colour management daemon,,,:/var/lib/colord:/usr/sbin/nologin
gnome-initial-setup:x:119:65534::/run/gnome-initial-setup/:/bin/false
gdm:x:120:121:Gnome Display Manager:/var/lib/gdm3:/bin/false
nm-openvpn:x:121:122:NetworkManager OpenVPN,,,:/var/lib/openvpn/chroot:/usr/sbin/nologin
vier:x:1000:1000:vier:/home/vier:/bin/bash

vier@UBUNTU:/etc$ cd -
/home/vier

vier@UBUNTU:~$ pwd
/home/vier
```

#### Penjelasan:

- `cd` → berpindah ke direktori home.
- `pwd` → menampilkan direktori saat ini.
- `ls -al` → menampilkan daftar file secara detail termasuk file tersembunyi.
- `cd .` → tetap di direktori saat ini.
- `cd ..` → berpindah ke direktori parent.
- `cd /etc` → berpindah ke direktori `/etc`.
- `ls -al | more` → menampilkan isi direktori per halaman.
- `cat passwd` → menampilkan isi file `passwd`.
- `cd -` → kembali ke direktori sebelumnya.
- `pwd` → memastikan direktori saat ini.
---

### 2. Penelusuran Pohon Sistem File

Penelusuran direktori dilakukan menggunakan perintah `cd`, `ls`, `pwd`, dan `cat` pada direktori `/bin`, `/usr/bin`, `/sbin`, `/tmp`, dan `/boot`.

#### a. Direktori /bin

Perintah:

```bash
cd /bin
pwd
ls -al | head -10
cat aconnect
```

Output:

```
vier@UBUNTU:~$ cd /bin
vier@UBUNTU:/bin$ pwd
/bin

vier@UBUNTU:/bin$ ls -al | head -10
total 192812
drwxr-xr-x  2 root root       61440 Feb 24 12:00 .
drwxr-xr-x 12 root root        4096 Feb 10 00:19 ..
-rwxr-xr-x  1 root root       55744 Jun 22  2025 [
-rwxr-xr-x  1 root root       14640 Mar 31  2024 411toppm
-rwxr-xr-x  1 root root       18744 Aug 15  2025 aa-enabled
-rwxr-xr-x  1 root root       18744 Aug 15  2025 aa-exec
-rwxr-xr-x  1 root root       18736 Aug 15  2025 aa-features-abi
-rwxr-xr-x  1 root root       22912 Apr  7  2024 aconnect
-rwxr-xr-x  1 root root        1622 Jan 13 13:56 acpidbg
```

Penjelasan:  
Direktori `/bin` berisi program atau perintah penting yang digunakan oleh sistem dan pengguna, seperti `ls`, `cp`, `mv`, `cat`, dan lain-lain.

#### b. Direktori /usr/bin

Perintah:

```bash
cd /usr/bin
pwd
ls -l | head -5
```

Output:

```
vier@UBUNTU:/usr/bin$ pwd
/usr/bin

vier@UBUNTU:/usr/bin$ ls -l | head -5
total 192744
-rwxr-xr-x 1 root root       55744 Jun 22  2025 [
-rwxr-xr-x 1 root root       14640 Mar 31  2024 411toppm
-rwxr-xr-x 1 root root       18744 Aug 15  2025 aa-enabled
-rwxr-xr-x 1 root root       18744 Aug 15  2025 aa-exec
```

Penjelasan:  
Direktori `/usr/bin` berisi program aplikasi tambahan dan utilitas yang digunakan oleh user, seperti editor, compiler, dan tools lainnya.

#### c. Direktori /sbin

Perintah:

```bash
cd /sbin
pwd
ls -l | head -5
cat adduser
```

Output:

```
vier@UBUNTU:/sbin$ pwd
/sbin

vier@UBUNTU:/sbin$ ls -l | head -5
total 38608
-rwxr-xr-x 1 root root     39680 Aug 15  2025 aa-load
-rwxr-xr-x 1 root root      3225 Aug 15  2025 aa-remove-unknown
-rwxr-xr-x 1 root root     40000 Aug 15  2025 aa-status
-rwxr-xr-x 1 root root       137 Apr 12  2024 aa-teardown
```

Penjelasan:  
Direktori `/sbin` berisi program sistem yang digunakan untuk administrasi sistem seperti `adduser`, `reboot`, `fsck`, dan lain-lain.

#### d. Direktori /tmp

Perintah:

```bash
cd /tmp
pwd
ls -l | head -5
cat snap-private-tmp
```

Output:

```
vier@UBUNTU:/tmp$ pwd
/tmp

vier@UBUNTU:/tmp$ ls -l | head -5
total 48
drwx------ 6 root root 4096 Apr  4 13:35 snap-private-tmp
drwx------ 3 root root 4096 Apr  4 12:56 systemd-private-xxxx
```

Penjelasan:  
Direktori `/tmp` digunakan untuk menyimpan file sementara. Beberapa file atau folder tidak dapat dibuka karena tidak memiliki izin akses (Permission denied).

#### e. Direktori /boot

Perintah:

```bash
cd /boot
pwd
ls -l | head -5
```

Output:

```
vier@UBUNTU:/boot$ pwd
/boot

vier@UBUNTU:/boot$ ls -l | head -5
total 101648
-rw-r--r-- 1 root root   302820 Jan 15 13:44 config-6.17.0-14-generic
drwxr-xr-x 5 root root     4096 Feb 15 15:33 grub
lrwxrwxrwx 1 root root       28 Feb 15 15:31 initrd.img -> initrd.img-6.17.0-14-generic
-rw-r--r-- 1 root root 75979108 Feb 15 15:32 initrd.img-6.17.0-14-generic
```

Penjelasan:  
Direktori `/boot` berisi file yang digunakan untuk proses booting sistem Linux seperti kernel, initrd, dan konfigurasi boot loader (GRUB).

#### Kesimpulan Penelusuran Sistem File

Setiap direktori pada Linux memiliki fungsi masing-masing:
- `/bin` → berisi perintah dasar Linux
- `/usr/bin` → berisi program aplikasi dan utilitas user
- `/sbin` → berisi perintah administrasi sistem
- `/tmp` → berisi file sementara
- `/boot` → berisi file untuk proses booting sistem
---

### 3. Telusuri direktori /dev

#### Perintah
```bash
cd /dev
pwd
ls -l | head -10
who am i
ls -l
```

#### Output
```bash
vier@UBUNTU:/boot$ cd /dev
vier@UBUNTU:/dev$ pwd
/dev
vier@UBUNTU:/dev$ ls -l | head -10
total 0
crw-r--r--  1 root root     10, 235 Apr  4 12:55 autofs
drwxr-xr-x  2 root root         440 Apr  4 13:04 block
drwxr-xr-x  2 root root          80 Apr  4 12:55 bsg
crw-------  1 root root     10, 234 Apr  4 12:55 btrfs-control
drwxr-xr-x  3 root root          60 Apr  4 12:55 bus
lrwxrwxrwx  1 root root           3 Apr  4 12:55 cdrom -> sr0
drwxr-xr-x  2 root root        3660 Apr  4 13:04 char
crw-------  1 root root      5,   1 Apr  4 12:55 console
lrwxrwxrwx  1 root root          11 Apr  4 12:55 core -> /proc/kcore
vier@UBUNTU:/dev$ who am i
vier@UBUNTU:/dev$ ls -l
total 0
crw-r--r--  1 root root     10, 235 Apr  4 12:55 autofs
drwxr-xr-x  2 root root         440 Apr  4 13:04 block
drwxr-xr-x  2 root root          80 Apr  4 12:55 bsg
crw-------  1 root root     10, 234 Apr  4 12:55 btrfs-control
drwxr-xr-x  3 root root          60 Apr  4 12:55 bus
lrwxrwxrwx  1 root root           3 Apr  4 12:55 cdrom -> sr0
drwxr-xr-x  2 root root        3660 Apr  4 13:04 char
crw-------  1 root root      5,   1 Apr  4 12:55 console
lrwxrwxrwx  1 root root          11 Apr  4 12:55 core -> /proc/kcore
drwxr-xr-x  6 root root         120 Apr  4 12:55 cpu
crw-------  1 root root     10, 260 Apr  4 12:55 cpu_dma_latency
crw-------  1 root root     10, 203 Apr  4 12:55 cuse
drwxr-xr-x  9 root root         180 Apr  4 12:55 disk
drwxr-xr-x  2 root root          60 Apr  4 12:55 dma_heap
drwxr-xr-x  3 root root         100 Apr  4 12:55 dri
crw-------  1 root root     10, 258 Apr  4 12:55 ecryptfs
crw-rw----  1 root video    29,   0 Apr  4 12:55 fb0
lrwxrwxrwx  1 root root          13 Apr  4 12:55 fd -> /proc/self/fd
crw-rw-rw-  1 root root      1,   7 Apr  4 12:55 full
crw-rw-rw-  1 root root     10, 229 Apr  4 12:55 fuse
crw-------  1 root root     10, 228 Apr  4 12:55 hpet
drwxr-xr-x  2 root root           0 Apr  4 12:55 hugepages
crw-------  1 root root     10, 183 Apr  4 12:55 hwrng
crw-------  1 root root     89,   0 Apr  4 12:55 i2c-0
lrwxrwxrwx  1 root root          12 Apr  4 12:55 initctl -> /run/initctl
drwxr-xr-x  3 root root         260 Apr  4 13:04 input
crw-r--r--  1 root root      1,  11 Apr  4 12:55 kmsg
lrwxrwxrwx  1 root root          28 Apr  4 12:55 log -> /run/systemd/journal/dev-log
brw-rw----  1 root disk      7,   0 Apr  4 12:55 loop0
brw-rw----  1 root disk      7,   1 Apr  4 12:55 loop1
brw-rw----  1 root disk      7,  10 Apr  4 12:55 loop10
brw-rw----  1 root disk      7,  11 Apr  4 12:55 loop11
brw-rw----  1 root disk      7,  12 Apr  4 13:01 loop12
brw-rw----  1 root disk      7,  13 Apr  4 13:02 loop13
brw-rw----  1 root disk      7,  14 Apr  4 13:03 loop14
brw-rw----  1 root disk      7,  15 Apr  4 13:04 loop15
brw-rw----  1 root disk      7,   2 Apr  4 12:55 loop2
brw-rw----  1 root disk      7,   3 Apr  4 12:55 loop3
brw-rw----  1 root disk      7,   4 Apr  4 12:55 loop4
brw-rw----  1 root disk      7,   5 Apr  4 12:55 loop5
brw-------  1 root root      7,   6 Apr  4 12:55 loop6
brw-rw----  1 root disk      7,   7 Apr  4 12:55 loop7
brw-rw----  1 root disk      7,   8 Apr  4 12:55 loop8
brw-rw----  1 root disk      7,   9 Apr  4 12:55 loop9
crw-rw----  1 root disk     10, 237 Apr  4 12:55 loop-control
drwxr-xr-x  2 root root          60 Apr  4 12:55 mapper
crw-------  1 root root     10, 227 Apr  4 12:55 mcelog
crw-r-----  1 root kmem      1,   1 Apr  4 12:55 mem
drwxrwxrwt  2 root root          40 Apr  4 12:55 mqueue
drwxr-xr-x  2 root root          60 Apr  4 12:55 net
crw-rw-rw-  1 root root      1,   3 Apr  4 12:55 null
crw-------  1 root root     10, 144 Apr  4 12:55 nvram
crw-r-----  1 root kmem      1,   4 Apr  4 12:55 port
crw-------  1 root root    108,   0 Apr  4 12:55 ppp
crw-------  1 root root     10,   1 Apr  4 12:55 psaux
crw-rw-rw-  1 root tty       5,   2 Apr  4 14:58 ptmx
drwxr-xr-x  2 root root           0 Apr  4 12:55 pts
crw-rw-rw-  1 root root      1,   8 Apr  4 12:55 random
crw-rw-r--+ 1 root root     10, 242 Apr  4 12:55 rfkill
lrwxrwxrwx  1 root root           4 Apr  4 12:55 rtc -> rtc0
crw-------  1 root root    247,   0 Apr  4 12:55 rtc0
brw-rw----  1 root disk      8,   0 Apr  4 12:55 sda
brw-rw----  1 root disk      8,   1 Apr  4 12:55 sda1
brw-rw----  1 root disk      8,   2 Apr  4 12:55 sda2
crw-rw----+ 1 root cdrom    21,   0 Apr  4 12:55 sg0
crw-rw----  1 root disk     21,   1 Apr  4 12:55 sg1
drwxrwxrwt  2 root root          40 Apr  4 12:55 shm
crw-------  1 root root     10, 231 Apr  4 12:55 snapshot
drwxr-xr-x  3 root root         180 Apr  4 12:55 snd
brw-rw----+ 1 root cdrom    11,   0 Apr  4 12:55 sr0
lrwxrwxrwx  1 root root          15 Apr  4 12:55 stderr -> /proc/self/fd/2
lrwxrwxrwx  1 root root          15 Apr  4 12:55 stdin -> /proc/self/fd/0
lrwxrwxrwx  1 root root          15 Apr  4 12:55 stdout -> /proc/self/fd/1
crw-rw-rw-  1 root tty       5,   0 Apr  4 12:55 tty
crw--w----  1 root tty       4,   0 Apr  4 12:56 tty0
crw--w----  1 root tty       4,   1 Apr  4 12:56 tty1
crw--w----  1 root tty       4,  10 Apr  4 12:55 tty10
crw--w----  1 root tty       4,  11 Apr  4 12:55 tty11
crw--w----  1 root tty       4,  12 Apr  4 12:55 tty12
crw--w----  1 root tty       4,  13 Apr  4 12:55 tty13
crw--w----  1 root tty       4,  14 Apr  4 12:55 tty14
crw--w----  1 root tty       4,  15 Apr  4 12:55 tty15
crw--w----  1 root tty       4,  16 Apr  4 12:55 tty16
crw--w----  1 root tty       4,  17 Apr  4 12:55 tty17
crw--w----  1 root tty       4,  18 Apr  4 12:55 tty18
crw--w----  1 root tty       4,  19 Apr  4 12:55 tty19
crw--w----  1 vier tty       4,   2 Apr  4 12:56 tty2
crw--w----  1 root tty       4,  20 Apr  4 12:55 tty20
crw--w----  1 root tty       4,  21 Apr  4 12:55 tty21
crw--w----  1 root tty       4,  22 Apr  4 12:55 tty22
crw--w----  1 root tty       4,  23 Apr  4 12:55 tty23
crw--w----  1 root tty       4,  24 Apr  4 12:55 tty24
crw--w----  1 root tty       4,  25 Apr  4 12:55 tty25
crw--w----  1 root tty       4,  26 Apr  4 12:55 tty26
crw--w----  1 root tty       4,  27 Apr  4 12:55 tty27
crw--w----  1 root tty       4,  28 Apr  4 12:55 tty28
crw--w----  1 root tty       4,  29 Apr  4 12:55 tty29
crw--w----  1 root tty       4,   3 Apr  4 12:55 tty3
crw--w----  1 root tty       4,  30 Apr  4 12:55 tty30
crw--w----  1 root tty       4,  31 Apr  4 12:55 tty31
crw--w----  1 root tty       4,  32 Apr  4 12:55 tty32
crw--w----  1 root tty       4,  33 Apr  4 12:55 tty33
crw--w----  1 root tty       4,  34 Apr  4 12:55 tty34
crw--w----  1 root tty       4,  35 Apr  4 12:55 tty35
crw--w----  1 root tty       4,  36 Apr  4 12:55 tty36
crw--w----  1 root tty       4,  37 Apr  4 12:55 tty37
crw--w----  1 root tty       4,  38 Apr  4 12:55 tty38
crw--w----  1 root tty       4,  39 Apr  4 12:55 tty39
crw--w----  1 root tty       4,   4 Apr  4 12:55 tty4
crw--w----  1 root tty       4,  40 Apr  4 12:55 tty40
crw--w----  1 root tty       4,  41 Apr  4 12:55 tty41
crw--w----  1 root tty       4,  42 Apr  4 12:55 tty42
crw--w----  1 root tty       4,  43 Apr  4 12:55 tty43
crw--w----  1 root tty       4,  44 Apr  4 12:55 tty44
crw--w----  1 root tty       4,  45 Apr  4 12:55 tty45
crw--w----  1 root tty       4,  46 Apr  4 12:55 tty46
crw--w----  1 root tty       4,  47 Apr  4 12:55 tty47
crw--w----  1 root tty       4,  48 Apr  4 12:55 tty48
crw--w----  1 root tty       4,  49 Apr  4 12:55 tty49
crw--w----  1 root tty       4,   5 Apr  4 12:55 tty5
crw--w----  1 root tty       4,  50 Apr  4 12:55 tty50
crw--w----  1 root tty       4,  51 Apr  4 12:55 tty51
crw--w----  1 root tty       4,  52 Apr  4 12:55 tty52
crw--w----  1 root tty       4,  53 Apr  4 12:55 tty53
crw--w----  1 root tty       4,  54 Apr  4 12:55 tty54
crw--w----  1 root tty       4,  55 Apr  4 12:55 tty55
crw--w----  1 root tty       4,  56 Apr  4 12:55 tty56
crw--w----  1 root tty       4,  57 Apr  4 12:55 tty57
crw--w----  1 root tty       4,  58 Apr  4 12:55 tty58
crw--w----  1 root tty       4,  59 Apr  4 12:55 tty59
crw--w----  1 root tty       4,   6 Apr  4 12:55 tty6
crw--w----  1 root tty       4,  60 Apr  4 12:55 tty60
crw--w----  1 root tty       4,  61 Apr  4 12:55 tty61
crw--w----  1 root tty       4,  62 Apr  4 12:55 tty62
crw--w----  1 root tty       4,  63 Apr  4 12:55 tty63
crw--w----  1 root tty       4,   7 Apr  4 12:55 tty7
crw--w----  1 root tty       4,   8 Apr  4 12:55 tty8
crw--w----  1 root tty       4,   9 Apr  4 12:55 tty9
crw-------  1 root root      5,   3 Apr  4 12:55 ttyprintk
crw-rw----  1 root dialout   4,  64 Apr  4 12:55 ttyS0
crw-rw----  1 root dialout   4,  65 Apr  4 12:55 ttyS1
crw-rw----  1 root dialout   4,  74 Apr  4 12:55 ttyS10
crw-rw----  1 root dialout   4,  75 Apr  4 12:55 ttyS11
crw-rw----  1 root dialout   4,  76 Apr  4 12:55 ttyS12
crw-rw----  1 root dialout   4,  77 Apr  4 12:55 ttyS13
crw-rw----  1 root dialout   4,  78 Apr  4 12:55 ttyS14
crw-rw----  1 root dialout   4,  79 Apr  4 12:55 ttyS15
crw-rw----  1 root dialout   4,  80 Apr  4 12:55 ttyS16
crw-rw----  1 root dialout   4,  81 Apr  4 12:55 ttyS17
crw-rw----  1 root dialout   4,  82 Apr  4 12:55 ttyS18
crw-rw----  1 root dialout   4,  83 Apr  4 12:55 ttyS19
crw-rw----  1 root dialout   4,  66 Apr  4 12:55 ttyS2
crw-rw----  1 root dialout   4,  84 Apr  4 12:55 ttyS20
crw-rw----  1 root dialout   4,  85 Apr  4 12:55 ttyS21
crw-rw----  1 root dialout   4,  86 Apr  4 12:55 ttyS22
crw-rw----  1 root dialout   4,  87 Apr  4 12:55 ttyS23
crw-rw----  1 root dialout   4,  88 Apr  4 12:55 ttyS24
crw-rw----  1 root dialout   4,  89 Apr  4 12:55 ttyS25
crw-rw----  1 root dialout   4,  90 Apr  4 12:55 ttyS26
crw-rw----  1 root dialout   4,  91 Apr  4 12:55 ttyS27
crw-rw----  1 root dialout   4,  92 Apr  4 12:55 ttyS28
crw-rw----  1 root dialout   4,  93 Apr  4 12:55 ttyS29
crw-rw----  1 root dialout   4,  67 Apr  4 12:55 ttyS3
crw-rw----  1 root dialout   4,  94 Apr  4 12:55 ttyS30
crw-rw----  1 root dialout   4,  95 Apr  4 12:55 ttyS31
crw-rw----  1 root dialout   4,  68 Apr  4 12:55 ttyS4
crw-rw----  1 root dialout   4,  69 Apr  4 12:55 ttyS5
crw-rw----  1 root dialout   4,  70 Apr  4 12:55 ttyS6
crw-rw----  1 root dialout   4,  71 Apr  4 12:55 ttyS7
crw-rw----  1 root dialout   4,  72 Apr  4 12:55 ttyS8
crw-rw----  1 root dialout   4,  73 Apr  4 12:55 ttyS9
crw-rw----  1 root kvm      10, 259 Apr  4 12:55 udmabuf
crw-------  1 root root     10, 239 Apr  4 12:55 uhid
crw-------  1 root root     10, 223 Apr  4 12:55 uinput
crw-rw-rw-  1 root root      1,   9 Apr  4 12:55 urandom
crw-------  1 root root     10, 257 Apr  4 12:55 userfaultfd
crw-------  1 root root     10, 240 Apr  4 12:55 userio
crw-------  1 root root     10, 261 Apr  4 12:55 vboxguest
crw-------  1 root root     10, 262 Apr  4 12:55 vboxuser
crw-rw----  1 root tty       7,   0 Apr  4 12:55 vcs
crw-rw----  1 root tty       7,   1 Apr  4 12:55 vcs1
crw-rw----  1 root tty       7,   2 Apr  4 12:55 vcs2
crw-rw----  1 root tty       7,   3 Apr  4 12:55 vcs3
crw-rw----  1 root tty       7,   4 Apr  4 12:55 vcs4
crw-rw----  1 root tty       7,   5 Apr  4 12:55 vcs5
crw-rw----  1 root tty       7,   6 Apr  4 12:55 vcs6
crw-rw----  1 root tty       7, 128 Apr  4 12:55 vcsa
crw-rw----  1 root tty       7, 129 Apr  4 12:55 vcsa1
crw-rw----  1 root tty       7, 130 Apr  4 12:55 vcsa2
crw-rw----  1 root tty       7, 131 Apr  4 12:55 vcsa3
crw-rw----  1 root tty       7, 132 Apr  4 12:55 vcsa4
crw-rw----  1 root tty       7, 133 Apr  4 12:55 vcsa5
crw-rw----  1 root tty       7, 134 Apr  4 12:55 vcsa6
crw-rw----  1 root tty       7,  64 Apr  4 12:55 vcsu
crw-rw----  1 root tty       7,  65 Apr  4 12:55 vcsu1
crw-rw----  1 root tty       7,  66 Apr  4 12:55 vcsu2
crw-rw----  1 root tty       7,  67 Apr  4 12:55 vcsu3
crw-rw----  1 root tty       7,  68 Apr  4 12:55 vcsu4
crw-rw----  1 root tty       7,  69 Apr  4 12:55 vcsu5
crw-rw----  1 root tty       7,  70 Apr  4 12:55 vcsu6
drwxr-xr-x  2 root root          60 Apr  4 12:55 vfio
crw-------  1 root root     10, 256 Apr  4 12:55 vga_arbiter
crw-------  1 root root     10, 137 Apr  4 12:55 vhci
crw-rw----  1 root kvm      10, 238 Apr  4 12:55 vhost-net
crw-rw----  1 root kvm      10, 241 Apr  4 12:55 vhost-vsock
crw-rw-rw-  1 root root      1,   5 Apr  4 12:55 zero
crw-------  1 root root     10, 249 Apr  4 12:55 zfs
```

#### Identifikasi TTY
```bash
crw--w----  1 vier tty 4, 2 Apr  4 12:56 tty2
```

#### Kesimpulan
Direktori `/dev` berisi file perangkat (device files) seperti harddisk, terminal, dan perangkat virtual lainnya.  
Terminal (tty) yang digunakan adalah **tty2** dan dimiliki oleh user **vier**.

---

### 4. Telusuri direktori /proc

#### Perintah
```bash
cd /proc
cat interrupts
cat devices
cat cpuinfo
cat meminfo
cat uptime
```

#### Penjelasan
Direktori /proc disebut pseudo-filesystem karena sistem file ini tidak disimpan di dalam harddisk, melainkan dibuat di atas RAM dan diatur langsung secara dinamis oleh kernel Linux. Itulah sebabnya kita bisa mengakses struktur data kernel dan melihat status hardware (seperti cpuinfo dan meminfo) secara real-time.

#### Output

#### interrupts
```bash
vier@UBUNTU:/proc$ cat interrupts
           CPU0       CPU1       CPU2       CPU3       
  0:        186          0          0          0  IO-APIC   2-edge      timer
  1:          0          0          0       5549  IO-APIC   1-edge      i8042
  8:          0          0          0          0  IO-APIC   8-edge      rtc0
  ...
```

#### devices
```bash
vier@UBUNTU:/proc$ cat devices
Character devices:
  1 mem
  4 tty
  5 /dev/tty
  7 vcs
 10 misc
 13 input
 21 sg
 29 fb
 ...
Block devices:
  7 loop
  8 sd
  9 md
 11 sr
 ...
```

#### cpuinfo
```bash
vier@UBUNTU:/proc$ cat cpuinfo
processor    : 0
vendor_id    : AuthenticAMD
model name   : AMD Ryzen 7 7730U with Radeon Graphics
cpu cores    : 4
...
```

#### meminfo
```bash
vier@UBUNTU:/proc$ cat meminfo
MemTotal:        4008056 kB
MemFree:          163576 kB
MemAvailable:    1938996 kB
Cached:          1805040 kB
...
```

#### uptime
```bash
vier@UBUNTU:/proc$ cat uptime
7871.46 28621.21
```

### Kesimpulan
Direktori `/proc` disebut pseudo-filesystem karena tidak tersimpan di disk, tetapi dibuat secara dinamis oleh kernel di memori (RAM). Direktori ini berisi informasi sistem dan kernel seperti interrupt, perangkat, CPU, memori, dan uptime yang dapat diakses secara real-time.```

---

### 5. Mengubah direktori home ke user lain menggunakan cd ~username

#### Perintah
```bash
cd ~vier
```

#### Output
```bash
vier@UBUNTU:/$ cd ~vier
vier@UBUNTU:~$
```

#### Penjelasan
Perintah `cd ~username` digunakan untuk langsung berpindah ke direktori home milik user tertentu tanpa harus mengetikkan path lengkapnya. Pada percobaan ini, perintah `cd ~vier` akan membawa kita ke direktori `/home/vier`.

---

### 6. Kembali ke direktori home sendiri

#### Perintah
```bash
cd /home
```

#### Output
```bash
vier@UBUNTU:~$ cd /home
vier@UBUNTU:/home$
```

#### Penjelasan
Perintah `cd /home` digunakan untuk berpindah ke direktori `/home`. Direktori ini berisi direktori home dari semua user yang ada pada sistem Linux.

---

### 7. Membuat subdirektori work dan play

#### Perintah
```bash
mkdir work play
ls -al
```

#### Output
```bash
vier@UBUNTU:~/praktikum-os/week04$ mkdir work play
vier@UBUNTU:~/praktikum-os/week04$ la -al
total 40
drwxrwxr-x 7 vier vier 4096 Apr  4 15:22 .
drwxrwxr-x 6 vier vier 4096 Mar  4 04:01 ..
drwxrwxr-x 4 vier vier 4096 Mar 11 10:13 A
lrwxrwxrwx 1 vier vier    1 Mar 15 06:12 bye.txt -> z
drwxrwxr-x 2 vier vier 4096 Mar 11 10:13 C
-rw-rw-r-- 3 vier vier   17 Mar 15 06:09 halo.txt
drwxrwxr-x 2 vier vier 4096 Mar 15 06:12 mydir
-rw-rw-r-- 1 vier vier 1187 Mar 15 06:44 myerror.txt
drwxrwxr-x 2 vier vier 4096 Apr  4 15:22 play
drwxrwxr-x 2 vier vier 4096 Apr  4 15:22 work
-rw-rw-r-- 3 vier vier   17 Mar 15 06:09 z
```

#### Penjelasan
Perintah `mkdir work play` digunakan untuk membuat dua direktori sekaligus, yaitu `work` dan `play` dalam direktori aktif.

---

### 8. Menghapus subdirektori work

#### Perintah
```bash
rmdir work
ls -al
```

#### Output
```bash
vier@UBUNTU:~/praktikum-os/week04$ rmdir work
vier@UBUNTU:~/praktikum-os/week04$ ls -al
total 36
drwxrwxr-x 6 vier vier 4096 Apr  4 15:24 .
drwxrwxr-x 6 vier vier 4096 Mar  4 04:01 ..
drwxrwxr-x 4 vier vier 4096 Mar 11 10:13 A
lrwxrwxrwx 1 vier vier    1 Mar 15 06:12 bye.txt -> z
drwxrwxr-x 2 vier vier 4096 Mar 11 10:13 C
-rw-rw-r-- 3 vier vier   17 Mar 15 06:09 halo.txt
drwxrwxr-x 2 vier vier 4096 Mar 15 06:12 mydir
-rw-rw-r-- 1 vier vier 1187 Mar 15 06:44 myerror.txt
drwxrwxr-x 2 vier vier 4096 Apr  4 15:22 play
-rw-rw-r-- 3 vier vier   17 Mar 15 06:09 z
```

#### Penjelasan
Perintah `rmdir work` digunakan untuk menghapus direktori kosong. Direktori `work` berhasil dihapus karena tidak berisi file.

---

### 9. Menyalin file /etc/passwd ke direktori home

#### Perintah
```bash
cp /etc/passwd ~
ls -l passwd
```

#### Output
```bash
vier@UBUNTU:~$ cp /etc/passwd ~
vier@UBUNTU:~$ ls -l passwd
-rw-r--r-- 1 vier vier 2858 Apr  4 15:26 passwd
```

#### Penjelasan
Perintah `cp /etc/passwd ~` digunakan untuk menyalin file `passwd` dari direktori `/etc` ke direktori home user. File tersebut berisi informasi akun pengguna pada sistem Linux.

---

### 10. Memindahkan file passwd ke subdirektori play

#### Perintah
```bash
mv ~/passwd ~/play
```

#### Output
```bash
vier@UBUNTU:~$ mv ~/passwd ~/play
```

#### Penjelasan
Perintah `mv` digunakan untuk memindahkan file `passwd` dari direktori home ke direktori `play`.

---

### 11. Membuat symbolic link bernama terminal yang menunjuk ke perangkat tty

#### Perintah
```bash
cd ~/praktikum-os/week04/play
ln -s /dev/pts/0 terminal
```

#### Output
```bash
vier@UBUNTU:~$ cd ~/praktikum-os/week04/play
vier@UBUNTU:~/praktikum-os/week04/play$ ln -s /dev/pts/0 terminal
```

#### Penjelasan
Perintah `ln -s /dev/pts/0 terminal` digunakan untuk membuat symbolic link bernama `terminal` yang menunjuk ke perangkat terminal (`tty`).

Jika melakukan hard link ke perangkat tty akan muncul pesan error. Hal ini karena sistem Linux tidak mengizinkan pembuatan hard link untuk file khusus demi keamanan sistem file.

---

### 12. Membuat file hello.txt berisi "hello world"

#### Perintah
```bash
echo "hello world" > hello.txt
cp terminal hello.txt
```

#### Output
```bash
vier@UBUNTU:~/praktikum-os/week04/play$ echo "hello world" > hello.txt
vier@UBUNTU:~/praktikum-os/week04/play$ cp terminal hello.txt
hello world
```

#### Penjelasan
Perintah `echo "hello world" > hello.txt` digunakan untuk membuat file `hello.txt` yang berisi teks "hello world".  
Perintah `cp terminal hello.txt` menggunakan symbolic link terminal sebagai sumber, sehingga menghasilkan efek yang sama karena terminal merupakan perangkat output.

---

### 13. Menyalin hello.txt ke terminal

#### Perintah
```bash
cp hello.txt terminal
```

#### Output
```bash
vier@UBUNTU:~/praktikum-os/week04/play$ cp terminal hello.txt
hello world
```

#### Penjelasan
Saat file `hello.txt` disalin ke terminal, sistem akan mencetak isi file tersebut ke layar terminal, yaitu "hello world".

---

### 14. Menyalin direktori play ke direktori work menggunakan symbolic link

#### Perintah
```bash
cd ~/praktikum-os/week04
ln -s play work
```

#### Output
```bash
vier@UBUNTU:~$ cd ~/praktikum-os/week04
vier@UBUNTU:~/praktikum-os/week04$ ln -s play work
```

#### Penjelasan
Perintah `ln -s play work` digunakan untuk membuat symbolic link bernama `work` yang menunjuk ke direktori `play`.

---

### 15. Menghapus direktori work dan isinya dengan satu perintah

#### Perintah
```bash
rm -rf work
```

#### Output
```bash
vier@UBUNTU:~/praktikum-os/week04$ rm -rf work
```

#### Penjelasan
Perintah `rm -rf work` digunakan untuk menghapus direktori `work` beserta seluruh isi di dalamnya secara rekursif dan paksa.

---

## LAPORAN RESMI

### 1. Analisa hasil percobaan yang Anda lakukan

#### a. Analisa setiap hasil tampilannya
Berdasarkan percobaan yang telah dilakukan, setiap perintah Linux yang digunakan menghasilkan tampilan yang berbeda sesuai dengan fungsinya.  
Perintah `pwd` menampilkan direktori aktif saat ini, `cd` digunakan untuk berpindah direktori, `mkdir` untuk membuat direktori baru, dan `rmdir` untuk menghapus direktori kosong.  

Perintah manipulasi file seperti `cp` digunakan untuk menyalin file, `mv` untuk memindahkan atau mengganti nama file, dan `rm` untuk menghapus file atau direktori.  

Pada percobaan link, symbolic link dapat dibuat menggunakan `ln -s` dan berfungsi sebagai shortcut yang menunjuk ke file asli. Sedangkan hard link tidak dapat dibuat pada perangkat khusus seperti `/dev/tty` karena alasan keamanan sistem file Linux.

Pada percobaan direktori `/proc`, terlihat bahwa file seperti `cpuinfo`, `meminfo`, dan `uptime` menampilkan informasi sistem secara real-time. Hal ini menunjukkan bahwa `/proc` merupakan pseudo-filesystem yang tidak tersimpan di harddisk melainkan di memori.


#### b. Pohon struktur file dan direktori
Struktur direktori yang dibuat pada percobaan dapat digambarkan sebagai berikut:

```
.
├── A
│   ├── D
│   │   └── A
│   └── E
├── B
│   └── F
├── C
```

Struktur di atas menunjukkan bahwa direktori dalam Linux tersusun secara hierarkis seperti pohon, dimana direktori dapat memiliki subdirektori di dalamnya.


#### c. Bila terdapat pesan error, jelaskan penyebabnya
Beberapa error yang muncul selama percobaan antara lain:

- **Permission denied** saat mencoba membuka file tertentu di `/tmp`, hal ini terjadi karena user tidak memiliki hak akses terhadap direktori atau file tersebut.
- Error saat membuat **hard link** ke perangkat `/dev/tty`, hal ini terjadi karena Linux tidak mengizinkan hard link untuk file khusus atau device demi menjaga keamanan dan konsistensi sistem file.
- Error saat menghapus direktori yang tidak kosong menggunakan `rmdir`, karena `rmdir` hanya dapat menghapus direktori kosong. Untuk direktori yang berisi file harus menggunakan `rm -r`.

---

### 2. Analisa latihan di atas dan hasil tampilannya
Berdasarkan latihan yang telah dilakukan, dapat dilihat bahwa sistem file Linux dapat dimanipulasi menggunakan berbagai perintah seperti membuat direktori, menghapus direktori, menyalin file, memindahkan file, serta membuat link.  
Hasil tampilan dari setiap perintah menunjukkan perubahan isi direktori sesuai dengan perintah yang dijalankan. Misalnya setelah menjalankan `mkdir`, direktori baru muncul pada hasil `ls`, setelah menjalankan `rm` file atau direktori akan hilang dari daftar, dan setelah membuat symbolic link akan muncul file dengan tanda panah yang menunjuk ke file tujuan.

---

### 3. Kesimpulan dari praktikum

- Organisasi file pada Linux memiliki struktur menyerupai pohon yang hierarkis, yang selalu diawali dari direktori paling dasar yaitu root. Di dalam root tersebut, kita dapat menciptakan file, direktori, hingga subdirektori ke bawah.
- Kita dapat memanipulasi dan menelusuri sistem file menggunakan instruksi baris perintah. Ini mencakup perintah direktori (`pwd`, `cd`, `mkdir`, `rmdir`), manipulasi file (`cp`, `mv`, `rm`), hingga perintah untuk mencari file dan isi teks di dalamnya (`find`, `which`, `locate`, `grep`).
- Linux memiliki teknik link untuk memberikan lebih dari satu nama pada data yang sama. Kita bisa membuat file duplikat yang identik dengan file asli (hard link), dan membuat file shortcut yang hanya menunjuk ke lokasi file asal (symbolic link).

---

*Jobsheet 4 - Sistem Operasi*