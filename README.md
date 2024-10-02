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
| Device      | Interface | IP Address | Netmask       | Gateway     |
|-------------|-----------|------------|---------------|-------------|
| **Erangel** | eth0      | DHCP (192.168.122.1)       |               |             |
|             | eth1      | 192.244.1.2| 255.255.255.0 |             |
|             | eth2      | 192.244.2.2| 255.255.255.0 |             |
|             | eth3      | 192.244.3.2| 255.255.255.0 |             |
| **Pochinki**| eth0      | 192.244.3.1| 255.255.255.0 | 192.244.3.2 |
| **Georgopol**| eth0     | 192.244.2.1| 255.255.255.0 | 192.244.2.2 |
| **Severny** | eth0      | 192.244.1.3| 255.255.255.0 | 192.244.1.2 |
| **Stalber** | eth0      | 192.244.1.4| 255.255.255.0 | 192.244.1.2 |
| **Lipovka** | eth0      | 192.244.1.5| 255.255.255.0 | 192.244.1.2 |
| **MyIta**   | eth0      | 192.244.2.3| 255.255.255.0 | 192.244.2.2 |
| **Ruins**   | eth0      | 192.244.2.4| 255.255.255.0 | 192.244.2.2 |
| **Apartments**| eth0    | 192.244.2.5| 255.255.255.0 | 192.244.2.2 |
 

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

```

### Majapahit (DNS Slave)
```

```

### Tanjungkulai (Web Server)
```

```

### Bedahulu (Web Server)
```

```

### Kotalingga (Web Server)
```

```

### Solok (Load Balancer)
```

```

### Samaratungga (Client)
```

```

### Mulawarman (Client)
```

```

### AlexanderVolta (Client)
```

```

### Balaraja (Client)
```

```

</details>


## Keterangan setiap file
`DiscorIT`
| File | Isi | Keterangan |
| :---:| :--- | :---      |
| `users.csv` | id_user |  int (mulai dari 1) |
|      | name | string |
|      | password |  string (di encrypt menggunakan bcrypt biar ga tembus) |
|      | global_role | string (pilihannya: ROOT / USER) |
| `channels.csv` | id_channel | int  (mulai dari 1) |
|      | channel | string |
|      | key |  string (di encrypt menggunakan bcrypt biar ga tembus) |

`Channels`
| File | Isi | Keterangan |
| :---:| :--- | :---      |
| `auth.csv` | id_user | int |
|      | name | string |
|      | role | string (pilihannya: ROOT/ADMIN/USER/BANNED) |
| `user.log` | [dd/mm/yyyy HH:MM:SS] | admin buat room1 |
|      | [dd/mm/yyyy HH:MM:SS] | user1 masuk ke channel “say hi” |
|      | [dd/mm/yyyy HH:MM:SS] | admin memberi role1 kepada user1 |
|      | [dd/mm/yyyy HH:MM:SS] | admin ban user1 |

`Rooms`
| File | Isi | Keterangan |
| :---:| :--- | :---      |
| `chat.csv` | date | int |
|      | id_chat | number  (mulai dari 1) |
|      | sender | string |
|      | chat | string |
