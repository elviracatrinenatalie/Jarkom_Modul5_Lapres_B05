# Jarkom_Modul5_Lapres_B05

- Elvira Catrine Natalie 05111840000016
- Vania Meilani Taqiyyah 05111840000045

## A dan B
- Melakukan pembagian subnet terlebih dahulu. Disini kelompok kami menggunakan metode **VLSM (Variable Length Subnet Masking)**.
<img src="https://user-images.githubusercontent.com/61219556/103123551-51302000-46b7-11eb-96e0-b7cf9f43c9b5.jpg" width="500" height="auto">

Keterangan	:
1. **SURABAYA** diberikan **IP TUNTAP**
2. **MALANG** merupakan **DNS Server** diberikan **IP DMZ**
3. **MOJOKERTO** merupakan **DHCP Server** diberikan **IP DMZ**
4. **MADIUN** dan **PROBOLINGGO** merupakan **WEB Server**
5. **Setiap Server** diberikan memory sebesar **128M**
6. **Client** dan **Router** diberikan memori sebesar **96M**
7. Jumlah host pada subnet **SIDOARJO 200 Host**
8. Jumlah host pada subnet **GRESIK 210 Host**

- Menentukan jumlah alamat IP yang dibutuhkan oleh tiap subnet dan lakukan labelling netmask berdasarkan jumlah IP yang dibutuhkan :
	<!DOCTYPE html>
	<html>
	<head>
		<meta charset="utf-8">
	</head>
	<body>

	 <table>
		<tr>
			<td> SUBNET </td>
			<td> JUMLAH IP </td>
	    		<td> SUBMASK </td>
		</tr>
		<tr>
			<td> A1 </td>
			<td> 201 </td>
	    <td> /24 </td>
		</tr>
	  <tr>
			<td> A2 </td>
			<td> 2 </td>
	    <td> /30 </td>
		</tr>
	  <tr>
			<td> A3 </td>
			<td> 2 </td>
	    <td> /30 </td>
		</tr><tr>
			<td> A4 </td>
			<td> 211 </td>
	    <td> /24 </td>
		</tr>
	  <tr>
			<td> A5 </td>
			<td> 3 </td>
	    <td> /30 </td>
		</tr>
	  <tr>
			<td> Total </td>
			<td> 419 </td>
	    <td> /22 </td>
		</tr>
	 </table>

	</body>
	</html>

- Membuat pohon dari VLSM serta subnetting.
<img src="https://user-images.githubusercontent.com/61219556/103123987-b6d0dc00-46b8-11eb-9433-eda56166f8eb.png" width="500" height="auto">

**SUBNET**
	<!DOCTYPE html>
	<html>
	<head>
		<meta charset="utf-8">
	</head>
	<body>
	 <table>
		<tr>
			<td> SUBNET </td>
			<td> JUMLAH IP </td>
			<td> SUBMASK </td>
			<td> NETWORK ID </td>
			<td> NETMASK </td>
		</tr>
		<tr>
			<td> A1 </td>
			<td> 201 </td>
			<td> /24 </td>
			<td> 192.168.1.0 </td>
			<td> 255.255.255.0 </td>
		</tr>
		 <tr>
			<td> A2 </td>
			<td> 2 </td>
			<td> /30 </td>
			<td> 192.168.0.0 </td>
			<td> 255.255.255.252 </td>
		</tr>
		 <tr>
			<td> A3 </td>
			<td> 2 </td>
			<td> /30 </td>
			<td> 192.168.0.4 </td>
			<td> 255.255.255.252 </td>
		</tr>
		 <tr>
			<td> A4 </td>
			<td> 211 </td>
			<td> /24 </td>
			<td> 192.168.2.0 </td>
			<td> 255.255.255.0 </td>
		</tr>
		 <tr>
			<td> A5 </td>
			<td> 3 </td>
			<td> /30 </td>
			<td> 192.168.0.8 </td>
			<td> 255.255.255.252 </td>
		</tr>
		 <tr>
			<td> Total </td>
			<td> 419 </td>
			<td> /22 </td>
			<td>  </td>
			<td>  </td>
		</tr>
	 </table>
	</body>
	</html>
	
