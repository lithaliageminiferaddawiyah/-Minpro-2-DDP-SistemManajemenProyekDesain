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
