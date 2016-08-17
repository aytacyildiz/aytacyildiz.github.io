---
layout: article
title: ADO.NET Ortamında Entity Framework İle Uygulama Geliştirme
categories: kodlama
description: Entity Framework ile objeleri veri tabanında saklanabilir halde kullanmak çok daha kolaylaşıyor.
tags: [EF, ADO.NET, .NET, Framework, Database, Visiual Studio]
---
Uygulama geliştiriken objeleri kullanmak bilinen bir yöntem. Bu yöntem objeler arasında ilişkiler oluşturmak için referanslar vermeyide içeriyor. Fakat, bu objeleri ve içerdikileri bilgileri bir veri tabanda saklamak istediğimizde ne yapmalıyız? Öncelikle objelerin niteliklerini veri tabanı veri türlerine (sayi, string, tarih vs.) dönüştirmeliyiz. Dahada zorlayıcı olanı diğer iş ise eğer obje bir diğer objeyi yada listesini içeriyorsa bunu veri tabanında primary key ve foreign key kullanarak modellemeliyiz. Ayrıca veri tabanındaki tabloları objelere çevirmek için tersi yönde bir iş daha yapmalıyız. Birçok kod satırı ve zaman gerektiren bir eylem. İşte bu yüzden zaman ve işten tasaruf için nesne ilişkisel eşleme (object-relational mapping) yazılım geliştirme yöntemi kullanılır. Bu yöntem ile objeye dayalı programlama veri türlerine uyumlu olmayan verileri uyumlu hale çevirme bizim için kendiliğinden gerçekleşir. Bu gerçeleştirimi yapan araçlardan biri ise [Entitiy Framework](http://msdn.microsoft.com/en-US/data/ef) (EF).

## Entitiy Framework Paketi
Bu yazımda [Microsoft Visual Studio 2013](https://en.wikipedia.org/wiki/Microsoft_Visual_Studio) kullanacağım. Objeye dayalı programala dili ile bir veri tabanı kullanarak çok sade bir örnek vereğim. <abbr title="Entitiy Framework">EF</abbr> araçları Visual Studio 2013 içerisinde entegre olarak bilgisayarımıza kuruluyor. Bu konuda bir şey yapmamıza gerek yok. Fakat <abbr title="Entitiy Framework">EF</abbr> runtime için [bir paket](http://www.nuget.org/packages/EntityFramework/) bulunuyor. Bu paketi indirip kurmamız gerekli. Bunu yapabilmek içinde bir paket yöneticisine ihtiyacımız var [NuGet](http://www.nuget.org/).

## NuGet Paket Yöneticisinin Kurulumu
Paket yöneticisini yüklemek için yapmamız gereken şey `Tools` > `Extensions and Updates...` yolunu izlemek.

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (1).png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (1).png" class="pure-img"></a>

Sağ kısımda `Online` kategorisinde arama kutusuna `nuget package manager` yazarak arama yapın ilk çıkacak sonuç bizim yükleyeceğimiz paket yöneticisinin kendisi.

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (3).png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (3).png" class="pure-img"></a>

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (4).png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (4).png" class="pure-img"></a>

Daha sonra `Install` butonuna basarak kullanıcı sözleşmesini kabul edip programı kuruyoruz.

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (5).png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (5).png" class="pure-img"></a>

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (6).png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (6).png" class="pure-img"></a>

Yapılan değişiklerin etki etki etmesi için `Restart Now` butonu ile Visual Studio programını tekrar başlatıyoruz.

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (7).png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (7).png" class="pure-img"></a>

Artık `Tools` menüsü altında `NaGet Package Manager` alt menüsünü görebiliriz.

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (8).png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (8).png" class="pure-img"></a>

## Entity Framework Paketini Yüklemek
Paketi iki şekilde yükleyebilirsiniz, bir kere yükledinizmi diğer projelirinizde kullanamak için tekrar yüklemenize gerekte kalmaz. Bu yöntemler şunlardır:

### 1. Paket Yöneticisi Konsolu
`Tools` menüsündeki `NaGet Package Manager` menüsü altında `Package Manager Console` ile konsol ekranına erişebiliriz.

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (14).png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (14).png" class="pure-img"></a>


Bu konsol ekranında <abbr title="Entitiy Framework">EF</abbr> paketini yükelemek için şu komutu yazıp çalıştırın (Not: `PM>` yazılmayacak):

```
PM> Install-Package EntityFramework
```

Komutun muhtemel çıktısı:

```
Installing 'EntityFramework 6.1.0'.
You are downloading EntityFramework from Microsoft, the license agreement to which is available at http://go.microsoft.com/fwlink/?LinkID=320539. Check the package for additional dependencies, which may come with their own license agreement(s). Your use of the package and dependencies constitutes your acceptance of their license agreements. If you do not accept the license agreement(s), then delete the relevant components from your device.
Successfully installed 'EntityFramework 6.1.0'.
Adding 'EntityFramework 6.1.0' to WpfApplication2.
Successfully added 'EntityFramework 6.1.0' to WpfApplication2.

Type 'get-help EntityFramework' to see all available Entity Framework commands.
```

Ayrıca şu komutla Solution içerisindeki varsayılan projede kullanılan NuGet paketlerini listeyebilirsiniz:

```
PM> Get-Package
```

Bu komutla aynı yerdeki güncellemesi mevcut olan paketleri listeleyebilirsiniz:

```
PM> Get-Package -Updates
```

### 2. NuGet Paket Yönetme Arayüzü
`Solution Explorer` panelinde projenizin `References` kısımını sağ tıklayıp `Manage NuGet Packages...` menü seçeneği ile bu arayüze erişebilirsiniz.

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (9).png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (9).png" class="pure-img"></a>

Arayüz karşınıza çıktığı zaman arama kutusuna `Entitiy Framework` yazıp aramdaki ilk sonucu yüklemeniz paketi yüklemek için yeterli olacaktır.

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (10).png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (10).png" class="pure-img"></a>

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (11).png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (11).png" class="pure-img"></a>

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (12).png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (12).png" class="pure-img"></a>

## Uygulama Geliştirme
Gerekli paketi yüklediğimize göre .NET ortamında uygulama geliştirirken nasıl kullanılacağına değinebiliriz artık. Şimdi çok basit bir örnek ile başlayalım. Bir C# ile WPF projesi yapacağımızı var sayalım. Projemizin adını üzerine sağ tıklayıp `Add` > `New Item...` alt menüsüne tıklayalım.

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (15).png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (15).png" class="pure-img"></a>

Daha sonra `Visual C#` > `Data` kategorisinde `ADO.NET Entity Data Model` nesnesini seçelim.

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (16).png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (16).png" class="pure-img"></a>

Karşımıza `Entity Data Model Wizard` arayüzü çıkacak. İşte bu kısımda bize iki seçenek sunulmakta. Var olan bir veri tabanı kullanmak (`Generate from database`) yada boş bir modeli kendimiz doldurmak (`Empty model`). Eğer elimizde hali hazırda bir veri tabanı bulunuyorsa ve onu kullanmayı düşüyorsak ilk seçeneği, elimizde bir veri tabanı bulunmuyorsa ikinci seçeneği seçmeliyiz.

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (18).png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (18).png" class="pure-img"></a>

Bizim elimizde bir [veri tabanı](https://msftdbprodsamples.codeplex.com/downloads/get/417885 "AdventureWorks2012-Full Database Backup.zip") olduğunu varsayalım. `Next` butonu ile ilerlediğimizde bir veri tabanına bağlanmamızı isteyen arayüz bizi karşılayacaktır. Benim öreğimde bilgisayarımda yerelde bulunan AdventureWorks2012 veri tabanına bağlanıyorum. Veri kaynağını belirten bağlantı karakter dizisini (connection string) daha sonra değiştirmek istiyorsak projemizdeki `App.Config` dosyasında `Save entity connection settings in App.Config as:` kutusundaki isimli değeri değiştirimemiz yeterlidir.

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (19).png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (19).png" class="pure-img"></a>

Bize hangi <abbr title="Entitiy Framework">EF</abbr> sürümünü kullacağımız soran bir arayüz karşılayacak. Yeni sürümlerin getirdiği özellikler ve değişiklere [şu adresten](http://msdn.microsoft.com/en-us/data/jj574253) ulaşabilirsiniz.

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (20).png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (20).png" class="pure-img"></a>

Ve en sonunda bizi veri tababının hangi tablolarını vs. kullanıp modeli oluşturacağımızı soran bir arayüz ile karşılaşacağız. Ben tüm veri tabanı yerine örnek vermek amacıyla sadece bir kısımını kullanıyorum. Buradaki `Pluralize or singularize genereted object names` seçeneğinin anlamı bir nesnenin koleksiyonunun isimi o nesnenin çoğul isimi olarak kullanmaktır. Örneğin `EmailAddress` nesnesinin birden fazla elmanlı koleksiyonu `EmailAddresses` olarak isimlendirilecektir.

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (21).png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/Screenshot (21).png" class="pure-img"></a>

## Entity Data Model
<abbr title="Entitiy Framework">EF</abbr> varlıklar ve aralarındaki ilişkileri belirtmek için [Entity Data Model](http://en.wikipedia.org/wiki/Entity_Framework#Entity_Data_Model) (EDM) tekniğini kullanır. Bu modeli düzenlemize yarayan [EF Designer](http://msdn.microsoft.com/en-us/data/jj713299.aspx) varsayılan olarak Visual Studio 2013 içerisindedir. Örneğin aşağıdaki veri tabanının varlık-bağıntı modeline ([entity-relationship model](http://tr.wikipedia.org/wiki/Entity-relationship_model) (ER)) bir göz atalım.

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/demo-er.png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/demo-er.png" class="pure-img"></a>

<abbr title="Entitiy Framework">EF</abbr> bu <abbr title="entity relationship">ER</abbr> modelini otomatik olarak <abbr title="Entity Data Model">EDM</abbr>e dönüştürür ve kullanımıza sunar. Aşağıda bu iki tablonun C# sınıflara dönüştürülerek nasıl modellendiğini görebilirsiniz.

<a href="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/EntityDesignerDiagram.png"><img src="/images/2014-05-08-ado-net-ortaminda-entity-framework-ile-uygulama-gelistirme/EntityDesignerDiagram.png" class="pure-img"></a>

Böylece `Person` sınıfının `EmailAdresses` adında `EmailAdress` sınıfı nesnelerinden oluşan bir kolaksiyona sahip olduğunu görürüz. Aynı şekilde `EmailAdress` sınıfının bir `Person` alanı bulunmakta. Böylece bir kişinin sahip olduğu mail adreslerine o kişinin nesnesi üzerinden erişebilir aynı şekilde bir mail adresinin sahibine o nesne üzerinden erişebiliriz.

Farklı bir seçenek olarak <abbr title="Entity Data Model">EDM</abbr> kullanmak için elinizde bir veri tabanı bulunmasına gerek yoktur. Yukarıda belirttiğim iki seçenekten biri `Empty model` ile boş bir <abbr title="Entity Data Model">EDM</abbr> kullanarak EF Designer ile veri modelimizi oluşturabiliriz. Böylece veri tabanı veri türleri ile C# veri türleri arasındaki uyumsuzluğu düşünmemize gerek kalmaz. Bu dönüşümü <abbr title="Entitiy Framework">EF</abbr> bizim için gerçekleştirir.

## Kodlama
Artık veri modelimiz projemize eklendiğine göre bu yeni sınıfları kullanmaya başlayabiliriz. Benim örneğimde `DemoEntities` olarak adlandırdığım sınıf veri tabanı bağlantısını ve varlık nesnelerini tutan bir sınıftır. Bu sınıf değişiklik takibi, ayrıt edici özellik takibi vs. işleri gereçekleştirir ve LINQ-tabanlı veri erşimi sağlar. Bu sınıfın myE adında bir nesnesini oluşturalım.

{% highlight c# %}
DemoEntities myE = new DemoEntities();
{% endhighlight %}

Artık elimizde kayıtlı olan verilere sınıflar araclığı ile erişebiliriz. Mesela `Person` tablosunda kayıtlı olan ve id numarası 1 olan (tablodaki id kolonunun isimini yazmayada gerek yok) nesneyi elde etmek için:

{% highlight c# %}
Person p = myE.People.Find(1);
{% endhighlight %}

Daha sonra bu elde ettiğimiz nesnenin özelliklerini değiştirebiliriz:

{% highlight c# %}
Person p = myE.People.Find(1);
p.name = "XXXXX";
p.lastname = "YYYYY";
{% endhighlight %}

Elimizde kaydı olan bir veriyi değiştirmek yanında yeni bir veri kaydı oluşturabilir yada bir veri kaydını bir daha kullanmamak adına silebiliriz. Yeni bir `Person` nesnesi oluşturduğumuzu varsayalım:

{% highlight c# %}
Person p_new = new Person();
p_new.personId = 4;
p_new.name = "XXXXX";
p_new.lastname = "YYYYY";
{% endhighlight %}

Bununla arkaplanda bu nesnenin var olduğu tablodaki satır hücrelerini doldurmuş oluyoruz. Fakat `Person` tablosu ile `EmailAdress` tablosu arasındaki foreign key ilişkisini nasıl tanımlayacağız? Bunu bir tablo hücresi doldurmak yerine o nesnenin ilgili alanındaki karşılığını yazarak yapabiliriz:

{% highlight c# %}
EmailAdress email = new EmailAdress();
email.email_id = 5;
email.email = "a@b.com";
p_new.EmailAdresses.Add(email);
{% endhighlight %}

Artık yeni oluşturduğumuz p_new nesnesi ile temsil ettiğimiz kişinin mail adresi email isimli nesne olacaktır.

Var olan veri sisteminde kayıtlara id ile erişmek yerine `myE` nesneside yer alan nesne koleksiyonlarında `where` fonksiyonu ile LINQ kullanarak sorgular yapabiliriz. Mesela isimi Henry olan tüm kişileri elde etmek için:

{% highlight c# %}
var p_where = myE.People.Where(prs => prs.name == "Henry");
{% endhighlight %}

### Değişiklikleri Kaydetme
Eğer yeni bir kayıt için nesne oluşturduysak bunu var olan nesne koleksiyonuna eklememiz gerekli. Yoksa bu yeni kayıt arkaplanda veri tabanında muhafaza edilmez.

{% highlight c# %}
myE.People.Add(p_new);
{% endhighlight %}

Var olan kayıtları temsil eden nesnelerdeki yaptığımız değişikler (isimini değiştirmek gibi) ve eklediğimiz yeni nesneleri veri tabanına kaydetmek için şu fonksiyonu `myE` nesnesi üzerinden çağırmalıyız:

{% highlight c# %}
myE.SaveChanges();
{% endhighlight %}

Sonunda <abbr title="Entitiy Framework">EF</abbr> ile oluşturulan nesneleri kullanarak arkaplandaki veri tabanını düşünmeden yazdığımız kod ile verilerimiz kayıt altında olacak. Bunun sayesinde veri tabanı ile kod arasındaki ilişkiyi sağlamak için harcayacağımız efor minimuma ulaşmış oldu. 

Bence güzel bir yöntem.
