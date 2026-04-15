# Modul 3 : Protokol Komunikasi

## 🎯 Tujuan Praktikum
1.	Memahami prinsip dasar protocol komunikasi pada Arduino pada Arduino Uno.
2.	Mengendalikan perangkat pada kit (misalnya LED) menggunakan perintah dari komputer.
3.	Mengimplementasikan pembacaan nilai analog dari potensiometer menggunakan LCD I2C.

## 📄 Dasar Teori
Mikrokontroler seperti Arduino merupakan bagian penting dari berbagai proyek DIY, termasuk robotika. Pada pembahasan sebelumnya, kita telah melihat tata letak pin dan fungsi GPIO pada Arduino Uno. Pin GPIO dapat digunakan untuk membaca atau menulis data digital, yaitu tegangan tinggi atau rendah secara kontinu, atau bekerja dengan data analog berupa sinyal PWM yang bergantian antara tegangan tinggi dan rendah dalam rentang waktu yang sangat singkat. Kita juga telah melihat bahwa mikrokontroler dan single-board computer ini mendukung berbagai fungsi GPIO, termasuk protokol untuk berkomunikasi data dengan perangkat keras lainnya.

Protokol komunikasi adalah seperangkat aturan yang menentukan bagaimana data ditransfer antar perangkat elektronik. Protokol ini mengatur bagaimana bit dikemas, dikirim, dan diinterpretasikan. Dalam Arduino, protokol ini memungkinkan mikrokontroler untuk berkomunikasi dengan sensor, modul, Arduino lain, bahkan komputer.

Pada Arduino ada beberapa jenis protokol komunikasi yaitu Serial (UART), I2C, and SPI

## 🚀 Tugas Pendahuluan

- Membuat semua program (source code) yang diperlukan untuk masing-masing percobaan (sertakan keterangan-keterangan penting pada source code menggunakan komentar); Jelaskan masing-masing baris atau bagian kode tersebut.
- Menyiapkan rangkaian hardware untuk percobaan (sudah dirangkai, sehingga saat percobaan langsung menjalankan program yang telah dibuat). Sertakan pada tugas pendahuluan dalam bentuk foto yang juga menampilkan wajah Anda. (Dilakukan untuk masing-masing percobaan; Sebelum praktikum, cukup siapkan untuk percobaan pertama saja jika space pada breadboard terbatas)

## ⚙️ Alat dan Bahan

Dalam percobaan sederhana ini, berikut alat dan bahan yang digunakan:

<div align="center">
<table border="1" cellpadding="10" cellspacing="0" width="100%">
  <tr>
    <th>Arduino</th>
    <th>Potensiometer</th>
    <th>LCD I2C</th>
    <th>LED</th>
    <th>Breadboard</th>
  </tr>

  <tr align="center">
    <td>
      <img width="192" height="136,1" alt="arduino_uno" src="https://github.com/user-attachments/assets/3e61e208-bb23-42aa-bbef-0ac539279ce0" /><br>
    </td>
    <td>
      <img width="79,5" height="125,75" alt="image" src="https://github.com/user-attachments/assets/f44c78e5-fd37-47e0-a2f4-0a5af2b6c86a" />
    </td>
    <td>
      <img width="160" height="141" alt="image" src="https://github.com/user-attachments/assets/416ce7db-b07e-4646-9b37-4883ad37d23c" />
    </td>
    <td>
      <img width="54" height="134" alt="RedLED_Fritzing" src="https://github.com/user-attachments/assets/80556570-c129-43fa-904b-39eac5677a2d" />
    </td>
    <td>
      <img width="200" height="126" alt="breadboard" src="https://github.com/user-attachments/assets/4c9fc9ea-116c-4bb7-b802-48314049936a" />
    </td>
  </tr>

  <tr align="center">
    <td>Arduino Uno, Leonardo, atau lainnya</td>
    <td>Potensiometer</td>
    <td>LCD I2C</td>
    <td>LED Merah</td>
    <td>Breadboard Mini</td>
  </tr>
</table>
</div>

## 💻 Percobaan
### Percobaan 3A: Komunikasi Serial (UART)
Komunikasi serial merupakan salah satu cara paling umum yang digunakan untuk bertukar data antar perangkat mikrokontroler, seperti Arduino. Melalui komunikasi serial, dua atau lebih perangkat dapat saling mengirim dan menerima informasi menggunakan jalur data tunggal, sehingga sistem dapat bekerja secara sinkron dan efisien. Salah satu komunikasi serial yang menjadi pembahasan pada bagian ini adalah Universal Asynchronous Receiver-Transmitter (UART).

Menampilkan ```"Hello World"``` menggunakan Serial Monitor. Menampilkan "Hello World" di Serial Monitor Arduino dilakukan dengan menginisialisasi komunikasi serial menggunakan ```Serial.begin(9600)``` di ```setup()``` dan mencetak teks dengan ```Serial.println("Hello World")``` di ```loop()``` atau ```setup()```

