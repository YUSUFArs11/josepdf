# Tarih PDF — Rapor Tarihi Düzenleyici

Bu küçük web uygulaması, aynı şablona sahip rapor PDF'lerindeki iki bölgeyi değiştirir:

1. Tablo satırlarındaki `GG.AA.YYYY` tarihi
2. Sağ üstteki `GG.AA.YYYY HH:MM:SS` tarih-saat alanı

Uygulama yalnızca tarayıcıda çalışır. PDF dosyasının kendisi bir sunucuya yüklenmez. PDF.js dosyayı okumak/görüntülemek, pdf-lib ise çıktı PDF'sini üretmek için CDN üzerinden yüklenir. Bu nedenle siteyi açarken internet bağlantısı gerekir; PDF içeriği ise tarayıcıda kalır.

## Yerelde çalıştırma

PDF.js worker'ı nedeniyle dosyayı doğrudan `file://` ile açmak yerine küçük bir yerel web sunucusu kullan:

```bash
python -m http.server 8000
```

Ardından tarayıcıda `http://localhost:8000` adresini aç. Komutu `index.html` dosyasının bulunduğu klasörde çalıştır.

## Ücretsiz GitHub Pages yayını

1. GitHub'da yeni ve **public** bir repository oluştur.
2. Bu klasördeki `index.html`, `.nojekyll` ve `README.md` dosyalarını repository'nin kök dizinine yükle.
3. Repository içinde **Settings → Pages** bölümünü aç.
4. **Build and deployment** altında **Deploy from a branch** seç.
5. Branch olarak `main`, klasör olarak `/(root)` seçip **Save**'e bas.
6. GitHub'ın gösterdiği `https://KULLANICI.github.io/REPOSITORY/` benzeri adresi aç.

GitHub Free için Pages kaynağı public repository olmalıdır. PDF raporlarını repository'ye yükleme; yalnızca web uygulamasının kaynak kodunu yükle.

## Tasarım ve sınırlar

- İşlem şablon odaklıdır; PDF'nin A4 portre sayfa düzeninde olması beklenir.
- Tablo tarihleri metin katmanından bulunur. Sağ üst tarih-saat bu şablonda görüntünün içinde olduğundan sabit alanda yenilenir.
- Çıktı, orijinal görünümü mümkün olduğunca korumak için görüntü tabanlı PDF olarak hazırlanır. Masaüstünde 300 DPI, dar ekranlarda (genellikle telefonlarda) bellek kullanımını azaltmak için 240 DPI kullanılır. Bu nedenle çıktı metnini seçme/arama özelliği korunmayabilir.
- Kaynak PDF değiştirilmez. Yeni bir çıktı dosyası oluşturulur.
- Yetkili olduğun raporlardaki tarih düzeltmeleri için kullan.

## Dosyalar

- `index.html` — arayüz ve tarayıcıda PDF işleme kodu
- `.nojekyll` — GitHub Pages'in kaynak dosyaları değiştirmeden yayınlamasını sağlar

## Telefonda kullanma

- GitHub Pages adresini telefonunun Chrome, Safari veya başka modern tarayıcısında aç.
- “PDF seç” ile Dosyalar/İndirilenler uygulamasından PDF'yi seç.
- İki tarihi gir, “PDF'yi oluştur” düğmesine dokun ve önizlemeyi kontrol et.
- “Düzenlenmiş PDF'yi indir” düğmesine dokun. İndirme konumu telefonun tarayıcısına göre değişebilir.
- Daha kolay açmak için tarayıcının menüsünden “Ana ekrana ekle” veya “Ana ekrana ekle / Add to Home Screen” seçeneğini kullanabilirsin.

GitHub Pages'te ücretsiz yayınlamak için depo genellikle public olmalıdır. Bu, uygulama kodunun ve site adresinin herkese açık olacağı anlamına gelir; ancak uygulama PDF içeriğini sunucuya yüklemez ve deponun içine rapor dosyaları koyulmamalıdır.
