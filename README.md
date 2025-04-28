# RailSight : Drone Technology for Obstacle Avoidance, Collision, Detection, and Smart Brake Management in Modern Tranin Systems
Proyek ini bertujuan untuk meningkatkan keamanan dan efisiensi kereta modern. Drone yang dikembangkan memiliki kemampuan membawa air dalam bentuk gelembung (bubble) untuk memadamkan api apabila terjadi kecelakaan pada kereta. Selain itu, drone dilengkapi dengan sistem keamanan berupa perisai (shield) yang akan aktif secara otomatis ketika api terdeteksi dalam jarak 20 cm dan suhu < 50. Setelah drone menjauh dan mencapai jarak aman, yaitu 20 cm dan suhu > 50, perisai akan kembali terbuka secara otomatis.
# Authors
1. Ahmad Rafli Al Adzani (2042231001)
2. Muhammad Naufal Zuhair (2042231005)
3. Daffa Naufal Wahyuaji (2042231081)
4. Ahmad Radhy (Supervisor)
# Komponen Utama
1. Lidar Velodyne vlp-16 (Sensor LIDAR mengukur jarak ke suatu objek)
2. Motor Servo (Menggerakkan shield dengan putaran sudut)
3. Shield / Tameng (Guna Menutup Drone jika api menyambar)
4. Sensor thermal digunakan untuk mengukur suhu. Jika suhu lebih dari 50°C
5. . Sensor gas/asap (contoh: MQ-135) – untuk mendeteksi adanya kebocoran gas atau asap di area sensitif.
6. . IMU (Inertial Measurement Unit) – untuk stabilisasi dan pengukuran gerakan drone.
# Cara Kerja Sistem
1. Sensor LIDAR mengukur jarak objek di depan dan mengirim data via UART ke STM32.
2. STM32 menerima data (contoh: DIST:7.5) dan mengubahnya menjadi angka jarak (dalam meter).
3. Berdasarkan jarak tersebut:
  -Jika objek ≤ 20 cm dan suhu ≤ 50 → shield ditutup (servo ke 90°).
  -Jika objek > 20 cm dan suhu > 50 → shield tetap terbuka.
4. Servo motor digerakkan dengan PWM sesuai sudut yang dibutuhkan.
5. LED Red > Nyala (bahaya) < Mati (Aman)
7. Proses ini berulang terus-menerus secara real-time.

# Tools
1. STM32CUBE
2. Keil uVison 5
3. MinGW (Testng)

# Hasil Testing
![Screenshot (41)](https://github.com/user-attachments/assets/b1b0a792-df17-4007-9e6d-575d74e30152)

# Ringkasan Alur System

[LIDAR] --(data jarak via UART)--> [STM32]
     |
     |--> [Parse data] --> [Cek kondisi]
                          |
                          |--> [Gerakkan Servo (Tutup/Buka Shield)]
# FlowChart Railsight
![image](https://github.com/user-attachments/assets/4a11fa90-d484-4b43-9592-c8be58419a5f)

```
