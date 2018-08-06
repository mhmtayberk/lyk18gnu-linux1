## UNIX Kabukları

### UNIX Kabukları

- Bourne Shell

- Korn Shell

- C Shell

- Ve diğerleri.



### Bash (Bourne Again Shell) Özellikleri

- Komut satırı düzenleme.

- Geçmiş komutları çağırma ve düzenleme.

- Bir bölümü yazılmış sözcükleri tamamlama.

- Fonksiyon ve takma isimleri destekler. (Takma ada örnek kullanım; `alias saatkac="date"`)

- Görevi askıya alıp art alanda çalıştırma imkanı.

- Aritmetik işlemler yapabilmekte.

- Komut istemini özelleştiren özel karakter dizileri.

- Key Sensitivy özelliği vardır. (Windows'ta bu özellik yok)



### Çevre Değişkenleri

- Kullanıcı sisteme giriş yaptığı anda kendisine /etc/passwd dosyasında tahsis edilen kabukla çalışmaya başlar.

- Çevre değişkeni başka kabukların kullanımı için ihraç edilebilir.

- TERM değişkeni uçbirimin türü bilgisini tutar.

- Kurulu çevre değişkenlerinin tamamı `set` ile listelenebilir.



### Kabuk Komut Satırı Düzenleme

- Ctrl + a -> Satır başına atar

- Ctrl + e -> Satır sonuna atar

- Ctrl + l -> Ekranı temizler

- Ctrl + r -> Reverse-i Search. Enter'a basıldığı zaman bulunan komutu çalıştırır.



### Görevi Art Alanda Çalıştırma

- Komutun sonuna `&` ekleyerek art alanda çalıştırılması sağlanabilir.

- Çalışan komut `Ctrl + z` kombinasyonu ile askıya alınabilir.

- `bg` komutu ile askıya alınan program başlatılabilir.

- `jobs` ile arka planda çalışan işler görünebilir.

- `fg %sira jobs` komutundaki sıra numarasına sahip art alandaki görev ön alana çağrılabilir.

- `kill %sira` ile belirtilen sıra numarasına sahip art alandaki görev durdurulabilir.

- `fg` komutu ile askıya alınan program öne çekilebilir.



### Kabuk Komut İstemini Özelleştirme (Promt)

- `\u` -> Kullanıcı adı.

- `\h` ->Bilgisayar adı.

- `\W` -> Çalışma dizini.

- `\w` -> Kökten itibaren çalışma dizini.

- `\j` -> Kabuk tarafından yönetilen görev sayısı.

- `\t` -> 24 saatlik biçemde saat.

- `\$` -> root ise # sıradan kullanıcı ise $.

- `echo $PS1` ile kullanılan promt görülebilir.



#### Notlar

- Kabuk kullanıcının işletim sistemi ile arayüzüdür.

- En esnek kabuklardan birisi olan Bourne Again Shell, kolay kullanımı ve özellikleri nedeniyle tercih edilir.

- `alias saatkac="kac"` şeklinde yapılan tanımlamalar kabuğa kaydedilmediği takdirde sadece o terminal oturumu kapatılana kadar geçerlidir.

- `unalias` komutu ile takma ad kaldırılabilir.

- Kabuk komutu PATH'den arayıp çalıştırır.

- Yukarı yön tuşu ile geçmiş komutlar geriye doğru gösterilir.

- Aşağı yön tuşu ile geçmiş komutlar ileriye doğru gösterilir.

- TAB tuşuna basarak bir bölümü yazılmış komut tamamlanabilir.

- TAB tuşuna basarak bir bölümü yazılmış dosya/dizin tamamlanabilir.
