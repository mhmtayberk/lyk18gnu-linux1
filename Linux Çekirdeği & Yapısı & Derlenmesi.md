## Linux Çekirdeği & Yapısı & Derlenmesi

### Çekirdek

- şletim sisteminin çekirdeği, kullanıcı yazılımları ile donanım arasında bir aracıdır.

- Linux çekirdeği **monolitik (yek pare, tek parça)** bir yapıya sahiptir.

- Çekirdek tek ve tüm özellikleri içerisinde barındıran bir yapıya sahiptir.

- Linux çekirdeği, monolitik yapısını esnek duruma getirmek için istendiğinde yüklenebilir modüller kullanmaktadır.



### Çekirdek Sürümü

- `uname -r` -> Çekirdek sürümünü verir. uname -a ile biraz daha detaylı bakılabilir.

- **A.B.C**



| A                                                         |
| --------------------------------------------------------- |
| Çekirdeğin ana sürüm numarasıdır.                         |
| Çekirdekteki çok büyük değişikliklerle birer birer artar. |
| **B**                                                     |
| Çift sayı ise çekirdek kararlıdır.                        |
| Tek sayı ise çekirdek geliştirme aşamasındadır.           |
| Ana sürüm numarası değişirse sıfırdan başlatılır.         |
| **C**                                                     |
| Çekirdek revizyon numarasıdır.                            |
| Çekirdekteki küçük değişikliklerle birer birer artar.     |

- Örneğin 4.15.0-24-generic -> A : 4, B : 15, C : 0



### Modüllerle Çalışma - Bilgi Edinme

- Yüklü modülleri `lsmod` komutu ile görüntüleyebiliriz.

- Modül bilgilerini `modinfo modül` komutu ile görüntüleyebiliriz.



### Modüllerle Çalışma

- `insmod modül` -> Çekirdeğe modül yüklenebilir.

- `rmmod modül` -> Modülü çekirdekten kaldırmak için.

- `modprobe` -> Bir modülün başka modüller ile çalıştırılacağı zaman.

- `depmod -a` -> Modüllerin bağımlılık tanımları.



### Çekirdek RPM'inin Güncellenmesi

- Linux dağıtımları, çekirdek güncellemelerini düzenli olarak RPM paketleri olarak dağıtmaktadır.

- Güncel çekirdek RPM dağıtılmadan önce dağıtım üreticisi tarafından ilgili Linux sürümü ile uyumlu çalışması, kapsamlı şekilde test edilmektedir.

- Bu yöntemle çekirdek güncellenmesi, sıradan bir paketin güncellenmesi kadar basite indirgenmiş durumdadır.

- Çekirdek RPM'i kurulunca sistem yükleyicisinin yapılandırma dosyaları da güncellenmektedir.

- Güncelleme öncesi hangi çekirdek paketinin yüklü olduğunu kontrol etmek için; `rpm -qa | grep kernel`

- kernel-docs, kernel-utils paketlerinin eski sürümlerinin sistemde saklaması istenmiyorsa bu paketler `rpm -Uvh paket_adi.rpm` ile güncellenebilir.

- Sistem ext3 dosya sistemini ya da SCSI arabirimini kullanıyorsa, **initrd** imajının yaratılması gerekir.

- `zypper se kernel` komutu ile Kernel paketlerini görebiliriz.



### /proc Dosya Sistemi

- Linux, çekirdek bilgilerinin izlenmesi ve çalışma anında çekirdek parametrelerinde değişiklik yapılmasını sağlamak için /proc sanal dosya sistemini sunar.

- `/proc/cpuinfo` -> İşlemci hakkında bilgi.

- `/proc/modules` -> Kullanımda olan çekirdek modülleri.

- `/proc/filesystems` -> Kullanılmakta olan dosya sistemleri

- `/proc/loadavg` -> Sistem yükü ortalaması.

- `/proc/meminfo` -> Bellek ve kullanım bilgileri.

- `/proc/swaps` -> Takas alanı kullanım bilgileri.

- `/proc/uptime` -> Sistem çalışma süresi bilgileri.

- `/proc/version` -> Çekirdek ve gcc sürüm bilgileri.

- Çalışma anında çekirdek parametresini değiştirmek için;` echo "1" > /proc/sys/net/ipv4/icmp_echo_ignore_all`



#### Notlar

- Default kurulu bir Desktop sistemde derleyiciler gelmez.

- Hurd çekirdeği uzun süredir GNU projesi ile geliştirilen fakat hala kararlı bir sürüme ulaşamamış bir çekirdektir.

- DKMS (Dynamic Kernel Module Support)

- [kernel.org](http://kernel.org/) 'dan son çıkan Kernel çekirdeklerini ve eski sürümleri takip edebilir, kurabiliriz.

- Kernel yeni sürüme güncellendikten sonra uninstall edilmezse sistemde kalır ve bir önceki sürümünde sisteme giriş yapmak mümkün olur.

- **modprobe** ile modül yükleme işlemi yapılabilmekte.
