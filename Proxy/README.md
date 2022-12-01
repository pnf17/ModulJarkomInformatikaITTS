# 2. Proxy Server

## 2.1 Pengertian, Fungsi, dan Manfaat

### 2.1.1 Pengertian

Proxy server adalah sebuah server atau program komputer yang berperan sebagai penghubung antara suatu komputer dengan jaringan internet. Atau dalam kata lain, proxy server adalah suatu jaringan yang menjadi perantara antara jaringan lokal dan jaringan internet.

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image32.jpeg?raw=true)

Proxy server dapat berupa suatu sistem komputer ataupun sebuah aplikasi yang bertugas menjadi gateway atau pintu masuk yang menghubungan komputer kita dengan jaringan luar.

### 2.1.2 Fungsi

1. ***Connection sharing*** : Proxy bertindak sebagai gateway yang menjadi pembatas antara jaringan lokal dengan jaringan luar. Gateway bertindak juga sebagai sebuah titik dimana sejumlah koneksi dari pengguna lokal dan koneksi jaringan luar juga terhubung kepadanya. Oleh sebab itu, koneksi dari jaringan lokal ke internet akan menggunakan sambungan yang dimiliki oleh gateway secara bersama-sama (connection sharing).
2. ***Filtering*** : Proxy bisa difungsikan untuk bekerja pada layar aplikasi dengan demikian maka dia bisa berfungsi sebagai firewalll paket filtering yang dapat digunakan untuk melindungi jaringan lokal terhadap gangguan maupun ancaman serangan dari jaringan luar. Fungsi filtering ini juga dapat diatur atau dikonfigurasi untuk menolak akses terhadap situs web tertentu dan pada waktu- waktu tertentu juga.
3. ***Caching*** : Sebuah proxy server mempunyai mekanisme penyimpanan obyek-obyek yang telah diminta dari server-server yang ada di internet. Dengan mekanisme caching ini maka akan menyimpan objek-objek yang merupakan berbagai permintaan/request dari para pengguna yang di peroleh dari internet.

### 2.1.3 Manfaat

Proxy server memiliki manfaat-manfaat berikut ini:

- Membagi koneksi
- Menyembunyikan IP
- Memblokir situs yang tidak diinginkan
- Mengakses situs yang telah diblokir
- Mengatur bandwith

### 2.1.4 Software Proxy Server

Beberapa contoh software proxy server yang sering digunakan adalah sebagai berikut:

1. CCProxy
2. WinGate
3. Squid
4. Nginx

### 2.1.5 Cara Kerja Squid

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image33.gif?raw=true)





## 2.2 Implementasi

Untuk praktikum jarkom kali ini, software proxy server yang digunakan adalah **Squid** dan UML yang digunakan sebagai proxy server adalah **Ardx**.

### 2.2.1 Instalasi Squid

**STEP 1** - Install squid pada UML **Ardx**, ketikkan:

```
apt-get install squid
```

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image34.png?raw=true)

**STEP 2** - Cek status squid untuk memastikan bahwa Squid telah berjalan dengan baik dengan mengetikkan

```
service squid status
```

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image35.png?raw=true)

Jika muncul status **ok** maka instalasi telah berhasil.



### 2.2.2 Konfigurasi Dasar Squid

**STEP 1** - Backup terlebih dahulu file konfigurasi default yang disediakan squid. Ketikkan perintah berikut untuk melakukan backup:

```
mv /etc/squid/squid.conf /etc/squid/squid.conf.bak
```

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image36.png?raw=true)

**STEP 2** - Buat konfigurasi baru dengan mengetikkan:

```
nano /etc/squid/squid.conf
```

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image37.png?raw=true)

**STEP 3** - Kemudian, pada file config yang baru, ketikkan script:

```
http_port 8080
visible_hostname Ardx
```

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image38.png?raw=true)

**Keterangan:**

- `http_port 8080` : Port yang digunakan untuk mengakses proxy, dalam kasus ini adalah **8080**. (Sintaks: `http_port 'PORT_YANG_DIINGINKAN'`)
- `visible_hostname Ardx` : Nama proxy yang akan terlihat oleh user (Sintaks: `visible_hostname 'NAMA_YANG_DIINGINKAN'`)

**STEP 4** - Restart squid dengan cara mengetikkan perintah:

```
service squid restart
```

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image39.png?raw=true)

**STEP 5** - Ubah pengaturan proxy browser. Gunakan **IP Ardx** sebagai host dan isikan port **8080**. Kemudian cobalah untuk mengakses web http://ittelkom-sby.ac.id (usahakan menggunakan mode **incognito/private**).

