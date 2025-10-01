# Jarkom-Modul-1-2025-K-04

Anggota :
| Nama | NRP |
| -------------------- | ---------- |
| Diva Aulia Rosa | 5027241003 |
|  | 5027 |

## Soal & Dokumentasi pengerjaan

### Soal 1 </br>
Untuk mempersiapkan pembuatan entitas selain mereka, Eru yang berperan sebagai Router membuat dua Switch/Gateway. Dimana Switch 1 akan menuju ke dua Ainur yaitu Melkor dan Manwe. Sedangkan Switch 2 akan menuju ke dua Ainur lainnya yaitu Varda dan Ulmo. Keempat Ainur tersebut diberi perintah oleh Eru untuk menjadi Client.
</br> Jadi inti dari soal 1 adalah Membuat tpologi jaringannya dulu, dengan komposisi : 
1 buah jaringan external </br>
1 buah Router (Eru) </br>
2 buah switch/gateway </br>
4 buah client </br>
DOKUMENTASI : </br>
<img width="553" height="386" alt="image" src="https://github.com/user-attachments/assets/aac4ae29-85a5-4d4b-a83b-0df76c74f6bd" />

### Soal 2 </br>
Karena menurut Eru pada saat itu Arda (Bumi) masih terisolasi dengan dunia luar, maka buat agar Eru dapat tersambung ke internet.
Perintah soal sebenarnya yaitu menghubungkan router serta gateway ke interet/jaringan eksternal, dengan cara mengubah dan mengkonfigurasi Eru dengan :
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.213.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.213.2.1
	netmask 255.255.255.0
```
`192.213.1.1` ini adalah gabungan dari IP Prefix dan alamat gateway
kemudian untuk memastikan bahwa sudah bisa terhubung ke jaringan kita sambungkan/akses jaringan pada terminal dengan `telnet 10.15.43.32 <alamat Eru>` jika suda berhasil maka bisa dilakukan ping ke google.com
</br> DOKUMENTASI : 
<img width="1259" height="594" alt="Screenshot 2025-09-29 195720" src="https://github.com/user-attachments/assets/a248d79f-6324-47a7-afb7-0cea58441e65" />

### Soal 3 </br>
Sekarang pastikan agar setiap Ainur (Client) dapat terhubung satu sama lain. Soal ini meminta kita agar setiap client bisa terhubung, caranya dengan mengubah dan mengkonfigurasi masing-masing client pada gateway dan IP Prefix
</br> Melkor
```
auto eth0
iface eth0 inet static
	address 192.213.1.2
	netmask 255.255.255.0
	gateway 192.213.1.1
```
</br> Manwe
```
auto eth0
iface eth0 inet static
	address 192.213.1.3
	netmask 255.255.255.0
	gateway 192.213.1.1
```
</br> Varda
```
auto eth0
iface eth0 inet static
	address 192.213.2.2
	netmask 255.255.255.0
	gateway 192.213.2.1
```
</br> Ulmo
```
auto eth0
iface eth0 inet static
	address 192.213.2.3
	netmask 255.255.255.0
	gateway 192.213.2.1
