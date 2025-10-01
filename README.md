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
[Soal 6]</br>
[Soal 14]</br>
[Soal 16]</br>
[Soal 17]</br>
[Soal 18]</br>
[Soal 19]</br>
[Soal 20]</br>
[creds](#creds)</br>
[ATM or ATP or FTP ? 🤔](#atm-or-atp-or-ftp--🤔)</br>
[How Many packets ?!](#how-many-packets)</br>
