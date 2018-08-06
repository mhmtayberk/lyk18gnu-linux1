## Sed ve Awk

### GNU sed Kullanımı - Bul ve Değiştir

- `sed 's/bulunacakkelime/yerinekonacakkelime/g' < metin > degismismetin`

- Ön tanımlı olarak her satırda ilk bulduğunu değiştirir.

- Eğer sonuna g konulursa işlemi belgenin tamamında yapar.

- GPL lisanslıdır ve C dili ile yazılmıştır.

- Örnek uygulama; `sed 's/linux/unix/' < ornek.txt > ornek2.txt`

- Örnek uygulama; `sed 's/linux/unix/g' < ornek.txt > ornek2.txt`



### GNU sed Kullanımı - Bul ve Değiştir - Özel Sırada Değiştirme

- `sed 's/linux/unix/2' < ornek.txt > ornek2.txt` -> İkinci sıradaki linux kelimelerini unix ile değiştirir.

- `sed 's/linux/unix/2' < ornek.txt > ornek2.txt` -> Üçüncü sıradaki linux kelimelerini unix ile değiştirir.



### GNU sed Kullanımı - Bul ve Değiştir - Dizi Kullanımı

- `sed -e 'y/abcdefghijklmnopqrstuvwxyz/ABCDEFGHIJKLMNOPQRSTUVWXYZ/' linux-seviyorum.txt`

- sed ile dizi kullanımına güzel bir örnek. tr komutu yerine sed ile de büyük küçük harf değişimi yapabiliriz.



### GNU sed Kullanımı - Bul ve Değiştir - Çoklu Dosya

- sed ile birden çok dosya üzerinde işlem yapabilirsiniz.

- Bir dizin içinde dosyalar ve alt dizinler bulunmaktadır. Bu dizinin altındaki tüm dosyalarda #include <stdio.h> geçen satırları #include <pthread.h> olarak değiştiriniz.

- `grep "#include <stdio.h>" * -r | wc -l`

- `grep -rl "#include <stdio.h>" | tail -3`

- `grep -rl "#include <stdio.h>" | xargs sed -i 's/#include <stdio.h>/#include <pthread.h>/'`



### GNU sed Kullanımı - Satır Silme

- Dosya içinden satır silme : 

- `sed -e 'satır_no d'`

- satır_no alanına bir aralık verilebilmektedir.

- Örnek kullanımı; `sed -e '2 d' linux-seviyorum`

- Örnek kullanımı; `sed -e '2,4 d' linux-seviyorum`

- Örnek kullanımı; `sed -e '2 d' -e '5 d' linux-seviyorum`



### GNU awk - Özel Değişkenler

- **FILENAME** : İşlem gören dosyanın adı.

- **FS (-F)**: Girdi alan ayracı

- **RS** : Girdi kayıt ayracı

- **NF** : Yürürlükteki kaydın alan sayısı

- **NR** : Yürürlükteki kaydın satır numarası

- **OFS** : Çktı alan ayracı

- **ORF** : Çktı kayıt ayracı

- **$** : Girdi kaydının tümü



### GNU awk - Ayraç Kullanmak

- awk'ı komut satırında belli bir ayraç kullanarak metinleri bölmek için kullanabiliriz.

- `head -3 /etc/passwd | awk -F ':' ' ' ' {print $1}'`

- `head -5 /etc/passwd | awk -F ':' '{print $1 " "$7}'`



### GNU awk - Arama - Bölme Birlikte Kullanım

- awk'ı komut satırında belli bir ayraç kullanarak metinleri bölmek için kullanırken bunun yanında sed gibi arama da yaptırabiliriz.

- Örnek uygulama olarak ev dizini /home 'da bulunan kullanıcıların username, uid, guid ve kabuğunu yazdıralım.

- `awk -F ':' '/home/ {print $1 " " $3 " " $7}' /etc/passwd`

- `grep syslog /etc/passwd; grep profelis /etc/passwd`



### GNU awk - Yazdırırken Değişkene Değer Atama

- awk ile ekrana basarken aynı zamanda bir değişkene değer atayabilirsiniz.

- `awk -F ' ' ' $2="Profelis" {print $0}' ogrenciler`



### GNU awk - Yazdırırken Dışarıdan Değişken Alma

- awk ile ekrana basarken dışarıdan tanımlanmış bir değişkeni awk içinde kullanabilirsiniz.

  ```
  soyadi=profelis 
  echo $soyadi
  awk -F ' ' -v sa=$soyadi '$2=sa {print $0}' ogrenciler
  ```

  

### GNU awk - Koşullu, Koşulsuz Süzme

- awk ile grep gibi süzme işlemleri yaparken bunu koşullara bağlayabilirsiniz.

- `awk '/pattern/{print $0}' file` -> Söz dizimi bu şekildedir.

- `awk -F ' ' '$2 ~ /Üçüncü|Beşinci/{print $0}' ogrenciler`

- `awk -F ' ' '$1 ~ /Jale|Ayşe/{print $2}' ogrenciler`



#### Notlar

- GNU sed, metin ve dizi (string) ler üzerinde işlem yapan bir programdır. Genel olarak programların çıktılarını düzenlemek veya pek çok dosyayı otomatik olarak düzenlemek için kullanılır.

- GNU sed en çok, aynı değişikliğin birden fazla dosyada yapılması gerektiği durumlarda kullanılır.

- AWK neredeyse UNIX ile yaşıt, derleyicisi olmayan bir yorumlayıcı programlama dilidir.

- Grep ve cut'da satır satır bakılır, awk'da ise önce satıra sonra sütuna bakılır.