**SUBNET SERVER**
	<!DOCTYPE html>
	<html>
	<head>
		<meta charset="utf-8">
	</head>
	<body>
	 <table>
		<tr>
			<td> INTERFACE </td>
			<td> IP </td>
			<td> SUBNET </td>
			<td> NETMASK </td>
		</tr>
		<tr>
			<td> Malang (DNS Server) </td>
			<td> 10.151.83.50 </td>
			<td> /29 </td>
			<td> 255.255.255.248 </td>
		</tr>
		<tr>
			<td> Mojokerto (DHCP Server) </td>
			<td> 10.151.83.51 </td>
			<td> /29 </td>
			<td> 255.255.255.248 </td>
		</tr>
	 </table>
	</body>
	</html>

- Karena setiap antar router dan antara router dengan klien dihubungkan dengan Switch, maka didapatkan gambar topologi sebagai berikut :
<img src="https://user-images.githubusercontent.com/61219556/103128569-76795a00-46c8-11eb-86c2-d56c78b0d4f8.JPG" width="500" height="auto">

- Sehingga, di dapatkan konfigurasi `topologi.sh`
```
# Switch
uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch2 > /dev/null < /dev/null &
uml_switch -unix switch3 > /dev/null < /dev/null &
uml_switch -unix switch4 > /dev/null < /dev/null &
uml_switch -unix switch5 > /dev/null < /dev/null &
uml_switch -unix switch6 > /dev/null < /dev/null &

# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,10.151.74.25 eth1=daemon,,,switch3 eth2=daemon,,,switch4 mem=96M &
xterm -T KEDIRI -e linux ubd0=KEDIRI,jarkom umid=KEDIRI eth0=daemon,,,switch3 eth1=daemon,,,switch1 eth2=daemon,,,switch5 mem=96M &
xterm -T BATU -e linux ubd0=BATU,jarkom umid=BATU eth0=daemon,,,switch4 eth1=daemon,,,switch2 eth2=daemon,,,switch6 mem=96M &

#Server
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch1 mem=128M &
xterm -T PROBOLINGGO -e linux ubd0=PROBOLINGGO,jarkom umid=PROBOLINGGO eth0=daemon,,,switch1 mem=128M &
xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch2 mem=128M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch2 mem=128M &

# Klien
xterm -T GRESIK -e linux ubd0=GRESIK,jarkom umid=GRESIK eth0=daemon,,,switch5 mem=96M &
xterm -T SIDORJO -e linux ubd0=SIDORJO,jarkom umid=SIDORJO eth0=daemon,,,switch6 mem=96M &
```
- Pada UML yang berperan sebagai router, melakukan uncomment pada perintah `net.ipv4.ip_forward=1` agar dapat meneruskan route yaitu dengan cara mengetikkan `nano /etc/sysctl.conf`. Lalu, ketik `sysctl -p`, untuk mengaktifkan perubahan baru. Kemudian, atur interface pada setiap UML dengan menjalankan perintah `nano /etc/network/interfaces` kemudian melakukan `restart networking restart`.

- Berikut setting file `/etc/network/interfaces` untuk setiap UML:

**SURABAYA (sebagai Router)** 
```
auto eth0
iface eth0 inet static
address 10.151.74.26
netmask 255.255.255.252
gateway 10.151.74.25

auto eth1
iface eth1 inet static
address 192.168.0.5
netmask 255.255.255.252

auto eth2
iface eth2 inet static
address 192.168.0.1
netmask 255.255.255.252
```

**KEDIRI (sebagai Router)** 
```
auto eth0
iface eth0 inet static
address 192.168.0.6
netmask 255.255.255.252
gateway 192.168.0.5

auto eth1
iface eth1 inet static
address 192.168.0.9
netmask 255.255.255.248

auto eth2
iface eth2 inet static
address 192.168.2.1
netmask 255.255.255.0
```

**MADIUN (sebagai web server)**
```
auto eth0
iface eth0 inet static
address 192.168.0.10
netmask 255.255.255.248
gateway 192.168.0.9
```

**PROBOLINGGO (sebagai web server)** 
```
auto eth0
iface eth0 inet static
address 192.168.0.11
netmask 255.255.255.248
gateway 192.168.0.9
```

**GRESIK (sebagai Client)**
```
auto eth0
iface eth0 inet static
address 192.168.2.2
netmask 255.255.252.0
gateway 192.168.2.1
```

