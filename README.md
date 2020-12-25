# Jarkom_Modul5_Lapres_B05

- Elvira Catrine Natalie 05111840000016
- Vania Meilani Taqiyyah 05111840000045

## 1.
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

** SURABAYA **
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

**KEDIRI**
``
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
``

**MADIUN**
``
auto eth0
iface eth0 inet static
address 192.168.0.10
netmask 255.255.255.248
gateway 192.168.0.9
``

**PROBOLINGGO** 
```
auto eth0
iface eth0 inet static
address 192.168.0.11
netmask 255.255.255.248
gateway 192.168.0.9
```

**GRESIK**
```
auto eth0
iface eth0 inet static
address 192.168.2.2
netmask 255.255.252.0
gateway 192.168.2.1
```

**BATU**
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

**MALANG**
```
auto eth0
iface eth0 inet static
address 10.151.83.50
netmask 255.255.255.248
gateway 10.151.83.49
```

**MOJOKERTO**
```
auto eth0
iface eth0 inet static
address 10.151.83.51
netmask 255.255.255.248
gateway 10.151.83.49
```

**SIDORJO**
```
auto eth0
iface eth0 inet static
address 192.168.1.2
netmask 255.255.255.0
```
gateway 192.168.1.1
