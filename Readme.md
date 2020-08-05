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
<h4>2. Gün (05.08.2020)</h4>

<h5><ins>Şablon Yapısı</ins></h5>

Bu tür web geliştirme projelerinde bir adet <b>Şablon Yapısı</b> kullanılmaktadır. Bunun nedeni ise aşağıdaki fotoğrafı yorumlayarak anlayabiliriz.

![Şablon Yapısı](/images/sablon-yapisi.jpg)

Bizim birçok sayfamız olacağı için her sayfa için benim <code>footer alanı</code>  ve <code>navbar</code> eklem gerekiyor. Eğer her sayfa için bu işlemi tek tek yaparsam hem sayfa hızı etkilenir hem de gereksiz bir iş yükü yaşarız. Bunu önlemek amacıyla kendimize bir şablon oluşturmalıyız.

<h5><ins>Şablon Yapısı Kullanmadan Sayfaları Oluşturma<ins></h5>

Bunun için <code>web.php</code> dosyamızın içine Route ile <code>view</code> kodlarını yazmanız gerekmektedir.

		Route::view('/kategori','kategori');
        Route::view('/urun','urun');
        Route::view('/sepet','sepet');
Buradaki kodlarda demek istediğimiz şudur:
<li> <i>Url'e <b>/kategori</b> eklediğimizde view dosyasının içinde bulunan <b>kategori.blade.php</b> dosyasını çalıştır. Diğer satırlarda da diğer sayfalar için bu işlemi gerçekleştir demiş olduk.</i></li></br>

><b><i>Route yapısında kullanılan view özelliği php 5.5 sürümünden sonra gelmiştir</i></b>        

Bu işlem gerçekleştikten sonra şimdi de <code><b>view</b></code> klasörüne <code><b>kategori.blade, urun.blade ve sepet.blade</b></code> adlı php dosyalarının oluşturulması gerekmektedir.

Daha sonra .blade olan view klasörlerin içine gerekli yönlendirmelerin yapılması gerekmektedir. Bu yönlendirmeler aşağıdaki gibidir:

		<a href="/">Anasayfa</a>
		<a href="/urun">Ürün</a>
		<a href="/kategori">Kategori</a>
		<a href="/sepet">Sepet</a>
	<hr>

		<h2 align="center">Ürün</h2>
	<hr>

			E Ticaret Sitesi
 yazılması gerekmektedir. Bu kodların işlevini aşağıdaki gife bakarak anlayabilirsiniz.
 
 ![Şablon Yapısı Kullanmadan Sayfa Oluşturma](/gifs/sablon-kullanamadan-sayfa-olustu.gif)

<h5><ins>Şablon Yapısı Kullanarak Sayfaları Oluşturma</ins></h5>

Öncelikle klasörlerimizde aradıklarımızı rahatlıkla bulabilmemiz için <b>layouts</b> adında bir klasör açıyoruz. Daha sonra bu klasörün içine genel şablon yapımızı kodlayacağımız bir <code><b>master.blade.php</b></code> adlı bir php file oluşturuyoruz.

> Html kodlarını içine kolaylıkla yazabilmek için <code><b>html:5</b></code> yazıp daha sonra <code><b>tab</b></code> tuşuna basabilirsiniz.

Daha sonra bu master.blade adlı php dosyamızın içine <code>Body</code> bölümüne Yukarıda verdiğimiz yönlendirme linklerini yerleştiriyoruz. Burada bizim istediğimiz <code><b>Dinamik Bir Web Sitesi</b></code> geliştirmek olduğu için <code><b>master.blade</b></code> dosyasındaki dinamik olacak kısımlara <b>@yield('title', config('app.name'))</b> ve <b>@yield('content')</b> yazılması gerekmektedir.

Yazdığımız bu <b><code>Title</b>ve <b>Content</b></code> adlı bilinmeyen kısımları karşılamak için 2 adet yapı kullanmamız gerekmektedir. Bunlar <b>extends</b> ve <b>section</b>'dır.

