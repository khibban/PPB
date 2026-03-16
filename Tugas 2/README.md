Aplikasi Tebak Gambar Sederhana (Flutter)

Aplikasi ini merupakan aplikasi Flutter sederhana yang menampilkan sebuah gambar acak dari internet dan meminta pengguna menebak gambar tersebut. Pengguna dapat memasukkan jawaban melalui form input, kemudian jawaban tersebut akan ditampilkan di layar.

Penjelasan

# 1. Fungsi main()
```dart
void main() {
  runApp(const MyApp());
}
```
Fungsi ini merupakan titik awal (entry point) dari aplikasi Flutter.

Fungsi runApp() digunakan untuk menjalankan widget utama yaitu MyApp.

# 2. Class MyApp
```dart
class MyApp extends StatelessWidget
```
MyApp adalah widget utama dari aplikasi yang mengatur konfigurasi dasar aplikasi.

Fungsi utama

- Menentukan tema aplikasi
- Menentukan halaman utama aplikasi
- Menggunakan MaterialApp sebagai dasar tampilan

# 3. Class RowColumnPage
```dart
class RowColumnPage extends StatelessWidget
```
Class ini merupakan halaman utama aplikasi yang menampilkan gambar, pertanyaan, dan form input.

# Struktur tampilan
Layout utama menggunakan Column sehingga komponen disusun secara vertikal.

```
Column
 ├── Container Gambar
 ├── Container Pertanyaan
 └── FormImage (Form Jawaban)
```

# 4. Widget FormImage

```dart
class FormImage extends StatefulWidget
```
Widget ini digunakan untuk membuat form input jawaban dari pengguna.

Karena data jawaban akan berubah, maka digunakan StatefulWidget.

# Class _FormImageState

Class ini menyimpan dan mengelola data dari form.

## Variabel
```dart
final _formKey = GlobalKey<FormState>();
String _answer = '';
```

| Variabel | Fungsi                          |
| -------- | ------------------------------- |
| _formKey | Mengontrol dan memvalidasi form |
| _answer  | Menyimpan jawaban pengguna      |

## Form
```dart
Form(
  key: _formKey
)
```
Widget Form digunakan untuk mengelompokkan field input serta memudahkan proses validasi.

## TextFormField
```dart
TextFormField(
  decoration: InputDecoration(label: Text("Enter your answer"))
)
```
Field ini digunakan untuk memasukkan jawaban pengguna.

## Validasi Input
```dart
validator: (value) => value!.isEmpty ? 'Please answer' : null
```
Field ini untuku menvalidasi input

## Menyimpan Jawaban
```dart
onSaved: (value) => setState(() {
  _answer = value!;
})
```
Ketika form disubmit:

- Nilai input disimpan ke variabel _answer
- setState() dipanggil untuk memperbarui tampilan

## Tombol Submit
```dart
ElevatedButton(
  onPressed: () {
    if (_formKey.currentState!.validate()) {
      _formKey.currentState!.save();
      _formKey.currentState!.reset();
    }
  }
)
```
Proses ketika tombol ditekan:
- Form akan divalidasi
- Jika valid, jawaban akan disimpan
- Field input akan dikosongkan kembali