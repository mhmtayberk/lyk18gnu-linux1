## Ağ  Ayarları

> UNIX ilk TCP/IP gerçekleştiriminin hazırlandığı işletim sistemidir.



### Ağ Arayüzleri

- Bilgisayarın, ağa bağlanmasını sağlayan **aygıt ağ arabirim kartı** dır.

- Çekirdek ağ arabirim kartlarını ağ programlarına ağ arayüzü olarak adlandırılan sanal bir aygıt olarak sunar.

- Her ağ arayüzünün çalışma biçimine göre farklı bir ismi vardır. (lo, eth0 eth1, ppp0 ppp1, dummy0 dummy1)

- Loopback : 127.0.0.1 (Kendi makinen)



### Arayüzlerin Listelenmesi

- `ifconfig -a` komutu ile görüntülenebilir.

- `ip` ile görüntülenebilir.

- `zypper install net-tool-deprecated `kurularak **ifconfig** kullanılabilir.



### Arayüzlerin Başlatılması ve Durdurulması

- `service network start | systemctl start network.service`

- `service network stop | systemctl stop network.service`

- `ifconfig eth0 up` -> Ağ arayüzünün başlatılması

- `ifconfig eth0 down` -> Ağ arayüzünün durdurulması



### Arayüz Yapılandırması

- Sistemdeki ağ arayüzleri ifconfig ile yapılandırılır.

  1. `ifconfig eth0 192.168.122.21`

  2. `ifconfig eth0 192.168.122.21 netmask 255.255.255.0`

  3. `ifconfig eth0 192.168.122.21 netmask 255.255.255.0 broadcast 192.168.122.255`

  4. `ifconfig eth0 hw ether 00:02:44:04:03:64`

- ifconfig ile yapılan yapılandırma sadece sistemin çalışma anı için geçerlidir, kalıcı değildir. (Bilgisayar reboot edilince çalışmalar kaybolur.)



### Arayüz Yapılandırma Dosyaları (debian / ubuntu)

- **/etc/network/interfaces** -> DHCP ile devingen IP adresi yapılandırması.

```
auto eth0
allow-hotplug eth0
iface eth0 inet dhcp
```

- **/etc/network/interfaces** -> Durağan IP adresi yapılandırması.

```
allow-hotplug eth0
iface eth0 inet static
adress 10.10.20.125
netmask 255.255.255.0
network 10.10.20.0
brodcast 10.10.20.255
gateway 10.10.20.2
```



### Arayüz Yapılandırma Dosyaları (suse / redhat)

- **/etc/sysconfig/network/ifcfg**-> Bağdaştırıcı isim



### IP Yönlendirme Yapılandırması (Routing)