urun.blade, kategori.blade ve sepet.blade olarak oluşturduğumuz dosyalarının başına hangi php dosyasından extend etmesi gerektiğini anlatabilmek için sayfanın başına <b>@extends('layouts/master')</b> yazmamız gerekmektedir.

Başlık kısmının dinamik olması için ise <b>@section('title','urun')</b> yazmamız gerekmektedir.

İçerik kısmını dinamik olarak ayarlayabilmek için ise;

		@section('content')
        <h2>Kategori Sayfası</h2
        @endsection
yazmalısınız.        

Yaptığımız tüm işlemleri daha iyi anlayabilmeniz adına aşağıdaki ilgili dosyaların içinde yazılan kodların bulunduğu giflere bakabilirsiniz.

![master.blade.php dosyası](/gifs/masterblade.gif)</br>
![urun-kategori-sepet.blade](/gifs/urun-kategori-sepetblade.gif)</br>

Bu giflerden sonra şimdi de nasıl bir görünüm elde ettiğimi aşağıdaki gife bakarak ulaşabilirsiniz.

![tum-gorunum](/gifs/tum-gorunum.gif)</br>

<h5><ins>Laravel Mix Yapısı</ins></h5>

Eğer projenizin alt yapısına bootstrap eklemek isterseniz projenizin olduğu dizine gelip terminali çalıştırıp <code>php artisan preset bootstrap</code> yazmanız gerekmektedir.

![Bootstrap install](/images/bootstrap-install.jpg)

Bu kurulumlar tamamlandıktan sonra <b>resources > assets > js</b> ve <b>sass</b> klasörlerinin içerisindeki aşağıdaki gibi eklemeler meydana gelir.

![Görüntülenen Dosyalar](/images/bootstrap-install-sonraki.jpg)

