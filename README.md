# tugas1-dockerize-wordpress
Tugas 1 - Dockerize WordPress dengan MySQL dan Redis
Langkah - Langkah untuk menjalankan stack :
1. Buka Docker Desktop dan pastikan status Docker running
2. Siapkan folder (wordpress-docker) dan pastikan ada file docker-compose.yml di dalamnya
3. Kemudian buka terminal dan jalankan docker compose up -d (untuk menjalankan semua service)
4. Untuk akses wordpress nya melalui http://localhost:8000
5. Lalu lakukan instalasi wp dengan memilih bahasa, nama web, username, dan password
   <img width="1600" height="996" alt="image" src="https://github.com/user-attachments/assets/afbcb9a5-af9a-405c-bab0-e58ebfb3eae2" />

7. Setelah terinstall dan masuk ke dashboard wordpress, lakukan konfigurasi Redis Object Cache dengan cara install plugin nya terlebih dahulu lalu melakukan konfigurasi pada wp-config.php
   define('WP_REDIS_HOST', 'redis');
define('WP_REDIS_PORT', 6379);
<img width="1600" height="999" alt="image" src="https://github.com/user-attachments/assets/3ec84874-31c2-446e-8dbf-acb32978b6f3" />

9. Setelah konfigurasi sesuai, aktifkan pada menu settings lalu klik Enable Object Cache
10. Untuk testing Redis CLI, jalankan docker exec -it wordpress-docker-redis-1 redis-cli ping
11. Outputnya akan keluar "PONG"
12. Lalu untuk testing persistent volume nya jalankan docker compose down pada terminal, untuk mematikan container, dan jalankan kembali docker compose up -d
13. Cek pada http://localhost:8000, jika data wp masih ada, berarti volume berfungsi dengan baik

Screenshots:
1. docker ps
   <img width="1600" height="998" alt="image" src="https://github.com/user-attachments/assets/a410e724-74f8-4350-8266-40d582d1709e" />
2. Redis CLI Ping test
   <img width="1600" height="999" alt="image" src="https://github.com/user-attachments/assets/a36fec49-9b5b-4120-8b9f-84b76a156e55" />

Jawaban pertanyaan:
1. Volume digunakan agar data database MySQL tetap tersimpan walaupun container dihentikan atau direstart. Tanpa volume, data akan hilang ketika container dihapus
2. depends_on digunakan untuk mengatur urutan startup container. WordPress membutuhkan MySQL, sehingga WordPress dijalankan setelah MySQL aktif
3. Wordpress terhubung ke MySQL dengan nama service (mysql) sebagai hostname melalui Docker internal network, bukan menggunakan localhost
4. Redis berfungsi sebagai object cache untuk menyimpan data dan query database di memory, sehingga meningkatkan performa WordPress dan mengurangi beban MySQL
5. 