**BATU (sebagai Router)**
```
auto eth0	
iface eth0 inet static
address 192.168.0.2
netmask 255.255.255.252
gateway 192.168.0.1

auto eth1	
iface eth1 inet static
address 10.151.83.49
netmask 255.255.255.248

auto eth2	
iface eth2 inet static
address 192.168.1.1
netmask 255.255.255.0
```

**MALANG (sebagai DNS Server)**
```
auto eth0
iface eth0 inet static
address 10.151.83.50
netmask 255.255.255.248
gateway 10.151.83.49
```

**MOJOKERTO (sebagai DHCP Server)**
```
auto eth0
iface eth0 inet static
address 10.151.83.51
netmask 255.255.255.248
gateway 10.151.83.49
```

**SIDORJO (sebagai Client)**
```
auto eth0
iface eth0 inet static
address 192.168.1.2
netmask 255.255.255.0
gateway 192.168.1.1
```
- Jalankan perintah `iptables –t nat –A POSTROUTING –o eth0 –j MASQUERADE –s 192.168.0.0/16` untuk koneksi ke jaringan luar pada semua router yang ada. 

## C. ROUTING
- Melakukan Routing dengan konfigurasi sebagai berikut :

**SURABAYA**
```
route add -net 192.168.1.0 netmask 255.255.255.0 gw 192.168.0.2
route add -net 192.168.2.0 netmask 255.255.255.0 gw 192.168.0.6
route add -net 10.151.83.48 netmask 255.255.255.248 gw 192.168.0.2
route add -net 192.168.0.8 netmask 255.255.255.248 gw 192.168.0.6
```

**KEDIRI**
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.0.5
```

**BATU**
```
route add -net 0.0.0.0 netmask 0.0.0.0 gw 192.168.0.1
```
- Jalankan `route.sh`.

## D. DHCP SERVER & RELAY
- Selanjutnya mengatur DHCP Server dan DHCP Relay. Karena **MOJOKERTO** menjadi **DHCP Server**, perlu diinstallkan dengan perintah `apt-get install isc-dhcp-server`, sedangkan **KEDIRI**, **SURABAYA**, dan **BATU** yang akan menjadi **DHCP Relay**, perlu diinstallkan dengan perintah `apt-get install isc-dhcp-relay`. 

#### Konfigurasi DHCP Server
- Buka file `/etc/default/isc-dhcp-server`.
- Tambahkan interface menjadi `INTERFACE="eth0"`.
- Buka file `/etc/dhcp/dhcpd.conf`
- Tambahkan script seperti dibawah ini :
```
subnet 10.151.83.48 netmask 255.255.255.248 {
	option routers 10.151.83.49;
	option broadcast-address 10.151.83.55;
}

#SIDOARJO
subnet 192.168.1.0 netmask 255.255.255.0 {
	range 192.168.1.2 192.168.1.254;
	option routers 192.168.1.1;
	option broadcast-address 192.168.1.255;
	option domain-name-servers 10.151.83.50;
	option domain-name-servers 202.46.129.2;
	default-lease-time 600;
	max-lease-time 7200;
}

#GRESIK
subnet 192.168.2.0 netmask 255.255.255.0 {
	range 192.168.2.2 192.168.2.254;
	option routers 192.168.2.1;
	option broadcast-address 192.168.2.255;
	option domain-name-servers 10.151.83.50;
	option domain-name-servers 202.46.129.2;
	default-lease-time 600;
	max-lease-time 7200;}