Cara Mengubah Pengaturan [Proxy Browser Chrome](https://www.niagahoster.co.id/blog/panduan-setting-proxy-browser/?amp) 

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image40.png?raw=true)

Maka akan muncul halaman seperti berikut:

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image41.png?raw=true)

**STEP 6** - Supaya bisa mengakses web http://ittelkom-sby.ac.id/, maka kalian harus menambah sebaris script pada konfigurasi squid. Buka kembali file konfigurasi tadi dan tambahkan baris berikut:

```
http_access allow all
```

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image42.png?raw=true)

**Keterangan:**

- `http_access allow all` : Memperbolehkan semuanya untuk mengakses proxy via http. Pengaturan ini perlu ditambahkan karena pengaturan default squid adalah **deny** (Sintaks: `http_access allow 'TARGET'`)
- Untuk menolak koneksi, maka **allow** diganti dengan **deny**.

**STEP 9** - **Simpan** file konfigurasi tersebut, lalu **restart** squid. Refresh halaman web http://ittelkom-sby.ac.id/.

Seharusnya halaman yang ditampilkan kembali normal.

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image43.png?raw=true)



### 2.2.3 Membuat User Login

**STEP 1** - Install `apache2-utils` pada UML **Ardx**. Sebelumnya kalian sudah harus melakukan `apt-get update`. Ketikkan:

```
apt-get install apache2-utils
```

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image44.png?raw=true)

**STEP 2** - Buat user dan password baru. Ketikkan:

```
htpasswd -c /etc/squid/passwd jarkom85
```

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image45.png?raw=true)

Ketikkan password yang diinginkan. Jika sudah maka akan muncul notifikasi:

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image46.png?raw=true)

**STEP 3** - Edit konfigurasi squid menjadi:

```
http_port 8080
visible_hostname Ardx

auth_param basic program /usr/lib/squid/basic_ncsa_auth /etc/squid/passwd
auth_param basic children 5
auth_param basic realm Proxy
auth_param basic credentialsttl 2 hours
auth_param basic casesensitive on
acl USERS proxy_auth REQUIRED
http_access allow USERS
```

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image47.png?raw=true)

**Keterangan:**

- `auth_param` digunakan untuk mengatur autentikasi (Sintaks: `auth_param 'SCHEME' 'PARAMETER' 'SETTING'`. Lebih lengkapnya di http://www.squid-cache.org/Doc/config/auth_param/).
- `program` : Perintah untuk mendefiniskan autentikator eksternal.
- `children` : Mendefinisikan jumlah maksimal autentikator muncul.
- `realm` : Teks yang akan muncul pada pop-up autentikasi.
- `credentialsttl` : Mengatur masa aktif suatu autentikasi berlaku.
- `casesensitive` : Mengatur apakah **username** bersifat case sensitive atau tidak.
- `acl` digunakan untuk mendefinisikan pengaturan akses tertentu. (Sintaks umum: **acl ACL_NAME ACL_TYPE ARGUMENT** . Lebih lengkapnya di http://www.squid-cache.org/Doc/config/acl/)
- Untuk melihat daftar apa saja yang bisa diatur dengan acl bisa diakses di: https://wiki.squid-cache.org/SquidFaq/SquidAcl)

**STEP 4** - Restart squid

**STEP 5** - Ubah pengaturan proxy browser. Gunakan **IP Ardx** sebagai host, dan isikan port **8080**. Kemudian cobalah untuk mengakses web **elearning.ittelkom-sby.ac.id** (usahakan menggunakan mode **incognito/private**), akan muncul pop-up untuk login.

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image48.png?raw=true)

**STEP 6** - Isikan username dan password.

**STEP 7** - E-learning berhasil dibuka.



### 2.2.4 Pembatasan Waktu Akses

Kita akan mencoba membatasi akses proxy pada hari dan jam tertentu. Asumsikan proxy dapat digunakan hanya pada hari **Senin** sampai **Jumat** pada jam **08.00-20.00**.

**STEP 1** - Buat file baru bernama **acl.conf** di folder **squid**

```
nano /etc/squid/acl.conf
```

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image49.png?raw=true)

**STEP 2** - Tambahkan baris berikut

```
acl KERJA time MTWHF 08:00-20:00
```

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image50.png?raw=true)

**STEP 3** - Simpan file **acl.conf**.

**STEP 4** - Buka file **squid.conf**.

```
nano /etc/squid/squid.conf
```

**STEP 5** - Ubah konfigurasinya menjadi:

```
include /etc/squid/acl.conf

http_port 8080
http_access allow KERJA
http_access deny all
visible_hostname Ardx
```

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image51.png?raw=true)

**STEP 6** - Simpan file tersebut. Kemudian restart squid.

