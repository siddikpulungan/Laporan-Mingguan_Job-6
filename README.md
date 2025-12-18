# Laporan-Mingguan_Job-6
Nama: Aulia Siddik Pulungan 
NPM: 2410017514009
Prodi: TRKJ
Mata Kuliah: LAB IV Basic Analog Electronic

## Tujuan Praktikum
Tujuan dari praktikum Seven Segment ini adalah:
   1. Mengetahui cara kerja komponen Seven Segment Display.
   2. Mengetahui cara kerja Arduino dalam mengendalikan Seven Segment.
   3. Menguji keterkiriman source code Arduino ke Seven Segment dan memastikan tampilan angka berjalan dengan benar.

###Teori Dasar
Seven Segment Display adalah komponen elektronika yang berfungsi menampilkan angka desimal (0–9) melalui kombinasi 7 segmen LED. Komponen ini sering digunakan pada jam digital, kalkulator, panel indikator, microwave, counter, dan perangkat digital lainnya.
Seven Segment memiliki 7 segmen utama (a–g) dan 1 titik desimal (dp).
Untuk menyalakan angka tertentu, Arduino harus mengaktifkan kombinasi segmen yang sesuai.

Jenis Seven Segment:
1. Common Cathode
   a. Semua kaki katoda (–) tergabung menjadi satu.
   b. Segmen akan menyala jika menerima tegangan positif pada kaki anoda.

2. Common Anode
   a. Semua kaki anoda (+) tergabung menjadi satu.
   b. Segmen menyala jika diberikan logika LOW pada kaki katoda.

#### Peralatan
Peralatan yang digunakan dalam praktikum ini:
-Laptop
-Board Arduino
-Kabel USB
-Breadboard
-Seven Segment
-Kabel jumper

##### Rangkaian Praktikum
Rangkaian Seven Segment dengan Arduino mengikuti skema pada modul (Gambar 5.3).
Konfigurasi umum pin:
1. Arduino → pin 2, 3, 4, 5, 6, 7, 8 (untuk segmen a–g)
2. Arduino → pin 9 (untuk titik “dot”)
Setiap segmen dihubungkan ke pin Arduino menggunakan resistor pembatas.

#####Prosedur Praktikum
Langkah kerja praktikum:
 1. Mempersiapkan peralatan yang diperlukan.
 2. Membuka Arduino IDE, kemudian menulis listing program untuk seven segment.
 3. Mengecek ulang kode yang telah ditulis.
 4. Merangkai Seven Segment ke Arduino sesuai diagram modul.
 5. Menyambungkan Arduino ke laptop melalui kabel USB.
 6. Mengecek kembali rangkaian apakah sudah benar.
 7. Meng-compile dan meng-upload program ke Arduino.
 8. Mengamati hasil percobaan, yaitu angka 0 sampai 9 menyala secara berurutan.

###### Screenshot Prosedur Praktikum

####### Source Code Arduino
Berikut kode program dari modul untuk menampilkan angka 0–9 pada Seven Segment:
Arduino pin: 2,3,4,5,6,7,8

byte seven_seg_digits[10][7] = { 
{ 0,0,0,0,0,0,1 },  // = 0
{ 1,0,0,1,1,1,1 },  // = 1
{ 0,0,1,0,0,1,0 },  // = 2
{ 0,0,0,0,1,1,0 },  // = 3
{ 1,0,0,1,1,0,0 },  // = 4
{ 0,1,0,0,1,0,0 },  // = 5
{ 0,1,0,0,0,0,0 },  // = 6
{ 0,0,0,1,1,1,1 },  // = 7
{ 0,0,0,0,0,0,0 },  // = 8
{ 0,0,0,0,1,0,0 },  // = 9
};

void setup() {               
  pinMode(2, OUTPUT);  
  pinMode(3, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(5, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(7, OUTPUT);
  pinMode(8, OUTPUT);
  pinMode(9, OUTPUT);

  writeDot(1);  // Mematikan titik (dot)
}

void writeDot(byte dot) {
  digitalWrite(9, dot);
}

void sevenSegWrite(byte digit) {
  byte pin = 2;
  for(byte segCount = 0; segCount < 7; ++segCount) {
    digitalWrite(pin, seven_seg_digits[digit][segCount]);
    ++pin;
  }
}

void loop() {
  for(byte count = 0; count < 10 ; ++count) {   
    sevenSegWrite(count);
    delay(1000);
  }

  for(byte count = 9; count > 0; --count) {
    sevenSegWrite(count-1);
    delay(1000);
  }
}
