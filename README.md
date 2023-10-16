# **Praktikum 2 Jaringan Komputer**
<div align=justify>

Berikut adalah Repository dari Kelompok A17 untuk pengerjaan Praktikum Modul 2 Jaringan Komputer. Dalam Repository ini terdapat Anggota Kelompok, Dokumentasi serta Penjelasan tiap soal, Screenshot Output, dan Kendala yang dialami.

# **Anggota Kelompok**

| Nama                      | NRP        | Kelas                |
| ------------------------- | ---------- | ----------------     |
| Andrian                | 5025211079 | Jaringan Komputer A  |
| Akmal Ariq Romadhon       | 5025211188 | Jaringan Komputer A  |

# **Dokumentasi dan Penjelasan Soal**
<div align=justify>

Berikut adalah dokumentasi yang berisi source code dari tiap soal dan penjelasan terkait perintah yang digunakan. 

## **Soal Nomor 1**
Yudhistira akan digunakan sebagai DNS Master, Werkudara sebagai DNS Slave, Arjuna merupakan Load Balancer yang terdiri dari beberapa Web Server yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Buatlah topologi dengan pembagian sebagai berikut. Folder topologi dapat diakses pada drive berikut 

## **Penyelesaian Soal Nomor 1**
Berikut adalah hasil pembuatan topologi dari kelompok A17 yang sesuai dengan drive (Topologi 7). Dalam topologi tersebut, terdapat 1 _DNS-Master_, 1 _DNS-Slave_, 3         _Webserver_, 2 _Client_, dan 1 _Load Balancer_. 

