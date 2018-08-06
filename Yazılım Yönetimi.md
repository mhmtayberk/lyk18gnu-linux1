## Yazılım Yönetimi

### Yazılım Yönetimi İhtiyacı

- Yazılım yönetimi, işletim sisteminin yazılımların yüklenmesi ve kaldırılması için sunduğu mekanizmadır.

- Bu mekanizma bize yazılımları güncelleme kolaylığı, kaldırma kolaylığı, yazılımın çalışması için gereken diğer yazılımları takip etme kolaylığı sunmaktadır.

| Dağıtım Hazırlayan                  |
| ----------------------------------- |
| **REPO**                            |
| **FTP (Release Dağıtımları / İso)** |
| **Image Hazırlayanlar**             |
| **Kontrol Grubu**                   |
| **Paket Hazırlayanlar**             |

> Tüm bu döngünün tamamı gönüllülük esası gerçekleşmektedir.

- `rpm -qa | wc -l` -> Sisteminizde kurulan tüm bu paket sayısının tamamı gönüllülük esası bazı aşamalardan geçmektedir. Ortalama **2000** repo'da **80.000** kişinin emeği bulunmakta.



### RPM (Redhat Package Manager)

| RPM'in Özellikleri                     |
| -------------------------------------- |
| Yeni yazılımların kaynak kodunu almayı |
| Kaynak kod / ikili biçimde paketlemeyi |
| Kolayca kurmayı                        |
| Kolayca takip etmeyi                   |
| Kolayca tekrar derlemeyi sağlar        |

| RPM Veritabanı                                        |
| ----------------------------------------------------- |
| Paketleri doğrulamak                                  |
| Paketler ve / veya dosyalar hakkında bilgi sorgulamak |



### Bilindik Paket Kaynakları

- Kurumsal Linux dağıtımları, sistem bütünlüğünün korunması amacıyla işletim sistemi ile birlikte gelen paketlerin kullanılmasını önermektedir.

- Bilindik paket dağıtımları Linux kurulum CD-ROM'larından ve FTP sunucularından, yansılarından elde edilebilir.



### Kurulu Paketlerin Sorgulanması

- `rpm -q paketadi` -> Kurulu bir paketin sorgulanması. Örneğin; rpm -q nano

- `rpm -qa` -> Sistemdeki tüm paketlerin sorgulanması.

- `rpm -qi paketadi` -> Kurulu paket hakkında detaylı bilgi alma. Örneğin; rpm -qi nano

- `rpm -ql paketadi` -> Kurulu paketin bileşenlerini sorgulama. Örneğin; rpm -ql nano

- `rpm -qf dosya` -> Bir dosyanın hangi pakete ait olduğunu sorgulama.



### Kurulum Öncesi Sorgulama

- `rmp -qpi paketdosyasi `-> Kurulu olmayan paket hakkında bilgi alma.

- `rpm -qpl paketdosyasi` -> Kurulu olmayan paket içeriği hakkında bilgi alma.

- `rpm -qpd paketdosyasi` -> Kurulu olmayan paketin belgelerini listeleme.



### Paket Kurma ve Kaldırma

- `rpm -i paketdosyasiadi` -> Paket kurmak için kullanılır.

- `rpm -i --force paketdosyasiadi` -> Paket kurmak için kullanılır. Bileşenleri de kurar.

- `rpm -e paketadi` -> Paket kaldırmak için kullanılır.

- `rpm -e --nodeps paketadi `-> Paket kaldırma için kullanılır. Bileşenleri de kaldırır.



### Paket Güncelleme

- `rpm -U patedosyasiadi` -> Paketi yeni sürüme yükseltmek için kullanılır.

- `rpm -U --oldpackage paketadi` -> Paketi eski sürümüne güncellemek için kullanılır.

- `rpm -Fvh paketdosyasiadi `-> Paketi yinelemek için kullanılır. Örneğin kopyalamayı unutup bozduğumuz dosyaları tekrar kullanılabilir hale getirmek için kullanabiliriz. Bir nevi fabrika ayarına döndürmektir.



### yum Aracı

- CentOS / Fedora / Redhat gibi dağıtımlarda RPM paketlerinin hızlı, pratik ve verimli bir yöntemle kurulabilmesini, paket bağımlılıkları yönetimi ve paket güncellemeleri sırasında konfigürasyon dosyalarının güncellenmesini sağlayacak bir araçtır.

- `yum search paket_adi` -> Paket arama.

- `yum install paket_adi` -> Paket kurma.

- `yum remove paket_adi` -> Paketi silme.

- `yum update paket_adi` -> Paketi güncelleme.



### zypper Aracı

- Suse Linux dağıtımlarında RPM paketlerinin hızlı, pratik ve verimli bir yöntemle kurulabilmesini, paket bağımlılıkları yönetimi ve paket güncellemeleri sırasında konfigürasyon dosyalarının güncellenmesini sağlayacak bir araçtır.

