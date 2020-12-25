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
			<td> Subnet </td>
			<td> Jumlah IP </td>
	    <td> Submask </td>
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
			<td> Subnet </td>
			<td> Jumlah IP </td>
			<td> Submask </td>
			<td> Network ID </td>
			<td> Netmask </td>
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
			<td> Interface </td>
			<td> IP </td>
			<td> Subnet </td>
			<td> Netmask </td>
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
