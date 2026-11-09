# Köybaşı Hukuk ve Danışmanlık — Web Sitesi

Av. Şule Köybaşı Göçmen'in hukuk bürosu için hazırlanmış, statik ve çok sayfalı kurumsal web sitesi.

- Yalnızca **HTML5, CSS3 ve Vanilla JavaScript** kullanır.
- Framework, Node.js, npm veya derleme adımı **yoktur**.
- `index.html` dosyasına çift tıklayarak doğrudan tarayıcıda açılır; yerel sunucu gerekmez.

## Dosya yapısı

```
.
├── index.html              Ana sayfa
├── hakkimizda.html         Büro ve kurucu avukat
├── calisma-alanlari.html   Çalışma alanları (içindekiler menülü)
├── iletisim.html           İletişim bilgileri, görüşme formu, KVKK bölümü
├── css/
│   └── style.css           Tüm stiller
├── js/
│   └── script.js           Hamburger menü, form doğrulama, küçük etkileşimler
├── images/
│   ├── favicon.svg         Tarayıcı sekme simgesi
│   └── logo.svg            Logo (paylaşım, belge vb. için)
├── README.md
└── .gitignore
```

## Siteyi Chrome'da açma

1. Proje klasörünü açın.
2. `index.html` dosyasına çift tıklayın (veya sağ tık → **Birlikte aç** → **Google Chrome**).
3. Menüdeki bağlantılar diğer `.html` sayfalarına gider; hepsi aynı klasörden çalışır.

> Yazı tipleri (Cormorant Garamond ve Inter) Google Fonts üzerinden yüklenir. İnternet bağlantısı yoksa site, Georgia ve sistem yazı tipleriyle düzgün biçimde görüntülenmeye devam eder.

## Yayına almadan önce doldurulacak alanlar

Sitede uydurma bilgi yoktur; gerçek bilgiler aşağıdaki yer tutucularla işaretlenmiştir. Tüm dosyalarda arayıp değiştirin:

| Yer tutucu | Bulunduğu yer |
| --- | --- |
| `[ADRES]` | Tüm sayfaların alt bilgisi, `iletisim.html` |
| `[TELEFON]` | Alt bilgi, `iletisim.html` (`tel:` bağlantılarında boşluksuz yazın, örn. `tel:+90...`) |
| `[E-POSTA]` | Alt bilgi, `iletisim.html` (`mailto:` bağlantıları ve formdaki `data-recipient`) |
| `[ÇALIŞMA SAATLERİ]` | `iletisim.html` |
| `[HARİTA]` | `iletisim.html` — Google Haritalar "Yerleştir" iframe kodu ile değiştirilebilir |
| `[FOTOĞRAF]` | `hakkimizda.html` — açıklamaya bakın |
| `[BİYOGRAFİ ...]`, `[BARO]`, `[SİCİL NO]`, `[EĞİTİM BİLGİSİ]`, `[YABANCI DİL]` | `hakkimizda.html` |
| `[KVKK AYDINLATMA METNİ ...]` | `iletisim.html` (`#kvkk` bölümü) |

### Fotoğraf eklemek

1. Fotoğrafı `images/` klasörüne koyun (örn. `images/sule-koybasi-gocmen.jpg`, dikey 4:5 oran önerilir).
2. `hakkimizda.html` içindeki `<div class="portrait-placeholder">…</div>` bloğunu şununla değiştirin:

```html
<img src="images/sule-koybasi-gocmen.jpg" alt="Av. Şule Köybaşı Göçmen">
```

### İletişim formu

Statik sitede sunucu olmadığı için form, doğrulama sonrası ziyaretçinin **e-posta uygulamasını** hazır bir mesajla açar (`mailto:`). Alıcı adresi `iletisim.html` içindeki şu özellikten okunur:

```html
<form id="contact-form" data-recipient="[E-POSTA]" novalidate>
```

`[E-POSTA]` yerine gerçek adres yazılmadıkça form gönderim yapmaz ve bunu ekranda belirtir. İleride Formspree, Netlify Forms vb. bir form servisi kullanılmak istenirse `js/script.js` içindeki `initContactForm` fonksiyonu uyarlanabilir.

## GitHub'a yükleme ve GitHub Pages ile yayınlama

1. GitHub'da yeni bir depo oluşturun (örn. `koybasi-hukuk`). Ücretsiz hesapta Pages için deponun **Public** olması gerekir.
2. Site dosyalarını depoya yükleyin:
   - **Tarayıcıdan:** Depo sayfasında **Add file → Upload files**; yukarıdaki dosya ve klasörlerin tamamını sürükleyip bırakın, **Commit changes** deyin.
   - **Git ile:** proje klasöründe

     ```bash
     git init
     git add index.html hakkimizda.html calisma-alanlari.html iletisim.html css js images README.md .gitignore
     git commit -m "İlk sürüm"
     git branch -M main
     git remote add origin https://github.com/KULLANICI_ADI/koybasi-hukuk.git
     git push -u origin main
     ```
3. Depoda **Settings → Pages** bölümüne gidin.
4. **Build and deployment → Source** olarak **Deploy from a branch** seçin.
5. **Branch** olarak `main`, klasör olarak `/ (root)` seçip **Save** deyin.
6. Birkaç dakika içinde site `https://KULLANICI_ADI.github.io/koybasi-hukuk/` adresinde yayına girer. Adres aynı sayfada görünür.

**Kendi alan adı (isteğe bağlı):** Settings → Pages → **Custom domain** alanına alan adını yazın; alan adı sağlayıcınızda GitHub'ın belirttiği DNS kayıtlarını (CNAME / A) tanımlayın ve **Enforce HTTPS** seçeneğini açın.

## Tasarım notları

- Renkler: lacivert (`#16233d`), kırık beyaz (`#f7f4ee`), taş (`#d8d0c2`), bronz (`#9a7b4f`). Tümü `css/style.css` başındaki `:root` değişkenlerinden değiştirilebilir.
- Başlıklar serif (Cormorant Garamond), metinler sans-serif (Inter).
- Hareket ölçülüdür; işletim sisteminde "hareketi azalt" açıksa efektler kapanır.
- Mobilde hamburger menü: `Esc` ile kapanır, menü açıkken klavye odağı menü içinde kalır.

## Mesleki uyarı

Avukatlık Kanunu ve Türkiye Barolar Birliği **Reklam Yasağı Yönetmeliği**, avukatların internet sitelerinde yer alabilecek içerikleri sınırlar (örn. üstünlük iddiası, başarı vaadi, müvekkil adı/yorumu, ücret bilgisi yasaktır). Site metinleri bu çerçevede bilgilendirici ve ölçülü tutulmuştur; yayına almadan önce içerikleri bu kurallar açısından gözden geçirmeniz önerilir.