![topologi](https://cdn.discordapp.com/attachments/1150687865420906517/1163510232002072761/image.png?ex=653fd658&is=652d6158&hm=9526708c8815b8296ef88f68d1d5e9ae46d409f835ab278ab78485bda229bc20&)

## **Soal Nomor 2**
Buatlah website utama pada node arjuna dengan akses ke arjuna.yyy.com dengan alias www.arjuna.yyy.com dengan yyy merupakan kode kelompok.

## **Penyelesaian Soal Nomor 2**
Untuk membuat _website_ utama dengan akses ke `arjuna.a17.com` dan `www.arjuna.a17.com`, dilakukan kongfigutasi pada file `/etc/bind/jarkom/Arjuna.A17.com` seperti pada code berikut:
```bash
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     Arjuna.A17.com. root.Arjuna.A17.com. (
                     2022100601         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      Arjuna.A17.com.
@       IN      A       192.177.1.4
www     IN      CNAME   Arjuna.A17.com.
@       IN      AAAA    ::1
```

Untuk proses testing, dapat dilakukan dengan cara melakukan ping mengarah ke arjuna.a17.com tersebut sesuai dengan gambar berikut:

![Image2](https://cdn.discordapp.com/attachments/1150687865420906517/1163512658092380321/image.png?ex=653fd89a&is=652d639a&hm=204f9391c4b3cb2695289c5710f9a6c0adc24fd341df0b9837258b5266b5941d&)

## **Soal Nomor 3**
Dengan cara yang sama seperti soal nomor 2, buatlah website utama dengan akses ke abimanyu.yyy.com dan alias www.abimanyu.yyy.com.

## **Penyelesaian Soal Nomor 3**
Untuk membuat _website_ utama dengan akses ke `abimanyu.a17.com` dan `www.abimanyu.a17.com`, dilakukan kongfigurasi pada file `/etc/bind/jarkom/Abimanyu.A17.com` seperti pada _code _ berikut:
```bash
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     Abimanyu.A17.com. root.Abimanyu.A17.com. (
                     2022100601           ; Serial
                         604800           ; Refresh
                          86400           ; Retry
                        2419200           ; Expire
                         604800 )         ; Negative Cache TTL
;
@               IN      NS      Abimanyu.A17.com.
@               IN      A       192.177.3.3
www             IN      CNAME   Abimanyu.A17.com.
ns1             IN      A       192.177.2.2
baratayuda      IN      NS      ns1
@               IN      AAAA    ::1
```
Untuk proses testing, dapat dilakukan dengan cara melakukan ping mengarah ke domain `abimanyu.a17.com` sesuai dengan gambar berikut:

![image3](https://cdn.discordapp.com/attachments/1150687865420906517/1163514542115008552/image.png?ex=653fda5b&is=652d655b&hm=b42d93165c321e2fb4b29c64ced88ada431e6a29b192651d3c064a5835f058f9&)

## **Soal Nomor 4**
Kemudian, karena terdapat beberapa web yang harus di-deploy, buatlah subdomain parikesit.abimanyu.yyy.com yang diatur DNS-nya di Yudhistira dan mengarah ke Abimanyu.

## **Penyelesaian Soal Nomor 4**
Untuk menyelesaikan soal nomor 4, hanya perlu menambah config dari nomor sebeumnya dengan config `CNAME`. Berikut adalah _code_ untuk melakukan hal tersebut:

```Bash
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     Abimanyu.A17.com. root.Abimanyu.A17.com. (
                     2022100601           ; Serial
                         604800           ; Refresh
                          86400           ; Retry
                        2419200           ; Expire
                         604800 )         ; Negative Cache TTL
;
@               IN      NS      Abimanyu.A17.com.
@               IN      A       192.177.3.3
www             IN      CNAME   Abimanyu.A17.com.
parikesit       IN      A       192.177.3.3
www.parikesit   IN      CNAME   parikesit.Abimanyu.A17.com.
ns1             IN      A       192.177.2.2
baratayuda      IN      NS      ns1
@               IN      AAAA    ::1

```
Dalam _code_ tersebut terdapat CNAME tambahan untuk `parikesit` dan `www.parikesit` sesuai dengan perintah soal. Testing dapat dilakukan dengan melakukan ping ke `parikesit.abimanyu.a17.com` dan `www.parikesit.abimanyu.a17.com`

## **Soal Nomor 5**
Buat juga reverse domain untuk domain utama. (Abimanyu saja yang direverse)

## **Penyelesaian Soal Nomor 5**
Untuk soal nomor 5, dilakukan proses pembuatan reverse domain dengan kongfigurasi pada file `2.177.192.in-addr.arpa` sehingga filenya menjadi sebagai berikut:

```bash
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     Abimanyu.A17.com. root.Abimanyu.A17.com. (
                     2022100601         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
2.177.192.in-addr.arpa. IN      NS      Abimanyu.A17.com.
3                       IN      PTR     Abimanyu.A17.com.

```
Untuk melakukan testing, dapat menggunakan `dnsutils` pada _client_ dengan syntax `host -t PTR "IP EniesLobby` seperti pada gambar berikut:

![image5](https://cdn.discordapp.com/attachments/1150687865420906517/1163520742089035806/image.png?ex=653fe022&is=652d6b22&hm=3184ebfa995d24ebd7914b93ebeb71cfa9246e68871912f7a2eb1652ca3e8f02&)

## **Soal Nomor 6**
Agar dapat tetap dihubungi ketika DNS Server Yudhistira bermasalah, buat juga Werkudara sebagai DNS Slave untuk domain utama.

## **Penyelesaian Soal Nomor 6** 
Untuk membuat DNS-Slave, perlu dilakukan kongfigurasi dari `named.config.local` pada DNS-Master dan DNS-Slave. Berikut adalah _code_ untuk membuat slave domain:

- DNS Master (Yudhistira)
```bash
/
// Do any local configuration here
//

// Consider adding the 1918 zones here, if they are not used in your
// organization
// include "/etc/bind/zones.rfc1918";

zone "Arjuna.A17.com" {
        type master;
        notify yes;
        also-notify { 192.177.2.2; };
        allow-transfer { 192.177.2.2; };
        file "/etc/bind/jarkom/Arjuna.A17.com";
};

zone "Abimanyu.A17.com" {
        type master;
        notify yes;
        also-notify { 192.177.2.2; };
        allow-transfer { 192.177.2.2; };
        file "/etc/bind/jarkom/Abimanyu.A17.com";
};

zone "2.177.192.in-addr.arpa" {
    type master;
    file "/etc/bind/jarkom/2.177.192.in-addr.arpa";
};
```
- DNS _Slave_ (Werkudara)
```bash
//
// Do any local configuration here
//

// Consider adding the 1918 zones here, if they are not used in your
// organization
//include "/etc/bind/zones.rfc1918";

zone "Arjuna.A17.com" {
    type slave;
    masters { 192.177.2.3; };
    file "/var/lib/bind/Arjuna.A17.com";
};

zone "Abimanyu.A17.com" {
    type slave;
    masters { 192.177.2.3; };
    file "/var/lib/bind/Abimanyu.A17.com";
};

zone "Baratayuda.Abimanyu.A17.com" {
        type master;
        file "/etc/bind/Baratayuda/Baratayuda.Abimanyu.A17.com";
};
```
Untuk melakukan _test_ untuk nomor 6, dapat dilakukan ping menuju salah satu _domain_ dengan mematikan Service DNS Masternya terlebih dahulu. Berikut adalah _screenshot_ untuk pembuktiannya:

![image7](https://cdn.discordapp.com/attachments/1150687865420906517/1163525732039921754/image.png?ex=653fe4c7&is=652d6fc7&hm=d2b5fbc0c72b504a7b44efd0228d85954ca81d19e95ecf4de03d84669fb08c5a&)

## **Soal Nomor 7**
Seperti yang kita tahu karena banyak sekali informasi yang harus diterima, buatlah subdomain khusus untuk perang yaitu baratayuda.abimanyu.yyy.com dengan alias www.baratayuda.abimanyu.yyy.com yang didelegasikan dari Yudhistira ke Werkudara dengan IP menuju ke Abimanyu dalam folder Baratayuda.

## **Penyelesaian Soal Nomor 7** 
Soal nomor 7 dapat diselesaikan dengan menambah kongfigurasi _file_ Baratayuda pada _DNS Slave_ (Werkudara) dengan direktori filenya terdapat pada `/etc/bind/Baratayuda/Baratayuda.Abimanyu.A17.com` sehingga _code_-nya menjadi seperti berikut:
```bash
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     Baratayuda.Abimanyu.A17.com. root.Baratayuda.Abimanyu.A17.com. (
                     2022100601         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      Baratayuda.Abimanyu.A17.com.
@       IN      A       192.177.3.3
www     IN      CNAME   Baratayuda.Abimanyu.A17.com.
```

Untuk melakukan _testing_ untuk soal nomor 7, dapat dilakukan ping ke `baratayuda.abimanyu.a17.com` dan `www.baratayuda.abimanyu.a17.com` seperti pada gambar berikut:

![Image7](https://cdn.discordapp.com/attachments/1150687865420906517/1163532187992338513/image.png?ex=653feacb&is=652d75cb&hm=7f248ab496ef39088be525f9ba79ca96485150beeb5dbf1cc6b61efecbbb9a89&)

## **Soal Nomor 8**
Untuk informasi yang lebih spesifik mengenai Ranjapan Baratayuda, buatlah subdomain melalui Werkudara dengan akses rjp.baratayuda.abimanyu.yyy.com dengan alias www.rjp.baratayuda.abimanyu.yyy.com yang mengarah ke Abimanyu.

## **Penyelesaian Soal Nomor 8**

Soal nomor 8 dapat diselesaikan dengan menambah kongfigurasi `CNAME`  pada _DNS Slave_ (Werkudara) sehingga _code_-nya menjadi seperti berikut:

```bash
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     Baratayuda.Abimanyu.A17.com. root.Baratayuda.Abimanyu.A17.com. (
                     2022100601         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      Baratayuda.Abimanyu.A17.com.
@       IN      A       192.177.3.3
www     IN      CNAME   Baratayuda.Abimanyu.A17.com.
rjp     IN      A       192.177.3.3
www.rjp IN      CNAME   rjp.Baratayuda.Abimanyu.A17.com.
```
Untuk melakukan _testing_ untuk soal nomor 7, dapat dilakukan ping ke domain `rjp.baratayuda.abimanyu.a17.com` dan `www.rjp.baratayuda.abimanyu.a17.com` seperti pada gambar berikut:

![Image8](https://cdn.discordapp.com/attachments/1150687865420906517/1163532442150379550/image.png?ex=653feb07&is=652d7607&hm=3b452d72a6c1d8352c345f734c72a40bf6c713f763767446a3f57ebeac4e0162&)

## **Soal Nomor 9**
Arjuna merupakan suatu Load Balancer Nginx dengan tiga worker (yang juga menggunakan nginx sebagai webserver) yaitu Prabakusuma, Abimanyu, dan Wisanggeni. Lakukan deployment pada masing-masing worker.

## **Penyelesaian Soal Nomor 9** 
    
## **Soal Nomor 10**
Kemudian gunakan algoritma Round Robin untuk Load Balancer pada Arjuna. Gunakan server_name pada soal nomor 1. Untuk melakukan pengecekan akses alamat web tersebut kemudian pastikan worker yang digunakan untuk menangani permintaan akan berganti ganti secara acak. Untuk webserver di masing-masing worker wajib berjalan di port 8001-8003. Contoh
- Prabakusuma:8001
- Abimanyu:8002
- Wisanggeni:8003

## **Penyelesaian Soal Nomor 10**

## **Soal Nomor 11**
Selain menggunakan Nginx, lakukan konfigurasi Apache Web Server pada worker Abimanyu dengan web server www.abimanyu.yyy.com. Pertama dibutuhkan web server dengan DocumentRoot pada /var/www/abimanyu.yyy

## **Penyelesaian Soal Nomor 11**

## **Soal Nomor 12**
Setelah itu ubahlah agar url www.abimanyu.yyy.com/index.php/home menjadi www.abimanyu.yyy.com/home.

## **Penyelesaian Soal Nomor 12**

## **Soal Nomor 13**
Selain itu, pada subdomain www.parikesit.abimanyu.yyy.com, DocumentRoot disimpan pada /var/www/parikesit.abimanyu.yyy

## **Penyelesaian Soal Nomor 13**

## **Soal Nomor 14**
Pada subdomain tersebut folder /public hanya dapat melakukan directory listing sedangkan pada folder /secret tidak dapat diakses (403 Forbidden).

## **Penyelesaian Soal Nomor 14**

## **Soal Nomor 15**
Buatlah kustomisasi halaman error pada folder /error untuk mengganti error kode pada Apache. Error kode yang perlu diganti adalah 404 Not Found dan 403 Forbidden.

## **Penyelesaian Soal Nomor 15**

## **Soal Nomor 16**
Buatlah kustomisasi halaman error pada folder /error untuk mengganti error kode pada Apache. Error kode yang perlu diganti adalah 404 Not Found dan 403 Forbidden.

## **Penyelesaian Soal Nomor 16** 

## **Soal Nomor 17**
Agar aman, buatlah konfigurasi agar www.rjp.baratayuda.abimanyu.yyy.com hanya dapat diakses melalui port 14000 dan 14400.

## **Penyelesaian Soal Nomor 17** 

## **Soal Nomor 18**
Untuk mengaksesnya buatlah autentikasi username berupa “Wayang” dan password “baratayudayyy” dengan yyy merupakan kode kelompok. Letakkan DocumentRoot pada /var/www/rjp.baratayuda.abimanyu.yyy.

## **Penyelesaian Soal Nomor 18**
    
## **Soal Nomor 19**
Buatlah agar setiap kali mengakses IP dari Abimanyu akan secara otomatis dialihkan ke www.abimanyu.yyy.com (alias)

## **Penyelesaian Soal Nomor 19** 
    
## **Soal Nomor 20**
Karena website www.parikesit.abimanyu.yyy.com semakin banyak pengunjung dan banyak gambar gambar random, maka ubahlah request gambar yang memiliki substring “abimanyu” akan diarahkan menuju abimanyu.png.

## **Penyelesaian Soal Nomor 20**

# **Kendala Saat Pengerjaan**

# **End of The Line**

```c
#include <stdio.h>

int main(){
    printf("Thank you!");
}
```