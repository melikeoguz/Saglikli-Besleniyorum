## Staj Günlükleri

<h5><ins>1. Gün (04.08.1998)</ins></h5>


<h2>E-Ticaret Sitesi Projesi</h2>
<ul>

<li>https://www.udemy.com/course/laravel-ile-sifirdan-eticaret-projesi/learn/lecture/8012488#overview  ile laravel eğitimine katıldım</li>
<li>XAMPP ve composer kurulumunu gerçekleştirdim </li>
<li>Daha sonra composer global require laravel/installer komutu ile gerekli laravel belgelerini ekledim</li>
<li>laravel new porje_adi şeklinde bir proje oluşturdum</li>
<li>composer create-project --prefer-dist laravel/laravel Project "5.6.*"</li>
<li>cd Project diyip oluşturduğumuz Proje isimli dosyaya girdikten sonra <b>php artisan serve</b> yazıp bağlantı bilgilerini alıyoruz</li>
<li>Artık projenize giriş yapmak istediğinizde bu bağlantı bilgisini kullanmanız gerekmektedir.</li>
<li>https://getcomposer.org/download/ adresine giderek composer seçimi yapıldı</li>
<li>https://laravel.com/docs/7.x buradaki komutlar kullanıldı</li>
<li>Kodlarımı çalıştırma ortamı olarak <b>Php storm</b> kullandım. Kurulumu yapabilmek için burdaki internet adresine tıkladım ve gerekli kurulumları gerçekleştirdim <i>https://www.jetbrains.com/phpstorm/download/#section=windows</i></li>
<li>Run ettiği yeri değiştirmek için <b>Run > Edit Configuration > + > Php Web Page</b> dedikten sonra server olarak <b>eticaret.test</b> olarak yazdım ve port ayarlamasını da 8085 olarak güncelledim</li>
<li>Projelerin neden kullanıldığını 7.video <b>8.01'den</b> öğrenebilirsiniz. (Laravel Proje Yapısı Videosu)</li>

<h4>Framework</h4>

<h4></h4>

<ul>

<li>Vendor altında bulunun tüm dosyalar <b>composer</b> sayesinde yüklenmektedir.</li>
<li>En önemli dosyası <code>.env</code></li>
<li>Php kodunu daha rahat geliştirebilmek için https://github.com/barryvdh/laravel-ide-helper sitesindeki zipi kullanabiliriz.</li>

</ul>

<h6>! Çok Önemli Bir Uyarı</h6>

http://eticaret.test:8085

şeklinde çalışması için port ayarlarını 8085 olarak tanımlamanız gerekmektedir.

</ul>


<h3>Proje Yapısında Bulunması Gerekenler</h3>

<li>Kategori</li>
<li>Ürün</li>
<li>Kullanıcı</li>
<li>Sepet</li>
<li>Ödeme</li>
<li>Sipariş</li>

gibi bölümlerin bulunması gerekmektedir. Ayrıca <code>Yönetici Arayüzü</code> ve <code>Kullanıcı Arayüzü</code> bulunması gerekmektedir.

<h4>Route Yapısı</h4>

Route::get('/', function () {
    return view('welcome');
});

<code>get :</code> İstek metodur. Patch,post,put.. gibi birçok metod bulunmaktadır.</br>
<code>'/' :</code>....</br>
<code>function(){} :</code> İstediğimiz metodun yazıldığı ve çıktısının girildiği kısımdır

<h4>Route ile Metinsel Değer Döndürme</h4>

Route mantığı ise sizin sitenizde bulunan sayfalar arasındaki yönlendirmeyi sağlamaktır. Bunun için <b>Project</b> kısmında yer alan <b>routes</b> dosyasına tıklayınız. Daha sonra <code>web.php</code> dosyasını açıp içerisine bir Route fonksiyonu yazınız.

	 Route::get('/about', function(){
     return ""Burası About Sayfasıdır
     });
şeklinde bir kısım yazarsanız aşağıdaki gibi bir görünüm elde etmiş olursunuz.

![](/images/route-metinsel-dondurme.jpg)
