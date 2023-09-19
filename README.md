## Informasi
### Nama  : Marsya Rahmadani
### NPM   : 2206028642
### Kelas : PBP E

#### Link tautan aplikasi Adaptable: https://marsyapparel.adaptable.app/main/

--Dibawah ini akan dipaparkan penjelasan untuk tugas individu 2 dan 3 PBP : --
 
#
# TUGAS 2 SECTION

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



#
# TUGAS 3 SECTION

### 1. Apa perbedaan antara form POST dan form GET dalam Django?

Berikut perbedaan antara form POST dan form GET:
| Metode GET | Metode POST |
| ---------- | ----------- |
| Digunakan untuk mengambil data dari web server| Digunakan untuk mengirim data ke web server|
| Data dikirimkan sebagai bagian dari URL | Data dikirimkan sebagai bagian dari permintaan HTTP, bukan sebagai bagian dari URL |
| Me-return HTTP status code 200 bila sukses mengambil data| Me-return HTTP status code 201 |


### 2. Apa perbedaan utama antara XML, JSON, dan HTML dalam konteks pengiriman data?

Berikut perbedaan antara XML, JSON dan HTML:
| XML | JSON | HTML |
| ---------- | ----------- | ----------- |
| Berdasarkan _markup language_ |  Berbasis notasi objek dalam JavaScript|Berdasarkan _markup language_|
| Digunakan untuk mengirim data | Digunakan untuk mengirim data | Digunakan untuk menampilkan layout depan page|
| Dapat menuliskan comments | Tidak dapat menuliskan comments| Dapat menuliskan comments | 
| Memerlukan tag pembuka dan penutup |Tidak memerlukan tag pembuka dan penutup | Memerlukan tag pembuka dan penutup |
| Tidak mendukung data tipe array| Mendukung data tipe array | Bisa menampilkan data dari sebuah array dengan framework tertentu |


### 3. Mengapa JSON sering digunakan dalam pertukaran data antara aplikasi web modern?

Beberapa keunggulan yang dimiliki JSON untuk pertukaran data antara aplikasi web modern yaitu:

- Mudah dibaca: Format teks JSON sangat ringkas dan mudah dibaca oleh manusia. 
- Pemrosesan yang cepat: JSON dapat melakukan parsing data dari sisi server dengan cepat, sehingga cocok untuk digunakan dalam aplikasi yang membutuhkan pertukaran data cepat.
- Struktur data yang fleksibel: JSON memungkinkan representasi data yang beragam dan kompleks karena mendukung tipe data seperti boolean, string, angka, array dan objek.
- Ringan: Sintaks yang digunakan berukuran lebih kecil dan ringan sehingga meminimalisir latensi.


### 4. Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step (bukan hanya sekadar mengikuti tutorial).

1. Membuat input `form` untuk menambahkan objek model pada app sebelumnya. Untuk mengimplementasikan checklist ini saya membuat terlebih dahulu file html bernama `base.html` sebagai template dasar yang akan digunakan sebagai kerangka umum untuk halaman web. File `base.html` dimasukkan kedalahm folder `templates` pada root folder dan diisi dengan kode berikut ini:

```
{% load static %}
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta
            name="viewport"
            content="width=device-width, initial-scale=1.0"
        />
        {% block meta %}
        {% endblock meta %}
    </head>

    <body>
        {% block content %}
        {% endblock content %}
    </body>
```
Selanjutnya saya menambahkan folder `templates` pada baris `TEMPLATES`  di file `settings.py` yang ada di subdirektori `MarsyApparel` hingga berbentuk seperti berikut:

```
...
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates'], # Tambahkan kode ini
        'APP_DIRS': True,
        ...
    }
]
...
```

Setelah itu saya ubah kode pada file `main.html` yang ada di subdirektori `templates`. Kita akan menjadikan `base.html` sebagai template utama dengan mengedit kode  file `main.html` menjadi seperti berikut: 

```
{% extends 'base.html' %}

{% block content %}
    <h1>Shopping List Page</h1>

    <h5>Name:</h5>
    <p>{{name}}</p>

    <h5>Class:</h5>
    <p>{{class}}</p>
{% endblock content %}
```

Kemudian ubah path server agar dapat dibuka tanpa menuliskan `main/` pada url website. Edit file `urls.py` yang ada pada folder `MarsyApparel` dengan mengubah path `main/` menjadi `''` seperti berikut

```
urlpatterns = [
    path('', include('main.urls')),
    path('admin/', admin.site.urls),
]
```
Hal ini dapat membuat server yang pada awal hanya bisa memberi tampilan dengan url path **https://marsyapparel.adaptable.app/main/** menjadi **https://marsyapparel.adaptable.app/** saja

Selanjutnya untuk membuat form input data kita akan membuat file baru bernama `forms.py` pada direktori `main` dan memasukkan kode berikut:
```
from django.forms import ModelForm
from main.models import Item

class ProductForm(ModelForm):
    class Meta:
        model = Item
        fields = ["name", "amount", "description"]
```

