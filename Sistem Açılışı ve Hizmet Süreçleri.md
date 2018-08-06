## Sistem Açılışı ve Hizmet Süreçleri

### BIOS İle Açılış

- AİB'ne güç geldiği anda AİB (Ana İşlem Birimi) BIOS programını çalıştırır.

- BIOS salt okunur bir devre üzerinde yazılıdır.

- Açılış sürecinin ilk adımından sorumludur.

- BIOS yalnızca x86 platformuna özgüdür.

- BIOS sistem bileşenlerini kontrol eder. (Post Check)

- Açılış sırasına göre BOOT edilecek açılış ortamını arar ve bularak sistemi başlatır.

- Açılış için disk aygıtı seçildiyse sabit diskin ilk sektörü (MBR) belleğe okunarak çalıştırılır.



### init'i Yönlendirme

- `init {Q|q}` -> /etc/inittab dosyasını tekrar okuması ve değişikliklerin geçerli olmasını sağlar.

- `init -t 9` -> SIGTERM sinyalinden sonra SIGKILL sinyalinin gönderilmesi için beklenmesi gereken zamanı bildirir.



### /etc/inittab Dosyası

- Açılışta ve rutin işleyişte çalıştırılacak süreçlerin tanımlandığı dosyadır.

- 3 çeşit tanımı vardır;

- Sistemin açılıştaki öntanımlı çalışma düzeyi,

- Çalıştırılacak, takip edilecek ve durduğu zaman yeniden başlatılacak programlar,

- Sistem yeni bir çalışma düzeyine geçtiğinde çalıştırılacak programlar.



### init Çalışma Biçimi

- `sysinit` -> Program sistem açılışında çalıştırılır ve sonlanması beklenir. Program sonlanmadan başka bir işlem yapılmaz. (Örneğin; sistem açılışındaki Post Check)

- `once` -> Program başlatılır, sonlanması beklenir; sonlandığı zaman bir daha başlatılmaz.

- `respawn` -> Program başlatılır ve çalışmasının sonlanması beklenir; program sonlandıkça yeniden başlatılır. (Örneğin; Shell)

- `wait` -> Program başlatılır ve sonlanana kadar beklenir.

- `powerfail` -> Kesintisiz güç kaynağı azaldığından program işletilir ve sonlanması beklenmez.

- `powerokwait` -> Kesintisiz güç kaynağını besleyen enerji geri geldiğinde program işletilir; sonlanması beklenmez.

- `initdefault` -> Varsayılan çalışma düzeyini tanımlar.

- `ctrlaltdel` -> Konsoldan CTRL + ALT + DEL kombinasyonu izlenerek çalıştırılacak program belirtilebilir.



### Hizmet Süreçleri

- Sistem hizmet programlarına ait betikler **"/etc/rc.d/init.d"** dizininde bulunur.

- Hizmet süreçleri bu betik ile başlatılıp durdurulabilir.



#### Notlar

- **halt** servisleri kontrollü olarak kapanır ve en son sistemin elektriğini keser.

- systemd ile klasik Linux arasındaki fark şudur: Klasik Linux açılışında deamon'lar birbirini beklediği için yavaş açılmasına sebep olmaktaydı. systemd'de ise deaoman'lar önceden çalıştırılıyor ve minimum seviyede bekletiliyor. Lazım olduğu zaman da deamon'lar çağırılıyor. Böylece systemd açılışı hızlanmış oluyor.
