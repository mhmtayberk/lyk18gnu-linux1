## Sistem Servislerine İlk Adımlar

### systemd Nedir?

- systemd, Linux işletim sistemleri için geliştirilmiştir.

- Bilgisayardaki sistem ve servislerin çalışmasını organize eder.

- Ana Process, Deamon'ların ihtiyaç duyduğu ana soketleri Deamon'lar olmadan oluşturuyor.

- Bütün soketleri peşinen açıyor. (eş zamanlı) Bütün soketler açık olduğu için Deamon'lar birbirini beklemeden doğrudan açılmış oluyor.

- Eski sistemlerde Deamon'lar denetim yaparak açılıyordu. Yani bir servis başlamadan ona ihtiyaç duyan sıradaki servis başlatılamıyordu. Bu yüzden açılma gecikiyordu.



### systemd Yapısında Hizmet Süreçlerinin Yönetimi

- Hizmet süreçleri SUSE Linux altında iki uygulama ile kolayca yönetilebilmekte. Bu uygulamalar; systemtctl ve chkconfig aracı.

- systemcl'nin söz dizimi şu şekildedir; `#systemctl start | stop | restart | reload | status servisadi.service`

- `systemctl start hizmetadi` -> Hizmet başlatma.

- `systemctl stop hizmetadi` -> Hizmeti durdurma.

- `systemctl enable hizmetadi `-> Otomatik başlatma.

- `systemctl disable hizmetadi` -> Otomatik başlatmayı iptal etme.

- `systemctl mask hizmetadi` -> Servisi elle başlatmayı engelleme.

- `systemctl poweroff hizmetadi` -> Uyku moduna alma.

- `systemctl suspend  hizmetadi` -> Derin uyku moduna alma. (Destekli sistemlerde)

- `systemctl reboot hizmetadi` -> Hizmeti yeniden başlatma. (Destekli sistemlerde)



#### Notlar

- İkame için gereken servisler sırayla açılır.

- **Uyku Modu** : Açık olan tüm pencereler durur. Sistem en düşük enerji seviyesinde tekrar çalıştırılmayı tetikte bekler. Sistemin güç kaynağı kesilirse açık pencereler kaybolur.

- **Hibernate** : Açık olan tüm pencere, program, sistemler vs. (RAM'i işgal eden her şey) bir dump'ını alır ve kaydeder. Ardından sistemi tamamen kapatır. Kapanıştan sonraki ilk açılışta Kernel Post Check'ten hemen sonra Hibernate verisi okunur ve son kapatılma anındaki veriler getirilir.
