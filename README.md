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
 

<details>

<summary>Detail Configure</summary>

#### Nusantara (Router)
```
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
```
auto eth0
iface eth0 inet static
	address 192.244.3.5
	netmask 255.255.255.0
	gateway 192.244.3.1
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Majapahit (DNS Slave)
```
auto eth0
iface eth0 inet static
	address 192.244.2.2
	netmask 255.255.255.0
	gateway 192.244.2.1
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Tanjungkulai (Web Server)
```
auto eth0
iface eth0 inet static
	address 192.244.2.3
	netmask 255.255.255.0
	gateway 192.244.2.1
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Bedahulu (Web Server)
```
auto eth0
iface eth0 inet static
	address 192.244.2.4
	netmask 255.255.255.0
	gateway 192.244.2.1
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Kotalingga (Web Server)
```
auto eth0
iface eth0 inet static
	address 192.244.3.6
	netmask 255.255.255.0
	gateway 192.244.3.1
	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Solok (Load Balancer)
```
auto eth0
iface eth0 inet static
	address 192.244.1.3
	netmask 255.255.255.0
	gateway 192.244.1.1
#	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Samaratungga (Client)
```
auto eth0
iface eth0 inet static
	address 192.244.1.2
	netmask 255.255.255.0
	gateway 192.244.1.1
#	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Mulawarman (Client)
```
auto eth0
iface eth0 inet static
	address 192.244.3.2
	netmask 255.255.255.0
	gateway 192.244.3.1
#	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### AlexanderVolta (Client)
```
auto eth0
iface eth0 inet static
	address 192.244.3.3
	netmask 255.255.255.0
	gateway 192.244.3.1
#	up echo nameserver 192.168.0.1 > /etc/resolv.conf
```

### Balaraja (Client)
```
auto eth0
iface eth0 inet static
	address 192.244.3.4
	netmask 255.255.255.0
	gateway 192.244.3.1
#	up echo nameserver 192.168.122.1 > /etc/resolv.conf
```

</details>
