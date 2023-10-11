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

<img width="410" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/6b6b765c-1350-41bb-ad52-496ea64a8d25">

Yang dimana topologi-8 sebagai berikut:

![08](https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/81dd9da2-d7c1-43c2-94a1-0781204158b9)

Berikut ini adalah topologi yang telah dibuat sesuai dengan ketentuan:

<img width="697" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/297661ff-7c78-4002-b421-0b052e9db1b4">

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
echo nameserver 192.180.1.1 > /etc/resolv.conf.
```

SadewaClient
```
auto eth0
iface eth0 inet static
	address 192.180.1.3
	netmask 255.255.255.0
	gateway 192.180.1.1
echo nameserver 192.180.1.1 > /etc/resolv.conf.
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
Buat direktori /etc/bind/arjuna/arjuna.B04.com dan copy file db.local ke dalam forlder arjuna yang baru dibuat sebagai berikut:

<img width="360" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/57372a8c-23ce-45d7-8d95-37585537d9a5">

Kemudian arahkan ke /etc/bind/named.conf.local dan ubah menggunakan nano berikut

<img width="361" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/dc2b30cb-cd59-45d5-a86e-34c3995b5262">

Selanjutnya, ubah isi arjuna.B04.com

<img width="362" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/899219e1-4d30-45f6-8b1e-84991fa84280">

Kemudian restart service dengan
```
service bind9 restart
```

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

Untuk mengecek keadaan status arjuna.B04.com, kita dapat melakukan ping dari node lain. Sebagai contoh saya melakukan ping dari NakulaClient:

<img width="360" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/edff5cef-12e3-4a6d-8ee3-de9cb132b590">


### ⭐ Nomor 3
### Soal
Dengan cara yang sama seperti soal nomor 2, buatlah website utama dengan akses ke abimanyu.yyy.com dan alias www.abimanyu.yyy.com.
### Jawaban

file bash nomor 3
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

Untuk mengecek koneksi abimanyu.B04.com saya melakukan ping dari client Sadewa

<img width="359" alt="image" src="https://github.com/rayrednet/Jarkom-Modul-2-B04-2023/assets/89933907/0c11aef5-07a5-47ac-b970-587cddc3d70a">


### ⭐ Nomor 4
### Soal
Kemudian, karena terdapat beberapa web yang harus di-deploy, buatlah subdomain parikesit.abimanyu.yyy.com yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu.
### Jawaban

### ⭐ Nomor 5
### Soal
Buat juga reverse domain untuk domain utama. (Abimanyu saja yang direverse)
### Jawaban

### ⭐ Nomor 6
### Soal
Agar dapat tetap dihubungi ketika DNS Server Yudhistira bermasalah, buat juga Werkudara sebagai DNS Slave untuk domain utama.
### Jawaban

### ⭐ Nomor 7
### Soal
Seperti yang kita tahu karena banyak sekali informasi yang harus diterima, buatlah subdomain khusus untuk perang yaitu baratayuda.abimanyu.yyy.com dengan alias www.baratayuda.abimanyu.yyy.com yang didelegasikan dari Yudhistira ke Werkudara dengan IP menuju ke Abimanyu dalam folder Baratayuda.
### Jawaban

### ⭐ Nomor 8
### Soal
Untuk informasi yang lebih spesifik mengenai Ranjapan Baratayuda, buatlah subdomain melalui Werkudara dengan akses rjp.baratayuda.abimanyu.yyy.com dengan alias www.rjp.baratayuda.abimanyu.yyy.com yang mengarah ke Abimanyu.
### Jawaban

### ⭐ Nomor 9
### Soal
Arjuna merupakan suatu Load Balancer Nginx dengan tiga worker (yang juga menggunakan nginx sebagai webserver) yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Lakukan deployment pada masing-masing worker.
### Jawaban

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
