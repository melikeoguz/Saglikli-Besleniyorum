## Staj Günlükleri

<h5><ins>1. Gün (04.08.2020)</ins></h5>


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

<h4>Route ile JSon Formatlı Değer Döndürme</h4>
 
Metinsel bir değer döndürürken hangi dosya üzerinde değişiklik yaptıysak yine o dosya içerisinde yani <code>web.php</code> dosyasının içinde değişiklikler meydana getiriyoruz.

    Route::get('/api/v1/merhaba',function()
    {
    	return ['mesaj'=>'Merhaba']
    });
    
    
![Json Görüntüleme](https://github.com/melikeoguz/Saglikli-Besleniyorum/blob/master/images/json-goruntulume.jpg)    

<h4>Route ile Parametre Kullanımı</h4>

    Route::get('/urun/{urunadi}',function($urunadi)
	{
		return "Ürün Adı:$urunadi";
	});
 
 http://sagliklibesleniyorum.test:8085/urun/Elma sitesine tıkladığınızda karşınıza <code><b>Ürün Adı: Elma</b> </code>yazısı çıkıyor.
 
 <h4>Route ile Opsiyonel Parametre Kullanımı</h4>
 
 		Route::get('/urun/{urunadi}/{id?}',function($urunadi)
	{
		return "Ürün Adı:$id $urunadi";
	});
 
<h4>Route İsimlendirme</h4>

		Route::get('/urun/{urunadi}/{id?}',function($urunadi,$id=0)
	{
   			 return "Ürün Adı:$id $urunadi";

	})->name('urun_detay');
Yukarıda bulunan kodlar route fonksiyonuna nasıl isimlendirme yapıldığını anlatmaktadır.

	Route::get('/kampanya',function()
	{
    	return redirect()->route('urun_detay',['urunadi'=>'elma',$id=5]);
	}
	);
    Burada ise sonradan yazılmış olan "Route" fonksiyonunun daha önce isimlendirmiş olduğumuz route fonksiyonuna nasıl yönlendirildiği anlatılmaktadır.
    
  <h3>Controller Yapısı</h3>
  
  Route kullanarak yaptığımız tüm işlemleri aslında <code>Controller</code> ile de yapabiliriz.
  
  
  <h5><ins>Artisan Komutu Kullanarak Controller Oluşturmak</ins> </h5>
  
  		php artisan make:controller AnasayfaController
  
  
  yazmanız yeterlidir. Bu işlemden sonra artık <b>controller</b> klasörünün altında <code>AnasayfaController</code> classı bulunmaktadır.
  
  <h5><ins>Route ile Controllerin Tanımı</ins></h5>
  
  AnasayfaController classını oluşturduktan sonra içerisine <code>index</code>
  adında bir fonksiyon yazalım ve bu fonksiyon view içerisinde bulunan <code>anasayfa.blande.php</code> dosyasını görüntülesin
  		
        public function index(){
        
          return view('anasayfa');
      }
      
  Daha sonra routeları oluşturduğumu <code>web.php</code> dosyasına gidip
  
  		Route::get('/','AnasayfaController@index');
diyerek <code>AnasayfaController</code> classında bulunan controllerdan <code>index</code> isimli fonksiyonu çalıştır demek istedik.
      
Dilerseniz kullanım kolaylığı açısından oluşturduğunuz Route'a isim verebilirsiniz. Bunun için <b><code>->name('anasayfa')</code></b> yazmanız yeterlidir.
      
<h4>View Yapısı ve Blade Template Engine</h4>

Herhangi bir yere değişken göndermek istersek <code>compact yapısını</code> kullanabiliriz. Örneğin bunun için şu şekilde değişken belirleyelim;

		$isim="Melike";
        $soyisim="Oğuz"
Daha sonra bunu <code>controller</code> ile gönderirken

		return view('anasayfa',compact('isim','soyisim'))
şeklinde gönderebilirsiniz.

Kullanacağınız sayfada kullanabilmek için ise;
	
  	  {{$isim}} {{$soyisim}} 
  yazmalısınız. Eğer bu değerleri ayrı ayrı yazmak istiyorsanız <b>Birleştirme Operatörünü</b> kullanabilirsiniz. Bunun için;

  	 {{$isim.''.$soyisim}}
yazmanız yeterli olacaktır. Bu işlemi compact yerine <b>with</b> ile de gerçekleştirebilirsiniz ama kod kolaylığı açısından <b>compact</b> tercih edilmektedir.

<h5>If-else Bloklarını Kullanma</h5>

Eğer bir yerde <code>if-else</code> yapısını kullanmak istersek bunun için;

		@if(koşul bilgisi)
        	koşul gerçekleştiğinde verilecek çıktı
        @else
        	koşul gerçekleştiğince verilecek çıktı
        @endif
şeklinde blog bilgisi kapatılır.

<h5>Switch Yapısı</h5>

		@swithc($degisken_adi)
        
        	@case('Melike')
            	Yönetici Olarak Giriş Yapmaktasınız
            @break
            
            @case('Oğuz')
            	Oğuz Bey Yönetici Yetkisine Sahip Değilsiniz 
            @break
            
            @default
            	Hoşgeldiniz
            
        @endswitch
  şeklinde bildiğimiz bir syntax yapısına sahiptir.
  
  ![switch-yapisi](/images/switch-yapisi.jpg)
  
  <h5>Döngü Yapısı</h5>
  
  Yine diğer dillerde öğrendiğimiz gibi for mantığı da aynı şekilde kullanılmaktadır. <code><b>@for</b></code> ile başlatılıp <code><b>@endfor</b></code> ile sona ermektedır.
  
      @for($i=0;$i<10;$i++)
        Döngü Değeri: {{$i}};
      @endfor
      
 <h5>Continue ve Break Yapısı</h5>     
 
 Öncelikle <b>Kullanıcı id</b>'leri ve <b>Kullanıcı Adlarının</b> bulunduğu bir dizi oluşturalım.Daha sonra oluşturduğumuz bu yapıyı <code>compact</code> kullanarak <b>Anasayfaya</b> gönderelim.
 
 $kullanicilar=[
 
 ['id'=>1,'adi'=>'Melike'],</br>
 ['id'=>2,'adi'=>'Oğuz'],</br>
 ['id'=>3,'adi'=>'Nefise'],</br>
 ['id'=>4,'adi'=>'Hayat']
 
 ];
 
 Oluşturduğumuz bu diziyi anasayfaya göndermek için aşağıdaki kodu yazmalısınız.
 
    	return view('anasayfa',compact('kullanicilar'));
 Daha sonra <b>continue</b> ve <b>break</b> yapılarını kullanabilmek için şu şekilde bir senaryo oluşturalım. Eğer <code>Kullanıcı id 1 ise onu ekrana basma ve Kullanici adi 4 ise işlemi sonlandır</code> gibi bir kod yazalım.

![Continue ve Break Ekran Görüntüsü](/images/continue-break-yapisi.jpg)

<h5>Yorum Satırı Nasıl Yapılır ? </h5>

<code>{{ -- -- }} </code> şeklinde yorum satılına alınmaktadır.

<h5>Php Kodları İçerisinde Html Kodu Nasıl Görüntülenir ?</h5>

Eğer php kodu yazmak istiyorsanız kodlarınızı <code>@php</code> tagi açıp daha sonra <code>@endphp</code> arasına yazabilirsiniz. Şimdi de php satırlarının arasında <b>Html </b> kodu yazmanız gerekirse <code>$html= "....";</code> şeklinde yazmalısınız. Daha sonra bu html kodu kapatmak için <code>{!! $html !!}</code> yazmalısınız.

![]()

<hr>
