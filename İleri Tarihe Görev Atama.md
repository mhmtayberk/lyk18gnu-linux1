## İleri Tarihe Görev Atama

### Bir Seferlik Görev Ataması

- Bir seferlik görev ataması için `at` ve `batch` komutlarını kullanmaktayız.

- Görevin çalışma vakti geldiğinde otomatik olarak çalıştırılır.

- Linux sistemi üzerinde belirli bir zaman diliminde, tek seferlik çalışacak görev ataması yapmaktır.

### at Sunucusu ve İşleyişi

- at ve batch komutları atd hizmeti ile çalışmaktadır.

- at ve batch komutları kullanılırken atd hizmetinin on durumda olması gerekmektedir.

### Bir Seferlik Görev Atama, Listeleme ve Silme

at 0545pm Jul 28

cd /calisma

cp -f * /yedek

ctrl + d

- `atq` -> Kuyrukta bekleyen işleri gösterir.

- `atrm <numara>` -> Numarası belirtilen işi siler.

### Periyodik Görev Ataması

- Periyodik görev ataması `crontab -e` komutu ile yapılmaktadır.

- Linux sistemi üzerinde bir görevin belirtilen periyodik aralıklarla çalıştırmasıdır.

- crontab çalışırken cron demaon'ının sürekli çalışır halde olması gerekmektedir.

- /etc/crontab sistemin crontab dosyadır.

- Saatlik, günlük, aylık çalışmalar planlanabilir.

- Root ve kullanıcının crontab'ları kendi prompt'una yazılır.



### Örnekler

- `30 3**** cp -f /etc/passwd /etc/passwd.bak` -> Her gün saat 3'te çalışmakta.

- `0 0 15 ** echo "filtreleri temizle"` -> Her ayın 15. gününün 0. saatinin 0. dakikasında çalışır.

- Hafta içi her gün Pazartesiden Cumaya 5 gün çalışacak. Sabah 6:30'da çalışacak. -> `30 6 * * 1-5`



| Dakika (0-59) | Saat (0-23) | Ayın Günü (1-31) | Ay (1-12)Haftanın Günü (0-6)          (Pazar 0 veya 7) |     |
|:------------- | ----------- | ---------------- | ------------------------------------------------------ | --- |
| *             | *           | *                | *                                                      | *   |



### anacron Sunucusu ve İşleyişi

- crond hizmeti ile aynı işi yapar.

- anacron, crond'den farklı olarak sistemin 24 saat açık olacağını farz etmez.

- Periyoduk görevler /etc/anacrontab dosyasına yazılır.

- Sistem kapalıyken periyodik görevin çalıştırılma vakti geçtiyse anacron ilk açılışta bunu algılar ve görevi işletir.

- `periyod(gün sayısı) tekrar_sayisi_gorev_adi görev` şeklinde tanımlanır.





#### Notlar

- `crontab -l` ile crontab'a yazılmış görevler görüntülenebilir.

- cron başlatıldığı zamanı da dahil eder.

- Google'da crontab generator'ler mevcuttur.

- at ve batch komutu artık modern Linux'ların bir çoğunda mevcut değil.

- at veya batch komutları ile atanan görevler `atq` ile listelenebilir, `atrm` ile silinebilir.
