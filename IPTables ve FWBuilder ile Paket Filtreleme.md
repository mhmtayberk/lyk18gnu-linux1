## IPTables ve FWBuilder ile Paket Filtreleme

### Netfilter ve IPTables

- netfilter, 2.4.x ve 2.6.x serisi Linux çekirdeği içinde tümleşik olarak bulunan güvenlik alt sistemidir.

- netfilter, iptables aracı kullanılarak yapılandırılır.

| netfilter Alt Sisteminin Becerileri                   |
| ----------------------------------------------------- |
| Durum korumalı veya durum korumasız paket filtreleme. |
| Ağ adres dönüşümü.                                    |
| IP maskeleme.                                         |
| Paket değiştirme ve işaretleme.                       |

### IPTables Kurallar

- **ACCEPT (Kabul Et)** -> IP paketine izin verilir.

- **DROP (Düşür)** -> IP paketi düşürülür.

- **REJECT (Reddet)** -> IP paketi reddedilir.

- **QUEUE (Kuyrukla)** -> IP paketi daha ayrıntılı işlenmek üzere kullanıcı alanına gönderilir.



### IPTables Kural Yazım Biçimi

- `iptables [-t tabloadi] komut zinciradi`

- `iptables -t filter -P INPUT DROP`

- `iptables -A INPUT -s 192.168.0.0/24 -j ACCEPT`

- `iptables -A OUTPUT -d 10.1.10.12 -j REJECT`

- `--reject-witch icmp-net-unreachable`



### IPTables Komut Seçenekleri

- **-A** : Ekle

- **-C** : Kontrol

- **-D** : Sil

- **-E** : İsim değiştir

- **-F** : Seçilen tablodaki kuralları boşalt

- **-H** : Yardım

- **-I** : Belirtilen konuma ekle

- **-L** : Listele

- **-N** : Yeni zincir yarat

- **-P** : Öntanımlı kural politikası belirle

- **-R** : Üzerine yaz / değiştir



### Kuralların Kaydedilmesi

- iptables ile girilen kurallar çalışma anı için geçerlidir.

- Tanımlı kuralları kalıcı kaydetmek için; `service iptables sve`



### Durum Korumalı Paket Filtreleme

- Tek tek tüm IP paketlerinin filtrelenmesi yerine bağlantı oturumu bazında filtreleme yapma.

- Bağlantı türüne göre uygulanacak kural devingen olarak seçilebilir.

- Etkinleştirilmesi için tek bir kuralın yazılması yeterlidir.

- netfilter/iptables, durum korumalı paket filtreleme özelliğini içermektedir.

`iptables -A INPUT -o eth0 -m state --state ESTABLISHED,RELATED`



### Ağ Adres Dönüşümü (NAT)

- Sistem üzerinden geçen tüm paketlerde hedef/kaynak dönüştürülmesi gerçek zamanlı olarak yapılabilmektedir.

- Ağ adres dönüşümü iki biçimde yapılabilir.

- SNAT (POSTROUTING)

- DNAT (PREROUTING)



#### Notlar

- Firewall'lar minimum üç bacaklı olmalıdır. Bunlar (Internet, LAN ve DMZ)

- Yazılan kurallarda yalnızca internet LAN arasına değil internet, DMZ ve LAN, DMZ arasına da kurallar yazılmalıdır.

- Zyxel, Fortigate, Cyberoam, Dell, Berq sıkça kullanılan bazı Firewall çözümleridir.

- Karmaşık güvenlik uygulamalarının kolaylıkla yapılandırılabilmesi için FWBuilder programı oldukça işlevsel olacaktır.

- `iptables -L -n` -> Sistemde kullanılan IPTables kurallarını listeler.

- `iptables -F` -> Tüm kuralları devre dışı bırakır.

- `nano -v `-> Read only açar.
