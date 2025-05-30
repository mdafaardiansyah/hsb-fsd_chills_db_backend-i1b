# Mission Back End Intermediate 1 B Harisenin Bootcamp FSD - Chill's Database

Repositori ini berisi setup MySQL menggunakan Docker Compose, beserta dua opsi untuk inisialisasi database: menggunakan SQL dump atau membuat dari nol dengan skrip SQL yang ditujukan untuk memenuhi **Mission Back End Intermediate 1 B Hari Senin Bootcamp.**

---

## 📦 Struktur Folder

```
.
├── .env                      # Konfigurasi environment (user, password, dsb)
├── docker-compose.yml        # Konfigurasi Docker Compose untuk MySQL
├── my.cnf/                   # Konfigurasi custom MySQL (opsional)
├── sql_dump/
│   └── dump-chills_db-202505301405.sql   # File dump SQL (backup)
└── sql_query/
    └── chill_apps_mysql_script_simple.sql # Skrip SQL untuk membuat database dari nol
```

---

## 🚀 Cara Menjalankan MySQL dengan Docker Compose

1. **Pastikan Docker & Docker Compose sudah terinstal.**

2. **Konfigurasi file `.env`**  
   Edit file `.env` untuk mengatur variabel seperti `MYSQL_ROOT_PASSWORD`, `MYSQL_DATABASE`, `MYSQL_USER`, dan `MYSQL_PASSWORD`.  
   Contoh:
   ```
   MYSQL_ROOT_PASSWORD=your_root_password
   MYSQL_DATABASE=chills_db
   MYSQL_USER=chills_user
   MYSQL_PASSWORD=your_password
   ```

3. **Jalankan Docker Compose:**
   ```sh
   docker compose up -d
   ```
   Ini akan menjalankan container MySQL dengan versi `latest` sesuai konfigurasi di `docker-compose.yml`.

4. **Cek status container:**
   ```sh
   docker compose ps
   ```

---

## 🗄️ Cara Import Database

### **A. Import dari SQL Dump**

1. **Pastikan container MySQL sudah berjalan.**
2. **Import file dump ke dalam database:**
   ```sh
   docker exec -i <nama_container_mysql> mysql -u"$MYSQL_USER" -p"$MYSQL_PASSWORD" "$MYSQL_DATABASE" < sql_dump/dump-chills_db-202505301405.sql
   ```
   - Ganti `<nama_container_mysql>` dengan nama container MySQL (lihat dengan `docker compose ps`).
   - Pastikan variabel diambil dari file `.env` atau sesuaikan manual.

   **Best Practice:**  
   - Selalu backup database sebelum melakukan import.
   - Pastikan struktur database (`MYSQL_DATABASE`) sudah sesuai di `.env`.

---

### **B. Membuat Database dari Nol dengan SQL Query**

1. **Pastikan container MySQL sudah berjalan.**
2. **Jalankan skrip SQL untuk membuat struktur dan data awal:**
   ```sh
   docker exec -i <nama_container_mysql> mysql -u"$MYSQL_USER" -p"$MYSQL_PASSWORD" "$MYSQL_DATABASE" < sql_query/chill_apps_mysql_script_simple.sql
   ```
   - Ganti `<nama_container_mysql>` sesuai nama container.

   **Best Practice:**  
   - Review skrip SQL sebelum dijalankan.
   - Gunakan user non-root untuk operasi sehari-hari.

---

## 📝 Tips & Best Practices

- **Jangan commit file `.env` yang berisi kredensial sensitif ke repository publik.**
- **Gunakan volume Docker untuk persistent storage agar data tidak hilang saat container dihapus.**
- **Selalu cek log container jika terjadi error:**
  ```sh
  docker compose logs <nama_service>
  ```
- **Gunakan user dengan hak akses terbatas untuk aplikasi, bukan root.**
- **Rutin backup database.**

---

## ❓ Troubleshooting

- **Port sudah digunakan:**  
  Ubah port mapping di `docker-compose.yml`.
- **Gagal koneksi:**  
  Pastikan variabel di `.env` sudah benar dan container berjalan.

---

## 📚 Referensi

- [Dokumentasi MySQL Docker](https://hub.docker.com/_/mysql)
- [Docker Compose](https://docs.docker.com/compose/)
