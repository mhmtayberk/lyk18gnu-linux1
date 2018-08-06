## Dosya Sistemi Kotaları

### Kota Kavramı

- Kota, kullanıcıların veya grupların Linux dosya sistemi üzerinde belirlenenden daha fazla disk alanı kullanmasının ve disk bölümlerinin kontrolsüz dolmasının önüne geçmek için geliştirilmiş bir mekanizmadır.

- Dosya sunucularında, web sunucularında, FTP sunucularında, E-Posta sunucularında kota kullanım ihtiyacı vardır.

- Kotalar esnetilebilir (soft) ve esnetilemez (hard) kota olmak üzere ikiye ayrılır.



### Kullanıcı ve Grup Kotası

- UNIX'te disk kotaları kullanıcı ve grup kotası şeklinde iki çeşittir.

- `usrquota` ve veya `grpquota` seçenekleri ile bağlanması gerekir.



### Kota Düzeneğinin Kurulması

- **/etc/fstab** düzenlenmesi `/dev/sda2 /home/ext2 usrquota,grpquota 0 2`

1. `mount /home`

2. `cd /home`

3. `touch aquota.user`

4. `touch aquota.group`

5. `chown root:root aquota.user aquota.group`

6. `chmod 600 aquota.user aquota.group`

7. `quotacheck -cmug /home`

8. `quotaon /home`



### Disk Kotası Kayıtları

- Kota desteği olan her dosya sisteminin kökünde **aquota.user** ve/veya **aquota.group** kota kayıt dosyaları bulunur.

- Kayıt dosyalarının erişim yetkileri **600** modunda olmalıdır.

- Kayıt dosyalarının sahibi **root** kullanıcısı ve grubu da **root** grubu olmalıdır.



### Kota Raporları

- `repquota` ile bir dosya sistemindeki kotalar görüntülenebilir. Örnek; `repquota -a`



#### Notlar

- UNIX sistemlerde artık kota işlemi pek kullanılmamaktadır. Bunun sebebi sistem adminleri haricinde SSH vs. ile bağlanmasıdır. Sistem adminleri dışında başka kullanıcıların sistemlere bağlanmamasıdır.

- Bir kurumun posta sunucusu, FTP sunucusu vs. yönetilirken kullanılmaktadır.
