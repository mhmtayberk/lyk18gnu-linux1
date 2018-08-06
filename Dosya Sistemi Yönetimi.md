## Dosya Sistemi Yönetimi

### Disk Bölümü ve Dosya Sistemi

- Diski farklı amaçlarla kullanılmasını sağlamak için oluşturulan mantıksal disk parçalarına disk bölümü denir.

- Dosya sistemi ise en az bir disk bölümü üzerine yerleşmiş, dosya ve dizinlerin belirli sistematik içerisinde depolanması için gerekli erişim denetimi altyapısını sağlayan yapıdır.

- Farklı amaçlar için geliştirilmiş pek çok dosya sistemi bulunmaktadır.



### Dizin Sıradüzeni

- UNIX, tek köklü bir hiyerarşiye sahiptir.

- Enterprise Linux Dağıtımları, Filesystem Hierarchy Standard (FHS)'ye göre yapılandırma sunar. (/etc /bin /sbin /lib /dev /proc /mnt /opt /usr /var)

- /tmp dizini ayrı bir dosya sistemine bağlanmalı.

- /var dizini yazıcı, kayıt e-posta sunucusu olarak kullanılacaksa ayrı bir dosya sistemine bağlanmalı.

- /home dizini dosya sunucusu olarak kullanılacaksa ayrı bir dosya sistemine kotalı olarak bağlanmalı.

- /tmp'de her kullanıcının +x yetkisi kendinedir. Ortak bir çalışma alanı olarak düşünülebilir. (chmod +t / Sticky Bit)



### Takas Alanının Etkinleştirilmesi (swap)

- UNIX sistemler bazı durumlarda bazı process'leri bellekte tutmak yerine swap'te tutmayı tercih eder. Bu sayede bellek (RAM) boşta kalır. RAM'in yetersiz kaldığı noktalarda oldukça faydalıdır.

- Veritabanı sunucusu olarak hizmet veren sistemlerde ne kadar RAM'in olursa olsun o sistem swap yapar. Çünkü orada kurulu olan veritabanı yönetim sistemi bazı kritik olmayan operasyonları zamana yayarak swap'te yapmayı tercih eder. (Örneğin indexing)

- `mkswap /dev/sda5` -> Swap alanını mount eder.

- `swapon /dev/sda5` -> Disk bölümündeki takas alanı sistem belleğine bağlanır.

- `swapoff /dev/sda5` -> Belleğe bağlanmış disk bölümü üzerindeki takas alanını bellekten ayırır.

- `swapon -s` -> Sistemde tanımlı takas alanlarının kullanım bilgilerini ve önceliklerini gösterir.



### Dosya Sisteminin Bakımı

- mount edilmiş bir diskin bakımı yapılamaz. Önce unmount edilmelidir.

- `fsck [-a] /dev/sda1` şeklinde kullanılır. Örneğin; `fsck /dev/sdb2`



#### Notlar

- `free RAM` kullanımını gösteren bir komuttur.

- `free -h` şeklinde bir kullanımı da bulunur.

- /etc'nin altındaki dizinlerde çalışma yapmadan önce muhakkak yedek alınmalıdır. (cp /etc/fstab /etc/sftab.old şeklinde olabilir.)

- Bir diski bir bölüme bağlamak için /etc/fstab üzerinde düzenleme yapılmalı. (Otomatik mount) (/dev/sdb2 /disk2 ext4 default 0 0 şeklinde olabilir.)

- Her ne olursa olsun disk bölümünü bağlamak için işlem yapıyorsak /etc/fstab'a disk bölümünün Block ID(UUID)'si yazılmalıdır. (Örneğin /sdb1 /sdc1 olsun sdb/1 diski çıkartıldığı zaman isimlendirme değişmekte.)

- `mount -a ve df -h` -> Tüm diskleri mount eder. df -h ile görüntülememiz mümkün.

- `swapon -a ve free` -> Tüm swapları mount eder. free ile görüntülememiz mümkün.

- fstab'a her zaman UUID isimleri ile kayıt yapılmalıdır. (`blkid` komutu ile **block id** numaraları görüntülenebilir.)
