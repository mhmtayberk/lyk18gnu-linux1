## Sistem Kayıt Sunucusu

### Sistem Kayıt Sunucusu Nedir?

- UNIX sistemleri ve üzerlerinde çalışan süreçler durum raporu, uyarı ve hata iletilerini sistem kayıt sunucusuna gönderirler.

- Sistem kayıtlarının tutulabilmesi için **syslogd** sürecinin çalışıyor olması gerekmekte.



### Kayıt Türleri

- **auth** : Kullanıcı doğrulaması.

- **authpriv** : Kullanıcı yetkilerinin yükseltilmesi.

- **cron** : cron ve at sunucularından gelen kayıtlar.

- **daemon** : Sunucu yazılımlarından gelen kayıtlar.

- **kern** : Çekirdekten gelen kayıtlar.

- **lpr** : Yazıcı hizmeti sunucusundan gelen kayıtlar.

- **mail** : E-Posta hizmeti sunucularından gelen kayıtlar.

- **news** : Usenet (Haber Grupları) hizmet sunucularından gelen kayıtlar.



### Kayıt Öncelikleri

- **debug**: Hata ayıklama bilgisi.

- **info** : Bilgilendirme.

- **notice** : Kayda değer bilgi.

- **warning** : Uyarılar.

- **error** : Hatalar.

- **crit** : Kritik durumlar.

- **alert** : Alarma geçilmesini gerektirebilecek durum.

- **emerg** : Acil durum.



### syslog Yapılandırması - /etc/syslog.conf

- Kurallar Tür ve Öncelik olmak üzere iki alandan oluşur.

- Sıradan dosya için **/** ile başlayan tam yol verilmelidir.

- Named pipe'lar için **|** ile başlayıp bir komut ile takip eder.

- Terminal veya konsol için aygıt dosyası yazılır. (/dev/console)

- Uzak bilgisayar için önüne **@** konulmalıdır.

- Birbirinden virgül ile ayrılmış kullanıcı listesi.

- Tüm kullanıcılar için * kullanılır.

- `*.*@uzakkayit` -> Bu **ASLA** kullanılmaması gereken bir yapıdır.



### Kayıt Dosyaları ve Kayıtların İncelenmesi

- Kayıt dosyaları salt metin dosyalarıdır. -> `tail -f /var/log/messages`

- Kayıt dosyalarını okuyarak anlamlı raporlar haline getiren onlarca ticari - açık kaynak kodlu yazılım mevcut. (Metin işleme komutlarını bilen bir sistemci buna ihtiyaç duymaz.)

- RedHat Enterprise Linux içerisinde **redhat-logviewer** aracı bulunmakta.



### Merkezi Kayıt Sunucusu Kullanımı

- Sistem kayıtları merkezi bir kayıt sunucusuna ağ üzerinden gönderilebilmektedir.

| Merkezi Kayıt Sunucusu Kullanmanın Getirileri                                                                   |
| --------------------------------------------------------------------------------------------------------------- |
| Tüm sunucu parkının kayıtlarını merkezi bir yerde toplama / inceleme imkanı sunar.                              |
| Güvenlik zafiyetinden faydalanan saldırganın sistem kayıtlarını silmesinden etkilenmemesi gibi avantajı vardır. |

| Merkezi Kayıt Sunucusu Çalıştırabilmek İçin                                                       |
| ------------------------------------------------------------------------------------------------- |
| Merkezi sunucunun başka sistemlerden kayıt dosyası kabul edecek şekilde yapılandırılması.         |
| Kayıt dosyası üreten sistemin başka bir sistem üzerine kayıt gönderecek biçimde yapılandırılması. |

- Sunucu yapılandırması **/etc/sysconfig/syslog** dosyasında aşağıdaki biçimde güncelleme yapılmalıdır : 

```
SYSLOGD_OPTIONS="-r -m 10"
```

- `service syslog restart` ile hizmet yeniden başlatılmalıdır.

- İstemci yapılandırması için **/etc/syslog.conf** için : 

```
*.*   @kayitcibasi.egitim.mhmtayberk.com.tr
```



### rsyslog Nedir?

- rsyslogd, syslogd'nin geliştirilmiş halidir.

- rsyslog kullanarak, logları MySQL, postgreSQL, Orace vs. gibi veritabanlarına yazdırabiliriz.

- **/etc/rsyslog.conf** dosyasından yapılandırılabilir.

- Yapılandırma direktifleri syslogd direktifleri ile benzerdir.



### Kayıtların Rotasyonu

- Kayıt dosyaları, boyutlarının aşırı büyümesinin önüne geçmek için zaman zaman otomatik olarak rotasyona tabi tutulurlar.

- Ön tanımlı rotasyon süresi bir haftadır ve en son rotasyona tabi tutulmuş dört kayıt dosyası sistemde saklanır.

- Özellikle sunucu sistemleri için rotasyon sürelerinin uzun tutulması anlamlı olacaktır.

- Kayıtlı rotasyonu yapılandırması **/etc/logrotate.conf** dosyası içinden yapılır.

- Rotasyon yapılandırma dosyaları **/etc/logrotate.d** dizini içinde tutulurlar.

- Örnek bir /etc/logrotate.conf dosyası aşağıdaki gibidir : 

```
#Rotasyon sıklığı (weekly | daily | monthly)
weekly
#Son kaç rotasyon kaydının saklanacağı
rotate 4
#Eski kayıt dosyaları rotasyona tabi tutulduğunda yenileri boş olarak yarat
create
#Eski kayıt dosyalarını gzip ile sıkıştır
compress
#Her uygulamanın kayıtları için ayrı rotasyon ayar dosyalarının içerileceği dizin
include /etc/logrotate.d
```



### Last ve Dmesg

- `last` komutu ile kullanıcıların sisteme giriş / çıkış zamanları izlenebilir. Örnek kullanımı; `last -20`

- `dmesg` komutu ile çekirdek bilgilendirme alanında bulunan son çekirdek mesajlarının listesini gösterir. Örnek kullanımı; `sudo dmesg | less`



#### Notlar

- **/var/log** bölümünün ayrı bir disk bölümünde tutulmasında fayda var. 

- Log kayıtlarını belirli aralıklarla temizlemekte fayda var.

- Log yönetimi ciddi bir konudur. Kayıt rotasyonunun yanlış yapılmasının hukuken ciddi cezaları bulunmaktadır. Geçmişe yönelik log kayıt yapılandırması yapılırken dikkat edilmelidir.

- **xferlog** sunucuda FTP ile üzerinden değişiklik yapılan işlemleri gösterir.

- Hangi işletim sistemi işletiyor olunursa olunsun log tutma konusu ciddi anlamda önemli bir konudur.
