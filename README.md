# Lapres Pratikum Jarkom-Modul-2-IT22-2024

**KELOMPOK IT22**
| Nama | NRP |
|---------------------------|------------|
|Muhamad Arrayyan | 5027231014 |
|Fadlillah Cantika Sari Hermawan | 5027231042 |

## Topologi 
<img width="1500" alt="image" src="https://github.com/user-attachments/assets/4da21f44-b5a4-4af5-ab88-b38abc6b979a">

<details>

<summary>Detail Gambar</summary>

GNS
<img width="1710" alt="image" src="https://github.com/user-attachments/assets/fa16d0ee-ea05-4df0-b6fb-7370ede1aef7">

</details>

## IP addresses
| Device              | Interface   | IP Address | Netmask       | Gateway     |
|---------------------|-------------|------------|---------------|-------------|
| **Nusantara**       | eth0        | DHCP (192.168.122.1)       |             |  
|                     | eth1        | 192.244.1.1| 255.255.255.0 |             |
|                     | eth2        | 192.244.2.1| 255.255.255.0 |             |
|                     | eth3        | 192.244.3.1| 255.255.255.0 |             |
| **Sriwijaya**       | eth0        | 192.244.3.5| 255.255.255.0 | 192.244.3.1 |
| **Majapahit**       | eth0        | 192.244.2.2| 255.255.255.0 | 192.244.2.1 |
| **Tanjungkulai**    | eth0        | 192.244.2.3| 255.255.255.0 | 192.244.2.1 |
| **Bedahulu**        | eth0        | 192.244.2.4| 255.255.255.0 | 192.244.2.1 |
| **Kotalingga**      | eth0        | 192.244.3.6| 255.255.255.0 | 192.244.3.1 |
| **Solok**           | eth0        | 192.244.1.3| 255.255.255.0 | 192.244.1.1 |
| **Samaratungga**    | eth0        | 192.244.1.2| 255.255.255.0 | 192.244.1.1 |
| **Mulawarman**      | eth0        | 192.244.3.2| 255.255.255.0 | 192.244.3.1 |
| **AlexanderVolta**  | eth0        | 192.244.3.3| 255.255.255.0 | 192.244.3.1 |
| **Balaraja**        | eth0        | 192.244.3.4| 255.255.255.0 | 192.244.3.1 |
 
## SOAL 1
> Untuk mempersiapkan peperangan World War MMXXIV (Iya sebanyak itu), Sriwijaya membuat dua kotanya menjadi web server yaitu Tanjungkulai, dan Bedahulu, serta Sriwijaya sendiri akan menjadi DNS Master. Kemudian karena merasa terdesak, Majapahit memberikan bantuan dan menjadikan kerajaannya (Majapahit) menjadi DNS Slave. 

<details>

<summary>Detail Configure</summary>

#### Nusantara (Router)
```jsx
auto eth0
iface eth0 inet dhcp
        up iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

auto eth1
iface eth1 inet static
	address 192.244.1.1
	netmask 255.255.255.0

auto eth2
iface eth2 inet static
	address 192.244.2.1
	netmask 255.255.255.0

auto eth3
iface eth3 inet static
	address 192.244.3.1
	netmask 255.255.255.0
```

### Sriwijaya (DNS Master)
```jsx
auto eth0
iface eth0 inet static
	address 192.244.3.5
	netmask 255.255.255.0
	gateway 192.244.3.1
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Majapahit (DNS Slave)
```jsx
auto eth0
iface eth0 inet static
	address 192.244.2.2
	netmask 255.255.255.0
	gateway 192.244.2.1
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Tanjungkulai (Web Server)
```jsx
auto eth0
iface eth0 inet static
	address 192.244.2.3
	netmask 255.255.255.0
	gateway 192.244.2.1
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Bedahulu (Web Server)
```jsx
auto eth0
iface eth0 inet static
	address 192.244.2.4
	netmask 255.255.255.0
	gateway 192.244.2.1
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Kotalingga (Web Server)
```jsx
auto eth0
iface eth0 inet static
	address 192.244.3.6
	netmask 255.255.255.0
	gateway 192.244.3.1
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Solok (Load Balancer)
```jsx
auto eth0
iface eth0 inet static
	address 192.244.1.3
	netmask 255.255.255.0
	gateway 192.244.1.1
#	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Samaratungga (Client)
```jsx
auto eth0
iface eth0 inet static
	address 192.244.1.2
	netmask 255.255.255.0
	gateway 192.244.1.1
#	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Mulawarman (Client)
```jsx
auto eth0
iface eth0 inet static
	address 192.244.3.2
	netmask 255.255.255.0
	gateway 192.244.3.1
#	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### AlexanderVolta (Client)
```jsx
auto eth0
iface eth0 inet static
	address 192.244.3.3
	netmask 255.255.255.0
	gateway 192.244.3.1
#	up echo nameserver 192.168.0.1 > /etc/resolv.conf
```

