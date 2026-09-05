# BioLinkKu - Aplikasi Bio Link Modern

## Deskripsi

BioLinkKu adalah aplikasi web Django yang memungkinkan pengguna membuat halaman bio link profesional dengan tampilan modern. Aplikasi ini ideal untuk bisnis, influencer, atau siapa saja yang ingin menampilkan layanan, produk, dan media sosial mereka dalam satu halaman yang menarik.

## Fitur Utama

- **Profil Pengguna**: Tampilkan foto, nama, jabatan, dan deskripsi
- **Layanan**: Tampilkan layanan dengan ikon, deskripsi, dan tautan
- **Produk**: Katalog produk dengan gambar, harga, dan diskon
- **Media Sosial**: Integrasi dengan berbagai platform media sosial
- **Template WhatsApp**: Template pesan WhatsApp siap pakai untuk berbagai keperluan
- **Kustomisasi Tampilan**: Warna, gradien, dan pengaturan visual lainnya
- **Responsif**: Tampilan yang optimal di semua perangkat (desktop, tablet, mobile)

## Persyaratan Sistem

- Python 3.8 atau lebih tinggi
- Django 5.0 atau lebih tinggi
- Pillow (untuk pemrosesan gambar)
- WhiteNoise (untuk penanganan file statis)
- Python-dotenv (untuk variabel lingkungan)

## Panduan Instalasi

### 1. Persiapan Lingkungan

```bash
# Clone repositori (jika menggunakan Git)
# git clone [URL_REPOSITORI]

# Buat virtual environment
python -m venv venv

# Aktifkan virtual environment
# Windows
venv\Scripts\activate
# Linux/Mac
source venv/bin/activate

# Install dependensi
pip install -r requirements.txt
```

### 2. Konfigurasi Aplikasi

1. Buat file `.env` di direktori root dengan konten berikut:

```
SECRET_KEY=buat-kunci-rahasia-yang-kuat-disini
DEBUG=True
```

2. Jalankan migrasi database:

```bash
python manage.py migrate
```

3. Buat superuser (admin):

```bash
python manage.py createsuperuser
```

4. Kumpulkan file statis:

```bash
python manage.py collectstatic
```

### 3. Menjalankan Aplikasi

```bash
python manage.py runserver
```

Akses aplikasi di browser: http://127.0.0.1:8000/

Akses panel admin: http://127.0.0.1:8000/admin/

## Panduan Penggunaan

### Login Admin

1. Buka http://127.0.0.1:8000/admin/
2. Masukkan username dan password yang dibuat saat `createsuperuser`

### Pengaturan Situs

1. Di panel admin, buka menu "Site Settings"
2. Atur judul situs, deskripsi, logo, dan warna tema
3. Simpan perubahan

### Mengelola Profil

1. Di panel admin, buka menu "User Profiles"
2. Edit profil yang ada atau buat profil baru
3. Isi informasi profil: nama tampilan, jabatan, foto, deskripsi, dan nomor WhatsApp
4. Simpan perubahan

### Menambahkan Layanan

1. Di panel admin, buka menu "Services"
2. Klik "Add Service"
3. Isi informasi layanan:
   - Judul
   - Deskripsi
   - Unggah ikon
   - Tautan (opsional)
   - Pengaturan warna dan gradien
4. Simpan perubahan

### Menambahkan Produk

1. Di panel admin, buka menu "Products"
2. Klik "Add Product"
3. Isi informasi produk:
   - Nama produk
   - Deskripsi
   - Unggah gambar utama
   - Tambahkan gambar tambahan (opsional)
   - Atur harga dan harga diskon (jika ada)
   - Tautan untuk pembelian
4. Simpan perubahan

### Menambahkan Media Sosial

1. Di panel admin, buka menu "Social Media"
2. Klik "Add Social Media"
3. Pilih platform media sosial
4. Masukkan username atau URL lengkap
5. Atur urutan tampilan
6. Simpan perubahan

### Mengelola Template WhatsApp

