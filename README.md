# Lapres Pratikum Jarkom-Modul-2-IT22-2024

**KELOMPOK IT22**
| Nama | NRP |
|---------------------------|------------|
|Muhamad Arrayyan | 5027231014 |
|Fadlillah Cantika Sari Hermawan | 5027231042 |

### Keterangan setiap file
  
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