```cpp
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  Serial.print("Hello World");
}

void loop() {
  // put your main code here, to run repeatedly:
}
```

Berikutnya compile dan upload program ke dalam Arduino board. Perhatikan hasil yang terjadi, apakah sesuai dengan spesifikasi atau tidak.

https://github.com/user-attachments/assets/d489cc42-f489-404b-93de-cca64eafb324

Selanjutnya praktikan diminta melakukan percobaan untuk memberikan perintah pada LED untuk hidup (ON) dan mati (OFF) dengan menggunakan perintah yang diketikkan melalui Serial Monitor.

<div align="center">
  Percobaan pada modul ini dapat diakses melalui
  <table border="1" align="center" width="100%" cellpadding="0" cellspacing="0">
  <tr>
    <td>
      <h2>
        <a href="https://github.com/reslabunsoed/modul3_protokol_komunikasi/tree/415f758f50f99b710c36248be8a7da379313428a/Percobaan%201">
          Percobaan 3A: Serial Komunikasi (UART)
        </a>
      </h2>
    </td>
  </tr>
  </table>
</div>

### Percobaan 3B: Inter-Integrated Circuit (I2C)
Inter-Integrated Circuit atau I2C merupakan sebuah protokol komunikasi yang digunakan untuk pertukaran data antar perangkat mikrokontroler dan sensor atau pun perangkat lainnya. I2C dirancang untuk menghubungkan berbagai perangkat dalam sebuah sistem menggunakan jalur komunikasi bersama.

Berikut adalah contoh untuk mencetak tulisan pada I2C dengan menggunakan library ```LiquidCrystal_I2C```

```cpp
#include <LiquidCrystal_I2C.h>

const int col = 16;
const int row = 2;

LiquidCrystal_I2C lcd(0x20, col, row);

void setup() {
  lcd.init();        // Inisialisasi LCD
  lcd.clear();       // Membersihkan tampilan LCD
  lcd.backlight();   // Menghidupkan lampu latar (backlight)

  // Menampilkan pesan pada LCD
  lcd.setCursor(2, 0);  // Posisi kolom ke-2, baris ke-0
  lcd.print("Hello World!");

  lcd.setCursor(2, 1);  // Posisi kolom ke-2, baris ke-1
  lcd.print("Tutorial LCD");
}

void loop() {
  // Tidak ada perintah berulang
}
```

Berikutnya compile dan upload program ke dalam Arduino board. Perhatikan hasil yang terjadi, apakah sesuai dengan spesifikasi atau tidak. Contoh program berikut dengan menggunakan alternatif library ```LiquidCrystal_I2C``` yaitu ```Adafruit_LiquidCrystal.h```

https://github.com/user-attachments/assets/f093c6b6-7f0c-47d5-9ed7-c90b6afa22fa

Selanjutnya praktikan diminta melakukan percobaan untuk membaca nilai analog dari potensiometer menggunakan LCD I2C.

<div align="center">
  Percobaan pada modul ini dapat diakses melalui
  <table border="1" align="center" width="100%" cellpadding="0" cellspacing="0">
  <tr>
    <td>
      <h2>
        <a href="https://github.com/reslabunsoed/modul3_protokol_komunikasi/tree/2e873565382d1b693322ec329266630ff9a45819/Percobaan%202">
          Percobaan 3B: Inter-Intergrated Circuit (I2C)
        </a>
      </h2>
    </td>
  </tr>
  </table>
</div>

## 📚 Pertanyaan Praktikum
1.	Sebutkan dan jelaskan keuntungan dan kerugian menggunakan UART dan I2C!
2.	Bagaimana peran alamat I2C pada LCD (misalnya 0x27 vs 0x20)? Berikan penjelasan!
3.	Jika UART dan I2C digabung dalam satu sistem (misalnya input dari Serial Monitor, output ke LCD), bagaimana alur kerja sistem tersebut? Bagaimana Arduino mengelola dua protokol sekaligus?

## 🧰 Mengakhiri Percobaan

Berikut hal yang perlu dilakukan setelah selesai praktikum:
- Sebelum keluar dari ruang praktikum, pastikan meja dalam keadaan rapi.
- Jangan lupa untuk mendokumentasikan dalam bentuk foto dan video serta diunggah lewat google drive dan sertakan tautan dokumentasi tersebut di Buku Catatan Praktikum.
- Pastikan asisten telah menandatangani catatan percobaan kali ini pada Buku Catatan Praktikum Anda. Catatan percobaan yang tidak ditandatangani oleh asisten tidak akan dinilai.
- Kumpulkan kode program tugas tambahan pada setiap percobaan dalam repository github dengan format name repository “Kelas(value)_Modul(value)_Nama_NIM”


<h2></h2>

<br>

[![banner](https://github.com/user-attachments/assets/f1f03032-41c0-4121-94e3-df1d513b42e5)](https://github.com/reslabunsoed)
