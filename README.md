# Jarkom_Modul5_Lapres_C15
Lapres Modul 5 Jarkom

### Nama Anggota Kelompok :
### 1. Anggara Yuda Pratama (05111840000008)
### 2. Patrick (05111840000098)

### Daftar Soal
* [Soal A]()
* [Soal B]()
* [Soal C]()
* [Soal D]()
* [No. 1]()
* [No. 2]()
* [No. 3]()
* [No. 4]()
* [No. 5]()
* [No. 6]()
* [No. 7]()

![topo](https://github.com/anggarayp/Jarkom_Modul5_Lapres_C15/blob/main/Screenshots/topo.png)

### Soal A

Membuat topologi jaringan sesuai dengan rancangan yang diberikan pada gambar di atas.

- Topologi.sh

  ```
  # Switch
  uml_switch -unix switch0 > /dev/null < /dev/null &
  uml_switch -unix switch1 > /dev/null < /dev/null &
  uml_switch -unix switch2 > /dev/null < /dev/null &
  uml_switch -unix switch3 > /dev/null < /dev/null &
  uml_switch -unix switch4 > /dev/null < /dev/null &
  uml_switch -unix switch5 > /dev/null < /dev/null &

  # Router
  xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.76.64 eth1=daemon,,,switch0 eth2=daemon,,,switch3 mem=96M &
  xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch3 eth1=daemon,,,switch2 eth2=daemon,,,switch5 mem=96M &
  xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch0 eth1=daemon,,,switch1 eth2=daemon,,,switch4 mem=96M &

  # Server
  xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch2 mem=128M &
  xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch2 mem=128M &
  xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch1 mem=128M &
  xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch1 mem=128M &

  # Klien 1
  xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch4 mem=96M &
  xterm -T GRESIK -e linux ubd0=GRESIK,jarkom umid=GRESIK eth0=daemon,,,switch5 mem=96M &
  ```

### Soal B

Membuat subnetting dengan teknik **CIDR** atau **VLSM**. Kelompok kami menggunakan teknik **VLSM**.

- Pembagian subnet dengan teknik VLSM

- IP Tree

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
