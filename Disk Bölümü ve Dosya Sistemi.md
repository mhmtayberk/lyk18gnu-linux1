## Disk Bölümü ve Dosya Sistemi

### Belli Başlı Dosya Sistemleri

- NTFS

- FAT32

- FAT16

- VFAT

- HPFS -> OS X

- ExFAT

- EXT 2,3,4

- ZFS -> Storage

- XFS

- SYSV -> Xenix



### Dosya Sisteminde Tutulan Bilgiler (Index)

- Dosya Adı (File Name)

- Boyut (File Size)

- Oluşturulma Tarihi (Creation Time)

- Son Erişim Tarihi (Access Time)

- Son Değişiklik Tarihi

- Dosya Sahibi (Owner, Group)

- Yetkilendirmeler (Permission)

- Dosyanın Konum Bilgisi



### Veriyi Diskten Silmek Ne Anlama Gelir?

- Index bilgisinin silinmesi anlamına gelir. Data aslında tam anlamıyla kaybolmaz. Üstüne yeni bir index bilgisi yazıldığı zaman veri silinmiş anlamına gelir.



### Silinen Veriyi Kurtarmak Ne Anlama Gelir?

- Index bilgisinin yeniden oluşturulması anlamına gelir.



### Ortak Nokta

- FAT32 ortak bağlamda bütün işletim sistemlerinde çalışmaktadır. Ancak 4 GB'dan daha büyük dosyalar yazılamamaktadır.

- exFAT'ta daha büyük dosyalar yazılabilmektedir ve bütün işletim sistemlerinde çalışmaktadır. (Ubuntu'ya ufak bir paket kurmak gerekmekte)

- exFAT eski Mac OS sürümlerinde çalışmamaktadır.



### Disklerin Yönetilmesi (fdisk) / Disk Bölümleme, Disk Türünü Değiştirme, Disk Formatlama, Disk Kurma İşlemleri

1. `su`

2. `fdisk -l` komutu ile sistemde kaç adet disk olduğunu görüntülüyoruz.

3. `fdisk /dev/sdb`

4. `m` tuşuna basarak yardım menüsüne erişebilirsiniz.

5. `n` tuşuna basarak yeni bir partition oluşturma ekranına gelebiliriz. Burada bize diskin Primary veya Extended (Genişletilmiş) mı olacağını soruyor.

6. `p` yazıp yani Primary seçip enterlıyoruz.

7. Kaçıncı partition olacağını soruyor. `1` yazıp enterlıyoruz.

8. Direkt `enter`'a basarak sektörleri ayarlıyoruz.

9. Boyut seçiyoruz. `+500M` yazdık.

10. `500M` oluşturuldu şeklinde bir bilgilendirme mesajı aldık. (/dev/sdb1)

11. `p` tuşuna basarak yaptığımız işlemi listeliyoruz.

12. Bu kez aynı işlemleri yaparak (p yerine e seçiyoruz) extended bir partition oluşturduk. Ve bütün boyutu verdik bunun için boyut sorduğunda direkt enter'lıyoruz.

13. Partition 2 (/sdb2)'nin dosya tipini NTFS olarak değiştireceğiz.

14. `t` tuşuna basıyoruz ve devam ediyoruz.

15. Diskimizi seçiyoruz biz `2` dedik.

16. `L` diyip enter'lıyoruz.

17. Karşımıza gelen tablodan NTFS'yi bulup seçiyoruz. `7` diyip enterlıyoruz.

18. Ve diskimizin tipi NTFS olarak değişmiş olmalı.

19. `w` tuşuna basıp enter'lıyoruz ve yaptığımız işlemleri diske kaydediyoruz.

20. `fdisk -l` ile kontrol ediyoruz.

21. `mkfs.ext4 /dev/sdb1` komutu ile sdb/1 disk bölümünü formatlayabiliyoruz.

22. Bu listenin tamamı için komut satırına mkfs. yazıp TAB TAB yaparak görebiliriz.

23. mkdir /disk2 ile kök dizine bir disk2 adında bir dizin oluşturuyoruz.

24. `mount /dev/sdb1 /disk2` komutu ile sdb1 partition'unu disk2'ye kurduk.

25. `df -h`



### Disklerin Yönetilmesi (gparted)

- gparted bir X Window gerektiren yazılımdır.

- Görsel arayüze sahiptir.



### /home'a Yeni Disk Bağlamak

1. Diski bölümle.

2. Disk bölümüne bir dosya sistemi oluştur.

3. Disk bölümünü geçici dizine bağla.

4. Sistemi tek kullanıcı moduna çek.

5. /home'un altındaki her şeyi yeni disk bölümünü bağladığın dizine haklarıyla beraber kopyala. (cp -r -p)

6. Datayı kopyaladığın disk bölümünü sistemden ayır. (umount) Eğer üzerinde bir procsess işlem yapıyorsa bu işlem yapılamaz.

7. Diski /home dizinine bağla.

8. `fstab`'a ekle.



### Disket ve CD Sürücüleriyle Çalışmak (Supermount)

- Bağlanılmış dizinlerin içerisindeyken bağ çözülemez.

- cd - ile root'un ana dizinine ayrıldıktan sonra umount komutu çalıştırılabilir.



### Disk Kullanım Bilgileri

