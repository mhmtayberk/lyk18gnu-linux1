## Kullanıcı ve Grup Yönetimi

### Kullanıcı ve Grup Veritabanları

- **/etc/passwd** dosyasında kullanıcı bilgileri tutulur.

- **/etc/group** dosyasında grup bilgileri tutulur.

- PAM sayesinde başka kullanıcı ve grup veritabanlarının kullanılması da mümkündür.

- UNIX sistemlerde erişim denetim mekanizmaları kullanıcı ve grup temellidir.

- NIS, LDAP, SMB, İlişkisel veritabanları vs. de mevcut.

- /etc/passwd'nin dosya biçimi şu şekildedir; kadı:kparolası:kkn:gkn:kbilgileri:kevdizini:kkabuğu

- /etc/group dosya biçimi şu şekildedir; gadı:gparolası:gkn:g1:g2

- `pwunconv` komutu ile /etc/shadow'da bulunması gereken bilgiler/etc/passwd'ye ekleniyor ve shadow suit devre dışı bırakılmış oluyor. **(Asla önerilmez)**

- `pwconv` komutu ile pwunconv'un yaptığı işlemleri reverse eder.



### Yeni Kullanıcı Tanımlanması

- `useradd` komutu ile tanımlanır.

- Örnek kullanım; `useradd -g users -G "floppy,cdrom,audio" -d /home/yonetici5 -s /bin/bash -c "Yönetici 5" yonetici5`

- Örnek kullanım; `useradd -g users -G "donanimcilar,programcilar" -m /home/oguz -s /usr/bin/tcsh oguz`

- Aynı işlemler **yast** ile yapılabilir.

- **/etc/shadow** dosyasında kullanıcının parolasının başına **!(ünlem)** karakteri ile kullanıcı disable edilebilir.



### Kullanıcı Bilgileri Değişikliği ve Silme

- `usermod -c "Mehmet Ayberk eğitim kullanısıcı" mhmtayberk`

- `usermod -m -d "/home/programcilar/mhmtayberk" mhmtayberk` -> Kullanıcının home dizinini değiştirir.

- `usermod -s "/bin/tcsh" mhmtayberk` -> Kullanıcının kabuğunu değiştirir.

- Bu komutları kullanırken kullanıcının hali hazırda sisteme bağlı bulunmaması gerekiyor.



### Kullanıcı Şifre Yönetimi

- Şifrenin geçerlilik süresini `chage` komutu ile düzenleyebiliriz.

- Örneğin; `chage mhmtayberk`

- Şifrenin geçerlilik süresinin izlenimi `chage -l k.adi` şeklinde izlenir.

- Bu komut shadow destekli sistemlerde kullanılabilmektedir. 

- **Minimum Password Age :** İki şifre değiştirme arasında gün bazında geçmesi gereken asgari süre. Örneğin; son şifre değişikliğinden sonra 10 gün boyunca şifre değiştirmeye izin verme.

- **Maximum Password Age :** Parolanın geçerli olacağı azami gün süresi. Örneğin; 20 gün sonra şifre değiştirmeye zorla.

- **Last Password Change :** Parolanın değiştirildiği son tarih.

- **Password Expiration Warning :** Parolanızı değiştirin uyarısının kaç gün görüntüleneceği.

- **Password Inactive :** Parolanın zaman aşımına başladıktan sonra hesabın kitlenmeden önce beklenecek süre.

- **Account Expiration Date :** Parolanın geçerli olacağı son tarih.



### Grup Yönetimi

- Tanımlı bir grubun id numarasını değiştirmek için; `groupmod -g yeni_grup_id grupadi`

- Tanımlı bir grubun ismini değiştirmek için; `groupmod -n yenigrupadi grupadi`

- Gruplara `gpasswd` ile parola atanabilir.
