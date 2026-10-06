# Minpro-2-DDP-SistemManajemenProyekDesain

**Nama:** [Lithalia Geminifer Addawiyah]  
**NIM:** [2609116088]  
**Kelas:** [C]  

---

## 1. Deskripsi Singkat Program
Program ini merupakan sistem manajemen data proyek desain berbasis Command Line Interface (CLI) menggunakan bahasa Python. Program menerapkan *Role-Based Access Control* (RBAC) dengan dua peran pengguna:
* **Admin:** Memiliki akses penuh terhadap fitur CRUD (Create, Read, Update, Delete) data proyek.
* **User:** Memiliki hak akses terbatas untuk menampilkan seluruh data proyek dan mencari proyek berdasarkan nama klien.

Program memanfaatkan struktur data **Dictionary** untuk menyimpan data proyek serta **Function** untuk memisahkan setiap modul logika program.

---

## 2. Gambar Flowchart & Penjelasan Alur

(<img width="2650" height="2260" alt="flowchart_minpro2" src="https://github.com/user-attachments/assets/2983e7fb-0670-4ae1-957f-861996278d72" />
)

### Penjelasan Alur Flowchart:
* **Menu Utama & Login:** Pengguna memilih menu Login. Sistem melakukan verifikasi username dan password. Jika salah 3 kali, batas kesempatan habis dan pengguna dikembalikan ke Menu Utama.
* **Menu Admin:**
  * **Tampilkan Data Proyek:** Menampilkan tabel daftar seluruh proyek desain.
  * **Tambah Data Proyek:** Menerima input nama klien, jenis desain, dan deadline, lalu menyimpannya ke dalam dictionary data proyek.
  * **Ubah Data Proyek:** Memvalidasi input nomor proyek (harus berupa angka dan ada di daftar). Jika valid, sistem memperbarui detail data proyek tersebut.
  * **Hapus Data Proyek:** Memvalidasi nomor proyek lalu menghapus data terkait dari dictionary.
  * **Logout:** Mengakhiri sesi Admin dan mengarahkan kembali ke Menu Utama.
* **Menu User:**
  * **Tampilkan Data Proyek:** Menampilkan daftar seluruh proyek desain yang ada.
  * **Cari Proyek:** Menerima input nama klien dan mencocokkan data pada sistem. Jika ditemukan, detail proyek ditampilkan.
  * **Logout:** Mengakhiri sesi User dan mengarahkan kembali ke Menu Utama.

---

## Penjelasan Code

### Import Library
(<img width="349" height="99" alt="image" src="https://github.com/user-attachments/assets/2a4a51b8-2465-44bc-be5d-2c1028164805" />
)

Empat baris pertama merupakan daftar library yang digunakan. `os` digunakan untuk membersihkan layar terminal, `time` untuk memberikan jeda agar pesan dapat terbaca sebelum layar dibersihkan, `PrettyTable` untuk membuat tampilan tabel, dan `pwinput` untuk menyembunyikan input password.

### Variabel Data
(<img width="535" height="98" alt="image" src="https://github.com/user-attachments/assets/b082cd16-5737-451d-891a-062bff3d21b9" />
)

Tiga variabel utama yang digunakan sebagai penyimpanan data program:
* `akun`: Berisi dictionary di dalam dictionary dengan *key* berupa username, serta nilai berupa dictionary yang menyimpan password dan role. Pengecekan role dilakukan dengan memanggil `akun[username]["role"]`. Akun terdaftar terdiri dari `admin` dan `user`.
* `daftar_proyek`: Menyimpan data proyek dengan *key* berupa nomor proyek dan nilai berupa dictionary berisi klien, jenis, dan deadline.
* `nomor_baru`: Bernilai awal 3, berfungsi sebagai penghitung otomatis untuk nomor proyek yang akan ditambahkan berikutnya.

### Fungsi Bersih Layar
(<img width="491" height="65" alt="image" src="https://github.com/user-attachments/assets/e37976ad-15ca-49bb-a838-50cc4acd2080" />
)

