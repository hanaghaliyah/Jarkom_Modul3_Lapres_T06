# Jarkom_Modul3_Lapres_T06
<b> Laporan Resmi Praktikum Jaringan Komputer </b> <br>
Modul 2 - DHCP dan Proxy Server <br>
Kelompok T06
1. Hana Ghaliyah Azhar  (05311840000032)
2. Azmi                 (05311840000047)


------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Persiapan
- Pertama-tama, kami akan melakukan konfigurasi terlebih dahulu pada file <b>topologi.sh</b>
<br>
- Pada router SURABAYA lakukan setting sysctl dengan mengetikkan perintah `nano /etc/sysctl.conf` Dan Hilangkan tanda pagar <b>(#)</b> pada bagian `net.ipv4.ip_forward=1` <br>
<img width="366" alt="surabaya2" src="https://user-images.githubusercontent.com/26424136/99187024-bde5ff80-2786-11eb-8ef7-2b2c3ca18dae.PNG"> <br>
Lalu ketikka sysctl -p untuk mengaktifkan perubahan yang ada. Dengan mengaktifkan fungsi IP Forward ini maka Linux nantinya dapat menentukan jalur mana yang dipilih untuk mencapai jaringan tujuan.
- Setting IP pada setiap UML dengan mengetikkan `nano /etc/network/interfaces` Lalu setting IPnya sebagai berikut:
SURABAYA (Sebagai Router)
<img width="367" alt="surabaya" src="https://user-images.githubusercontent.com/26424136/99187023-bde5ff80-2786-11eb-9782-116a08d8ea0e.PNG">
MALANG  (Sebagai DNS Master Server)
<img width="368" alt="malang" src="https://user-images.githubusercontent.com/26424136/99187017-baeb0f00-2786-11eb-966d-3281c37b1553.PNG">
MOJOKERTO (Sebagai DNS Slave Server)
<img width="367" alt="mojokerto" src="https://user-images.githubusercontent.com/26424136/99187018-baeb0f00-2786-11eb-825c-f110054fa002.PNG">
PROBOLINGGO  (Sebagai Web Server)
<img width="366" alt="probolinggo" src="https://user-images.githubusercontent.com/26424136/99187021-bcb4d280-2786-11eb-988b-dd3dee8a965b.PNG">
GRESIK (Sebagai Klien Subnet 1)
<img width="366" alt="gresik" src="https://user-images.githubusercontent.com/26424136/99187016-ba527880-2786-11eb-9151-ba59475cbad2.PNG"> 
SIDOARJO (Sebagai Klien Subnet 1)
<img width="365" alt="sidoarjo" src="https://user-images.githubusercontent.com/26424136/99187022-bd4d6900-2786-11eb-8c69-a2611458bf60.PNG"> 
- Terakhir, membuat script yang berisi `halt tiap uml` pada file <b>bye.sh</b> untuk mematikan setiap UML. Script file bernama bye.sh dapat dilihat melalui gambar dibawah ini:
<img width="499" alt="bye sh" src="https://user-images.githubusercontent.com/26424136/99186444-ee2b9f00-2782-11eb-93b7-16e69aaf9619.PNG">

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
