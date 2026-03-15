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

*Jobsheet 4 - Sistem Operasi*