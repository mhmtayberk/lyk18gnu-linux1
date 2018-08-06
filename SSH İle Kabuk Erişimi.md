## SSH İle Kabuk Erişimi

### İletişim Protokolleri ve Güvenlik

- Yaygın biçimde kullanılan pek çok iletişim protokolü, o günün ihtiyaçları doğrultusunda, güvenlik gereksinimleri göz önünde bulundurulmadan geliştirilmiştir. Bunlar;

- **Uzak Erişim :** Telnet / RSH / RLogin

- **E-Posta :** SMTP / IMAP / POP

- **Dosya İletimi :** FTP / NFS

- Ve diğerleri.

- Bu protokoller, iletişimin güvenliği bağlamında gizlilik ve bütünlük sağlamaktan uzaktır. (Mesajlar dinlenemesin ve değiştirilemesin)



### SSH Nedir?

- Komut satırı uzak erişim protokolü ve bu protokol ile iletişim kuran yazılım kümesi;

- Telnet'in iletişim gizliliği ve bütünlüğü sağlayan bir biçimi.

- Uçtan uca şifreleme (end to end encrpytion)

- Karşılıklı kimlik doğrulama (mutual authentication)

- İletişim bütünlüğü (communications integrity)

- İletişim güvenliği gerektiren hemen her uygulamada **güvenli tünel** olarak da kullanılabilir. (Güvenlik veritabanı bağlantısı, dosya transferi vs.)



### SSH İletişiminin Gerçekleştirilmesi

1. Sunucu üzerinde SSH sunucusu (sshd) çalıştırılır.

2. `rcsshd start`

3. `/etc/init.d/sshd start`

4. `systemctl start sshd.service`

5. İstemci bilgisayardan uzak sisteme bağlantı için SSH istemci programı uygun parametreler ile başlatılır.

6. `ssh kullanici@sunucu_adresi`



### SSH Sunucu Doğrulaması

1. SSH istemci, bağlantı sırasında sunucunun kimliğini denetler. (İstemci, doğru sunucuya bağlandığından emin olur.)

2. Bağlantı gerçekleştirildiğinde sunucu anahtarı kaydedilir.

3. Her SSH sunucusunun bir anahtar ikilisi vardır. (SSH, açık anahtarlı şifreleme üzerine kuruludur.)

4. SSH istemci ayarlarının tümü ~/.ssh dizini altındadır. (Sunucu ayarlarının tümü, /etc/ssh altındadır.)

5. İstemci tarafından doğruluğuna güvenilen tüm sunucu açık anahtarları **~/.ssh/known_hosts** dosyası içerisinde yer alır.



### SSH : Kullanıcı Doğrulama.

| Geleneksel Parola Temelli Kullanıcı Doğrulama                                                                                             |
| ----------------------------------------------------------------------------------------------------------------------------------------- |
| Ön tanımlı çalışma biçimi.                                                                                                                |
| **Açık Anahtarlı Doğrulama**                                                                                                              |
| Kullanıcı, kendisini tanımlamak için kullanacağı anahtar çiftini SSH-Keygen programı ile üretir.                                          |
| Sunucu üzerinde "anahtar ile doğrulama" yöntemi ile giriş yapacağı hesaba açık anahtarını "güvenilen bir kullanıcı" olarak tanımlar.      |
| Kendi sistemi üzerinde yer alan gizli anahtar kullanıcının tanımlayıcısıdır. (Gizli anahtar, çalınmaya karşı bir parola ile korunabilir.) |



### Kullanıcılar İçin Anahtar Üretimi

- `ssh-keygen -t dsa`



### Sunucuya Kullanıcı Anahtarı Yükleme

- Kullanıcı, açık anahtar doğrulaması ile bağlanmak istediği sunucu üzerine **~/.ssh/authorized_keys** dosyasına anahtarının içeriğini **(id_dsa.pub)** eklemeli.

- Önce `ssh-keygen -t dsa` komutu ile keyimizi oluşturduk. Daha sonra `cd .ssh` ile dizine geldik ve **id_dsa.pub**'un içindeki keyi kopyaladık. Sunucuya bağlanıp `mkdir .ssh` dizinini oluşturduk ve içine **authorized_keys** dosyası oluşturup keyimizi yapıştırdık. (nano authorized_keys)



### sftp - Güvenli Dosya Transferi Programı

- SSH uygulamalarından birisi olan sftp ile sunucu üzerinde depolanan dosyalara güvenli erişim sağlanabilir. Bu işlem sırasıyla şöyle yapılabilir;

  1. `sftp [kullaniciadi@xxx.xxx.xxx.xxx]`

  2. `put data.txt`



### scp - Güvenli Dosya Kopyalama Programı

- SSH uygulamalarından birisi olan scp ile sunucu üzerinde depolanan dosyalara güvenli erişim sağlanabilir. Bu işlem sırasıyla şöyle yapılabilir;

  1. `scp data.txt [kullaniciadi@xxx.xxx.xxx.xxx]`

  2. `scp [kullaniciadi@xxx.xxx.xxx.xxx]:/home/profelis/data1.gz`



### SSH Üzerinden rsync Aracı ile Dosya Kopyalama

- rsync hızlı, çok yönlü bir dosya kopyalama aracıdır ve SSH üzerinden kullanımı mümkündür. Bu işlem sırasıyla şöyle yapılabilir;

  1. `rsync -av data.txt [kullaniciadi@xxx.xxx.xxx.xxx]:/home/mhmtayberk/data.txt/` -> Tek dosya aktarımı için. (Kendi bilgisayarımızda çalıştırdık.)

  2. `rsync -av /home/mhmtayberk/dizin1 /home/mhmtayberk/dizin2/` -> Sunucuda çalıştırdık.

  3. Böylece büyük dosyalar bir sunucudan başka bir sunucuya güvenli bir şekilde taşınabilmekte. Alınan yansıda değişiklik olduğu zaman bu değişiklik de yazdırılır. rsync'nin en büyük avantajlarından biri de budur.

  4. `rsync -av --delete /home/mhmtayberk/dizin1 /home/mhmtayberk/dizin2/ `-> Yalnızca silinen dizinlerin yansılarında değişiklik yapar.

  5. `rsync -av --delete /home/mhmtayberk/ [kullaniciadi@xxx.xxx.xxx.xxx]:/home/ayberk/` -> /home/mhmtayberk'deki her şeyi sunucudaki /home/ayberk' aktarır. Bu işlem yapılırken gizli dosyalar da aktarılır.



### Zayıf Protokollere Destek

- Pek çok iletişim protokolünün güvenlik özellikleri yetersizdir.

- Bu protokolleri güvenli hale getirmek iki biçimde mümkün olabilir. (Tüm istemci ve sunucular değiştirilir veya ilgili protokol, yüksek güvenliğe sahip bir diğer protokol ile değiştirilir.)



### SSH Tünelleri : Örnek

```
SSH ile socks proxy uygulaması:
ssh -D 8080 kullaniciadi@xxx.xxx.xxx.xxx
Tarayıcı Proxy yapılandırması. (127.0.0.1 socks proxy)
```



### SSH Tünelleri : Diğer

- SMB

- X11, VNC

- NFS

- POP, SMTP

- Ve niceleri...



### X Tünellemesi

- DISPLAY değişkeninin tanımlanması vb. gerekmez,



### OpenSSH ve OpenSSL

- OpenSSH, şifreleme kitaplığı olarak OpenSSL'i kullanmaktadır.

- En yaygın özgür yazılım SSH kümesi OpenSSL'dir.



### Putty

- MS-Windows altında en yaygın istemcilerden birisidir.

- Özgür bir yazılımdır.

- SSH, SCP, SFTP ve diğerlerinden oluşan eksiksiz bir kümedir.

- Putty'nin de **PuttyGen** adından bir **RSA Key** oluşturan programı bulunmaktadır.

- PuttyGen mouse hareketlerine göre random bir şekilde key üretmektedir. Bu oldukça güvenlidir. Key sunucuya Auth. edildikten sonra Putty'den gerekli konfigürasyon ayarları yapılmalı. (**SSH > AUTH** altından yapılabilir.)



### Putty İle Sock Proxy

- **SSH > Tunnels > Dynamic / Port : 8080** ve ardından tarayıcı ayarları.



### sshfs (Secure Shell File System) Nedir?

- SSHF, SSH ve SFTP ile bağlanabiliyor olduğunuz uzaktaki sunucudaki bir dizini dosya sisteminizin bir dizine bağlayarak sanki yerelinizdeki bir dizin gibi kullanmanıza olacak sağlar.

- Windows'ta üçüncü parti uygulamalar ile yapılabilmekte.

- Şöyle bir örnek ile daha net açıklanabilir;

  1. `mkdir uzaksunucu`

  2. `sshfs [kullaniciadi@xxx.xxx.xxx.xxx]:/home/mhmtayberk /home/mhmtayberk/uzaksunucu`

  3. `df -h`

  4. `cd uzaksunucu`

  5. `ls -al`

  6. `fusermount -u /home/mhmtayberk/uzaksunucu`

  7. `df -h`





#### Notlar

- SSH bir kütüphane olarak SSL'i kullanır.

- SSH sunucuya değil kullanıcıya yapılır.

- SSH ile Port Forwarding yapmak mümkün.

- FileZilla ile SFTP bağlantısı yapılabilir. FileZilla açık kaynak kodlu bir yazılımdır.

- VNC'de X Window çekip kullanılabilir.

- Windows 10'da SSH istemcisi bulunmakta. Fakat kullanılması **ASLA** önerilmemekte.

- Linux'ta üretilen Private Key ile Windows'ta üretilen Private Key farklıdır.

- SSH paketi, güvenli iletişim için basit ve etkin bir altyapı sağlar. (Güvenli uzak erişim ve güvenli dosya iletimi)

- Açık anahtarlı kullanıcı doğrulaması parola korumasından daha etkindir.

- TCP temelli hemen her protokol SSH içerisinden tünellenebilir.
