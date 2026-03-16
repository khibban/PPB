# Demo Flutter Row & Column

Aplikasi Flutter sederhana yang menampilkan penggunaan **Row**, **Column**, **Container**, **AspectRatio**, dan **StatefulWidget** dengan counter.

## Fitur

* Menampilkan gambar berbentuk kotak menggunakan `AspectRatio`.
* Menampilkan teks deskriptif di bawah gambar.
* `Row` berisi ikon dengan label: **Food**, **Scenery**, **People**.
* Counter sederhana menggunakan `StatefulWidget` dan `setState`.

## Struktur Kode dan Penjelasan

### `MyApp`

Merupakan widget root dari aplikasi. Di sini kita menggunakan `MaterialApp` dengan pengaturan `theme` menggunakan `ColorScheme` dari seed color `deepPurple` dan `useMaterial3: true`. Widget utama (`home`) diarahkan ke `RowColumnPage`.

```dart
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepPurple),
        useMaterial3: true,
      ),
      home: const RowColumnPage(),
    );
  }
}
```

### `RowColumnPage`

Widget ini menggunakan `Scaffold` untuk membuat struktur halaman dengan `AppBar` dan `body`. Bagian `body` menggunakan `Column` sebagai layout utama.

#### Bagian Gambar

* Dibungkus `AspectRatio` dengan rasio 1:1 agar berbentuk kotak.
* `Container` di dalamnya memiliki margin dan padding.
* Gambar diambil dari URL menggunakan `Image.network`.

```dart
Container(
  child: AspectRatio(
    aspectRatio: 1.0,
    child: Container(
      margin: EdgeInsets.fromLTRB(20.0, 5.0, 20.0, 10.0),
      padding: EdgeInsets.all(20.0),
      color: Colors.lightBlue[100],
      child: Center(
        child: Image.network(
          'https://picsum.photos/200',
          fit: BoxFit.cover,
          width: 500,
        ),
      ),
    ),
  ),
),
```

#### Bagian Teks

* `Container` menampilkan teks deskriptif di bawah gambar.
* Padding dan margin digunakan untuk memberi ruang agar tidak menempel pada sisi layar.

```dart
Container(
  width: MediaQuery.of(context).size.width,
  margin: EdgeInsets.fromLTRB(20.0, 5.0, 20.0, 10.0),
  padding: EdgeInsets.all(20.0),
  color: Colors.pink[200],
  child: Text('What image is that', style: TextStyle(fontSize: 16)),
),
```

#### Bagian Row Ikon

* Menggunakan `Row` untuk menampilkan tiga kolom ikon dengan label.
* `mainAxisAlignment.spaceEvenly` untuk jarak yang sama antar kolom.
* Setiap ikon dan teks dibungkus `Column` agar vertikal.

```dart
Container(
  width: MediaQuery.of(context).size.width,
  color: Colors.yellow[200],
  padding: EdgeInsets.all(20.0),
  margin: EdgeInsets.fromLTRB(20.0, 5.0, 20.0, 5.0),
  child: Row(
    mainAxisAlignment: MainAxisAlignment.spaceEvenly,
    crossAxisAlignment: CrossAxisAlignment.start,
    children: <Widget>[
      Column(children: [Icon(Icons.food_bank), Text("Food")]),
      Column(children: [Icon(Icons.landscape), Text("Scenery")]),
      Column(children: [Icon(Icons.people), Text("People")]),
    ],
  ),
),
```

### `CounterCard`

* `StatefulWidget` untuk menampilkan counter yang bisa diubah.
* Variabel `_counter` menyimpan nilai saat ini.
* Fungsi `_incrementCounter` menggunakan `setState` untuk memperbarui UI saat tombol ditekan.

```dart
class CounterCard extends StatefulWidget {
  const CounterCard({super.key});

  @override
  State<CounterCard> createState() => _CounterCardState();
}

class _CounterCardState extends State<CounterCard> {
  int _counter = 0;

  void _incrementCounter() {
    setState(() {
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Container(
      margin: EdgeInsets.fromLTRB(20.0, 5.0, 20.0, 5.0),
      padding: EdgeInsets.all(20.0),
      width: MediaQuery.of(context).size.width,
      color: Colors.cyan[100],
      child: Row(
        mainAxisAlignment: MainAxisAlignment.spaceBetween,
        children: [
          Text("Counter here: $_counter", style: TextStyle(fontSize: 16)),
          Container(
            color: Colors.cyan[200],
            padding: EdgeInsets.all(5.0),
            child: IconButton(
              onPressed: _incrementCounter,
              icon: Icon(Icons.add, color: Colors.black, size: 16),
            ),
          ),
        ],
      ),
    );
  }
}
```