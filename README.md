# Praktikum RTOS - SEMESTER 5 (3 Teknik Komputer A)
- Triyas Rahmadiyanti (3222600001)
- Duta Fithra Qolby (3222600003)
# EXERCISE 8 - Demonstrate how to eliminate resource contention in a selective manner - using a semaphore to protect the critical code section
## Deskripsi Projek
Proyek ini adalah implementasi sistem kendali berbasis STM32 yang mengontrol tiga LED (merah, hijau, dan kuning) menggunakan FreeRTOS untuk multitasking. 
Fokus utamanya adalah sinkronisasi akses ke sumber daya bersama melalui semaphore untuk menghindari konflik antar-tugas (threads). Setiap tugas memiliki fungsi spesifik,
seperti mengatur nyala/mati LED dengan interval tertentu atau melakukan operasi pada sumber daya bersama.
### Tugas-tugas dari projek ini
1. Pengendalian LED:
   - LED Merah: Menyala selama 550 ms, mengakses sumber daya bersama, lalu mati.
   - LED Hijau: Menyala selama 200 ms, mengakses sumber daya bersama, lalu mati.
   - LED Kuning: Berkedip pada frekuensi 10 Hz (toggle setiap 50 ms).
   - LED Biru: Indikasi konflik akses sumber daya bersama.
2. Sinkronisasi Sumber Daya Bersama: Semaphore digunakan untuk mengamankan akses ke sumber daya bersama (fungsi AccessSharedData()).
3. Operasi Timer: Timer digunakan untuk menghitung waktu operasi sumber daya bersama (dalam fungsi AccessSharedData()).
4. Penggunaan FreeRTOS: Penjadwalan berbasis prioritas untuk mengelola tugas.

## Alur Kerja
1. Inisialisasi Sistem:
   - Perangkat keras (GPIO, Timer) diinisialisasi.
   - RTOS diaktifkan, semaphore dibuat, dan tugas didefinisikan.
2. Multitasking dengan FreeRTOS:
   Scheduler RTOS mengatur eksekusi tiga tugas berdasarkan prioritas:
   - Tugas LED Merah dan Hijau: Prioritas Normal.
   - Tugas LED Kuning: Prioritas Di Atas Normal.
3. Eksekusi Tugas:
   - Tugas Hijau & Merah: Menggunakan semaphore untuk mengakses sumber daya bersama.
   - Tugas Kuning: Berkedip tanpa mengakses sumber daya bersama.
4. Pengelolaan Konflik: Jika akses sumber daya bersama dilakukan tanpa semaphore, LED Biru menyala untuk menunjukkan konflik.
5. Operasi Sumber Daya Bersama:
   - Simulasi akses data dengan penghitungan waktu menggunakan timer.
   - Flag digunakan untuk memastikan sinkronisasi.
6. Penanganan Error: Jika terjadi kesalahan sistem, eksekusi dihentikan dalam fungsi Error_Handler().

## Alur Eksekusi
1. Inisialisasi Sistem: HAL → Timer → GPIO → RTOS.
2. Pembuatan Tugas: red_led, green_led, yellow_led dengan prioritas masing-masing.
3. Scheduler: RTOS menjalankan tugas secara bergantian berdasarkan prioritas.
4. Eksekusi Tugas:
    - LED Merah & Hijau → Akses sumber daya bersama dengan semaphore.
    - LED Kuning → Toggle setiap 50 ms.
5. Akses Sumber Daya:
   - Akses data dengan sinkronisasi semaphore.
   - Deteksi konflik melalui flag dan LED Biru.
6. Error Handling: Sistem masuk ke infinite loop jika terjadi error.

# Gambar Hardware
<img width="182" alt="image" src="https://github.com/user-attachments/assets/850afa5f-655e-4793-80d5-399a436269b4">

# Video Hardware

https://github.com/user-attachments/assets/e9e2e87b-108e-429c-8c4b-26a62ae26d41


