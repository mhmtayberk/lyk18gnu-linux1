## Bind İle DNS Hizmetleri

### DNS Temelleri

- İnternet'te bilgisayarlara iki şekilde ulaşılmaktadır. (IP adresi ve ismiyle)

- DNS isimleri IP adreslerine dönüştürür.

- IP adreslerini isimlere dönüştürür.

- E-Posta yönlendirmelerinin tarif edilmesini sağlar.

- UNIX'ye DNS hizmeti genellikle bind yazılımı ile sağlanır. Bind internet kadar eski bir yazılımdır.



### DNS Ne Zaman Kullanılır?

- Bir ağ internete bağlı ise DNS kullanılmalıdır. Ağda bir DNS sunucu bulundurabilir ya da bulundurmayabilir.

- Ağ internete bağlı değilse ve büyük bir ağ ise kullanılmalıdır. Gelecekte farklı ağlara ya da internete bağlanma ihtimali varsa DNS kullanılmalıdır.



### DNS Hakkında

- DNS sıradüzensel ve dağıtık bir yapıya sahiptir.

- Her düğümün adı 63 harf uzunluğunda olabilir.

- DNS'de kökten itibaren en uca kadar en fazla 127 fazla alt seviye bulunabilir.



### DNS Hakkında - Alan Adları

- DNS'de her bir alt ağaç bir alan adıdır.

- En üstteki DNS sunuculara **root servers** adı verilmektedir.

- Bir DNS sunucu, tüm bir alan adları ağacını tutabildiği gibi bazı alt dallarını farklı DNS sunucularının yönetimine devredebilir.



### DNS Nasıl Çalışır?

- Kullanıcı bir bilgisayara bağlantı kurmak ister.

- Kullanıcının verdiği bilgisayar adı DNS sunucusuna sorulur.

- DNS sunucusu yanıt verebiliyorsa yanıtı verir, veremiyorsa kök DNS sunucuya istemi iletir.

- DNS sunucudan istenen IP adresi istemciye iletilir.

- İstemci, DNS sunucusundan öğrenmiş olduğu IP adresi ile nihai sunucuya bağlantı kurar.

- Her istemde kök sunucuya çıkılarak gereksiz DNS trafiği yaratılmamaktadır.

- Bir DNS kaydı bir kez öğrenildiğince yaşam süresi (TTL) boyunca DNS sunucunun ön belleğinde (cache) saklanır.

- Aynı ismin IP adresi karşılığı yeniden istendiğinde DNS sunucusu ön belleğindeki kaydı cevap olarak verir.



### Birincil ve İkincil DNS Sunucuları

- **Master :**

- Alanın ana DNS sunucusudur.

- Tüm kayıtları tutar, güncellemeler üzerinde yapılır.

- **Slave :**

- Alanın yardımcı DNS sunucusudur.

- Bilgileri Primary Master sunucudan indirir.



### Bind DNS Sunucusu

- BIND (Berkeley Internet Name Domain), DNS hizmeti sunan bir sunucu hizmet yazılımıdır.

- İnternetin yaklaşık %96'sı BIND'dır.



### Genel Bind Ayarları

- **options** bölümünde genel BIND yapılandırması yer alır.

- zone bölümleri her bir zone'a ilişkin yapılandırmayı içerir. (Bu sunucunun zone için nasıl bir sunucu olduğu, zone bilgilerinin hangi dosyada tutulduğu.)



### Zone Tanımı

- Birincil DNS sunucusu için zone tanımı örneği;

```
zone "mehmetayberk.com" IN {
type master;
file "/var/lib/named/master/mehmetayberk.com.zone";
allow-transfer {10.10.10.102;};
notify yes;
};
```

- İkincil DNS sunucusu için zone tanımı örneği;

```
zone "mehmetayberk.com" {
type master;
file "/var/lib/named/slave/mehmetayberk.com.zone";
allow-transfer {10.10.10.102;};
};
```



### Bind Düz ve Ters Zone Tanımlamaları

- İsimden IP öğrenme sorguları -> Düz DNS sorguları

- IP'den isim öğrenme sorguları -> Ters DNS sorguları

- Düz DNS sorgusunda -> STR

- Ter DNS sorgusunda -> PTR



### Güvenlik Düzenlemeleri

- **/etc/named.conf** dosyasındaki options bölümünde;

- DNS istemi kabul edilecek istemciler belitrilebilir : 

  ```
  allow-query { 192.168.200.0/24; localhost; };
  ```

  

- zone dosyası transferi yapmaya yetkili secondary DNS sunucuları belirtilebilir : 

  ```
  allow-transfer { 192.168.200.114; localhost; };
  ```

  

- özyineli sorgular yalnızca belirli IP blokları ile kısıtlanabilir : 

  ```
  allow-recursion { 192.168.200.0/24; localhost; };
  ```

  

### Bind'in Çalıştırılması

- DNS Servisini Başlatmak :

  ```
  /etc/rc.d/init.d/named start
  /etc/init.d/bind9 start
  systemctl start named.service
  ```

  

### Bind ile Round-Robin Yük Paylaşımı

sunucu1            A            10.10.10.101

sunucu2            A            10.10.10.102

sunucu3            A            10.10.10.103



### SUSE Linux DNS Sunucu Kurulumu

- Gerekli paketler `zypper in bind bind-utils` komutu ile kurulabilir.

- DNS sorgulama komutları işimize yarayacaktır. (host, nslookup, dig)



#### Notlar

- Servis sağlayıcı değiştirilirken IP bloğunun değişmesi istenmiyorsa RIPE'dan IP bloğu talep etmeli.

- RIPE'ın ellinde IPv4 adresi kalmadı. Fakat iade halinde gelen ufak IP blokları alınabilir.

- Bir master beş slave olabilir. (Örnek olarak)

- **/etc/named/root.hinds** -> Root server bilgileri yer alır.

- **SOA** -> Yetki başlangıcı bilgileri.

- **NS** -> İsim sunucusu tanımı.

- **MX** -> Mail Exchanger.

- allow-transfer işlemi IP Spoofing ile atlatılabilir. Bu sayede Zone kayıtları download edilir. Bunu önlemenin en güzel yolu Auth. doğrulamasıdır. DNS sunucu konfigürasyonuna anahtar eklenerek yapılabilir.

- Restart yapılınca cache silinir.

- Cache RAM'e tutulur. Çünkü hızlı cevap vermesi gerekmekte.
