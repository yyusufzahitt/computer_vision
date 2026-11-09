# Kaynak ve Yapay Zekâ Beyanı — YZM411 Ödev 1

**Öğrenci:** Yusuf Zahit Altın · **No:** 230212031 · **Tarih:** 10 Kasım 2026

## 1. Veri

Üç fotoğrafı ben çektim (9 Kasım 2026, saat 23:13). Fotoğraflarda kişi tanınmıyor; gölge fotoğrafında yalnızca ayaklarım görünüyor.

| Dosya | Koşul | SHA-256 |
|---|---|---|
| `data/normal.jpg` | Normal ışık | `3119c1693d6859b7720e90c63e654523fafab3381d394ba3bbb40708dbd85778` |
| `data/golge.jpg` | Gölge (normal ışıkta kendi gövdemin gölgesi) | `d74a962fde4b9612c22a1f6668ac3d66df6500f8fc0a0595ce81e6210944d10c` |
| `data/lamba.jpg` | Sarı ışıklı lamba | `c5ea2bde2a859bba8aa67264c8e62cb31f0f5cd456fb41d46ddff133793eb89a` |

- Kamera: Samsung Galaxy A54, Pro mod; **beyaz dengesi "Auto"daydı**.
- Fotoğraflar WhatsApp ile aktarıldı. Bu yüzden EXIF bilgisi silindi ve çözünürlük 2040×1530'a düştü.
- Kamera üç çekimde elde tutuldu; konum ve açı değişti. Defterde homografi ile hizalama yapıldı ve bu durum raporda sınırlılık olarak yazıldı.

## 2. Kaynaklar

- YZM411 Bilgisayarlı Görü ders notları, Hafta 1–2 (görüntünün sayısal temsili, renk uzayları, örnekleme).
- OpenCV resmî belgeleri: `cvtColor`, `inRange`, `resize` (`INTER_NEAREST`, `INTER_AREA`, `INTER_CUBIC`), `SIFT_create`, `findHomography`, `findTransformECC`, `fitEllipse`.
- NumPy, pandas ve matplotlib resmî belgeleri.
- Başka bir kişinin verisi veya kodu kullanılmadı.

## 3. Yapay zekâ beyanı

**Araç:** Claude Code (Anthropic), model: Claude Opus 5.5.

| Tarih | Kullanım amacı | Etkilediği dosya / hücre | Nasıl doğrulandı |
|---|---|---|---|
| 08.11.2026 | Ödev PDF'inden adım planı çıkarma; klasör yapısı ve paket listesi | `requirements.txt` | Plan maddeleri ödevin 1–8. adımlarıyla tek tek eşleştirildi |
| 09.11.2026 | Fotoğraf çekim talimatı; çekimlerin kontrolü (EXIF, kadraj kayması) | — (fotoğrafları ben çektim) | Fotoğraflar görsel olarak ve ölçümle incelendi |
| 09.11.2026 | Defter iskeleti: kurulum, parametreler, veri tablosu, SIFT + ECC homografi hizalaması | `YZM411_Odev1.ipynb` Bölüm 0–2 | Defter baştan çalıştırıldı; hizalama dama tahtası görüntüsüyle gözle kontrol edildi |
| 09.11.2026 | Dört deneyin **tahmin taslakları** | Defterdeki 4 "Tahmin" hücresi | Taslakları okudum ve değiştirmeden onayladım; deney kodu yazılmadan **önce** deftere konuldu. 15 tahmin ve beklentiden 5'inin tutmaması, sonuca göre uydurulmadığını gösteriyor |
| 09–10.11.2026 | Deney 1–4 kodu, ek analiz (geniş eşik), kontrol deneyleri (renk düzeltmesi, örnekleme fazı), ölçüme dayalı yorum taslakları | Defter Bölüm 3–6, `outputs/03_*` – `06_*` | Defter `nbconvert` ile baştan sona birçok kez çalıştırıldı ve aynı sonuçları verdi; formüller ödevdeki örnekle doğrulandı (64 → 127,75 / 16,06); nokta konumları kırpıntılarla gözle kontrol edildi |
| 10.11.2026 | Sonuç ve karşılaştırma tabloları, rapor şekilleri | Defter Bölüm 7, `outputs/07_*`, `outputs/08_*` | Tablo değerleri defterdeki değişkenlerden otomatik okunuyor; önceki hücre çıktılarıyla karşılaştırıldı |
| 10.11.2026 | 2 sayfalık rapor taslağı, README ve bu beyan | `rapor/`, `README.md`, `KAYNAK_BEYANI.md` | Rapordaki her sayı `outputs/*.csv` ile karşılaştırıldı; sayfa sayısı programla kontrol edildi |

**Kendi yaptıklarım:**
- Sahneyi kurup üç fotoğrafı çektim.
- Çekim koşullarını (Pro mod, beyaz dengesi Auto, gölge ve lamba) bildirdim.
- Tahmin taslaklarını okuyup onayladım.
- Sonuçları ve raporu okuyup kontrol ettim.

**Genel doğrulama:** Rapordaki bütün sayılar, defterin çalıştırılmasıyla üretilen `outputs/` dosyalarından alındı. Hiçbir ölçüm elle yazılmadı.
