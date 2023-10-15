# Laporan Resmi Praktikum Jaringan Komputer Modul 2 - DNS & Web Server

## Identitas Kelompok
| Nama                                 | NRP        |
| -------------------------------------|------------|
| Rayssa Ravelia                       | 5025211219 |
| Immanuel Pascanov Samosir            | 5025211257 |

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

### ⭐ Nomor 4
### Soal
Kemudian, karena terdapat beberapa web yang harus di-deploy, buatlah subdomain parikesit.abimanyu.yyy.com yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu.
### Jawaban
Untuk membuat subdomain parikesit.abimanyu.B04.com, kita harus mengedit file dari /etc/bind/abimanyu/abimanyu.B04.com menjadi seperti berikut:
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

kemudian lakukan perintah 
```
service bind9 restart
```

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

<img width="359" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/3b4ff62c-8095-4d1f-bbc7-e6ff75a7385d">


### ⭐ Nomor 5
### Soal
Buat juga reverse domain untuk domain utama. (Abimanyu saja yang direverse)
### Jawaban
Untuk melakukan reverse domain utama pertama-tama kita harus mengedit file /etc/bind/named.conf.local di YudhistiraDNSMaster dengan meanmbahkan reverse 3 byte dari IP YudhistiraDNSMaster.
IP Yudhistira adalah 192.180.2.4 dengan 3 byte pertama 192.180.2 sehingga direverse menjadi 2.180.192. Maka tambahkan pada file /etc/bind/named.conf.local sebagai berikut:
```
zone "2.180.192.in-addr.arpa." {
    type master;
    file "/etc/bind/abimanyu/2.180.192.in-addr.arpa";
};
```

Kemudian, copy file db.local ke dalam folder abimanyu dan ubah namanya menjadi 2.180.192.in-addr.arpa

```
cp /etc/bind/db.local /etc/bind/abimanyu/2.180.192.in-addr.arpa
```

Selanjutnya, edit file 2.180.192.in-addr.arpa menjadi
nano /etc/bind/abimanyu/2.180.192.in-addr.arpa
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
Lalu jalankan
```
service bind9 restart
```

Untuk mengecek konfigurasi sudah benar, saya melakukan testing pada client Nakula. Pastikan ini sudah ada

```
apt-get update
apt-get install dnsutils
```

ubah  /etc/resolv.conf dan pastikan namserver adalah YudhistiraDNSMaster
kemudian jalankan perintah
```
host -t PTR 192.180.2.4
```

Diperoleh sebagai berikut:

<img width="359" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/3f8ae4ea-a448-4e12-a927-2ed98cb39c11">

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

### ⭐ Nomor 6 (Yudhistira & Werkudara)
### Soal
Agar dapat tetap dihubungi ketika DNS Server Yudhistira bermasalah, buat juga Werkudara sebagai DNS Slave untuk domain utama.
### Jawaban

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
Kemudian lakukan
```
service bind9 restart
```

Selanjutnya, lakukan konfigurasi pada WerkudaraDNSSlave
Buka /etc/bind/named.conf.local dan tambahkan:
```
zone "abimanyu.B04.com" {
    type slave;
    masters { 192.180.2.4; }; // IP Yudhistira
    file "/var/lib/bind/abimanyu.B04.com";
};
```
dan lakukan perintah 
```
service bind9 restart
```

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

dan file bash di node WerkudaraDNSSlave
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

Untuk memastikan koneksi berjalan sesuai, kita dapat melakukan tes pada client

Pastikan pengaturan nameserver mengarah ke IP Yudhistira dan IP Werkudara di /etc/resolv.conf

Lalu, lakukan ping abimanyu.B04.com, kalau berhasil ke 192.180.1.4 (ip point abimanyu) 
Berikut ini adalah hasil tesnya:

<img width="360" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/eb2067ef-fbdc-4da5-873b-f4418b486b89">

### ⭐ Nomor 7 (Yudhistira & Werkudara)
### Soal
Seperti yang kita tahu karena banyak sekali informasi yang harus diterima, buatlah subdomain khusus untuk perang yaitu baratayuda.abimanyu.yyy.com dengan alias www.baratayuda.abimanyu.yyy.com yang didelegasikan dari Yudhistira ke Werkudara dengan IP menuju ke Abimanyu dalam folder Baratayuda.
### Jawaban

Pertama-tama, kita harus melakukan delegasi dari Yudhitira ke Werdukara dengan 
mengubah isi file dari /etc/bind/abimanyu/abimanyu.B04.com menjadi:
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
Lalu, di Yudhistira edit file
```
nano /etc/bind/named.conf.options
```
lalu  comment dnssec-validation auto; dan tambahkan baris berikut pada /etc/bind/named.conf.options
```
allow-query{any;};
```

<img width="441" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/ecf2e686-131c-48ec-819d-71f25fcedad0">

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

Selanjutnya, restart
```
service bind9 restart
```

Kemudian, kita masuk ke Werkudara

pertama, lakukan
```
nano /etc/bind/named.conf.options
```
Kemudian comment dnssec-validation auto; dan tambahkan baris berikut pada /etc/bind/named.conf.options
```
allow-query{any;};
```

