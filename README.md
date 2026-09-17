# İç Denetim Standardizasyonu ve Bulgulardan Eğitim Programı

Çok mağazalı bir bölgede iç denetimleri (mağaza müdürlerinin birbirini denetlediği çapraz denetim) ve esas denetimleri **tek ortak yapıda** toplayan, puanlayan, düzeltici-önleyici faaliyetleri (DÖF) izleyen ve **en sık tekrar eden uygunsuzluklardan eğitim önceliği** çıkaran Excel sistemi.

> **Not:** Bu dosya, bir kahve zincirinde 16 mağazalık bölge için kurduğum ve yürüttüğüm yapının **yeniden kurulmuş sürümüdür**. Orijinal dosyalar (şirketin SharePoint ortamındaki iç denetim dosyası ve denetim takvimi) elimde olmadığı için yapı, sistemin nasıl çalıştığı hatırlanarak baştan oluşturulmuştur. Puanlama yöntemi (önem derecesine göre ceza katsayıları) ve gıda güvenliği denetimindeki soru dağılımı, elimde kalan eski bir bölge raporundan alınmıştır.
>
> Mağazalar, denetim maddeleri, bulgular, tarihler ve faaliyetler uydurmadır. Madde metinleri genel ifadelerdir; şirketin denetim formundan alınmamıştır.

## Hangi problemi çözüyor

Bölgede üç denetim vardır: genel operasyon (ASA), kayıp önleme ve çalışan güvence (PAP), gıda güvenliği (RSA). Bu yapı kurulmadan önce sonuçlar denetim PDF'lerinden tek tek okunuyordu; mağazalar arasında karşılaştırma, tekrar eden bulguların tespiti ve iç denetimle esas denetimin kıyaslanması yapılamıyordu.

Bu sistemde:

- **Karşılıklı iç denetim** çeyrekte bir planlanır. Yakın mağazaların müdürleri birbirini denetler; her müdür uzman olduğu denetim türüne gider. Takvim, yanlış atamaları (kendi mağazası, uzmanlık dışı) işaretler.
- **Tahmini esas denetim tarihleri** aynı takvimde tutulur, yaklaşanlar uyarı verir.
- Her denetim ve her bulgu **aynı formatta** kaydedilir. Puan, bulgulardan otomatik hesaplanır.
- **Dashboard** her mağazanın iç ve esas denetim puanını yan yana gösterir. Aradaki fark, iç denetimin gerçeği ne kadar yansıttığını ölçer. Mağazalar birbirinin sonucunu görür.
- **Öncelik listesi** en sık tekrar eden uygunsuzlukları önem derecesiyle ağırlıklandırarak sıralar; her maddenin eğitim konusunu ve en sık görüldüğü mağazayı gösterir. Bölge eğitim programı bu listeden hazırlanır, mağaza bazlı aksiyonlar da buradan belirlenir.

## Öncesi

İç denetim sonuçları ortak bir yapıda tutulmuyordu; esas denetim sonuçları denetim PDF'leri üzerinden takip ediliyordu.

## Sayfalar

| Sayfa | Ne yapar |
|---|---|
| `Nasil_Kullanilir` | Akış, puan hesabı, kısaltmalar |
| `Dashboard` | Mağaza × denetim türü: iç puan, esas puan, fark; sıra; bulgu, kritik bulgu, açık ve gecikmiş DÖF sayısı; takvim durumu; grafik |
| `Oncelik_Listesi` | En sık tekrar eden 15 uygunsuzluk (tümü veya tek denetim türü); eğitim konusu bazında toplam ve grafik |
| `Madde_Magaza` | Madde × mağaza tekrar matrisi (ısı haritası) |
| `Denetim_Takvimi` | Çeyreklik iç denetim rotasyonu, durum ve rotasyon kontrolü; tahmini esas denetim tarihleri |
| `Denetimler` | Her denetim bir satır: tarih, mağaza, tür, tip (iç / esas), denetçi, bulgu sayıları, puan, hedef durumu |
| `Bulgular` | Her uygunsuzluk bir satır: denetim no, madde kodu, açıklama; madde bilgileri otomatik gelir |
| `DOF_Takip` | Bulguya bağlı faaliyet, sorumlu, termin, kapanış; durum ve gecikme günü |
| `Madde_Listesi` | Denetim maddeleri: tür, kod, metin, kategori, önem derecesi, eğitim konusu |
| `Magazalar` | Mağaza, yakınlık grubu, müdürün uzman olduğu denetim |
| `Ayarlar` | Bugünün tarihi, ceza katsayıları, denetim başına toplam soru ve hedef puan, uyarı süresi |

