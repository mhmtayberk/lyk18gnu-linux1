## systemd Servis Kontrol Sistemi

### systemctl Aracı - Servislerin Listelenmesi

- `systemctl list-unit files` -> Tüm unit fileları durumları ile birlikte listeler.

- `systemctl reboot` -> Yeniden başlatma.

- `systemctl start <hizmet adi>` -> Hizmet başlatır.

- `systemctl stop <hizmet adi>` -> Hizmeti durdurur.

- `systemctl restart <hizmet adi>` -> Hizmeti yeniden başlatır.

- `systemctl status <hizmet adi>` -> Hizmet bilgisini verir.

- `systemctl enable <hizmet adi>` -> Sistemi açılışa ekler.

- `systemctl disable <hizmet adi>` -> Sistemi açılıştan kaldırır.

- `systemctl mask <hizmet adi>` -> Sistemi elle başlatmayı engeller.

- `systemctl unmask <hizmet adi>` -> Sistemi elle başlatma engelini kaldırır.

- `systemctl list-unit-files -type service -all` -> Devrede olan olmayan tüm servisleri gösterir.



### systemd Yapılandırma Dosyaları

- Paket yöneticisi üzerinden kurulan uygulamalara ait unit file dosyaları **/usr/lib/systemd/system** dizini altındadır.

- Default olarak gelen unit file dosyaları **/etc/systemd/system** dizini altındadır.

- Run time'da oluşturulan unit file dosyaları **/run/systemd/system** altında bulunur.

- `.service` -> Servisleri aittir.

- `.target` -> Birden çok servisi toplu halde yönetebilmek için hazırlanmış dosyalardır. (Servis demetleri)

- `.mount` -> Sisteme bağlanması istenen disk bölümleri için direktifleri içerir.

- `.swap` -> swap yapılandırması ile ilgili direktifleri içerir.

- `systemctl get-default` -> Ön tanımlı target'ı görüntüler.

- `systemctl list-units --type target` -> Sistemdeki tüm target'ları görüntüler.

- `systemctl set-default <target adı> .target` -> Bir sebeple ön tanımlı target'ı değiştirmek isterseniz.

- `systemctl isolate <target adı> .target` -> An itibari ile runlevel'ı değiştirmek için kullanılır.



### Açılışa Betik / Servis Ekleme (SUSE)

- Sisteme eklenmesi istenen betik **Unit File** yapısında hazırlanmalı ve **/usr/lin/systemd/system** dizinine konulmalıdır.

- Servisi başlatmak için : `systemctl start <hiz_adi>`

- Servisi açmak için : `systemctl enable <hiz_adi>`



### Unit File Yapısı

```
[Unit]
Description= Genel açıklama.
After=

[Service]
EnvironmentFile= Çalışması için ihtiyaç duyduğu programlar.
ExecStartPre= Servis çalıştıktan sonra ilk yapılması gereken işlem.
ExecStart= Hangi programların çalışması gerektiği.
ExecReload= Yeniden çalışması gereken programlar.
KillMode= Öldürülmesi gereken programlar.

[Install]
WantedBy= Araması gereken target.
```

### Unit File - Simple Service Örneği

```
[Unit]
Description=Foo

[Service]
ExecStart=/usr/sbin/foo-deamon

[Install]
WantedBy=multi-user.target
```

- Servisi başlatır ve geçer. Sonlanmasını beklemez.



### Unit File - One Shot (Tek Atış)

```
[Unit]
Description=Cleanup old Foo data

[Service]
Type=oneshot
ExecStart=/usr/sbin/foo-cleanup

[Install]
WantedBy=multi-user.target
```

- Servisi başlatır sonlanmasını bekler.



### Unit File - Stoppable One Shot (Durdurulabilir Tek Atış)

```
[Unit]
Description=Simple firewall

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=/usr/local/sbin/simple-firewall-start
ExecStart=/usr/local/sbin/simple-firewall-stop

[Install]
WantedBy=multi-user.target
```



### Unit File - Geleneksel Forking Servisi

```
[Unit]
Description=Some simple daemon

[Service]
Type=forking
ExecStart=/usr/sbin/my-simple-daemon -d

[Install]
WantedBy=multi-user.target
```

- Tüm deamon'larda kullanıyoruz.



### Unit File Hazırlama

1. **/usr/lib/systemd/system/deneme.service** 'e unit file'ımızı oluşturduk.

2. **/usr/local/deneme.sh**

3. `route -n` veya `ip r gateway`'i öğrenip deneme.sh scriptini oluşturduk.

4. `chmod +x deneme.sh`

5. `systemctl start deneme.service`

6. `systemctl status deneme.service`



### Unit File'ı Başlangıca Ekleme

- `systemctl enable deneme.service`



### systemd.timer (Cron Benzeri systemd Servisi)

- systemd 'nin cron'u diyebiliriz. Yani bir nevi zamanlayıcı.

- Root olarak timer'ı başlatmak için; `#systemctl start <timer adı> .timer`

- Timer'ı açılışa eklemek için; `#systemctl enable <timer adı> .timer`



