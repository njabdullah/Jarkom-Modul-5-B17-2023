# Jarkom-Modul-5-B17-2023

## Anggota Kelompok
| Nama                       | NRP        |
| -------------------------- | ---------- |
| Abdullah Nasih Jasir       | 5025211111 |
| Yohanes Teguh Ukur Ginting | 5025211179 |

---

## **Soal Nomor 0**
Setelah pandai mengatur jalur-jalur khusus, kalian diminta untuk membantu North Area menjaga wilayah mereka dan kalian dengan senang hati membantunya karena ini merupakan tugas terakhir.

Topology beserta subnet
![image](https://github.com/njabdullah/Jarkom-Modul-5-B17-2023/assets/92930757/f72fe981-0e03-45af-983e-40e947c006e2)

---

Rute dalam penentuan subnetting
| Nama Subnet         | Rute                                    | Jumlah IP | Netmask |
|---------------------|-----------------------------------------|------------|---------|
| A1                  | Aura-Heiter                             | 2          | /30     |
| A2                  | Heiter-TurkRegion(1022)                 | 1023       | /21     |
| A3                  | Heiter-Switch1-Sein-Switch1-GrobeForest | 514        | /22     |
| A4                  | Aura-Frieren                            | 2          | /30     |
| A5                  | Frieren-Startk                          | 2          | /30     |
| A6                  | Frieren-Himmel                          | 2          | /30     |
| A7                  | Himmel-LaubHills                        | 256        | /23     |
| A8                  | Himmel-Switch2-SchwerMountains-Switch2-Fern | 66    | /25     |
| A9                  | Fern-Richter                            | 2          | /30     |
| A10                 | Fern-Switch3-Revolte                    | 2          | /30     |
| Total               |                                         | 1871       |         |

---

Perhitungan dengan VLSM (dalam bentuk tree)

![image](https://github.com/njabdullah/Jarkom-Modul-5-B17-2023/assets/92930757/9b51cf1f-1fd4-4946-8b1b-29bfa47a3685)

---

Pembagian NID, Netmask, dan Broadcast
| Subnet | Network ID | Netmask       | Broadcast    | Netmask |
|--------|------------|---------------|--------------|---------|
| A1     | 10.17.14.128 | 255.255.255.252 | 10.17.14.131 | /30     |
| A2     | 10.17.0.0  | 255.255.248.0 | 10.17.7.255  | /21     |
| A3     | 10.17.8.0  | 255.255.252.0 | 10.17.11.255 | /22     |
| A4     | 10.17.14.132 | 255.255.255.252 | 10.17.14.135 | /30     |
| A5     | 10.17.14.136 | 255.255.255.252 | 10.17.14.139 | /30     |
| A6     | 10.17.14.140 | 255.255.255.252 | 10.17.14.143 | /30     |
| A7     | 10.17.12.0 | 255.255.254.0 | 10.17.13.255 | /23     |
| A8     | 10.17.14.0 | 255.255.255.128 | 10.17.14.127 | /25     |
| A9     | 10.17.14.144 | 255.255.255.252 | 10.17.14.147 | /30     |
| A10    | 10.17.14.148 | 255.255.255.252 | 10.17.14.151 | /30     |

---

Pembagian IP setiap node

| Subnet | Node      | Eth   | IP            | Netmask       | Gateway      |
|--------|-----------|-------|---------------|---------------|--------------|
| A1     | Aura      | eth1  | 10.17.14.129  | 255.255.255.252 |              |
|        | Heiter    | eth0  | 10.17.14.130  |               | 10.17.14.129 |
| A2     | Heiter    | eth1  | 10.17.0.1     | 255.255.248.0 |              |
|        | TurkRegion| eth0  | 10.17.0.2     |               | 10.17.0.1    |
| A3     | Heiter    | eth2  | 10.17.8.1     | 255.255.252.0 |              |
|        | GrobeForest| eth0 | 10.17.8.3     |               | 10.17.8.1    |
|        | Sein      | eth0  | 10.17.8.2     |               | 10.17.8.1    |
| A4     | Aura      | eth2  | 10.17.14.133  | 255.255.255.252 |              |
|        | Frieren   | eth0  | 10.17.14.134  |               | 10.17.14.133 |
| A5     | Frieren   | eth2  | 10.17.14.137  | 255.255.255.252 |              |
|        | Stark     | eth0  | 10.17.14.138  |               | 10.17.14.137 |
| A6     | Frieren   | eth1  | 10.17.14.141  | 255.255.255.252 |              |
|        | Himmel    | eth0  | 10.17.14.142  |               | 10.17.14.141 |
| A7     | Himmel    | eth1  | 10.17.12.1    | 255.255.254.0 |              |
|        | LaubHills | eth0  | 10.17.12.2    |               | 10.17.12.1   |
| A8     | Himmel    | eth2  | 10.17.14.1    | 255.255.255.128 |             |
|        | SchwerMountains| eth0 | 10.17.14.3 |               | 10.17.14.1   |
|        | Fern      | eth0  | 10.17.14.2    |               | 10.17.14.1   |
| A9     | Fern      | eth1  | 10.17.14.145  | 255.255.255.252 |             |
|        | Richter   | eth0  | 10.17.14.146  |               | 10.17.14.145 |
| A10    | Fern      | eth2  | 10.17.14.149  | 255.255.255.252 |             |
|        | Revolte   | eth0  | 10.17.14.150  |               | 10.17.14.149 |

---
Configurasi Setiap Node<br>
Aura
    
    auto eth0
    iface eth0 inet dhcp
    
    auto eth1
    iface eth1 inet static
    	address 10.17.14.129
    	netmask 255.255.255.252
    
    auto eth2
    iface eth2 inet static
    	address 10.17.14.133
    	netmask 255.255.255.252

Heiter

    auto eth0
    iface eth0 inet static
    	address 10.17.14.130
    	netmask 255.255.255.252
            	gateway 10.17.14.129
    
    auto eth1
    iface eth1 inet static
    	address 10.17.0.1
    	netmask 255.255.248.0
    
    auto eth2
    iface eth2 inet static
    	address 10.17.8.1
    	netmask 255.255.252.0

TurkRegion

    auto eth0
    iface eth0 inet dhcp

GrobeForest

    auto eth0
    iface eth0 inet dhcp

Sein

    auto eth0
    iface eth0 inet static
    	address 10.17.8.2
    	netmask 255.255.252.0
    	gateway 10.17.8.1

Frieren

    auto eth0
    iface eth0 inet static
    	address 10.17.14.134
    	netmask 255.255.255.252
        gateway 10.17.14.133

    auto eth1
    iface eth1 inet static
    	address 10.17.14.141
    	netmask 255.255.255.252
    
    auto eth2
    iface eth2 inet static
    	address 10.17.14.137
    	netmask 255.255.255.252

Stark

    auto eth0
    iface eth0 inet static
    	address 10.17.14.138
    	netmask 255.255.255.252
        gateway 10.17.14.137

Himmel

    auto eth0
    iface eth0 inet static
    	address 10.17.14.142
    	netmask 255.255.255.252
            gateway 10.17.14.141
    
    auto eth1
    iface eth1 inet static
    	address 10.17.12.1
    	netmask 255.255.254.0
    
    auto eth2
    iface eth2 inet static
    	address 10.17.14.1
    	netmask 255.255.255.128

Laubhills

    auto eth0
    iface eth0 inet dhcp

SchewerMountain

    auto eth0
    iface eth0 inet dhcp

Richter

    auto eth0
    iface eth0 inet static
    	address 10.17.14.146
    	netmask 255.255.255.252
        gateway 10.17.14.145

Fern

    auto eth0
    iface eth0 inet static
    	address 10.17.14.2
    	netmask 255.255.255.128
        gateway 10.17.14.1
    
    auto eth1
    iface eth1 inet static
    	address 10.17.14.145
    	netmask 255.255.255.252
    
    auto eth2
    iface eth2 inet static
        address 10.17.14.149
    	netmask 255.255.255.252

Revolte

    auto eth0
    iface eth0 inet static
    	address 10.17.14.150
    	netmask 255.255.255.252
        gateway 10.17.14.149

---

Routing

Aura

    route add -net 10.17.0.0 netmask 255.255.248.0 gw 10.17.14.130
    route add -net 10.17.8.0 netmask 255.255.252.0 gw 10.17.14.130
    route add -net 10.17.14.136 netmask 255.255.255.252 gw 10.17.14.134
    route add -net 10.17.14.140 netmask 255.255.255.252 gw 10.17.14.134
    route add -net 10.17.12.0 netmask 255.255.254.0 gw 10.17.14.134
    route add -net 10.17.14.0 netmask 255.255.255.128 gw 10.17.14.134
    route add -net 10.17.14.144 netmask 255.255.255.252 gw 10.17.14.134
    route add -net 10.17.14.148 netmask 255.255.255.252 gw 10.17.14.134

Frieren

    route add -net 10.17.12.0 netmask 255.255.254.0 gw 10.17.14.142
    route add -net 10.17.14.0 netmask 255.255.255.128 gw 10.17.14.142
    route add -net 10.17.14.144 netmask 255.255.255.252 gw 10.17.14.142
    route add -net 10.17.14.148 netmask 255.255.255.252 gw 10.17.14.142

Himmel

    route add -net 0.0.0.0 netmask 0.0.0.0 gw 10.17.14.141
    route add -net 10.17.14.144 netmask 255.255.255.252 gw 10.17.14.2
    route add -net 10.17.14.148 netmask 255.255.255.252 gw 10.17.14.2

## **Soal Nomor 1**
Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.

## **Penyelesaian Nomor 1**

---

## **Soal Nomor 2**
Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.

## **Penyelesaian Nomor 2**

---

## **Soal Nomor 3**
Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.

## **Penyelesaian Nomor 3**

---

## **Soal Nomor 4**
Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.

## **Penyelesaian Nomor 4**

---

## **Soal Nomor 5**
Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.

## **Penyelesaian Nomor 5**

---

## **Soal Nomor 6**
Lalu, karena ternyata terdapat beberapa waktu di mana network administrator dari WebServer tidak bisa stand by, sehingga perlu ditambahkan rule bahwa akses pada hari Senin - Kamis pada jam 12.00 - 13.00 dilarang (istirahat maksi cuy) dan akses di hari Jumat pada jam 11.00 - 13.00 juga dilarang (maklum, Jumatan rek).

## **Penyelesaian Nomor 6**
Di Web Server (Sein dan Stark)

    iptables -A INPUT -p tcp --dport 80 -m time --timestart 13:01 --timestop 10:59 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
    iptables -A INPUT -p tcp --dport 80 -m time --timestart 12:00 --timestop 13:00 --weekdays Mon,Tue,Wed,Thu -j DROP
    iptables -A INPUT -p tcp --dport 80 -m time --timestart 11:00 --timestop 13:00 --weekdays Fri -j DROP
    iptables -A INPUT -p tcp --dport 80 -j DROP

Lalu, lakukan testing di client (saya run di TurkRegion) dengan mengubah tanggalnya terlebih dahulu

    nmap 10.17.8.2
    nmap 10.17.14.138
    
![image](https://github.com/njabdullah/Jarkom-Modul-5-B17-2023/assets/92930757/fe2c1899-d423-4b60-82b8-e545d2468d6c)
![image](https://github.com/njabdullah/Jarkom-Modul-5-B17-2023/assets/92930757/cd8c6bb9-eb58-440e-97d9-9e391b80866b)

Pada hari Senin, 18 Desember 2023 pukul 12.30 muncul filterred

---

## **Soal Nomor 7**
Karena terdapat 2 WebServer, kalian diminta agar setiap client yang mengakses Sein dengan Port 80 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan dan request dari client yang mengakses Stark dengan port 443 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan.

## **Penyelesaian Nomor 7**
Di Router yang menempel dengan Web Server (Heiter dan Frieren)

    iptables -A PREROUTING -t nat -p tcp --dport 80 -d 10.17.8.2 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 10.17.14.138
    
    iptables -A PREROUTING -t nat -p tcp --dport 80 -d 10.17.8.2 -j DNAT --to-destination 10.17.14.138
    
    iptables -A PREROUTING -t nat -p tcp --dport 443 -d 10.17.14.138 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 10.17.8.2
    
    iptables -A PREROUTING -t nat -p tcp --dport 443 -d 10.17.14.138 -j DNAT --to-destination 10.17.8.2

lalu, lakukan testing di client (saya run di TurkRegion) deengan meengubah tanggalnya terlebih dahulu

Di Sein, jalankan

    while true; do nc -l -p 80 -c 'echo "ini sein bro"'; done

Di Stark, jalankan

    while true; do nc -l -p 80 -c 'echo "ini stark bro"'; done

Lalu, di client TurkRegion, jalankan

    nc 10.17.8.2 80
    nc 10.17.14.138 80

![image](https://github.com/njabdullah/Jarkom-Modul-5-B17-2023/assets/92930757/47ec18f3-e281-4a82-a8b2-9dd087187d11)

---

## **Soal Nomor 8**
Karena berbeda koalisi politik, maka subnet dengan masyarakat yang berada pada Revolte dilarang keras mengakses WebServer hingga masa pencoblosan pemilu kepala suku 2024 berakhir. Masa pemilu (hingga pemungutan dan penghitungan suara selesai) kepala suku bersamaan dengan masa pemilu Presiden dan Wakil Presiden Indonesia 2024.

## **Penyelesaian Nomor 8**
Di web server (Sein dan Stark), lakukan seperti di bawah ini

    iptables -A INPUT -s 10.17.14.150 -p tcp --dport 80 -m time --datestart 2023-12-14 --datestop 2024-06-26 -j DROP

Lalu, lakukan testing di Revolte dengan mengganti date teerlebih dahulu dan memasukkan syntax berikut

    nmap 10.17.8.2 80
    nmap 10.17.14.138 80

Jika disetting pada masa pemilu
![image](https://github.com/njabdullah/Jarkom-Modul-5-B17-2023/assets/92930757/95f16b34-e42c-4f0c-91f9-4776865883ec)

Jika disetting di luar masa pemilu
![image](https://github.com/njabdullah/Jarkom-Modul-5-B17-2023/assets/92930757/5d643213-5ebe-4ef4-9e1e-63920c05cb2a)

---

## **Soal Nomor 9**
Sadar akan adanya potensial saling serang antar kubu politik, maka WebServer harus dapat secara otomatis memblokir  alamat IP yang melakukan scanning port dalam jumlah banyak (maksimal 20 scan port) di dalam selang waktu 10 menit (clue: test dengan nmap).

## **Penyelesaian Nomor 9**
Lakukan setting di wweb server (sein dan stark) dan masukkan configurasi sebagai berikut

    iptables -N scan_port
    
    iptables -A INPUT -m recent --name scan_port --update --seconds 600 --hitcount 20 -j DROP
    
    iptables -A FORWARD -m recent --name scan_port --update --seconds 600 --hitcount 20 -j DROP
    
    iptables -A INPUT -m recent --name scan_port --set -j ACCEPT
    
    iptables -A FORWARD -m recent --name scan_port --set -j ACCEPT

Lalu, lakukan setting dengan menjalankan syntax berikut di GrobeForest

    ping 10.17.8.2
    ping 10.17.14.138

![image](https://github.com/njabdullah/Jarkom-Modul-5-B17-2023/assets/92930757/0c046779-d1c3-4ab0-ab66-c20478f24bdd)
![image](https://github.com/njabdullah/Jarkom-Modul-5-B17-2023/assets/92930757/d79b514f-cc9f-46bf-92db-2e3bcb208610)

---

## **Soal Nomor 10**
Karena kepala suku ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level. 

## **Penyelesaian Soal Nomor 10**
Masukkan syntax berikut ke setiap node server (DNS, DHCP, Web) dan setiap router

    iptables -A INPUT  -j LOG --log-level debug --log-prefix 'Dropped Packet' -m limit --limit 1/second --limit-burst 10

![image](https://github.com/njabdullah/Jarkom-Modul-5-B17-2023/assets/92930757/2deb8908-f00a-4f6b-a1c9-cedcab106800)

