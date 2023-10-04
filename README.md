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
from main.models import Item
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

![image](https://github.com/marsyarahmadani/Marsy-Apparel/assets/116958619/b4c6e29b-e007-4afd-a28a-d945ce33bc67)
![image](https://github.com/marsyarahmadani/Marsy-Apparel/assets/116958619/8aac1622-396f-41eb-8b76-0be0ed5d3958)
![image](https://github.com/marsyarahmadani/Marsy-Apparel/assets/116958619/07a75b13-6f63-4011-83bd-151ea430590b)
![image](https://github.com/marsyarahmadani/Marsy-Apparel/assets/116958619/6b0aabdb-fac0-416f-ad88-b50930f18956)
![image](https://github.com/marsyarahmadani/Marsy-Apparel/assets/116958619/748d3739-3eab-4116-b108-34023a4b4e64)


#
# TUGAS 4 SECTION

### Apa itu Django `UserCreationForm`, dan jelaskan apa kelebihan dan kekurangannya?
`UserCreationForm` merupakan impor formulir yang disediakan oleh `django` yang memudahkan proses pembuatan formulir pendaftaran pengguna dalam aplikasi web. Formulir ini berfungsi bagi pengguna baru untuk registrasi dengan mudah di website dengan menyimpan nama pengguna (username), kata sandi (password), dan konfirmasi kata sandi. 
**Kelebihan :**
 - Dengan menggunakan `UserCreationForm`, pengguna bisa melakukan registrasi dengan lebih mudah.
 - Cepat untuk diterapkan ke dalam proyek django manapun karena hanya perlu melakukan pemanggilan dan mudah diimplementasikan.
 - `UserCreationForm` cocok digunakan bila akan menggunakan model bawaan `user` dari `django`.

**Kekurangan :**
 - `UserCreationForm` memiliki batasan dalam kustomisasi, sehingga lebih sulit untuk mengubah dan memodifikasinya sesuai kebutuhan. 
 - `UserCreationForm` sangat bergantung dengan model user bawaan, hanya bisa melakukan registrasi sederhana seperti meminta data Username, dan Password. Untuk hal lebih dari itu perlu membuat form kustom sendiri.
 - Bentuk tampilan desainnya akan selalu sama, sehingga penggunaan `UserCreationForm` bisa saja tidak cocok digunakan dengen tema desain yang ada pada website. 

### Apa perbedaan antara autentikasi dan otorisasi dalam konteks Django, dan mengapa keduanya penting?

**Autentikasi :** Proses verifikasi identitas pengguna yang mencoba mengakses suatu sistem atau aplikasi. Proses ini dilakukan dengan mencocokkan kebenaran data yang tersimpan dengan input username dan kata sandi atau data biometrik lainnya seperti sidik jari dan face recognition.

**Otorisasi :** Proses yang berjalan setelah proses autentikasi untuk memberi batasan apa saja yang diizinkan atau tidak diizinkan dilakukan oleh pengguna yang telah di verifikasi.

**Autentikasi dan Otorisasi** penting karena keduanya melindungi data sensitif dari akses yang tidak sah. Keduanya dapat membatasi hanya orang yang sah dapat mengakses informasi atau suberdaya tertentu yang sesuai dengan peran atau hak yang mereka miliki. 

### Apa itu cookies dalam konteks aplikasi web, dan bagaimana Django menggunakan cookies untuk mengelola data sesi pengguna?

Cookies adalah sebagian dari data yang disimpan pada perangkat pengguna pada web browser saat berinteraksi dalam sebuah website. Data yang disimpan oleh cookies disimpan pada sisi klien/pengguna. Cookies sering digunakan untuk menyimpan data autentikasi saat mengidentifikasi pengguna, pelackan aktifitas dan penyimpanan preferensi (bahasa atau tema) pengguna.

`Django` menggunakan cookies untuk mengelola data pengguna dengan membuat sebuah ID sesi unik khusus pengguna tersebut. Kemudian ID sesi tersebut dikirim ke perangkat pengguna dan disimpan dalam bentuk cookie di browser mereka. ID sesi tersebut akan menjadi kunci untuk melakukan penyimpanan, penyediaan dan manipulasi data. Artinya setiap kali pengguna masuk ke aplikasi, maka aplikasi web akan selalu mempertahankan keadaan (state) dan konteks dari permintaan HTTP setiap login, sehingga memberikan kesan personal untuk masing-masing pengguna.

### Apakah penggunaan cookies aman secara default dalam pengembangan web, atau apakah ada risiko potensial yang harus diwaspadai?
Cookies dapat aman digunakan dalam penggembangan web jika dilakukan dengan benar dan memperhatikan risiko-risiko potensial yang harus diwaspadai, beberapa diantaranya yaitu :
 - Kebocoran data. Sebagai antisipasi bila terjadi kebocoran data, pengguna tidak boleh menyimpan data sensitif seperti kata sand atau informasi kartu kredit dalam cookies.
 - Cross-Site Scripting (XSS). Serangkaian script jahat yang dapat dimasukkan ke halaman web dan mencuri cookies pengguna, sehingga mereka dapat mengakses situs sebagai pengguna tersebut. 
 - Penyusupan data. Cookies yang tidak memiliki atribut keamanan (seperti 'HttpOnly') bisa diakses oleh JavaScript di halaman yang sama untuk mencuri data cookies pengguna.

###  Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step (bukan hanya sekadar mengikuti tutorial).

**1. Mengimplementasikan fungsi registrasi, login, dan logout untuk memungkinkan pengguna untuk mengakses aplikasi sebelumnya dengan lancar.**

Untuk mengimplementasikan fungsi-fungsi diatas, pertama jalankan _Virtual environment_ terlebih dahulu, kemudian menambahkan beberapa import pada `views.py` yang ada pada folder `main`:
```
from django.shortcuts import redirect
from django.contrib.auth.forms import UserCreationForm
from django.contrib import messages 
from django.contrib.auth import authenticate, login, logout
```
Seperti yang dijelaskan pada soal sebelumnya, `UserCreationForm` berfungsi untuk memudahkan pembuatan formulir registrasi.

Kemudian pada `views.py` tambahkan fungsi register berikut ini:
```
def register(request):
    form = UserCreationForm()

    if request.method == "POST":
        form = UserCreationForm(request.POST)
        if form.is_valid():
            form.save()
            messages.success(request, 'Your account has been successfully created!')
            return redirect('main:login')
    context = {'form':form}
    return render(request, 'register.html', context)
```
untuk fungsi login tambahkan fungsi berikut:
```
def login_user(request):
    if request.method == 'POST':
        username = request.POST.get('username')
        password = request.POST.get('password')
        user = authenticate(request, username=username, password=password)
        if user is not None:
            login(request, user)
            return redirect('main:show_main')
        else:
            messages.info(request, 'Sorry, incorrect username or password. Please try again.')
    context = {}
    return render(request, 'login.html', context)
```
Kemudian untuk fungsi logout tambahkan fungsi berikut:

```
def logout_user(request):
    logout(request)
    return redirect('main:login')
```

Selanjutnya akan dibuat file HTML baru pada `main/templates` yang bernama `register.html` dengan isi berikut:
```
{% extends 'base.html' %}

{% block meta %}
    <title>Register</title>
{% endblock meta %}

{% block content %}  

<div class = "login">
    
    <h1>Register</h1>  

        <form method="POST" >  
            {% csrf_token %}  
            <table>  
                {{ form.as_table }}  
                <tr>  
                    <td></td>
                    <td><input type="submit" name="submit" value="Daftar"/></td>  
                </tr>  
            </table>  
        </form>

    {% if messages %}  
        <ul>   
            {% for message in messages %}  
                <li>{{ message }}</li>  
                {% endfor %}  
        </ul>   
    {% endif %}

</div>  

{% endblock content %}
```

Kemudian untuk disambungkan dengan fungsi login, buat file HTML baru pada `main/templates` yang bernama `login.html` dengan isi berikut:

```
{% extends 'base.html' %}

{% block meta %}
    <title>Login</title>
{% endblock meta %}

{% block content %}

<div class = "login">

    <h1>Login</h1>

    <form method="POST" action="">
        {% csrf_token %}
        <table>
            <tr>
                <td>Username: </td>
                <td><input type="text" name="username" placeholder="Username" class="form-control"></td>
            </tr>
                    
            <tr>
                <td>Password: </td>
                <td><input type="password" name="password" placeholder="Password" class="form-control"></td>
            </tr>

            <tr>
                <td></td>
                <td><input class="btn login_btn" type="submit" value="Login"></td>
            </tr>
        </table>
    </form>

    {% if messages %}
        <ul>
            {% for message in messages %}
                <li>{{ message }}</li>
            {% endfor %}
        </ul>
    {% endif %}     
        
    Don't have an account yet? <a href="{% url 'main:register' %}">Register Now</a>

</div>

{% endblock content %}
```
Kemudian agar bisa disambungkan dengan fungsi logout, pada file `main.html` di folder yang sama, tambahkan kodr berikut setelah _hyperling tag_ untuk _Add New Product_
```
<a href="{% url 'main:logout' %}">
    <button>
        Logout
    </button>
</a>
```

Kemudian pada `urls.py` tambahkan impor berikut :
```
from main.views import register, login_user, logout_user
```
dan tambahkan _path url_ berikut ini pada `urlpatterns`:
```
path('register/', register, name='register'),
path('login/', login_user, name='login'),
path('logout/', logout_user, name='logout'),
```
Selanjutnya agar registrasi, login dan logout dapat digunakan untuk membatasi akses data pribadi, maka akan dilakukan hal berikut.

Pertama, pada `views.py` di folder `main`, tambahkan import berikut:
```
from django.contrib.auth.decorators import login_required
```

Lalu tambahkan kode `@login_required(login_url='/login')` sebelum fungsi `show_main`, seperti berikut:
```
...
@login_required(login_url='/login')
def show_main(request):
...
```
Setelah melakukan semua diatas, maka kini fungsi registrasi, login dan logout dapat diakses oleh pengguna dan data akan dibatasi hanya pengguna yang sudah login dapat melihat data mereka. 


**2. Menampilkan detail informasi pengguna yang sedang logged in seperti username dan menerapkan cookies seperti last login pada halaman utama aplikasi.**

Agar cookies menambahkan last login pada halaman main, pada `views.py` di folder `main`, import `datetime`. Kemudian pada fungsi `login_user` tambahkan cookie baru dengan mengganti kode pada `if user not none` menjadi berikut ini:
```
if user is not None:
    login(request, user)
    response = HttpResponseRedirect(reverse("main:show_main")) 
    response.set_cookie('last_login', str(datetime.datetime.now()))
    return response
```
Kemudian pada fungsi `show_main`, tambahkan `'last_login': request.COOKIES.get()'last_login')` ke dalam variabel `context`.

Selanjutnya modifikasi fungsi `logout_user` dengan kode `response.delete_cookie('last_login')` yang berfungsi untuk menghapus cookie pada `last_login` saat dilakukan proses `logout`.

Untuk menampilkan data _last login_ tambahkan kode berikut diantara tabel dann tombol logout pada `main.html`:
```
<h5>Sesi terakhir login: {{ last_login }}</h5>
```


**3. Menghubungkan model Item dengan User.**

Yang pertama dilakukan untuk menghubungkan `Item` dengan `User` adalah mengimport user pada `model.py` dengan baris kode berikut:
```
from django.contrib.auth.models import User
```
Kemudian pada model `Item`, tambahkan kode `user = models.ForeignKey(User, on_delete=models.CASCADE)` pada baris pertama setelah inisiasi class.

Kemudian ubah fungsi `show_main` dan `create_product` pada `views.py` di `main` dengan kode berikut:
```
def show_main(request):
    products = Item.objects.filter(user=request.user)

    context = {
        'name': request.user.username,
        'class': 'PBP E', 
        'products': products,
        'last_login': request.COOKIES.get('last_login'),

    }

    return render(request, "main.html", context)

def create_product(request):
    form = ProductForm(request.POST or None)

    if form.is_valid() and request.method == "POST":
        product = form.save(commit=False)
        product.user = request.user
        product.save()
        return HttpResponseRedirect(reverse('main:show_main'))
    context = {'form': form}
    return render(request, "create_product.html", context)

```
Jangan lupa untuk melakukan migrasi model dengan `python manage.py makemigrations` agar semua perubahan tersimpan.
Kemudian akan ada error yang mucul. Pilih `1` lalu ketik `1` lagi.

<<<<<<< HEAD
*Tambahan Bonus: membuat button add, remove dan delete*

Untuk membuat fungsi menghapus saya menambah fungsi `delete_product` pada views dengan rincian seperti berikut (dan saya mengimport get_object_or_404):
```
def delete_product(request, product_id):
    product = get_object_or_404(Item, pk=product_id)
    
    # Pastikan hanya pemilik produk yang dapat menghapusnya
    if product.user == request.user:
        product.delete()
    
    return HttpResponseRedirect(reverse('main:show_main'))

```
Untuk fungsi menambah produk saya membuat fungsi `increment_product` dengan rincian sebagai berikut:
```
def increment_product(request, product_id):
    product = get_object_or_404(Item, pk=product_id)
    
    # Pastikan hanya pemilik produk yang dapat mengubah jumlahnya
    if product.user == request.user:
        product.amount += 1
        product.save()
    
    return HttpResponseRedirect(reverse('main:show_main'))
```
Untuk fungsi menambah produk saya membuat fungsi `decrement_product` dengan rincian sebagai berikut:

```
def decrement_product(request, product_id):
    product = get_object_or_404(Item, pk=product_id)
    
    if product.user == request.user:
        if product.amount > 1:
            product.amount -= 1
            product.save()
    
    return HttpResponseRedirect(reverse('main:show_main'))

```
Setelah membuat fungsi2 tersebut, jangan lupa untuk tambahkan path pada `urls.py` dengan mengimport nama2 fungsi tersebut dan memasukkan path seperti berikut:
```    
path('delete-product/<int:product_id>/', delete_product, name='delete_product'),
    path('increment-product/<int:product_id>/', increment_product, name='increment_product'),
    path('decrement-product/<int:product_id>/', decrement_product, name='decrement_product'),
```
Kemudian beri adjustment pada `main.html` agar bisa menerapkan fungsi2 tersebut pad button, sehingga ketika diklik, proses fungsi dipanggil dan akan melakukan proses yang diminta.


*Tambahan modifikasi pada bentuk tampilan HTML*
=======
**Tambahan modifikasi pada bentuk tampilan HTML**

Saya menambahkan beberapa modifikasi pada tampilah main.html saya agar tampilan website lebih enak dibaca. Beberapa hal yang saya tambahkan adalah : memberikan style pada tabel, meng-set semua objek agar align ditengah.


**4. Membuat dua akun pengguna dengan masing-masing tiga dummy data menggunakan model yang telah dibuat pada aplikasi sebelumnya untuk setiap akun di lokal.**

Sebagai percobaan, untuk membuat dua akun, maka harus melakukan tahapan registrasi dua kali dengan username dan password yang berbeda. Lalu ditambahkan 3 data dummy pada setiap akun.




#
# TUGAS 5 SECTION

###  Jelaskan manfaat dari setiap element selector dan kapan waktu yang tepat untuk menggunakannya.

1. ID Selector:
- Menggunakan ID dari elemen HTML
- Setiap ID yang dipilih harus unik
- Bermanfaat ketika ingin mengganti satu elemen pada webpage
contoh: #colorBox {background-color: white;}

2. Class Selector:
- Memanggil elemen yang beradai di class tertentu.
- Class tidak harus unik, sehingga Class Selector dapat digunakan berkali-kali
- Bermanfaat ketika ingin mengganti beberapa elemen sekaligus
contoh: .logo{ font-size: 25px; }

3. Element Selector:
- Selector memilih dengan memanggil suatu elemen langsung dengan namanya.
- ELement Selector bermanfaat ketika ingin mengubah seluruh style yang ada pada suatu webpage menjadi satu style yang seragam.
contoh: a { color: #313131; }

4. Pseudo-element Selector:
- Selector memilih dengan memberi style pada bagian dari elemen.
- Bermanfaat ketika ingin menerapkan style pada suatu bagian tertentu dari elemen.
contoh: button::before{ content: "-->"}

5. Pseudo-class Selector:
- Selector memilih elemen berdasarkan state tertentu dari class
- Bermanfaat ketika ingin mengganti suatu state dari class ketika diberi action tertentu.
contoh: a:hover { text-decoration = underline; }

6. Combinator selection:
- Selector memilih elemen bedasarkan keterhubungannya dengan elemen lain.
- Bermanfaat ketika ingin memberi style pada elemen yang memiliki suatu keterhubungan dengan elemen lainnya.
contoh: ul li {float: left;}

7. Attribute Selector:
- Selector memilih elemen berdasarkan atribut.
- Bermanfaat digunakan ketika ingin menggambarkan elemen bedasar suatu atribut tertentu.
contoh: a[target="_blank"]{ color: blue;}


### Jelaskan HTML5 Tag yang kamu ketahui.
- `<html>` = Untuk mendefinisikan akar file
- `<head>` = Untuk menyimpan informasi file
- `<body>` = Untuk menyimpan isi tubuh file
- `<table>, <tr>, <td>` = Untuk meninisiasikan bentuk tabel 
- `<img>` = Untuk menampilkan gambar berdasarkan path source yang dimasukkan
- `<p>` = Untuk menginisiasikan paragraf
- `<a>` = Untuk mendefinisikan hyperlink
- `<div>` = Untuk mendefinisikan suatu bagian dalam dokumen
- `<button>` = Untuk menggambarkan tombol yang bisa diklik
- `<input>` = Untuk menggambarkan space yang bisa dijadikan input bagi pengguna
- `<form>` = Untuk mendefinisikan formulir HTML 
- `<nav>`  = Untuk menggambarkan bagian menu navigasi
- `<section>` = Untuk mengelompokkan konten independen yang bisa berdiri sendiri.

### Jelaskan perbedaan antara margin dan padding.
- **Margin** : Margin adalah ruang di sekitar elemen yang berada di luar border elemen. Sehingga bisa dipakai untuk mengatur jarak antar elemen. Margin tidak memiliki latar belakang (transparan). 

- **Padding** : Padding adalah ruang di dalam border elemen. Sehingga bisa dipakai untuk mengatur jarak antar konten yang berada di dalam elemen. Berbeda dengan margin, padding memilki latar belakang yang bisa diisi warna.

### Jelaskan perbedaan antara framework CSS Tailwind dan Bootstrap. Kapan sebaiknya kita menggunakan Bootstrap daripada Tailwind, dan sebaliknya?
1. **Tailwaind CSS** : 
    - Dengan menggunakan Tailwand CSS, dapat dibangun komponen yang menggabungkan Class-class kecil yang mengatur properti seperti ukuran, warna dan margin.
    - Framework ini lebih fleksibel karena dapat menyeusaikan dengan mandiri desain yang dibuat.
    - Framework ini cocok digunakan ketika ingin memiliik kontrol lebih besar atas desain agar mencapai sebuah tampilan yang sangat unik.
    - Tailwand CSS juga cocok ketika ingin menghindari penulisan CSS yang rumit. 
    
2. **Bootstrap** :
    - Bootstrap lebih dekat dengan kerangka kerja CSS yang lebih tradisional dengan menggunakan komponen-konponen siap pakai yang memiliki desain bawaan.
    - Jika dibandingkan dengan framework Tailwand CSS, Bootstrap kurang fleksibel karena tidak memerlukan penyesuaian desain. 
    - Framework ini cocok digunakan jika kita menyukai desain bawaan Bootstrap dan ingin melakukan desain secara cepat.
    - Framework ini juga lebih cocok digunakan bagi programmer yang kurang berpengalaman dalam CSS.


### Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step (bukan hanya sekadar mengikuti tutorial).
