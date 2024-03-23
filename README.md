# Tutorial 6

## Commit 1 : Handle-connection, check response

```std::io::prelude``` dan ```std::io::Bufreader``` digunakan agar kita dapat membaca dan menulis dari stream.
Pada fungsi ```handle_connection```, dibuat instance baru sebuah ```Bufreader``` untuk membaca input data dari TCP Stream. Hasil pembacaan input data dibagi per line dengan menambahkan ```.lines``` yang mengembalikan sebuah iterator dari ```Result<String, std::io::Bufread>```. Untuk mendapatkan setiap String, setiap Result dimap lalu diunwrap. Lalu dicek hingga terdapat line yang kosong. Hasil String yang didapatkan berupa detail dari HTTP Request lalu dicollect lalu dimasukkan ke dalam sebuah vector. Lalu hasil dicetak ke layar.

## Commit 2 : Returning HTML

Perubahan dari commit sebelumnya adalah didefinisikan sebuah response untuk http request yang ada. Didefinisikan header responsenya, lalu dibuat satu halaman html. Dengan menggunakan modul ```fs```, file html itu dibaca dan lalu dihitung panjang kontennya. Lalu semua output yang ada diformat ke dalam satu variabel response. Panjang konten dihitung untuk memastikan konten http yang valid (sesuai dengan panjang ```hello.html```). Response lalu ditulis sebagai output ke stream. Saat ini belum dilakukan handling input dari request, sehingga semua request akan mendapatkan response berupa ```hello.html```.

![Commit 2 screen capture 1](/assets/images/commit2a.jpg)
![Commit 2 screen capture 2](/assets/images/commit2b.jpg)

## Commit 3 : Validating request and selectively responding

Untuk dapat melakukan split pada case request sukses dan not found, dapat digunakan if else seperti ini. Untuk mengecek request get yang sukses atau kasus di mana not found.

```
    if request_line == "GET / HTTP/1.1" {
        let status_line = "HTTP/1.1 200 OK";
        let contents = fs::read_to_string("hello.html").unwrap();
        // --snip--
    } else {
        let status_line = "HTTP/1.1 404 NOT FOUND";
        let contents = fs::read_to_string("404.html").unwrap();
        // --snip--
    }
```

Bagian kode snip sama namun isi variabel berbeda. Sehingga terjadi duplikasi kode yang dibutuhkan refactoring. Refactoring dapat dengan mendefinisikan terlebih dahulu status line dan filename konten html yang akan dibaca untuk setiap split ke variabel. Lalu variabel itu akan diproses menjadi response tanpa split seperti ini:

```
    let (status_line, filename) = if request_line == "GET / HTTP/1.1" {
        ("HTTP/1.1 200 OK", "hello.html")
    } else {
        ("HTTP/1.1 404 NOT FOUND", "404.html")
    };

```

![Commit 3 screen capture 1](/assets/images/commit3a.jpg)
![Commit 3 screen capture 2](/assets/images/commit3b.jpg)