1. Di panel admin, buka menu "WhatsApp Templates"
2. Klik "Add WhatsApp Template"
3. Isi informasi template:
   - Judul
   - Kategori
   - Isi pesan
   - Deskripsi singkat
4. Simpan perubahan

## Kustomisasi Tampilan

### Warna dan Tema

1. Di panel admin, buka "Site Settings"
2. Atur warna primer dan sekunder
3. Pilih jenis gradien dan arah gradien
4. Simpan perubahan

### Logo dan Favicon

1. Di panel admin, buka "Site Settings"
2. Unggah logo situs
3. Favicon secara otomatis menggunakan file `static/favicon.svg`

## Panduan Deployment ke cPanel

Untuk panduan lengkap deployment ke cPanel, silakan lihat file [DEPLOYMENT_GUIDE.md](DEPLOYMENT_GUIDE.md).

## Penjelasan Kode dan Struktur Proyek

### Struktur Direktori

```
biolink/                # Direktori proyek utama
├── biolink/            # Konfigurasi proyek Django
│   ├── __init__.py
│   ├── asgi.py
│   ├── settings.py     # Pengaturan Django
│   ├── urls.py         # URL router utama
│   └── wsgi.py         # Konfigurasi WSGI
├── core/               # Aplikasi utama
│   ├── __init__.py
│   ├── admin.py        # Konfigurasi admin
│   ├── apps.py
│   ├── forms.py        # Form untuk input data
│   ├── models.py       # Model database
│   ├── urls.py         # URL router aplikasi
│   ├── views.py        # View dan logika aplikasi
│   ├── templates/      # Template HTML
│   └── templatetags/   # Custom template tags
├── media/              # File media yang diunggah
├── static/             # File statis (CSS, JS, gambar)
├── staticfiles/        # File statis yang dikumpulkan
├── manage.py           # Script manajemen Django
├── passenger_wsgi.py   # Konfigurasi untuk deployment
├── requirements.txt    # Dependensi Python
└── .env                # Variabel lingkungan
```

### Penjelasan Kode Utama

#### settings.py

```python
# Konfigurasi dasar Django
SECRET_KEY = os.environ.get('SECRET_KEY', 'django-insecure-key-placeholder')  # Kunci rahasia dari .env
DEBUG = os.environ.get('DEBUG', 'True').lower() == 'true'  # Mode debug dari .env

# Host yang diizinkan
ALLOWED_HOSTS = ['biolinkku.my.id', 'www.biolinkku.my.id', 'localhost', '127.0.0.1', 'testserver']  # Daftar host yang diizinkan

# Aplikasi yang diinstal
INSTALLED_APPS = [
    'django.contrib.auth',  # Autentikasi bawaan Django
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',  # Penanganan file statis
    'django.contrib.humanize',  # Format angka dan tanggal
    'core',  # Aplikasi utama
]

# Middleware
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',  # Keamanan
    'whitenoise.middleware.WhiteNoiseMiddleware',  # Penanganan file statis di production
    # ... middleware lainnya
]

# Database
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',  # Menggunakan SQLite
        'NAME': BASE_DIR / 'db.sqlite3',  # Lokasi file database
    }
}

# Konfigurasi file statis
STATIC_URL = '/static/'  # URL untuk akses file statis
STATIC_ROOT = BASE_DIR / 'staticfiles'  # Direktori untuk collectstatic
STATICFILES_DIRS = [BASE_DIR / 'static']  # Direktori file statis tambahan

# Konfigurasi file media
MEDIA_URL = '/media/'  # URL untuk akses file media
MEDIA_ROOT = BASE_DIR / 'media'  # Direktori penyimpanan file media
```

#### models.py

