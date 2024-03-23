# Tutorial 6

## Handle-connection, check response

```std::io::prelude``` dan ```std::io::Bufreader``` digunakan agar kita dapat membaca dan menulis dari stream.
Pada fungsi ```handle_connection```, dibuat instance baru sebuah ```Bufreader``` untuk membaca input data dari TCP Stream. Hasil pembacaan input data dibagi per line dengan menambahkan ```.lines``` yang mengembalikan sebuah iterator dari ```Result<String, std::io::Bufread>```. Untuk mendapatkan setiap String, setiap Result dimap lalu diunwrap. Lalu dicek hingga terdapat line yang kosong. Hasil String yang didapatkan berupa detail dari HTTP Request lalu dicollect lalu dimasukkan ke dalam sebuah vector. Lalu hasil dicetak ke layar.