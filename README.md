# Motor Listrik Induksi & Sistem Pengasutan Star-Delta

Repositori ini berisi materi pembelajaran, dokumentasi rangkaian, serta file simulasi untuk **Praktikum Mesin-Mesin Listrik (Tugas 2)** mengenai prinsip kerja Motor Listrik Induksi 3-Fasa dan sistem pengendali *Star-Delta Starter*.

---

## Pokok Bahasan Materi

### 1. Pengenalan Motor Induksi 3-Fasa
* **Prinsip Operasional:** Bekerja berdasarkan induksi elektromagnetik di mana suplai arus AC 3-fasa pada belitan stator membangkitkan medan magnet putar. Medan ini menginduksi rotor dan menghasilkan torsi putar dengan karakteristik adanya perbedaan kecepatan antara medan putar stator dan putaran rotor (*slip*).
* **Komponen Utama:** 
  * **Stator:** Bagian statis (diam) tempat terpasangnya belitan/kumparan tembaga.
  * **Rotor:** Bagian dinamis yang berputar menggerakkan beban mekanis.
  * **Terminal Box:** Pusat integrasi kelistrikan untuk menghubungkan suplai tegangan dengan ujung-ujung belitan motor (`U1, V1, W1` dan `U2, V2, W2`) guna mengatur konfigurasi hubung Bintang (*Star*) atau Segitiga (*Delta*).

### 2. Sistem Pengasutan Star-Delta (*Star-Delta Starter*)
* **Perbandingan dengan Metode DOL (*Direct On-Line*):** Pengasutan langsung (DOL) pada motor berkapasitas besar menyebabkan lonjakan arus awal (*starting current*) mencapai 5 hingga 7 kali lipat arus nominal. Metode *Star-Delta* mengatasi hal ini dengan mengasut motor pada konfigurasi *Star* (tegangan dan arus lebih rendah) saat awal berputar, lalu bertransisi ke konfigurasi *Delta* untuk operasional daya penuh.
* **Arsitektur Rangkaian:**
  * **Rangkaian Daya:** Mengatur jalur distribusi arus 3-fasa utama menuju terminal motor melalui Kontaktor Utama (`KM`), Kontaktor Star (`KS`), dan Kontaktor Delta (`KD`), dilengkapi pengaman *Thermal Overload Relay* (`OL`) dan MCB 3-Fasa.
  * **Rangkaian Kontrol:** Mengatur logika sekuensial perpindahan kontaktor secara otomatis menggunakan *Timer* (`T1`), dilengkapi sistem pengunci (*latching*), *interlock* pengaman, tombol `START`/`STOP`, *Emergency Stop* (`EMS`), serta lampu indikator status (`ON`, `OFF`, dan `TRIP`).

---

## Simulasi Rangkaian (CADe_SIMU)

Simulasi dirancang dan diuji menggunakan perangkat lunak **CADe_SIMU** untuk memvalidasi logika kontrol dan alur daya sebelum perakitan perangkat keras.

### Alur Kerja Simulasi:
1. **Kondisi Standby:** Saat `MCB` (rangkaian daya) dan `CB1` (rangkaian kontrol) diaktifkan, arus masuk ke jalur kontrol dan menyalakan lampu indikator **OFF** melalui kontak NC `KM`.
2. **Fase Starting (Hubung Star):** Saat tombol `START` ditekan, koil Kontaktor Utama (`KM`), *Timer* (`T1`), dan Kontaktor Star (`KS`) aktif secara bersamaan. Motor mulai berputar dengan konfigurasi *Star* dan lampu indikator **ON** menyala.
3. **Fase Transisi ke Running (Hubung Delta):** Setelah waktu tunda pada *Timer* (`T1`) tercapai, kontak NC `T1` (55-56) membuka untuk memutus suplai ke `KS`, sedangkan kontak NO `T1` (67-68) menutup untuk mengaktifkan Kontaktor Delta (`KD`). Motor beroperasi penuh pada konfigurasi *Delta*.
4. **Proteksi Beban Lebih (*Overload*):** Jika terjadi gangguan arus lebih pada motor, komponen `OL` akan bekerja membuka kontak NC `OL` (95-96) sehingga menghentikan seluruh operasi motor secara otomatis, sekaligus menutup kontak NO `OL` (97-98) untuk menyalakan lampu indikator **TRIP**.
5. **Penghentian Operasional:** Menekan tombol `STOP` atau `EMS` akan memutus aliran listrik pada rangkaian kontrol dan mengembalikan sistem ke kondisi *standby*.

---

## Perangkat Lunak yang Digunakan
* **CADe_SIMU** — *Software* desain skematik dan simulasi rangkaian elektromagnetik / kendali motor listrik
---

## Identitas Penyusun

* **Nama:** Elva Rizqina Khoirun Nisa
* **NIM:** 40040325650031
* **Program Studi:** Teknologi Rekayasa Otomasi
* **Departemen:** Teknologi Industri
* **Fakultas:** Sekolah Vokasi
* **Institusi:** Universitas Diponegoro

### Dosen Pengampu:
1. Rofiq Cahyo Prayogo, S.T., M.T.
2. Priyo Sasmoko, S.T., M.Eng.

---
*Disusun untuk memenuhi penugasan mata kuliah Praktikum Mesin-Mesin Listrik — Teknologi Rekayasa Otomasi, Universitas Diponegoro.
