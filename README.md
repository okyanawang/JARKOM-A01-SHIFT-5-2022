# JARKOM-A01-SHIFT-5-2022

## Kelompok A01

| **No** | **Nama**              | **NRP**    |
| ------ | --------------------- | ---------- |
| 1      | Okyan Awang Ramadhana | 5025201252 |
| 2      | M Dzikri Fakhrizal    | 5025201201 |
| 3      | Fachrendy Zulfikar A  | 5025201018 |

## List

1. [Soal A](#Question-A)
2. [Soal B](#Question-B)
3. [Soal C](#Question-C)
4. [Soal D](#Question-D)
5. [Soal 1](#Question-1)
6. [Soal 2](#Question-2)
7. [Soal 3](#Question-3)
8. [Soal 4](#Question-4)
9. [Soal 5](#Question-5)
10. [Soal 6](#Question-6)

## Konfigurasi

- **Strix**

    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet dhcp
    hwaddress ether 6e:96:f5:fa:c5:4b

    auto eth1
    iface eth1 inet static
    address 192.169.7.145
    netmask 255.255.255.252

    auto eth2
    iface eth2 inet static
    address 192.169.7.149
    netmask 255.255.255.252
    ```

- **Ostania**

    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 192.169.7.150
    netmask 255.255.255.252
    gateway 192.169.7.149

    auto eth1
    iface eth1 inet static
    address 192.169.7.137
    netmask 255.255.255.248

    auto eth2
    iface eth2 inet static
    address 192.169.4.1
    netmask 255.255.254.0

    auto eth3
    iface eth3 inet static
    address 192.169.6.1
    netmask 255.255.255.0
    ```

- **Westalis**

    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet static
    address 192.169.7.146
    netmask 255.255.255.252
    gateway 192.169.7.145

    auto eth1
    iface eth1 inet static
    address 192.169.7.129
    netmask 255.255.255.248

    auto eth2
    iface eth2 inet static
    address 192.169.7.1
    netmask 255.255.255.128

    auto eth3
    iface eth3 inet static
    address 192.169.0.1
    netmask 255.255.252.0
    ```

- **Eden**

    ```
    auto eth0
    iface eth0 inet static
    address 192.169.7.130
    netmask 255.255.255.248
    gateway 192.169.7.129
    ```

- **Wise**

    ```
    auto eth0
    iface eth0 inet static
    address 192.169.7.131
    netmask 255.255.255.248
    gateway 192.169.7.129
    ```

- **Garden**

    ```
    auto eth0
    iface eth0 inet static
    address 192.169.7.138
    netmask 255.255.255.248
    gateway 192.169.7.137
    ```

- **SSS**

    ```
    auto eth0
    iface eth0 inet static
    address 192.169.7.139
    netmask 255.255.255.248
    gateway 192.169.7.137
    ```

- **Semua Client**

    ```
    auto lo
    iface lo inet loopback

    auto eth0
    iface eth0 inet dhcp
    ```

## Question A

> Tugas pertama kalian yaitu membuat topologi jaringan sesuai dengan rancangan yang diberikan Loid dibawah ini:
> 1. Eden adalah DNS Server
> 2. WISE adalah DHCP Server
> 3. Garden dan SSS adalah Web Server
> 4. Jumlah Host pada Forger adalah 62 host
> 5. Jumlah Host pada Desmond adalah 700 host
> 6. Jumlah Host pada Blackbell adalah 255 host
> 7. Jumlah Host pada Briar adalah 200 host

### Answer

![image](https://user-images.githubusercontent.com/90445721/206849799-4f1b9345-2331-4fdf-b1fc-f42e0b0e9b0f.png)

## Question B

> Untuk menjaga perdamaian dunia, Loid ingin meminta kalian untuk membuat topologi tersebut menggunakan teknik CIDR atau VLSM setelah melakukan subnetting.

### Answer
Dalam mengerjakan praktikum modul 5, kami menggunakan teknik VLSM.

Pertama, tentukan subnet pada topologi. Setelah itu, setiap subnet akan dicatat berapa jumlah IP yang dibutuhkan dan netmask yang dihasilkan sesuai dengan node yang terhubung.

![image](https://user-images.githubusercontent.com/90445721/206849866-c5191774-a83d-48eb-ab75-b96bd0d066fb.png)

Setelah mendapatkan jumlah IP dari masing-masing subnet, buat VLSM Treenya. Dengan subnet induk `192.169.0.0` dengan netmask /21, lakukan pembagian IP sampai subnet paling bawah

![image](https://user-images.githubusercontent.com/90445721/206849873-82a5bd5f-8166-4b25-b6e4-6df89b04a8f1.png)

Gambar di bawah ini adalah hasil pembagian dari VLSM Tree. Dengan NID per setiap subnet dan nama devicenya.

![image](https://user-images.githubusercontent.com/90445721/206849878-8b4b5bee-f997-4d37-b2fc-269be1545a1b.png)

## Question C

> Anya, putri pertama Loid, juga berpesan kepada anda agar melakukan Routing agar setiap perangkat pada jaringan tersebut dapat terhubung.

### Script

Setelah lakukan network configuration pada setiap node, lakukan routing pada GNS3 agar semua router, client, dan server saling terhubung.

- **Westalis**
    ```
    # kiri
    route add -net 192.169.7.128 netmask 255.255.255.248 gw 192.169.7.146
    route add -net 192.169.7.0 netmask 255.255.255.128 gw 192.169.7.146
    route add -net 192.169.0.0 netmask 255.255.252.0 gw 192.169.7.146

    # kanan
    route add -net 192.169.4.0 netmask 255.255.254.0 gw 192.169.7.150
    route add -net 192.169.6.0 netmask 255.255.255.0 gw 192.169.7.150
    route add -net 192.169.7.136  netmask 255.255.255.248 gw 192.169.7.150
    ```

### Test

![image](https://user-images.githubusercontent.com/90445721/206849897-381417b8-bd44-4921-852d-1e6874c69b0a.png)

## Question D

> Tugas berikutnya adalah memberikan ip pada subnet Forger, Desmond, Blackbell, dan Briar secara dinamis menggunakan bantuan DHCP server. Kemudian kalian ingat bahwa kalian harus setting DHCP Relay pada router yang menghubungkannya.

### Script

Pada Ostania dan Westalis, install `apt-get install isc-dhcp-relay -y`. Kemudian edit server dengan mengarahkan dhcp-relay menuju WISE `192.169.7.131` lalu tambahkan interfaces. Lakukan `service isc-dhcp-relay start`.

- **Ostania**
    ```
    echo "nameserver 192.168.122.1" > /etc/resolv.conf

    apt-get update
    echo "" | apt-get install isc-dhcp-relay -y

    echo -e '
    # Defaults for isc-dhcp-relay initscript
    # sourced by /etc/init.d/isc-dhcp-relay
    # installed at /etc/default/isc-dhcp-relay by the maintainer scripts

    #
    # This is a POSIX shell fragment
    #

    # What servers should the DHCP relay forward requests to?
    SERVERS="192.169.7.131"

    # On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
    INTERFACES="eth0 eth1 eth2 eth3"

    # Additional options that are passed to the DHCP relay daemon?
    OPTIONS=""
    ' > /etc/default/isc-dhcp-relay

    service isc-dhcp-relay start
    ```


- **Westalis**
    ```
    echo "nameserver 192.168.122.1" > /etc/resolv.conf
    
    apt-get update
    echo "" | apt-get install isc-dhcp-relay -y
    
    echo -e '
    # Defaults for isc-dhcp-relay initscript
    # sourced by /etc/init.d/isc-dhcp-relay
    # installed at /etc/default/isc-dhcp-relay by the maintainer scripts
    
    #
    # This is a POSIX shell fragment
    #
    
    # What servers should the DHCP relay forward requests to?
    SERVERS="192.169.7.131"
    
    # On what interfaces should the DHCP relay (dhrelay) serve DHCP requests?
    INTERFACES="eth0 eth1 eth2 eth3"
    
    # Additional options that are passed to the DHCP relay daemon?
    OPTIONS=""
    ' > /etc/default/isc-dhcp-relay
    
    service isc-dhcp-relay start
    ```

Pada Eden, install `apt-get install bind9 -y`, kemudian masukkan nameservers. Lakukan `service bind9 start`.

- **Eden**
    ```
    echo "nameserver 192.168.122.1" > /etc/resolv.conf

    apt-get update
    apt-get install bind9 -y

    echo -e '
    options {
            directory "/var/cache/bind";

            // If there is a firewall between you and nameservers you want
            // to talk to, you may need to fix the firewall to allow multiple
            // ports to talk.  See http://www.kb.cert.org/vuls/id/800113
               forwarders {
                    192.168.122.1;
               };

            //========================================================================
            // If BIND logs error messages about the root key being expired,
            // you will need to update your keys.  See https://www.isc.org/bind-keys
            //========================================================================
            //dnssec-validation auto;
            allow-query{any;};
            auth-nxdomain no;    # conform to RFC1035
            listen-on-v6 { any; };
    };
    ' > /etc/bind/named.conf.options

    service bind9 start
    ```

Pada WISE, edit file `/etc/default/isc-dhcp-server`, dengan menambahkan `INTERFACES="eth0"`. Pada dhcp-server isikan data pada `/etc/dhcp/dhcpd.conf` di WISE, lalu lakukan `service isc-dhcp-server restart`.

- **Wise**
    ```
    echo "nameserver 192.168.122.1" > /etc/resolv.conf

    apt-get update
    apt-get install isc-dhcp-server -y

    echo -e '
    INTERFACES="eth0"
    ' > /etc/default/isc-dhcp-server

    echo -e '
    # Forger A2
    subnet 192.169.7.0 netmask 255.255.255.128 {
            range 192.169.7.2 192.169.7.126;
            option routers 192.169.7.1;
            option broadcast-address 192.169.7.127;
            option domain-name-servers 192.169.7.130;
            default-lease-time 600;
            max-lease-time 7200;
    }

    # Desmond A3
    subnet 192.169.0.0 netmask 255.255.252.0 {
            range 192.169.0.2 192.169.3.254;
            option routers 192.169.0.1;
            option broadcast-address 192.169.3.255;
            option domain-name-servers 192.169.7.130;
            default-lease-time 600;
            max-lease-time 7200;
    }


    # Blackbell A6
    subnet 192.169.4.0 netmask 255.255.254.0 {
            range 192.169.4.2 192.169.5.254;
            option routers 192.169.4.1;
            option broadcast-address 192.169.5.255;
            option domain-name-servers 192.169.7.130;
            default-lease-time 600;
            max-lease-time 7200;
    }


    # Briar A7
    subnet 192.169.6.0 netmask 255.255.255.0 {
            range 192.169.6.2 192.169.6.254;
            option routers 192.169.6.1;
            option broadcast-address 192.169.6.255;
            option domain-name-servers 192.169.7.130;
            default-lease-time 600;
            max-lease-time 7200;
    }

    # Routing dari Wise ke router
    subnet 192.169.7.128 netmask 255.255.255.248 {
            option routers 192.169.7.129;
    }
    ' > /etc/dhcp/dhcpd.conf

    service isc-dhcp-server restart
    ```

Pada SSS dan Garden, install `apt-get install apache2` dan `apt-get install libapache2-mod-php7.0` kemudian lakukan `service apache2 start`.

- **SSS**
    ```
    echo 'nameserver 192.168.122.1' > /etc/resolv.conf
    
    apt-get update
    echo "" | apt-get install apache2
    echo "" | apt-get install libapache2-mod-php7.0
    service apache2 start
    
    echo 'Garden' > '/var/www/html/index.html'
    
    echo 'Listen 80
    Listen 443' > '/etc/apache2/ports.conf'
    
    service apache2 start
    ```


- **Garden**
    ```
    echo 'nameserver 192.168.122.1' > /etc/resolv.conf

    apt-get update
    echo "" | apt-get install apache2
    echo "" | apt-get install libapache2-mod-php7.0
    service apache2 start

    echo 'Garden' > '/var/www/html/index.html'

    echo 'Listen 80
    Listen 443' > '/etc/apache2/ports.conf'

    service apache2 start
    ```    

### Test

![image](https://user-images.githubusercontent.com/90445721/206849919-b8cc846c-4397-4203-9025-93b6a7fd6d06.png)

## Question 1

> Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Strix menggunakan iptables, tetapi Loid tidak ingin menggunakan MASQUERADE.

### Script

Pertama, cek IP dari Strix yang berhubungan dengan NAT dengan menggunakan command `ip a`. Karena diminta untuk tidak menggunakan `MASQUERADE`, maka digunakan SNAT. Source akan diubah dari yang awalnya 0.0 ke Strix dengan --to-source `192.168.122.80`.

Cek apakah eth0 pada setiap client sudah berada dalam range yang ada di dalam tree. Lakukan command `cat /etc/resolv.conf` pada tiap client. Kemudian lakukan `ping google.com` pada tiap client.

- **Strix**
    ```
    iptables -t nat -A POSTROUTING -s 192.169.0.0/21 -o eth0 -j SNAT --to-source 192.168.122.80
    ```

### Test

![image](https://user-images.githubusercontent.com/90445721/206849934-1293be52-6b81-4732-a710-a86d3daacf47.png)

![image](https://user-images.githubusercontent.com/90445721/206849941-8b558d38-21c0-4f05-a874-55fda2bf5dfb.png)

![image](https://user-images.githubusercontent.com/90445721/206849948-c41a7dbc-c2b5-473f-b547-bc9ed5fc75b5.png)

## Question 2

> Kalian diminta untuk melakukan drop semua TCP dan UDP dari luar Topologi kalian pada server yang merupakan DHCP Server demi menjaga keamanan.

### Script

- **Strix**
    ```
    iptables -A FORWARD -p tcp -d 192.169.7.131 -i eth0 -j DROP # Drop semua TCP
    iptables -A FORWARD -p udp -d 192.169.7.131 -i eth0 -j DROP # Drop semua UDP
    ```
Keterangan:
- `A FORWARD`: Menggunakan chain FORWARD
- `p tcp`: Mendefinisikan protokol yang digunakan, yaitu tcp
- `p udp`: Mendefinisikan protokol yang digunakan, yaitu udp
- `d 192.169.7.131`: Mendefinisikan alamat tujuan dari paket (DHCP) berada pada subnet 192.169.7.131
- `i eth0`: Paket masuk dari eth0 Strix
- `j DROP`: Paket di-drop

### Test

![image](https://user-images.githubusercontent.com/90445721/206858705-ee5c5b48-94dd-4dd3-affd-98e720cbc7f7.png)

## Question 3

> Loid meminta kalian untuk membatasi DHCP dan DNS Server hanya boleh menerima maksimal 2 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya didrop.

### Script

- **Eden**
    ```
    iptables -A INPUT -p icmp -m connlimit --connlimit-above 2 --connlimit-mask 0 -j DROP
    ```

- **Wise**
    ```
    iptables -A INPUT -p icmp -m connlimit --connlimit-above 2 --connlimit-mask 0 -j DROP
    ```
    
Keterangan:
- `A INPUT`: Menggunakan chain INPUT
- `p icmp`: Mendefinisikan protokol yang digunakan, yaitu ICMP (ping)
- `m connlimit`: Menggunakan rule connection limit
- `connlimit-above 2`: Limit yang ditangkap paket adalah di atas 2
- `connlimit-mask 0`: Hanya memperbolehkan 2 koneksi setiap subnet dalam satu waktu
- `j DROP`: Paket di-drop

### Test

![image](https://user-images.githubusercontent.com/90445721/206850009-16684bef-cace-4672-bf06-d3ebf12effe9.png)

![image](https://user-images.githubusercontent.com/90445721/206850016-45ae489d-efbf-4700-ba28-f4134b5baade.png)

## Question 4

> Akses menuju Web Server hanya diperbolehkan disaat jam kerja yaitu Senin sampai Jumat pada pukul 07.00 - 16.00.

### Script

- **Garden**
    ```
    iptables -A INPUT -m time --timestart 07:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
    iptables -A INPUT -j REJECT
    ```

- **SSS**
    ```
    iptables -A INPUT -m time --timestart 07:00 --timestop 16:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
    iptables -A INPUT -j REJECT
    ```

Keterangan:
- `A INPUT`: Menggunakan chain INPUT
- `m time`: Menggunakan rule time
- `weekdays Mon,Tue,Wed,Thu,Fri`: Melimitasi hanya untuk weekdays (Senin-Jumat)
- `timestart 07:00`: Mendefinisikan waktu mulai yaitu 07:00
- `timestop 16:00`: Mendefinisikan waktu berhenti yaitu 16:00
- `j REJECT`: Paket ditolak

### Test

![image](https://user-images.githubusercontent.com/90445721/206850056-0589cb23-c89a-4115-a1b3-3f9f42908bd3.png)

![image](https://user-images.githubusercontent.com/90445721/206850061-b22ea3ed-8a63-4309-b522-f00f5fc1be85.png)

## Question 5

> Karena kita memiliki 2 Web Server, Loid ingin Ostania diatur sehingga setiap request dari client yang mengakses Garden dengan port 80 akan didistribusikan secara bergantian pada SSS dan Garden secara berurutan dan request dari client yang mengakses SSS dengan port 443 akan didistribusikan secara bergantian pada Garden dan SSS secara berurutan.

### Script

Konfigurasi untuk masing-masing node adalah 80 dan 443 menggunakan `--dport`, serta akan dibatasi secara bergantian menggunakan `--every 2`. Oleh karena itu, distribusinya akan dilakukan secara bergantian dengan mengarahkan ke node lain menggunakan `-to-destination`.

- **Ostania**
    ```
    iptables -A PREROUTING -t nat -p tcp -d 192.169.7.138 --dport 80 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.169.7.138:80
    iptables -A PREROUTING -t nat -p tcp -d 192.169.7.138 --dport 80 -j DNAT --to-destination 192.169.7.139:80
    iptables -A PREROUTING -t nat -p tcp -d 192.169.7.139 --dport 443 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 192.169.7.139:443
    iptables -A PREROUTING -t nat -p tcp -d 192.169.7.139 --dport 443 -j DNAT --to-destination 192.169.7.138:443
    ```

### Test

![image](https://user-images.githubusercontent.com/90445721/206850083-f0df4134-3508-4fc2-bb63-68301936c84d.png)

## Question 6

> Karena Loid ingin tau paket apa saja yang di-drop, maka di setiap node server dan router ditambahkan logging paket yang di-drop dengan standard syslog level.

### Script

Lakukan command dibawah ini untuk melihat paket apa saja yang di-drop

- **Eden**
    ```
    iptables -N LOGGING
    iptables -A INPUT -j LOGGING
    iptables -A LOGGING -j LOG --log-prefix "IPTables-Dropped: " --log-level 4
    iptables -A LOGGING -j DROP
    ```

- **Wise**
    ```
    iptables -N LOGGING
    iptables -A INPUT -j LOGGING
    iptables -A LOGGING -j LOG --log-prefix "IPTables-Dropped: " --log-level 4
    iptables -A LOGGING -j DROP
    ```

### Test

![image](https://user-images.githubusercontent.com/90445721/206858681-4e5521f6-fde0-4af3-8bd4-da3e4165d3c9.png)