### Timer Yapısı

```
[Unit]
Description=Minute Timer

[Timer]
OnBootSec=5min
OnCalendar=*:0/1
Unit=minute-timer.target

[Install]
WantedBy=basic.target
```



### journalctl Aracı ve Sistem Kayıtları

- Kayıtları okumak için kullanılır.

- Normalde kayıtlar **/var/log/journal** altında tutulur.

- systemd journal /**etc/systemd/journal.conf** ile özelleştirilebilir.

- journal kapatiseti ilgili dosya sisteminin büyüklüğünün %10'u olarak ön tanımlıdır. Bu değer journald.conf dosyasında **SystemMaxUse=switch** ile değiştirilebilir.

- `journalctl -u TAB TAB` -> Tüm log'ları listeler.

- `journalctl -u sshd.service` -> sshd.service ile ilgili bilgileri listeler.

- `journalctl -f` -> Sistemdeki tüm aktiviteyi listeler.

- `journalctl -b` -> Boot logları listeler.

- `journalctl -k` -> Kernel'e ait logları listeler.

- `journalctl --since=yesterday` -> Dünkü tüm kayıtlar anlamındadır.

- `journalctl -b -p err` -> Boot log'daki errorları listeler.

- `journalctl --since"2015-09-03 14:00:00" --until="2015-09-03 23:59:9"` -> Zaman aralığındaki logları listeler.

- `journalctl -u sshd --since=06:00 --until:11:30` -> Saat aralığındaki sshd loglarını listeler.



### journalctl ile Özelleştirme ve Kayıt Yönetimi

- Logları tty12'de sürekli akıtmak için **/etc/systemd/journal.conf** dosyasına : 

```
[Journal]
ForwardToConsole=yes
TTYPath=/dev/tty12
MaxLevelConsole=info
```

- satırları eklenmelidir.

- journald.conf'da bir değişiklik yaptıktan sonra `#systemctl restart systemd-journald` ile journald restart edilmeli.

- Başka bir Linux'a ait journal kayıtlarını incelemek için `#journalctl -D /mnt/var/log/journal -xe`



### systemd-analyze Aracı

- `systemd-analyze time` -> Servislerin açılış sürelerini gösterir.

- `systemd-analyze blame` -> Açılışta run edilen servislerin açılması için harcanan zamanları detaylı bir şekilde gösterir.

- `sysdemd-analyze critical-chain` -> Servislerin açılış sürelerini tree şeklinde listeler. (Aşağıdan yukarıya okunmalı)

- `systemd-analyze plot` -> Servislerin açılış sürelerini detaylı bir şekilde grafik olarak döker.. Örnek; systemd-analyze plot > /home/mhmtayberk/systemd.svg ardından chown mhmtayberk:users /home/mhmtayberk/systemd.svg



### systemd-cgtop Aracı

- `systemd-cgtop` şeklinde kullanılır.

- Çalışan servislerin ne kadar RAM tükettiği, üzerinde bulunan iş sayısı, CPU meşguliyeti sayısını vs. listeler.



### systemd-loginctl Aracı

- systemd giriş yöneticisini (logind) yönetmek için loginctl kullanılır.

- `loginctl <TAB><TAB>` şeklinde bir kullanımı bulunmaktadır. Örnek kullanımı; loginctl list-users ile sisteme bağlı kullanıcılar listelenebilir.

- `loginctl session-status <number>` -> number kullanıcısının session bilgisi görüntülenebilir.

- `loginctl terminate-session <number>` -> number kullanısı terminate edilebilir.



### systemd-cgls Aracı

- systemd çalışma mantığında yer alan kontrol gruplarının durumunu ve hangi kontrol grubunda (target'lar) hangi servislerin çalıştığını kontrol etmeye yarar.



#### Notlar

- systemd yalnızca bir açılış yapısı değil kocaman bir ahtapottur :)

- `systemctl list-unit files | grep service | wc -l` -> Örnek olarak sistemde çalışan servislerin sayısını gösterir.

- journald dosyaları binary olarak saklanır bu çok büyük bir eksidir. Sistem log kayıtlarını kaybetmeye yol açabilir.

- Log'ların zaman damgası ile saklanması hukuki açından oldukça önemlidir. Zaman otoritesinden abonelik alınması gerekiyor. Belgenin hash bilgisi gönderilir ve karşı hash bilgisi saklanır. (TUBİTAK ücretsiz veriyor)

- Merkezi kayıt sunucusu da log kaydının yedeğinin alınması ve hukuki açıdan oldukça önemlidir.

- systemctl `isolate rescue.target` şeklinde sistemi **Rescue Mod**'a getirebiliriz.

- **Hatırlatma** : systemd ile klasik Linux arasındaki fark şudur; klasik Linux açılışında deamon'lar birbirini beklediği için yavaş açılmasına sebep olmaktaydı. systemd'de ise deaoman'lar önceden çalıştırılıyor ve minimum seviyede bekletiliyor. Lazım olduğu zaman da deamon'lar çağırılıyor. Böylece systemd açılışı hızlanmış oluyor.
