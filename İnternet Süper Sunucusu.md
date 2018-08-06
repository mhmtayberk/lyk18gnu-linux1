## İnternet Süper Sunucusu

- Bilgisayar kaynaklarının çok kısıtlı olduğu dönemde daha etkin kaynak kullanımı için geliştirilmiştir.

- Kullanılmayan ağ hizmetlerini çalıştırmaz, yalnızda gerektiğinde çalıştırır ve işi bitince durdurur.

- Bellek tasarrufu sağlar.

- Çok sayıda ağ hizmeti için bir vekil olarak çalışır.



### Bilindik Bağlantı Noktaları

- Bilindik bağlantı noktalarına ilişkin isim karşılıkları **/etc/services** dosyası içinde tanımlanmıştır.



### /etc/inetd.conf

- Geleneksel inetd sunucusu için ayar dosyası /etc/inetd.conf 'tur.

- Bu dosyanın her bir satırı hizmet adı soket protokol seçenek kullanıcı hizmet yazılımının tamyolu parametreler. Örneğin;

`ftp                stream        tcp        nowaitroot        /usr/sbin/in.ftp                in.ftpd`



### inetd ve Güvenlik

- Ağa sunulan her farklı hizmet yeni güvenlik risklerini de beraberinde getirir.

- Sistemde kullanılmayan ve ihtiyaç duyulmayan ağ hizmetlerini durdurmak için **/etc/inetd.conf** başlangıç yeridir.



#### Notlar

- xinetd'yi inetd'nin babası gibi telaffuz edebiliriz. 

- xinetd yapılandırması /etc/xinetd.conf dosyası ve /etc/xinetd.d dizini içeriği aracılığı ile gerçekleştirilir.
