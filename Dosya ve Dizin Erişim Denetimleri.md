## Dosya ve Dizin Erişim Denetimleri

### Bilgisayar Açılış Anında Yaşananlar

1. BIOS donanımları tarar. (Post Check)

2. Boot Order'a bakar.

3. Boot Order işletim sistemi olduğunu Master Boot Record'a ve Boot Flag'a bakarak anladı.

4. GRUB / Lilo / Windows Loader devreye girer.

5. Loader, sistem çekirdeğini belleğe yükler.

6. Çekirdek açıldığı zaman ilk olarak Post Check işlemi yapar.

7. İkame için gerekli servisler başlatılır.

8. Başlangıca eklenmiş servisler başlatılır. (Linux'ta en kritik olarak **sislog** bulunur.)

9. Login ekranı gelir.



### drwxr-x 1 mhmtayberk users

- rwx -> Okuma var, yazma var, çalıştırma var.

- tw- ->Okuma var, yazma var, çalıştırma yok.

- r-- ->Okuma var, yazma yok, çalıştırma yok.



### Yetkilerin Düzenlenmesi

- `chmod [user group other] [+ -] [rwxst] [, ...] dosya/dizin`

- u -> Sahibinin.

- o -> Diğerlerinin.

- g -> Grubun.

- Örneğin; `chmod o-rxw dosya.txt` -> others'ın dosya.txt üzerindeki okuma, yazma, çalıştırma hakkını kaldırdık.

- Örneğin; `chmod u+r dosya.txt` -> user'a dosya.txt için okuma hakkı verdik.



| User    | Group   | Other   |
| ------- |:-------:| -------:|
| r  w  x | r  w  x | r  w  x |
| 4+2+1   | 4+2+1   | 4+2+1   |
| 7       | 7       | 7       |

- Bu sayısal değerler 8'lik tabandan gelmektedir.

- Örnek bir tablo oluşturacak olursak : 

| User    | Group   | Other   |
| ------- |:-------:| -------:|
| r  w  x | r  -  x | -  x  - |
| 4+2+1   | 4+0+1   | 0+1+0   |
| 7       | 5       | 1       |

### Özel Erişim Yetkileri

- **setuid (s)** -> Sahibinin çalıştırma yetkisi olan dosya kim tarafından çalıştırılırsa çalıştırılsın sahibi tarafından çalışmış gibi davranır.

- **setgrid (s)** -> Grubunun çalıştırma yetkisi olan dosya kim tarafından çalıştırılırsa çalıştırılsın sahibi tarafından çalışmış gibi davranır.

- **sticky (t)** -> Dizinlerdeki yetkisi, dizinin içine herkesin yazabilmesini fakat başkalarına ait dosyaları/dizinleri değiştirememesini ve silememesini sağlar. (Örneğin /tmp)

- s : 4,  s : 2,  t : 1



### Dosya Yaratma Modu Maskesi

- Ön tanımlı olarak **unmask** `022` dir.

- Temel mantığı yanında verilen parametre ile belirli flag'ı maskelemek üzerinedir.



| Maskelenmemiş | rwx | rwx   | rwx   |
| ------------- | --- | ----- | ----- |
| Maskelenmiş   | rwx | r - x | r - x |

- Unmask `000` olduğunda;

- - Dizin Hakları ; `777`

  - Dosya Hakları ; `666`



### Dosya Sahip / Grup Değişikliği

- `chown [-R] yenisahip dosya/dizin` komutu ile dosyanın/dizinin sahibi değiştirilir.

- `chgrp [-R] yenigrup dosya/dizin komutu` ile dosyanın/dizinin grubu değiştirilir.



### chown

- `chown ayşe.users sunum.ppt`



#### Notlar

- Dizinler için erişim yetkileri dosyalar için olandan farklıdır.

- Her dizinin izini (permission) kendisi ile alakalıdır.
