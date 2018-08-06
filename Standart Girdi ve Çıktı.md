## Standart Girdi ve Çıktı

- UNIX'te bir komutun standart çıktısını başka bir komutun standart girdisine verilebilir.

- Standart girdi(stdin) kanalının numarası `0`'dır.

- Standart çıktı(stdout) kanalının numarası `1`'dir.

- Standart hata(stderr) kanalının numarası `2`'dir.

- `program1 2> hatalar1 | program2> hatalar2` -> Program1'in hataları hatalar1'e yazılıyor standart çıktısı program2'ye yazıldı. Program2'nin hataları hatalar2'ye yazılıyor, standart çıktısı ekrana yazılıyor.

- Bir program çıktısını girdi olarak gönderebiliriz. Örnek kullanımı; `program < dosya`

- Bir program çıktısını bir dosyaya yönlendirebiliriz. Örnek kullanımı; `program > dosya`

- Bir program çıktısını mevcut olan bir dosyaya ekleme yaparak yönlendirebiliriz. Örnek kullanımı; `program >> dosya`

- Bir programın standart çıktısını başka bir programa standart girdi olarak yönlendirme. Örnek kullanımı; `program1 | program2`

- `cat /etc/passwd | grep user` -> /etc/passwd datasının tamamını görüntülemek yerine o datanın içerisinde user kelimesi geçen satırları gösterir.

- `cat /etc/passwd | sort | grep mhmtayberk` -> sort komutu alfabeye ve küçükten büyüğe şeklinde sıralama yapar.

- Uç uca bağlanarak çalıştırılan komutların ara sonuçları `tee` ile dosyalara kaydedilebilir.
