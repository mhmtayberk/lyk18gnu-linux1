## Kabuk Programlama

### UNIX Kabuğunun Gelişmiş Programlama Yetenekleri

- Çevre değişkenleri

- Aritmetik işlemler

- Diziler

- if yapısı

- case yapısı

- for döngüsü

- while döngüsü

- İşlevler



### Kabuk Programı Nasıl Yazılır?

- Herhangi bir metin düzenleme programı ile kolayca yazılabilir ve kodlanabilir.

- Dosyaya çalıştırma yetkisi verilmesi gerekir. ( **chmod +x programadi** )

- Komut yazar gibi dosyanın ismi yazılır.

- Kabuk yazdığımız dosyayı satır satır yorumlar ve çalıştırır.

- **#!/bin/bash** gibi yazacağımız betiğin hangi kabukta çalışacağını belirtmemiz gerekir.



### Kabuk Değişkenleri

- Çevre değişkenlerini aktarmak için; `degiskenadi=deger`

- Çevre değişkenlerini okumak için; `echo $degiskenadi ardından yenidegisken=$degiskenadi`



| Tırnak Türü       | Değişken | Komut |     |     |
| ----------------- |:--------:| -----:| --- | --- |
| Çift Tırnak **"** | Evet     | Hayır |     |     |
| Tek Tırnak **'**  | Hayır    | Hayır |     |     |
| Ters Tırnak **`** | Evet     | Evet  |     |     |

### Değişken Niteleyiciler

- `${degisken}` -> Değişkenin değeri kullanılır.

- `${degisken:-kelime}` -> Değişken kurulu değilse veya boş ise "kelime" kullanılır. Aksi durumda değişkenin değeri kullanılır.

- `${degisken:=kelime}` -> Değişken kurulu değilse veya boş ise "kelime" değişkene aktarılır ve kullanılır. Aksi durumda değişkenin değeri kullanılır.

- `${degisken?kelime:}` -> Değişken kurulu değilse veya boş ise "kelime" standart hata aygıtında görüntülenir ve kabuktan çıkılır.

- `${degisken:+kelime}` -> Değişken kurulu değilse veya boş ise hiçbir şey kullanılmaz. Değişken bir değer içeriyorsa yerine "kelime" kullanılır.

- `${#degiskenadi}` -> Değişkenin karakter sayısını verir.



### Diziler

```DIZI[0]=ilkeleman
DIZI[0]=ilkeleman
echo ${DIZI[0]}
DIZI[1]=ikincieleman
echo ${DIZI[1]}
DIZI[2]=üçüncüeleman
echo ${DIZI[2]}
```



### IF, CASE Yapıları

```
if durum
then
komutlar
[
elif durum
then
komutlar
]
.......
[
else
komutlar
]
]
```



### Test - Dosyalar

- if ve while yapılarındaki durumlar test komutu ile oluşturulmaktadır.

- test ifade biçiminde kullanılır.

- `-f dosya` -> Dosya varsa ve türü dosya ise doğrudur.

- `-d dosya` -> Dosya varsa ve türü dizin ise doğrudur.

- `-s dosya` -> Dosya varsa ve boş değilse ise doğrudur.

- `-w dosya` -> Dosya varsa ve yazılabilir ise ise doğrudur.

- `-x dosya` -> Dosya varsa ve çalıştırılabilir ise ise doğrudur.

- `-O dosya` ->Dosya varsa ve sahibi geçerli kullanıcı ise ise doğrudur.



### Özel Değişkenler

- `$0.....$9` -> $0 programın adı, $1.....$9 sırasıyla komut satırındaki parametrelerin değerleridir.

- `$#` -> Toplam parametre sayısı.

- `$?` -> En son programın çıkış durumu.

- `$$` -> Çalışan kabuğun süresi

- `$!` -> En son çalıştırılmış art alan görevinin süreç numarasını gösterir.

- `$* -> "$1......$9" `

- `$@ -> "$1"......"$9"` 'a kadar olan parametrelerin hepsi.

- `shift `komutu parametre olan gelen değişkenleri öteler.



### Function Yapısı

```
function isim()
{
komutlar
}    
```



#### Notlar

- echo $$ çalışan kabuğun process numarasını verir. Bu işlemi uzun uzadıya ps aux | grep bash şeklinde de görebiliriz.

- /dev/null sistemde bir boşluktur. Karadelik olarak nitelendirebiliriz.