> <i>Laravel Mix hakkında daha detaylı bilgi için [lütfen tıklayınız](https://laravel.com/docs/7.x/mix)</i>

<h5><ins>Kategori Sayfasının Oluşturulması<ins></h5>

Herhangi bir sayfa oluştururken öncelikle onun <code>Controller</code> dosyasını oluşturmalısınız. Bunun için terminal ekranına <code><b>php artisan make:controller KategoriController</b></code> yazıp controller dosyasının oluşturmalısınız.

Controller dosyasında ilgili methodu yazdıktan sonra <code><b>web.php</b></code> dosyasının içerisine Route::get.. diye başlayan tanımlamayı yapınız. Daha sonra route komutu ile yönlendirme yaptıktan sonra bu yönlendirmeye <code>-> name('kategori');</code> gibi isim verebilirsiniz.

<h5><ins>Route Fonksiyonlarının Gruplandırılması</ins></h5>

Web sitenizde birçok sayfa bulunacaksa eğer birden fazla route fonksiyonu yazacaksınız demektir. Kod tekrarına girmemek adına yönlendirmelerinizi gruplandırabilirsiniz. Örneğin kullanıcı oturum açma ve kullanıcı kaydolma sayfaları için aşağıdaki gibi yönlendirme yapıyorsunuz.

    Route::get('/kullanici/oturumac','KullaniciController@giris_form')->name('kullanici.oturumac');
    
    Route::get('/kullanici/kaydol','KullaniciController@kaydol_form')->name('kullanici.kaydol');
	
Dikkat ederseniz <b>oturumac</b> ve <b>kaydol</b> uzantılarından önce <b>/kullanici</b> yazmaktadır. Önünde yazdığı için Route Gruplandırma yaparken <code>prefix</code> kullanmak zorundayız. Bunun için gereken ise aşağıdaki kodu yazmaktır:

		Route::group(['prefix'=>'kullanici'],function ()
    {
        Route::get('/oturumac','KullaniciController@giris_form')->name('kullanici.oturumac');
        Route::get('/kaydol','KullaniciController@kaydol_form')->name('kullanici.kaydol');
    });
		
<h4>Veritabanı Ayarları</h4>    

Veritabanı ile ilgili tüm ayarlamaları <code><b>database.php</b></code> dosyasının içinde yapmak yerine <code>env</code> dosyası altında gerçekleştirilmelidir. Çünkü env dosyası git versiyon control sistemine entegre edilmemiştir. Böylelikle veritabanınıza kimse ulaşamayacaktır.

Şimdi ise <b>database</b> klasörünün altına <code>database.sqlite</code>adlı bir dosya oluşturun. Daha sonra ev klasörü içerisine <code>DB_CONNECTION=sqlite</code> ve <code>DB_DATABASE=</code> kısmına database.sqlite dosyasının <b>path'ini</b> yazınız. 

Bu işlemler tamamlandıktan sonra PhpStorm'da sağ üst tarafta yer alan <b>Database</b> kısmına tıklayınız. Daha sonra <b>DataSource</b> kısmına tıklayarak kullanacağınız veritabanı türünü seçiniz. Bu projede gerekli Database işlemleri aşağıdaki gibi yapılmıştır.

![SQLite ayarları](/images/sqlite.jpg)

Daha sonra karşınıza aşağıdaki gibi bir kısım çıkacak. Burada <b>file</b> kısmına veritabanınızın olduğu <b>path'i</b> yazmanız gerekmektedir. <code>Sağlıklı Besleniyorum</code> adlı e ticaret sitesinde SQLite kullanıldığı için gerekli kısımlar aşağıdaki gibi yapılmıştır.

![Drivers](/images/successful.jpg)

> <i>Eğer bilgisayarınızda gerekli driverlar bulunmuyorsa size uyarı vermektedir. Download kısmına tıklayarak gerekli dosyaları indirin. Daha sonra <b>Test Connnection</b> kısmına tıklayarak her şeyin doğru olduğuna emin olun.</i>

<h5><ins>Veritabanı Tablolarını Oluşturma</ins></h5>

Veritabını tablolarını aşağıdaki gife bakarak oluşturabilirsiniz.

![Tablo Oluşturma](/gifs/create-table.gif)

<h5><ins>Tablolara Veri Ekleme</ins></h5>

Veri ekleme işlemlerini aşağıdaki gif yardımıyla yapabilirsiniz.

![Tabloya Veri Ekleme](/gifs/veri-ekleme.gif)

<h5><ins>Tinker Kullanımı</ins></h5>

Tinker kurulumu için PhpStorm içinde bulunan terminali kullanabilirsiniz. Bunun için aşağıdaki gife bakabilirsiniz.

![Tinker Kurulumu](/gifs/tinker-kurulum.gif)

>Tinkerda sorgulamalar yapılırken <b>Raw Sql Query</b> yapısı kullanılmaktadır.

<h5><ins>Raw Sql Query Sorgulaması</ins></h5>

Sorgu işlemlerinin nasıl yapıldığını anlayabilmek için aşağıdaki gife bakabilirsiniz.

![Raw Sql Query](/gifs/raw-sql-query.gif)

<h6><ins>Kayıt Ekleme İşlemleri</ins></h6>

Bu işlemi sırası ile takip etmek için aşağıdaki gife bakabilirsiniz.

![terminal ile kayıt ekleme](/gifs/terminal-ile-kayit-ekleme.gif)

>DB::statement("VACUUM") yazarak veritabanımızın belleğimizde kaplayan boyutunu küçültmüş olursunuz.

<h5><ins>Query Builder Yapısı</ins></h5>

Eğer bu sorgulama yapısını kullanırsanız Query Builder, sizin yerinize <code><b>Injection</b></code> saldırılarına karşı koruma sağlar.

<h6><ins>Query Builder Kullanarak Tabloya Veri Eklemek</ins></h6>

Bu işlemleri aşağıdaki gife bakarak gerçekleştirebilirsiniz.

![Query Builder Kullanarak Veri Ekleme](/gifs/Query-builder-yapisi.gif)