Fungsi `bersih()` digunakan untuk membersihkan layar terminal. Pengecekan `os.name == "nt"` menentukan perintah `cls` untuk Windows atau `clear` untuk sistem operasi lain.

---

## Fungsi Olah Data Proyek

### 1. Fungsi Tampil Proyek
(<img width="1221" height="211" alt="image" src="https://github.com/user-attachments/assets/06efb21b-f55f-475e-9f57-acd76a6804f2" />
)

Tabel dibuat menggunakan `PrettyTable`. Jika `daftar_proyek` kosong, sistem menampilkan pesan *"Data proyek masih kosong"*. Jika berisi data, *header* kolom diatur melalui `field_names`, lalu setiap baris data dimasukkan melalui iterasi. Fungsi ini digunakan pada menu tampil data, ubah data, dan hapus data.

### 2. Fungsi Tambah Proyek
(<img width="834" height="302" alt="image" src="https://github.com/user-attachments/assets/1dec8d4b-924a-47ac-87e6-91e65950b679" />
)

Admin menginput nama klien, jenis desain, dan deadline. Jika ada input yang kosong, sistem menampilkan pesan *"Data tidak boleh kosong!"*. Jika seluruh input valid, data disimpan ke `daftar_proyek` dengan *key* dari `nomor_baru`, kemudian nilai `nomor_baru` ditambah 1 menggunakan kata kunci `global`.

### 3. Fungsi Ubah Proyek
(<img width="866" height="417" alt="image" src="https://github.com/user-attachments/assets/da7dbad5-1e22-4a1c-b1f7-d61af852cb1a" />
)

Sistem menampilkan tabel proyek dan meminta masukan nomor proyek yang akan diubah. Input divalidasi menggunakan `try-except ValueError` untuk menangani input non-angka. Jika nomor proyek terdaftar, admin memasukkan data pembaruan yang divalidasi agar tidak kosong sebelum memperbarui dictionary.

### 4. Fungsi Hapus Proyek
(<img width="625" height="291" alt="image" src="https://github.com/user-attachments/assets/b6e9312d-5621-496f-8614-664879d290c7" />
)

Sistem menampilkan tabel proyek dan meminta masukan nomor proyek. Validasi angka dilakukan menggunakan `try-except ValueError`. Jika nomor ditemukan, data dihapus dari dictionary menggunakan perintah `del`.

### 5. Fungsi Cari Proyek
(<img width="646" height="286" alt="image" src="https://github.com/user-attachments/assets/50f96cf5-4ff0-4583-b987-90cd3a73e5c8" />
)

Fitur pencarian pada menu user menerima input nama klien dan melakukan iterasi pada seluruh data proyek. Jika nama klien cocok, detail proyek ditampilkan. Variabel penanda `ketemu` digunakan untuk menentukan penampilkan pesan *"Klien tidak ditemukan"*.

---

## Menu dan Login

### 1. Menu Admin
(<img width="622" height="595" alt="image" src="https://github.com/user-attachments/assets/a21ec753-cedb-463d-8597-b0c5ab62d75a" />
)

Memiliki pilihan menu: tampilkan, tambah, ubah, hapus, dan logout. Input pilihan berupa string untuk mencegah error jika dimasukkan karakter non-angka. Perulangan berjalan hingga admin memilih menu logout.

### 2. Menu User
(<img width="623" height="458" alt="image" src="https://github.com/user-attachments/assets/c334c1d9-d186-48c8-a9b3-ae4c4e614bf8" />
)

Memiliki tiga pilihan menu: tampilkan data, cari proyek, dan logout. Access control membatasi user agar tidak dapat melakukan penambahan, pembaruan, atau penghapusan data.

### 3. Fungsi Login
(<img width="741" height="454" alt="image" src="https://github.com/user-attachments/assets/326a31ed-b781-4ac0-8bed-e93383be906c" />
)

