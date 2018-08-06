## Apache Web Sunucusu

### Apache Nedir?

- Apache web sunuusu NCSA Web sunucusu temellidir.

- NCSA sunucusunun üzerine yapılan yamalar ile geliştirilmeye başlanmıştır.

- Web sunucusu pazarın yaklaşık %60'ını elinde bulundurmaktadır.

- Günümüzde 1.x ve 2.x olmak üzere birbirinden mimari olarak farklı iki seri olarak geliştirilmektedir.

- Tüm Linux dağıtımlarının ön tanımlı web sunucusu Apache'dir.

- Hata iletileri özelleştirilebilmektedir.

- Detaylı erişim kayıtları tutabilmektedir.

- Yapılandırması tek bir dosya üzerinden kolaylıkla yapılmaktadır.

- lighttpd, nginx vs.

- memcached, APC vs.



### Apache Olanakları

- Doğrulama, yetkilendirme ve erişim denetimi.

- CGI ile dinamik içerik.

- Handlers.

- Kayıt dosyaları.

- Server Side Includes.

- URL Mapping.

- URL Rewriting.

- Virtual Hosts.



### Apache'nin Çalıştırılması

- Linux Başlangıç Betikleri :

  ```
  
  	* /etc/rc.d/init.d start
  	* 
  /etc/rc.d/init.d stop
  	* 
  /etc/rc.d/init.d restart
  ```

  

- apachectl ile :

  ```
  
  	* apachectl start
  	* 
  apachectl stop
  	* 
  apachectl configtest
  ```

  

### httpd.conf - 1

```
ServerType standalone
ServerRoot "/etc/httpd"
MinSpareServers 5
MaxSpareServers 10
```



### httpd.conf - 2

```
KeepAlive On
MaxKeepAliveRequests 100
KeepAliveTimeout 15
```



### httpd.conf - 3

```
User nobody
Group nobody
ServerAdmin sysadmin@mehmetayberk.com
DocumentRoot /var/www/html
AccessFileName .htaccess
DefaultType text/plain
HostnameLookups Off
ServerSignature On
```



### httpd.conf - 4

```
Port 80
BindAddress *
NameVirtualHost 111.222.33.44
```



### Erişim Denetim Yapılandırması - 1

- `<Directory>` ve `</Directory>`

  ```
  Options [+-]Özellik...
  AllowOverride All
  
  <Directory /var/www/html>
  Options Indexes FollowSymLinks Includes
  AllowOverride All
  Order Allow,Deny
  Allow from All
  </Directory>
  ```

  

- Belirli HTTP Yöntemlerine Erişim Denetimi

```
<Limit>ve</Limit>

<Limit GET POST>
        Order allow,deny
        Allow from all
</Limit>
```



### Erişim Denetim Yapılandırması - 2

- Dizinde .htaccess adında dosya yaratılır : 

  ```
  AuthType Basic
  AuthName "Sınırlı Erişim."
  AuthUserFile /var/www/users
  AuthGroupFile /var/www/groups
  <Limit GET POST>
  Require group admin
  </Limit>
  ```

  

- AuthUserFile : 

  ```
  user1:ŞİFRE
  user2:ŞİFRE
  user3:ŞİFRE
  ```

  

- AuthGroupFile : 

  ```
  admin: user1 user2
  operator: user1 user2 user3
  ```

  

### Apache Modülleri ve Ayarları - 1

- **mod_dir** - "trailing slash" yönlendirmesini yapar ve dizin indisi dosyalarını sunar.

  ```
  <IfModule mod_dir.c>
  DirectoryIndex index.html index.php index.shtml index.htm Default.htm default.htm
  </IfModule>
  ```

  

- **mod_alias** - Dosya sisteminin değişik dizinlerini URL'e bağlar ve yönlendirir.

- **mod_access** - İstemci ismine ve IP adresine göre erişim denetimi sağlar.

  

### Erişim Kayıtlarının İncelenmesi

- Erişim kayıtlarının saklandığı dosya **/var/log/httpd/access_log** dosyasıdır.

- Hata kayıtlarının saklandığı dosya **/var/log/httpd/error_log** dosyasıdır.

- Tüm erişim kayıtları tek bir dosyada tutulabilir.

- Web sunucusu erişim kayıtlarının incelenmesi için webalizer, webtrends log analyzer gibi uygulamaların kullanılması daha pratiktir.

- Erişim kayıtları 4 farklı şekilde tutulabilir.

- Yaygın (Common) Kayıt Biçimi

- Birleştirilmiş (Combined) Kayıt Biçimi

- Çoklu Erişim (Multiple Access) Kayıt Biçimi

- Koşula Bağlı (Conditional) Kayıt Biçimi
