# Funlet — Play Store & App Store Paket Rehberi

Bu klasör, Funlet'i Google Play Store ve Apple App Store'a göndermek için gereken
her şeyi içeriyor: oyunun kendisi, tüm ikon boyutları, mağaza ekran görüntüleri,
mağaza metinleri ve gizlilik politikası.

**Önemli ve dürüst bir not:** Gerçek, imzalı ve yüklenebilir bir `.aab` (Android)
veya `.ipa` (iOS) dosyasını bu ortamda benim için üretmek mümkün değil — bunun
için Android SDK / Xcode gibi araçlar ve (iOS için) mutlaka bir Mac + Apple
Developer hesabı gerekiyor; bunlara buradan erişimim yok. Ama bu klasördeki
her şey, aşağıdaki ücretsiz/kolay adımlarla o dosyaları **senin** üretmen için
tamamen hazır.

## Klasördeki Dosyalar
```
index.html          → Oyunun kendisi (PWA olarak yapılandırıldı)
manifest.json        → Uygulama adı, ikonlar, ekran görüntüleri tanımı
sw.js                 → Çevrimdışı çalışma desteği
icons/                → Android + iOS için gereken tüm ikon boyutları (25 adet)
screenshots/          → Mağaza listelemesi için hazır ekran görüntüleri
store-listing.md      → Kopyala-yapıştır mağaza açıklama metinleri (Türkçe)
privacy-policy.html   → Her iki mağazanın da zorunlu tuttuğu gizlilik politikası
```

---

## ADIM 1 — Dosyaları bir web adresine yükle (her iki mağaza için de gerekli)

Hem PWABuilder hem de Apple/Google, paketleme sırasında dosyalara bir URL üzerinden
erişmek ister. En kolay ücretsiz yöntem:

1. [GitHub](https://github.com)'da ücretsiz bir hesap aç (yoksa)
2. Yeni bir repo oluştur (örn. `funlet-oyunu`)
3. Bu klasördeki **tüm dosyaları** repoya yükle
4. Repo ayarlarından **GitHub Pages**'i aç (Settings → Pages → "Deploy from branch" → main)
5. Birkaç dakika sonra oyunun şu adreste yayında olacak:
   `https://kullanici-adin.github.io/funlet-oyunu/`
6. `privacy-policy.html` dosyasının linkini not al — her iki mağaza da bunu isteyecek:
   `https://kullanici-adin.github.io/funlet-oyunu/privacy-policy.html`

---

## ADIM 2A — Android (Play Store) için AAB üretme

1. [pwabuilder.com](https://www.pwabuilder.com) adresine git
2. ADIM 1'de aldığın linki yapıştır, "Start" de
3. PWABuilder sitenin manifest.json ve ikonlarını otomatik algılayacak (hepsi hazır)
4. "Android" sekmesine geç → **"Generate Package"**
5. İmzalı bir `.aab` (Android App Bundle) dosyası inecek — Play Store bunu doğrudan kabul eder
6. [Google Play Console](https://play.google.com/console)'da (tek seferlik 25$ geliştirici
   ücreti gerekir) yeni uygulama oluştur, `.aab` dosyasını yükle,
   `store-listing.md` içindeki metinleri ve `screenshots/` klasöründeki görselleri
   ilgili alanlara yapıştır, gizlilik politikası linkini ekle, gönder.

## ADIM 2B — iOS (App Store) için

Apple, App Store'a yüklenecek her uygulamanın **mutlaka bir Mac'te Xcode ile**
derlenip imzalanmasını şart koşar — bunun teknik bir istisnası yok, ben de dahil
hiçbir bulut/Linux ortamı bunu atlayamaz. Ayrıca yıllık 99$ Apple Developer
Program üyeliği gerekiyor. İki gerçekçi yolun var:

**A) Kendi Mac'in varsa:**
1. PWABuilder'da aynı linki kullanarak "iOS" sekmesinden bir Xcode proje paketi indir
2. Mac'te Xcode ile aç, kendi Apple Developer hesabınla imzala, App Store Connect'e gönder
3. `store-listing.md` ve `privacy-policy.html` aynı şekilde kullanılır

**B) Mac'in yoksa:**
Codemagic, Appcircle veya MacStadium gibi bulut tabanlı Mac derleme servisleri
(çoğunun ücretsiz deneme katmanı var) PWABuilder'ın ürettiği Xcode projesini
senin yerine derleyip imzalayabilir — Mac satın almana gerek kalmaz.

---

## Özet
- ✅ Oyun, ikonlar, ekran görüntüleri, mağaza metinleri, gizlilik politikası: **hazır**
- ⏳ Senin yapman gereken: dosyaları bir siteye yükle → PWABuilder'a linki ver →
  Android için AAB indir → Play Console'a yükle (Android ~15 dakika sürer)
- ⏳ iOS için ayrıca bir Mac (kendi/kiralık) ve Apple Developer üyeliği gerekiyor
