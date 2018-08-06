## Veritabanı Yönetim Sistemlerine Giriş

### Temel Kavramlar (Keywords)

- Veritabanı

- Veri

- Veri Modelleri

- İlişkisel Veri Modeli

- İlişki Türleri

- İlişki (Relation)

- Normalleştirme

- Foreign Key

- ACID

- Transaction

- İlişkisel Veritabanı

- İlişkisel Veritabanı Yönetim Sistemleri (RDBMS)



### Veri Modelleri

- **Flat Data Model :** Veriler satır satır yazılı. Fakat efektif değil. Tek tek veriler sayılmaktaydı. Geliştirilince satır numaraları eklenmiş fakat çok büyük veritabanları için yine efektif değildi.

- **Hierarchical Data Model :** Veri dizinlere ayrılmış. Dizin içinde dizin şeklinde bir veri ağacı oluşmuş. Böl ve yönet mantığı. Fakat bir dizin silindiği zaman alt dizindeki tüm veriler silinmiş oluyordu.

- **Network Data Model :** Dizinlerin alt dizinlerine hep aynı yoldan gitmek yerine farklı bir dizin silsilesi ile de gidilebilmek amaçlanmış. 

- **Relational Data Model :** Her şey satır ve sütunlardan oluşsun mantığı var. (Excel mantığı / Rows and columns) Column'lara isimler verilmiş. Row'lara ise değişken verilen girilmiş. Ve oluşan bu tabloya SQL dili ile sorgular gönderilerek elde edilmek istenen veri çekilmeye başlanmış. Her bir bilgiye de field denilmiş.



### İlişkisel Veritabanı Tasarımı ve İlişki Kavramı

- İlişkisel veritabanında olabilecek ilişki türleri;

| Birebir İlişki         |
| ---------------------- |
| **Birden Çoğa İlişki** |
| **Çoktan Çoğa İlişki** |



### Normalleştirme / Normalizasyon

- Normalizasyon, veritabanlarında çok fazla sütun ve satırdan oluşan bir tabloyu tekrarlardan arındırmak için daha az satır ve sütun içeren alt kümelerine ayrıştırma işlemidir.

- Hedefleri / Seviyeleri;

- Veri tabanında bulunan tabloların ilişki (bağlantı, join) kurulabilir şekilde tasarlanması ve tablolarda veri tekrarı (repeating groups) bulunmaması. (1NF / Normal Form)

- Eğer mümkünse aday anahtar (candidate key) olarak tanımlanabilecek bir anahtara bütün diğer kolonların tam bağlı olması ve herhangi bir alt kümesine bağlı olmaması. (2NF / Normal Form)

- Hatta, veritabanında bulunan anahtarların birbirine fonksiyonel olarak bağlı olması. (3NF / Normal Form)



### Veritabanı Yönetim Sistemi Bileşenleri

- **Bellek Yönetisini (Storage Manager) -> Dosya Yöneticisi (File Manager) ve Tampon Yöneticisi (Buffer Manager)**

- Hareket Yöneticisi (Transaction Manager)

- **Sorgu İşleyicisi (SQL)**

- Veri İşleme Dili (Data Manipulation Language - DML)

- Veri Tanımlama Dili (Data Definition Language - DDL)

- Veri Kontrol Dili (Data Control Language - DCL)



### Transaction (Hareket)

- Bir bütün oluşturan ve tutarlılık açısından veri tabanı üzerinde birlikte gerçekleştirilmesi gereken işlemler bütünüdür. Örneğin; bir bankada bir veritabanı olduğunu var sayalım ve birçok field olduğunu var sayalım. Bir havale işlemi gerçekleşiyor. (1 transaction 5 işlem) Kural şu; X'in bakiyesi güncellenene kadar transaction sonlanmaz.

- Bir hareketin başarılı bir şekilde gerçekleşebilmesi için ACID ilkelerine uyması gerekir.



### ACID İlkeleri

- Bölünmezlik (Atomicity)

- Tutarlılık (Consistency)

- İzolasyon (İsolation)

- Dayanıklılık (Durabilty)



### Bilinen Veritabanı Yönetim Sistemleri

- IBM DB2

- Oracle

- Sybase

- MS SQL

- MySQL

- Maria DB

- Postgre SQL : Transaction, inheritance, trigger, stored procedure destekler. Tablo başına 64 TB tutulur. Ücretsizdir. Çok güçlüdür ve güvenlik ön plandadır.



#### Notlar

- Veri bilgidir.

- Veritabanları ilk oluştuğu zamanlar düz metinler idi. Veriler alt alta yazılı satırlardı. Ancak bu hiç efektif değildi.

- Network Data Model'den Relational Data Model'e geçişte ilk Veritabanı Yönetim Sistemi (DBMS) ortaya çıkmış.

- DBMS'de gönderilen SQL cümleciği önce compile edilir daha sonra gönderilir.
