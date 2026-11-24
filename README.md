# İç Denetim Standardizasyonu ve Bulgulardan Eğitim Programı

**Türkçe** | [English](README.en.md)

Çok mağazalı bir bölgede mağaza müdürlerinin yürüttüğü çapraz iç denetimleri ve esas denetimleri **tek ortak yapıda** toplayan, otomatik puanlayan, düzeltici-önleyici faaliyetleri (DÖF) izleyen ve **en sık tekrar eden uygunsuzluklardan bölge eğitim önceliği** çıkaran Excel sistemi.

> **Gizlilik ve Sentetik Veri Notu:** Bu çalışma kitabı, 16 mağazalık bölge operasyonunda kurduğum ve yürüttüğüm iç denetim ve DÖF takip sisteminin **tamamen sentetik (kurgu) veriyle** yeniden oluşturulmuş sürümüdür. Kurumsal gizlilik gereği marka, mağaza adı, kurum içi denetim formları ve gerçek denetim kayıtları yer almaz; tüm mağazalar (`Mağaza A`–`Mağaza H`), kontrol maddeleri, tarihler ve bulgular örnekleme amacıyla üretilmiştir.

## Hangi problemi çözüyor

Bölgede üç ayrı denetim disiplini yürütülür: genel operasyon (`ASA`), kayıp önleme ve çalışan güvencesi (`PAP`) ile gıda güvenliği (`RSA`). Bu sistem kurulmadan önce sonuçlar tekil PDF raporlarında kalıyor; mağazalar arası karşılaştırma, tekrar eden kök bulguların tespiti ve iç denetim puanıyla esas denetim puanı arasındaki sapma analizi yapılamıyordu.

Bu sistemde:

- **Karşılıklı iç denetim rotasyonu** çeyreklik planlanır; yakın mağaza müdürleri uzmanlık alanlarına göre birbirini denetler ve takvim hatalı atamaları (kendi mağazası veya uzmanlık dışı atama) otomatik uyarır.
- **Tahmini esas denetim tarihleri** aynı takvimde izlenir, yaklaşan denetimler için uyarı üretilir.
- Her denetim ve bulgu **standart yapıda** kaydedilir; ceza katsayılarına göre puan otomatik hesaplanır.
- **Dashboard** her mağazanın iç ve esas denetim puanını yan yana göstererek iç denetimin sahadaki gerçek durumu ne ölçüde yakaladığını ölçer.
- **Öncelik listesi** en sık tekrar eden uygunsuzlukları önem derecesiyle ağırlıklandırarak sıralar; her maddeyi ilgili eğitim başlığıyla eşleştirip bölge eğitim programına doğrudan girdi üretir.

## Öncesi

İç denetim kayıtları ortak bir veri yapısında tutulmuyordu; esas denetim sonuçları PDF dosyalarından tek tek okunarak takip ediliyordu.

## Sayfalar

| Sayfa | Ne yapar |
|---|---|
| `Nasil_Kullanilir` | Çalışma akışı, puanlama kuralları ve kısaltmalar |
| `Dashboard` | Mağaza × denetim türü: iç puan, esas puan, fark, sıra, toplam/kritik bulgu, açık/gecikmiş DÖF sayıları, takvim özeti ve grafik |
| `Oncelik_Listesi` | En sık tekrar eden 15 uygunsuzluk (tümü veya seçili denetim türü), eğitim konusu bazında dağılım ve grafik |
| `Madde_Magaza` | Denetim maddesi × mağaza tekrar ısı haritası |
| `Denetim_Takvimi` | Çeyreklik çapraz iç denetim rotasyonu, atama kontrolü ve tahmini esas denetim takvimi |
| `Denetimler` | Denetim kayıtları: tarih, mağaza, tür, iç/esas tipi, denetçi, bulgu sayıları ve otomatik puan |
| `Bulgular` | Uygunsuzluk satırları: denetim no ve madde kodu girildiğinde kategori, önem derecesi ve eğitim konusu otomatik gelir |
| `DOF_Takip` | Bulguya bağlı aksiyon, sorumlu, termin, kapanış tarihi, durum ve gecikme günü |
| `Madde_Listesi` | Denetim kontrol maddeleri, önem dereceleri ve eşleştirilen eğitim konuları |
| `Magazalar` | Mağaza listesi, yakınlık kümesi ve müdür denetim uzmanlığı |
| `Ayarlar` | Referans tarih, önem katsayıları, toplam soru sayıları ve hedef puanlar |

## Hesaplar

- **Ceza puanı** = kritik bulgu × 2 + major bulgu × 1,5 + minör bulgu × 1
- **Denetim puanı** = `(toplam soru − ceza puanı) ÷ toplam soru × 100`
- **Hedef puanlar**: ASA 90 · PAP 85 · RSA 90
- **İç − esas farkı**: yüksek pozitif fark, iç denetimin esas denetimde çıkan eksikleri yeterince yakalayamadığını gösterir
- **Ağırlıklı öncelik skoru** = maddenin tekrar sayısı × önem katsayısı
- **DÖF durumu**: *Kapandı*, *Geç kapandı*, *Gecikmiş* veya *Açık*

## Kullanım

Makro içermez; `ic-denetim-sistemi.xlsx` Excel 2010+ ve LibreOffice'te doğrudan açılır.

1. Çeyrek başında `Denetim_Takvimi` sayfasında rotasyonu planlayın (rotasyon kontrol sütununda uyarı kalmamalıdır).
2. Tamamlanan denetimleri `Denetimler` sayfasına, tespit edilen uygunsuzlukları `Bulgular` sayfasına, aksiyon gerektiren maddeleri `DOF_Takip` sayfasına işleyin.
3. Aylık ve çeyreklik değerlendirmelerde `Dashboard`, `Oncelik_Listesi` ve `Madde_Magaza` sayfalarını kullanın.

## Lisans

MIT. Ayrıntılar için `LICENSE` dosyasına bakın.