- Dosya sistemlerinin kullanım bilgilerini görüntülemek için `df` parametresi kullanılır. Örnek kullanımı; `df -k` şeklindedir.

- Dizinin kullanım bilgileri için `du` parametresi kullanılır. Örnek kullanımı; `du -h /usr` şeklindedir.



### Bağ Dosyaları

- Windows'taki kısayola benzer mantıktadır.

- Katı bağ ve sembolik bağ olmak üzere kendi arasında ikiye ayrılır.

- Katı bağın bir bağ olduğunu `ls -l` çıktısında ayırt edilemezken sembolik bağ ls -l çıktısında ayırt edilebilir.

- Bir verinin silinebilmesi için tüm katı bağların silinmiş olması gerekmektedir.

- `ln -s dosyaadi bagadi` -> Sembolik bağ bu komut satırı ile oluşturulur.

- `ln dosyaadi bagadi` -> Katı bağ bu komut satırı ile oluşturulur.

- Katı bağlar aynı disk bölümü içerisinde oluşturulabilir.

- Sembolik bağın dosya türü karakteri küçük L harfidir. (link'ten gelmektedir)

- Katı bağlar disk üzerinde yer kaplamaz. Ham veri olarak kayıtlı bulunmakta. Aynı verinin katı bağlarının hepsi aynı fiziki noktaya point eder.



### Aygıt Dosyaları

- **b**rw-rw---- : b yani block device anlamına gelmektedir. (Örneğin; hard disk)

- Mouse, klavye, yazıcı, disk vs.

- **c**rw-rw---- : c yani elle oluşturulmuş sanal bilgisayar parçaları.(Örneğin; terminal girişleri)



### Arşiv Komutları

- `tar` komutu sıkıştırma yapmaz.

- `tar -cvf arsiv.tar dosya/dizin` -> Dosya ve dizinleri "arsiv.tar" dosyası içine arşivler.

- `tar -tvf arsiv.tar` -> Arşivin içerisindekiler listeler.

- `zip -r arsiv` -> Dosya ve dizinleri "arşiv.zip" dosyasına sıkıştırır.

- `gzip -9 arsiv` -> Dosya ve dizinleri "arşiv.gz" dosyasına sıkıştırır. gunzip arsiv.gz ile arşiv dosyası çıkarılır.

- `bzip2 -9 arsiv` -> Dosya ve dizinleri "arşiv.bz2" dosyasına sıkıştırır. bunzip2 arsiv.bz2 ile arşiv dosyası çıkarılır.

- `7z a arsiv` -> Dosya ve dizinleri "arşiv.7z" dosyasına sıkıştırır.

- `xz -z arsiv arsiv.xz` -> Dosya ve dizinleri "arşiv.xz" dosyasına sıkıştırır.

- `compress arsiv` ->Dosya ve dizinleri "arşiv.Z" dosyasına sıkıştırır. uncompress dozya.Z ile arşiv dosyası çıkarılır.



#### Notlar

- Eski anakart teknolojilerinde iki adet kablo üzerinde diskler takılabiliyordu ve bu dikler Master, Slame ve Cable Slame olarak Jumper üzerinden düzenlenebiliyordu.

- Bu eski teknolojide 4 veya 4'ten fazla disk bağlanamıyordu.

- Pata'dan sonra Sata geliştirildi.

- Eski teknolojide; /dev/hda, /dev/hdc, /dev/hdd olan dosya düzeni SATA ile birlikte /dev/sda, /dev/cdc..... şeklinde değişti. Ve artık istenildiği kadar disk takılıp çıkartılabilir hale geldi.

- Bir disk en fazla 4 birincil bölüme ayrılabilir. /dev/sda1, /dev/sda2, /dev/sda3, /dev/sda4.

- **Extended Partition** : n tane disk bölümü oluşturulabilir. /dev/sda5, /dev/sda6, /dev/sda7......

- Örneğin /dev/sda1 extended edilirse bunun altındaki bölümler /dev/sda5.... şeklinde devam eder.

- Ext3 ve RaiserFS transaction ve kayıt temellidir.

- Bir veri sistem içinde bir yerden bir yere taşındığı zaman yalnızda dosyanın index'indeki konum bilgisinin değiştirilmesi anlamına gelir.

- Partition Table : Bölüm bilgisi tablosu.

- UNIX içinde bulunan her şeyi /dev/device içerisine bağlar.

- `wc -l` dosyaadi komutu ile dosyanın satır sayısını öğrenebilirsiniz.

- `seq <karakter> <adet> > <dosyaadi>` komutu ile dosyanın içerisi doldurulabilir.

- Komut satırında & ayracı ile birden fazla komut kullanılabilir.

- `history` komutu ile terminalde son girilen komutları görmek mümkün.

- **7z** başarılı bir arşiv programıdır. Hem hızlı çalışır hem de boyutu oldukça düşürür.

- Bir dosyayı önce tar ile sıkıştırıp daha sonra başka bir sıkıştırma programı ile tekrar sıkıştırmak mantıklı olabilmekte.

- tar'ı tek backup almak için kullanabiliriz.

- **Tape Backup Unit** : Yüksek kapasiteli manyetik kaset. tar komutu ile aktarılabiliyor. Uzun ömürlü veri saklamak için ideal.