```
kemudian IP masing-masing client akan kita sambungkan, dengan melakukan beberapa langkah : 
</br> Install iptables pada linux dengan command `apt update && apt install iptables -y`
</br> Masukkan command `iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.213.0.0/16` yang berfungsi agar semua perangkat yang terhubung bisa mengakses jaringan eksternal

### Soal 4 </br>
Setelah berhasil terhubung, sekarang Eru ingin agar setiap Ainur (Client) dapat mandiri. Oleh karena itu pastikan agar setiap Client dapat tersambung ke internet
</br> Dengan Membuat tab linux baru untuk setiap client dan mencoba command yang disesuaikan dengan IP masing-masing client,
</br> Melkor
`telnet 10.15.43.32 5062`
</br> Manwe
`telnet 10.15.43.32 5025`
</br> Ulmo
`telnet 10.15.43.32 5043`
</br> Varda
`telnet 10.15.43.32 5033`
</br> kemudian untuk memastikan sudah tersambung dengan command : 
`echo nameserver 192.168.122.1 > /etc/resolv.conf`
`cat /etc/resolv.conf`
`ping google.com -c 5`

### Soal 5 </br>
Ainur terkuat Melkor tetap berusaha untuk menanamkan kejahatan ke dalam Arda (Bumi). Sebelum terjadi kerusakan, Eru dan para Ainur lainnya meminta agar semua konfigurasi tidak hilang saat semua node di restart.
</br> Dengan cara menambhakan script serta mengkonfig ulang Eru dengan :
```
up apt update && apt install iptables
up iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.242.0.0/16
up echo nameserver 192.168.122.1 > /etc/resolv.conf
```
### Soal 6 </br>
Setelah semua Ainur terhubung ke internet, Melkor mencoba menyusup ke dalam komunikasi antara Manwe dan Eru. Jalankan file berikut (link file) lalu lakukan packet sniffing menggunakan Wireshark pada koneksi antara Manwe dan Eru, lalu terapkan display filter untuk menampilkan semua paket yang berasal dari atau menuju ke IP Address Manwe. Simpan hasil capture tersebut sebagai bukti.
</br> Untuk mengerjakan soal no.6 harus menggunakan aplikasi GNS3 client, dengan langkah :
</br> - Install dan masuk menggunakan kredensial yang diberikan asisten
</br> - Kemudian ke menu file, dan pilih open project & project library lalu pilih sesuai dengan kelompok yang telah diplotting.
</br> <img width="1497" height="776" alt="Screenshot 2025-09-29 222354" src="https://github.com/user-attachments/assets/418a2b7d-0848-489b-90f7-48b2b39ef044" />
</br> - Setelah berhasil masuk pada project kelompok maka, akan muncul topologi jaringan yang sudah dibuat sebelumnya pada web
</br> <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2365d321-4964-4dd8-be55-23505439f7dd" />
</br> - Jangan lupa download file yang disediakan pada soal, file soal berisi traffic.sh yang didalamnya terdapat code :
</br> <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f4ccf626-4db7-428c-a0a8-a5101290ef01" />
</br> - Pada soal kita berperan sebagai Melkor, maka kita akan masuk sebagai Melkor pada terminal dengan menggonakan alamat Melkor yang sudah tersedia. Tapi sebelumnya kita akan mengcapture semua yang terjadi pada gateway 1 dengan start capture, maka otomatis wireshark akan terbuka
</br> <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0cf21c2e-219d-4a3f-a217-78685868724d" />
</br> <img width="1004" height="217" alt="Screenshot 2025-09-29 223455" src="https://github.com/user-attachments/assets/f316c3c4-e607-452d-b39b-512a5400abef" />
</br> - Ketika sudah masuk ke melkor, kita buat script dengan menyalin apa yang ada di dalam traffic.sh
</br> <img width="1558" height="863" alt="Screenshot 2025-09-29 223614" src="https://github.com/user-attachments/assets/f2d2eb97-656d-46d9-8512-232449991cf7" />
</br> - Jalankan script dengan command yang ada pada gambar, maka kemudian traffic akan berjalan
</br> <img width="857" height="160" alt="Screenshot 2025-09-29 223654" src="https://github.com/user-attachments/assets/6842e935-a14b-4a06-8e13-493545d84002" /> 
</br> - Ketika sudah 10 detik maka hentikan wireshark, dan gunakan filter `ip.addr == 192.213.1.2`
</b> - Kemudia simpan hasil capture yang sudah di filter tadi
</br> <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ecbbd3c0-c2cb-43bf-b9eb-5c426f72b331" />


### Soal 14 </br>
Setelah gagal mengakses FTP, Melkor melancarkan serangan brute force terhadap  Manwe. Analisis file capture yang disediakan dan identifikasi upaya brute force Melkor. 
(link file) nc 10.15.43.32 3401
</br> ![WhatsApp Image 2025-09-30 at 10 55 00_02e9b739](https://github.com/user-attachments/assets/9e217add-a202-4148-9fc7-225bd3bfb1ac)

### Soal 16 </br>
Melkor semakin murka ia meletakkan file berbahaya di server milik Manwe. Dari file capture yang ada, identifikasi file apa yang diletakkan oleh Melkor.
(link file) nc 10.15.43.32 3403
</br> ![WhatsApp Image 2025-09-30 at 13 40 47_adf98f93](https://github.com/user-attachments/assets/4dbf9836-02c6-4e77-af61-b5ab7df5c486)

### Soal 17 </br>
Manwe membuat halaman web di node-nya yang menampilkan gambar cincin agung. Melkor yang melihat web tersebut merasa iri sehingga ia meletakkan file berbahaya agar web tersebut dapat dianggap menyebarkan malware oleh Eru. Analisis file capture untuk menggagalkan rencana Melkor dan menyelamatkan web Manwe.
(link file) nc 10.15.43.32 3404
</br> ![WhatsApp Image 2025-09-30 at 14 21 38_d642a440](https://github.com/user-attachments/assets/97ab3aa5-9d26-454e-8928-2169400b2ace)

### Soal 18 </br>
Karena rencana Melkor yang terus gagal, ia akhirnya berhenti sejenak untuk berpikir. Pada saat berpikir ia akhirnya memutuskan untuk membuat rencana jahat lainnya dengan meletakkan file berbahaya lagi tetapi dengan metode yang berbeda. Gagalkan lagi rencana Melkor dengan mengidentifikasi file capture yang disediakan agar dunia tetap aman.
(link file) nc 10.15.43.32 3405
</br> ![WhatsApp Image 2025-09-30 at 14 38 25_ca1a8fb9](https://github.com/user-attachments/assets/3c099a9d-9b10-4838-8ce0-49780f5b5fcc)

### Soal 19 </br>
Manwe mengirimkan email berisi surat cinta kepada Varda melalui koneksi yang tidak terenkripsi. Melihat hal itu Melkor sipaling jahat langsung melancarkan aksinya yaitu meneror Varda dengan email yang disamarkan. Analisis file capture jaringan dan gagalkan lagi rencana busuk Melkor.
(link file) nc 10.15.43.32 3406
</br> ![WhatsApp Image 2025-09-30 at 15 18 37_f66e9b14](https://github.com/user-attachments/assets/5e103a03-30e3-4f8f-bcc0-b3e2a5089a94)

### Soal 20 </br>
Untuk yang terakhir kalinya, rencana besar Melkor yaitu menanamkan sebuah file berbahaya kemudian menyembunyikannya agar tidak terlihat oleh Eru. Tetapi Manwe yang sudah merasakan adanya niat jahat dari Melkor, ia menyisipkan bantuan untuk mengungkapkan rencana Melkor. Analisis file capture dan identifikasi kegunaan bantuan yang diberikan oleh Manwe untuk menggagalkan rencana jahat Melkor selamanya.
(link file) nc 10.15.43.32 3407
</br> ![WhatsApp Image 2025-09-30 at 16 06 20_bf704f00](https://github.com/user-attachments/assets/fdf82ecb-d053-437f-82a6-c4467b6d37fa)
