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
dig -x 192.244.3.6
```
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

## SOAL 8
> Kamu juga diperintahkan untuk membuat subdomain khusus melacak kekuatan tersembunyi di Ohio dengan subdomain cakra.sudarsana.xxxx.com yang mengarah ke Bedahulu.

## SOAL 9
> Karena terjadi serangan DDOS oleh shikanoko nokonoko koshitantan (NUN), sehingga sistem komunikasinya terhalang. Untuk melindungi warga, kita diperlukan untuk membuat sistem peringatan dari siren man oleh Frekuensi Freak dan memasukkannya ke subdomain panah.pasopati.xxxx.com dalam folder panah dan pastikan dapat diakses secara mudah dengan menambahkan alias www.panah.pasopati.xxxx.com dan mendelegasikan subdomain tersebut ke Majapahit dengan alamat IP menuju radar di Kotalingga.

## SOAL 10
> Markas juga meminta catatan kapan saja meme brain rot akan dijatuhkan, maka buatlah subdomain baru di subdomain panah yaitu log.panah.pasopati.xxxx.com serta aliasnya www.log.panah.pasopati.xxxx.com yang juga mengarah ke Kotalingga.