Pengguna diberikan batas percobaan sebanyak 3 kali via variabel `kesempatan`. Password diinput menggunakan `pwinput`. Pengecekan `username in akun` dilakukan terlebih dahulu untuk mencegah `KeyError`. Jika autentikasi berhasil, pengguna diarahkan ke menu sesuai dengan nilai `akun[username]["role"]`.

### 4. Program Utama
(<img width="633" height="403" alt="image" src="https://github.com/user-attachments/assets/f3a72ee9-ab6c-4e75-b9cf-539ceb9d3f05" />
)

Titik awal eksekusi program yang menampilkan pilihan Login atau Keluar. Memanggil fungsi `login()` jika memilih opsi 1, dan menghentikan perulangan jika memilih opsi 2.

---

## Dokumentasi Output

Skenario pengujian mencakup percobaan login gagal, pengoperasian fitur admin, pengoperasian fitur user, hingga keluar dari sistem.

### 1. Login Gagal dan Kesempatan Login Habis
Pengujian input password salah dengan penurunan sisa kesempatan login:
(<img width="468" height="422" alt="image" src="https://github.com/user-attachments/assets/c68fbdd2-bb49-4e78-a269-ed9a401842a3" />
)

### 2. Tampilkan Data Proyek
Pengujian penampilkan seluruh data proyek pada menu admin:
(<img width="468" height="331" alt="image" src="https://github.com/user-attachments/assets/a6cf352d-b854-4c8d-bede-ce6e3c1d52e2" />
)

### 3. Tambah Proyek
Pengujian penambahan data baru serta validasi input kosong dan tampilan saat data berhasil ditambahkan:
(<img width="295" height="332" alt="image" src="https://github.com/user-attachments/assets/c5f7dc71-f295-4f04-a9e2-1c67ee84ab1e" />
)(<img width="299" height="316" alt="image" src="https://github.com/user-attachments/assets/7e037b86-496c-441d-82c6-9f90c3204433" />
)()<img width="483" height="379" alt="image" src="https://github.com/user-attachments/assets/b0069db7-336b-4d3b-848c-c136af3fe6e1" />


### 4. Ubah Proyek
Pengujian pembaruan data beserta penanganan error input non-angka dan tampilan data setelah diubah:
(<img width="482" height="423" alt="image" src="https://github.com/user-attachments/assets/c7e4bb88-f13f-485b-ae77-690930a7eff0" />
)(<img width="484" height="484" alt="image" src="https://github.com/user-attachments/assets/a7640a71-0767-44a6-ac69-69f0df230200" />
)(<img width="460" height="376" alt="image" src="https://github.com/user-attachments/assets/1e7fca8e-f44a-4388-80e9-617fcd13fae5" />
)

### 5. Hapus Proyek
(<img width="458" height="420" alt="image" src="https://github.com/user-attachments/assets/d3e1f626-9931-4fdb-a092-2e5741e6f7dd" />
)(<img width="440" height="420" alt="image" src="https://github.com/user-attachments/assets/aa9653d8-893e-43e6-8767-9a76ea0e06af" />
)(<img width="457" height="346" alt="image" src="https://github.com/user-attachments/assets/3985335d-74ba-4f77-860d-65fcdf80c355" />
)

### 6. Tampilkan dan Cari Data
Pengujian pencarian data proyek berdasarkan nama klien pada menu user:
<img width="437" height="316" alt="image" src="https://github.com/user-attachments/assets/c7db527e-b24d-4666-8263-c0a5dc4d3c59" />
)(<img width="326" height="283" alt="image" src="https://github.com/user-attachments/assets/e68ffbea-6558-49f3-bb2a-8711d7221b6a" />
)

### 7. Keluar Program
Pengujian keluar dari program utama:
(<img width="231" height="228" alt="image" src="https://github.com/user-attachments/assets/857eca78-e382-4163-be0f-fe30727bd1c7" />
)
