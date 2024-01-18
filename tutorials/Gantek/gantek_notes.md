## 26.09.2023 - Gantech Academy Eğitimleri

### Gerekli İndirmeler
1. Install VMWare Fusion
2. Install Ubuntu 22.04 Server Iso &rarr; for lightspeed version
3. Install Docker on Ubuntu 22.04 LTS Server


### Program Kaynakları

1. [Drive PDF Linkleri](https://drive.google.com/drive/folders/1E8p4rvxTbiRxlsgaoEzozzmQVcG2WwOA?usp=sharing)
   1. Rest API Uygulamaları ile ilgili dosyalar da bulunuyor. Program dosyaları vs burada bulunuyor.
   2. Hafta hafta tekrardan incele. Özellikle ilk haftanın konularını tekrardan araştır.

2. [Youtube Genel Bilgiler Videosu](https://www.youtube.com/playlist?list=PL2Ll3dKR1vYa8Wl9wJplw_4Fx45n4-yqj)

## 03.10.2023 - Gantek Academy Docker Eğitimi

* HyperV, windows sanal makinaları yönetmek için bir yazılım.
  * Windows subsystem?
  * wsl -install

* Docker Kurulumu
  * Docker yeni sürümü indirmek için Ubuntunun docker kısmından indiriyoruz
  * sudo apt update -> ubuntu update sitesine bağlanıp en son sürümdeki paketlerle karşılaştırıyor. Eski sürümde olanları güncellemek
istiyor. Yeni inenleri de indiriyor.
  * docker server da çalışmak için root yetkilerine ihtiyaç duyar. Bu docker için bir zaafiyet oluyor.
  * docker'ın root yetkilerinin getirdiği zaafiyetleri ortadan kaldıran ocp, kubernetes
  * alpine busybox araştır.
  * --tty
    * Tele TYpe Write
  * ``docker run -dit alpine`` &rarr; ``docker run --detach --tty --interactive alpine``
  * ``/var/lib/docker`` -> imagelar burada açılıyor.
  * ephemeral -> tüm konteynerlar vazgeçilebilir varlıklardır.
  * ``docker inspect <IMAGE>``driver: overlay2??? overlay file system
  * ``docker info``
  * docker arka planda dockerserver ile restapi üzerinden haberleştiği için aynı anda sadece 1 container üzerinde işlem yapma imkanı veriyor.
  * container çalışan sistemlerde swap özelliği nedir?
  * linux CFS (Completely Fair Scheduler)
* ``docker cp <filename> <image_id>:???``
* **docker image ları tar dosyası olarak standardize ediyoruz. Bunu cloud ortamında deploy edebiliyoruz. Docker güçlü bir paketleme yöntemidir. Her yerde docker image olarak deploy edebiliyoruz.**
* ``docker image tag <image_id> postgres:16.1`` -> image ların tag ler ile etiketliyoruz. Daha sonradan ekleyeceğimiz farklı versiyonlar ile update ediyoruz
* yerel olarak bir registry oluşturabiliyoruz. <<registry>> image docker üzerinden çekilebilir ``docker -v ``
* ``docker commit <image_tag> <new_iamge_name>`` ``docker save -o <filename>.tar <filename>`` iamge ları tar hale getirip registry üzerinde saklayabiliyoruz.

* nginx
  * nginx -> Rus birisi yazdığı için Avrupada kullanılmaz :)
  * 
---

### Kendime Notlar
* Monolith bir uygulamanını microservis mimarisine geçmesi uygulamanın baştan yazılmasını gerektirir.


* Tip-1 ve Tip-2 Hipervizörler
  * Tip-1
    * Donanım üzerine inşa edilir. Farklı işletim sistemi kurmaya olanak sağlar. Kaynak paylaşımının yapar.
  * Tip-2
    * İşletim sistemi üzerine inşa edilir. Aynı işletim sistemi üzerinde farklı ortamların kurulumuna olanak sağlar.

* KVM -> Kernel Virtualization Machine
---

#### Medium Yazı Fikirleri
* How to give a pasword to root user. The default root password is blank and is not reachable!
  * How to unset root user's passwd

*   * container çalışan sistemlerde swap özelliği nedir?
