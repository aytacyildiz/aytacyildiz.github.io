---
layout: article
title: Microsoft Azure Nedir?
categories: genel
description: Microsoft Azure bulut platformu nedir, kısaca bir bakış.
tags: [bulut bilişim, azure, virtual mechine, sanal makine, microsoft azure, windows azure, bulut, sunucu, server, iş uygulamaları]
---
<a href="/images/2014-07-15-microsoft-azure-nedir/azure.png" title="Microsoft Azure"><img src="/images/2014-07-15-microsoft-azure-nedir/azure.png" alt="Microsoft Azure"></a>

Micorosft Azure  birçok farklı servisi içerisinde barındıran bir bulut platformudur. Dünyanın çeşitli yerlerinde konumlandırılmış Microsoft veri merkezlerinde barındırılırmaktadır. Bir çok Azure servisi bulut bilişim kalıplarına tam olarak uymasada <a title="Infrastructure as a service" href="http://en.wikipedia.org/wiki/Infrastructure_as_a_service#Infrastructure_as_a_service_.28IaaS.29">IaaS</a> olarak Sanal Makineler üzerinde kosan işletim sistemleri, Depolama ve Ağ <a title="Platform as a service" href="http://en.wikipedia.org/wiki/Platform_as_a_service">PaaS</a> olarak Bulut Servisleri, Mobil Servisler gibi hızlıca bir ayrım yapabiliriz.
<h2>Neden Bulut?</h2>
Fiziksel olarak sunucu barındırmanın yerine bulut bilişim hizmetlerini kullanmanın ne gibi yararlar sağlayacağına gelin birlikte bakalım;
<ul>
	<li><strong>Hız:</strong> Bulutta çalışan uygulamaları geliştirmek geleneksel uygulama geliştirimine göre çok daha hızlıdır. Bunun sebebi altyapıda yatan hesaplama, depolama ve network mimarilerini yaratma, yapılandırma ve idare etme işlemlerini yapmanıza gerek yoktur. Bunun yerine bu kaynakları bulut barındırma servis sağlayıcınızdan elde edebilirsiniz.</li>
	<li><strong>Esneklik: </strong>Bulut uygulamaları hızlıca genişletilebilir(kullandığı kaynaklar çoğaltılabilir) çünkü hesplama, depolama ve network kaynakları servis sağlayıcı tarafından bir havuzda toplanmıştır. İhtiyaçlar artarsa size bu havuzdan kaynakları kiralatabilir. Eğer kullandığınız kaynaklar ihtiyacınızın çok üstüde ise bu kaynakları azaltabilirsiniz.</li>
	<li><strong>Ekonomi: </strong>Kullandığın kadarını öde modeli ve hızlıca kapasite artırma ve azaltma sayesinde firmalar iş uygulamarını bulutta çalıştırarak ekonomik verimlilik elde edebilmektedir.</li>
</ul>
<h2>Microsoft Azure Servisleri</h2>
Microsoft Azure dört temel bulut-tabanlı servis kategorisi içermektedir. <a title="Microsoft Azure Documentation" href="https://azure.microsoft.com/en-us/documentation/">Bunlar</a>;
<ul>
	<li>Hesaplama servisleri (Compute services)
<ul>
	<li>Sanal Makineler (Virtual Mechines)</li>
	<li>İnternet Siteleri (Web Sites)</li>
	<li>Bulut Servisleri (Clout Services)</li>
	<li>Mobil Servisleri (Mobile Services)</li>
</ul>
</li>
	<li>Ağ servisleri (Network services)
<ul>
	<li>ExpressRoute</li>
	<li>Sanal Ağ (Virtual Network)</li>
	<li>Trafik Yöneticisi (Traffic Manager)</li>
</ul>
</li>
	<li>Veri servisleri (Data services)
<ul>
	<li>Depolama (Storage)</li>
	<li>SQL Veritabanı (SQL Database)</li>
	<li>HDInsight</li>
	<li>Cache</li>
	<li>Yedekleme (Backup)</li>
	<li>Site Kurtarımı (Site Recovery)</li>
</ul>
</li>
	<li>Uygulama servisleri (App services)
<ul>
	<li>Medya Servisleri (Media Services)</li>
	<li>Servis Veriyolu (Service Bus)</li>
	<li>Push Bildirimleri (Push Notifications)</li>
	<li>Zamanlayıcı (Schedular)</li>
	<li>BizTalk Servisleri (Biztalk Services)</li>
	<li>Aktif Rehber (Active Directory)</li>
	<li>Çok Faktörlü Doğrulama (Multi-fator Authentication)</li>
	<li>Otomasyon (Automation)</li>
	<li>İçerik Dağıtım Ağı (Content Delivery Network)</li>
	<li>API Yönetimi (API Managment)</li>
	<li>Azure RemoteApp</li>
</ul>
</li>
</ul>
Yukarıda görüldüğü üzere hayli fazla servis bulunmakta. Bu servisleri tekil yada bir biri ile birlikte koordineli olarak çoğul kullanabilirsiniz. Ayrıca Sanal Özel Ağ (VPN) gibi teknolojiler kullanarak hem kurumsal sunucular hemde bulut üzerindeki sunucular ile hibrit uygulamalar çalıştırabilirsiniz.

Kaynaklar:

1. [http://download.microsoft.com/download/D/6/7/D670D322-5771-409E-BF34-5B98496DEB0A/Microsoft_Press_ebook_Introducing_Azure_PDF.pdf](http://download.microsoft.com/download/D/6/7/D670D322-5771-409E-BF34-5B98496DEB0A/Microsoft_Press_ebook_Introducing_Azure_PDF.pdf "Introducing Windows Azure for IT Professionals")
2. [http://en.wikipedia.org/wiki/Microsoft_Azure](http://en.wikipedia.org/wiki/Microsoft_Azure "Microsoft Azure Wikipedia")