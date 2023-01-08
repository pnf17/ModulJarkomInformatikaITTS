# **ROUTING**

Berikut sub-bab yang akan kita pelajari pada materi routing :
1. [Pengertian](#pengertian)
2. [Istilah](#istilah)
3. [Praktik](#praktik)

## Pengertian

Routing adalah proses meneruskan paket-paket data dari satu jaringan ke jaringan yang lainnya. Proses ini dapat diartikan juga sebagai penggabungan beberapa jaringan untuk meneruskan paket data dari satu jaringan ke jaringan selanjutnya.

Routing terbagi atas 2 cara, yaitu : 
 - **Routing Statis**
 - **Routing Dinamis**

**Routing statis** adalah proses mengkonfigurasi router jaringan menggunakan tabel routing yang dikonfigurasi secara manual oleh administrator jaringan.

**Routing Dinamis** adalah proses mengkonfigurasi router yang secara otomatis dapat menghasilkan tabel routing berdasarkan lalu lintas jaringan dan router yang terhubung.

Tidak seperti routing statis, routing dinamis memiliki protokol perutean yang secara otomatis mengatur router untuk berkomunikasi satu sama lain dengan memberikan informasi tentang jaringan dan koneksi antar router.

Routing yang akan dipelajari pada praktikum saat ini yaitu Static Routing (Perutean Statis), yang mengharuskan administrator jaringan untuk menambahkan/memberitahukan rute (route) baru ke dalam tabel routing ketika terdapat subnet tambahan dalam jaringannya.

Konsep static routing sederhana, daftarkan NID dan netmask yang ada serta tentukan gateway untuk menuju ke subnet tersebut. Untuk mencoba teknik routing static, kita akan menggunakan aplikasi Cisco Packet Tracer.

## Istilah

Istilah | Penjelasan
--------|-----------
ip route | Perintah untuk membuat static routing itu sendiri.
destination | Network yang hendak ditambahkan ke routing table
next_hop_address | Address dari hop router selanjutnya, yakni yang akan menerima paket dan mem-forward-nya lagi ke network remote.
iface | Disebut network interface, antarmuka yang menghubungkan 2 layer protokol. Setiap interface memiliki nama yang berbeda
eth0 | Salah satu nama interface yang digunakan untuk berhubungan dengan subnet
address | Sebuah alamat IP unik bagi komputer dalam sebuah jaringan
netmask | Kombinasi angka sepanjang 32 bit yang berfungsi membagi IP ke dalam subnet-subnet dan menentukan rentang alamat IP pada subnet yang bisa digunakan
gateway | Alamat IP yang menjadi pintu keluar menuju subnet lain, biasanya diisi alamat IP router terdekat

## Praktik

Buka software `cisco packet tracer` yang telah diinstal. Jika belum silahkan ikuti langkah-langkah pada [install Cisco](./install_cisco.md).

### 1). Membuat topologi
<img src="https://i.ibb.co/qB3ZKv3/image.png" alt="1" border="0" />

Untuk menambahkan Router, Switch, dan PC dapat dilakukan dengan *drag and drop* yang ada pada menu. Pada praktik kali ini, sesuaikan *device* dengan pilihan dengan kotak merah pada gambar di bawah 

* untuk menambahkan Cloud
<img src="https://i.ibb.co/VLxcnNf/image.png" alt="1" border="0" />

* untuk menambahkan Router
<img src="https://i.ibb.co/Q8X3Q2R/image.png" alt="1" border="0" />

* untuk menambahkan Switch
<img src="https://i.ibb.co/NT3mpWL/image.png" alt="1" border="0" />

* untuk menambahkan PC
<img src="https://i.ibb.co/JQWjqm7/image.png" alt="1" border="0" />

* untuk menambahkan Kabel
<img src="https://i.ibb.co/F0M3LnK/image.png" alt="1" border="0" />

* jika terdapat peringatan (*alert*) seperti dibawah ini ketika menyambungkan kabel antar device
<img src="https://i.ibb.co/NFMwL7q/image.png" alt="1" border="0" />

* Maka tambahkan port pada router terlebih dahulu.
<img src="https://i.ibb.co/VpmRp8N/image.png" alt="1" border="0" />

### 2). Subnetting

Praktik kali ini akan menerapkan cara routing untuk teknik *subnetting* **VLSM** yang telah kita lakukan sebelumnya.
<img src="https://i.ibb.co/3FgydKD/image.png" alt="1" border="0" />
<img src="https://i.ibb.co/Gk8BNT9/image.png" alt="1" border="0" />

Atur IP untuk masing-masing **interface** yang ada di setiap *device* sesuai dengan pembagian subnet pada pohon **VLSM**.

Pada Cisco Packet Tracer, interface dapat diatur pada menu **Config** > **INTERFACE** > **“nama interface”** (contoh: FastEthernet0/0). Isi alamat IP dan subnet mask dari subnet interface tersebut. Berikut contoh untuk mengatur IP pada subnet **A4**.

Atur IP pada interface LAB-PUSAT yang mengarah ke LABKOM-1 dengan **192.168.1.5**.
<img src="https://i.ibb.co/WvWn5zz/image.png" alt="1" border="0" />

Atur IP pada interface LABKOM-1 yang mengarah ke LAB-PUSAT dengan **192.168.1.6**.
<img src="https://i.ibb.co/T4Lrp6w/image.png" alt="1" border="0" />

Selanjutnya atur IP pada subnet A3.
Atur IP pada interface LABKOM-1 yang mengarah ke *client* dengan **192.168.1.65**.
<img src="https://i.ibb.co/BB7SDPj/image.png" alt="1" border="0" />

Atur IP pada *client* LABKOM-1 dengan cara :
- Masuk ke *client*
- Pilih tab Desktop
- Pilih IP Configuration

<img src="https://i.ibb.co/z5WZpKN/image.png" alt="1" border="0" />

<img src="https://i.ibb.co/f9k09d4/image.png" alt="1" border="0" />

Lakukan hal yang sama untuk mengatur alamat IP setiap ***interface*** pada device yang ada dalam topologi. Setelah selesai, lakukan langkah selanjutnya yaitu ***Routing*** agar topologi dapat berfungsi dengan semestinya.

### 3). Routing

Pada Cisco Packet Tracer, ***Routing*** dapat dilakukan pada menu **Config** > **Routing** > **Static** pada device **Router**. Lalu isi **Static Routes** seperti gambar dibawah pada LAB-PUSAT dan tekan tombol **Add**

![image](https://user-images.githubusercontent.com/31590281/211186519-b7d79c28-8551-4ad7-87b6-4272dc253b6d.png)

Pada *static routing* juga dibutuhkan ***default routing*** agar router dapat mengirimkan paket sesuai dengan tujuan. Default routing dibutuhkan untuk router yang berada di bawah router utama (router yang terhubung internet), contohnya LABKOM-1

![image](https://user-images.githubusercontent.com/31590281/211186553-ba757f74-f86e-4154-a510-09b29798a842.png)

***Keterangan*** : 
1. Network 192.168.1.64 adalah Network ID yang akan dihubungkan
2. Mask 255.255.255.192 adalah netmask dari subnet A3
3. Next Hop 192.168.1.65 (disebut **gateway**), adalah IP yang dituju ketika ingin menuju subnet poin 1, yaitu interface pada LABKOM-1 yang mengarah ke LAB-PUSAT

Sekarang, LAB-PUSAT dan *host* pada LABKOM-1 sudah saling terhubung. Agar semua subnet dapat saling terhubung, tambahkan *static routing* berikut :

1. Pada LAB-PUSAT
    
        Network 192.168.1.128 Netmask 255.255.255.128 Next Hop 192.168.1.6
        Network 192.168.1.0 Netmask 255.255.255.252 Next Hop 192.168.1.6
        Network 192.168.1.12 Netmask 255.255.255.252 Next Hop 192.168.1.10
        Network 192.168.1.16 Netmask 255.255.255.240 Next Hop 192.168.1.10
        Network 192.168.1.32 Netmask 255.255.255.224 Next Hop 192.168.1.10

2. Pada LABKOM-1

        Network 192.168.1.128 Netmask 255.255.255.128 Next Hop 192.168.1.2

3. Pada LABKOM-2
        
        Network 0.0.0.0 Netmask 0.0.0.0 Next Hop 192.168.1.1

4. Pada LABKOM-3

        Network 0.0.0.0 Netmask 0.0.0.0 Next Hop 192.168.1.9
        Network 192.168.1.16 Netmask 255.255.255.240 Next Hop 192.168.1.14
        Network 192.168.1.32 Netmask 255.255.255.224 Next Hop 192.168.1.14

5. Pada LABKOM-4

        Network 0.0.0.0 Netmask 0.0.0.0 Next Hop 192.168.1.13

**Kesimpulannya**, untuk melakukan *static routing* disesuaikan dengan daftar NID yang ada. Semakin banyak NID dalam suatu topologi, semakin banyak pula rute yang perlu ditambahkan ke router, maka diperlukan teknik pengelompokkan (***Subnetting***) yang tepat untuk menyederhanakan ***Routing***.
        
### 4). Testing

Untuk mengetesnya dapat dilakukan dengan cara ping dari client ke IP tujuan atau menggunakan tombol dengan ikon surat pada *toolbar*.
![image](https://user-images.githubusercontent.com/31590281/211187014-c741add7-5b1b-448b-8fb5-c23da01d201f.png)

Untuk hasilnya dapat dilihat pada tab hasil sebelah ujung kanan bawah
![image](https://user-images.githubusercontent.com/31590281/211187061-2874c476-ef81-4a65-8416-d4695b0dd7de.png)

## Latihan

![image](https://user-images.githubusercontent.com/31590281/211187699-9d0c3af3-907a-4655-bd01-ec78895e7a8c.png)

Implementasikan subnetting dan routing pada topologi di atas untuk IP dan subnet sesuai imajinasi/keinginan anda.

# SELAMAT MENCOBA !!
