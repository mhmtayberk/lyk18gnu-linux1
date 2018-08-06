## E-Posta İnternet Devinimi

### Bir E-Posta İnternet'de Nasıl Bir Yol İzler?

- Gri liste uygulaması.

- Alan adı geçerli bir alan adı mı?

- Mail'i getiren sunucunun reverse DNS kaydı var mı?

- Mail SPF kaydındaki sunucudan mı geliyor?

- Mail'in geldiği sunucu, domain key ile örtüşüyor mu?

- Mail'i getiren sunucu IP'si RBL listelerinde var mı?

- Header_Cheks (Saat, başlık bilgisi düzgün mü?)

- Body_Cheks (Mail'in içinde belirli bir kelime taranır)

- Content Security (Anti Virüs vs.)



### Keywords

- SPF

- DNS Query

- Domain Key

- RBL

- STMP / SMTPS

- POP3 / POP3S - IMAP / IMAPS



### Kara Liste Servisleri İle Entegrasyon (RBL)

- Spamhaus, Spamcop, Sorbs sıkça kullanılan RBL servisleridir.

```
smtpd_client_restrictions = reject_maps_rbl,
reject_rbl_client sbl.xbl.spamhaus.org
reject_rbl_client bl.spamcop.net
reject_rbl_clien xxx.sorbs.net
```



#### Notlar

- POP3'te posta sunucusu açıldıktan sonra mailler bilgisayara indirilir ve posta sunucusunda mail kalmaz.

- IMAP'te gönderilen / alınan tüm E-Posta'lar posta sunucusunda tutulur.

- IMAP bütün cihazlar (tablet, PC, telefon vs.) aynı noktaya point ettiği için çoklu kullanım mümkündür.

- IMAP'te yalnızca okunmak istenen E-Posta içeriği açıldığı zaman bilgisayara indirilir. Buda büyük bir avantajdır.

- IMAP'in bir avantajı da posta sunucusunun yedeği alındığı takdirde mail kullanıcılarının da yedeğinin alınmasıdır.
