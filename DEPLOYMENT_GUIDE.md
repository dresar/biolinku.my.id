# Panduan Deployment Bio Link ke cPanel

## Persiapan File untuk Upload

### 1. File yang Diperlukan
- Semua file aplikasi Django
- File `passenger_wsgi.py` (sudah dikonfigurasi)
- File `.env` (sudah dikonfigurasi untuk production)
- Database `db.sqlite3`
- Folder `media/` dengan semua konten
- Folder `staticfiles/` (hasil dari collectstatic)

### 2. Konfigurasi yang Sudah Disiapkan

#### Settings Production:
- `DEBUG = False`
- `ALLOWED_HOSTS` sudah diset untuk `biolinkku.my.id`
- Static files dikonfigurasi dengan WhiteNoise
- Custom error handlers 404 dan 500
- Security settings untuk HTTPS

#### File Favicon:
- SVG favicon baru sudah dibuat di `static/favicon.svg`
- Design modern dengan tema bio link

## Langkah Deployment di cPanel

### 1. Upload File
1. Compress semua file aplikasi ke dalam ZIP
2. Upload ke folder `public_html` di cPanel
3. Extract file di cPanel File Manager

### 2. Struktur Folder di cPanel
```
public_html/
├── passenger_wsgi.py
├── manage.py
├── db.sqlite3
├── .env
├── biolink/
├── core/
├── media/
├── staticfiles/
├── static/
└── requirements.txt
```

### 3. Konfigurasi Python di cPanel
1. Buka "Python App" di cPanel
2. Create New App:
   - Python Version: 3.8+ (sesuai yang tersedia)
   - Application Root: `/public_html`
   - Application URL: `/` (untuk root domain)
   - Application Startup File: `passenger_wsgi.py`

### 4. Install Dependencies
1. Masuk ke Python App yang sudah dibuat
2. Buka Terminal atau gunakan pip install:
   ```
   pip install Django>=5.0.2
   pip install whitenoise>=6.0.0
   pip install Pillow>=10.0.0
   pip install python-dotenv>=1.0.0
   ```

### 5. Konfigurasi Domain
1. Pastikan domain `biolinkku.my.id` sudah pointing ke hosting
2. Jika menggunakan subdomain, buat subdomain di cPanel
3. Set Document Root ke `/public_html`

### 6. Pengaturan File Permissions
- Set permission 755 untuk folder
- Set permission 644 untuk file
- Set permission 600 untuk file `.env`

### 7. Testing
1. Akses `http://biolinkku.my.id`
2. Test halaman admin: `http://biolinkku.my.id/admin/login/`
3. Test error pages: `http://biolinkku.my.id/404-test`

## Catatan Penting

### Database
- Menggunakan SQLite (tidak perlu setup database terpisah)
- File `db.sqlite3` sudah berisi data yang ada
- Backup database secara berkala

### Static Files
- WhiteNoise menangani static files di production
- Tidak perlu konfigurasi web server tambahan
- File favicon SVG sudah siap

### Security
- SSL/HTTPS akan dihandle oleh cPanel/hosting
- Security headers sudah dikonfigurasi
- CSRF protection aktif

### Error Handling
- Custom 404 dan 500 pages sudah siap
- Error logging akan tersimpan di log cPanel

## Troubleshooting

### Jika Ada Error 500:
1. Cek error log di cPanel
2. Pastikan semua dependencies terinstall
3. Cek permission file dan folder
4. Pastikan `passenger_wsgi.py` dapat diakses

### Jika Static Files Tidak Muncul:
1. Pastikan folder `staticfiles/` sudah terupload
2. Cek setting `STATIC_ROOT` dan `STATIC_URL`
3. Jalankan `python manage.py collectstatic` jika diperlukan

### Jika Media Files Tidak Muncul:
1. Pastikan folder `media/` sudah terupload
2. Cek permission folder media
3. Pastikan setting `MEDIA_ROOT` dan `MEDIA_URL` benar

## Maintenance

### Update Aplikasi:
1. Backup database dan media files
2. Upload file baru
3. Restart Python App di cPanel

### Backup:
- Backup file `db.sqlite3` secara berkala
- Backup folder `media/` 
- Backup file `.env`

Aplikasi sudah siap untuk production deployment di `http://biolinkku.my.id/`