### Nama  : Marsya Rahmadani
### NPM   : 2206028642
### Kelas : PBP E

#### Link tautan repositori aplikasi Adaptable: https://marsyapparel.adaptable.app/main/

**(1) Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step (bukan hanya sekadar mengikuti tutorial).**

1. Cheklist pertama yaitu membuat proyek django baru. Untuk melaksanakan perintah ini kita perlu membuat terlebih dahulu repository baru di github dengan bernamakan aplikasi ` Marsy-Apparel `, kemudian membuat direktori lokal yang ditambahkan file requirements.txt yang berisikan dependencies yang perlu diinstal yaitu:

![image](https://github.com/marsyarahmadani/Marsy-Apparel/assets/116958619/c5d99505-51eb-44fa-90be-1bdf63a082c7)

kemudian untuk menginstal dependencies yang ada di requirements.txt dengan terlebih dahulu menjalankan mode virtual environment sebelum melakukan perintah berikut ini:
```
pip install -r requirements.txt
```
lalu untuk membuat proyek Django baru yang sesuai dengan nama aplikasi, lakukan perintah
```
django-admin startproject MarsyApparel .
``` 

selanjutnya tambahkan `*` pada `ALLOWED_HOST` di `settings.py` untuk deployment, sehingga semua host dapat diberi akses.

Setelah itu untuk menjalankan server Django lakukan perintah :
```
python manage.py runserver
```

Selanjutnya mengunggah proyek ke repositori github, namun sebelumnya perlu ditambahkan file `.gitignore` di direktori lokal `MarsyApparel` lalu lakukan `add`, `commit`, dan `push` untuk menyimpan perubahan ke repositori


2. Ceklis kedua yaitu Membuat aplikasi dengan nama `main` pada proyek tersebut. Yang pertama dilakukan adalah menjalankan perintah untuk membuat aplikasi baru bernama main menggunakan perintah:
```
python manage.py startapp main
```
kemudian menambahkan `main` ke dalam proyek dengan menambahkan `main` pada variabel `INSTALLED_APPS` yang ada pada berkas `settings.py`

3. Melakukan routing pada proyek agar dapat menjalankan aplikasi main.Untuk melaksanakan ceklis ini, kita perlu membuat file baru bernama `urls.py` di direktori `main`. Kemudian isi `urls.py` dengan kode berikut ini:
```
from django.urls import path
from main.views import show_main

app_name = 'main'

urlpatterns = [
    path('', show_main, name='show_main'),
]
```
Kemudian pada file lain yaitu file `urls.py` pada direktori `MarsyApparel` impor fungsi `include` kemudian tambahkan rute URL yang memanggil tampilan `main` yang sebelumnya sudah dibuat, sehingga menjadi seperti berikut ini:

![image](https://github.com/marsyarahmadani/Marsy-Apparel/assets/116958619/fc34088a-1fee-4217-af0a-349732c8eb68)

4.Membuat model pada aplikasi main dengan nama Item dan memiliki atribut wajib sebagai berikut.
    - `name` sebagai nama item dengan tipe `CharField`.
    - `amount` sebagai jumlah item dengan tipe `IntegerField`.
    - `description` sebagai deskripsi item dengan tipe `TextField`.
Sehingga isi berkas `models.py` seperti berikut ini:

![image](https://github.com/marsyarahmadani/Marsy-Apparel/assets/116958619/6f38c992-d558-4505-870e-0169322b229f)


5. Ceklis kelima yaitu membuat fungsi pada `views.py` untuk dikembalikan ke dalam sebuah template HTML yang menampilkan nama aplikasi serta nama dan kelas. Untuk ini dapat diimplementasikan template `main.html` dan isi file tersebut seperti berikut:

![image](https://github.com/marsyarahmadani/Marsy-Apparel/assets/116958619/a5182a06-10e5-4b26-ab6b-e7acc8de6e63)



kemudian untuk membuat `views.py ` mengeluarkan tampilan yang sesuai, maka edit pada file `views.py` untuk mengimport :
```
from django.shortcuts import render
```
kemudian tambahkan fungsi berikut dibawah import
```
def show_main(request):
    context = {
        'name': 'Pak Bepe',
        'class': 'PBP A'
    }

    return render(request, "main.html", context)
```

6. Ceklis keenam yaitu membuat sebuah routing pada `urls.py` aplikasi main untuk memetakan fungsi yang telah dibuat pada `views.py`. Langkah pertama adalah membuat berkas `urls.py` di dalam direktori `main`. Lalu isi dengan kode seperti berikut:

![image](https://github.com/marsyarahmadani/Marsy-Apparel/assets/116958619/903f4a19-c170-493e-b73c-1ce832fd61f0)


dan untuk menggabungkan dengan fungsi yang ada di `views.py`, tambahkan pada file `urls.py` pada direktori `MarsyApparel` dengan mengimpor `include` dan menambahkan rute URL baru, sehingga kode menjadi seperti berikut:

![image](https://github.com/marsyarahmadani/Marsy-Apparel/assets/116958619/66e7af81-879d-4de7-9363-d1ac7d10c1d6)


7. Ceklis ketujuh yaitu melakukan deployment ke Adaptable terhadap aplikasi yang sudah dibuat sehingga nantinya dapat diakses oleh teman-temanmu melalui Internet. Setelah membuat akun Adaptable.io menggunakan akun github yang sama dengan akun yang memiliki repositori `Marsy-Apparel` selanjutnya adalah membuat app baru dengan cara:
- tekan `New App` lalu sambungkan dengan cara `Connect an Existing Repository`
- pilih proyek `Marsy-Apparel` lalu pilih `Python App Template`, `PostgreSQL` dan versi python yang sesuai. kemudian masukkan perintah `python manage.py migrate && gunicorn MarsyApparel.wsgi` pada `Start Command`

kemudian deploy applikasi agar apikasi dapat dilihat di internet.


**(2) Buatlah bagan yang berisi request client ke web aplikasi berbasis Django beserta responnya dan jelaskan pada bagan tersebut kaitan antara `urls.py`, `views.py`, `models.py`, dan berkas `html`.**

![image](https://github.com/marsyarahmadani/Marsy-Apparel/assets/116958619/aa8be6e4-bc3a-4d4a-835f-e6433bca76c8)



**(3) Jelaskan mengapa kita menggunakan **virtual environment**? Apakah kita tetap dapat membuat aplikasi web berbasis Django tanpa menggunakan **virtual environment**?**
Virtual environment berguna untuk mengisolasi package dan dependencies dari aplikasi sehingga tidak bertabrakan dengan versi lain yang ada pada komputermu. Kita membutuhkan Virtual Environment untuk menginstal dependencies yang dibutuhkan dalam membuat proyek django maka kemungkinan. Namun kita tetap bisa membuat aplikasi web berbasis django tanpa menggunakan venv, akan tetapi akan ada masalah yang bisa saja terjadi.

**(4) Jelaskan apakah itu MVC, MVT, MVVM dan perbedaan dari ketiganya.**
- _MVC (Model-View-Controller):_   
    Model: Menyimpan data dan logika aplikasi.
    View: Menampilkan data dari model kepada pengguna.
    Controller: Mengontrol aliran data antara kedua Model-View
- _MVT (Model-View-Template):_
    Model: Menyimpan data dan logika aplikasi.
    View: Menampilkan data dari model dan menghubungkannya dengan template.
    Template: Menentukan tampilan antarmuka pengguna.
- _MVVM (Model-View-ViewModel):_
    Model: Menyimpan data dan logika aplikasi.
    View: Menampilkan data dari model kepada pengguna.
    ViewModel: Berisi logika yang memungkinkan tampilan berinteraksi dengan Model tanpa mengetahui rincian internal Model. Ini memungkinkan pengikatan data yang lebih kuat antara Model dan View.
=> perbedaan nya: MVC biasanya digunakan untuk aplikasi berbasis server-side. MVT memisahkan tugas tampilan ke dalam komponen Template yang lebih spesifik. MVVM memberikan lebih banyak pengikatan data dan pemisahan tugas yang lebih kuat antara tampilan dan logika bisnis.
