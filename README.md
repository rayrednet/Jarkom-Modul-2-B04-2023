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