```
mkdir /etc/bind/baratayuda
cp /etc/bind/db.local /etc/bind/baratayuda/baratayuda.abimanyu.B04.com
```

Terus,  edit file /etc/bind/named.conf.local tambahkan di bagian bawah:
```
zone "baratayuda.abimanyu.B04.com" {
	type master;
 	file "/etc/bind/baratayuda/baratayuda.abimanyu.B04.com";
};
```
terus, edit file /etc/bind/baratayuda/baratayuda.abimanyu.B04.com
jadi begini

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
@       	IN      A      	192.180.1.4	; IP Abimayu
@       	IN      AAAA    ::1
```

terus lakukan
```
service bind9 restart
```

untuk melakukan contoh tes, kami melakukan pada NakulaClient. Pastikan bahwa pada /etc/resolv.conf mengarah kepada IP Yudhistira dan Werkudara
kemudian lakukan ping 
```
ping baratayuda.abimanyuB04.com -c 5
```
diperoleh sebagai berikut:

<img width="359" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/c96d8f76-b04d-402b-b021-0e41c01fd32a">

Berikut ini adalah file bash untuk nomor 7
Yudhistira
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
baratayuda      IN      NS      ns1
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
Werkudara

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

### ⭐ Nomor 8 (Werkudara)
### Soal
Untuk informasi yang lebih spesifik mengenai Ranjapan Baratayuda, buatlah subdomain melalui Werkudara dengan akses rjp.baratayuda.abimanyu.yyy.com dengan alias www.rjp.baratayuda.abimanyu.yyy.com yang mengarah ke Abimanyu.
### Jawaban

Untuk membuat subdomain melalui werkudara yang mengarah ke abimanyu, pertama tama kita ubah di node Werkudara

ubah /etc/bind/baratayuda/baratayuda.abimanyu.B04.com menjadi:

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

Selanjutnya lakukan 

```
service bind9 restart
```

diperoleh hasil sebagai berikut:

<img width="358" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/142a42fa-41fb-4745-992c-00b9b16f4be4">

script bash untuk nomor 8:

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
echo 'Halo, Kamu berada di PrabukusumaWebServer';
?>" > /var/www/arjuna/index.php

# Membuat file konfigurasi Nginx di /etc/nginx/sites-available/arjuna
echo "server {
    listen 80;
    root /var/www/arjuna;
    index index.php index.html index.htm;
    server_name _;
    location / {
        try_files $uri $uri/ /index.php?\$query_string;
    }
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
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

echo "Konfigurasi Arjuna selesai."

```

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
        try_files $uri $uri/ /index.php?\$query_string;
    }
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
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
echo 'Halo, Kamu berada di WisanggeniWebServer';
?>" > /var/www/arjuna/index.php

# Membuat file konfigurasi Nginx di /etc/nginx/sites-available/arjuna
echo "server {
    listen 80;
    root /var/www/arjuna;
    index index.php index.html index.htm;
    server_name _;
    location / {
        try_files $uri $uri/ /index.php?\$query_string;
    }
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
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

### ⭐ Nomor 10
### Soal
Kemudian gunakan algoritma Round Robin untuk Load Balancer pada Arjuna. Gunakan server_name pada soal nomor 1. Untuk melakukan pengecekan akses alamat web tersebut kemudian pastikan worker yang digunakan untuk menangani permintaan akan berganti ganti secara acak. Untuk webserver di masing-masing worker wajib berjalan di port 8001-8003. Contoh
    - Prabakusuma:8001
    - Abimanyu:8002
    - Wisanggeni:8003
### Jawaban

### ⭐ Nomor 11
### Soal
Selain menggunakan Nginx, lakukan konfigurasi Apache Web Server pada worker Abimanyu dengan web server www.abimanyu.yyy.com. Pertama dibutuhkan web server dengan DocumentRoot pada /var/www/abimanyu.yyy
### Jawaban

### ⭐ Nomor 12
### Soal
Setelah itu ubahlah agar url www.abimanyu.yyy.com/index.php/home menjadi www.abimanyu.yyy.com/home.
### Jawaban

### ⭐ Nomor 13
### Soal
Selain itu, pada subdomain www.parikesit.abimanyu.yyy.com, DocumentRoot disimpan pada /var/www/parikesit.abimanyu.yyy
### Jawaban

### ⭐ Nomor 14
### Soal
Pada subdomain tersebut folder /public hanya dapat melakukan directory listing sedangkan pada folder /secret tidak dapat diakses (403 Forbidden).
### Jawaban

### ⭐ Nomor 15
### Soal
Buatlah kustomisasi halaman error pada folder /error untuk mengganti error kode pada Apache. Error kode yang perlu diganti adalah 404 Not Found dan 403 Forbidden.
### Jawaban

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

### ⭐ Nomor 19
### Soal
Buatlah agar setiap kali mengakses IP dari Abimanyu akan secara otomatis dialihkan ke www.abimanyu.yyy.com (alias)
### Jawaban

### ⭐ Nomor 20
### Soal
Karena website www.parikesit.abimanyu.yyy.com semakin banyak pengunjung dan banyak gambar gambar random, maka ubahlah request gambar yang memiliki substring “abimanyu” akan diarahkan menuju abimanyu.png.
### Jawaban
