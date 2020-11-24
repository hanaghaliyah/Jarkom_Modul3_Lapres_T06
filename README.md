# Jarkom_Modul3_Lapres_T06
<b> Laporan Resmi Praktikum Jaringan Komputer </b> <br>
Modul 2 - DHCP dan Proxy Server <br>
Kelompok T06
1. Hana Ghaliyah Azhar  (05311840000032)
2. Azmi                 (05311840000047)


------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Persiapan
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
- Terakhir, membuat script yang berisi `halt tiap uml` pada file <b>bye.sh</b> untuk mematikan setiap UML. Script file bernama bye.sh dapat dilihat melalui gambar dibawah ini: <br>
![bye](https://user-images.githubusercontent.com/61286109/100133485-6ac42900-2eb9-11eb-8c18-5fefe92de51d.PNG)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Nomer 1
### Soal
Membuat topologi jaringan
### Penyelesaian

## Nomer 2
### Soal
Surabaya mennjadi DHCP Relay
### Penyelesaian

## Nomer 3
### Soal
Client pada subnet 1 mendapatkan range IP dari 192.168.0.10 sampai 192.168.0.100 dan 192.168.0.110 sampai 192.168.0.200.
### Penyelesaian

## Nomer 4
### Soal
Client pada subnet 3 mendapatkan range IP dari 192.168.1.50 sampai 192.168.1.70.
### Penyelesaian

## Nomer 5
### Soal
Client mendapatkan DNS Malang dan DNS 202.46.129.2 dari DHCP
### Penyelesaian

## Nomer 6
### Soal
Client di subnet 1 mendapatkan peminjaman alamat IP selama 5 menit, sedangkan (6) client pada subnet 3 mendapatkan peminjaman IP selama 10 menit.
### Penyelesaian

## Nomer 7
### Soal
User autentikasi milik Anri memiliki format: <b>User: userta_t06 | Password: inipasw0rdta_t06</b>
### Penyelesaian

## Nomer 8
### Soal
Jadwal TA Selasa-Rabu pukul 13.00-18.00.
### Penyelesaian

## Nomer 1
### Soal
Membuat topologi jaringan
### Penyelesaian