**STEP 7** - Cobalah untuk mengakses web **http://ittelkom-sby.ac.id** (usahakan menggunakan mode **incognito/private**). Akan muncul halaman error jika mengakses diluar waktu yang telah ditentukan.

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image52.png?raw=true)

Keterangan:

- **MTWHF** adalah hari-hari dimana user diperbolehkan menggunakan proxy. **(S: Sunday, M: Monday, T: Tuesday, W: Wednesday, H: Thursday, F: Friday, A: Saturday)**
- Penulisan jam menggunakan format: **h1:m1-h2:m2**. Dengan syarat **h1<h2** dan **m1<m2**



### 2.2.5 Pembatasan Akses ke Website Tertentu

Kita akan mencoba membatasi akses ke beberapa website. Untuk contoh disini, kita akan memblokir website **elearning.ittelkom-sby.ac.id**

**STEP 1** - Buat file bernama **bad-sites.acl** di folder **squid** dengan mengetikkan:

```
nano /etc/squid/bad-sites.acl
```

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image53.png?raw=true)

**STEP 2** - Tambahkan alamat url yang akan diblock seperti baris berikut:

```
elearning.ittelkom-sby.ac.id
```

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image54.png?raw=true)

**STEP 3** - Ubah file konfigurasi squid menjadi seperti berikut ini.

```
http_port 8080
visible_hostname Ardx

acl BLACKLISTS dstdomain "/etc/squid/bad-sites.acl"
http_access deny BLACKLISTS
http_access allow all
```

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image55.png?raw=true)

**STEP 4** - Restart squid. Kemudian cobalah untuk mengakses web **elearning.ittelkom-sby.ac.id** (usahakan menggunakan mode **incognito/private**). Seharusnya muncul halaman error seperti di bawah ini.

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image56.png?raw=true)

Keterangan:

- **dstdomain** artinya destination domain/domain tujuan. Sintaksnya bisa diikuti dengan nama domain tujuan atau file yang menampung list-list alamat website.



### 2.2.6 Pembatasan Bandwidth

Kita akan mencoba untuk membatasi bandwidth yang akan diberikan kepada user proxy. Untuk contoh disini kita akan membatasi penggunaannya maksimal 512 kbps.

**STEP 1** - Buat file bernama **acl-bandwidth.conf** di folder squid

```
nano /etc/squid/acl-bandwidth.conf
```

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image57.png?raw=true)

**STEP 2** - Ketikkan baris berikut

```
delay_pools 1
delay_class 1 1
delay_access 1 allow all
delay_parameters 1 16000/64000
```

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image58.png?raw=true)

**STEP 3** - Ubah konfigurasi squid menjadi:

```
include /etc/squid/acl-bandwidth.conf
http_port 8080
visible_hostname Ardx

http_access allow all
```

![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image59.png?raw=true)

**STEP 4** - Restart Squid

**STEP 5** - Cobalah untuk melakukan speed test. Berikut perbedaan sebelum dan sesudah adanya pembatasan bandwidth saat melakukan speed test

|                           Sebelum                            |                           Setelah                            |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| ![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image60.png?raw=true) | ![jpeg](https://github.com/aldonesia/ModulJarkomInformatikaITTS/blob/modul-3/img/image61.png?raw=true) |

Keterangan:

- **delay_pools** digunakan untuk menentukan berapa bagian/pool yang akan dibuat. (Sintaks: **delay_pools JUMLAH_YANG_DIINGINKAN**. Lebih lengkap lihat di http://www.squid-cache.org/Doc/config/delay_pools/).
- **delay_class** digunakan untuk menentukan tipe/class pembagian bandwith dari setiap pool. (Sintaks: **delay_class POOL_KE_BERAPA KELAS**.) Lebih lengkap lihat di http://www.squid-cache.org/Doc/config/delay_class/.
- **delay_access** mirip seperti http_access, tetapi digunakan untuk mengakses pool yang telah dibuat (Sintaks: **delay_access POOL_KE_BERAPA allow/deny TARGET**. Lebih lengkap lihat di http://www.squid-cache.org/Doc/config/delay_access/).
- **delay_parameters** digunakan untuk mengatur parameter dari pool yang telah dibuat. Sintaks berbeda-beda sesuai dengan tipe/kelas dari pool yang dibuat. Lebih lengkap lihat di http://www.squid-cache.org/Doc/config/delay_parameters/
- **16000/64000** **(restore/max)** **restore** menentukan besarnya bandwith dalam satuan bytes/second **max** menentukan besarnya file atau bucket yang dapat dilewatkan tanpa melalui delay dalam satuan bytes.
- Penjelasan dari fitur **delay_pools** lebih lengkap bisa dilihat di https://wiki.squid-cache.org/Features/DelayPools