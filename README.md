# RailSight : Drone Technology for Obstacle Avoidance, Collision, Detection, and Smart Brake Management in Modern Tranin Systems
Proyek ini bertujuan untuk meningkatkan keamanan dan efisiensi kereta modern, drone ini dirancang untuk memadamkan api jika kereta mengalami kecelakaan dan drone memiliki sistem keamanan berupa shield akan aktif ketika api mendekati drone dengan jarak 5 meter, lalu drone akan kembali membuka shield nya ketika tempuh jarak normal yaitu 10 meter.
# Authors
1. Ahmad Rafli Al Adzani (2042231001)
2. Muhammad Naufal Zuhair (2042231005)
3. Daffa Naufal Wahyuaji (2042231081)
4. Ahmad Radhy (Supervisor)
# Komponen Utama
1. Lidar Velodyne vlp-16 (Sensor LIDAR mengukur jarak ke suatu objek)
2. Motor Servo (Menggerakkan shield dengan putaran sudut)
3. Shield / Tameng (Guna Menutup Drone jika api menyambar)
# Cara Kerja Sistem
1. Sensor LIDAR mengukur jarak objek di depan dan mengirim data via UART ke STM32.
2. STM32 menerima data (contoh: DIST:7.5) dan mengubahnya menjadi angka jarak (dalam meter).
3. Berdasarkan jarak tersebut:
  -Jika objek ≤ 5 meter → shield ditutup (servo ke 90°).
  -Jika objek > 5 meter tapi ≤ 10 meter → shield dibuka (servo ke 0°).
  -Jika objek > 10 meter → shield tetap terbuka.
4. Servo motor digerakkan dengan PWM sesuai sudut yang dibutuhkan.
5. Proses ini berulang terus-menerus secara real-time.
# Ringkasan Alur Sistem
```
[LIDAR] --(data jarak via UART)--> [STM32]
     |
     |--> [Parse data] --> [Cek kondisi]
                          |
                          |--> [Gerakkan Servo (Tutup/Buka Shield)]
