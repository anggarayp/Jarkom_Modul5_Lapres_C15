# Jarkom_Modul5_Lapres_C15
Lapres Modul 5 Jarkom

### Nama Anggota Kelompok :
### 1. Anggara Yuda Pratama (05111840000008)
### 2. Patrick (05111840000098)

### Daftar Soal
* [Soal A](https://github.com/anggarayp/Jarkom_Modul5_Lapres_C15#soal-a)
* [Soal B](https://github.com/anggarayp/Jarkom_Modul5_Lapres_C15#soal-b)
* [Soal C](https://github.com/anggarayp/Jarkom_Modul5_Lapres_C15#soal-c)
* [Soal D](https://github.com/anggarayp/Jarkom_Modul5_Lapres_C15#soal-d)
* [No. 1](https://github.com/anggarayp/Jarkom_Modul5_Lapres_C15#nomor-1)
* [No. 2]()
* [No. 3]()
* [No. 4]()
* [No. 5]()
* [No. 6]()
* [No. 7]()

![topo](https://github.com/anggarayp/Jarkom_Modul5_Lapres_C15/blob/main/Screenshots/topo.png)

### Soal A

Membuat topologi jaringan sesuai dengan rancangan yang diberikan pada gambar di atas. Sekalian membuat ```bye.sh```nya.

- Topologi.sh

  ```
  # Switch
  uml_switch -unix switch0 > /dev/null < /dev/null & #A0
  uml_switch -unix switch1 > /dev/null < /dev/null & #A1
  uml_switch -unix switch2 > /dev/null < /dev/null & #A2
  uml_switch -unix switch3 > /dev/null < /dev/null & #A3
  uml_switch -unix switch4 > /dev/null < /dev/null & #A4
  uml_switch -unix switch5 > /dev/null < /dev/null & #A5

  # Router
  xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.76.65 eth1=daemon,,,switch0 eth2=daemon,,,switch3 mem=96M &
  xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch3 eth1=daemon,,,switch2 eth2=daemon,,,switch5 mem=96M &
  xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch0 eth1=daemon,,,switch1 eth2=daemon,,,switch4 mem=96M &

  # Server
  xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch1 mem=128M &
  xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch1 mem=128M &
  xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch2 mem=128M &
  xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch2 mem=128M &

  # Klien 1
  xterm -T GRESIK -e linux ubd0=GRESIK,jarkom umid=GRESIK eth0=daemon,,,switch4 mem=96M &
  xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch5 mem=96M &
  ```
  
- bye.sh

  ```
  uml_mconsole SURABAYA HALT
  uml_mconsole MALANG HALT
  uml_mconsole MOJOKERTO HALT
  uml_mconsole SIDOARJO HALT
  uml_mconsole GRESIK HALT
  uml_mconsole BATU HALT
  uml_mconsole KEDIRI HALT
  uml_mconsole PROBOLINGGO HALT
  uml_mconsole MADIUN  HALT
  ```

### Soal B

Membuat subnetting dengan teknik **CIDR** atau **VLSM**. Kelompok kami menggunakan teknik **VLSM**.

- Pembagian subnet dengan teknik VLSM
  
  ![subnet](https://github.com/anggarayp/Jarkom_Modul5_Lapres_C15/blob/main/Screenshots/subnet%20vlsm.png)
  
- IP Tree

  ![tree](https://github.com/anggarayp/Jarkom_Modul5_Lapres_C15/blob/main/Screenshots/vlsm%20tree%20modul5.png)
  
- Setting **Interfaces** tiap UML

  *UML Surabaya (Router)*

  ```
  auto lo
  iface lo inet loopback

  auto eth0
  iface eth0 inet static
  address 10.151.76.66
  netmask 255.255.255.252
  gateway 10.151.76.65

  auto eth1
  iface eth1 inet static
  address   192.168.0.1
  netmask 255.255.255.252

  auto eth2
  iface eth2 inet static
  address 192.168.0.5
  netmask 255.255.255.252
  ```

  *UML Kediri (Router)*

  ```
  auto lo
  iface lo inet loopback

  auto eth0
  iface eth0 inet static
  address 192.168.0.2
  netmask 255.255.255.252
  gateway 192.168.0.1

  auto eth1
  iface eth1 inet static
  address 192.168.0.9
  netmask 255.255.255.248

  auto eth2
  iface eth2 inet static
  address 192.168.1.1
  netmask 255.255.255.0
  ```

  *UML Batu (Router)*

  ```
  auto lo
  iface lo inet loopback

  auto eth0
  iface eth0 inet static
  address 192.168.0.6
  netmask 255.255.255.252
  gateway 192.168.0.5

  auto eth1
  iface eth1 inet static
  address 10.151.77.129 
  netmask 255.255.255.248

  auto eth2
  iface eth2 inet static
  address 192.168.2.1
  netmask 255.255.255.0
  ```

  *UML Sidoarjo (Client)*

  ```
  auto eth0
  iface eth0 inet static
  address 192.168.2.2
  netmask 255.255.255.0
  gateway 192.168.2.1
  ```

  *UML Gresik (Client)*

  ```
  auto eth0
  iface eth0 inet static
  address 192.168.1.2
  netmask 255.255.255.0
  gateway 192.168.1.1
  ```

  *UML Probolinggo (Server)*

  ```
  auto eth0
  iface eth1 inet static
  address 192.168.0.10
  netmask 255.255.255.248
  gateway 192.168.0.9
  ```

  *UML Mojokerto (Server)*

  ```
  auto eth0
  iface eth0 inet static
  address 10.151.77.130
  netmask 255.255.255.248
  gateway 10.151.77.129
  ```

  *UML Malang (Server)*

  ```
  auto eth0
  iface eth0 inet static
  address 10.151.77.131
  netmask 255.255.255.248
  gateway 10.151.77.129
  ```

  *UML Madiun (Server)*

  ```
  auto eth0
  iface eth0 inet static
  address 192.168.0.11
  netmask 255.255.255.252
  gateway 192.168.0.9
  ```

### Soal C

Melakukan routing agar setiap perangkat pada jaringan tersebut dapat terhubung.

- Routing pada UML Surabaya
  
  ```
  route add -net 192.168.1.0 netmask 255.255.255.0 gw 192.168.0.2
  route add -net 192.168.2.0 netmask 255.255.255.0 gw 192.168.0.6
  route add -net 192.168.0.8 netmask 255.255.255.248 gw 192.168.0.2
  route add -net 10.151.77.128 netmask 255.255.255.248 gw 192.168.0.6
  ```
  
### Soal D

Memberikan ip pada subnet SIDOARJO dan GRESIK secara dinamis menggunakan bantuan DHCP SERVER (Selain subnet tersebut menggunakan ip static). Kemudian setting DHCP RELAY pada router yang menghubungkannya.

- *UML Surabaya, Batu, dan Kediri*

  1. Buka file ```nano /etc/sysctl.conf```

  2. Tambahkan :

  ```
  net.ipv4.ip_forward=1
  net.ipv4.conf.all.accept_source_route = 1
  ```

  3. Lakukan ```sysctl -p```

  4. Install DHCP RELAY : ```apt-get install isc-dhcp-relay -y```

  5. Buka filenya ```nano /etc/default/isc-dhcp-relay```

  ![tree](https://github.com/anggarayp/Jarkom_Modul5_Lapres_C15/blob/main/Screenshots/kediri%20dhcp%20relay.png)

- *UML Mojokerto*

  1. Install DHCP : ```apt-get install isc-dhcp-server -y```

  2. Buka filenya ```nano /etc/default/isc-dhcp-server```

  3. Menambahkan ```INTERFACES="eth0"```

  4. Buka file ```nano /etc/dhcp/dhcpd.conf```

  5. Tambahkan :

  ```
  subnet 10.151.83.0 netmask 255.255.255.0 {  
          option routers 10.151.83.91; 
  }

  subnet 192.168.0.0 netmask 255.255.255.0 {
      option routers 10.151.83.89;
      option broadcast-address 192.168.0.255;
      option domain-name-servers 10.151.83.90;
  }

  subnet 192.168.2.0 netmask 255.255.255.0 {
      option routers 10.151.83.89;
      option broadcast-address 192.168.2.255;
      option domain-name-servers 10.151.83.90;
  }
  ```

### Nomor 1

Agar topologi yang dibuat dapat mengakses keluar, kita mengkonfigurasi SURABAYA menggunakan iptables, namun tidak menggunakan MASQUERADE.

- Pada *UML Surabaya* tambahkan perintah :
  
  ```
  iptables -t nat -A POSTROUTING -s 192.168.0.0/16 -o eth0 -j SNAT --to source 10.151.76.66
  ```

- Testing dengan cara ping **its.ac.id** di seluruh UML

### Nomor 2

Mendrop semua akses SSH dari luar Topologi (UML) kita pada server yang memiliki ip DMZ (DHCP dan DNS SERVER) pada SURABAYA demi menjaga keamanan.

- Pada *UML Surabaya* tambahkan perintah :

  ```
  iptables -A FORWARD -d 10.151.77.128/29 -i eth0 -p tcp --dport 22 -j DROP
  ```
  
- Testing

  1. Install netcat di *UML Mojokerto* dan *UML Malang* : ```apt-get install netcat```
  
  2. Pada UML Mojokerto dan Malang, ketikkan : ```nc -l -p <nomor_port>```
  
### Nomor 3

Membatasi DHCP dan DNS server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan yang berasal dari mana saja menggunakan iptables pada masing masing server, selebihnya akan di DROP.

- Pada *UML Mojokerto* dan *UML Malang* tambahkan perintah :

  ```
  iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
  ```

- Testing :

  1. Melakukan ping ke IP MALANG atau IP MOJOKERTO di 4 UML.
  
  2. Jika saat di UML ke 4 tidak bisa melakukan ping, maka berhasil.
  
### Nomor 4

Akses dari subnet SIDOARJO hanya diperbolehkan pada pukul 07.00 - 17.00 pada hari Senin sampai Jumat. Selain itu akan diREJECT.

Pada *UML Malang* tambahkan :

```
iptables -A INPUT -s 192.168.2.0/24 -m time --timestart 07:00 --timestop 17:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -s 192.168.2.0/24 -j REJECT
```

- Testing

  1. Ubah tanggal dan jam hari ini dengan perintah ```date -s '2020-12-27 :::'```
  
  2. Cek tanggal sudah benar atau belum dengan perintah ```date```

### Nomor 5

Akses dari subnet GRESIK hanya diperbolehkan pada pukul 17.00 hingga pukul 07.00 setiap harinya. Selain itu akan diREJECT.

Pada *UML Malang* tambahkan :

```
iptables -A INPUT -s 192.168.1.0/24 -m time --timestart 07:01 --timestop 16:59 -j REJECT
```

- Testing

  1. Ubah tanggal dan jam hari ini dengan perintah ```date -s '2020-12-27 :::'```
  
  2. Cek tanggal sudah benar atau belum dengan perintah ```date```

### Nomor 6

SURABAYA disetting sehingga setiap request dari client yang mengakses DNS Server akan didistribusikan secara bergantian pada PROBOLINGGO port 80 dan MADIUN port 80.

- Pada *UML Surabaya* :

  ```
  
  ```

- Testing
  
  1. Install netcat pada *UML Probolinggo* dan *UML Madiun* : ```apt-get install netcat```
  
  2. Pada Putty Yudhistira, ketikkan ``nc 10.151.77.90 22```
  
  3. Pada UML MADIUN dan PROBOLINGGO, ketikkan ```nc -l -p 22```
  
  4. Ketikkan sesuatu
  
  5.Apabila hasilnya seperti gambar di bawah, maka konfigurasi berhasil
  
### Nomor 7

Semua paket didrop oleh firewall (dalam topologi) tercatat dalam log pada setiap UML yang memiliki aturan drop.

- Pada *UML Surabaya* tambahkan :

  ```
  iptables -N LOGGING
  iptables -A INPUT -j LOGGING
  iptables -A OUTPUT -j LOGGING
  iptables -A LOGGING -j LOG --log-prefix "IPTables-Dropped: " --log-level 4
  iptables -A LOGGING -j DROP
  ```
  
- Testing

  1. Jalankan iptablesnya
  
  2. Pindah directory ke ```/var/log```
  
  3. Ketikkan perintah ```tail messages```
