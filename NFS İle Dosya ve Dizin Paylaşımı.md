## NFS İle Dosya ve Dizin Paylaşımı

### Ağ Üzerinden Dosya ve Dizin Paylaşımı : NFS

- UNIX'ler için ağ üzerinden dizin paylaşım sistemi.

- NIS ile birlikte kullanıldığında anlamlı olur.

- Sun Microsystems tarafından geliştirilmiştir.

- Uzak bilgisayardan paylaştırılan dizin yerel dizin hiyerarşisine bağlanır.



### NFS Sunucu Yapılandırması

- NFS sunucu süreçlerini çalıştırmak.

- **/etc/exports** dosyasını düzenlemek.



### NFS İstemci Yapılandırması

- Bir SUSE Linux'un NFS istemci olabilmesi için; `zypper in nfs-client`

- Paylaşımların bağlanması; `mount nfssunucu:paylaşım bağlanmanoktası`



### NFS Bağlama Seçenekleri

| SOFT Bağlama                                                                                |
| ------------------------------------------------------------------------------------------- |
| Dosya istemi başarısız olursa NFS istemci dosya isteminde bulunan sürece hata raporu verir. |
| Bu raporlamayı bazı programlar ele almakta iken bazıları alamamaktadır.                     |
| **HARD Bağlama**                                                                            |
| Dosya istemi başarısız olursa NFS istemciden dosya isteminde bulunan süreç askıya alınırsa; |
| Askıya alınan süreç öldürülemez veya kesilemez (eğer intr bağlama seçeneği kullanılmazsa)   |
| Tavsiye edilen NFS bağlama biçimidir.                                                       |



#### Notlar

- NFS büyük kolaylık sağladığı kadar doğru şekilde konfigüre edilmezse çok ciddi sorunlar çıkartabilir.

- YaST ile NFS server tanımlaması yapılabilmekte.

- Bağlama mount komutuyla çalışma anında ya da /etc/fstab dosyasına eklenerek yapılır.

- NFS ile paylaştırılmış dizinler yerel dosya sistemine bağlanılarak çalışır.

- SAMBA Linux sistemlerin NetBios üzerinde çalışmasını sağlar. Fakat SAMBA 4 ile beraber bir domain controller olarak da kullanılabilmekte. Günümüzde yalnızca SAMBA'yı kullanarak active directory her şeyi ile domine edilebilmekte.