Selanjutnya tambahkan import berikut pada file `views.py` yang ada di direktori `main`
```
from django.http import HttpResponseRedirect
from main.forms import ProductForm
from django.urls import reverse
```
Kemudian tambahkan fungsi `create_product` dan edit fungsi `show_main` seperti berikut ini:
```
def show_main(request):
    products = Item.objects.all()

    context = {
        'name': 'Marsya Rahmadani',
        'class': 'PBP E', 
        'products': products
    }

    return render(request, "main.html", context)

def create_product(request):
    form = ProductForm(request.POST or None)

    if form.is_valid() and request.method == "POST":
        form.save()
        return HttpResponseRedirect(reverse('main:show_main'))

    context = {'form': form}
    return render(request, "create_product.html", context)

```

Fungsi `create_product` akan berfungsi untuk menerima input submisi kemudian menambahkan data produk secara otomatis. Kemudian fungsi `Item.objects.all()` digunakan untuk mengambik semua objek Item yang tersimpan pada database.

Selanjutnya buka file `urls.py` pada `main` untuk mengimport fungsi `create_product` tadi dengan menuliskan `from main.views import show_main, create_product`

Kemudian kita akan menambahkan `create_product` pada path url di `urlpatterns` pada `urls.py` di `main` dengan menambahkan baris berikut:
```
path('create-product', create_product, name='create_product'),
```

Selanjutnya buatlah file HTML baru dengan nama `create_product.html` pada direktori `template` dalam `main` dan isi file tersebut dengan kode berikut:
```
{% extends 'base.html' %} 

{% block content %}
<h1>Add New Product</h1>

<form method="POST">
    {% csrf_token %}
    <table>
        {{ form.as_table }}
        <tr>
            <td></td>
            <td>
                <input type="submit" value="Add Product"/>
            </td>
        </tr>
    </table>
</form>

{% endblock %}
```

Setelah itu pada file `main.html` tambahkan kode berikut dalam batasan `{% block content %}`:

```
. . .
    <table>
        <tr>
            <th>Name</th>
            <th>Amount</th>
            <th>Description</th>

        </tr>

        {% comment %} Berikut cara memperlihatkan data produk di bawah baris ini {% endcomment %}

        {% for product in products %}
            <tr>
                <td>{{product.name}}</td>
                <td>{{product.amount}}</td>
                <td>{{product.description}}</td>

            </tr>
        {% endfor %}
    </table>

<br />

<a href="{% url 'main:create_product' %}">
    <button>
        Add New Product
    </button>
</a>


{% endblock content %}
```

Dengan melakukan langkah-langkah diatas, kini proyek bisa menambahkan data-data produk baru dan ditampilkan secara real time.

2. Tambahkan 5 fungsi `views` untuk melihat objek yang sudah ditambahkan dalam format HTML, XML, JSON, XML by ID, dan JSON by ID. 

Untuk melihat objek dalam format XML, JSON, XML by ID, dan JSON by ID, kita perlu menambahkan import berikut pada file `views.py` di folder `main` 

```
from django.http import HttpResponse
from django.core import serializers

```
Kemudian tambahkan fungsi-fungsi berikut:
```
def show_xml(request):
    data = Item.objects.all()
    return HttpResponse(serializers.serialize("xml", data), content_type="application/xml")

def show_json(request):
    data = Item.objects.all()
    return HttpResponse(serializers.serialize("json", data), content_type="application/json")

def show_xml_by_id(request, id):
    data = Item.objects.filter(pk=id)
    return HttpResponse(serializers.serialize("xml", data), content_type="application/xml")

def show_json_by_id(request, id):
    data = Item.objects.filter(pk=id)
    return HttpResponse(serializers.serialize("json", data), content_type="application/json")
```
Setelah itu pada file `urls.py` import fungsi-tadi dengan menuliskannya seperti berikut:

```
from main.views import show_main, create_product, show_xml, show_json, show_xml_by_id, show_json_by_id 
```
Kemudian tambahkan path berikut ini:
```
urlpatterns = [
    path('', show_main, name='show_main'),
    path('create-product', create_product, name='create_product'),
    path('xml/', show_xml, name='show_xml'), 
    path('json/', show_json, name='show_json'), 
    path('xml/<int:id>/', show_xml_by_id, name='show_xml_by_id'),
    path('json/<int:id>/', show_json_by_id, name='show_json_by_id'), 

]
```

Setelah melakukan langkah-langkah diatas, kini proyek Django dapat dilihat dalam bentuk XML, JSON, XML by ID, dan JSON by ID. Untuk mengetesnya jalankan perintah `python manage.py runserver` dalam `env` kemudian bukalah http://localhost:8000 ,  http://localhost:8000/xml ,  http://localhost:8000/json  

Server akan menampilkan seluruh data produk-produk yang telah ditambahkan , dan bila ingin melihat per id bisa menggunakan path berikut dan masukkan id data produng yang ingin dilihat 
http://localhost:8000/xml/[id] , http://localhost:8000/json/[id]

### Screenshot dari hasil akses URL pada Postman :
