---
layout: article
title: Lazca Türkçe Sözlük Uygulaması
categories: genel
description: Daha önce internet sitesi olarak rastladığım Türkçe Lazca sözlük için çevrimdışı mobil uygulama.
tags: [cordova, apachecordova, html, js, css, mobileapp, desktopapp, website]
---
[Apache Cordova](https://cordova.apache.org/) teknolojisini ilk duyduğumda ve belgelerini okuduğumda içimde onunla bir deneme yapmak isteği uyandı. Aklımda dönen bir kaç fikirlerden sonra bir sözlük yapmaya karar verdim. Bu karardaki en büyük etken otomatik tamamlama özelliğinin HTML5 ile ([datalist](http://www.w3schools.com/tags/tag_datalist.asp)) kolay olması ve bunu bir sözlükte denemek istememdi.

[Lazca](https://tr.wikipedia.org/wiki/Lazca) dili bir miktar aşına yöresel bir dil (aksan değil). Konuşulduğunda büyük kısmını anlayabiliyorum fakat bu dile hakim olduğum söylenemez. Birçok kez Lazca bir kelimenin Türkçe karşılığını merak ederken buluyorum kendimi. Bu da bana kolay erişebilen bir sözlük ihtiyacı hissettirdi. Eğer masaüstü bilgisayarda isem [lazuri.com/lazuri_ceviri](http://www.lazuri.com/lazuri_ceviri/) tüm ihtiyacımı görüyor. Mobil tarafta ise durum biraz farklı. Dokunmatik ekranda yazmak pek yetenekli olmadığım bir konu. Bundan dolayı yazdığını otomatik tamamlayan bu sözlük işimi daha kolaylaştırabilir. Bu sebepten bu sözlüğü yapmaya karar verdim.

## Sözlüğün İçeriği
Tabi yapılacak en temel iş sözlüğü sözlük yapan kelimeler ve çevirilerini elde etmekti. Bunun için bir sözlük taslağı olan [http://ayla7.free.fr/laz/](http://ayla7.free.fr/laz) adresindeki verileri kullanmak için sitedeki mail adresine ulaşarak izin istedim. Sağ olsun bu mail adresinin sahibi verileri kullanmama izin verdi. Verileri html sayfalarından alıp kullanılabilir şekilde ayıklayan [uygulamayı](https://github.com/aytacyildiz/lazcasozlukfetcher) yazdım ve kelimelerin çevirilerini küçük html dosyaları olarak diske kayıt ettim.

Daha sonra bu verileri kullanacak olan [cordova uygulamasını](https://github.com/aytacyildiz/lazcasozluk) yazdım. Cordova ile proje geliştirmek aslında keyif verici ve beklediğimden daha kolay bir deneyimdi. Bir sıkıntı yaşadım oda çok sayıda küçük html dosyası bulunan projemin bazı cordova komutlarını büyük derecede yavaş çalıştırmasıydı. Çok sayıda kastım 19317 olduğu için bu anlaşılabilir bir durum :)

## Lazca Sözlük
Sonuç olarak sade ve kullanışlı bir sözlük ortaya çıktı ve sonuçtan memnunum. Aşağıdaki ekran görüntüleri ile nasıl göründüğünü görebilirsiniz. Hatta en sonda bir hareketli gif bile bulunmakta.

Android uygulaması kelime arama:
<a href="/images/2016-08-20-lazca-sozluk/android_uygulama_ekran_goruntusu_2.png" title="Lazca Sözlük Uygulaması Ekran Görüntüsü"><img src="/images/2016-08-20-lazca-sozluk/android_uygulama_ekran_goruntusu_2_small.png" class="pure-img" alt="Lazca Sözlük Uygulaması Ekran Görüntüsü"></a>

Android uygulaması sonuç sayfası:
<a href="/images/2016-08-20-lazca-sozluk/android_uygulama_ekran_goruntusu_1.png" title="Lazca Sözlük Uygulaması Ekran Görüntüsü"><img src="/images/2016-08-20-lazca-sozluk/android_uygulama_ekran_goruntusu_1_small.png" class="pure-img" alt="Lazca Sözlük Uygulaması Ekran Görüntüsü"></a>

İnternet sitesi çalışma demosu  (dosyanın yüklenmesi zaman alabilir lütfen bekleyin):
<a href="/images/2016-08-20-lazca-sozluk/desktop_animated_demo.gif" title="Lazca Sözlük Web Sitesi Ekran Görüntüsü"><img src="/images/2016-08-20-lazca-sozluk/desktop_animated_demo.gif" class="pure-img" alt="Lazca Sözlük Web Sitesi Ekran Görüntüsü"></a>

Kaynak kodlarına buradan erişebilirsiniz:

- [https://github.com/aytacyildiz/lazcasozluk](https://github.com/aytacyildiz/lazcasozluk)
- [https://github.com/aytacyildiz/lazcasozlukfetcher](https://github.com/aytacyildiz/lazcasozlukfetcher)