### Balaraja (Client)
```jsx
auto eth0
iface eth0 inet static
	address 192.244.3.4
	netmask 255.255.255.0
	gateway 192.244.3.1
#	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

</details>

## SOAL 2
> Karena para pasukan membutuhkan koordinasi untuk melancarkan serangannya, maka buatlah sebuah domain yang mengarah ke Solok dengan alamat sudarsana.xxxx.com dengan alias www.sudarsana.xxxx.com, dimana xxxx merupakan kode kelompok. Contoh: sudarsana.it01.com.

<details>

<summary>Detail Configure</summary>

## Setup DNS @ Sriwijaya

Update package lists
```
apt-get update -y
```
Install bind9
```
 apt-get install bind9 -y
```
Edit the DNS record
```
nano sriwijaya.sh
```
Edit config file:
```bash
#!/bin/bash

# Buat domain sudarsana.it22.com
echo 'zone "sudarsana.it22.com" {
	type master;
	file "/etc/bind/jarkom/sudarsana.it22.com";
};' > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

cp /etc/bind/db.local /etc/bind/jarkom/sudarsana.it22.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     sudarsana.it22.com. root.sudarsana.it22.com. (
                        2024050301      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      sudarsana.it22.com.
@       IN      A       192.244.1.3     ; IP Solok
www     IN      CNAME   sudarsana.it22.com.' > /etc/bind/jarkom/sudarsana.it22.com

service bind9 restart
```
- Specify hostname in NS records: sudarsana.it22.com.
- Specify address in A records: 192.244.1.3
- Specify canonical name (alias) in CNAME records: sudarsana.it22.com.
<img height="150" width="300" alt="image" src="https://github.com/user-attachments/assets/24b79f63-1e3d-46f3-882f-2f5f1ba6dc84">

</details>

## SOAL 3
> Para pasukan juga perlu mengetahui mana titik yang akan diserang, sehingga dibutuhkan domain lain yaitu pasopati.xxxx.com dengan alias www.pasopati.xxxx.com yang mengarah ke Kotalingga.

<details>

<summary>Detail Configure</summary>

## Setup DNS @ Sriwijaya

Update package lists
```
apt-get update -y
```
Install bind9
```
 apt-get install bind9 -y
```
Edit the DNS record
```
nano pasopati.sh
```
Edit config file:
```bash
#!/bin/bash

# Buat domain pasopati.it22.com
echo 'zone "pasopati.it22.com" {
	type master;
	file "/etc/bind/jarkom/pasopati.it22.com";
};' > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

cp /etc/bind/db.local /etc/bind/jarkom/pasopati.it22.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     pasopati.it22.com. root.pasopati.it22.com. (
                        2024050301      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      pasopati.it40.com.
@       IN      A       192.244.3.6     ; IP Kotalingga
www     IN      CNAME   pasopati.it22.com.' > /etc/bind/jarkom/pasopati.it22.com

service bind9 restart
```
- Specify hostname in NS records: pasopati.it22.com.
- Specify address in A records: 192.244.3.6
- Specify canonical name (alias) in CNAME records: pasopati.it22.com.
<img height="150" width="300" alt="image" src="https://github.com/user-attachments/assets/24b79f63-1e3d-46f3-882f-2f5f1ba6dc84">

</details>

## SOAL 4
> Markas pusat meminta dibuatnya domain khusus untuk menaruh informasi persenjataan dan suplai yang tersebar. Informasi dan suplai meme terbaru tersebut mengarah ke Tanjungkulai dan domain yang ingin digunakan adalah rujapala.xxxx.com dengan alias www.rujapala.xxxx.com.
3
<details>

<summary>Detail Configure</summary>

## Setup DNS @ Sriwijaya

Update package lists
```
apt-get update -y
```
Install bind9
```
 apt-get install bind9 -y
```
Edit the DNS record
```
nano rujapala.sh
```
Edit config file:
```bash
#!/bin/bash

# Buat domain rujapala.it22.com
echo 'zone "rujapala.it22.com" {
	type master;
	file "/etc/bind/jarkom/rujapala.it22.com";
};' > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

