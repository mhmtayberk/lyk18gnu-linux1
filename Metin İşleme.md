## Metin İşleme

- `cat dosya1` -> Dosyaların içeriğini gösterir.

- `cat dosya1 dosya2` -> Dosyaları birleştirerek belirtilen sırada ekranda gösterir.

- `head -#` -> Dosyanın # satırını gösterir.

- `tail -#` -> Dosyanın son # satırını gösterir.

- `tail -f `-> Akan (yenilenen/devam eden) bir döküman okunabilir.

- `sort dosya1` -> Dosyanın içindeki satırları sıralı olarak gösterir.

- `cut -d ' ' -f1 dosya1` -> Dosyanın parçalara bölünmesi için kullanılır. (Boşluk)

- `uniq` -> Tekrarlayan satırları tek satıra düşürmek için kullanılır.

- `tr "degistirilecekkarakter" "yenikarakter"` -> Bir karakterin yerine başka bir karakter koymak için kullanılır. Örnek kullanımı;`tr "[A-Z]" "[a-z]" < sporcular`

- tr komutu karakter değiştirmez. Harf değiştirir.

- tr komutunun Türkçe karakter desteği yoktur. 

- `grep pattern dosya` -> Pattern ile belirtilen kurala göre kendisine gelen standart input'u ekrana basar. Büyük küçük harf duyarlılığı vardır. Bu duyarlılığı iptal etmek için `-i` parametresi kullanılır. `-v` parametresi ise uyan katarı ekrana basmaz geri kalan her şeyi ekrana basar.

- `split -l 5 dosya önek` -> Dosya datasını 5 satırlık parçalara bölüp her bir parçanın adını önek olarak belirtir. 

- `split -b 500 dosya öne`k -> Dosya datasını 500 bytelık parçalara bölüp her bir parçanın adını önek olarak belirtir. (Örneğin 4 GBlik bir veriyi 2'şer GB'lik 2 USB belleğe aktarırken kullanılabilir. Sonrasında cat ile birleştirme işlemi yapılıp kullanılabilir.)

- split komutları kullanılmadan önce yedeğini ve hash imzasını almakta fayda var.

- `paste` -> İki datayı satır satır veya sütun sütun birleştirir.

- `join` -> İki datayı birleştirir fakat bunu yaparken iki dosyadaki sütunları eşleştirerek birleştirir. Paste gibi bir komuttur fakat daha gelişmiş bir komuttur. -t parametresi ile farklı ayraçlarla ayrılmış metinlerde ayraç belirtilebilir. -i ile büyük küçük harf duyarlılığı iptal edilebilir. 

- `more dosya `-> Enter ile satır satır Space ile sayfa sayfa dosya içeriğini gösterir. Geriye dönme şansı yok.

- `less dosya` -> more ile aynı şekilde çalışır. Geri dönme şansı da tanır.

- `diff dosya1 dosya2` -> İki dosya kıyaslanır. İki dosya arasındaki farkları söyler. c : changed, d : deleted, a : added manasına gelmektedir.

- `md5sum dosya` -> Bir verinin değişip değişmediğini anlamak için kullanılır.

- `sha1sum dosya` -> Bir verinin değişip değişmediğini anlamak için kullanılır.

- `fmt -w sayi dosya` -> Verinin paragraflara ayırmasını sağlar.

- `nl dosya` -> Dosyaya satır sayısı oluşturur.

- `expand --tabs=sayi dosya` -> Boşlukları belirtilen TAB sayısı kadar (Örneğin çift tab) algılayarak çıktı verir.

- `unexpand --tabs=sayi dosya` -> Expand işleminin tam tersi işlemi yaparak çıktı verir.

- `cat -n` -> Dosya içeriğini satır, sütun sayıları ile beraber göstermekte.

- `htop` -> Anlık veri kullanımını gösterir.

- `time` -> Komutların en başına gelen bir komuttur. İşlemin ne kadar süre içerisinde yapıldığı bilgisini verir.

- `tac dosyaadi` -> cat komutunu reverse şekilde çalıştırılır.

- mv cp'den daha hızlı çalışır çünkü fiziki bir taşıma işlemi yapmaz. Yalnızca index bilgisini taşır.

- İndex'teki her bir satıra inode denir. Optimumu 4096 fakat spesifik olarak değişebilir. (Örneğin büyük dosyalar tutulacaksa 8132 yapılabilir.)
