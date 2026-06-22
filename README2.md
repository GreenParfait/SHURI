# Laundry JOSJIS

[![Java](https://img.shields.io/badge/Java-%23ED8B00.svg?style=flat&logo=openjdk&logoColor=white)](https://www.oracle.com/java/)
[![MySQL](https://img.shields.io/badge/MySQL-%2300758F.svg?style=flat&logo=mysql&logoColor=white)](https://www.mysql.com/)
[![Apache Tomcat](https://img.shields.io/badge/Apache_Tomcat-%23F8DC75.svg?style=flat&logo=apachetomcat&logoColor=black)](https://tomcat.apache.org/)
[![Apache Maven](https://img.shields.io/badge/Apache_Maven-%23C71A36.svg?style=flat&logo=apachemaven&logoColor=white)](https://maven.apache.org/)

**Laundry JOSJIS** adalah aplikasi manajemen bisnis laundry berbasis web yang dirancang untuk menyederhanakan dan mengotomatisasi alur operasional mulai dari pendataan pelanggan, pencatatan transaksi, hingga pemrosesan pembayaran dalam satu platform terpusat yang mudah digunakan.

Sistem ini dikembangkan menggunakan arsitektur **_MVC_ (Model-View-Controller)** dengan _Java EE_ (Servlet & JSP) dan **database MySQL**. Prinsip-prinsip Pemrograman Berorientasi Objek (OOP) diterapkan langsung dalam kode, mencakup konsep Encapsulation, Abstraction, Inheritance, Polymorphism, Robustness, dan Role-Based Access Control.

Proyek ini dibangun sebagai **Tugas Besar PBO IF-04-04** di Telkom University Surabaya.

---

## Project Layout

```
📦 demo/                                # Root direktori proyek
┣ 📂 src/
┃ ┣ 📂 main/
┃ ┃ ┣ ☕ java/                          # Source code Java (Model, Servlet/Controller)
┃ ┃ ┗ 🌐 webapp/                        # Aset web (JSP/View, CSS, JS, konfigurasi)
┣ ⚙️ pom.xml                            # Konfigurasi utama Apache Maven
┣ ⚙️ pom1.xml                           # Konfigurasi Maven alternatif
┣ 🗄️ laundry_db.sql                     # Skema Database
┗ 📄 README.md                          # Dokumentasi Project
```

## Development Ecosystem

- **Architecture:** _MVC (Model-View-Controller)_
- **Backend:** Java (Java EE / Servlet)
- **Frontend:** JSP + JSTL
- **Database:** MySQL
- **Build Tool:** Apache Maven
- **Server Container:** Apache Tomcat 7

---

## Fitur Utama

- **Encapsulation:** Data kredensial dan sesi pengguna dikelola melalui class `User` dan `SistemLogin` dengan prinsip _encapsulation_ untuk menjamin keamanan akses dan integritas data.
- **Abstraction:** _Abstract class_ `RoleUser` dan _interface_ `Pembayaran` mendefinisikan kontrak perilaku tanpa mengekspos detail implementasinya, sehingga sistem lebih modular dan mudah dikembangkan.
- **Inheritance:** _Abstract class_ `RoleUser` diturunkan menjadi class `Admin` dan `Kasir`, serta class `User` sebagai dasar hierarki pengguna sistem.
- **Polymorphism:** Implementasi _interface_ `Pembayaran` dengan dua konkretisasi — `Cash` dan `QRIS` — memungkinkan sistem memproses berbagai metode pembayaran secara polimorfik.
- **Robustness:** Setiap operasi kritis dilengkapi mekanisme _exception handling_ untuk memastikan stabilitas sistem saat terjadi input tidak valid atau kegagalan koneksi.
- **Role-Based Access Control:** Class `Admin` dan `Kasir` memiliki hak akses dan menu yang berbeda sesuai perannya, sehingga setiap pengguna hanya dapat mengakses fitur yang relevan dengan tanggung jawabnya.

---

## Anggota Tim

Proyek ini merupakan hasil kolaborasi tim yang masing-masing anggotanya bertanggung jawab atas modul dan implementasi konsep OOP tertentu.

| **Nama**                           | **Role & Tanggung Jawab OOP**                                                                                                 |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **Bezaliel Agung Trilaksana**      | Manajemen Transaksi: Membuat class `Transaksi`, menghubungkan pelanggan & laundry, serta menampilkan detail transaksi.        |
| **Heilyn Alfreda Aritonang**       | Pembayaran: Membuat _interface_ `Pembayaran` serta membuat class `Qris` dan `Cash` untuk modul pembayaran.                    |
| **Moch. Andy Yusuf Hendrawan E P** | Sistem Login dan User: Membuat class `User` dan `SistemLogin`, implementasi login, serta menentukan level user (admin/kasir). |
| **Faiz Agit Zahiri**               | Role User: Membuat _abstract class_ `RoleUser`, membuat class `Admin` dan `Kasir`, serta menentukan menu berdasarkan role.    |
| **Rizky Yusuf Maulana**            | Data Pelanggan & Laundry: Membuat class `Pelanggan` dan `Laundry`, serta membuat logika untuk menghitung harga laundry.       |

---

## 🛠️ Prasyarat (Prerequisites)

Sebelum menjalankan proyek ini, pastikan perangkat Anda sudah terinstal:

1. **Java Development Kit (JDK)** versi 8 atau yang lebih baru.
2. **Apache Tomcat** (Direkomendasikan versi 9).
3. **MySQL Server** (Bisa menggunakan XAMPP, WAMP, atau MySQL Server terpisah).
4. **Apache Maven** (Untuk manajemen dependensi dan _build_).

## Setup dan Penggunaan

### 1. Konfigurasi Database

1. Buka MySQL / PHPMyAdmin.
2. Buat database baru dengan nama `laundry`.
3. Import file struktur tabel SQL ke dalam database tersebut. _(Pastikan tabel `users`, `transaksi`, `pelanggan`, dan `layanan` sudah terbentuk)._
4. Pastikan terdapat setidaknya satu data karyawan dengan level `Admin` di dalam tabel `users`.

### 2. Konfigurasi Koneksi Database (Java)

Buka file `DatabaseConnection.java` (berada di `src/main/java/com/laundry/util/DatabaseConnection.java`) dan sesuaikan kredensial berikut dengan server MySQL Anda:

````java
String url = "jdbc:mysql://localhost:3306/laundry";
String username = "root"; // Sesuaikan dengan username MySQL Andas
String password = "";     // Sesuaikan dengan password MySQL Anda

````

### 3. Setup Project

1. Pastikan **JDK 8**, dan **Apache Maven** sudah terinstal.
2. Masuk ke direktori root proyek (`demo/`) melalui terminal.
3. Jalankan proyek langsung menggunakan plugin Tomcat 7 yang sudah dikonfigurasi di Maven:
   ```bash
   mvn clean package tomcat7:run

4. Pastikan build berhasil dengan keluaran `BUILD SUCCESS` dan server mulai berjalan di terminal.

### 4. Access Website

1. Setelah perintah `mvn tomcat7:run` berhasil, server Tomcat 7 akan berjalan.
2. Buka browser dan akses aplikasi di:
   ```
   http://localhost:8080
   ```
3. Gunakan kredensial berikut untuk pengujian awal:

   | Role      | Username | Password |
   | --------- | -------- | -------- |
   | **Admin** | `admin`  | `admin`  |
