---
layout: article
title: Bir bölgedeki popüler mekanlar
categories: genel
description: Bir ildeki anlık popüler mekanların sıralı listesini veri tabanında saklama.
tags: [C#, api, restfulapi, consoleapp, geolocation]
---
<a href="/images/2016-08-20-foursquare-api/canakkale_sinirlari.jpg" title="Çanakkale Sınırları"><img src="/images/2016-08-20-foursquare-api/canakkale_sinirlari.jpg" class="pure-img" alt="Çanakkale Sınırları"></a>

Üniversite yıllarımda Mekansal adında bir projede yer almıştım, projenin amacı kabaca popüler mekanları göstermekti. Ben burada gerekli olan veriyi sağlama görevini üstlenmiştim. Bunun için o zamanlar popüler foursquare kullanmak iyi bir veri kaynağı demekti. Foursquare resmi API hizmeti ihtiyacım olan temel bilgileri sunuyordu fakat fazlasını değil. Büyük verileri gözden geçirmek istiyorsanız direkt iletişime geçerek konuyu onlarla konuşmanız yani ikna etmeniz gerekliydi. Buna enerji harcamak ve kesin olmayan bir cevap beklemekten ise standart API kullanarak istediğim şeyi elde etmeye karar verdim. İstediğim şey basitti: bir ildeki **anlık** en popüler mekanlar. Anlık olması demek o saatler içerisinde mekanda bulunan foursquare kullanıcı sayısını değerlendirmek anlamına geliyor.

# Foursquare API

API bize sunduğu özelliklerden biri belli bir daire içerisindeki en popüler yaklaşık 50 (tam sayıyı hatırlamıyorum) mekanı özellikleri ile birlikte vermesiydi. Mekanların özellikleri adı, türü gibi bilgiler içermekte olup ayrıca o anda orada bulunan kullanıcı sayısını içermekteydi (bugüne kadar kaç kişinin orada olduğu bilgisi dahi bulunmakta). Aşağıda Bing MAPS üzerinde gerçek API verileri ile bir örneğini gösterebilirim: 
<a href="/images/2016-08-20-foursquare-api/vanue_search.png" title="foursquare vanue search"><img src="/images/2016-08-20-foursquare-api/vanue_search.png" class="pure-img" alt="foursquare vanue search"></a>
*Yeşil çizgi: daire sınırları, M: merkez, Sayılar: o anda orada bulunan kişi*

Bu daireleri yan yana aralarında boşluk kalmayacak şekilde birden fazla kullanarak belli bir bölgenin tamamını arayabilirim:
<a href="/images/2016-08-20-foursquare-api/pushpinler2.png" title="pushpins"><img src="/images/2016-08-20-foursquare-api/pushpinler2.png" class="pure-img" alt="pushpins"></a>

Burada tekrar bir sorun karşıma çıkıyor. Bu noktaları sadece bir bölge sınırı içerisine koymak. Bunu resmi API sağlamadığından kendim yapmalıyım. Her bölge için bir kere noktaların konumlarını bulmak yeterli olacaktır.

Başlangıç olarak bir dikdörtgen içerisini dolduralım:
<a href="/images/2016-08-20-foursquare-api/pushpinler.png" title="pushpins"><img src="/images/2016-08-20-foursquare-api/pushpinler.png" class="pure-img" alt="pushpins"></a>

Daha sonra bölge sınırları dışarısındaki noktaları atabiliriz (point in polygon):
<a href="/images/2016-08-20-foursquare-api/point_in_polygon.png" title="point_in_polygon"><img src="/images/2016-08-20-foursquare-api/point_in_polygon.png" class="pure-img" alt="point_in_polygon"></a> 

## Konsol Uygulaması

Noktaları belli kurallara göre belirlediğime göre geriye API sorgularını yapmak kalıyor. Sorgular topluca ve periyodik şekilde tekrarlı gerçekleşmesi gerekiyor. Bunun için makinenin anlaması kolay olan konsol uygulamasını uygun gördüm. Böylece program bulutta bir sanal sunucuda parametreler vererek periyodik olarak otomatik çalıştırılabilir. Programlama dili olarakta C# kullandım. Kısaca yaptığı şey sorgu yapacağı noktaları .json dosyasından parametre olarak almak sorguları yapmak bunları bir dosyaya kaydetmek. Bütün sorgular bitince verileri temizleyip (birbirinin aynı verileri silmek) düzenleyerek bir SQL veri tabanına kayıt etmek.

Visual Studio üzeride çalışan hali (konsol çıktısında mekan isimleri var):
<a href="/images/2016-08-20-foursquare-api/topluca_veri_cekme.png" title="topluca_veri_cekme"><img src="/images/2016-08-20-foursquare-api/topluca_veri_cekme.png" class="pure-img" alt="topluca_veri_cekme"></a> 

API sorgularının sonucunu Debug ekranında gösterimi:
<a href="/images/2016-08-20-foursquare-api/topluca_veri_cekme_zoomed.png" title="topluca_veri_cekme_zoomed"><img src="/images/2016-08-20-foursquare-api/topluca_veri_cekme_zoomed.png" class="pure-img" alt="topluca_veri_cekme_zoomed"></a>