cp /etc/bind/db.local /etc/bind/jarkom/rujapala.it22.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     rujapala.it22.com. root.rujapala.it22.com. (
                        2024050301      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      pasopati.it40.com.
@       IN      A       192.244.2.3     ; IP Tanjungkulai
www     IN      CNAME   rujapala.it22.com.' > /etc/bind/jarkom/rujapala.it22.com

service bind9 restart
```
- Specify hostname in NS records: rujapala.it22.com.
- Specify address in A records: 192.244.2.3
- Specify canonical name (alias) in CNAME records: rujapala.it22.com.
<img height="150" width="300" alt="image" src="https://github.com/user-attachments/assets/24b79f63-1e3d-46f3-882f-2f5f1ba6dc84">

</details>

## SOAL 5
> Pastikan domain-domain tersebut dapat diakses oleh seluruh komputer (client) yang berada di Nusantara.

<details>

<summary>Detail Configure</summary> 

Setting IP Client
```
nano /etc/resolv.conf
```
Edit config file:
```jsx
nameserver 192.244.3.5   # IP Sriwijaya
nameserver 192.244.2.2   # IP Majapahit
nameserver 192.168.122.1 # IP Router 
```
Izinkan File:
```jsx
chmod +x sriwijaya.sh
chmod +x pasopati.sh
chmod +x rujapala.sh
```
Start program:
```bash
./sriwijaya.sh
./pasopati.sh
./rujapala.sh
```
Note: Restore bind
```jsx
apt-get -o DPkg::Options::="--force-confmiss" --reinstall install bind9
```

</details>

<details>

<summary>Detail Dokumentasi</summary>


## Samaratungga (Client)

```jsx
ping sudarsana.it22.com
```
<img height="400" width="1500" alt="image" src="https://github.com/user-attachments/assets/7dce1827-e738-40d9-82bd-32da510b1c3e">

```jsx
ping pasopati.it22.com
```
<img height="400" width="1500" alt="image" src="https://github.com/user-attachments/assets/74860f32-377d-4d37-829e-300479b92237">

```jsx
ping rujapala.it22.com
```
<img height="400" width="1500" alt="image" src="https://github.com/user-attachments/assets/649babd0-fb84-423f-8e38-994357195f5a">


## Mulawarman (Client)

```jsx
ping sudarsana.it22.com
```
<img height="400" width="1500" alt="image" src="https://github.com/user-attachments/assets/f14a6a58-8186-4171-a617-91906e3a4caf">

```jsx
ping pasopati.it22.com
```
<img height="400" width="1500" alt="image" src="https://github.com/user-attachments/assets/3f7863f1-37ed-467a-b567-d1a3bfa114cb">

```jsx
ping rujapala.it22.com
```
<img height="400" width="1500" alt="image" src="https://github.com/user-attachments/assets/ff020a1d-8f77-49d0-abc4-f8d067859bc6">


## AlexanderVolta (Client)

```jsx
ping sudarsana.it22.com
```
<img height="400" width="1500" alt="image" src="https://github.com/user-attachments/assets/7dfe93c0-d13d-4127-8d4d-19e6ec6eee82">

```jsx
ping pasopati.it22.com
```
<img height="400" width="1500" alt="image" src="https://github.com/user-attachments/assets/a0f074c0-90b6-40d7-9ae4-edda9fa2835f">

```jsx
ping rujapala.it22.com
```
<img height="400" width="1500" alt="image" src="https://github.com/user-attachments/assets/2cfb2674-9e2c-44f8-86e0-93f3eb47006a">


### Balaraja (Client)

```jsx
ping sudarsana.it22.com
```
<img height="400" width="1500" alt="image" src="https://github.com/user-attachments/assets/a76d8252-730e-4304-9746-ec15e55c484f">

```jsx
ping pasopati.it22.com
```
<img height="400" width="1500" alt="image" src="https://github.com/user-attachments/assets/bb403a3e-d8ed-4185-9514-9af662556da1">

```jsx
ping rujapala.it22.com
```
<img height="400" width="1500" alt="image" src="https://github.com/user-attachments/assets/59f1b8d7-fbd6-47fa-a33a-44176379a30c">

</details>

## SOAL 6
> Beberapa daerah memiliki keterbatasan yang menyebabkan hanya dapat mengakses domain secara langsung melalui alamat IP domain tersebut. Karena daerah tersebut tidak diketahui secara spesifik, pastikan semua komputer (client) dapat mengakses domain pasopati.xxxx.com melalui alamat IP Kotalingga (Notes: menggunakan pointer record).

<details>

<summary>Detail Configure</summary> 

## Setup DNS @ Sriwijaya
Pada DNS Master lakukan konfigurasi dengan melakukan pengubahan pada named.conf.local dan in-addr.arpa seperti pada konfigurasi berikut (membalik IP server Sriwijaya, yang awalnya `10.83.3' menjadi '3.83.10') :
```bash
#!/bin/bash

# Buat reverse DNS (Record PTR)
echo 'zone "3.244.192.in-addr.arpa" {
    type master;
    file "/etc/bind/jarkom/3.244.192.in-addr.arpa";
};' >> /etc/bind/named.conf.local

cp /etc/bind/db.local /etc/bind/jarkom/3.244.192.in-addr.arpa

echo ';
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     pasopati.it22.com. root.pasopati.it22.com. (
                        2024050301      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
3.244.192.in-addr.arpa.    IN      NS      pasopati.it22.com.
3                          IN      PTR     pasopati.it22.com.' > /etc/bind/jarkom/3.244.192.in-addr.arpa

service bind9 restart
```
Setelah itu pada masing-masing client (Samaratungga, Mulawarman, AlexanderVolta, Balaraja) lakukan setup konfigurasi
```bash
# Set nameserver ke IP Nusantara
echo 'nameserver 192.168.122.1' > /etc/resolv.conf

# Install utils
apt-get update
apt-get install dnsutils -y

# Kembalikan nameserver ke Sriwijaya and Majapahit
echo '
nameserver 192.244.3.5
nameserver 192.244.2.2' > /etc/resolv.conf
```
```jsx
host -t PTR 192.244.3.6
```
</details> 

<details>

<summary>Detail Dokumentasi</summary>

![image](https://github.com/user-attachments/assets/d5c60a13-60c4-4610-aef1-45f04a82136a)

</details>

## SOAL 7
> Akhir-akhir ini seringkali terjadi serangan brainrot ke DNS Server Utama, sebagai tindakan antisipasi kamu diperintahkan untuk membuat DNS Slave di Majapahit untuk semua domain yang sudah dibuat sebelumnya yang mengarah ke Sriwijaya.

<details>

<summary>Detail Configure</summary> 

Buka file konfigurasi BIND di Majapahit:
```jsx
nano /etc/bind/named.conf.local
```
Tambahkan konfigurasi untuk setiap domain yang ada di DNS Master (Sriwijaya):
```bash
#!/bin/bash

# Tambahkan kebutuhan untuk menjadi master Sriwijaya
echo '
zone "sudarsana.it22.com" {
        type master;
        notify yes;
        also-notify { 192.244.2.2; }; //IP Majapahit
        allow-transfer { 192.244.2.2; }; //IP Majapahit
        file "/etc/bind/jarkom/sudarsana.it22.com";
};

zone "pasopati.it22.com" {
        type master;
        notify yes;
        also-notify { 192.244.2.2; }; //IP Majapahit
        allow-transfer { 192.244.2.2; }; //IP Majapahit
        file "/etc/bind/jarkom/pasopati.it22.com";
};

zone "rujapala.it22.com" {
        type master;
        notify yes;
        also-notify { 192.244.2.2; }; //IP Majapahit
        allow-transfer { 192.244.2.2; }; //IP Majapahit
        file "/etc/bind/jarkom/rujapala.it22.com";
};' > /etc/bind/named.conf.local

service bind9 restart
```
Lalu lakukan setup konfigurasi juga pada DNS Slave (Majapahit)
```bash
#!/bin/bash
# Cek apakah bind9 sudah terinstal
if ! command -v named &> /dev/null
then
    echo "Bind9 belum terinstal, melakukan instalasi..."
    # Melakukan instalasi bind9
    apt-get update
    apt-get install bind9 -y
else
    echo "Bind9 sudah terinstal."
fi

echo '
zone "sudarsana.it22.com" {
    type slave;
    masters {  192.244.3.5; }; // IP Sriwijaya
    file "/var/lib/bind/sudarsana.it22.com";
};

zone "pasopati.it22.com" {
    type slave;
    masters {  192.244.3.5; }; // IP Sriwijaya
    file "/var/lib/bind/pasopati.it22.com";
};

zone "rujapala.it22.com" {
    type slave;
    masters {  192.244.3.5; }; // IP Sriwijaya
    file "/var/lib/bind/rujapala.it22.com";
};' > /etc/bind/named.conf.local

service bind9 restart
```
</details>

<details>

<summary>Detail Dokumentasi</summary>

![image](https://github.com/user-attachments/assets/3104d08e-1cc6-4392-9b72-4996467f5ccd)

![image](https://github.com/user-attachments/assets/346403b3-fd95-495f-8b67-845767d4dbbe)

![image](https://github.com/user-attachments/assets/5adfcc3c-21c1-4815-a904-3ae866765eb6)

![image](https://github.com/user-attachments/assets/26196f38-1cb3-4923-a840-56e4b1ed8b58)

</details> 

## SOAL 8
> Kamu juga diperintahkan untuk membuat subdomain khusus melacak kekuatan tersembunyi di Ohio dengan subdomain cakra.sudarsana.xxxx.com yang mengarah ke Bedahulu.
<details>

<summary>Detail Configure</summary> 

Lakukan setup konfigurasi pada Sriwijaya (DNS Master)
```bash
#!/bin/bash

# Tambahkan konfigurasi untuk membuat subdomain cakra.sudarsana.it22.com
echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     sudarsana.it22.com. sudarsana.it22.com. (
                        2024050301      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      sudarsana.it22.com.
@       IN      A       192.244.1.3     ; IP Solok
www     IN      CNAME   sudarsana.it22.com.
cakra  IN      A        192.244.2.4     ; IP Bedahulu' > /etc/bind/jarkom/sudarsana.it22.com

service bind9 restart
```
</details> 

<details>

<summary>Detail Dokumentasi</summary>



</details>

</details>

## SOAL 9
> Karena terjadi serangan DDOS oleh shikanoko nokonoko koshitantan (NUN), sehingga sistem komunikasinya terhalang. Untuk melindungi warga, kita diperlukan untuk membuat sistem peringatan dari siren man oleh Frekuensi Freak dan memasukkannya ke subdomain panah.pasopati.xxxx.com dalam folder panah dan pastikan dapat diakses secara mudah dengan menambahkan alias www.panah.pasopati.xxxx.com dan mendelegasikan subdomain tersebut ke Majapahit dengan alamat IP menuju radar di Kotalingga.

<details>

<summary>Detail Configure</summary> 

Lakukan set up konfigurasi di Sriwijaya (DNS Master)
```bash
#!/bin/bash

# Tambahkan konfigurasi untuk delegasi panah.pasopati.it22.com ke Majapahit
echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     pasopati.it22.com. pasopati.it22.com. (
                        2024050301      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      pasopati.it40.com.
@       IN      A       192.244.3.6     ; IP Kotalingga
www     IN      CNAME   pasopati.it40.com.
ns1     IN      A       192.244.2.2     ; Terusin ke Majapahit
panah   IN      NS      ns1' > /etc/bind/jarkom/pasopati.it22.com

echo '
options {
        directory "/var/cache/bind";

        //dnssec-validation auto;
        allow-query{any;};

        auth-nxdomain no;    # confirm to RFC1035
        listen-on-v6 { any; };
};' > /etc/bind/named.conf.options

service bind9 restart
```
Lakukan setup konfigurasi juga di Majapahit (DNS Slave)
```bash
#!/bin/bash

# Setup
echo '
options {
        directory "/var/cache/bind";

        //dnssec-validation auto;
        allow-query{any;};

        auth-nxdomain no;
        listen-on-v6 { any; };
};' > /etc/bind/named.conf.options

echo 'zone "panah.pasopati.it22.com" {
	type master;
	file "/etc/bind/panah/panah.pasopati.it22.com";
};' >> /etc/bind/named.conf.local

mkdir /etc/bind/panah

cp /etc/bind/db.local /etc/bind/panah/panah.pasopati.it22.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     panah.pasopati.it22.com. root.panah.pasopati.it22.com. (
                        2024050301      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      panah.pasopati.it22.com.
@       IN      A       192.244.3.6     ; IP Kotalingga
www     IN      CNAME   panah.pasopati.it22.com.' > /etc/bind/panah/panah.pasopati.it22.com

service bind9 restart
```
![image](https://github.com/user-attachments/assets/d8adb605-f7ec-4ece-a427-c4fc103add26)

![image](https://github.com/user-attachments/assets/06a1fc76-0e15-4de5-94b4-a96a538a0586)

![image](https://github.com/user-attachments/assets/a0d60df4-c165-4395-a3a9-5502efca6982)

</details>

## SOAL 10
> Markas juga meminta catatan kapan saja meme brain rot akan dijatuhkan, maka buatlah subdomain baru di subdomain panah yaitu log.panah.pasopati.xxxx.com serta aliasnya www.log.panah.pasopati.xxxx.com yang juga mengarah ke Kotalingga.

<details>

<summary>Detail Configure</summary> 

Buat konfigurasi script pada Majapahit (DNS Slave)
```bash
#!/bin/bash

# Tambahkan konfigurasi untuk membuat subdomain log.panah.pasopati.it22.com
echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     panah.pasopati.it22.com. panah.pasopati.it22.com. (
                        2024050301      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      panah.pasopati.it22.com.
@       IN      A       192.244.3.6     ; IP Kotalingga
www     IN      CNAME   panah.pasopati.it40.com.
log     IN      A       192.244.3.6     ; IP Kotalingga
www.log IN      CNAME   panah.pasopati.it22.com.' > /etc/bind/panah/panah.pasopati.it22.com

service bind9 restart
```
![image](https://github.com/user-attachments/assets/ee464037-7951-47c6-94b8-82852bdac6a5)

</details>

## SOAL 11
> Setelah pertempuran mereda, warga IT dapat kembali mengakses jaringan luar dan menikmati meme brainrot terbaru, tetapi hanya warga Majapahit saja yang dapat mengakses jaringan luar secara langsung. Buatlah konfigurasi agar warga IT yang berada diluar Majapahit dapat mengakses jaringan luar melalui DNS Server Majapahit.

<details>

<summary>Detail Configure</summary> 

Lakukan setup konfigurasi pada Sriwijaya (DNS Master)
```bash
#!/bin/bash

# Tambahkan konfigurasi untuk DNS forwarder
echo '
options {
        directory "/var/cache/bind";

        forwarders {
                192.168.122.1; //IP Nusantara
        };
        //dnssec-validation auto;
        allow-query{any;};

        auth-nxdomain no;
        listen-on-v6 { any; };
};' > /etc/bind/named.conf.options

service bind9 restart
```
Lakukan setup konfigurasi Majapahit (DNS Slave)
```bash
#!/bin/bash

# Tambahkan konfigurasi untuk DNS forwarder
echo '
options {
        directory "/var/cache/bind";

        forwarders {
                192.168.122.1; //IP Nusantara
        };
        //dnssec-validation auto;
        allow-query{any;};

        auth-nxdomain no;
        listen-on-v6 { any; };
};' > /etc/bind/named.conf.options

service bind9 restart
```
![image](https://github.com/user-attachments/assets/adc5125f-6c55-47a3-90e5-c085b80c873c)

</details>

## SOAL 12
> Karena pusat ingin sebuah laman web yang ingin digunakan untuk memantau kondisi kota lainnya maka deploy laman web ini (cek resource yg lb) pada Kotalingga menggunakan apache.

<details>

<summary>Detail Configure</summary> 

Lakukan config network dengan menambahkan ip Kotalingga pada Sriwijaya (DNS Master)
```bash
#!/bin/bash

# Tambahkan nameserver Ip Kotalingga
echo '
nameserver 192.244.3.6' > /etc/resolv.conf
```
Setelah itu lakukan instalasi browser lynx pada setiap client
```bash
#!/bin/bash

# Lakukan instalasi browser Lynx
if ! command -v named &> /dev/null
then
    echo "Lynx belum ada, melakukan penginstalan..."

    # Melakukan instalasi lynx
    apt-get update
    apt-get install lynx -y
else
    echo "lynx sudah ada dan siap digunakan."
fi
```
Lakukan setup konfigurasi pada Kotalingga (Web Server)
```bash
#!/bin/bash

# Tambahkan konfigurasi agar bisa deploy

# Cek apakah apache2 sudah terinstal
if ! command -v named &> /dev/null
then
    echo "Apache2 belum ada, melakukan penginstalan..."
    # Melakukan instalasi apache2
    apt-get update
    apt-get install apache2 -y
    apt-get install libapache2-mod-php7.0 -y
else
    echo "apache2 sudah terinstal."
fi

# Cek apakah unzip sudah terinstal
if ! command -v named &> /dev/null
then
    echo "Unzip belum ada, melakukan penginstalan..."
    # Melakukan instalasi unzip
    apt-get update
    apt-get install unzip -y
else
    echo "unzip sudah terinstal."
fi

# Cek apakah php sudah terinstal
if ! command -v named &> /dev/null
then
    echo "PHP belum ada, melakukan penginstalan..."
    # Melakukan instalasi php
    apt-get update
    apt-get install php -y
else
    echo "php sudah terinstal."
fi

# Download file lb.zip
curl -k "https://drive.usercontent.google.com/download?id={1Sqf0TIiybYyUp5nyab4twy9svkgq8bi7}&confirm=xxx" -o lb.zip

# Unzip file lb.zip
unzip lb.zip

# Hapus file template
rm -rf /var/www/html/index.php

# Copy file index.php
cp worker/index.php /var/www/html/index.php

service apache2 restart
```

![image](https://github.com/user-attachments/assets/6f0acaa3-f01f-4d52-899d-fb0b449bc33c)

</details>

## SOAL 13
> Karena Sriwijaya dan Majapahit memenangkan pertempuran ini dan memiliki banyak uang dari hasil penjarahan (sebanyak 35 juta, belum dipotong pajak) maka pusat meminta kita memasang load balancer untuk membagikan uangnya pada web nya, dengan Kotalingga, Bedahulu, Tanjungkulai sebagai worker dan Solok sebagai Load Balancer menggunakan apache sebagai web server nya dan load balancer nya.

<details>

<summary>Detail Configure</summary> 

Lakukan setup konfigurasi pada Sriwijaya (DNS Master) dan Majapahit (DNS Slave)
```bash
#!/bin/bash

# Tambahkan nameserver Ip Solok (LoadBalancer)
echo '
nameserver 192.168.122.1
nameserver 192.244.1.3' > /etc/resolv.conf
```
Lakukan setup konfigurasi pada Load Balancer (Solok)
```bash
#!/bin/bash

# Tambahkan keperluan untuk setting load balancer pada Solok

# Cek apakah apache2 wes onok bolo.
if ! command -v named &> /dev/null
then
    echo "Apache2 durung keinstall, utiwi get..."
    # Melakukan instalasi apache2
    apt-get update
    apt-get install apache2 -y
    apt-get install libapache2-mod-php7.0 -y
else
    echo "apache2 wes onok bolo.."
fi

# Cek apakah php sudah ada.
if ! command -v named &> /dev/null
then
    echo "PHP durung keinstall, utiwi get..."
    # Melakukan instalasi php
    apt-get update
    apt-get install php -y
else
    echo "php wes onok bolo.."
fi

# Enable apache2 module
a2enmod proxy_balancer
a2enmod proxy_http
a2enmod lbmethod_byrequests
echo '
<VirtualHost *:80>
    <Proxy balancer://serverpool>
        BalancerMember http://192.244.3.6/ #Kotalingga
        BalancerMember http://192.244.2.4/ #Bedahulu
        BalancerMember http://192.244.2.3/ #Tanjungkulai
        Proxyset lbmethod=byrequests
    </Proxy>
    ProxyPass / balancer://serverpool/
    ProxyPassReverse / balancer://serverpool/
</VirtualHost>' > /etc/apache2/sites-available/000-default.conf

service apache2 restart
```
Lakukan setup konfigurasi pada masing-masing Web Server / Worker yang ada (Kotalingga, Bedahulu, Tanjungkulai)
```bash
#!/bin/bash

# Tambahkan untuk keperluan load balancer
# Cek apakah apache2 sudah terinstal
if ! command -v named &> /dev/null
then
    echo "Apache2 belum terinstal, melakukan instalasi..."
    # Melakukan instalasi apache2
    apt-get update
    apt-get install apache2 -y
    apt-get install libapache2-mod-php7.0 -y
else
    echo "apache2 sudah terinstal."
fi

# Cek apakah unzip sudah terinstal
if ! command -v named &> /dev/null
then
    echo "Unzip belum terinstal, melakukan instalasi..."
    # Melakukan instalasi unzip
    apt-get update
    apt-get install unzip -y
else
    echo "unzip sudah terinstal."
fi

# Cek apakah php sudah terinstal
if ! command -v named &> /dev/null
then
    echo "PHP belum terinstal, melakukan instalasi..."
    # Melakukan instalasi php
    apt-get update
    apt-get install php -y
else
    echo "php sudah terinstal."
fi

# Download file lb.zip
curl -k "https://drive.usercontent.google.com/download?id={1Sqf0TIiybYyUp5nyab4twy9svkgq8bi7}&confirm=xxx" -o lb.zip

# Unzip file lb.zip
unzip lb.zip

# Hapus file template
rm -rf /var/www/html/index.php

# Copy file index.php
cp worker/index.php /var/www/html/index.php

service apache2 restart
```
Testing menggunakan salah satu client dengan command lynx `http://192.244.1.3/index.php`

</details>

## SOAL 14
> Selama melakukan penjarahan mereka melihat bagaimana web server luar negeri, hal ini membuat mereka iri, dengki, sirik dan ingin flexing sehingga meminta agar web server dan load balancer nya diubah menjadi nginx.
<details>

<summary>Detail Configure</summary> 

Ubah konfigurasi pada semua web server / worker (Kotalingga, Bedahulu, Tanjungkulai)
```jsx
service apache2 stop

apt install nginx php php-fpm -y

service php7.0-fpm start

echo 'server {
listen 80;

root /var/www/html;
index index.php index.html index.htm index.nginx-debian.html;

server_name _;

location / {
try_files $uri $uri/ /index.php?$query_string;
}

location ~ \.php$ {
include snippets/fastcgi-php.conf;
fastcgi_pass unix:/run/php/php7.0-fpm.sock;
}

location ~ /\.ht {
deny all;
}
}' > /etc/nginx/sites-enabled/default

service php7.0-fpm restart

service nginx restart
```
Lakukan juga pengubahan pada konfigurasi Load Balancer (Solok)
```jsx
service apache2 stop

#Lakukan instalasi php dan nginx
apt-get update
apt install nginx php php-fpm -y
apt-get install nginx -y

echo "upstream backend {
  server 192.244.3.6; # Kotalingga
  server 192.244.2.4; # Bedahulu
  server 192.244.2.3; # Tanjungkulai
}

server {
  listen 80;

  location / {
    proxy_pass http://backend;
  }
}
" > /etc/nginx/sites-enabled/default

service nginx restart
```
![image](https://github.com/user-attachments/assets/61982af0-d9cc-494d-9b07-0cae354fb416)

![image](https://github.com/user-attachments/assets/d0ada24a-3c41-49bf-a94f-bd295f813fff)

![image](https://github.com/user-attachments/assets/130b2ed1-f421-4c74-9652-af0203e5d965)

![image](https://github.com/user-attachments/assets/3a91691c-e5fd-4906-af55-0759fc8eb88d)

</details>

## SOAL 15
> Markas pusat meminta laporan hasil benchmark dengan menggunakan apache benchmark dari load balancer dengan 2 web server yang berbeda tersebut dan meminta secara detail dengan ketentuan:
> - Nama Algoritma Load Balancer
> - Report hasil testing apache benchmark
> - Grafik request per second untuk masing masing algoritma. 
> - Analisis
> - Meme terbaik kalian (terserah ( ͡° ͜ʖ ͡°)) 🤓
<details>

<summary>Detail Configure</summary> 

Lakukan instalasi apache2-utils untuk melakukan instalasi pada tools yang diperlukan
```jsx
apt-get install apache2-utils -y
```
Jalankan command:   
```jsx
`ab -n 1000 -c 100 http://(ip load balancer)`
```
disini kami memakai
```jsx
`ab -n 1000 -c 100 http://192.244.1.3`
```
</details>

## SOAL 16
> Karena dirasa kurang aman dari brainrot karena masih memakai IP, markas ingin akses ke Solok memakai solok.xxxx.com dengan alias www.solok.xxxx.com (sesuai web server terbaik hasil analisis kalian).

<details>

<summary>Detail Configure</summary> 

Lakukan reconfig pada DNS Master (Sriwijaya)
```bash
echo 'zone "solok.it22.com" {
        type master;
        file "/etc/bind/jarkom/solok.it22.com";
};' > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

cp /etc/bind/db.local /etc/bind/jarkom/solok.it22.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     solok.it22.com. root.solok.it22.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      solok.it22.com.
@       IN      A       192.244.3.6     ; IP Kotalingga
www             IN      CNAME   solok.it22.com.
' > /etc/bind/jarkom/solok.it22.com

service bind9 restart
```
Lakukan reconfig pada Load Balancer (Solok)
```bash
service nginx stop

echo 'upstream backend {
server 192.244.3.6; # IP Kotalingga
server 192.244.2.4; # IP Bedahulu
server 192.244.2.3; # IP Lipovka
}

server {
listen 80;
server_name solok.it22.com www.solok.it22.com; 

location / {
proxy_pass http://backend;
}
}
' > /etc/nginx/sites-enabled/default

service nginx restart
```
</details>

## SOAL 17
> Agar aman, buatlah konfigurasi agar solok.xxx.com hanya dapat diakses melalui port sebesar π x 10^4 = (phi nya desimal) dan 2000 + 2000 log 10 (10) +700 - π = ?.

<details>

<summary>Detail Configure</summary> 

Lakukan reconfig pada Load Balancer (Solok)
```bash
echo 'upstream backend {
server 192.244.3.6; # IP Kotalingga
server 192.244.2.4; # IP Bedahulu
server 192.244.2.3; # IP Lipovka
}

server {
listen 31400;
listen 4696;
server_name solok.it22.com www.solok.it22.com; 

location / {
proxy_pass http://backend;
}
}
' > /etc/nginx/sites-enabled/default

service nginx restart
```
Testing melalui client lain dengan command 
```jsx
lynx http://solok.it22.com:(31400/4696)
```
</details>

## SOAL 18
> Apa bila ada yang mencoba mengakses IP solok akan secara otomatis dialihkan ke www.solok.xxxx.com.

<details>

<summary>Detail Configure</summary> 

Lakukan reconfig solok dengan script berikut
```bash
echo 'upstream backend {
server 192.244.3.6; # IP Kotalingga
server 192.244.2.4; # IP Bedahulu
server 192.244.2.3; # IP Lipovka
}

server {
listen 80;
listen 31400;
listen 4696;
server_name solok.it22.com www.solok.it22.com; 

location / {
proxy_pass http://backend;
if ($host = 192.244.1.3) {
return 301 http://www.solok.it22.com:31400$request_uri;
}
}
}
' > /etc/nginx/sites-enabled/default

service nginx restart
```
Testing di client:
```jsx
http://192.244.1.3/
```
</details>

## SOAL 19
> Karena probset sudah kehabisan ide masuk ke salah satu worker buatkan akses direktori listing yang mengarah ke resource worker2.

<details>

<summary>Detail Configure</summary> 

Konsep soalnya adalah dengan membuat domain baru dimana kami menggunakan `sekianterimakasih.it22.com` sebagai domainnya dan melakukan setting directory listing
```bash
#!/bin/bash

# Function to check if last command was successful
check_error() {
    if [ $? -ne 0 ]; then
        echo "ERROR: $1"
        exit 1
    fi
}

# Cek port 80 dipakai atau tidak
if netstat -tuln | grep -q ":80 "; then
    echo "Port 80 is already in use. Stopping potentially conflicting services..."
    service nginx stop 2>/dev/null
    service apache2 stop 2>/dev/null
    sleep 2
fi

mkdir -p /var/www/sekianterimakasih.it22.com
check_error "Failed to create directory"

cd /var/www/sekianterimakasih.it22.com
check_error "Failed to change directory"

curl -k "https://drive.usercontent.google.com/download?id={1JGk8b-tZgzAOnDqTx5B3F9qN6AyNs7Zy}&confirm=xxx" -o worker2.zip
check_error "Failed to download worker2.zip"

unzip -o worker2.zip
check_error "Failed to unzip worker2.zip"

rm -rf /var/www/sekianterimakasih.it22.com/worker2

# Pindahkan direktori worker2 
if [ -d "dir-listing/worker2" ]; then
    cp -r dir-listing/worker2 /var/www/sekianterimakasih.it22.com/
    check_error "Failed to copy worker2 directory"
    rm -rf dir-listing
else
    echo "ERROR: Could not find worker2 directory"
    exit 1
fi

chown -R www-data:www-data /var/www/sekianterimakasih.it22.com
chmod -R 755 /var/www/sekianterimakasih.it22.com

# Ubah file config Apache virtual host
cat << 'EOF' > /etc/apache2/sites-available/sekianterimakasih.it22.com.conf
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/sekianterimakasih.it22.com
    ServerName sekianterimakasih.it22.com
    ServerAlias www.sekianterimakasih.it22.com

    <Directory /var/www/sekianterimakasih.it40.com/worker2>
        Options +Indexes
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/sekianterimakasih.it22.com_error.log
    CustomLog ${APACHE_LOG_DIR}/sekianterimakasih.it22.com_access.log combined
</VirtualHost>
EOF
check_error "Failed to create Apache configuration file"

# cek log apache2 dan ubah permission
mkdir -p /var/log/apache2
chown -R www-data:www-data /var/log/apache2
chmod -R 755 /var/log/apache2

a2dissite 000-default.conf
a2ensite sekianterimakasih.it22.com.conf

# bantu redirect
a2enmod rewrite

apache2ctl configtest

# Restart Apache more forcefully
service apache2 stop
sleep 2
service apache2 start

echo "Script execution completed. Checking Apache status..."
service apache2 status
```
Dan terakhir, testing di client dengan:
```jsx
lynx 192.244.3.6/worker2
```
</details>

## SOAL 20
> Worker tersebut harus dapat di akses dengan sekiantterimakasih.xxxx.com dengan alias www.sekiantterimakasih.xxxx.com.
<details>

<summary>Detail Configure</summary> 

Buat suatu setup konfigurasi pada DNS MAster (Sriwijaya)
```bash
#!/bin/bash

# Buat domain sekianterimakasih.it22.com
echo 'zone "sekianterimakasih.it22.com" {
	type master;
	file "/etc/bind/jarkom/sekianterimakasih.it22.com";
};' > /etc/bind/named.conf.local

mkdir /etc/bind/jarkom

cp /etc/bind/db.local /etc/bind/jarkom/sekianterimakasih.it22.com

echo '
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     sekianterimakasih.it22.com. sekianterimakasih.it22.com. (
                        2024050301      ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      sekianterimakasih.it22.com.
@       IN      A       192.244.3.6     ; IP Kotalingga
www     IN      CNAME   sekianterimakasih.it22.com.' > /etc/bind/jarkom/sekianterimakasih.it22.com

service bind9 restart
```
Setelah itu testing di client dengan command:
```jsx
lynx sekianterimakasih.it22.com
```
```jsx
www.sekianterimakasih.it22.com
```
</details>