```python
# Model UserProfile - Profil pengguna
class UserProfile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE, related_name='profile')  # Relasi ke User Django
    display_name = models.CharField(max_length=100)  # Nama yang ditampilkan
    title = models.CharField(max_length=100, blank=True, null=True)  # Jabatan/deskripsi singkat
    photo = models.ImageField(upload_to='profiles/')  # Foto profil
    description = models.TextField(blank=True, null=True)  # Deskripsi lengkap
    whatsapp = models.CharField(max_length=20, blank=True, null=True)  # Nomor WhatsApp
    slug = models.SlugField(max_length=100, unique=True)  # Slug untuk URL
    # ... field lainnya

# Model Service - Layanan yang ditawarkan
class Service(models.Model):
    title = models.CharField(max_length=100)  # Judul layanan
    description = models.TextField()  # Deskripsi layanan
    icon = models.ImageField(upload_to='services/')  # Ikon layanan
    link = models.URLField(blank=True, null=True)  # Link untuk layanan
    color = models.CharField(max_length=50, default='blue')  # Warna utama
    gradient_color = models.CharField(max_length=50, blank=True, null=True)  # Warna gradien
    # ... field lainnya

# Model Product - Produk yang dijual
class Product(models.Model):
    name = models.CharField(max_length=100)  # Nama produk
    description = models.TextField()  # Deskripsi produk
    image = models.ImageField(upload_to='products/')  # Gambar utama produk
    price = models.DecimalField(max_digits=10, decimal_places=2)  # Harga produk
    discount_price = models.DecimalField(max_digits=10, decimal_places=2, blank=True, null=True)  # Harga diskon
    link = models.URLField(blank=True, null=True)  # Link untuk pembelian
    # ... field lainnya

# Model SocialMedia - Media sosial yang ditampilkan
class SocialMedia(models.Model):
    platform = models.CharField(max_length=50)  # Platform media sosial
    username = models.CharField(max_length=100)  # Username
    url = models.URLField()  # URL lengkap
    icon = models.CharField(max_length=50)  # Ikon (dari library ikon)
    # ... field lainnya
```

#### views.py

```python
# View utama - Halaman beranda
def home(request):
    services = Service.objects.filter(is_active=True).order_by('order')  # Ambil layanan aktif
    products = Product.objects.filter(is_active=True).order_by('id')  # Ambil produk aktif
    socials = SocialMedia.objects.filter(is_active=True).order_by('order')  # Ambil media sosial aktif
    site_settings = SiteSettings.objects.first() or SiteSettings.objects.create()  # Ambil pengaturan situs
    whatsapp_templates = WhatsAppTemplate.objects.filter(is_active=True).order_by('order')  # Ambil template WhatsApp
    
    # Siapkan judul halaman
    title = site_settings.site_title or 'Link Bio'
    
    context = {
        'services': services,
        'products': products,
        'socials': socials,
        'site_settings': site_settings,
        'whatsapp_templates': whatsapp_templates,
        'title': title,
    }
    
    return render(request, 'core/user/home.html', context)  # Render template dengan context
```

## Pemecahan Masalah

### Database Tidak Terbaca

**Masalah**: Aplikasi tidak dapat membaca database atau menampilkan error database.

**Solusi**:
1. Pastikan file `db.sqlite3` ada di direktori root
2. Pastikan file memiliki permission yang benar (644)
3. Jalankan migrasi ulang: `python manage.py migrate`

### File Media Tidak Muncul

**Masalah**: Gambar atau file media tidak muncul di halaman web.

**Solusi**:
1. Pastikan folder `media/` ada dan memiliki permission yang benar
2. Periksa URL media di pengaturan Django
3. Pastikan file media telah diunggah dengan benar

### Error Saat Deployment

**Masalah**: Aplikasi error saat di-deploy ke hosting.

**Solusi**:
1. Periksa log error di cPanel
2. Pastikan versi Python di hosting kompatibel
3. Periksa file `passenger_wsgi.py` sudah benar
4. Pastikan semua dependensi terinstal

## Kontak dan Dukungan

Jika Anda memiliki pertanyaan atau membutuhkan bantuan, silakan hubungi:

- Email: support@biolinkku.my.id
- WhatsApp: +628xxxxxxxxxx

## Lisensi

Aplikasi ini dilisensikan untuk penggunaan pribadi dan komersial sesuai dengan ketentuan yang disepakati saat pembelian.

---

© 2024 BioLinkKu. Hak Cipta Dilindungi.