## Hesaplar

- **Ceza puanı** = kritik bulgu × 2 + major bulgu × 1,5 + minör bulgu × 1
- **Denetim puanı** = (toplam soru − ceza puanı) ÷ toplam soru × 100
- **Hedef puan**: ASA 90, PAP 85, RSA 90
- **İç − esas farkı**: pozitif ve büyükse iç denetim, esas denetimin bulduğu sorunları yakalayamamıştır
- **Ağırlıklı skor** (öncelik listesi) = maddenin bulgu sayısı × önem katsayısı
- **DÖF durumu**: kapanış termin içinde ise *Kapandı*, sonra ise *Geç kapandı*; kapanış yoksa ve termin geçtiyse *Gecikmiş*, geçmediyse *Açık*
- **Takvim durumu**: gerçekleşme tarihi varsa *Yapıldı*; yoksa plan tarihi geçmişse *Gecikti*, 30 gün içindeyse *Yaklaşıyor*

## Kullanım

Makro yoktur, kurulum gerekmez. `ic-denetim-sistemi.xlsx` Excel 2010 ve sonrası ile LibreOffice'te açılır.

1. Çeyrek başında `Denetim_Takvimi`'ne rotasyonu ve tahmini esas denetim tarihlerini girin. Rotasyon kontrolü sütununda kırmızı satır kalmamalıdır.
2. Her denetimden sonra `Denetimler`'e bir satır ekleyin (denetim no, tarih, mağaza, tür, tip, denetçi) ve takvimdeki gerçekleşen tarihi doldurun.
3. Denetimin her bulgusunu `Bulgular`'a girin: denetim no, madde kodu (listeden), açıklama.
4. Faaliyet gerektiren bulguları `DOF_Takip`'e girin; kapandığında kapanış tarihini yazın.
5. `Ayarlar` > **Bugünün tarihi** hücresini güncelleyin (ya da `=TODAY()` yazın).
6. Toplantı ve eğitim planlaması için `Dashboard`, `Oncelik_Listesi` ve `Madde_Magaza` sayfalarını kullanın.

## Kendi verinize uyarlama

| Nerede | Ne değiştirilir |
|---|---|
| `Madde_Listesi` | Kurumun denetim maddeleri, önem dereceleri ve eşleştirilen eğitim konuları |
| `Magazalar` | Mağazalar, yakınlık grupları, müdür uzmanlıkları |
| `Ayarlar` | Ceza katsayıları, toplam soru sayıları, hedef puanlar |

`Bulgular` sayfası yaklaşık 570 bulgu satırı için formül içerir; daha fazlası için son satırın formülleri aşağı kopyalanır. `Dashboard` ve `Madde_Magaza` 8 mağaza için kuruludur; mağaza eklenirse satır veya sütun kopyalanır.

## Sınırlar

- Rotasyon elle planlanır; sistem atamayı yapmaz, yalnızca kontrol eder.
- Denetim formunun kendisi burada yoktur; bulgular denetim sonrası girilir.
- ASA ve PAP'ın toplam soru sayıları örnek değerdir.

## Lisans

MIT. Ayrıntılar için `LICENSE` dosyasına bakın.
