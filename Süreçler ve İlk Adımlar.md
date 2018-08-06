## Süreçler ve İlk Adımlar

### Süreç (Process) Nedir?

- Çalışmaya başlaması ile çalışmanın sonlanması arasında her bir programa denir.

- Her sürecin bir ata süreci (ppid) bulunur.

- Süreçlerin kendilerini biricik tarif edecek süreç kimliği (pid) bulunur.

- Bu süreçlerin denetim sinyal mekanizması ile yapılır.

- Süreçler `ps` komutu ile izlenebilmektedir.

- Örnek kullanımı; `ps ax | grep program1`

- ps komutunda CPU kullanımı, başlatan, memory kullanımı, başlatılma zamanı, durumu id'si, işlettiği komut bilgileri yer almaktadır.



### Sinyal Mekanizması

- Süreçler arasında iletişim kurulabilmesi için kullanılan en temel iletişim biçimi sinyal mekanizmasıdır.

- Bir süreç diğerine sinyal göndererek diğerinin bu sinyal ile eylemi gerçekleştirmesini bekler.

- `SIGTERM` -> Çalışan süreci sonlandırmak.

- `SIGKILL` -> Çalışan ve sonlandırılmasını kabul etmeyen süreci sonlandırmak.

- `SIGSTOP` -> Çalışan süreci duraklatmak.

- `SIGCONT` -> Duraklatılmış süreci yeniden başlatmak.

- `SIGHUP` -> Ayar dosyalarının yeniden okutulmasını sağlamak. (/etc'nin altındaki config dosyaları)

- > Bu sinyaller evrenseldir.



### kill

- `kill -SIGHUP süreçnumarasi` şeklinde örnek bir kullanımı vardır.

- `kill -SIGKILL süreçnmarasi` şeklinde örnek bir kullanımı vardır.



### killall

- Süreçlere sinyalleri süreç ismi ile iletmekdir.

- `killall -SIGSTIOP httpd` şeklinde örnek bir kullanımı vardır.

- `kilall -SIGCONT httpd`  şeklinde örnek bir kullanımı vardır.



### Süreçlerin Öncelikleri

- Süreçlerin arasındaki öncelikler nice komutu ile belirlenir.

- `nice` -> Gereçli önceliği gösterir.

- `nice komut parametre` -> Komutun önceliğini 10 azaltır. (nice değerini 10 arttırır)

- `nice -n 12 komut parametre` -> Komutun önceliğini 12 azaltır. (nice değerini 12 arttırır.)

- Çalışmakta olan süreçlerin öncelikleri `renice` ile değiştirilebilir.



### Zamanlama Algoritmaları (Scheduling) Amaçları

- Cevap Süresi

- Orantılı Olma

- Veri Kaybından Sakınma

- Son Teslim Süresine Riayet Etme
