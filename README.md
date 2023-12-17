# Jarkom-Modul-5-B17-2023

## Anggota Kelompok
| Nama                       | NRP        |
| -------------------------- | ---------- |
| Abdullah Nasih Jasir       | 5025211111 |
| Yohanes Teguh Ukur Ginting | 5025211179 |


## **Soal Nomor 0**
Setelah pandai mengatur jalur-jalur khusus, kalian diminta untuk membantu North Area menjaga wilayah mereka dan kalian dengan senang hati membantunya karena ini merupakan tugas terakhir.

## **Soal Nomor 1**
Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Aura menggunakan iptables, tetapi tidak ingin menggunakan MASQUERADE.

## **Penyelesaian Nomor 1**

## **Soal Nomor 2**
Kalian diminta untuk melakukan drop semua TCP dan UDP kecuali port 8080 pada TCP.

## **Penyelesaian Nomor 2**

## **Soal Nomor 3**
Kepala Suku North Area meminta kalian untuk membatasi DHCP dan DNS Server hanya dapat dilakukan ping oleh maksimal 3 device secara bersamaan, selebihnya akan di drop.

## **Penyelesaian Nomor 3**

## **Soal Nomor 4**
Lakukan pembatasan sehingga koneksi SSH pada Web Server hanya dapat dilakukan oleh masyarakat yang berada pada GrobeForest.

## **Penyelesaian Nomor 4**

## **Soal Nomor 5**
Selain itu, akses menuju WebServer hanya diperbolehkan saat jam kerja yaitu Senin-Jumat pada pukul 08.00-16.00.

## **Penyelesaian Nomor 5**

## **Soal Nomor 6**
Lalu, karena ternyata terdapat beberapa waktu di mana network administrator dari WebServer tidak bisa stand by, sehingga perlu ditambahkan rule bahwa akses pada hari Senin - Kamis pada jam 12.00 - 13.00 dilarang (istirahat maksi cuy) dan akses di hari Jumat pada jam 11.00 - 13.00 juga dilarang (maklum, Jumatan rek).

## **Penyelesaian Nomor 6**
Di Web Server (Sein dan Stark)

    iptables -A INPUT -p tcp --dport 22 -s 10.17.8.3/22 -m time --timestart 08:00
    iptables -A INPUT -p tcp --dport 22 -j DROP
    
    iptables -A INPUT -p tcp --dport 22 -s 10.17.8.3/22 -m time --timestart 12:00
    iptables -A INPUT -p tcp --dport 22 -s 10.17.8.3/22 -m time --timestart 11:00

Lalu, lakukan testing di client (saya run di GrabeForest) dengan mengubah tanggalnya terlebih dahulu

    nmap 10.17.8.2
    nmap 10.17.14.138

## **Soal Nomor 7**
Karena terdapat 2 WebServer, kalian diminta agar setiap client yang mengakses Sein dengan Port 80 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan dan request dari client yang mengakses Stark dengan port 443 akan didistribusikan secara bergantian pada Sein dan Stark secara berurutan.

## **Penyelesaian Nomor 7**
Di Router yang menempel dengan Web Server (Heiter dan Frieren)

    iptables -A PREROUTING -t nat -p tcp --dport 80 -d 10.17.8.2 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 10.17.14.138
    
    iptables -A PREROUTING -t nat -p tcp --dport 80 -d 10.17.8.2 -j DNAT --to-destination 10.17.14.138
    
    iptables -A PREROUTING -t nat -p tcp --dport 443 -d 10.17.14.138 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 10.17.8.2
    
    iptables -A PREROUTING -t nat -p tcp --dport 443 -d 10.17.14.138 -j DNAT --to-destination 10.17.8.2

lalu, lakukan testing di client (saya run di GrabeForest) deengan meengubah tanggalnya terlebih dahulu

Di Sein, jalankan

    while true; do nc -l -p 80 -c 'echo "ini sein bro"'; done

Di Stark, jalankan

    while true; do nc -l -p 80 -c 'echo "ini stark bro"'; done

Lalu, di client GrabeForest, jalankan

    nc 10.17.8.2 80
    nc 10.17.14.138 80
    
## **Soal Nomor 8**
Karena berbeda koalisi politik, maka subnet dengan masyarakat yang berada pada Revolte dilarang keras mengakses WebServer hingga masa pencoblosan pemilu kepala suku 2024 berakhir. Masa pemilu (hingga pemungutan dan penghitungan suara selesai) kepala suku bersamaan dengan masa pemilu Presiden dan Wakil Presiden Indonesia 2024.

## **Penyelesaian Nomor 8**
Di web server (Sein dan Stark), lakukan seperti di bawah ini

    iptables -A INPUT -s 10.17.14.150 -p tcp --dport 80 -m time --datestart 2023-12-14 --datestop 2024-06-26 -j DROP

Lalu, lakukan testing di Revolte dengan mengganti date teerlebih dahulu dan memasukkan syntax berikut

    nmap 10.17.8.2 80
    nmap 10.17.14.138 80

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

## **Soal Nomor 10**
Karena kepala suku ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level. 

Masukkan syntax berikut ke setiap node server (DNS, DHCP, Web) dan setiap router

    iptables -A INPUT  -j LOG --log-level debug --log-prefix 'Dropped Packet' -m limit --limit 1/second --limit-burst 10

## **Penyelesaian Soal Nomor 10**
