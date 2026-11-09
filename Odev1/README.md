# YZM411 Bilgisayarlı Görü — Ödev 1: Renk, Aydınlatma ve Örnekleme

**Yusuf Zahit Altın · 230212031**

Kendi kurduğum bir masa sahnesinde iki olguyu ölçtüm:
- aynı nesnenin farklı ışıkta neden farklı piksel değerleri ürettiği,
- küçültmenin hangi bilgiyi kalıcı olarak kaybettirdiği.

Her deneyden önce sonucu tahmin ettim, sonra ölçtüm ve tahminimi ölçümle karşılaştırdım.

- **Rapor (PDF, 2 sayfa):** [`rapor/YZM411_Odev1_Rapor.pdf`](rapor/YZM411_Odev1_Rapor.pdf)
- **Defter:** [`YZM411_Odev1.ipynb`](YZM411_Odev1.ipynb)
- **Sonuç tablosu:** [`outputs/07_sonuc_tablosu.csv`](outputs/07_sonuc_tablosu.csv) (tahmin, ölçüm, karar ölçütü, kaynak dosya)
- **Kaynak ve yapay zekâ beyanı:** [`KAYNAK_BEYANI.md`](KAYNAK_BEYANI.md)

## Çalıştırma

Python 3.11.9 ile test edildi.

```bash
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute --inplace YZM411_Odev1.ipynb
```

Ya da Jupyter'de defteri açıp **Kernel → Restart & Run All** seçilir. Hücreler yukarıdan aşağıya sırayla çalışır. Tamamı birkaç dakika sürer.

- **Giriş dosyaları:** `data/normal.jpg`, `data/golge.jpg`, `data/lamba.jpg`. Kendi çekimim; defter bu dosyaları değiştirmez.
- **Parametreler:** Hepsi defterin 0.1 numaralı hücresinde (eşik bölgesi ve payları, b = +40, γ = 0,5 / 2,0, küçültme 1/4 vb.).
- **Paket sürümleri:** Defterin ilk kod hücresi yazdırır.
- **Çıktılar:** Bütün şekiller ve tablolar `outputs/` klasörüne yazılır.

## Klasör yapısı

```
YZM411_Odev1.ipynb   # tüm deneyler: tahmin → kod → ölçüm → yorum
data/                # 3 özgün fotoğraf (normal, gölge, lamba)
outputs/             # defterin ürettiği CSV/JSON tablolar ve PNG şekiller
rapor/               # 2 sayfalık PDF rapor ve HTML kaynağı
requirements.txt
KAYNAK_BEYANI.md
```

## Defterin bölümleri

| Bölüm | İçerik |
|---|---|
| 0–1 | Paket sürümleri, parametreler, giriş dosyaları (SHA-256), çekim koşulları |
| 2 | Kamera sabit olmadığı için masa düzlemi üzerinden homografi (SIFT + RANSAC, ECC ince ayarı) |
| 3 | **H1:** boyut, veri türü, değer aralığı, `img[y, x, kanal]`, BGR → RGB, 3 nokta × 3 fotoğraf |
| 4 | **H2:** normal fotoğrafta dondurulan RGB/HSV eşikleri, 6 maske ve alan oranları, geniş eşik ek analizi, renk düzeltmesi kontrolü |
| 5 | **H3:** parlaklık kaydırması (b = +40) ve gama (γ = 0,5 / 2,0), ortalama ve 255'te kırpma |
| 6 | **H4:** 1/4 küçültme (`INTER_NEAREST` / `INTER_AREA`), yan yana kesit, geri döndürülemezlik kanıtı, örnekleme fazı kontrolü |
| 7 | Sonuç tablosu, karşılaştırma tablosu, rapor şekilleri |

## Kısa sonuç

- Normal ışıkta dondurulan eşikler gölge ve lamba fotoğraflarında **hiç piksel seçmedi**; hem RGB'de hem HSV'de %0.
  - Kupanın tonu 29'dan 20–21'e kaydı, doygunluğu 193'ten yaklaşık 130'a düştü.
  - Beyaz dengesi Auto'daydı; bu nedenle "yalnızca ışık değişti" iddiasında bulunmuyorum.
- Kupayı her ışıkta yakalayacak kadar geniş bir eşik, normal fotoğrafta ahşap masayı ve hardal yastığı da seçti (%19,22).
- b = +40 sonrası ortalama 136,85 yerine 135,69 çıktı. Aradaki farkın tamamı 255'te kırpmadan geliyor.
- 1/4 küçültmede yazı okunamaz hâle geldi.
  - Yazılı özgün görüntü ile yazısı silinmiş görüntülerin küçültülmüş hâlleri **piksel piksel aynı** çıktı. Bu yüzden büyütme yazıyı geri getiremez.
- 15 tahmin ve beklentiden 10'u tuttu, 5'i tutmadı.
