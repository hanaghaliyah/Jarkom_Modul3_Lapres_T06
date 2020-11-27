# Jarkom_Modul3_Lapres_T06
<b> Laporan Resmi Praktikum Jaringan Komputer </b> <br>
Modul 2 - DHCP dan Proxy Server <br>
Kelompok T06
1. Hana Ghaliyah Azhar  (05311840000032)
2. Azmi                 (05311840000047)


------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Nomer 1
### Soal
Membuat topologi jaringan
### Penyelesaian
- Pertama-tama, kami akan melakukan konfigurasi terlebih dahulu pada file <b>topologi.sh</b>
![Topologi](https://user-images.githubusercontent.com/61286109/100124518-57f82700-2eae-11eb-817f-011103f5aacb.PNG) <br>
- Pada router SURABAYA lakukan setting sysctl dengan mengetikkan perintah `nano /etc/sysctl.conf` Dan Hilangkan tanda pagar <b>(#)</b> pada bagian `net.ipv4.ip_forward=1` <br>
<img width="366" alt="surabaya2" src="https://user-images.githubusercontent.com/26424136/99187024-bde5ff80-2786-11eb-8ef7-2b2c3ca18dae.PNG"> <br>
Lalu ketikka sysctl -p untuk mengaktifkan perubahan yang ada. Dengan mengaktifkan fungsi IP Forward ini maka Linux nantinya dapat menentukan jalur mana yang dipilih untuk mencapai jaringan tujuan.
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
Banyuawangi (Sebagai Klien Subnet 3) <br>
![bwi](https://user-images.githubusercontent.com/61286109/100133235-13be5400-2eb9-11eb-93fe-50c42af57252.PNG) <br>
Madiun (Sebagai Klien Subnet 3) <br>
![mdi](https://user-images.githubusercontent.com/61286109/100133392-48321000-2eb9-11eb-8143-7b520b3d5338.PNG) <br>
- Membuat script yang berisi `halt tiap uml` pada file <b>bye.sh</b> untuk mematikan setiap UML. Script file bernama bye.sh dapat dilihat melalui gambar dibawah ini: <br>
![bye](https://user-images.githubusercontent.com/61286109/100133485-6ac42900-2eb9-11eb-8c18-5fefe92de51d.PNG) <br>
- Install DHCP Relay di Surabaya <br>
- Install DHCP Server di Tuban <br>
![dhcp server](https://user-images.githubusercontent.com/61286109/100180554-f87c3480-2f0a-11eb-8909-0840fc5bcbdf.PNG) <br>
- Install Bind9 di Malang <br>
![bind9](https://user-images.githubusercontent.com/61286109/100180643-28c3d300-2f0b-11eb-94f3-fb1c93d63c1c.PNG) <br>
- Install Squid3 di Mojokerto <br>
![squid3](https://user-images.githubusercontent.com/61286109/100180916-c6b79d80-2f0b-11eb-9558-d2564bbb913f.PNG) <br>

## Nomer 2
### Soal
Surabaya menjadi DHCP Relay
### Penyelesaian

## Nomer 3
### Soal
Client pada subnet 1 mendapatkan range IP dari 192.168.0.10 sampai 192.168.0.100 dan 192.168.0.110 sampai 192.168.0.200.
### Penyelesaian
- Buka `nano /etc/default/isc-dhcp-server` kemudian interface nya diganti `eth0` <br>
![3](https://user-images.githubusercontent.com/61286109/100181594-337f6780-2f0d-11eb-8c6c-5d9c21b89334.PNG) <br>
- Buka `nano /etc/dhcp/dhcpd.conf` kemudian ubah konfigurasinya
![3a](https://user-images.githubusercontent.com/61286109/100183790-6f68fb80-2f12-11eb-9336-757446170d60.PNG) <br>
- Kemudian restart DHCP dengan syntax `service isc-dhcp-server restart`
### Testing
- Jalankan `ifconfig` pada setiap <b>client subnet 1</b>
- Gresik <br>
![3b](https://user-images.githubusercontent.com/61286109/100182706-d89b3f80-2f0f-11eb-9c75-4a0762500740.PNG) <br>
- Sidoarjo <br>
![3c](https://user-images.githubusercontent.com/61286109/100182812-14cea000-2f10-11eb-9356-83a6c5a3e862.PNG) <br>

## Nomer 4
### Soal
Client pada subnet 3 mendapatkan range IP dari 192.168.1.50 sampai 192.168.1.70.
### Penyelesaian
- Buka `nano /etc/dhcp/dhcpd.conf` kemudian ubah konfigurasinya
![4](https://user-images.githubusercontent.com/61286109/100183850-99222280-2f12-11eb-956e-3bdae54880a9.PNG) <br>
- Kemudian restart DHCP dengan syntax `service isc-dhcp-server restart`
### Testing
- Jalankan `ifconfig` pada setiap <b>client subnet 3</b>
- Banyuawangi <br>
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
- Banyuawangi <br>
![5c](https://user-images.githubusercontent.com/61286109/100184436-1306db80-2f14-11eb-9859-59a802cb8f81.PNG) <br>
- Madiun <br>
![5d](https://user-images.githubusercontent.com/61286109/100184530-49445b00-2f14-11eb-87dd-71bdc372d24f.PNG) <br>

## Nomer 6
### Soal
Client di subnet 1 mendapatkan peminjaman alamat IP selama 5 menit, sedangkan client pada subnet 3 mendapatkan peminjaman IP selama 10 menit.
### Penyelesaian
- Buka `nano /etc/dhcp/dhcpd.conf` kemudian ubah konfigurasinya
![6](https://user-images.githubusercontent.com/61286109/100184810-e99a7f80-2f14-11eb-841c-0fbbe2747499.PNG) <br>
- Kemudian restart DHCP dengan syntax `service isc-dhcp-server restart`

## Nomer 7
### Soal
User autentikasi milik Anri memiliki format: <b>User: userta_t06 | Password: inipassw0rdta_t06</b>
### Penyelesaian
- Lakukan `apt-get update` dan install `apache2-utils` pada UML MOJOKERTO.
- Buat user dan password dengan syntax `htpasswd -c /etc/squid/passwd userta_t06` kemudian masukkan password yang diinginkan.
- Edit konfigurasi pada `/etc/squid3/squid.conf`
```
http_port 8080
visible_hostname mojokerto

auth_param basic program /usr/lib/squid/basic_ncsa_auth /etc/squid/passwd
auth_param basic children 5
auth_param basic realm Proxy
auth_param basic credentialsttl 2 hours
auth_param basic casesensitive on
acl USERS proxy_auth REQUIRED
http_access allow USERS
```
- Lakukan `service squid3 restart`
- Ubah pengaturan proxy browser. Gunakan <b>IP MOJOKERTO</b> sebagai host, dan isikan <b>port 8080</b>.
- Mengatur waktu dengan perintah `date --set "Tanggal Bulan Tahun Jam:Menit:Detik"`
### Testing
![Screenshot (258)](https://user-images.githubusercontent.com/26424136/100244877-03b27d00-2f6a-11eb-8486-9754d392f21b.png)

## Nomer 8
### Soal
Jadwal TA Selasa-Rabu pukul 13.00-18.00.
### Penyelesaian
- Buat file baru `nano /etc/squid3/acl.conf`
- Tambahkan baris `acl AVAILABLE_WORKING time TW 13:00-18:00` <br>
![8](https://user-images.githubusercontent.com/61286109/100478394-a101e280-311d-11eb-90c0-7a90b83efa3e.PNG) <br>
- Kemudian ke file `/etc/squid3/squid.conf` dan tambahkan baris berikut: <br>
![8b](https://user-images.githubusercontent.com/61286109/100478765-c80ce400-311e-11eb-9327-66993b28d742.PNG) <br>
- Lakukan `service squid3 restart`

## Nomer 9
### Soal
Setiap hari Selasa-Kamis pukul 21.00 - 09.00 keesokan harinya (sampai Jumat jam 09.00).
### Penyelesaian
- Tambahkan baris pada file `nano /etc/squid3/acl.conf`
```
acl AVAILABLE_WORKING2 time TWH 21:00-24:00
acl AVAILABLE_WORKING3 time WHF 00:00-09:00
```
![9](https://user-images.githubusercontent.com/61286109/100478787-de1aa480-311e-11eb-8887-0ee7b88a7ad1.PNG) <br>
- Kemudian ke file `/etc/squid3/squid.conf` dan tambahkan baris berikut:
```
http_access allow AVAILABLE_WORKING2 USERS
http_access allow AVAILABLE_WORKING2 USERS
```
![9a](https://user-images.githubusercontent.com/61286109/100478891-33ef4c80-311f-11eb-9f77-f0f7af85be2e.PNG) <br>
- Lakukan `service squid3 restart`

## Nomer 10
### Soal
Setiap dia mengakses google.com, maka akan di redirect menuju monta.if.its.ac.id
### Penyelesaian
BELUM

## Nomer 11
### Soal
Untuk menandakan bahwa Proxy Server ini adalah Proxy yang dibuat oleh Anri, Bu Meguri meminta Anri untuk mengubah error page default squid menjadi seperti gambar berikut:
### Penyelesaian
<img width="364" alt="11a" src="https://user-images.githubusercontent.com/26424136/100244764-e5e51800-2f69-11eb-9f68-b23922f67731.PNG"> <br>
<img width="366" alt="11b" src="https://user-images.githubusercontent.com/26424136/100244780-e8477200-2f69-11eb-84f8-d01a22114306.PNG"> <br>
### Testing
![Screenshot (257)](https://user-images.githubusercontent.com/26424136/100244857-001ef600-2f6a-11eb-88fd-f901c9a6bccb.png)

## Nomer 12
### Soal
Ketika menggunakan proxy cukup dengan mengetikkan domain janganlupa-ta.yyy.pw dan memasukkan port 8080.
### Penyelesaian
Membuat Domain pada DNS Server
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
- Restart bind9 dengan perintah
```
service bind9 restart
```
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------