- `route` -> Route tablosunu gösterir. (Yeni Linux'larda ip route)

- `route del default` -> Default route yapılandırmasını siler.

- `route add default gw 192.168.212.2 eno16777736` -> Yeni bir route tablosu oluşturur.

- İçerisinde Destination, Gateway, Genmask, Flags Metric, Ref, Use, Iface bilgileri bulunmaktadır.



### NIC Bonding / Network Teaming

- En basit anlatımla birden fazla ağ kartının tek ağ kartı gibi tanımlanmasıdır.

- Yüksek bant genişliği gereken durumlar.

- Continuity (Süreklilik/kesintisizlik)

- Ağlarda hız diye bir şey **YOKTUR!** Bant genişliği vardır. (10 Mbit -> 10 şeritli yol iken 30 Mbit -> 30 şeritli yoldur. Birim zamanda daha fazla data taşınır.)

- Bonding için minimum 2 ethernet kartı gereklidir.



### NIC Bonding / Network Teaming - Çalışma Modları

- Bonding modülü Linux işletim sisteminde çekirdek desteği ile gelir.

- 6 farklı çalışma modu vardır.

- Kartlar mode0'da round robin çalışır.

- mode0'da kart ethernet kartı bağlı ise trafik bu ethernet kartlarına rastlantısal olarak dağıtılır. Doğal olarak yük paylaşımı olur ve sistem hafifler.

- Çoğunlukla ilk 4 mod kullanılmaktadır.

- Bağlı olunan switch destekliyor ise NIC Bonding işlemi yapılabilir.

- Sunucunun IP adresleri interface'de yer alır, ethernet kartında yer almaz. (/etc)

| mode=0 (balance-rr)    | Yük paylaşımı ve hata toleransı.                                         |
| ---------------------- | ------------------------------------------------------------------------ |
| mode=1 (active-backup) | Aktif-yedek, amaç hata toleransı.                                        |
| mode=2 (balance-xor)   | Hangisinden gelirse oradan cevap, amaç yük paylaşımı ve hata toleransı.  |
| mode=3 (broadcast)     | Tüm kartlardan gönderir, amaç hata toleransı.                            |
| mode=4 (802.3ad)       | Bağlantı kümeleme, amaç daha büyük bir bant genişliği ve hata toleransı. |
| mode=5 (balance-tlb)   | Gelen trafik için, kartların yüküne göre dengeleme.                      |
| mode=6 (balance-alb)   | Gelen-Giden trafik için, kartların yüküne göre dengeleme.                |



### ARP ve Adres Çözümleme Tablosu Yönetimi

- ARP, IP adreslerine karşılık gelen donanım adreslerini bulmayı sağlayan bir protokoldür.

- IP adreslerine karşılık gelen donanım adresleri çekirdek tarafından otomatik olarak güncellenen bir tabloda tutulur.

- `arp` komutu ile tablo incelenebilir. 

- arp komutu ile tabloya değişmez biçimde eklemeler yapılabilir.

- `arp -a` -> Tüm arp tablosu görüntülenir.



### Ağ Bağlantılarının Durumu

- `netstat` ile ağ bağlantıları hakkında detaylı bilgi alınabilir.

- netstat'ın günümüzdeki karşılığı ip ve ss komutudur.

- `ss -l` -> Dışa açık portları listeler. Aynı işlem netstat -ntap ile yapılabilir.

- `netstat -rn` -> Routing table'ı görüntüler.

- `netstat -i` -> Arayüzü görüntüler.



### Ağ Sorunlarının Gözlenmesi

- `ping <IP/URL>`

- `traceroute <IP/URL>` -> Paketlerin nereden gittiğinin takibi için kullanılır.



### DNS Kayıtlarının Sorgulanması

- `nslookup` DNS kayıtlarının etkileşimli sorgulanması için kullanılır.

- `set q=mx` -> Mail Exchanger sorgulaması yapar.

- `host <MX adresi>` -> IP adresini verir.

- `server <IP>` -> Sorgu yapılacak IP adresini değiştirir. (Örneğin server 8.8.8.8)

- `host -t ns <URL>` -> Name Server adreslerini sorgular.



### Diğer Ağ Komutları

- `hostname` -> Sistemin hostname'ini gösterir.

- `hostname egitim1.mhmtayberk` -> Sistemin hostname'ini değiştirir.

- `hostnamectl set-hostname egitim.mhmtayberk` -> Sistemin hostname'ini kalıcı olarak değiştirir.

- `dig` ile ilişkili DNS bilgileri sorgulanır.

- `dig <URL> +short` -> Sistemin yayın yaptığı IP adresini verir.

- `dig <URL> mx +short` -> Sistemin MX kayıtlarını gösterir.

- `dig <URL> soa +short` -> Sistemin SOA kayıtlarını gösterir.



#### Notlar

- UNIX'i ağa dahil etmek için 4 adet bilgiye ihtiyaç vardır. (IP, Netmask, Gateway, DNS)
 -IP internetteki kimliklerimizdir.
 -Netmask veya Subnetmask ağın büyüklüğünü belirlemek için kullanılır. Ayrıca Netmask kullanımı ile iki farklı IP adresinin aynı mı       yoksa farklı ağlarda mı olduğu belirlenebilir.
 -Gateway internete çıkış kapımızdır. Gatewaye routerımızın IP adresini verdiğimiz de farklı ağlarda bulunan IP adreslerine ait           paketleri bilgisayar bu adrese gönderir.
 -DNS hostname-IP eşleşmesini sağlar. DNS sunucuları sayesinde kolayca internet adreslerini kullanırız.
  
- DHCP otomatik IP atamada önemli rol oynar.

- DHCP, IP atarken, aynı zamanda bunu kaydını tutar.

- Bir ethernet kartına birden fazla IP adresi konumlandırmak için IP Aliasing yapılır.

- 255.255.255.0 bulunduğu class'ın tamamı demektir. Yani /24'tür.
  -Mantığı ise ikilik düzenden gelir.

- 192.168.10.15 gibi bir IP adresi var ise Network adresi 192.168.10.0'dır. Broadcast'i tanımlı IP'nin son geçerli adresidir. Yani 192.168.10.255'tir.

- Google'da subnet hesaplama ile ilgili araçlar bulunmakta. Ip Subnet Calculator şeklinde bir arama ile pek çok araç bulunabilir.

- `ifconfig eno16777736:1 10.11.0.23 netmask 255.255.0.0 broadcast 10.11.255.255 up`

- İsim çözümlemesi **/etc/hosts** altında yapılabilir.

- İsim çözümlemesinde (resolver) değişiklik yapmak için **/etc/resolv.conf** dosyasında değişiklik yapılabilir.

- **/etc/nsswitch.conf**
