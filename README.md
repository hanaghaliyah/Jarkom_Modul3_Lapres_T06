# Jarkom_Modul3_Lapres_T06
<b> Laporan Resmi Praktikum Jaringan Komputer </b> <br>
Modul 3 - DHCP dan Proxy Server <br>
Kelompok T06
1. Hana Ghaliyah Azhar  (05311840000032)
2. Azmi                 (05311840000047)


------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Nomer 1
### Soal
Membuat topologi jaringan <br>
<img width="387" alt="Topologi" src="https://user-images.githubusercontent.com/26424136/100494290-fae0c780-3172-11eb-84e1-adb54e4486a2.PNG"> <br>
SURABAYA sebagai router, MALANG sebagai DNS Server, TUBAN sebagai DHCP server, serta MOJOKERTO sebagai Proxy server, dan UML lainnya sebagai client. <br>
### Penyelesaian
- Pertama-tama, kami akan melakukan konfigurasi terlebih dahulu pada file <b>topologi.sh</b>
<img width="709" alt="Topologi" src="https://user-images.githubusercontent.com/26424136/100542894-8e9fba00-327f-11eb-8465-f45ce6370601.PNG"> <br>
- Membuat script yang berisi `halt tiap uml` pada file <b>bye.sh</b> untuk mematikan setiap UML. <br>
![bye](https://user-images.githubusercontent.com/61286109/100133485-6ac42900-2eb9-11eb-8c18-5fefe92de51d.PNG)
- Pada router SURABAYA lakukan setting sysctl dengan mengetikkan perintah `nano /etc/sysctl.conf` Dan Hilangkan tanda pagar <b>(#)</b> pada bagian `net.ipv4.ip_forward=1` <br>
<img width="366" alt="surabaya2" src="https://user-images.githubusercontent.com/26424136/99187024-bde5ff80-2786-11eb-8ef7-2b2c3ca18dae.PNG"> <br>
Lalu ketikka `sysctl -p` untuk mengaktifkan perubahan yang ada. Dengan mengaktifkan fungsi IP Forward ini maka Linux nantinya dapat menentukan jalur mana yang dipilih untuk mencapai jaringan tujuan.
- Setting IP pada setiap UML dengan mengetikkan `nano /etc/network/interfaces` Lalu setting IPnya sebagai berikut: <br>
SURABAYA (Sebagai Router dan DHCP Relay) <br>
![sby](https://user-images.githubusercontent.com/61286109/100125231-203daf00-2eaf-11eb-86ac-2a2c03567084.PNG) <br>
MALANG  (Sebagai DNS Server) <br>
![mlg](https://user-images.githubusercontent.com/61286109/100125650-95a97f80-2eaf-11eb-8ed5-203b012ed6e8.PNG) <br>
MOJOKERTO (Sebagai Proxy Server) <br>
![mjk](https://user-images.githubusercontent.com/61286109/100126705-e2da2100-2eb0-11eb-888e-489aac0122a4.PNG) <br>
TUBAN  (Sebagai DHCP Server) <br>
![tbn](https://user-images.githubusercontent.com/61286109/100127201-77dd1a00-2eb1-11eb-943f-a9fc3b429a35.PNG) <br>
GRESIK (Sebagai Klien Subnet 1) <br>
![gsk](https://user-images.githubusercontent.com/61286109/100128366-c6d77f00-2eb2-11eb-948c-f99a86d02c47.PNG) <br>
SIDOARJO (Sebagai Klien Subnet 1) <br>
![sda](https://user-images.githubusercontent.com/61286109/100131641-e40e4c80-2eb6-11eb-8f37-60bf47db1bde.PNG) <br>
BANYUWANGI (Sebagai Klien Subnet 3) <br>
![bwi](https://user-images.githubusercontent.com/61286109/100133235-13be5400-2eb9-11eb-93fe-50c42af57252.PNG) <br>
MADIUN (Sebagai Klien Subnet 3) <br>
![mdi](https://user-images.githubusercontent.com/61286109/100133392-48321000-2eb9-11eb-8143-7b520b3d5338.PNG) <br>
- Kemudian lakukan `service networking restart` pada tiap uml.
- Jalankan `iptables` pada uml SURABAYA dengan konfigurasi berikut
```
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE -s 192.168.0.0/16
```

## Nomer 2
### Soal
SURABAYA ditunjuk sebagai perantara (DHCP Relay) antara DHCP Server dan client. 
### Penyelesaian
- Update <i>package lists</i> di router SURABAYA dengan perintah
```
apt-get update
```
- Install isc-dhcp-relay di router SURABAYA
```
apt-get install isc-dhcp-relay
```
- Buka file konfigurasi interface dengan perintah `nano /etc/default/isc-dhcp-relay`
```
SERVERS="10.151.73.180" #IP TUBAN 

INTERFACES="eth1 eth2 eth3"
```
### TESTING
<img width="366" alt="2" src="https://user-images.githubusercontent.com/26424136/100494552-6deb3d80-3175-11eb-82f7-1b050ad0368d.PNG">

## Nomer 3
### Soal
Client pada subnet 1 mendapatkan range IP dari 192.168.0.10 sampai 192.168.0.100 dan 192.168.0.110 sampai 192.168.0.200.
### Penyelesaian
- Update <i>package lists</i> di uml TUBAN dengan perintah
```
apt-get update
```
- Install isc-dhcp-server di uml TUBAN
```
apt-get install isc-dhcp-server
```
![dhcp server](https://user-images.githubusercontent.com/61286109/100180554-f87c3480-2f0a-11eb-8909-0840fc5bcbdf.PNG) <br>
- Buka file konfigurasi interface dengan perintah `nano /etc/default/isc-dhcp-server`, kemudian interface nya diganti `eth0` <br>
![3](https://user-images.githubusercontent.com/61286109/100181594-337f6780-2f0d-11eb-8c6c-5d9c21b89334.PNG) <br>
- Buka `nano /etc/dhcp/dhcpd.conf`, kemudian ubah konfigurasinya
```
range 192.168.0.10 192.168.0.100;
range 192.168.0.110 192.168.0.200;
```
![3a](https://user-images.githubusercontent.com/61286109/100183790-6f68fb80-2f12-11eb-9336-757446170d60.PNG) <br>
- Kemudian restart DHCP dengan syntax `service isc-dhcp-server restart`
### Testing
- Jalankan `ifconfig` pada setiap <b>client subnet 1</b> untuk mengetahui IP address.
- Gresik <br>
![3b](https://user-images.githubusercontent.com/61286109/100182706-d89b3f80-2f0f-11eb-9c75-4a0762500740.PNG) <br>
- Sidoarjo <br>
![3c](https://user-images.githubusercontent.com/61286109/100182812-14cea000-2f10-11eb-9356-83a6c5a3e862.PNG) <br>

## Nomer 4
### Soal
Client pada subnet 3 mendapatkan range IP dari 192.168.1.50 sampai 192.168.1.70.
### Penyelesaian
- Buka `nano /etc/dhcp/dhcpd.conf` kemudian ubah konfigurasinya
```
range 192.168.1.50 192.168.1.70;
```
![4](https://user-images.githubusercontent.com/61286109/100183850-99222280-2f12-11eb-956e-3bdae54880a9.PNG) <br>
- Kemudian restart DHCP dengan syntax `service isc-dhcp-server restart`
### Testing
- Jalankan `ifconfig` pada setiap <b>client subnet 3</b> untuk mengetahui IP address.
- Banyuwangi <br>
![4a](https://user-images.githubusercontent.com/61286109/100182950-5b23ff00-2f10-11eb-86ac-f73c74ce04f6.PNG) <br>
- Madiun <br>
![4b](https://user-images.githubusercontent.com/61286109/100183400-688db900-2f11-11eb-9d49-ff16ea16e868.PNG) <br>

## Nomer 5
### Soal
Client mendapatkan DNS Malang dan DNS 202.46.129.2 dari DHCP
### Penyelesaian
- Buka `nano /etc/dhcp/dhcpd.conf` kemudian ubah konfigurasinya
![5](https://user-images.githubusercontent.com/61286109/100184064-29f8fe00-2f13-11eb-91bc-fd670ee1b9f6.PNG) <br>
- Kemudian restart DHCP dengan syntax `service isc-dhcp-server restart`
### Testing
- Jalankan `cat /etc/resolv.conf` pada setiap <b>client</b>
- Gresik <br>
![5a](https://user-images.githubusercontent.com/61286109/100184269-b3a8cb80-2f13-11eb-8e3e-09212261af6c.PNG) <br>
- Sidoarjo <br>
![5b](https://user-images.githubusercontent.com/61286109/100184337-df2bb600-2f13-11eb-9181-2832884917b0.PNG) <br>
- Banyuwangi <br>
![5c](https://user-images.githubusercontent.com/61286109/100184436-1306db80-2f14-11eb-9859-59a802cb8f81.PNG) <br>
- Madiun <br>
![5d](https://user-images.githubusercontent.com/61286109/100184530-49445b00-2f14-11eb-87dd-71bdc372d24f.PNG) <br>

## Nomer 6
### Soal
Client di subnet 1 mendapatkan peminjaman alamat IP selama 5 menit, sedangkan client pada subnet 3 mendapatkan peminjaman IP selama 10 menit.
### Penyelesaian
- Buka `nano /etc/dhcp/dhcpd.conf` kemudian ubah konfigurasinya pada `default-lease-time` diedit dalam satuan detik.
![6](https://user-images.githubusercontent.com/61286109/100184810-e99a7f80-2f14-11eb-841c-0fbbe2747499.PNG) <br>
- Kemudian restart DHCP dengan syntax `service isc-dhcp-server restart`
### Testing
IP berubah karena telah melewati waktu peminjaman. <br>
<img width="365" alt="6a" src="https://user-images.githubusercontent.com/26424136/100494553-6fb50100-3175-11eb-9682-a1e9012906b4.PNG"> <br>
<img width="366" alt="6b" src="https://user-images.githubusercontent.com/26424136/100494555-704d9780-3175-11eb-95da-14c0f6ab979e.PNG"> <br>

## Nomer 7
### Soal
User autentikasi milik Anri memiliki format: <b>User: userta_t06 | Password: inipassw0rdta_t06</b>
### Penyelesaian
- Update <i>package lists</i> di UML MOJOKERTO dengan perintah
```
apt-get update
```
- Install squid pada UML MOJOKERTO
```
apt-get install squid
```
- Cek status squid untuk memastikan bahwa Squid telah berjalan dengan baik
```
service squid status
```
- Backup terlebih dahulu file konfigurasi default yang disediakan Squid.
```
mv /etc/squid/squid.conf /etc/squid/squid.conf.bak
```
- Lakukan `apt-get update` dan install `apache2-utils` pada UML MOJOKERTO. Ketikkan:
```
apt-get install apache2-utils
```
- Buat user dan password dengan syntax `htpasswd -c /etc/squid/passwd userta_t06` kemudian masukkan password `inipassw0rdta_t06`.
- Edit konfigurasi pada `/etc/squid/squid.conf`
```
http_port 8080
visible_hostname mojokerto

auth_param basic program /usr/lib/squid/ncsa_auth /etc/squid/passwd
auth_param basic children 5
auth_param basic realm Proxy
auth_param basic credentialsttl 2 hours
auth_param basic casesensitive on
acl USERS proxy_auth REQUIRED
http_access allow USERS
```
<img width="366" alt="7" src="https://user-images.githubusercontent.com/26424136/100494556-70e62e00-3175-11eb-8a25-7afbf3b64032.PNG"> <br>
- Lakukan `service squid restart`

### Testing
- Ubah pengaturan proxy browser.
- Akses web <b>google.com</b> dan akan muncul pop-up untuk login.
![Screenshot (258)](https://user-images.githubusercontent.com/26424136/100244877-03b27d00-2f6a-11eb-8486-9754d392f21b.png)

## Nomer 8
### Soal
Jadwal TA Selasa-Rabu pukul 13.00-18.00.
### Penyelesaian
- Buat file baru `nano /etc/squid/acl.conf`
- Tambahkan baris `acl AVAILABLE_TA time TW 13:00-18:00` <br>
<img width="369" alt="8b" src="https://user-images.githubusercontent.com/26424136/100494559-72175b00-3175-11eb-86c1-aca50fcdfadb.PNG"> <br>
- Kemudian ke file `/etc/squid/squid.conf` dan tambahkan baris berikut: <br>
<img width="367" alt="8" src="https://user-images.githubusercontent.com/26424136/100494558-717ec480-3175-11eb-8a71-05df4d4fcd3a.PNG"> <br>
- Lakukan `service squid restart`
### Testing
- Atur waktu sesuai dengan waktu akses yang tersedia/digunakan dengan perintah 
```
date --set "Tanggal Bulan Tahun Jam:Menit:Detik"
```
- Akses web pada waktu yang ditentukan, disini kami mengakses <b>its.ac.id</b>
![Screenshot (270)](https://user-images.githubusercontent.com/26424136/100542498-c9542300-327c-11eb-87c7-4df53fd860a5.png)
![Screenshot (271)](https://user-images.githubusercontent.com/26424136/100542501-cc4f1380-327c-11eb-8062-97bcc5a7745a.png)

## Nomer 9
### Soal
Setiap hari Selasa-Kamis pukul 21.00 - 09.00 keesokan harinya (sampai Jumat jam 09.00).
### Penyelesaian
- Tambahkan baris pada file `nano /etc/squid/acl.conf`
```
acl AVAILABLE_BIMBINGAN1 time TWH 21:00-24:00
acl AVAILABLE_BIMBINGAN2 time WHF 00:00-09:00
```
<img width="369" alt="9b" src="https://user-images.githubusercontent.com/26424136/100494561-73488800-3175-11eb-9a7c-61ab06e3facc.PNG"> <br>
- Kemudian ke file `/etc/squid/squid.conf` dan tambahkan baris berikut:
```
http_access allow AVAILABLE_BIMBINGAN1 USERS
http_access allow AVAILABLE_BIMBINGAN2 USERS
```
<img width="366" alt="9" src="https://user-images.githubusercontent.com/26424136/100494560-72aff180-3175-11eb-991d-699cae2057af.PNG"> <br>
- Lakukan `service squid restart`
### Testing
- Atur waktu sesuai dengan waktu akses yang tersedia/digunakan dengan perintah 
```
date --set "Tanggal Bulan Tahun Jam:Menit:Detik"
```
- Akses web pada waktu yang ditentukan, disini kami mengakses <b>elearning.if.its.ac.id</b>
![Screenshot (272)](https://user-images.githubusercontent.com/26424136/100542502-ce18d700-327c-11eb-97c9-bb5b651c5548.png)
![Screenshot (273)](https://user-images.githubusercontent.com/26424136/100542503-ceb16d80-327c-11eb-93cf-c43c09093042.png)

## Nomer 10
### Soal
Setiap dia mengakses google.com, maka akan di redirect menuju monta.if.its.ac.id
### Penyelesaian
- Buka file `nano /etc/squid/squid.conf` dan tambahkan baris berikut:
```
acl block dstdomain google.com
deny_info http://monta.if.its.ac.id block
http_reply_access deny block
```
<img width="366" alt="10" src="https://user-images.githubusercontent.com/26424136/100494562-73488800-3175-11eb-9c76-e6fb3fe59606.PNG">

### Testing
Buka private browser dengan proxy yang sudah dijalankan, lalu akses `google.com`. Situs `google` langsung otomatis redirect ke situs `monta.if.its.ac.id`. <br>
[![Watch the video](https://img.youtube.com/vi/Myq17cuu9iI/0.jpg)](http://www.youtube.com/watch?v=Myq17cuu9iI)

## Nomer 11
### Soal
Untuk menandakan bahwa Proxy Server ini adalah Proxy yang dibuat oleh Anri, Bu Meguri meminta Anri untuk mengubah error page default squid menjadi seperti gambar berikut:
### Penyelesaian
- Pindah ke `cd /usr/share/squid/errors/en` <br>
<img width="368" alt="11b" src="https://user-images.githubusercontent.com/26424136/100542089-9e68cf80-327a-11eb-99a0-c1a648254966.PNG"> <br>
- Kemudian `rm ERR_ACCESS_DENIED` <br>
- Download file <b>Error Page</b> dengan perintah `wget 10.151.36.202/ERR_ACCESS_DENIED` <br>
<img width="364" alt="11a" src="https://user-images.githubusercontent.com/26424136/100244764-e5e51800-2f69-11eb-9f68-b23922f67731.PNG"> <br>

### Testing
Akses web diluar waktu yang telah ditentukan agar muncul halaman error. <br>
![Screenshot (257)](https://user-images.githubusercontent.com/26424136/100244857-001ef600-2f6a-11eb-88fd-f901c9a6bccb.png)

## Nomer 12
### Soal
Ketika menggunakan proxy cukup dengan mengetikkan domain janganlupa-ta.yyy.pw dan memasukkan port 8080.
### Penyelesaian
- Buka MALANG dan update <i>package lists</i> dengan menjalankan command:
```
apt-get update
```
Setalah melakukan update silahkan install aplikasi bind9 pada MALANG dengan perintah:
```
apt-get install bind9 -y
```
![bind9](https://user-images.githubusercontent.com/61286109/100180643-28c3d300-2f0b-11eb-94f3-fb1c93d63c1c.PNG) <br>
<br>
<b>Membuat Domain pada DNS Server </b>
- Lakukan perintah pada MALANG. Isikan seperti berikut:
```
nano /etc/bind/named.conf.local
```
- Isikan configurasi domain janganlupa-ta.t06.pw sesuai dengan syntax berikut:
```
zone "janganlupa-ta.t06.pw" {
	type master;
	file "/etc/bind/t06/janganlupa-ta.t06.pw";
};
```
- Buat folder <b>t06</b> di dalam /etc/bind
```
mkdir /etc/bind/t06
```
- Copykan file db.local pada path /etc/bind ke dalam folder <b>t06</b> yang baru saja dibuat dan ubah namanya menjadi janganlupa-ta.t06.pw
```
cp /etc/bind/db.local /etc/bind/t06/janganlupa-ta.t06.pw
```
- Kemudian buka file janganlupa-ta.t06.pw dan edit seperti gambar berikut dengan IP MOJOKERTO
```
nano /etc/bind/t06/janganlupa-ta.t06.pw
```
![12](https://user-images.githubusercontent.com/61286109/100479308-62215c00-3120-11eb-9a20-ecafe2b085cc.PNG) <br>
- Edit file <b>/etc/bind/named.conf.local</b> pada MALANG 
```
nano /etc/bind/named.conf.local
```
- Isikan configurasi domain janganlupa-ta.t06.pw sesuai dengan syntax berikut:
```
zone "73.151.10.in-addr.arpa" {
    type master;
    file "/etc/bind/t06/73.151.10.in-addr.arpa";
};
```
![12a](https://user-images.githubusercontent.com/61286109/100479558-23d86c80-3121-11eb-9b15-be38f8481935.PNG) <br>
- Copykan file db.local pada path /etc/bind ke dalam folder <b>t06</b> yang baru saja dibuat dan ubah namanya menjadi 73.151.10.in-addr.arpa
```
cp /etc/bind/db.local /etc/bind/t06/73.151.10.in-addr.arpa
```
- Buka file 73.151.10.in-addr.arpa dan edit menjadi seperti gambar di bawah ini
<img width="397" alt="12b" src="https://user-images.githubusercontent.com/26424136/100542009-2f8b7680-327a-11eb-858f-ae4e21e302e9.PNG"> <br>
- Restart bind9 dengan perintah
```
service bind9 restart
```
### Testing
- Ubah pengaturan proxy browser. Gunakan `janganlupa-ta.t06.pw` sebagai host, dan isikan port 8080. <br>
<img width="543" alt="12" src="https://user-images.githubusercontent.com/26424136/100542506-d4a74e80-327c-11eb-9c5d-283312c69116.PNG"> <br>
- Kemudian akses web <br>
![Screenshot (258)](https://user-images.githubusercontent.com/26424136/100244877-03b27d00-2f6a-11eb-8486-9754d392f21b.png)
