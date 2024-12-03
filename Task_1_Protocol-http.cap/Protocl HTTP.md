
# Tugas 1 Protocol `http.cap`

Pada tugas ini menjelaskan terkait dari cara kerja protokol `http.cap`

HTTP (HyperText Transfer Protocol) adalah protokol yang digunakan untuk mengirimkan data di web, memungkinkan komunikasi antara klien (misalnya, browser web) dan server. File `http.cap` adalah file tangkapan network (network capture) yang berisi data HTTP dalam bentuk paket yang dapat dianalisis, seperti menggunakan Wireshark atau alat lain. Berikut adalah penjelasan rinci tentang cara kerja protokol HTTP dan aspek teknisnya:


## Aspek Teknis

- Cara Kerja Protokol HTTP dan Socket
- Header HTTP
- Jumlah Paket dalam HTTP Capture
- Flow Graph dari HTTP


## 1. Cara Kerja Protokol HTTP dan Socket

- HTTP adalah protokol berbasis teks dan bekerja di lapisan aplikasi dari model OSI. Klien (browser) menginisiasi koneksi ke server melalui soket TCP (biasanya port 80 untuk HTTP dan 443 untuk HTTPS).
- Socket: Klien membuka soket TCP ke alamat IP server pada port yang ditentukan, lalu mengirimkan permintaan HTTP. Koneksi TCP ini menggunakan mekanisme three-way handshake, yaitu SYN, SYN-ACK, dan ACK untuk memulai komunikasi.
- HTTP adalah protokol stateless, yang berarti setiap permintaan klien tidak bergantung pada permintaan sebelumnya. Pada HTTP/1.1, koneksi tetap terbuka untuk memungkinkan komunikasi yang lebih efisien, sementara HTTP/2 dan HTTP/3 memiliki pengelolaan koneksi yang lebih canggih dan paralel.

### Hasil tangkapan layar
![Port HTML](https://github.com/infans4/Tugas-1_Penjelasan-Protokol-http.cap/blob/main/assets/Port%20HTML.png)
![Socket](https://github.com/infans4/Tugas-1_Penjelasan-Protokol-http.cap/blob/main/assets/Socket.png)
![HTTP1.1](https://github.com/infans4/Tugas-1_Penjelasan-Protokol-http.cap/blob/main/assets/HTTP1.1.png)

## 2. Header HTTP

Header HTTP berisi informasi penting tentang permintaan dan respons, dan dibagi menjadi dua jenis: **Header Permintaan** (Request Header) dan **Header Respons** (Response Header).

**Header Permintaan**: Digunakan oleh klien untuk memberikan informasi tentang permintaan. Contoh:
- `GET /index.html HTTP/1.1`: Menyatakan permintaan untuk mengunduh sumber daya index.html.
- `Host`: Nama domain yang ingin diakses, misalnya Host: www.example.com.
- `User-Agent`: Menyatakan aplikasi atau browser yang digunakan klien.

**Header Respons**: Digunakan oleh server untuk mengirimkan informasi status respons. Contoh:
- `HTTP/1.1 200 OK`: Status HTTP yang menunjukkan permintaan berhasil.
- `Content-Type`: Menyatakan tipe konten yang dikirimkan, misalnya text/html atau application/json.
- `Content-Length`: Menyatakan ukuran konten yang dikirimkan dalam respons.

### Hasil tangkapan layar
![HTTP Get](https://github.com/infans4/Tugas-1_Penjelasan-Protokol-http.cap/blob/main/assets/HTTP%20Get.png)
![HTTP Response](https://github.com/infans4/Tugas-1_Penjelasan-Protokol-http.cap/blob/main/assets/HTTP%20Response.png)
## 3. Jumlah Paket dalam HTTP Capture

Jumlah paket yang dikirimkan dalam komunikasi HTTP bergantung pada jenis dan ukuran permintaan serta respons. Berikut ini adalah beberapa jenis paket yang dapat ditemukan dalam tangkapan HTTP:

**Permintaan Klien ke Server**:
- Satu paket untuk membuka koneksi TCP (three-way handshake).
- Satu paket untuk permintaan HTTP itu sendiri (misalnya, `GET /index.html HTTP/1.1`).
**Respons Server ke Klien**:
- Paket respons status dan header, seperti `HTTP/1.1 200 OK`.
- Paket data yang berisi konten halaman web atau file yang diminta.
**Penutupan Koneksi**:
- Untuk HTTP/1.0, koneksi ditutup setelah respons selesai.
- Untuk HTTP/1.1 atau yang lebih baru, koneksi bisa tetap terbuka untuk beberapa permintaan.
Total jumlah paket dapat bervariasi, namun untuk satu permintaan dasar (misalnya, sebuah permintaan `GET` sederhana yang menerima respons kecil), biasanya diperlukan sekitar 4-6 paket, tergantung pada ukuran konten.
### Hasil tangkapan layar
![Client to Server](https://github.com/infans4/Tugas-1_Penjelasan-Protokol-http.cap/blob/main/assets/Client%20to%20Server.png)
![Server to Client](https://github.com/infans4/Tugas-1_Penjelasan-Protokol-http.cap/blob/main/assets/Server%20to%20Client.png)
![Close conn](https://github.com/infans4/Tugas-1_Penjelasan-Protokol-http.cap/blob/main/assets/Close%20conn.png)
## 4. Flow Graph dari HTTP di Wireshark

Untuk melihat grafik alur HTTP, dapat menggunakan fitur Flow Graph di Wireshark yang menampilkan aliran komunikasi antara klien dan server, termasuk handshakes dan paket HTTP yang dikirim. Flow Graph menunjukkan langkah-langkah komunikasi berikut:

1. **YN, SYN-ACK, ACK**: Koneksi TCP diinisiasi oleh klien.
2. **HTTP GET**: Permintaan `GET` dari klien ke server.
3. **HTTP 200 OK**: Respons dari server jika permintaan berhasil.
4. **Pengiriman Data**: Pengiriman data konten dari server ke klien.
5. **Penutupan Koneksi**: Jika tidak ada permintaan lebih lanjut, koneksi TCP akan ditutup.

Pada halaman Wiki Wireshark dapat menemukan file `http.cap` untuk mengunduh tangkapan paket HTTP sebagai sampel. Setelah diunduh, file tersebut bisa dibuka di Wireshark untuk melihat detail komunikasi dalam bentuk paket.
### Hasil tangkapan layar
![Flow1](https://github.com/infans4/Tugas-1_Penjelasan-Protokol-http.cap/blob/main/assets/Flow1.png)
![Flow2](https://github.com/infans4/Tugas-1_Penjelasan-Protokol-http.cap/blob/main/assets/Flow2.png)
