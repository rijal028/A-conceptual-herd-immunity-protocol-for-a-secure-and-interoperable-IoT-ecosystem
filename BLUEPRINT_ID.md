# Blueprint: Kerangka Kerja Keamanan IoT "Cerebrum"
### Sebuah Desain Konseptual untuk Ekosistem Rumah Pintar yang Aman dan Terbuka

**Oleh: Rijal Saepuloh**

---

### Daftar Isi
1.  [Filosofi Inti: Penjaga Gerbang, Bukan Raja](#1-filosofi-inti-penjaga-gerbang-bukan-raja)
2.  [Fungsi Ganda Cerebrum](#2-fungsi-ganda-cerebrum)
3.  [Arsitektur Pertahanan Berlapis](#3-arsitektur-pertahanan-berlapis)
    * [3.1. Lapisan 1: Manifesto Perangkat Terverifikasi](#31-lapisan-1-manifesto-perangkat-terverifikasi)
    * [3.2. Lapisan 2: Protokol Pembaruan Aman](#32-lapisan-2-protokol-pembaruan-aman)
    * [3.3. Lapisan 3: Deteksi Anomali Jaringan](#33-lapisan-3-deteksi-anomali-jaringan)
    * [3.4. Lapisan 4: Micro-segmentation Internal](#34-lapisan-4-micro-segmentation-internal)
4.  [Studi Kasus: Skenario Serangan "Lampu Bohlam"](#4-studi-kasus-skenario-serangan-lampu-bohlam)
5.  [Kesimpulan: Menuju Interoperabilitas yang Aman](#5-kesimpulan-menuju-interoperabilitas-yang-aman)

---

### 1. Filosofi Inti: Penjaga Gerbang, Bukan Raja

Arsitektur "Cerebrum" menolak model ekosistem tertutup yang membatasi pilihan pengguna. Sebaliknya, ia dirancang sebagai sebuah **platform terbuka** yang memungkinkan perangkat dari ratusan pabrikan berbeda untuk bekerja sama.

Untuk mencapai ini, Cerebrum tidak bertindak sebagai "raja" atau pengendali pusat yang mendikte setiap perangkat. Ia berfungsi sebagai **"Penjaga Gerbang" (Gatekeeper)** yang tangguh. Filosofinya adalah: setiap pabrikan perangkat bertanggung jawab atas keamanan produknya sendiri, dan Cerebrum menyediakan lapisan keamanan jaringan tambahan dan jembatan agar semua perangkat tersebut bisa berkomunikasi dengan aman.

### 2. Fungsi Ganda Cerebrum

Berdasarkan filosofi di atas, Cerebrum memiliki dua tugas utama:

1.  **Sebagai Jembatan Interoperabilitas:** Menyediakan platform dan protokol standar agar lampu Philips, kunci pintu Samsung, dan sensor cuaca Xiaomi bisa saling "berbicara" dan bekerja sama dalam satu ekosistem rumah pintar.
2.  **Sebagai Penjaga Keamanan Jaringan:** Secara aktif memantau, menganalisis, dan mengontrol semua lalu lintas data—baik antar perangkat di dalam rumah, maupun antara perangkat dengan internet—untuk mendeteksi dan menetralisir aktivitas berbahaya.

### 3. Arsitektur Pertahanan Berlapis

Cerebrum menerapkan empat lapisan pertahanan utama untuk melindungi jaringan rumah pintar.

#### 3.1. Lapisan 1: Manifesto Perangkat Terverifikasi
Ini adalah fondasi kepercayaan. Saat perangkat baru terhubung, Cerebrum tidak menebak-nebak perilakunya. Ia mengunduh sebuah **"Manifesto Perilaku"** yang disediakan dan ditandatangani secara digital oleh pabrikan. Manifesto ini berisi daftar aturan ketat: server mana yang boleh dihubungi, port apa yang digunakan, batas transfer data, dll.

#### 3.2. Lapisan 2: Protokol Pembaruan Aman
Saat sebuah perangkat mencoba memperbarui *firmware*-nya, Cerebrum menjalankan protokol validasi 4 langkah untuk mencegah serangan rantai pasokan (*supply chain attack*):
1.  **Izin Pengguna:** Meminta persetujuan eksplisit dari pemilik rumah.
2.  **Pemeriksaan Manifesto Baru:** Membandingkan perubahan antara manifesto lama dan baru.
3.  **Validasi Otoritas Berlapis:** Memeriksa keaslian manifesto baru melalui beberapa sumber tepercaya (pihak ketiga, komunitas, ledger).
4.  **Karantina Pasca-Update:** Memantau perangkat dengan kecurigaan tinggi selama 24 jam setelah pembaruan untuk memastikan perilakunya sesuai dengan manifesto baru.

#### 3.3. Lapisan 3: Deteksi Anomali Jaringan
Ini adalah "Protokol Kognitif" yang diterapkan pada perangkat. Cerebrum terus-menerus mempelajari pola lalu lintas data normal untuk setiap perangkat. Jika sebuah kulkas yang biasanya hanya memakai data 500KB per hari tiba-tiba mencoba mengirim data 50MB, sistem akan mendeteksinya sebagai anomali dan bisa langsung memutus koneksinya.

#### 3.4. Lapisan 4: Micro-segmentation Internal
Ini adalah pertahanan terhadap gerakan lateral. Cerebrum memiliki sebuah **matriks hak akses** internal. Setiap perangkat hanya diizinkan untuk "berbicara" dengan perangkat lain yang relevan.
* Lampu bohlam **tidak punya hak** untuk berkomunikasi dengan kunci pintu pintar.
* Sensor suhu **tidak punya hak** untuk mengakses data dari kamera keamanan.

### 4. Studi Kasus: Skenario Serangan "Lampu Bohlam"

1.  **Serangan:** Peretas menemukan celah di lampu bohlam dan berhasil menyusup ke dalamnya.
2.  **Tindakan Cerebrum:**
    * Peretas mencoba menggunakan lampu untuk terhubung ke server komandonya di Rusia. -> **Gagal.** Ditolak oleh **Lapisan 3 (Deteksi Anomali)** karena tujuannya tidak ada di dalam Manifesto.
    * Peretas mencoba menginstal *firmware* jahat pada lampu. -> **Gagal.** Ditolak oleh **Lapisan 2 (Protokol Pembaruan)**.
    * Peretas mencoba menggunakan lampu untuk mengirim perintah "Buka Kunci" ke kunci pintu pintar. -> **Gagal.** Ditolak oleh **Lapisan 4 (Micro-segmentation)** karena lampu tidak punya hak akses ke kunci pintu.
3.  **Hasil:** Serangan berhasil dibendung pada titik masuknya dan tidak bisa menyebar. Rumah tetap aman.

### 5. Kesimpulan: Menuju Interoperabilitas yang Aman

"Cerebrum" bukanlah solusi untuk menggantikan tanggung jawab keamanan pabrikan. Ia adalah sebuah **jembatan keamanan universal** yang memungkinkan ekosistem IoT yang beragam dan terbuka untuk bisa eksis secara aman. Ia memberikan ketenangan pikiran bagi pengguna dan menciptakan arena bermain yang adil bagi semua inovator di dunia rumah pintar.
