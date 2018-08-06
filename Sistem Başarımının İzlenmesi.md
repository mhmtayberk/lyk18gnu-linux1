## Sistem Başarımının İzlenmesi

### Kaynak Kullanımının İzlenmesi

- `top` uygulaması çalışırken **P** tuşuna basarak çalışan süreçler işlemci kullanım oranlarına göre, **M** tuşuna basarak bellek kullanım oranlarına göre sıralanabilir.

- Bilgisayarın PCI veriyolları ve bunlara takılı aygıtlar `lspci` komutu ile sorgulanabilir.



### Disk Kullanımının İzlenmesi

- `df -h` komutu ile disk kullanımının izlenmesi mümkündür.



#### Notlar

- `lscpu` -> CPU bilgisi görüntülenir.

- `cat /proc/cpuinfo` -> CPU bilgisi görüntülenir.

- `free -h` -> RAM bilgisi görüntülenir.

- `cat /proc/meminfo` -> RAM bilgisini daha detaylı görüntüler.

- `fdisk -l`-> Sürücü sayısını ve sürücü bilgilerini görüntüler.

- `fdisk -l | grep dev` -> Sürücü sayısını ve sürücü bilgilerini görüntüler.

- `uname -a` -> Çekirdek sürümünü gösterir. Bazen distro bilgisini de görüntüler.

- `cat /etc/issue` -> Linux'un hangi distro olduğunu görüntüler. Bazen göstermeyebilir.

- rpm veya dpkg yazarak Linux'un distro'su hakkında olasılıklar düşürülebilir.

- `cat /etc/os-release` -> Linux'un hangi distro olduğunu görüntüler.

- `crontab -l `-> Root'un cron'u olup olmadığını görüntüler.

- `cat /etc/cron. <TAB> <TAB>` -> Cron bilgilerini görüntüler.

- `uptime` -> Sistemin load average'ını gösterir. (Sırası ile 1, 5 ve 15 dakikalık yük ortalamasını gösterir.)

- `top` -> Çalışan process'ler hakkında bilgi verir.

- `htop` -> Çalışan process'ler hakkında bilgi verir.

- `vmstat 1 5` -> 1 saniye ara ile 5 kere sistemden bilgi toplar. swpd, free, buff, cache, si, so, bi, bo, id, wa vs. bilgilerini verir.

- `dmidecode` -> Sistem hakkında aşırı derecede detaylı bilgiler verir. Çok fazla parametresi vardır.

- `dmidecode -t system` -> Sistemin sanal makine mi, fiziksel makine mi olduğu bilgisini verir.
