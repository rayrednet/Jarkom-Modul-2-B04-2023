# Laporan Resmi Praktikum Jaringan Komputer Modul 2 - DNS & Web Server

## Identitas Kelompok
| Nama                                 | NRP        |
| -------------------------------------|------------|
| Rayssa Ravelia                       | 5025211219 |
| Immanuel Pascanov Samosir            | 5025211257 |

## Daftar Isi
[Nomor 1](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-1) <br/>
[Nomor 2](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-2) <br/>
[Nomor 3](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-3) <br/>
[Nomor 4](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-4) <br/>
[Nomor 5](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-5) <br/>
[Nomor 6](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-6) <br/>
[Nomor 7](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-7) <br/>
[Nomor 8](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-8) <br/>
[Nomor 9](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-9) <br/>
[Nomor 10](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-10) <br/>
[Nomor 11](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-11) <br/>
[Nomor 12](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-12) <br/>
[Nomor 13](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-13) <br/>
[Nomor 14](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-14) <br/>
[Nomor 15](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-15) <br/>
[Nomor 16](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-16) <br/>
[Nomor 17](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-17) <br/>
[Nomor 18](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-18) <br/>
[Nomor 19](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-19) <br/>
[Nomor 20](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/#-nomor-20) <br/>

### ⭐ Nomor 1
### Soal
Yudhistira akan digunakan sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna merupakan Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Buatlah topologi dengan pembagian [sebagai berikut](https://docs.google.com/spreadsheets/d/1OqwQblR_mXurPI4gEGqUe7v0LSr1yJViGVEzpMEm2e8/edit#gid=1475903193). Folder topologi dapat diakses pada [drive berikut](https://drive.google.com/drive/folders/1Ij9J1HdIW4yyPEoDqU1kAwTn_iIxg3gk) 
### Jawaban
Berdasarkan soal tersebut, kelompok kami (B04) mendapatkan topologi no-8

<img width="275" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/7f8812be-db98-49d9-b717-300920969759">

Yang dimana topologi-8 sebagai berikut:

<img width="458" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/79a6b810-caf4-495c-9e36-5743ebac6bae">

Berikut ini adalah topologi yang telah dibuat sesuai dengan ketentuan:

<img width="700" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/45fa2d34-b858-49a2-93cd-a17d562f379b">

Adapun network configuration masing-masing node sebagai berikut:

Router
```
auto eth0
iface eth0 inet dhcp

auto eth1
iface eth1 inet static
	address 192.180.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.180.2.1
	netmask 255.255.255.0
```

NakulaClient
```
auto eth0
iface eth0 inet static
	address 192.180.1.2
	netmask 255.255.255.0
	gateway 192.180.1.1
```

SadewaClient
```
auto eth0
iface eth0 inet static
	address 192.180.1.3
	netmask 255.255.255.0
	gateway 192.180.1.1
```

AbimanyuWebServer
```
auto eth0
iface eth0 inet static
	address 192.180.1.4
	netmask 255.255.255.0
	gateway 192.180.1.1
```

PrabukusumaWebServer
```
auto eth0
iface eth0 inet static
	address 192.180.1.5
	netmask 255.255.255.0
	gateway 192.180.1.1
```

WisanggeniWebServer
```
auto eth0
iface eth0 inet static
	address 192.180.1.6
	netmask 255.255.255.0
	gateway 192.180.1.1
```

YudhistiraDNSMaster
```
auto eth0
iface eth0 inet static
	address 192.180.2.4
	netmask 255.255.255.0
	gateway 192.180.2.1
```

WerkudaraDNSSlave
```
auto eth0
iface eth0 inet static
	address 192.180.2.3
	netmask 255.255.255.0
	gateway 192.180.2.1
```

ArjugaLoadBalancer
```
auto eth0
iface eth0 inet static
	address 192.180.2.2
	netmask 255.255.255.0
	gateway 192.180.2.1
```
**Kendala:** Tidak ada kendala didalam mengerjakan nomor ini.


### ⭐ Nomor 2
### Soal
Buatlah website utama pada node arjuna dengan akses ke arjuna.yyy.com dengan alias www.arjuna.yyy.com dengan yyy merupakan kode kelompok.
### Jawaban
Untuk membuat website utama pada node arjuna dengan akses ke arjuna.B04.com dengan alias www.arjuna.B04.com kita harus membuatnya di dalam node Yudhistira. Hal ini dikarenakan Yudhistira berperan sebagai DNSMaster. Berikut ini adalah langkah-langkah yang harus dilakukan:
1. Buat direktori /etc/bind/arjuna/arjuna.B04.com dan copy file db.local ke dalam forlder arjuna yang baru dibuat
2. Kemudian arahkan ke /etc/bind/named.conf.local dan ubah menggunakan nano berikut

	<img width="538" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/767970a4-16e4-4832-98a1-044ead1d4889">

 	Pada file konfigurasi di atas digunakan untuk zone "arjuna.B04.com" dalam server DNS BIND.

	`zone "arjuna.B04.com"`: Ini adalah awalan konfigurasi zona yang menyatakan bahwa sedang mendefinisikan konfigurasi untuk zona dengan nama "arjuna.B04.com". Dalam DNS, "zone" merujuk pada wilayah domain yang dikelola oleh server DNS.
	
	`type master;`: Ini adalah tipe zona, yang dalam konteks ini diatur sebagai "master". Tipe "master" menunjukkan bahwa server DNS ini adalah sumber otoritatif untuk zona "arjuna.B04.com". Artinya, server ini adalah sumber utama yang memiliki catatan DNS untuk zona tersebut dan dapat menerima pembaruan terkait zona ini.
	
	`file "/etc/bind/arjuna/arjuna.B04.com";`: Ini adalah alamat file zona. Ini mengacu pada file yang berisi catatan DNS aktual untuk zona "arjuna.B04.com". File ini adalah tempat di mana akan mendefinisikan catatan A, CNAME, MX, NS, dan catatan DNS lainnya yang terkait dengan domain "arjuna.B04.com".
	
	Dengan konfigurasi ini, server DNS BIND telah diinformasikan bahwa ia adalah server otoritatif untuk zona "arjuna.B04.com", dan bahwa catatan DNS terkait dengan zona ini akan ditemukan dalam file "/etc/bind/arjuna/arjuna.B04.com". Ini memungkinkan server BIND untuk meresolusi permintaan DNS yang berkaitan dengan domain "arjuna.B04.com" dan mengembalikan informasi yang tepat.

4. Selanjutnya, ubah isi /etc/bind/arjuna/arjuna.B04.com menjadi seperti berikut:

   	<img width="516" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/c507f61e-ef98-4332-9422-a842d34869b3">
	
	File `/etc/bind/arjuna/arjuna.B04.com` adalah file zona yang mengandung catatan DNS untuk domain "arjuna.B04.com." Berikut inia dalah penjelasan setiap bagian dari file ini:

	1. `$TTL 604800`: Ini adalah TTL (Time to Live) default untuk catatan DNS dalam zona ini, diukur dalam detik. TTL menunjukkan berapa lama catatan DNS akan disimpan dalam cache DNS sebelum perlu diperbarui. Dalam hal ini, TTL diatur ke 604800 detik, yang setara dengan 1 minggu.
	
	2. `@ IN SOA arjuna.B04.com. root.arjuna.B04.com. (`: Ini adalah catatan SOA (Start of Authority), yang menunjukkan bahwa "arjuna.B04.com" adalah zona otoritatif, dan "root.arjuna.B04.com" adalah alamat email administrator. Bagian selanjutnya adalah parameter-parameter SOA:
	   - `2023100901` adalah nomor seri (serial number) zona. Ini adalah tanda waktu yang digunakan untuk mengidentifikasi pembaruan pada zona. Biasanya, akan diperbaharui nomor seri setiap kali Anda melakukan perubahan pada zona.
	   - `604800` adalah waktu segar (refresh), yaitu berapa sering server DNS lain harus memeriksa zona untuk perubahan. Dalam hal ini, 604800 detik adalah setara dengan 1 minggu.
	   - `86400` adalah waktu ulang (retry), yang menunjukkan berapa sering server DNS lain harus mencoba lagi jika gagal saat meminta zona.
	   - `2419200` adalah waktu kadaluwarsa (expire), yaitu berapa lama zona dapat dianggap valid sebelum harus diperbarui oleh sumber otoritatif. Dalam hal ini, 2419200 detik setara dengan 4 minggu.
	   - `604800` adalah TTL untuk cache negatif, yang mengatur berapa lama catatan DNS yang tidak ditemukan (misalnya, kesalahan DNS) akan disimpan dalam cache negatif.
	
	3. `@ IN NS arjuna.B04.com.`: Ini adalah catatan NS yang menunjukkan bahwa "arjuna.B04.com" adalah server Name Server (NS) yang bertanggung jawab atas zona ini. Dalam DNS, catatan NS mengarahkan ke server DNS yang memiliki otoritas atas zona.
	
	4. `@ IN A 192.180.2.2`: Ini adalah catatan A yang menghubungkan domain "arjuna.B04.com" ke alamat IP 192.180.2.2. Dengan demikian, ketika nama domain "arjuna.B04.com" dicari, ia akan dikembalikan dengan alamat IP ini (IP ArjunaLoadBalancer). Dipilih untuk menggunakan IP ini dikarenakan pada soal dikatakan domain ini mengarah ke node arjuna.
	
	5. `www IN CNAME arjuna.B04.com.`: Ini adalah catatan CNAME yang menunjukkan bahwa "www" adalah alias dari "arjuna.B04.com". Ini berarti jika seseorang mencari "www.arjuna.B04.com," ia akan diarahkan ke "arjuna.B04.com."
	
	6. `@ IN AAAA ::1`: Ini adalah catatan AAAA yang menghubungkan domain "arjuna.B04.com" ke alamat IPv6 "::1". Ini berlaku jika ada permintaan DNS untuk alamat IPv6 dari domain "arjuna.B04.com."

5. Kemudian restart service dengan
	```
	service bind9 restart
	```

 	Penting untuk dilakukan restart service BIND9 untuk mengaktifkan perubahan konfigurasi dan menerapkan perubahan zona yang dilakukan. 

Berikut ini adalah bash untuk perintah nomor 2
```
#!/bin/bash

# Membuat direktori /etc/bind/arjuna
mkdir -p /etc/bind/arjuna

# Membuat file arjuna.B04.com dan mengeditnya
cat <<EOL > /etc/bind/arjuna/arjuna.B04.com
;
; BIND data file for local loopback interface
;
\$TTL    604800
@       IN      SOA     arjuna.B04.com. root.arjuna.B04.com. (
                        2023100901      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      arjuna.B04.com.
@       IN      A       192.180.2.2        ; IP arjuna
www     IN      CNAME   arjuna.B04.com.
@       IN      AAAA    ::1
EOL

# Mengedit named.conf.local
echo 'zone "arjuna.B04.com" {' >> /etc/bind/named.conf.local
echo '    type master;' >> /etc/bind/named.conf.local
echo '    file "/etc/bind/arjuna/arjuna.B04.com";' >> /etc/bind/named.conf.local
echo '};' >> /etc/bind/named.conf.local

# Restart bind9 service
service bind9 restart

echo "Setup DNS telah selesai."
```

Untuk mengecek keadaan status arjuna.B04.com, kita dapat melakukan ping dari node lain. 

Sebagai contoh saya melakukan ping dari NakulaClient. Sebelum melakukan ping, kita harus memastikan bahwa nameserver yang terhubung di dalam /etc/resolv.conf adalah IP Yudhistira sebagai berikut:

<img width="522" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/4aa1beb6-ba7a-4d37-9ef0-02007eb51ddd">


Kemudian, dicoba untuk melakukan ping www.arjuna.B04.com dan arjuna.B04.com sebagai berikut:

<img width="435" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/0066140d-abde-451d-af79-e3fdfaa86455">

Berdasarkan hasil tersebut, dapat dilihat bahwa domain sudah berhasil dibuat. Pada hasil ping tersebut juga dapat dilihat ping berasal dari 192.180.2.2 yang merupakan IP ArjunaLoadBalancer.

**Kendala:** Tidak ada kendala didalam mengerjakan nomor ini.

### ⭐ Nomor 3
### Soal
Dengan cara yang sama seperti soal nomor 2, buatlah website utama dengan akses ke abimanyu.yyy.com dan alias www.abimanyu.yyy.com.
### Jawaban

Untuk membuat website utama dengan akses ke abimanyu.B04.com dengan alias www.abimanyu.B04.com, kita menggunakan cara yang sama seperti pada soal nomor 2. Hanya saja yang perlu diubah adalah nama arjuna menjadi abimanyu dan IP tujuannya mengarah ke IP AbimanyuWebServer. Berikut ini adalah langkah-langkahnya:

1. Buat direktori /etc/bind/abimanyu/abimanyu.B04.com dan copy file db.local ke dalam forlder arjuna yang baru dibuat
2. Kemudian arahkan ke /etc/bind/named.conf.local dan ubah menggunakan nano berikut

	<img width="512" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/f688e757-d252-4dff-b498-2052f84b84b0">

 	Pada file konfigurasi di atas digunakan untuk zone "abimanyu.B04.com" dalam server DNS BIND.
	
	`zone "abimanyu.B04.com" {`: Ini adalah awalan dari definisi zona. Ini menunjukkan bahwa kita akan mendefinisikan zona dengan nama "abimanyu.B04.com".
	
	`type master;`: Ini menunjukkan bahwa zona ini adalah zona master. Dalam konteks BIND, zona master adalah zona yang memiliki otoritas tertinggi atas catatan DNS di dalamnya. Ini berarti bahwa server BIND ini akan mengelola dan menyimpan informasi otoritatif untuk zona "abimanyu.B04.com" yang disebutkan dalam file ini.
	
	`file "/etc/bind/abimanyu/abimanyu.B04.com";`: Baris ini menentukan lokasi file zona yang berisi catatan DNS untuk "abimanyu.B04.com". Jadi, semua informasi DNS untuk zona ini akan disimpan dalam file yang ditunjukkan (dalam kasus ini, "/etc/bind/abimanyu/abimanyu.B04.com"). Ini adalah file zona yang akan digunakan oleh server BIND untuk merespons permintaan DNS terkait dengan "abimanyu.B04.com".
	
	Dengan konfigurasi ini, server BIND akan mengelola zona "abimanyu.B04.com" sebagai zona master dan akan menggunakan file "/etc/bind/abimanyu/abimanyu.B04.com" sebagai sumber otoritatif untuk semua catatan DNS yang ada di dalam zona tersebut. Semua perubahan terkait dengan zona "abimanyu.B04.com" harus diperbarui dalam file ini dan akan tersedia untuk resolusi DNS ketika diperlukan.

4. Selanjutnya, ubah isi /etc/bind/abimanyu/abimanyu.B04.com menjadi seperti berikut:

   	<img width="514" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/2184e9f5-43f8-4df3-91a0-37e1e271aba1">

File `/etc/bind/abimanyu/abimanyu.B04.com` adalah file zona DNS untuk domain "abimanyu.B04.com" dalam server DNS BIND. Ini adalah file yang digunakan untuk mengkonfigurasi catatan DNS yang terkait dengan domain tersebut. Berikut adalah penjelasan baris per baris dari isi file ini:

	1. `;`: Ini adalah komentar dalam file konfigurasi DNS. Baris yang dimulai dengan titik koma (;) adalah komentar dan tidak memengaruhi konfigurasi DNS. Ini digunakan untuk memberikan penjelasan atau dokumentasi.
	
	2. `$TTL 604800`: TTL (Time to Live) adalah parameter yang menentukan berapa lama catatan DNS dapat disimpan dalam cache. Dalam kasus ini, TTL diatur ke 604800 detik atau 1 minggu.
	
	3. `@ IN SOA abimanyu.B04.com. root.abimanyu.B04.com. (2023100901...`: Ini adalah catatan SOA (Start of Authority). Ini mendefinisikan informasi yang berkaitan dengan zona, termasuk:
	
	   - Nama Server Otoritatif (NS): "abimanyu.B04.com."
	   - Alamat email administrator: "root.abimanyu.B04.com."
	   - Nomor Serial: 2023100901
	   - Refresh: 604800 detik (7 hari)
	   - Retry: 86400 detik (1 hari)
	   - Expire: 2419200 detik (4 minggu)
	   - Negative Cache TTL: 604800 detik (7 hari)
	
	4. `@ IN NS abimanyu.B04.com.`: Ini adalah catatan NS (Name Server) yang menunjukkan bahwa "abimanyu.B04.com" adalah nama server otoritatif untuk zona "abimanyu.B04.com".
	
	5. `@ IN A 192.180.1.4`: Ini adalah catatan A (Address) yang menghubungkan domain "abimanyu.B04.com" ke alamat IP 192.180.1.4. Ini berarti ketika seseorang mencari "abimanyu.B04.com," server DNS akan memberikan alamat IP ini sebagai jawaban. IP ini adalah IP dari AbimanyuWebServer, dipilih IP ini sebab domain tersebut mengarah ke node abimanyu.
	
	6. `www IN CNAME abimanyu.B04.com.`: Ini adalah catatan CNAME (Canonical Name) yang mengaitkan subdomain "www" dengan "abimanyu.B04.com." Ini berarti bahwa ketika seseorang mencari "www.abimanyu.B04.com," itu akan diarahkan ke "abimanyu.B04.com."
	
	7. `@ IN AAAA ::1`: Ini adalah catatan AAAA yang memberikan alamat IPv6 (::1) untuk domain "abimanyu.B04.com." Ini menghubungkan domain ini dengan alamat IPv6 tertentu.
	
	File ini digunakan oleh server BIND untuk memberikan informasi DNS yang sesuai ketika ada permintaan yang berkaitan dengan zona "abimanyu.B04.com."
	 
5. Kemudian restart service dengan
	```
	service bind9 restart
	```
	Tujuan dari perintah "service bind9 restart" adalah untuk memulai ulang layanan BIND (Berkeley Internet Name Domain) yang bertanggung jawab atas server DNS. Dengan merestart BIND, diterapkan perubahan konfigurasi baru atau memperbaiki masalah yang terkait dengan layanan DNS tanpa harus memulai ulang seluruh server.

Berikut ini adalah file bash nomor 3
```
#!/bin/bash

# Membuat direktori /etc/bind/abimanyu
mkdir -p /etc/bind/abimanyu

# Membuat file abimanyu.B04.com dan mengeditnya
cat <<EOL > /etc/bind/abimanyu/abimanyu.B04.com
;
; BIND data file for local loopback interface
;
\$TTL    604800
@       IN      SOA     abimanyu.B04.com. root.abimanyu.B04.com. (
                        2023100901      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.B04.com.
@       IN      A       192.180.1.4        ; IP abimanyu
www     IN      CNAME   abimanyu.B04.com.
@       IN      AAAA    ::1
EOL

# Mengedit named.conf.local
echo 'zone "abimanyu.B04.com" {' >> /etc/bind/named.conf.local
echo '    type master;' >> /etc/bind/named.conf.local
echo '    file "/etc/bind/abimanyu/abimanyu.B04.com";' >> /etc/bind/named.conf.local
echo '};' >> /etc/bind/named.conf.local

# Restart bind9 service
service bind9 restart

echo "Setup DNS telah selesai dengan nama Abimanyu."
```

Untuk mengecek keadaan status abimanyu.B04.com, kita dapat melakukan ping dari node lain. 

Sebagai contoh saya melakukan ping dari SadewaClient. Sebelum melakukan ping, kita harus memastikan bahwa nameserver yang terhubung di dalam /etc/resolv.conf adalah IP Yudhistira sebagai berikut:

<img width="522" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/4aa1beb6-ba7a-4d37-9ef0-02007eb51ddd">

Kemudian, dicoba untuk melakukan ping www.abimanyu.B04.com dan abimanyu.B04.com sebagai berikut:

<img width="429" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/b8748f2c-9a18-436d-b3a9-cef21ec10951">

Berdasarkan hasil tersebut, dapat dilihat bahwa domain sudah berhasil dibuat. Pada hasil ping tersebut juga dapat dilihat ping berasal dari 192.180.1.4 yang merupakan IP AbimanyuWebServer.

**Kendala:** Tidak ada kendala didalam mengerjakan nomor ini.

### ⭐ Nomor 4
### Soal
Kemudian, karena terdapat beberapa web yang harus di-deploy, buatlah subdomain parikesit.abimanyu.yyy.com yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu.
### Jawaban
Untuk membuat subdomain parikesit.abimanyu.B04.com dengan abimanyu.B04.com sebagai domain utamanya, berikut ini adalah tahapan yang dilakukan:

1. Kita harus mengedit file dari /etc/bind/abimanyu/abimanyu.B04.com menjadi seperti berikut:
```
;
; BIND data file for local loopback interface
;
\$TTL    604800
@       IN      SOA     abimanyu.B04.com. root.abimanyu.B04.com. (
                        2023100901      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.B04.com.
@       IN      A       192.180.1.4        ; IP abimanyu
www     IN      CNAME   abimanyu.B04.com.
parikesit	IN	  A 	   192.180.1.4	 	; IP abimanyu
@       IN      AAAA    ::1
```

<img width="352" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/5c7673fc-8a0e-40ae-94ab-7cec05b67486">

	File `/etc/bind/abimanyu/abimanyu.B04.com` adalah file konfigurasi BIND, yang digunakan untuk mengatur zona DNS untuk domain `abimanyu.B04.com`.Berikut ini adalah pembahasan baris per baris:
	
	1. `; BIND data file for local loopback interface`: Ini adalah komentar untuk memberikan deskripsi tentang isi file. Ini tidak memengaruhi konfigurasi DNS.
	
	2. `$TTL 604800`: TTL (Time to Live) default untuk semua catatan dalam zona ini adalah 604800 detik, atau 1 minggu.
	
	3. `@ IN SOA abimanyu.B04.com. root.abimanyu.B04.com. (2023100901...`: Ini adalah catatan Start of Authority (SOA) yang mengatur otoritas untuk zona DNS. 
	
	   - `@` mengacu pada domain utama (`abimanyu.B04.com`).
	   - `IN` menunjukkan tipe catatan yang berlaku di sini (Internet).
	   - `SOA` adalah jenis catatan yang menunjukkan informasi otoritas.
	   - `abimanyu.B04.com.` adalah nama server otoritas.
	   - `root.abimanyu.B04.com.` adalah alamat email administrator DNS yang diakhiri dengan titik.
	   - `2023100901` adalah nomor seri untuk catatan ini. Ini harus ditingkatkan setiap kali ada perubahan dalam zona DNS.
	   - `604800` adalah nilai Refresh, yang menunjukkan berapa lama nama server sekunder harus menunggu sebelum memeriksa apakah ada perubahan di zona DNS ini.
	   - `86400` adalah nilai Retry, yang menunjukkan berapa lama nama server sekunder harus menunggu sebelum mencoba lagi jika terjadi kesalahan saat mengambil zona DNS ini.
	   - `2419200` adalah nilai Expire, yang menunjukkan berapa lama zona DNS akan dianggap kadaluarsa jika server sekunder tidak dapat menggunakannya.
	   - `604800` adalah Negative Cache TTL, yang menunjukkan berapa lama cache negatif (misalnya, jika sebuah domain tidak ada) akan berlaku.
	
	4. `@ IN NS abimanyu.B04.com.`: Ini adalah catatan Name Server (NS) yang menunjukkan bahwa server DNS yang bertanggung jawab untuk zona ini adalah `abimanyu.B04.com`.
	
	5. `@ IN A 192.180.1.4`: Ini adalah catatan Address (A) yang mengaitkan domain utama (`abimanyu.B04.com`) dengan alamat IP `192.180.1.4` (IP AbimanyuWebServer)
	
	6. `www IN CNAME abimanyu.B04.com.`: Ini adalah catatan Canonical Name (CNAME) yang mengaitkan subdomain `www` dengan `abimanyu.B04.com`. Ini berarti ketika seseorang mencoba mengakses `www.abimanyu.B04.com`, itu akan diarahkan ke `abimanyu.B04.com`.
	
	7. `parikesit IN A 192.180.1.4`: Ini adalah catatan Address (A) yang mengaitkan subdomain `parikesit` dengan alamat IP `192.180.1.4` (IP AbimanyuWebServer)
	
	8. `@ IN AAAA ::1`: Ini adalah catatan IPv6 Address (AAAA) yang mengaitkan domain utama (`abimanyu.B04.com`) dengan alamat IPv6 `::1`.
	
	File ini mengatur zona DNS untuk domain `abimanyu.B04.com` dengan beberapa catatan yang menghubungkan domain dan subdomain ke alamat IP atau alamat lainnya. 

2. Kemudian lakukan perintah 
```
service bind9 restart
```
Perintah tersebut digunakan untuk menerapkan konfigurasi yang sudah ditetapkan.


Berikut ini adalah file bash untuk soal nomor 4
```
#!/bin/bash

# Mengubah isi file /etc/bind/abimanyu/abimanyu.B04.com
cat <<EOL > /etc/bind/abimanyu/abimanyu.B04.com
;
; BIND data file for local loopback interface
\$TTL    604800
@       IN      SOA     abimanyu.B04.com. root.abimanyu.B04.com. (
                        2023100901      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.B04.com.
@       IN      A       192.180.1.4        ; IP abimanyu
www     IN      CNAME   abimanyu.B04.com.
parikesit	IN      A       192.180.1.4        ; IP abimanyu
@       IN      AAAA    ::1
EOL

# Restart bind9 service
service bind9 restart

echo "Isi file Abimanyu.B04.com telah diubah, dan bind9 telah di-restart."
```

Untuk mengecek subdomain tersebut, lakukan perintah
```
ping parikesit.abimanyu.B04.com -c 5
```

Sebagai contoh saya melakukan ping pada NakulaClient berikut:

<img width="321" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/901701ee-5396-4fed-bce4-aafb079973cc">

Dari hasil ping dapat dilihat bahwa ping berasal dari IP 192.180.1.4 yang merupakan IP AbimanyuWebServer.

**Kendala:** Tidak ada kendala didalam mengerjakan nomor ini.

### ⭐ Nomor 5
### Soal
Buat juga reverse domain untuk domain utama. (Abimanyu saja yang direverse)
### Jawaban
Untuk melakukan reverse domain utama pertama-tama kita harus mengedit file /etc/bind/named.conf.local di YudhistiraDNSMaster dengan menambahkan reverse 3 byte dari IP YudhistiraDNSMaster.
IP Yudhistira adalah `192.180.2.4` dengan 3 byte pertama `192.180.2` sehingga direverse menjadi `2.180.192`. Maka tambahkan pada file /etc/bind/named.conf.local sebagai berikut:
```
zone "2.180.192.in-addr.arpa." {
    type master;
    file "/etc/bind/abimanyu/2.180.192.in-addr.arpa";
};
```

Konfigurasi di atas adalah file konfigurasi BIND yang menentukan zona reverse DNS (zona arpa.in-addr) untuk alamat IP subnet 192.180.2.x. Berikut ini adalah pembahasan tiap barisnya:

1. `zone "2.180.192.in-addr.arpa." {`: Ini mendefinisikan zona reverse DNS. Zona reverse digunakan untuk mengaitkan alamat IP dengan nama domain, sebaliknya dari zona DNS biasa yang mengaitkan nama domain dengan alamat IP. "2.180.192.in-addr.arpa." adalah notasi terbalik untuk alamat IP subnet 192.180.2.x.

2. `type master;`: Ini menunjukkan bahwa zona ini adalah zona master, yang berarti server DNS ini memiliki otoritas penuh atas zona ini dan akan menggunakan file yang ditentukan untuk merespons permintaan DNS yang berkaitan dengan zona reverse ini.

3. `file "/etc/bind/abimanyu/2.180.192.in-addr.arpa";`: Ini adalah alamat file zona yang berisi catatan DNS untuk zona reverse ini. Catatan DNS dalam file ini akan menghubungkan alamat IP dengan nama domain terkait. Dengan kata lain, ini akan digunakan untuk mengatasi permintaan DNS terkait dengan alamat IP dalam subnet 192.180.2.x dan memberikan nama domain yang sesuai dengan alamat IP tersebut.

Dengan konfigurasi ini, server BIND akan merespons permintaan DNS reverse lookup untuk alamat IP dalam subnet 192.180.2.x dengan menggunakan informasi dalam file "/etc/bind/abimanyu/2.180.192.in-addr.arpa".

Langkah selanjutnya, copy file db.local ke dalam folder abimanyu dan ubah namanya menjadi `2.180.192.in-addr.arpa`

```
cp /etc/bind/db.local /etc/bind/abimanyu/2.180.192.in-addr.arpa
```

Selanjutnya, edit file /etc/bind/abimanyu/2.180.192.in-addr.arpa menggunakan:

```
nano /etc/bind/abimanyu/2.180.192.in-addr.arpa
```

Isi file tersebut sebagai berikut:
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.B04.com. root.abimanyu.B04.com. (
                        2023100901      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
2.180.192.in-addr.arpa.	IN	NS	abimanyu.B04.com.
4			IN	PTR	abimanyu.B04.com. ; Byte ke-4 YudhistiraDNSServer
```

File `/etc/bind/abimanyu/2.180.192.in-addr.arpa` adalah file zona reverse DNS yang mengaitkan alamat IP dengan nama domain, khususnya untuk subnet 192.180.2.x. Berikut adalah penjelasan isi file lebih detailnya:

1. `$TTL 604800`: Ini adalah pengaturan TTL (Time to Live) dalam detik. TTL menentukan berapa lama catatan DNS dapat disimpan dalam cache. Dalam hal ini, TTL diatur ke 604800 detik atau 1 minggu.

2. `@ IN SOA abimanyu.B04.com. root.abimanyu.B04.com. (2023100901...`: Ini adalah catatan SOA (Start of Authority) yang mendefinisikan informasi yang berkaitan dengan zona reverse DNS, termasuk:
   - Nama Server Otoritatif (NS): "abimanyu.B04.com."
   - Alamat email administrator: "root.abimanyu.B04.com."
   - Nomor Serial: 2023100901
   - Refresh: 604800 detik (7 hari)
   - Retry: 86400 detik (1 hari)
   - Expire: 2419200 detik (4 minggu)
   - Negative Cache TTL: 604800 detik (7 hari)

3. `2.180.192.in-addr.arpa. IN NS abimanyu.B04.com.`: Ini adalah catatan NS (Name Server) yang menunjukkan bahwa "abimanyu.B04.com" adalah nama server otoritatif untuk zona reverse DNS ini.

4. `4 IN PTR abimanyu.B04.com. ; Byte ke-4 YudhistiraDNSServer`: Ini adalah catatan PTR (Pointer) yang menghubungkan alamat IP 192.180.2.4 dengan nama domain "abimanyu.B04.com."

Dengan konfigurasi ini, server DNS akan menggunakan file ini untuk mengatasi permintaan reverse DNS lookup terkait dengan alamat IP dalam subnet 192.180.2.x dan akan memberikan nama domain yang sesuai dengan alamat IP tersebut.

Terakhir, jalankan perintah berikut untuk menerapkan konfigurasi yang ditentukan.
```
service bind9 restart
```

Untuk mengecek konfigurasi sudah benar, saya melakukan testing pada SadewaClient. Pastikan sudah dilakukan perintah berikut:

```
apt-get update
apt-get install dnsutils
```

Berikut ini adalah konfigurasi yang saya tambahkan di bashrc pada SadewaClient dan juga NakulaClient:

<img width="359" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/24fa1438-5d44-4a2a-af2e-b723e6136e84">


<img width="359" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/0bdb0764-b9ba-476b-b84f-81f3ee8f200a">


Kita juga harus memastikan nameserver adalah YudhistiraDNSMaster

<img width="357" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/ac948df6-41e0-4da2-adaf-d04d548971ec">

Untuk mengecek reverse domain jalankan perintah

```
host -t PTR 192.180.2.4
```

Diperoleh sebagai berikut:

<img width="292" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/1205d90b-4606-4ed9-9089-e85a8767679f">


Dari hasil tersebut dapat dilihat bahwa hasil reverse mengarah ke abimanyu.B04.com yang berarti reverse domain ini sudah benar.

Berikut ini adalah script bash untuk nomor 5:
```
#!/bin/bash

# 1. Menambahkan konfigurasi zone pada /etc/bind/named.conf.local
echo 'zone "2.180.192.in-addr.arpa." {' >> /etc/bind/named.conf.local
echo '    type master;' >> /etc/bind/named.conf.local
echo '    file "/etc/bind/abimanyu/2.180.192.in-addr.arpa";' >> /etc/bind/named.conf.local
echo '};' >> /etc/bind/named.conf.local

# 2. Menyalin file db.local ke direktori /etc/bind/abimanyu/2.180.192.in-addr.arpa
cp /etc/bind/db.local /etc/bind/abimanyu/2.180.192.in-addr.arpa

# 3. Mengganti isi file /etc/bind/abimanyu/2.180.192.in-addr.arpa
cat <<EOL > /etc/bind/abimanyu/2.180.192.in-addr.arpa
;
; BIND data file for local loopback interface
;
\$TTL    604800
@       IN      SOA     abimanyu.B04.com. root.abimanyu.B04.com. (
                        2023100901      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
2.180.192.in-addr.arpa.    IN  NS  abimanyu.B04.com.
4           IN  PTR abimanyu.B04.com. ; Byte ke-4 YudhistiraDNSServer
EOL

# 4. Restart layanan bind9
service bind9 restart
```

**Kendala:** Tidak ada kendala didalam mengerjakan nomor ini.

### ⭐ Nomor 6
### Soal
Agar dapat tetap dihubungi ketika DNS Server Yudhistira bermasalah, buat juga Werkudara sebagai DNS Slave untuk domain utama.
### Jawaban
Untuk soal ini kita melakukan konfigurasi untuk Yudhistira sebagai DNS Master dan Werkudara sebagai DNS Slave. Konfigurasi ini dilakukan pada kedua node sebagai berikut:

1. Konfigurasi pada Yudhistira
   
Untuk membuat DNS Slave pada Werkudara, kita harus mengubah file /etc/bind/named.conf.local di Yudhistira pada zone abimanyu.B04.com menjadi:
```
zone “abimanyu.B04.com" {
    	type master;
	notify yes;
	also-notify { 192.180.2.3; }; //IP Werkudara DNS Slave
	allow-transfer { 192.180.2.3; };
    	file "/etc/bind/abimanyu/abimanyu.B04.com";
};
```

Konfigurasi pada file `/etc/bind/named.conf.local` di server DNS Yudhistira untuk membuat DNS Slave (server DNS sekunder) untuk zona DNS `abimanyu.B04.com`. Berikut adalah penjelasan dari konfigurasi tersebut:

1. `zone "abimanyu.B04.com" {`: Ini adalah awal dari definisi zona DNS untuk domain `abimanyu.B04.com`.

2. `type master;`: Ini mengatur tipe zona DNS menjadi "master", yang berarti Yudhistira adalah server DNS utama yang memiliki otoritas penuh atas zona DNS ini.

3. `notify yes;`: Ini mengaktifkan pemberitahuan kepada server DNS slave ketika ada perubahan dalam zona DNS ini. Ini memungkinkan server sekunder (DNS Slave) untuk secara otomatis mendapatkan pembaruan ketika terjadi perubahan pada zona ini.

4. `also-notify { 192.180.2.3; };`: Ini adalah daftar alamat IP yang akan diberitahu ketika ada perubahan pada zona DNS. Dalam hal ini, hanya IP `192.180.2.3` (server DNS Slave di Werkudara) yang akan diberitahu.

5. `allow-transfer { 192.180.2.3; };`: Ini mengizinkan transfer zona ke server DNS slave dengan alamat IP `192.180.2.3`. Ini diperlukan untuk memungkinkan server DNS slave untuk menyalin zona DNS dari server utama (master).

6. `file "/etc/bind/abimanyu/abimanyu.B04.com";`: Ini menentukan lokasi file zona DNS yang akan digunakan oleh server DNS master. Zona DNS untuk `abimanyu.B04.com` akan diambil dari file `/etc/bind/abimanyu/abimanyu.B04.com`.

Dengan konfigurasi ini, Yudhistira akan berfungsi sebagai server DNS master untuk zona `abimanyu.B04.com`, dan Werkudara (yang memiliki IP `192.180.2.3`) akan menjadi server DNS slave yang akan secara otomatis mengikuti perubahan pada zona DNS ini dan menggantinya jika diperlukan.

Kemudian lakukan restart service untuk menerapkan konfigurasi
```
service bind9 restart
```
2. Konfigurasi pada Werkudara

Berikut ini adalah hal-hal yang dilakukan untuk melakukan konfigurasi pada WerkudaraDNSSlave:
Pertama-tama buka /etc/bind/named.conf.local dan tambahkan:
```
zone "abimanyu.B04.com" {
    type slave;
    masters { 192.180.2.4; }; // IP Yudhistira
    file "/var/lib/bind/abimanyu.B04.com";
};

Konfigurasi tersebut adalah langkah-langkah yang perlu dilakukan di server DNS sekunder (DNS Slave) di Werkudara untuk mengonfigurasi zona DNS `abimanyu.B04.com`. Berikut adalah penjelasan dari konfigurasi tersebut:

1. `zone "abimanyu.B04.com" {`: Ini adalah awal dari definisi zona DNS untuk domain `abimanyu.B04.com`.

2. `type slave;`: Ini mengatur tipe zona DNS menjadi "slave", yang menunjukkan bahwa Werkudara adalah server DNS sekunder yang akan mendapatkan zona DNS dari server utama (YudhistiraDNSMaster).

3. `masters { 192.180.2.4; };`: Ini adalah daftar alamat IP server DNS master yang akan digunakan oleh server DNS slave untuk mengambil zona DNS. Dalam hal ini, hanya ada satu server master, yaitu Yudhistira dengan alamat IP `192.180.2.4`.

4. `file "/var/lib/bind/abimanyu.B04.com";`: Ini menentukan lokasi di mana zona DNS yang diambil dari server master akan disimpan di server DNS slave. Zona DNS untuk `abimanyu.B04.com` akan disimpan di direktori `/var/lib/bind` dengan nama file `abimanyu.B04.com`.

Dengan konfigurasi ini, Werkudara akan berfungsi sebagai server DNS slave yang akan secara teratur meminta pembaruan zona DNS dari Yudhistira (server master) dan menyimpannya di direktori `/var/lib/bind`. Ini memungkinkan Werkudara untuk memiliki salinan yang akurat dari zona DNS `abimanyu.B04.com`, dan jika ada perubahan di server master, Werkudara akan secara otomatis mengikuti pembaruan tersebut.

```
dan lakukan perintah berikut untuk menerapkan konfigurasi:
```
service bind9 restart
```
3. Testing

Untuk melakukan testing, sebagai contoh saya melakukannya pada NakulaClient.
Pertama-tama, matikan YudhistiraDNSMaster dengan:
```
service bind9 stop
```

<img width="360" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/95e596bc-504f-4807-913c-6193cc3ee748">

Selanjutnya pastikan pengaturan nameserver mengarah ke IP Yudhistira dan IP Werkudara di /etc/resolv.conf

<img width="236" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/d76676db-2d70-4601-9ca5-8c8b2666584a">

Kemudian lakukan ping abimanyu.B04.com pada NakulaClient

<img width="339" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/c194fc99-b8f3-43a7-bc75-8734cba22e73">

Berdasarkan hasil tersebut dapat dilihat bahwa ping berasal dari 192.180.1.4, yang dimana itu merupakan IP AbimanyuWebServer. Maka dapat disimpulkan bahwa ketika DNSMaster dimatikan kita tetap dapat mengakses domain yang telah diregister melalui DNSSlave yaitu Werkudara.

Berikut ini adalah file bash untuk nomor 6 di node YudhistiraDNSMaster
```
#!/bin/bash

# Mencari dan menghapus zona "abimanyu.B04.com"
sed -i '/zone "abimanyu\.B04\.com" {/,/};/d' /etc/bind/named.conf.local

# Menambahkan zona "abimanyu.B04.com" yang baru
cat <<EOL >> /etc/bind/named.conf.local
zone "abimanyu.B04.com" {
    type master;
    notify yes;
    also-notify { 192.180.2.3; }; //IP Werkudara DNS Slave
    allow-transfer { 192.180.2.3; };
    file "/etc/bind/abimanyu/abimanyu.B04.com";
};
EOL

# Menjalankan service bind9 restart
service bind9 restart
```

Berikut ini adalah file bash untuk nomor 6 di node WerkudaraDNSSlave
```
#!/bin/bash

# Tambahkan konfigurasi zona ke /etc/bind/named.conf.local
echo 'zone "abimanyu.B04.com" {' >> /etc/bind/named.conf.local
echo '    type slave;' >> /etc/bind/named.conf.local
echo '    masters { 192.180.2.4; }; // IP Yudhistira' >> /etc/bind/named.conf.local
echo '    file "/var/lib/bind/abimanyu.B04.com";' >> /etc/bind/named.conf.local
echo '};' >> /etc/bind/named.conf.local

# Restart layanan bind9
service bind9 restart
```

**Kendala:** Tidak ada kendala didalam mengerjakan nomor ini.

### ⭐ Nomor 7
### Soal
Seperti yang kita tahu karena banyak sekali informasi yang harus diterima, buatlah subdomain khusus untuk perang yaitu baratayuda.abimanyu.yyy.com dengan alias www.baratayuda.abimanyu.yyy.com yang didelegasikan dari Yudhistira ke Werkudara dengan IP menuju ke Abimanyu dalam folder Baratayuda.
### Jawaban
Untuk melakukan delegasi di dalam folder Baratayuda, kita harus melakukan konfigurasi di node Yudhistira dan Werkudara. Berikut ini adalah tahapannya:

1. Konfigurasi di Yudhistira

Pertama-tama, kita harus mengubah isi file dari /etc/bind/abimanyu/abimanyu.B04.com menjadi:
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     abimanyu.B04.com. root.abimanyu.B04.com. (
                        2023100901      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       	IN      NS      abimanyu.B04.com.
@       	IN      A       192.180.2.4        ; IP Yudhistira
www     	IN      CNAME   abimanyu.B04.com.
parikesit	IN	A	192.180.1.4	; IP Abimayu
ns1		IN	A	192.180.2.3	; IP Werkudara
baratayuda	IN	NS	ns1
@       	IN      AAAA    ::1
```

<img width="505" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/ca8c8ba1-7ba7-4b84-9c66-2a5dd6959dfc">

File `/etc/bind/abimanyu/abimanyu.B04.com` adalah file konfigurasi zona DNS untuk domain `abimanyu.B04.com`. Berikut ini adalah pembahasan baris per baris:

	1. `; BIND data file for local loopback interface`: Ini adalah komentar yang memberikan deskripsi tentang isi file. Ini tidak memengaruhi konfigurasi DNS.
	
	2. `$TTL 604800`: TTL (Time to Live) default untuk semua catatan dalam zona ini adalah 604800 detik, atau 1 minggu.
	
	3. `@ IN SOA abimanyu.B04.com. root.abimanyu.B04.com. (2023100901...`: Ini adalah catatan Start of Authority (SOA) yang mengatur otoritas untuk zona DNS. Penjelasan rinci adalah sebagai berikut:
	
	   - `@` mengacu pada domain utama (`abimanyu.B04.com`).
	   - `IN` menunjukkan tipe catatan yang berlaku di sini (Internet).
	   - `SOA` adalah jenis catatan yang menunjukkan informasi otoritas.
	   - `abimanyu.B04.com.` adalah nama server otoritas.
	   - `root.abimanyu.B04.com.` adalah alamat email administrator DNS yang diakhiri dengan titik.
	   - `2023100901` adalah nomor seri untuk catatan ini. Ini harus ditingkatkan setiap kali ada perubahan dalam zona DNS.
	   - `604800` adalah nilai Refresh, yang menunjukkan berapa lama nama server sekunder harus menunggu sebelum memeriksa apakah ada perubahan di zona DNS ini.
	   - `86400` adalah nilai Retry, yang menunjukkan berapa lama nama server sekunder harus menunggu sebelum mencoba lagi jika terjadi kesalahan saat mengambil zona DNS ini.
	   - `2419200` adalah nilai Expire, yang menunjukkan berapa lama zona DNS akan dianggap kadaluarsa jika server sekunder tidak dapat menggunakannya.
	   - `604800` adalah Negative Cache TTL, yang menunjukkan berapa lama cache negatif (misalnya, jika sebuah domain tidak ada) akan berlaku.
	
	4. `@ IN NS abimanyu.B04.com.`: Ini adalah catatan Name Server (NS) yang menunjukkan bahwa server DNS yang bertanggung jawab untuk zona ini adalah `abimanyu.B04.com`.
	
	5. `@ IN A 192.180.2.4`: Ini adalah catatan Address (A) yang mengaitkan domain utama (`abimanyu.B04.com`) dengan alamat IP `192.180.2.4`. Ini menghubungkan nama domain ke alamat IP AbimanyuWebServer.
	
	6. `www IN CNAME abimanyu.B04.com.`: Ini adalah catatan Canonical Name (CNAME) yang mengaitkan subdomain `www` dengan `abimanyu.B04.com`. Ini berarti ketika seseorang mencoba mengakses `www.abimanyu.B04.com`, itu akan diarahkan ke `abimanyu.B04.com`.
	
	7. `parikesit IN A 192.180.1.4`: Ini adalah catatan Address (A) yang mengaitkan subdomain `parikesit` dengan alamat IP `192.180.1.4`.
	
	8. `ns1 IN A 192.180.2.3`: Ini adalah catatan Address (A) yang mengaitkan subdomain `ns1` dengan alamat IP `192.180.2.3`.
	
	9. `baratayuda IN NS ns1`: Ini adalah catatan Name Server (NS) yang menunjukkan bahwa subdomain `baratayuda` ditangani oleh server DNS `ns1`.
	
	10. `@ IN AAAA ::1`: Ini adalah catatan IPv6 Address (AAAA) yang mengaitkan domain utama (`abimanyu.B04.com`) dengan alamat IPv6 `::1`.

Dalam file ini, zona DNS untuk `abimanyu.B04.com` dikonfigurasi dengan berbagai catatan yang menghubungkan domain dan subdomain ke alamat IP atau alamat lainnya, serta menentukan otoritas untuk zona ini dengan catatan SOA.

Selanjutnya edit file /etc/bind/named.conf.options dengan cara:
```
nano /etc/bind/named.conf.options
```

Di dalam file tersebut lakukan comment `dnssec-validation auto;` dan tambahkan baris berikut pada /etc/bind/named.conf.options
```
allow-query{any;};
```

Maka file /etc/bind/named.conf.options menjadi:
```
options {
	directory "/var/cache/bind";


        // If there is a firewall between you and nameservers you want
        // to talk to, you may need to fix the firewall to allow multiple
        // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

        // If your ISP provided one or more IP addresses for stable
        // nameservers, you probably want to use them as forwarders.
        // Uncomment the following block, and insert the addresses replacing
        // the all-0's placeholder.

        // forwarders {
        //      0.0.0.0;
        // };

        //========================================================================
        // If BIND logs error messages about the root key being expired,
        // you will need to update your keys.  See https://www.isc.org/bind-keys
        //========================================================================
        //dnssec-validation auto;
        allow-query{any;};

        auth-nxdomain no;    # conform to RFC1035
	listen-on-v6 { any; };
};
```

<img width="520" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/402b9abb-4002-4859-a59c-3263ee8990c5">

`//dnssec-validation auto;`: Ini adalah comment yang mematikan konfigurasi DNSSEC validation. DNSSEC adalah sebuah mekanisme keamanan yang digunakan untuk memverifikasi integritas data DNS, dan dalam konfigurasi ini, fitur DNSSEC validation dimatikan (dijadikan komentar)

`allow-query { any; };`: dalam konfigurasi BIND DNS mengatur siapa yang diizinkan untuk melakukan permintaan DNS ke server.

`auth-nxdomain no;`: mengatur parameter auth-nxdomain menjadi no. Ketika opsi ini diaktifkan (dalam konfigurasi standar), server DNS akan mengembalikan pesan NXDOMAIN (Non-Existent Domain) yang dikonfirmasi secara otentik jika domain yang dicari tidak ada dalam zona. Namun, dengan opsi ini dinonaktifkan (dijadikan komentar), server DNS tidak akan mengembalikan pesan NXDOMAIN yang dikonfirmasi otentik, yang dapat menghasilkan sedikit lebih cepat.


Selanjutnya, lakukan service restart untuk menerapkan konfigurasi
```
service bind9 restart
```

2. Konfigurasi pada Werkudara

Langkah pertama adalah lakukan perintah:
```
nano /etc/bind/named.conf.options
```
Kemudian comment `dnssec-validation auto;` dan tambahkan baris berikut pada /etc/bind/named.conf.options
```
allow-query{any;};
```

Maka menjadi seperti berikut:

<img width="522" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/d3456652-edb4-407e-8fb3-a0edf25c7347">

Selanjutnya, lakukan perintah berikut:
```
mkdir /etc/bind/baratayuda
cp /etc/bind/db.local /etc/bind/baratayuda/baratayuda.abimanyu.B04.com
```

Pada file /etc/bind/named.conf.local tambahkan di bagian bawah:
```
zone "baratayuda.abimanyu.B04.com" {
	type master;
 	file "/etc/bind/baratayuda/baratayuda.abimanyu.B04.com";
};
```


<img width="356" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/15e8a346-05c6-4b47-8006-2d53e692129e">

Penambahan zona tersebut digunakan untuk memberikan delegasi pada baratayuda sehingga berhasil melakukan register domain pada DNSSlave.

Kemudian edit file /etc/bind/baratayuda/baratayuda.abimanyu.B04.com menjadi seperti ini:

```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     baratayuda.abimanyu.B04.com. root.abimanyu.B04.com. (
                        2023100901      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       	IN      NS     	baratayuda.abimanyu.B04.com.
@       	IN      A      	192.180.1.4	; IP Abimanyu
www.baratayuda	IN	CNAME	baratayuda.abimanyu.B04.com
@       	IN      AAAA    ::1
```

<img width="359" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/5f55cf3f-5d0e-479c-937c-354a23d0da6d">


Selanjutnya lakukan restart untuk menerapkan konfigurasi
```
service bind9 restart
```

3. Testing

Untuk melakukan contoh tes, kami melakukan pada SadewaClient. Pastikan bahwa pada /etc/resolv.conf mengarah kepada IP Yudhistira dan Werkudara.

Kemudian lakukan ping berikut:
```
ping baratayuda.abimanyuB04.com -c 5
```
diperoleh sebagai berikut:

<img width="313" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/e4a4811f-0124-4caa-9cb6-658d61b1c4f5">

Berdasarkan hasil ping tersebut dapat dilihat bahwa hasil ping diperoleh dari IP 192.180.1.4 yang merupakan IP dari AbimanyuWebServer.

Berikut ini adalah file bash untuk nomor 7 di node Yudhistira
```
#!/bin/bash

# Mengubah isi file abimanyu.B04.com
cat <<EOL > /etc/bind/abimanyu/abimanyu.B04.com
;
; BIND data file for local loopback interface
;
\$TTL    604800
@       IN      SOA     abimanyu.B04.com. root.abimanyu.B04.com. (
                        2023100901      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      abimanyu.B04.com.
@       IN      A       192.180.2.4        ; IP Yudhistira
www     IN      CNAME   abimanyu.B04.com.
parikesit       IN      A       192.180.1.4      ; IP Abimayu
ns1     IN      A       192.180.2.3      ; IP Werkudara
baratayuda	IN      NS      ns1
www.baratayuda	IN	CNAME	baratayuda.abimanyu.B04.com
@       IN      AAAA    ::1
EOL

# Mengubah isi file named.conf.options
cat <<EOL > /etc/bind/named.conf.options
options {
        directory "/var/cache/bind";

        // If there is a firewall between you and nameservers you want
        // to talk to, you may need to fix the firewall to allow multiple
        // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

        // If your ISP provided one or more IP addresses for stable
        // nameservers, you probably want to use them as forwarders.
        // Uncomment the following block, and insert the addresses replacing
        // the all-0's placeholder.

        // forwarders {
        //      0.0.0.0;
        // };

        //========================================================================
        // If BIND logs error messages about the root key being expired,
        // you will need to update your keys.  See https://www.isc.org/bind-keys
        //========================================================================
        //dnssec-validation auto;
        allow-query { any; };

        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
};
EOL

# Restart layanan bind9
service bind9 restart

```

Berikut ini adalah file bash untuk nomor 7 di node Werkudara

```
#!/bin/bash

# Mengubah isi file named.conf.options
cat <<EOL > /etc/bind/named.conf.options
options {
        directory "/var/cache/bind";

        // If there is a firewall between you and nameservers you want
        // to talk to, you may need to fix the firewall to allow multiple
        // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

        // If your ISP provided one or more IP addresses for stable
        // nameservers, you probably want to use them as forwarders.
        // Uncomment the following block, and insert the addresses replacing
        // the all-0's placeholder.

        // forwarders {
        //      0.0.0.0;
        // };

        //========================================================================
        // If BIND logs error messages about the root key being expired,
        // you will need to update your keys.  See https://www.isc.org/bind-keys
        //========================================================================
        //dnssec-validation auto;
        allow-query { any; };

        auth-nxdomain no;    # conform to RFC1035
        listen-on-v6 { any; };
};
EOL

# Membuat direktori /etc/bind/baratayuda
mkdir -p /etc/bind/baratayuda

# Menyalin file db.local ke /etc/bind/baratayuda/baratayuda.abimanyu.B04.com
cp /etc/bind/db.local /etc/bind/baratayuda/baratayuda.abimanyu.B04.com

# Mengedit named.conf.local untuk menambahkan zona baru
cat <<EOL >> /etc/bind/named.conf.local
zone "baratayuda.abimanyu.B04.com" {
    type master;
    file "/etc/bind/baratayuda/baratayuda.abimanyu.B04.com";
};
EOL

# Mengubah isi file /etc/bind/baratayuda/baratayuda.abimanyu.B04.com
cat <<EOL > /etc/bind/baratayuda/baratayuda.abimanyu.B04.com
;
; BIND data file for local loopback interface
;
\$TTL    604800
@       IN      SOA     baratayuda.abimanyu.B04.com. root.abimanyu.B04.com. (
                        2023100901      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      baratayuda.abimanyu.B04.com.
@       IN      A       192.180.1.4      ; IP Abimayu
@       IN      AAAA    ::1
EOL

# Restart layanan bind9
service bind9 restart
```

**Kendala:** Tidak ada kendala didalam mengerjakan nomor ini.

### ⭐ Nomor 8 (Werkudara)
### Soal
Untuk informasi yang lebih spesifik mengenai Ranjapan Baratayuda, buatlah subdomain melalui Werkudara dengan akses rjp.baratayuda.abimanyu.yyy.com dengan alias www.rjp.baratayuda.abimanyu.yyy.com yang mengarah ke Abimanyu.
### Jawaban

Untuk membuat subdomain melalui werkudara yang mengarah ke abimanyu, kita harus mengubahnya pada WerkudaraDNSSlave.

Pertama-tama ubah /etc/bind/baratayuda/baratayuda.abimanyu.B04.com menjadi seperti berikut:

```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     baratayuda.abimanyu.B04.com. root.abimanyu.B04.com. (
                        2023100901      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       	IN      NS     	baratayuda.abimanyu.B04.com.
@       	IN      A      	192.180.1.4	; IP Abimanyu
rjp		IN	A	192.180.1.4	; IP Abimanyu
www.rjp		IN	CNAME	baratayuda.abimanyu.B04.com.
@       	IN      AAAA    ::1
```

<img width="355" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/b4e1043d-2f31-4a32-b852-17a3c034db3d">

Dari perubahan diatas ditambahkan subdomain untuk rjp dan juga alias www.rjp sesuai dengan perintah soal yang keduanya mengarah ke IP Abimanyu.

Selanjutnya lakukan service bind9 restart untuk menerapkan konfigurasi

```
service bind9 restart
```

Untuk melakukan testing, saya melakukan testing pada SadewaClient dengan menjalankan:
```
ping rjp.baratayuda.abimanyu.B04.com
```
dan juga
```
ping www.rjp.baratayuda.abimanyu.B04.com
```

diperoleh hasil ping sebagai berikut:

<img width="332" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/3a637f1c-19de-43cc-ba2e-4bdd1120fcf9">

Berdasarkan hasil ping tersebut dapat dilihat bahwa kedua ping mengarah ke IP yang sama, yaitu IP 192.180.1.4 (IP AbimanyuWebServer).

Berikut ini adalah script bash untuk nomor 8:

```
#!/bin/bash

# Nama file yang akan diubah
file="/etc/bind/baratayuda/baratayuda.abimanyu.B04.com"

# Isi file yang baru
new_content=";
; BIND data file for local loopback interface
;
\$TTL    604800
@       IN      SOA     baratayuda.abimanyu.B04.com. root.abimanyu.B04.com. (
                        2023100901      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       	IN      NS     	baratayuda.abimanyu.B04.com.
@       	IN      A      	192.180.1.4	; IP Abimanyu
rjp		IN	A	192.180.1.4	; IP Abimanyu
www.rjp		IN	CNAME	baratayuda.abimanyu.B04.com.
@       	IN      AAAA    ::1
"

# Mengganti isi file
echo "$new_content" > "$file"

# Merestart layanan BIND9
service bind9 restart

echo "File $file telah diubah, dan layanan BIND9 telah di-restart."
```
**Kendala:** Tidak ada kendala didalam mengerjakan nomor ini.

### ⭐ Nomor 9
### Soal
Arjuna merupakan suatu Load Balancer Nginx dengan tiga worker (yang juga menggunakan nginx sebagai webserver) yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Lakukan deployment pada masing-masing worker.
### Jawaban

Berdasarkan soal, load balancernya adalah Arjuna dengan 3 worker yaitu Prabakusuma, Abimanyu, dan Wisanggeni. 
Pertama-tama, lakukan setting di Yudhistira
```
 apt-get update && apt install nginx php php-fpm -y
```
Pada soal load balancernya adalah arjuna maka yang dipakai adalah arjuna.B04.com

Lakukan tes ping arjuna.B04.com di client

<img width="314" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/6d835f77-f6ed-42f0-91c9-e998313d8b2d">

#### AbimanyuWebServer
jalankan perintah 
```
 apt-get update && apt install nginx php php-fpm -y
```
buat direktori
```
mkdir /var/www/arjuna
```

masuk direktori /var/www/arjuna lalu buat file index.php dengan isi file
```
 <?php
 echo "Halo, Kamu berada di AbimanyuWebServer";
 ?>
```

selanjutnya kita akan melakukan konfigurasi pada Nginx, pertama masuk ke direktori /etc/nginx/sites-available lalu buat file baru dengan nama arjuna
Isi file arjuna dengan ini
```
 server {

 	listen 80;
	listen 8002;

 	root /var/www/arjuna;

 	index index.php index.html index.htm;
 	server_name _;

 	location / {
 			try_files $uri $uri/ /index.php?$query_string;
 	}

 	# pass PHP scripts to FastCGI server
 	location ~ \.php$ {
 	include snippets/fastcgi-php.conf;
 	fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
 	}

 location ~ /\.ht {
 			deny all;
 	}

 	error_log /var/log/nginx/arjuna_error.log;
 	access_log /var/log/nginx/arjuna_access.log;
 }
```
Kemudian, buat symlink
```
 ln -s /etc/nginx/sites-available/arjuna /etc/nginx/sites-enabled
```
Terus, lakukan 
```
service nginx restart
```

script bash abimanyu
```
#!/bin/bash

# Membuat direktori /var/www/arjuna
mkdir -p /var/www/arjuna

# Membuat file index.php
echo "<?php
\$hostname = gethostname();
\$date = date('Y-m-d H:i:s');
\$php_version = phpversion();
\$username = get_current_user();

echo 'Hello World!<br>';
echo 'Saya adalah: ' . \$username . '<br>';
echo 'Saat ini berada di: ' . \$hostname . '<br>';
echo 'Versi PHP yang saya gunakan: ' . \$php_version . '<br>';
echo 'Tanggal saat ini: ' . \$date . '<br>';
?>" > /var/www/arjuna/index.php

# Membuat file konfigurasi Nginx di /etc/nginx/sites-available/arjuna
echo "server {

    listen 80;

    root /var/www/arjuna;

    index index.php index.html index.htm;
    server_name _;

    location / {
        try_files \$uri \$uri/ /index.php?\$query_string;
    }

    # pass PHP scripts to FastCGI server
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }

    error_log /var/log/nginx/arjuna_error.log;
    access_log /var/log/nginx/arjuna_access.log;
}" > /etc/nginx/sites-available/arjuna


# Membuat symlink ke direktori sites-enabled
ln -s /etc/nginx/sites-available/arjuna /etc/nginx/sites-enabled

# Merestart layanan Nginx
service nginx restart

echo "Konfigurasi Abimanyu selesai."
```

#### PrabukusumaWebServer
jalankan perintah 
```
 apt-get update && apt install nginx php php-fpm -y
```
buat direktori
```
mkdir /var/www/arjuna
```

masuk direktori /var/www/arjuna lalu buat file index.php dengan isi file
```
 <?php
 echo "Halo, Kamu berada di PrabukusumaWebServer";
 ?>
```

selanjutnya kita akan melakukan konfigurasi pada Nginx, pertama masuk ke direktori /etc/nginx/sites-available lalu buat file baru dengan nama arjuna
Isi file arjuna dengan ini
```
 server {

 	listen 80;

 	root /var/www/arjuna;

 	index index.php index.html index.htm;
 	server_name _;

 	location / {
 			try_files $uri $uri/ /index.php?$query_string;
 	}

 	# pass PHP scripts to FastCGI server
 	location ~ \.php$ {
 	include snippets/fastcgi-php.conf;
 	fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
 	}

 location ~ /\.ht {
 			deny all;
 	}

 	error_log /var/log/nginx/arjuna_error.log;
 	access_log /var/log/nginx/arjuna_access.log;
 }
```
Kemudian, buat symlink
```
 ln -s /etc/nginx/sites-available/arjuna /etc/nginx/sites-enabled
```
Terus, lakukan 
```
service nginx restart
```

script bash prabukusuma
```
#!/bin/bash

# Membuat direktori /var/www/arjuna
mkdir -p /var/www/arjuna

# Membuat file index.php
echo "<?php
\$hostname = gethostname();
\$date = date('Y-m-d H:i:s');
\$php_version = phpversion();
\$username = get_current_user();

echo 'Hello World!<br>';
echo 'Saya adalah: ' . \$username . '<br>';
echo 'Saat ini berada di: ' . \$hostname . '<br>';
echo 'Versi PHP yang saya gunakan: ' . \$php_version . '<br>';
echo 'Tanggal saat ini: ' . \$date . '<br>';
?>" > /var/www/arjuna/index.php

# Membuat file konfigurasi Nginx di /etc/nginx/sites-available/arjuna
echo "server {

    listen 80;
listen 8001;

    root /var/www/arjuna;

    index index.php index.html index.htm;
    server_name _;

    location / {
        try_files \$uri \$uri/ /index.php?\$query_string;
    }

    # pass PHP scripts to FastCGI server
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }

    error_log /var/log/nginx/arjuna_error.log;
    access_log /var/log/nginx/arjuna_access.log;
}" > /etc/nginx/sites-available/arjuna


# Membuat symlink ke direktori sites-enabled
ln -s /etc/nginx/sites-available/arjuna /etc/nginx/sites-enabled

# Merestart layanan Nginx
service nginx restart

echo "Konfigurasi Prabukusuma selesai."
```

#### WisanggeniWebServer
jalankan perintah 
```
 apt-get update && apt install nginx php php-fpm -y
```
buat direktori
```
mkdir /var/www/arjuna
```

masuk direktori /var/www/arjuna lalu buat file index.php dengan isi file
```
 <?php
 echo "Halo, Kamu berada di WisanggeniWebServer";
 ?>
```

selanjutnya kita akan melakukan konfigurasi pada Nginx, pertama masuk ke direktori /etc/nginx/sites-available lalu buat file baru dengan nama arjuna
Isi file arjuna dengan ini
```
 server {

 	listen 80;
	listen 8003;

 	root /var/www/arjuna;

 	index index.php index.html index.htm;
 	server_name _;

 	location / {
 			try_files $uri $uri/ /index.php?$query_string;
 	}

 	# pass PHP scripts to FastCGI server
 	location ~ \.php$ {
 	include snippets/fastcgi-php.conf;
 	fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
 	}

 location ~ /\.ht {
 			deny all;
 	}

 	error_log /var/log/nginx/arjuna_error.log;
 	access_log /var/log/nginx/arjuna_access.log;
 }
```
Kemudian, buat symlink
```
 ln -s /etc/nginx/sites-available/arjuna /etc/nginx/sites-enabled
```
Terus, lakukan 
```
service nginx restart
```

script bash wisanggeni
```
#!/bin/bash

# Membuat direktori /var/www/arjuna
mkdir -p /var/www/arjuna

# Membuat file index.php
echo "<?php
\$hostname = gethostname();
\$date = date('Y-m-d H:i:s');
\$php_version = phpversion();
\$username = get_current_user();

echo 'Hello World!<br>';
echo 'Saya adalah: ' . \$username . '<br>';
echo 'Saat ini berada di: ' . \$hostname . '<br>';
echo 'Versi PHP yang saya gunakan: ' . \$php_version . '<br>';
echo 'Tanggal saat ini: ' . \$date . '<br>';
?>" > /var/www/arjuna/index.php

# Membuat file konfigurasi Nginx di /etc/nginx/sites-available/arjuna
echo "server {

    listen 80;

    root /var/www/arjuna;

    index index.php index.html index.htm;
    server_name _;

    location / {
        try_files \$uri \$uri/ /index.php?\$query_string;
    }

    # pass PHP scripts to FastCGI server
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }

    error_log /var/log/nginx/arjuna_error.log;
    access_log /var/log/nginx/arjuna_access.log;
}" > /etc/nginx/sites-available/arjuna


# Membuat symlink ke direktori sites-enabled
ln -s /etc/nginx/sites-available/arjuna /etc/nginx/sites-enabled

# Merestart layanan Nginx
service nginx restart

echo "Konfigurasi Wisanggeni selesai."
```
#### ArjunaLoadBalancer
pertama -tama pastikan sudah dilakukan

```
apt-get update && apt install nginx
```
buat file baru di direktori /etc/nginx/sites-available dengan nama lb-arjuna

Isi file lb-arjuna menjadi
```
 # Default menggunakan Round Robin
 upstream myweb  {
 	server 192.180.1.4; #IP abimanyu
 	server 192.180.1.5; #IP prabukusuma
 	server 192.180.1.6; #IP wisanggeni
 }

 server {
 	listen 80;
 	server_name arjuna.B04.com;

 	location / {
 	proxy_pass http://myweb;
 	}
 }
```

Lalu simpan lalu buat symlink

```
 ln -s /etc/nginx/sites-available/lb-arjuna /etc/nginx/sites-enabled
```

script bash arjunaloadbalancer
```
#!/bin/bash

# Membuat file konfigurasi Nginx lb-arjuna di /etc/nginx/sites-available
echo "# Default menggunakan Round Robin
upstream myweb  {
    server 192.180.1.4; # IP abimanyu
    server 192.180.1.5; # IP prabukusuma
    server 192.180.1.6; # IP wisanggeni
}

server {
    listen 80;
    server_name arjuna.B04.com;

    location / {
        proxy_pass http://myweb;
    }
}" > /etc/nginx/sites-available/lb-arjuna

# Membuat symlink ke direktori sites-enabled
ln -s /etc/nginx/sites-available/lb-arjuna /etc/nginx/sites-enabled

# Merestart layanan Nginx
service nginx restart

echo "Konfigurasi lb-arjuna selesai."

```

#### Testing Client
sebagai contoh testing di nakula
pertama tama pastikan sudah ada
```
apt-get update && apt-get install lynx
```

lalu ketikkan
```
lynx http://arjuna.B04.com
```

**Kendala:** Tidak ada kendala didalam mengerjakan nomor ini.

### ⭐ Nomor 10
### Soal
Kemudian gunakan algoritma Round Robin untuk Load Balancer pada Arjuna. Gunakan server_name pada soal nomor 1. Untuk melakukan pengecekan akses alamat web tersebut kemudian pastikan worker yang digunakan untuk menangani permintaan akan berganti ganti secara acak. Untuk webserver di masing-masing worker wajib berjalan di port 8001-8003. Contoh
    - Prabakusuma:8001
    - Abimanyu:8002
    - Wisanggeni:8003
### Jawaban
Selanjutnya, kita akan melakukan penyesuaian port pada server-server tersebut sesuai dengan petunjuk yang telah diberikan. Karena telah berhasil melakukan deployment pada nomor 9. Berikutnya, kita perlu untuk mengubah masing-masing port pada worker menuju port yang telah ditentukan yaitu Prabakusuma:8001, Abimanyu:8002, Wisanggeni:8003. Kita juga perlu mengubah port load-balancing dengan menambahkan :800X pada masing-masing server.

**Arjuna (Load Balancing)**
- Pada ArjunaLoadBalancer, yang diubah dari no 9 adalah isi file `lb-arjuna` menjadi sebagai berikut:
  ```
  # Default menggunakan Round Robin
  upstream myweb  {
    server 192.180.1.4: 8002; #IP abimanyu
    server 192.180.1.5: 8001; #IP prabukusuma
    server 192.180.1.6: 8003; #IP wisanggeni
  }

  server {
    listen 80;
    server_name arjuna.B04.com;

    location / {
    proxy_pass http://myweb;
    }
  }
  server {
    listen 8001;
    server_name arjuna.B04.com;

    location / {
    proxy_pass http://myweb;
    }
  }
  server {
    listen 8002;
    server_name arjuna.B04.com;

    location / {
    proxy_pass http://myweb;
    }
  }
  server {
    listen 8003;
    server_name arjuna.B04.com;

    location / {
    proxy_pass http://myweb;
    }
  }
  ```
- Lalu jalankan `service nginx restart`.

**Prabakusuma**

Pada Prabakusuma, edit file arjuna pada root, hapus `listen 80` dan tambahkan `listen 8001` pada konfigurasi server block.
```
server {

 	listen 8001;

 	root /var/www/arjuna;

 	index index.php index.html index.htm;
 	server_name _;

 	location / {
 			try_files $uri $uri/ /index.php?$query_string;
 	}

 	# pass PHP scripts to FastCGI server
 	location ~ \.php$ {
 	include snippets/fastcgi-php.conf;
 	fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
 	}

 location ~ /\.ht {
 			deny all;
 	}

 	error_log /var/log/nginx/arjuna_error.log;
 	access_log /var/log/nginx/arjuna_access.log;
 }
```

**Abimanyu**

Pada Abimanyu, edit file arjuna pada root, hapus `listen 80` dan tambahkan `listen 8002` pada konfigurasi server block.
```
server {

 	listen 8002;

 	root /var/www/arjuna;

 	index index.php index.html index.htm;
 	server_name _;

 	location / {
 			try_files $uri $uri/ /index.php?$query_string;
 	}

 	# pass PHP scripts to FastCGI server
 	location ~ \.php$ {
 	include snippets/fastcgi-php.conf;
 	fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
 	}

 location ~ /\.ht {
 			deny all;
 	}

 	error_log /var/log/nginx/arjuna_error.log;
 	access_log /var/log/nginx/arjuna_access.log;
 }
```

**Wisanggeni**

Pada Wisanggeni, edit file arjuna pada root, hapus `listen 80` dan tambahkan `listen 8003` pada konfigurasi server block.
```
server {

 	listen 8003;

 	root /var/www/arjuna;

 	index index.php index.html index.htm;
 	server_name _;

 	location / {
 			try_files $uri $uri/ /index.php?$query_string;
 	}

 	# pass PHP scripts to FastCGI server
 	location ~ \.php$ {
 	include snippets/fastcgi-php.conf;
 	fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
 	}

 location ~ /\.ht {
 			deny all;
 	}

 	error_log /var/log/nginx/arjuna_error.log;
 	access_log /var/log/nginx/arjuna_access.log;
 }
```
### Testing
Pada client Nakula, pastikan pada `/etc/resolv.conf` terdapat nameserver yudhistira dan werkudara dan install dependencies `apt-get update && apt-get install lynx` (dimasukkan ke .bashrc).

- Testing dengan menjalankan `lynx http://arjuna.B04.com:8001`
![imageprabukusuma10](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89269231/75ac4361-0f7f-48a4-87fa-d064f0fb5dfd)
- Testing dengan menjalankan `lynx http://arjuna.B04.com:8002`
![imageabimanyu10](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89269231/7be2f5d6-0fdb-42e7-b167-d8c08bdbe4ed)

- Testing dengan menjalankan `lynx http://arjuna.B04.com:8003`
![imagewisanggeni10](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89269231/30a8f65a-c40e-4ff0-9615-7063df9b3084)

### ⭐ Nomor 11
### Soal
Selain menggunakan Nginx, lakukan konfigurasi Apache Web Server pada worker Abimanyu dengan web server www.abimanyu.yyy.com. Pertama dibutuhkan web server dengan DocumentRoot pada /var/www/abimanyu.yyy
### Jawaban

**Abimanyu**
- Di root, simpan file `abimanyu.B04.com.conf`, dan isinya sebagai berikut:
  ```shell
  <VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/abimanyu.B04
    ServerName abimanyu.B04.com
    ServerAlias www.abimanyu.B04.com

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
  </VirtualHost>  
  ```
- Buat directory var/www/abimanyu.B04
- Untuk mengambil asset dari resource untuk webserver abimanyu.B04.com, digunakan metode git clone dari repository `http.sslVerify=false clone https://github.com/bombshelll/abimanyu.B04.com` yang akan di copy kedalam directory /var/www/abimanyu.B04


Script bash pada Webserver Abimanyu
```
service nginx stop

rm -r /var/www/abimanyu.B04

cp abimanyu.B04.com.conf /etc/apache2/sites-available/abimanyu.B04.com.conf

a2ensite abimanyu.B04.com.conf

mkdir -p /var/www/abimanyu.B04
apt-get install git -y
git -c http.sslVerify=false clone https://github.com/bombshelll/abimanyu.B04.com /var/www/abimanyu.B04

service apache2 restart
```

### Testing
Pada client Nakula, testing dengan menjalankan `lynx http://abimanyu.B04.com/index.php/home`

**Kendala:** Tidak ada kendala didalam mengerjakan nomor ini.

### ⭐ Nomor 12
### Soal
Setelah itu ubahlah agar url www.abimanyu.yyy.com/index.php/home menjadi www.abimanyu.yyy.com/home.
### Jawaban
**Abimanyu**
- Di dalam `abimanyu.B04.com.conf`, tambahkan:
  ```shell
  <VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/abimanyu.B04
    ServerName abimanyu.B04.com
    ServerAlias www.abimanyu.B04.com

    <Directory /var/www/abimanyu.B04/index.php/home>
          Options +Indexes
    </Directory>

    Alias "/home" "/var/www/abimanyu.B04/index.php/home"

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
  </VirtualHost>  
  ```

### Testing
Pada client Nakula, testing dengan menjalankan
`lynx http://abimanyu.B04.com/home`

**Kendala:** Tidak ada kendala didalam mengerjakan nomor ini.

### ⭐ Nomor 13
### Soal
Selain itu, pada subdomain www.parikesit.abimanyu.yyy.com, DocumentRoot disimpan pada /var/www/parikesit.abimanyu.yyy
### Jawaban
**Abimanyu**
- Di root, simpan file `parikesit.abimanyu.B04.com.conf`, dan isinya sebagai berikut:
  ```shell
  <VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/parikesit.abimanyu.B04
    ServerName parikesit.abimanyu.B04.com
    ServerAlias www.parikesit.abimanyu.B04.com

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
  </VirtualHost>  
  ```
- Buat directory var/www/parikesit.abimanyu.B04
- Untuk mengambil asset dari resource untuk webserver parikesit.abimanyu.B04.com, digunakan metode git clone dari repository `http.sslVerify=false clone https://github.com/bombshelll/parikesit.abimanyu.B04.com` yang akan di copy kedalam directory /var/www/parikesit.abimanyu.B04

Script bash pada Webserver Abimanyu
```
service nginx stop

rm -r /var/www/parikesit.abimanyu.B04

cp parikesit.abimanyu.B04.com.conf /etc/apache2/sites-available/parikesit.abimanyu.B04.com.conf

a2ensite parikesit.abimanyu.B04.com.conf

mkdir -p /var/www/parikesit.abimanyu.B04
apt-get install git -y
git -c http.sslVerify=false clone https://github.com/bombshelll/parikesit.abimanyu.B04.com /var/www/parikesit.abimanyu.B04

service apache2 restart
```

### Testing
Pada client Nakula, testing dengan menjalankan `lynx http://parikesit.abimanyu.B04.com/index.php/home`


**Kendala:** Tidak ada kendala didalam mengerjakan nomor ini.

### ⭐ Nomor 14
### Soal
Pada subdomain tersebut folder /public hanya dapat melakukan directory listing sedangkan pada folder /secret tidak dapat diakses (403 Forbidden).
### Jawaban

**Abimanyu**

Jalankan script di bawah ini, dimana untuk directory public, menggunakan `+Indexes` sedangkan pada directory secret menggunakan `-Indexes`.
Script bash pada Webserver Abimanyu
  ```shell
  echo '<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/parikesit.abimanyu.B04
  ServerName parikesit.abimanyu.B04.com
  ServerAlias www.parikesit.abimanyu.B04.com

  <Directory /var/www/parikesit.abimanyu.B04/public>
          Options +Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.B04/secret>
          Options -Indexes
  </Directory>

  Alias "/public" "/var/www/parikesit.abimanyu.B04/public"
  Alias "/secret" "/var/www/parikesit.abimanyu.B04/secret"

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
  </VirtualHost>' > /etc/apache2/sites-available/parikesit.abimanyu.B04.com.conf

  service apache2 restart
  ```

### Testing
Pada client Nakula, testing dengan menjalankan:
- lynx parikesit.abimanyu.B04.com/public


- lynx parikesit.abimanyu.B04.com/secret



**Kendala:** Tidak ada kendala didalam mengerjakan nomor ini.

### ⭐ Nomor 15
### Soal
Buatlah kustomisasi halaman error pada folder /error untuk mengganti error kode pada Apache. Error kode yang perlu diganti adalah 404 Not Found dan 403 Forbidden.
### Jawaban
**Abimanyu**
Jalankan script di bawah ini, dimana untuk error dengan kode 404, menggunakan `ErrorDocument 404 /error/404.html` dan untuk error kode 403 menggunakan `ErrorDocument 403 /error/403.html`.
Script bash pada Webserver Abimanyu
  ```shell
  echo '<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/parikesit.abimanyu.B04
  ServerName parikesit.abimanyu.B04.com
  ServerAlias www.parikesit.abimanyu.B04.com

  <Directory /var/www/parikesit.abimanyu.B04/public>
          Options +Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.B04/secret>
          Options -Indexes
  </Directory>

  Alias "/public" "/var/www/parikesit.abimanyu.B04/public"
  Alias "/secret" "/var/www/parikesit.abimanyu.B04/secret"

  ErrorDocument 404 /error/404.html
  ErrorDocument 403 /error/403.html

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
  </VirtualHost>' > /etc/apache2/sites-available/parikesit.abimanyu.B04.com.conf

  service apache2 restart
  ```

### Testing
Pada client Nakula, testing dengan menjalankan:
- lynx parikesit.abimanyu.B04.com/asalasalan

- lynx parikesit.abimanyu.B04.com/secret



**Kendala:** Tidak ada kendala didalam mengerjakan nomor ini.

### ⭐ Nomor 16
### Soal
Buatlah suatu konfigurasi virtual host agar file asset www.parikesit.abimanyu.yyy.com/public/js menjadi 
www.parikesit.abimanyu.yyy.com/js 
### Jawaban

### ⭐ Nomor 17
### Soal
Agar aman, buatlah konfigurasi agar www.rjp.baratayuda.abimanyu.yyy.com hanya dapat diakses melalui port 14000 dan 14400.
### Jawaban

### ⭐ Nomor 18
### Soal
Untuk mengaksesnya buatlah autentikasi username berupa “Wayang” dan password “baratayudayyy” dengan yyy merupakan kode kelompok. Letakkan DocumentRoot pada /var/www/rjp.baratayuda.abimanyu.yyy.
### Jawaban
Dalam membuat autentikasi sesuai dengan perintah soal lakukan pada node Abimanyu di dalam file `rjp.baratayuda.abimanyu.B04.com.conf` sebagai berikut:
```
  echo '<VirtualHost *:14000 *:14400>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/rjp.baratayuda.abimanyu.B04
  ServerName rjp.baratayuda.abimanyu.B04.com
  ServerAlias www.rjp.baratayuda.abimanyu.B04.com

    <Directory /var/www/html/rjp.baratayuda.abimanyu.B04>
        AuthType Basic
        AuthName "Protected"
        AuthUserFile /etc/apache2/.htpasswd
        Require valid-user
    <Directory>

  ErrorDocument 404 /error/404.html
  ErrorDocument 403 /error/403.html

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
  </VirtualHost>' > /etc/apache2/sites-available/rjp.baratayuda.abimanyu.B04.com.conf

  service apache2 restart
```

Selanjutnya, untuk kita menjalankan pada Abimanyu untuk setup username dan password dengan menjalankan 
```
htpasswd -c /etc/apache2/.htpasswd Wayang
```
 Kemudian set password menjadi baratayudaB04

![image](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/e70dfb8f-4551-4493-aa31-878ff52dc5ef)


### ⭐ Nomor 19
### Soal
Buatlah agar setiap kali mengakses IP dari Abimanyu akan secara otomatis dialihkan ke www.abimanyu.yyy.com (alias)
### Jawaban
Untuk melakukan soal nomor ini, kita harus membuat scrip bash pada node Abimanyu. Di dalam folder `abimanyu-redirect.conf` diisi seperti berikut:
```
<VirtualHost *:80>
    ServerAdmin webmaster@abimanyu.B04.com
    DocumentRoot /var/www/abimanyu.B04

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    Redirect / http://www.abimanyu.B04.com/
</VirtualHost>
```

Berikut ini adalah file bash untuk nomor 19:

```
#!bin/bash
cp abimanyu-redirect.conf /etc/apache2/sites-available/000-default.conf
a2ensite abimanyu-redirect.conf
apache2ctl configtest
service apache2 restart
```

Sebagai testing, kita jalankan pada client Nakula dengan:
```
lynx 192.180.1.4
```
diperoleh hasil sebagai berikut:

![image](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/5d06f9e1-354a-4f55-8f95-8953231bc2d0)


### ⭐ Nomor 20
### Soal
Karena website www.parikesit.abimanyu.yyy.com semakin banyak pengunjung dan banyak gambar gambar random, maka ubahlah request gambar yang memiliki substring “abimanyu” akan diarahkan menuju abimanyu.png.
### Jawaban
Berdasarkan soal tersebut, semua url yang mengandung kata "abimanyu" akan menuju "abimanyu.png". Oleh karena itu, kita harus melakukan konfigurasi di AbimanyuWebServer. Pada Abimanyu kita juga harus melakukan rewrite modul
```
a2enmod rewrite
```

Kemudian jalankan program ini untuk direktori parikesit.abimanyu.B04
```
echo 'RewriteEngine On
RewriteCond %{REQUEST_URI} ^/public/images/(.*)(abimanyu)(.*\.(png|jpg))
RewriteCond %{REQUEST_URI} !/public/images/abimanyu.png
RewriteRule abimanyu http://parikesit.abimanyu.B04.com/public/images/abimanyu.png$1 [L,R=301]' > /var/www/parikesit.abimanyu.B04/.htaccess
```

Selanjutnya ubah konfigurasi dan gunakan `AllowOverride All` 
```
echo -e '<VirtualHost *:80>
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/parikesit.abimanyu.B04

  ServerName parikesit.abimanyu.B04.com
  ServerAlias www.parikesit.abimanyu.B04.com

  <Directory /var/www/parikesit.abimanyu.B04/public>
          Options +Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.B04/secret>
          Options -Indexes
  </Directory>

  <Directory /var/www/parikesit.abimanyu.B04>
          Options +FollowSymLinks -Multiviews
          AllowOverride All
  </Directory>

  Alias "/public" "/var/www/parikesit.abimanyu.B04/public"
  Alias "/secret" "/var/www/parikesit.abimanyu.B04/secret"
  Alias "/js" "/var/www/parikesit.abimanyu.a09/public/js"

  ErrorDocument 404 /error/404.html
  ErrorDocument 403 /error/403.html

  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>' > /etc/apache2/sites-available/parikesit.abimanyu.B04.com.conf

service apache2 restart
```

Untuk testing dilakukan pada client, sebagai contoh Sadewa sebagai berikut:
```
lynx parikesit.abimanyu.B04.com/public/images/not-abimanyu.png
lynx parikesit.abimanyu.B04.com/public/images/abimanyu-student.jpg
lynx parikesit.abimanyu.B04.com/public/images/abimanyu.png
lynx parikesit.abimanyu.B04.com/public/images/notabimanyujustmuseum.177013
```

Berikut ini adalah hasil saat dijalankan:

