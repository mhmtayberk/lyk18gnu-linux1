## uid & Shell & Dizinler & Komutlara Giriş

### mhmtayberk:pass:500:510:Mehmet Ayberk:/home/mhmtayberk:/bin/bash

- mhmtayberk -> Kullanıcı Adı

- pass -> Kulanıcı Paroları

- 500 -> uid

- 510 -> guid

- Mehmet Ayberk -> Full Name

- /home/mhmtayberk -> Ev dizini altındaki kullanıcı

- /bin/bash -> Kullanıcının çekirdekte bulunduğu bilgisi

### Dizinler

- /tmp -> Geçici dizindir. Özel bilgilerin burada saklanmaması gerekir. Kalıcı bilgiler tutulmaz.

- /home -> Kullanıcı dizinidir.

### Kılavuz

- Kullandığımız her komutun bir kılavuz dosyası vardır.

- `man  <komutadi>` şeklinde kılavuza erişebiliriz. Örneğin: `man ls`

### write

- `write kullanici_adi` ile iki kullanıcı chat yapabilir.

### wall

- Sisteme bağlı tüm kullanıcılara anlık mesaj gönderir. Sudo gerektirir.

### /etc/mod Dizini

- Sisteme giren kullanıcılara göndereceğiniz duyuruları buraya yazmanız gerekmekte.

### su -

- Root olmaya yarar.

### groupadd ve groupdel

- `groupadd` yeni bir group oluşturmaya yarar.

- `groupdel` mevcut bir group'u silmeye yarar.

- Örnek kullanım şu şekildedir; `groupadd programcilar`

### gpasswd

- gpasswd komutu bir kullanıcıyı bir group'a eklemek veya çıkarmak için kullanılır.

- `gpasswd -a kullaniciadi groupadi` şeklinde kullanıldığı zaman kullanıcı o gruba **eklenmiş** olur.

- `gpasswd -d kullaniciadi groupadi` şeklinde kullanıldığı zaman kullanıcı o gruptan **silinmiş** olur.

### newgrp

- Bu komut ile kullanıcının ön tanımlı group'unu değiştirebiliriz.

### w

- `w` komutu ile tüm kullanıcıları görmemiz mümkün.

- Aynı zamanda TTY, FROM, LOGIN, IDLE, JCPU, PCPU, WHAT bilgilerini de gösterir.

- TTY -> Sisteme girdiği kapı.

- WHAT -> O an kullanıcının yaptığı işlem bilgisi.

- FROM -> Kullanıcının nerede bulunduğu.

- LOGIN -> Ne zaman giriş yaptığı.

### who

- Sistemde kimlerin olduğunu gösterir.

- `who` ile `w` komutunun birbirinden farkı; who yalnızca LOGIN, TTY bilgilerinin verirken w daha geniş bilgiler göstermektedir.

### passwd

- Kullanıcımızın parolasını değiştirmek için kullanılır.

- Root kullanıcısı ne söylerse kabul eder fakat diğer kullanıcılarda abc123 gibi basit şifreleri kabul etmez.

### /etc/shells

- Sistemdeki kabuk alternatifleri bu dosyaya yazılır.

### chsh

- Bu komut ile kullanıcının kabuğu (shell) değiştirilir.

- Kullanımı `chsh kullaniciadi` şeklindedir.

### su

- Bir kullanıcının başka bir kullanıcının kimliğine bürünmesini sağlar.

- Örnek kullanımı `su root` şeklindedir.

### sudo

- Bir kullanıcının başka bir kullanıcının kimliği ile komut işletmesini sağlar.

- Örnek kullanımı `sudo root` şeklindedir.

### visudo

- /etc/sudo dosyasını editlemek için kullanılır.

### /etc/shadow

- Root kullanıcıları erişebilir.

- Kullanıcı parolalarının şifreleri bulunur.

### PAM

- Kullanıcı doğrulamasını kodlamasına gerek kalmadan kütüphaneyi include etmeye yarar.



#### Notlar :

- Linux sistemlerde 1000'den küçük User ID (uid)'ler sistem kullanıcılarıdır.

- uid ve parola 8 karakterden büyük olmamalıdır. Bunun sebebi de şuradan gelir; 8 bit = 1 bayt. Veri kurtarma işlemlerinde kolaylık sağlamaktadır. 

- UNIX sistemlerde sizin şifrenize erişen birisi parolanızı teorik olarak elde edemez.

- root kullanıcısının uid ve gui değerleri sıfır (0)'dır.

- Grup bilgileri /etc/group dosyasında tutulur.

- Eski Linux sürümlerinde grup parolaları /etc/gshadow dosyasında tutuluyordu.

- Kullanıcılar herhangi bir anda yalnızca bir grubun üyesi olarak çalışabilirler.

- /etc/pam.d altında her servis için ayrı bir dosya bulunur.

- Bazı sistemlerde bu dosya /etc/pam.conf'tadır.

- Bir kullanıcı en az 1 group'a üye olmak zorundadır.

- Bir dizin veya dosya sistemde var olabilmek için muhakkak 1 group'a ait olmalıdır.
