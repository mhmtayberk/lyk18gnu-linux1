## Metin Editörleri

### Pico Metin Editörü

- Pico (Pine COmposer)

- Pine E-Posta istemcisi ile birlikte dağıtılmaktadır.

- Komut satırından `pico dosyaadi` şeklinde çalıştırılabilir.

- Açılan ekrandan istenilen metinler yazılır, tanımlı komutlar CTRL + komut baş harfi biçiminde verilir.

- Temel komutları şunlardır;

- `^X` : Çıkış

- `^W` : Metin Arama

- `^Y` : Önceki Sayfa

- `^O` : Kaydederek Çıkış



### Nano Metin Editörü

- Nano, kullanımı pico'ya benzeyen GPL lisanlı bir editördür.

- Kullanım ve komutların veriliş şekilleri ile tüm komutlar pico ile birebir aynıdır.

- Komut satırından `nano dosyaadi` şeklinde çalıştırılabilir.

- /etc dizininin içinde nanorc adında bir dosya bulunur. Nano'ya kısayollar ekleyip çıkarmak bu sayede mümkün olabiliyor. Renklendirme gibi ayarlar da yapılabiliyor.

- Metnin en altına dönmek için **CTRL + W -> CTRL + V**

- Metnin en üstüne dönmek için **CTRL + W -> CTRL + W**

- Çıkmak için **CTRL + X -> Çık**

- Arama yapmak için **CTRL + W**

- Örneğin tüm büyük M'leri küçük m harfine çevirmek için **CTRL + W -> CTRL + R**

- Çıkmadan kaydetmek için **CTRL + O**

- Bir dosya ile bir dosyayı birleştirmek için **CTRL + R**



### Vi Metin Editörü

- Vi gelişmiş bir metin editörüdür.

- Komut satırından `vi dosyaadi` şeklinde çalıştırılabilir.

- vi yalnızca UNIX komut satırında değil X Window Sistemi'nde de kullanılmaktadır.

- İki kere A'ya basıldığı takdirde kullanılmaya başlatılır. Açılışta kilitlidir.

- ESC'ye bastıktan sonra `:q!` yazarak çıkılabilir.

- Bütün UNIX sistemlerde bulunan bir editördür.



### Vim Metin Editörü

- VIM sadece bir metin editörü değil, aynı zamanda bir yazılım geliştirme ortamıdır.

- VI Improved.

- Komut satırından `vim dosyaadi` şeklinde çalıştırılabilir.

- Komut renklendirme, 300+ farklı progralama dili desteği, birden fazlan pencerede çalışma gibi ek özellikler eklenmiş bir editördür.

- Diğer editörlerden farklı olarak üç temel konumu vardır. (Komut konumu, metin giriş konumu ve satır editörü konumu)

- VIM çalıştırıldığı anda komut konumunda başlar. Metin girişi konumuna geçmek için a, i ya da o harflerinden herhangi birine basılabilir. Satır editörü konumuna geçiş yapmak için `:` yazılır. Komut konumuna dönmek için ESC tuşuna basılır.

- h, j, k, l tuşları -> İmleç Hareketi

- Ok Tuşları -> İmleç Hareketi

- `i <metin> Esc` -> Metnin arasına <metin> metnini girmek

- `cw <sözcük> Esc` -> İmleçin sağında bulunan sözcüğü <sözcük> ile değiştirmek

- `x` -> İmlecin üzerinde bulunduğu karakteri silmek

- `dd` -> İmlecin bulunduğun satırın tamamını silmek

- `u` -> Son yapılan işlemi geri almak.

- `ZZ` -> Açık olan dosyayı kaydederek Vi'den çıkmak.

- `q!` -> Dosyayı kaydetmeden vi'dan çıkmak.

- `:/<sözcük>` -> Metinde sözcük arama.



#### Notlar

- UNIX türevlerinde çevre birimleri dahil her türlü ortam, cihaz ve uygulama birer dosya olduğu için; en sık kullanılan UNIX uygulamaları metin editörleridir.

- Deneyimsiz UNIX kullanıcıları kolay kullanılan pico ya da nano gibi editörleri tercih etmektedir.

- Deneyimli kullanıcılar için gelişkin özellikleri nedeniyle vi ya da vim gibi editörleri tercih etmektedir.

- emacs, joe, sed, jed, ee, mcedit, Kwrite, KVI, Elvis, gEdit, blew sık kullanılan bazı metin editörleridir.