```
- Restart menggunakan `service isc-dhcp-server restart`.

#### Konfigurasi DHCP Relay
- Buka file `/etc/default/isc-dhcp-relay`.
- Lalu, edit file seperti dibawah ini :
```
SERVERS="10.151.83.51" #IP MOJOKERTO
```
- Untuk **KEDIRI** dan **BATU** ganti Interfaces dengan `INTERFACES="eth0 eth1 eth2"`.
- Untuk **SURABAYA** ganti Interfaces dengan `INTERFACES="eth1 eth2"`.
- Restart menggunakan `service isc-dhcp-relay restart`.

#### Konfigurasi DHCP Client
- Lalu, karena disuruh ip dinamis, maka edit file `/etc/network/interfaces` pada **GRESIK** dan **SIDOARJO** :
```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet dhcp
```
contoh : Client GRESIK

<img src="https://user-images.githubusercontent.com/61219556/103269221-f31d7880-49e7-11eb-8c46-4898620ae51c.JPG" width="500" height="auto">

- Restart menggunakan `service networking restart`.

## 1.Router SURABAYA bisa mengakses keluar tanpa menggunakan MASQUERADE.
- Pada Router **SURABAYA**, kami membuat file `nano soal1.sh`.
- Lalu, isi file dengan :
```
iptables -t nat -A POSTROUTING -o eth0 -j SNAT -s 192.168.0.0/16 --to-source 10.151.74.26
```
Keterangan :<br>
`--to-source 10.151.74.26` : source ip address akan diubah dengan ip eth0 **SURABAYA**.

- Lakukan `bash soal1.sh`.
- Untuk memeriksanya, kami melakukan `ping google.com` pada semua UML. Salah satu contohnya yaitu :

<img src="https://user-images.githubusercontent.com/61219556/103273622-57453a00-49f2-11eb-89ad-547beb7d6afa.JPG" width="500" height="auto">

## 2. DROP semua akses SSH dari luar topologi (UML) pada server yang memiliki IP DMZ dan konfigurasi di router SURABAYA
- Pada router **SURABAYA**, kami membuat file `nano soal2.sh`.
- Lalu, isi file dengan  :
```
iptables -A FORWARD -i eth0 -d 10.151.83.48/29 -p tcp --dport 22 -j DROP
```
keterangan :<br>
`-p tcp` 	: karena menggunakan SSH <br>
`--dport 22` 	: port SSH

- Lakukan `bash soal2.sh`.
- Untuk memeriksanya, di **MALANG** ketikan `nc -l -p 22`. Dan pada client (disini kami menggunakan client **SIDOARJO**) ketikan `nc 10.151.83.50 22`.
- Ketika kata apa saja pada client, apabila kata tersebut masuk pada server **MALANG** maka konfigurasi tersebut berhasil.

<img src="https://user-images.githubusercontent.com/61219556/103282942-d5610b00-4a09-11eb-8c70-8a8364803783.JPG" width="500" height="auto">

## 3. Membatasi DHCP dan DNS server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan yang berasal dari mana saja menggunakan iptables pada masing masing server, selebihnya akan di DROP.
- Pada server **MALANG** dan **MOJOKERTO**, kami membuat file `nano soal3.sh`.
- Lalu, isi dengan :
```
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```
keterangan : <br>
`-p icmp`		: menggunakan koneksi icmp <br>
`--connlimit-mask 0`	: menandakan koneksi untuk semua sumber (berasal dari mana saja).

- lakukan `bash soal3.sh`.
- Untuk memeriksanya, maka bisa melakukan `ping <IP MALANG>` atau `ping <IP MOJOKERO>` di 4 UML yang berbeda secara bersamaan. Maka akan ada 1 UML yang tidak bisa akes karena telah ada 3 koneksi yang masuk secara bersamaan. 

## 4. Akses dari subnet SIDOARJO hanya diperbolehkan pada pukul 07.00 - 17.00 pada hari Senin sampai Jumat dengan konfigurasi pada MALANG. Selain itu paket akan di REJECT.
- Pada **MALANG**, kami membuat file `nano soal4.sh`.
- Lalu, isi file dengan :
```
iptables -A INPUT -s 192.168.1.0/24 -m time --timestart 07:00 --timestop 17:00 --weekdays Mon,Tue,Wed,Thu,Fri -j ACCEPT
iptables -A INPUT -s 192.168.1.0/24 -j REJECT
```
- Lakukan `bash soal4.sh`.
- Untuk memeriksanya, pada **SIDOARJO** lakukan `ping 10.151.83.50`. Apabila pada UML, waktu nya masuk antara 07:00 - 17:00 , maka ping tersebut akan berhasil, begitu juga sebaliknya. 

## 5. Akses dari subnet GRESIK pukul 17.00 hingga pukul 07.00 setiap harinya dengan konfigurasi pada MALANG. Selain itu paket akan di REJECT.
- Pada **MALANG**, kami membuat file `nano soal5.sh`.
- Lalu, isi file dengan :
```
iptables -A INPUT -s 192.168.2.2/24 -m time --timestart 07:00 --timestop 17:00 -j REJECT 
```
- Lakukan `bash soal5.sh`.
- Untuk memeriksanya, pada **GRESIK** lakukan `ping 10.151.83.50`. Apabila pada UML, waktu nya masuk antara 17:00 - 07:00 esok hari , maka ping tersebut akan berhasil, begitu juga sebaliknya.

[ 6 DAN 7 UP ]
