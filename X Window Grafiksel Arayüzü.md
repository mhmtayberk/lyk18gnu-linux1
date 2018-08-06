## X Window Grafiksel Arayüzü

### X Window Nedir?

- UNIX ve türevleri için X Konsorsiyumu tarafından standartlandırılmış ağ tabanlı grafiksel arayüzüdür.

- Mevcut sistem sürümü X11R6'dır

- Karmaşık ve kapsamlı bir standarttır.

- Özgür bir X yazılım kümesi XFree86 projesi tarafından üretilmektedir.



### İşlemci ve Sunucu Mimarisi

- X sunucusu, X istemcilerine grafik arabirimi sunmak için çalışan yerel yada ağ temelli bir sunucudur.

- Pencerelerin gösterildiği bilgisayar **sunucu**, uygulamanın çalıştığı bilgisayar **istemci** olarak isimlendirilir.

- Ağ üzerinde kullanılma zorunluluğu bulunmamaktadır.

- Aynı bilgisayar hem istemci, hem sunucu olabilir.

- Devamlı çalışır olmak zorunda değildir.

- X Window, kullanıcılar tarafından başlatılabilir ve yine kullanıcılar tarafından durdurulabilir.



### Pencere Yöneticileri

- Dileyenler bu zeminin üzerine kendi arayüzlerini programlayabilirler.

- Farklı arayüzler farklı biçimde davranabilir ve farklı biçimde görünebilir.

- Arayüz yazılımlarına **Pencere Yöneticisi** denir.

- Popüler bazı pencere yöneticileri şunlardır; FluBox, IceWM, BlackBox, AfterStep, SawFish, WindowMaker, FVWM, MetaCity...



### Masaüstü Ortamları

- Sistemin kullanıcı arayüz tamamiyle değiştirilebilir.

- KDE ve GNOME en popüler masaüstü ortamlarıdır.

- Masaüstü ortamları, pencere yöneticisi, ilgili yapılandırma programları, çok genel uygulama yazılımları, simgeler, sesler ve temalardan oluşan bir **paket**tir.

- Masaüstü ortamları, yalın bir pencere yöneticisinden daha fazla sistem kaynağı tüketir.



### GNOME Masaüstü Ortamı

- The GNU Network Object Model Enviroment.

- Kullanıcı dostudur.

- CORBA, XML gibi en yeni teknolojilerden yararlanılarak geliştirilmektedir.

- Yazılım geliştiriciler için güçlü bir yazılım geliştirme platformu mevcuttur.

- Türkçe de dahil pek çok dili desteklemektedir.



### KDE Masaüstü Ortamı

- Tamamı LGL/GLP lisansı ile dağıtılmaktadır.

- Öntanımlı pencere yöneticisi kwm'dir.

- 1996 yılından beli geliştirilmektedir.

- Dosya yöneticisi Dolphin'dir.

- Tamamı yerelleştirilmiştir.



### Masaüstü Ortamlarının Değiştirilmesi

- X'e login olma aşamasında grafiksel arabirimden istenilen masaüstü ortamı ya da pencere yöneticisi seçilebilir. 

- ~/.xsession dosyasına GNOME için; 'exec gnome-session' ; KDE için 'exec startkde' satırları eklenebilir.

- X oturumu konsoldan `startx` komutu ile başlatılıyorsa;

- ~/.xinitrc dosyasına GNOME için 'exec gnome-session'



#### Notlar

- KDE'nin K-Mail adında kendi E-Posta istemcisi bulunmaktadır.

- Başka bir E-Posta istemcisi de ThunderBird'dür.

- Çok eski bir dosya yöneticisi olan NortonCommader'ı UNIX için de yapmışlar. (MidNight Commander)

- Nautilus, Dolphin, Midgniht Commander, Krusader, PCmanFM, Konqueror, XFE File Manager, Nemo, Thunar, SpaceFM, Caja, Ranger Console, Command Line, Worker, Emacs, ROX, Spacemacs, JFile bazı dosya yöneticilerindendir.

- Open SUSE'ye özgü **Yast Kontrol Merkezi** bulunmaktadır. SUSE Enterprise Server, SUSE Enterprise Dekstop'da da Yast bulunmaktadır. SUSE'nin kendi geliştirdiği bir araçtır. Diğer dağıtımlarda Yast'a karşılık gelen hazır olarak kurulan bir araç bulunmamaktadır. Komut satırında yapılan önemli birçok iş grafiksel arayüz yardımı ile yapılabilmektedir.

- **Snaptic Packet Manager** : Paketleri ve uygulamaları kurmak için görsel arayüz sağlayan bir araçtır.

- Terminator, xterm, Tilda, Guake, Timux, Yakuake, ROXTerm, Eterm, Rxvt, Wterm, LXTerminal, Konsole, TermKit, st, Gnome-Terminal, Final Term, Terminology, LilyTerm, Sakura,rxvt-unicode bazı terminallerdir.
