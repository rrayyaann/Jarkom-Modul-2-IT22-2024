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

Sett IP 
```
nano /etc/resolv.conf
```
```jsx
nameserver 192.244.3.5  # IP Sriwijaya
nameserver 192.244.2.2  # IP Majapahit
nameserver 192.168.122.1 # IP Router 
```

</details>

## SOAL 3
> Para pasukan juga perlu mengetahui mana titik yang akan diserang, sehingga dibutuhkan domain lain yaitu pasopati.xxxx.com dengan alias www.pasopati.xxxx.com yang mengarah ke Kotalingga.

<details>

<summary>Detail Configure</summary>

## Setup DNS @ Pochinki

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
nano /etc/bind/it22/airdrop.it22.com
```
Edit file /etc/bind/it22/airdrop.it22.com as follows:
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
@       IN      A       10.83.3.6     ; IP Kotalingga
www     IN      CNAME   pasopati.it22.com.' > /etc/bind/jarkom/pasopati.it22.com

service bind9 restart
```
- Specify hostname in NS records: airdrop.it22.com.
- Specify address in A records: 192.244.1.4
- Specify canonical name (alias) in CNAME records: airdrop.it22.com.

</details>

## SOAL 4
> Markas pusat meminta dibuatnya domain khusus untuk menaruh informasi persenjataan dan suplai yang tersebar. Informasi dan suplai meme terbaru tersebut mengarah ke Tanjungkulai dan domain yang ingin digunakan adalah rujapala.xxxx.com dengan alias www.rujapala.xxxx.com.
3
<details>

<summary>Detail Configure</summary>

## Setup DNS @ Pochinki

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
nano /etc/bind/it22/airdrop.it22.com
```
Edit file /etc/bind/it22/airdrop.it22.com as follows:
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
@       IN      A       10.83.3.6     ; IP Kotalingga
www     IN      CNAME   rujapala.it22.com.' > /etc/bind/jarkom/rujapala.it22.com

service bind9 restart
```
- Specify hostname in NS records: airdrop.it22.com.
- Specify address in A records: 192.244.1.4
- Specify canonical name (alias) in CNAME records: airdrop.it22.com.

</details>

## SOAL 5
> Pastikan domain-domain tersebut dapat diakses oleh seluruh komputer (client) yang berada di Nusantara.
