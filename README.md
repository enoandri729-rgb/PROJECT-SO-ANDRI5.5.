# PROJECT-SO-ANDRI5.5.

#### Langkah 1: Personalisasi Dasar
1. **Buka CMD**: Tekan `Win + R`, ketik `cmd`, dan tekan Enter.
2. **Ubah Warna ke Hijau Matrix (0A)**:  
   Jalankan perintah berikut di CMD:  
   ```
   color 0A
   ```  
   Ini mengatur latar belakang hitam (0) dan teks hijau terang (A), seperti efek Matrix.
3. **Set Judul Custom**:  
   Jalankan:  
   ```
   title My Command Center
   ```  
   Judul jendela CMD akan berubah menjadi "My Command Center".
4. **Buat Prompt Custom**:  
   Jalankan:  
   ```
   prompt $P$G
   ```  
   Ini mengubah prompt menjadi path direktori saat ini diikuti oleh `>`, misalnya `C:\Users\YourName>`.

#### Langkah 2: Simpan Preferensi dalam Batch File Startup
Untuk membuat pengaturan ini otomatis setiap kali CMD dibuka, buat file batch (.bat) yang berisi perintah di atas. Ini akan berfungsi sebagai "startup script".

1. **Buat File Batch**:  
   Buka Notepad (atau editor teks lain), salin kode berikut, dan simpan sebagai `cmd_startup.bat` di lokasi yang mudah diakses, misalnya `C:\Scripts\cmd_startup.bat`.  
   ```
   @echo off
   color 0A
   title My Command Center
   prompt $P$G
   cls
   echo CMD Personalized! Selamat datang di My Command Center.
   ```  
   - `@echo off`: Menyembunyikan perintah saat dieksekusi.  
   - `cls`: Membersihkan layar setelah pengaturan.  
   - Pesan echo adalah opsional untuk konfirmasi.

2. **Jalankan Batch File**:  
   Klik dua kali file `cmd_startup.bat` untuk menguji. CMD akan terbuka dengan pengaturan yang dipersonalisasi.

3. **Otomatisasi Startup (Opsional)**:  
   Untuk menjalankan ini setiap kali CMD dibuka:  
   - Buka CMD sebagai admin.  
   - Jalankan: `reg add "HKCU\Software\Microsoft\Command Processor" /v AutoRun /t REG_SZ /d "C:\Scripts\cmd_startup.bat" /f`  
     (Ganti path sesuai lokasi file Anda).  
   - Sekarang, setiap kali Anda membuka CMD baru, pengaturan akan diterapkan otomatis. Untuk menghapus, jalankan `reg delete "HKCU\Software\Microsoft\Command Processor" /v AutoRun /f`.

#### Bonus: Menu Interaktif Sederhana dengan Batch Script
Buat menu interaktif yang menawarkan pilihan tools sederhana, seperti membuka aplikasi atau menjalankan perintah. Ini menggunakan loop dan pilihan dalam batch.

1. **Buat File Batch untuk Menu**:  
   Buka Notepad, salin kode berikut, dan simpan sebagai `menu.bat` (di lokasi yang sama dengan `cmd_startup.bat`).  
   ```
   @echo off
   :menu
   cls
   echo ====================================
   echo       My Command Center Menu
   echo ====================================
   echo 1. Buka Notepad
   echo 2. Periksa IP Address
   echo 3. Jalankan Ping ke Google
   echo 4. Keluar
   echo ====================================
   set /p choice="Pilih opsi (1-4): "

   if %choice%==1 (
       start notepad.exe
       goto menu
   ) else if %choice%==2 (
       ipconfig
       pause
       goto menu
   ) else if %choice%==3 (
       ping google.com
       pause
       goto menu
   ) else if %choice%==4 (
       echo Terima kasih! Keluar...
       exit
   ) else (
       echo Pilihan tidak valid. Coba lagi.
       pause
       goto menu
   )
   ```  
   - `:menu` adalah label untuk loop.  
   - `set /p choice` meminta input pengguna.  
   - `if` statements menangani pilihan dan kembali ke menu setelah eksekusi.  
   - `pause` menunggu input sebelum melanjutkan.

2. **Integrasikan dengan Startup**:  
   Tambahkan baris `call menu.bat` di akhir `cmd_startup.bat` untuk menjalankan menu setelah personalisasi.  
   ```
   @echo off
   color 0A
   title My Command Center
   prompt $P$G
   cls
   echo CMD Personalized! Selamat datang di My Command Center.
   call menu.bat
   ```

3. **Jalankan dan Uji**:  
   Jalankan `cmd_startup.bat`. Setelah personalisasi, menu akan muncul. Pilih opsi untuk menguji tools.

Dengan ini, CMD Anda akan terasa lebih personal dan fungsional. Jika ada error atau perlu penyesuaian (misalnya, tools tambahan), beri tahu detail sistem Anda (versi Windows). Pastikan untuk mencadangkan registry sebelum mengubahnya.
