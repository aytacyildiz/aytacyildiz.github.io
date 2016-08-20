---
layout: article
title: Bir Microsoft Yaz Okulu projesi Ekna
categories: kodlama
description: Microsoft Yaz Okulu için hazırladığım Windows 8.1 ve Windows Phone 8.1 uygulama projesi
tags: [c#, microsoft, windowsphone, windows, microsoftazure, cloud]
---
<a href="/images/2016-08-20-ekna-projesi/ekna_logo.png" title="Ekna Posteri"><img src="/images/2016-08-20-ekna-projesi/ekna_logo.png" class="pure-img" alt="Ekna Posteri"></a>

Üniversite yıllarımda (tam olarak 2014) Microsoft'un [yaz okulu](https://www.microsoft.com/turkiye/yaz-okulu/) düzenlediğini öğrendim. Katılabilmek için bir proje sunmanız ve bu projenin kabul edilmesi gerekliydi. O zamanlar C# ile ilgilendiğimden şansımı denemek istedim ve başvurmak için bir proje düşünmeye başladım. Yapacağım projede ana hedeflerden birisi yeni teknolojileri öğrenmek olacaktı. Bu arada öğrenilmesi hedeflenen teknolojileri sıralarsam yaz okulunun kapsamını aklınızda canlandırmanız kolay olacaktır:

- Üyelik sistemi geliştirilecek ise Windows Azure Mobile Services Authentication
- Geliştirilen uygulamada skorlar saklanacak ise Windows Azure Mobile Services
- Şayet uygulama içerisinde yüzlerce resim kullanmayı düşünüyorsanız Windows Azure Blob Storage
- Resimler üzerinde Image Processing işlemleri yapılacaksa Nokia Imagine SDK
- Bunlarla birlikte kullanıcı deneyimini daha üst noktalara çıkartmak için Windows 8 ve Windows Phone için hazırlanan Telerik kontrolleri
- Son olarak Visual Studio ile birlikte gelen Blend

Yukarıdaki listeyi başvuru için gönderdiğim elektronik postaya yazılan cevaplardan birinden aldım. Bu teknolojileri kafamdaki fikirle harmanlayarak ekna projesini başvuru olarak göndermeye karar verdim.

## Ekna Projesi Nedir?
Projeyi kısaca açıklamak gerekirse kişiler arasından şahsi mesajlarla konum paylaşmayı sağlayan bir uygulama olacaktı. Evet çok büyük bir yenilik değil ama hedef bir şeyler öğrenmek olduğundan bu konuyu farklı değerlendirebiliriz. Uygulamanın temel özellikleri:

- Kişi listesi
- Bildirimler
- Uygulama dışında konum paylaşmak için kısa URL oluşturma
- Belirli süre periyotlarında (örneğin 60 saniyede bir) birini takip edebilme

Uygulamanın tasarım çizimleri ise şöyle:
<a href="/images/2016-08-20-ekna-projesi/mockups.png" title="Ekna Mockups"><img src="/images/2016-08-20-ekna-projesi/mockups.png" class="pure-img" alt="Ekna Mockups"></a>

Bu gönderim kabul edildi ve bende Yaz Okulunun bir parçası olarak Microsoft Türkiye binası konferans salonuna gitmeye başladım. Benim gibi bir çok geliştiricinin bulunduğu ortamdan keyif alarak ayrıldım. Bir çok şeyi orada deneyimledim ve sonunda hem verilen dersleri takip ederek hem de uygulamamı geliştirerek Yaz Okulunu tamamladım. Uygulamam zamanın kısıtlılığından ve derslerin yoğunluğundan dolayı olgun bir hale gelemedi fakat çalışan ve işlevsel olan düz sade bir uygulama olarak uygulama mağazasında yerini aldı:

<a href="/images/2016-08-20-ekna-projesi/ekna_wp_store.png" title="Ekna Windows Phone Store"><img src="/images/2016-08-20-ekna-projesi/ekna_wp_store.png" class="pure-img" alt="Ekna Windows Phone Store"></a>

Tabi ne yazık ki Yaz Okulunda verilen bir yıl ücretsiz Microsoft Azure hesabı ve Microsoft Dreamspark üyeliği sonlanacağı için uygulamayı bir süre sonra mağazadan kaldırdım.

## Kullandığım Teknolojiler
Eğer uygulamayı nasıl geliştirdiğimden bahsedecek olursak projeyi Universal Windows App olarak hazırlamaya başladım. Odak noktam mobil fakat Windows masaüstü bilgisayarlar için bazı özellikleri kırpılmış bir uygulama koymak hedeflerimden biriydi. Özelliklerinin kırpılmasını tek sebebi Windows masaüstünde şahsın o anki konumunu bulabileceğimiz konum hizmetinin (GPS) bulunmamasıydı.

Programlama dili olarak C# ve bulut tarafında JavaScript kullandım. Buluttan bahsetmişken uygulamanın İnternet ile iletişimini Microsoft Azure kullanarak sağladım. Yaz Okulunun en temel konularından biri buydu. Microsoft Azure üzerinden verileri (mesajlar, kullanıcılar ...) saklamak için Table Storage, şahsa özel bildirimler için Notification Hubs, zamana yayılmış rutin işler için Scheduler servisini kullandım.

Aslında yaz okulunun büyük kısmı kamera altına alındı ve yaz okulunun tüm derslerine bu linkten erişebilirsiniz: [https://www.youtube.com/user/acikakademitv/videos](https://www.youtube.com/user/acikakademitv/videos) 

*Not: Benim olduğum yılın oynatma listesi ne yazık ki bulunmuyor bütün yıllar topluca bulunuyor. Merak ediyorsanız aşağılardaki (tarih sıralılar) 2014 tarihindeki videolara bakabilirsiniz.*