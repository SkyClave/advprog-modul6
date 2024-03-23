# Tutorial 6

## Commit 1 : Handle-connection, check response

```std::io::prelude``` dan ```std::io::Bufreader``` digunakan agar kita dapat membaca dan menulis dari stream.
Pada fungsi ```handle_connection```, dibuat instance baru sebuah ```Bufreader``` untuk membaca input data dari TCP Stream. Hasil pembacaan input data dibagi per line dengan menambahkan ```.lines``` yang mengembalikan sebuah iterator dari ```Result<String, std::io::Bufread>```. Untuk mendapatkan setiap String, setiap Result dimap lalu diunwrap. Lalu dicek hingga terdapat line yang kosong. Hasil String yang didapatkan berupa detail dari HTTP Request lalu dicollect lalu dimasukkan ke dalam sebuah vector. Lalu hasil dicetak ke layar.

## Commit 2 : Returning HTML

Perubahan dari commit sebelumnya adalah didefinisikan sebuah response untuk http request yang ada. Didefinisikan header responsenya, lalu dibuat satu halaman html. Dengan menggunakan modul ```fs```, file html itu dibaca dan lalu dihitung panjang kontennya. Lalu semua output yang ada diformat ke dalam satu variabel response. Panjang konten dihitung untuk memastikan konten http yang valid (sesuai dengan panjang ```hello.html```). Response lalu ditulis sebagai output ke stream. Saat ini belum dilakukan handling input dari request, sehingga semua request akan mendapatkan response berupa ```hello.html```.

![Commit 2 screen capture 1](/assets/images/commit2a.jpg)
![Commit 2 screen capture 2](/assets/images/commit2b.jpg)