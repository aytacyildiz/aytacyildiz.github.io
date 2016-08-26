---
layout: article
title: Bilgisayarınıza kurulum yapmadan .NET Core ile deneysel uygulama geliştirme.
categories: kodlama
description: Bilgisayarınıza herhangi kurulum yapmadan .NET Core uygulaması geliştirebilirsiniz.
tags: [framework, netcore, dotnetcore, cloud, IDE, C#]
---
[.NET Core](https://www.microsoft.com/net/core/platform) platformunu daha önce duymadıysanız kısaca anlatmak gerekirse [standart .NET platformunun](https://www.microsoft.com/net/framework) temel düzeydeki özelliklerini barındıran [açık kaynak](https://github.com/dotnet/core) bir .NET framework gerçekleştirimidir. En temel farkı özelliklerinin bir kısmını aldığı platformun aksine sadece Windows işletim sisteminde değil Mac ve Linux/GNU işletim sistemlerinde bile çalışıyor olmasıdır. Ayrıca Windows üzerinde uygulama geliştiriyorsanız modüler olmasından dolayı standart .NET yerine tercih edebilirsiniz. Çünkü bir kaç özellik için büyük bir platformu kullanmak yerine sadece ihtiyacımız olan özellikleri barındıran hafif bir platform tercih etmek sistem yükü ve karmaşıklığını azaltmamıza yarayabilir.

<a href="/images/2016-08-26-dotnetcore-fiziksel-kurulumsuz-kullanim/dotnet.png" title=".NET info"><img src="/images/2016-08-26-dotnetcore-fiziksel-kurulumsuz-kullanim/dotnet.png" class="pure-img" alt=".NET info"></a>

Eğer hemen şimdi .NET Core denemek istiyorsanız elbette önereceğim en iyi yol [Visual Studio Community](https://www.visualstudio.com/free) ve [.NET Core 1.0.0 - VS 2015 Tooling Preview 2](https://go.microsoft.com/fwlink/?LinkID=824849) ya da [Visual Studio Code](https://code.visualstudio.com/) ve [.NET Core SDK for Windows](https://go.microsoft.com/fwlink/?LinkID=809122). Bunlar bilgisayarınız kurulum yapmanızı gerektiren programlar. Uzun vadede çalışmak isterseniz tercih edilebilir. Fakat bu yeni teknolojiyi tanımak ve deneme yapmak amacındaysanız bir diğer yol bulut üzerinde deneme yapmak ve bilgisayarınız hiç bir şey kurmak zorunda kalmamak.

## Cloud9 Geliştirme Ortamı
Bunun için bize ücretsiz bir sanal makine (aslında IDE ile kullanımımıza açılan) veren [c9.io](https://c9.io/) hizmetinin iyi bir tercih olacağını düşünüyorum. Hızlıca elektronik posta adresimiz veya diğer seçenekleri kullanarak bir hesap açabiliriz. Eğer hesabı açtıysanız yeni bir çalışma alanı açmaya hazırız demektir. [Kontrol paneline](https://c9.io/dashboard.html) üzerinden "Create a new workspace" seçeneği seçmeniz gerekiyor:

<a href="/images/2016-08-26-dotnetcore-fiziksel-kurulumsuz-kullanim/dashboard.png" title="cloud9 dashboard"><img src="/images/2016-08-26-dotnetcore-fiziksel-kurulumsuz-kullanim/dashboard.png" class="pure-img" alt="cloud9 dashboard"></a>

Çalışma alanına bir ad (Workspace name) ve açıklama (Description) ekledikten sonra isteğinize bağlı olarak size özel (Private) çalışma alanı yaratabilirsiniz. Gerekli araçları biz ekleyeceğimizden kalıp (Template) olarak boş (Blank) çalıma alanı seçiyorum:

<a href="/images/2016-08-26-dotnetcore-fiziksel-kurulumsuz-kullanim/create-a-new-workspace.png" title="cloud9 create a new workspace"><img src="/images/2016-08-26-dotnetcore-fiziksel-kurulumsuz-kullanim/create-a-new-workspace.png" class="pure-img" alt="cloud9 create a new workspace"></a>

İsmini vererek oluşturduğumuz çalışma alanı aşağıdaki gibi karşımıza çıkacaktır. Kısaca arayüzden bahsedecek olursam: Kırmızı ile işaretlemiş alan dosya ve klasörlerimizin listelendiği yer, yeşil ile işaretlenmiş alan açılan dosyaların sekmeli şekilde sıralanmış hali ve son olarak şimdi kullanacağımız yer olan mavi ile işaretlenmiş alan konsol komutlarını gireceğimiz uçbirim (bash terminal). Sarı ok ile gösterilen düğme ile uçbirimi tam ekran kullanabiliriz:

<a href="/images/2016-08-26-dotnetcore-fiziksel-kurulumsuz-kullanim/workspace.png" title="cloud9 workspace"><img src="/images/2016-08-26-dotnetcore-fiziksel-kurulumsuz-kullanim/workspace.png" class="pure-img" alt="cloud9 workspace"></a>

İlk olarak hangi sanal makineyi kullandığımızı öğrenelim:

```
aytac:~/workspace $ lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 14.04.3 LTS
Release:        14.04
Codename:       trusty
```

Buradan da öğrendiğimiz gibi sanal makinede Ubuntu 14.04 dağıtımı kullanıyor. 

```
aytac:~/workspace $ uname -a
Linux aytac-dotnetcore-3683701 4.2.0-c9 #1 SMP Wed Sep 30 16:14:37 UTC 2015 x86_64 x86_64 x86_64 GNU/Linux
```

64 bit komutları çalıştırabilen 4.2.0 Linux çekirdeğini kullanan bir sisteme sahibiz.

## .NET Core ve SDK

Şimdi proje geliştirme yapmamıza yarayan komutları ve platformun kendisini içeren .NET Core SDK paketini [resmi sitesinde anlatıldığı şekilde](https://www.microsoft.com/net/core#ubuntu) Ubuntu 14.04 için yükleyelim:

```
aytac:~/workspace $ sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ trusty main" > /etc/apt/sources.list.d/dotnetdev.list'

aytac:~/workspace $ sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
Executing: gpg --ignore-time-conflict --no-options --no-default-keyring --homedir /tmp/tmp.dnKQL6MPE9 --no-auto-check-trustdb --trust-model always --keyring /etc/apt/trusted.gpg --primary-keyring /etc/apt/trusted.gpg --keyring /etc/apt/trusted.gpg.d/fkrull-deadsnakes.gpg --keyring /etc/apt/trusted.gpg.d/git-core-ppa.gpg --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
gpg: requesting key 417A0893 from hkp server apt-mo.trafficmanager.net
gpg: key 417A0893: public key "MS Open Tech <interop@microsoft.com>" imported
gpg: Total number processed: 1
gpg:               imported: 1  (RSA: 1)

aytac:~/workspace $ sudo apt-get update
E: The method driver /usr/lib/apt/methods/https could not be found.
N: Is the package apt-transport-https installed?
```

Fakat `sudo apt-get update` komutunda bir sorun ile karşılaştık, bize sorduğu sorudan (`Is the package apt-transport-https installed?`) anlayacağımız gibi `apt-transport-https` paketini yüklememiz gerekiyor:

```
aytac:~/workspace $ sudo apt-get install apt-transport-https
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package apt-transport-https
```

Bir başka sorun daha. Komutun çıktısında `apt-transport-https` paketini bulamadığını bize söylüyor. Google aramalarında boğulup sorunun kaynağını öğrenmek yerine paketi el ile indirip kurmak daha hızlı ve enerji harcatmayacak bir çözüm olacaktır. Bende öyle yaptım:

```
aytac:~/workspace $ wget http://security.ubuntu.com/ubuntu/pool/main/a/apt/apt-transport-https_1.0.1ubuntu2.13_amd64.deb
.
.
.
2016-08-26 20:07:35 (2.09 MB/s) - ‘apt-transport-https_1.0.1ubuntu2.13_amd64.deb’ saved [25104/25104]

aytac:~/workspace $ sudo dpkg -i apt-transport-https_1.0.1ubuntu2.13_amd64.deb
Selecting previously unselected package apt-transport-https.
.
.
.
Setting up apt-transport-https (1.0.1ubuntu2.13) ...
```

Artık `apt-get update` komutu çalışacaktır:

```
aytac:~/workspace $ sudo apt-get update
Get:1 http://ppa.launchpad.net trusty InRelease [15.5 kB]
Get:2 http://security.ubuntu.com trusty-security InRelease [65.9 kB]           
.
.
.
```

Bu ufak sıkıntıyı atlattığımıza göre artık .NET Core SDK paketini yükleyebiliriz (paket adındaki sürüm yazıyı yazdığım tarihteki sürümüdür siz bunu okurken büyük ihtimalle daha yeni sürüm numarası olacaktır):

```
aytac:~/workspace $ sudo apt-get install dotnet-dev-1.0.0-preview2-003121
Reading package lists... Done
.
.
.
Setting up dotnet-host (1.0.1-1) ...
Setting up dotnet-hostfxr-1.0.1 (1.0.1-1) ...
Setting up dotnet-sharedframework-microsoft.netcore.app-1.0.0 (1.0.0-1) ...
Setting up dotnet-dev-1.0.0-preview2-003121 (1.0.0-preview2-003121-1) ...
.
.
.
```

## İlk Projeyi Yaratmak

Sonunda gerekli paketleri yüklediğimize göre ilk projemizi yaratabiliriz:

```
aytac:~/workspace $ mkdir dotnetcore
aytac:~/workspace $ cd dotnetcore/
aytac:~/workspace/dotnetcore $ dotnet new

Welcome to .NET Core!
.
.
.
Created new C# project in /home/ubuntu/workspace/dotnetcore.
```

## Projeyi Hazırlamak ve Kodu Çalıştırmak

Yukarıdaki komutlar sayesinde klasörde `Program.cs` ve `project.json` dosyaları yaratıldı. JSON dosyasındaki paketleri yükleyip hazırlaması için:

```
aytac:~/workspace/dotnetcore $ dotnet restore
log  : Restoring packages for /home/ubuntu/workspace/dotnetcore/project.json...
log  : Writing lock file to disk. Path: /home/ubuntu/workspace/dotnetcore/project.lock.json
log  : /home/ubuntu/workspace/dotnetcore/project.json
log  : Restore completed in 3002ms.
```

`Program.cs` dosyasındaki kodu derleyip çalıştırmak için ise:

```
aytac:~/workspace/dotnetcore $ dotnet run
Project dotnetcore (.NETCoreApp,Version=v1.0) will be compiled because expected outputs are missing
Compiling dotnetcore for .NETCoreApp,Version=v1.0

Compilation succeeded.
    0 Warning(s)
    0 Error(s)

Time elapsed 00:00:02.7805778
 

Hello World!
```

Artık ilk .NET Core projemizi bir sanal makine içerisinde derleyip çalıştırmış olduk. Uçbirimi tam ekrandan çıkarıp sol tarafta `dotnetcore` klasöründeki programın kodlarını değiştirip deneylerimize başlayabiliriz.

## Kullanım Verilerinin Toplanması

Eğer `sudo apt-get install dotnet-dev-1.0.0-preview2-003121` ve `dotnet new` komutlarının çıktılarının tamamına göz atarsanız (yazımın uzun olmaması için çıktıların bir kısımını sildim) sizinde dikkatinizden kaçmayacaktır. Çıktıların dediğine göre .NET Core Tools araçları kullanım verilerini bizim deneyimimizi iyileştirmek için toplamakta. Bunu anonim şekilde kendi sunucularına göndermekte. Bu konuda daha fazla bilgi için [https://aka.ms/dotnet-cli-telemetry](https://aka.ms/dotnet-cli-telemetry) adresi verilmiş. Eğer verilerin toplanmasını kapatmak istiyorsanız bize sunulmuş olan seçenek `DOTNET_CLI_TELEMETRY_OPTOUT` çevresel değişkeninin değerini `1` olarak atamamız. Bunu `.bash_rc` dosyasını değiştererek yapabilirsiniz. 