- `zypper se paket_adi` -> Paket arama.

- `zypper in paket_adi` -> Paket kurma.

- `zypper rm paket_adi` -> Paket silme.

- `zypper up paket_adi` -> Paket güncelleme.

- `zypper ref` -> REPO veritabanını güncelleme.

- `zypper up `-> Tüm paketleri yeni sürüme yükseltme.



### dpkg (Debian Paket Yönetim Sistemi)

- **.deb** uzantılıdır.

- Debian geliştirimi sırasında, kurulu paketlerin yönetimini sağlayacak bir sisteme ihtiyaç duyunca dpkg geliştirildi.



### dpkg - Kurulu Paketlerin Sorgulanması

- `dpkg -l `-> Kurulu tüm paketlerin sorgulanması.

- `dpkg --info paketadi.deb` -> Paket hakkında bilgi alma.

- `dpkg -p paketadi` -> Kurulu paket hakkında bilgi alma.

- `dpkg -L paketadi` -> Kurulu paketin bileşenlerini sorgulama.

- `dpkg -S dosya` -> Bir dosyanın hangi pakete ait olduğunu sorgulama.



### dpkg - Paket Kurma ve Kaldırma

- `dpkg -i paketadi.deb `-> Paket kurma.

- `dkpg -r paketadi `-> Paket kaldırma.



### Debian apt Aracı

- `apt-cache search paket_adi` -> Paket arama.

- `apt-get install paket_adi` -> Paket kurma.

- `apt-get remove paket_adi` -> Paket kaldırma.

- `apt-get update` -> REPO veritabanını güncelleme.

- `apt-get install --only-upgrade paket_adi` -> Kurulu paketi yeni sürüme yükseltme. Örneğin; apache hariç her şeyi güncelle ama apache'yi güncelleme.

- `apt-get upgrade` -> Tüm paketleri yeni sürüme yükseltme.



### Debian aptitude Aracı

- `aptitude search paket_adi` -> Paket arama.

- `aptitude install paket_adi` -> Paket kurma.

- `aptitude remove paket_adi` -> Paket kaldırma.

- `aptitude update` -> REPO veritabanını güncelleme.

- `aptitude upgrade paket_adi` -> Paketi güncelleme.

- `aptitude upgrade` -> Tüm paketleri güncelleme.



### Paylaşılan Nesneler

- Pek çok programın ortak kullandığı **rutinler** ya da program parçaları vardır.

- Bu kod kesimlerinin bellekte ve diskte defalarca yer kaplamaması için devingen bağlanan kütüphaneler geliştirilmiştir.

- Belleğe yüklenen bir **paylaşılan nesne (shared object)** tüm programlar tarafından kullanılabilmektedir.

- MS-Windows ortamındaki **DLL** dosyaları, UNIX ortamındaki paylaşılan nesnelere karşılık gelmektedir.

- UNIX'te paylaşılan nesneler genel olarak **.so** uzantısına sahiptirler.



### Paylaşılan Nesnelerin Kullanılması

- Paylaşılan nesneler ortak kullanım amacıyla **/lib**, **/usr/lib** ve **/usr/local/lib** dizinlerinde bulunur.



### Paylaşılan Nesne Bağımlılığı

- Bir programın paylaşılan nesne bağımlılığı **ldd** komutu ile öğrenilir.

- Örneğin; `ldd /usr/bin/rm`

- Örneğin; `ldd /sbin/fdisk`

- ldd sayesinde hangi rutinin eksik olduğunu gözlemleyebiliriz.



#### Notlar

- Yazılım Geliştiriciler <--> Alfa Tester <--> Beta Tester

- **Conflict :** Yazılım bağımlılığı. A yazılımının çalışması için B yazılımına bağımlı olması.

- `rpm -ql nano | wc -l` yazdığımız zaman nano editörün sistemimizde 69 farklı yere dosya koyduğunu görürüz. Eğer paket yönetimimiz olmasaydı nano editörü sistemden kaldırmak için bu 69 dosyayı tek tek silmemiz gerekecekti.

- rpm bir paket yönetim sistemidir, zypper, yum vs. ise birer araçtır.

- dpkg bir paket yönetim sistemidir, apt, apt-get vs. ise birer araçtır.

- dpkg'de paket pinlenebiliyor. rpm'de bu özellik mevcut değil.

- Open SUSE'de YaST ile kurulum DVD'sini repo olarak ekleyebiliyoruz.

- **Delta Kavramı :** Önce paketi alır, yeni paket ile kıyaslar ve aradaki farkları kıyaslar. Tüm paketi indirmek yerine aradaki farkları indirmiş oluruz. Bu sayede internet kullanımını azaltmış olur.

- [rpmfind.net](http://rpmfind.net/)

- [software.opensuse.org](http://software.opensuse.org/)

- REPO'da olmayan bir paketi kurmak için (Root) örneğin; `rpm -ivh nano-2.9.6-lp150.1.x86_64.rpm`
