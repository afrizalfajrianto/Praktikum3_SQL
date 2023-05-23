# Praktikum3_SQL

# **SQL Constraint**

- SQL Constraint digunakan untuk menentukan aturan untuk data dalam tabel.
- Constraint digunakan untuk membatasi jenis data yang bisa masuk ke tabel. Ini memastikan keakuratan dan keandalan data dalam tabel.
- Constraint dapat berupa level kolom atau level tabel.
- Constraint level kolom berlaku untuk kolom, dan batasan level tabel berlaku untuk seluruh tabel.

## **Tugas Praktikum**

- Implementasikan penggunaan **_CONSTRAINT FOREIGN KEY_** pada semua tabel yang berelasi.
- yang perlu diperhatikan:
  - tipe data pada field yang berelasi harus sama termasuk juga ukuran datanya.
  - misal: pada tabel dosen, kd_ds VARCHAR(10) maka tabel yang merujuk yaitu tabel mahasiswa, kd_ds juga harus bertipe VARCHAR(10).

1. Lakukan penambahan data pada tabel mahasiswa dengan mengisi kd_ds yang belum ada pada data dosen.
2. Hapus satu record data pada tabel dosen yang telah dirujuk pada tabel mahasiswa.
3. Ubah mode menjadi ON UPDATE CASCADE ON DELETE RESTRICT
4. Lakukan perubahan data pada tabel dosen (kd_ds)
5. Lakukan penghapusan data pada tabel dosen
6. Ubah mode menjadi ON UPDATE CASCADE ON DELETE SET NULL
7. Lakukan penghapusan data pada tabel dosen

### **Evaluasi dan Pertanyaan**

- [Tulis semua perintah-perintah SQL percobaan di atas beserta outputnya!](#syntax-sql)
- [Apa bedanya penggunaan RESTRICT dan penggunaan CASCADE](#perbedan-rastrict--cascade)
- [Berikan kesimpulan anda! ](#kesimpulan)
- [Buat laporan praktikum yang berisi, langkah-langkah praktikum beserta screenshot yang sudah dilakukan dalam bentuk dokumen](LAPORAN_PRAKTIKUM_3.pdf)

### Syntax SQL

- Membuat foreign key

  - Dalam ALTER TABLE:
    ```SQL
    ALTER TABLE mahasiswa
    ADD CONSTRAINT fk_dosenwali FOREIGN KEY (kd_ds)     REFERENCES dosen(kd_ds)
    ```
  - Dalam CREATE TABLE:
    ```sql
    CREATE TABLE mahasiswa(
    nim VARCHAR(10) NOT NULL,
    nama VARCHAR(100) NOT NULL,
    kd_ds VARCHAR(10),
    PRIMARY KEY(nim),
    CONSTRAINT fk_DosenWali FOREIGN KEY (kd_ds)
    REFERENCES dosen(kd_ds)
    );
    ```

  ```

  ```

- Mengubah data
  ```sql
  UPDATE mahasiswa
  SET kd_ds = 'DS011' WHERE nim = 112233445;
  ```
- Menampilkan CREATE TABLE
  ```sql
  SHOW CREATE TABLE  mahasiswa;
  ```
- Mode ON UPDATE CASCADE ON DELETE CASCADE
  ```sql
  ALTER TABLE mahasiswa
  DROP FOREIGN KEY fk_mahasiswa_dosen,
  ADD CONSTRAINT fk_dosenwali FOREIGN KEY (kd_ds) REFERENCES dosen(kd_ds) ON UPDATE CASCADE ON DELETE CASCADE;
  ```
- Menghapus data
  ```sql
  DELETE FROM dosen WHERE kd_ds = 'DS001';
  ```
- Mode ON UPDATE CASCADE ON DELETE NOT NULL
  ```sql
  ALTER TABLE <table>
  DROP FOREIGN KEY <nama_constraint_lama>,
  ADD CONSTRAINT <nama_constraint_baru> FOREIGN KEY (field) REFERENCES <table_references(filed_references)> ON UPDATE CASCADE ON DELETE NOT NULL;
  ```
- Mengubah data
  ```sql
  UPDATE dosen
  SET kd_ds = 'DS006' WHERE nama = 'Haha Hihi';
  ```
- Menghapus data
  ```sql
  DELETE FROM dosen WHERE nim = 'DS003';
  ```

### Perbedan RASTRICT & CASCADE

- RESTRICT : ketika menggunakan opsi RESTRICT dalam keterkatian, aturan keterkaitan akan membatasi aksi yang dapat dilakukan pada data yang terkait. Jika ada aksi yang menyebabkan konflik atau melanggar aturan keterkaitan. RESTRICT akan mencegaah aksi tersebut dilakukan. Misalnya, jika ada keterkaitan antara Tabel A dan Tabel B, dan kita mencoba untuk menghapus baris dari Tabel A yang memiliki keterkaitan dengan Tabel B, RESTRICT akan mencegah penghapusan tersebut jika ada baris yang masih terkait dalam Tabel B. Dengan menggunakan RESTRICT, aksi yang melanggar keterkaitan akan ditolak.
- CASCADE : ketika menggunakan opsi CASCADE dalam keterkaitan, aturan keterkaitan akan menyebabkan aksi yang dilakukan pada satu tabel juga mempengaruhi tabel yang terkait. Jadi, jika ada aksi yang dilakukan pada tabel yang memiliki ketertakitan dengan tabel lain, CASCADE akan mengakibatkan aksi tersebut juga berdampak pada tabel yang terkait. Misalnya, jika ada keterkaitan antara Tabel A dan Tabel B, dan kita menghapus baris dari Tabel A, CASCADE akan menghapus semua baris yang terkait dengan Tabel B secara otomatis. Dengan menggunakan CASCADE, aksi yang dilakukkan pada satu tabel akan menyebabkan kaskade aksi pada tabel yang terkait.

### Kesimpulan

- RESTRICT : RESTRICT membatasi aksi yang melanggar keterkaitan antara tabel.
- CASCADE : CASCADE mempengaruhi tabel yang terkait dengan aksi yang dilakukan pada tabel utama.
  Keitka memilih antara RESTRICT dan CASCADE, pertimbangkan tujuan dan kebutuhan skema basis data yang sedang Anda bangun. RESTRICT cocok jika Anda ingin menerapkan pembatasan yang ketat pada aksi yang melanggar keterkaitan, sementara CASCADE memungkinkan aksi pada satu tabel juga berdampak pada tabel terkait.