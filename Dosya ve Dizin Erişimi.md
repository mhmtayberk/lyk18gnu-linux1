## Dosya ve Dizin Erişimi

### mkdir

- Yeni bir dizin oluşturur.

- Örnek kullanımı; `mkdir dizinadi` şeklindedir.



### mkdir -p

- Alt alta dizinlerin tek bir komutla yaratılmasını sağlar.

- Örnek kullanımı; `mkdir -p dizinadi1/dizinadi2` şeklindedir.

- `dizinadi1` ebeveyn dizin olur.



### rmdir

- Boş dizinleri silmek için kullanılır.

- Boş olmayan dizinleri silmez.



### rm

- Bir dosyayı silmek için kullanılır.



### rm -i

- Tek tek sileceği tüm dosyalar için onay ister.



### rm -rf

- Dizinin içi dolu dahi olsa o dizini silmek için kullanılır. Onay istemeden işlem yapar.

- `rm -rf <dosyaadi>` şeklinde kullanılır.



### touch

- 0 bayt boyutunda bir dosya yaratır.

- Oluşturmak istenilen isimde bir dosya var ise dosyanın son erişim zamanı güncellenir.

- Kullanımı; `touch <dosyaadi>` şeklindedir.



### cp

- Dosya veya dizini kopyalamak için kullanılır.

- `cp <kaynak> <hedef>` şeklinde kullanılır.



### mv

- Dosya veya dizini belirtilen hedefe taşımak için kullanılır.

- Dosya veya dizin ismini değiştirmek için de yine bu komut kullanılır.

- `mv <kaynak> <hedef>` şeklinde kullanılır.



### file

- Dosyanın türü hakkında bilgi vermek için kullanılır.

- `file <dosyaadi>` şeklinde kullanılır.



### Karakter Eşleme (Pattern Matching)

- Yıldız (*) -> Her türlü karakter dizisi veya hiçbir şey. Örn: `ls sayfa*`

- Soru İşareti (?) -> Herhangi bir karakter. Örn: `ls sayfa?.txt`

- Köşeli Tırnak ([]) -> Belirtilen karakter aralığından bir karakter. Örn: `ls sayfa*[12579].txt`



### find Söz Dizimi

- find arama işlemleri için kullanılan çok kapsamlı bir parametredir.

- `find <aramayeri> -name "<aranan>"` şeklinde kullanılır.

- `find /usr/include -name "stdio.h"` -> /usr/include dizinindeki stdio.h isimli her şeyi arar.

- `find /home -name "*.[İi][Ss][Oo]" `-> /home dizinindeki tüm .iso kombinasyonlarını arar. Örn: .iso, .iSo, .isO, .İSO vs.

- `find /home/mhmtaybek -user root` -> /home/mhmtayberk dizininde root'a ait olan her şeyi arar.

- `find /home -uid 500` -> /home dizininde uid'si 500 olan her şeyi arar.

- `find /home -size +2000M `-> /home dizinindeki 2GB'den büyük dosyaları arar.

- `find /home -size +10240k` -> /home dizinindeki 10MB'den büyük dosyaları arar.

- `find / -type f -mmin -90` -> Kök dizindeki90 dakika içerisinde en son değiştirilmiş olan dosyaları arar.

- `find / -type f -mmin +90` -> Kök dizindeki 90 dakika ve yukarısında değiştirilen dosyaları arar.

- `find / -type f -mtime -1` -> Kök dizindeki son 1 gün içerisinde değiştirilmiş dosyaları arar.

- Örnek kullanım; `find /home/han -name "*.pdf"`



#### Notlar

- UNIX'te peş peşe komut çalıştırılabilir. Bunun için komutlar arasına noktalı virgül koymak yeterlidir.

- Satırda komutla && ile ayrılırsa, soldaki komut başarılı olur ise sağdaki çalıştırılır, değilse çalıştırılmaz.
