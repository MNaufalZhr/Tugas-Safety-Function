# RailSight : Drone Technology for Obstacle Avoidance, Collision, Detection, and Smart Brake Management in Modern Tranin Systems
Proyek ini bertujuan untuk meningkatkan keamanan dan efisiensi kereta modern. Drone yang dikembangkan memiliki kemampuan membawa air dalam bentuk gelembung (bubble) untuk memadamkan api apabila terjadi kecelakaan pada kereta. Selain itu, drone dilengkapi dengan sistem keamanan berupa perisai (shield) yang akan aktif secara otomatis ketika api terdeteksi dalam jarak 5 meter. Setelah drone menjauh dan mencapai jarak aman, yaitu 10 meter, perisai akan kembali terbuka secara otomatis.
# Authors
1. Ahmad Rafli Al Adzani (2042231001)
2. Muhammad Naufal Zuhair (2042231005)
3. Daffa Naufal Wahyuaji (2042231081)
4. Ahmad Radhy (Supervisor)
# Komponen Utama
1. Lidar Velodyne vlp-16 (Sensor LIDAR mengukur jarak ke suatu objek)
2. Motor Servo (Menggerakkan shield dengan putaran sudut)
3. Shield / Tameng (Guna Menutup Drone jika api menyambar)
4. Kamera RGB – untuk dokumentasi visual dan pemantauan kondisi area.
5. Sensor suhu / thermal camera (contoh: FLIR Lepton) – untuk mendeteksi overheat atau anomali termal.
6. Sensor gas/asap (contoh: MQ-135) – untuk mendeteksi adanya kebocoran gas atau asap di area sensitif.
7. IMU (Inertial Measurement Unit) – untuk stabilisasi dan pengukuran gerakan drone.
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
**# FlowChart Railsight**

+---------------------------+
|           Start           |
+---------------------------+
             |
             v
+---------------------------+
|  Deteksi Kecelakaan Kereta |
+---------------------------+
             |
             v
+---------------------------+
|      Aktifkan Drone       |
+---------------------------+
             |
             v
+---------------------------+
| Bawa Air dalam Gelembung |
+---------------------------+
             |
             v
+---------------------------+
|     Deteksi Jarak Api     |
+---------------------------+
             |
             v
+-------------------------------+
| Api dalam Jarak ≤ 5 Meter?   |
+-------------------------------+
         |               |
        Ya              Tidak
         |               |
         v               v
+----------------+   +------------------------+
| Aktifkan Shield|   | Shield Tetap Terbuka  |
+----------------+   +------------------------+
         \               /
          \             /
           v           v
+-------------------------------+
|     Api Sudah Padam?         |
+-------------------------------+
         |               |
        Ya              Tidak
         |               |
         v               v
+------------------+  +----------------------+
| Kembali ke Basis |  | Lanjutkan Pemadaman |
+------------------+  +----------------------+
         |
         v
+---------------------------+
|            End            |
+---------------------------+
