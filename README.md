<p align="center">
  <img src="macos/Resources/icon.png" width="128" alt="Claude Usage Bar icon">
</p>

# Claude Usage Bar

Claude kullanım limitine ne kadar yaklaştığını görmek için sayfayı yenilemeye son. Menu bar'dan bir bakışta öğren.

<p align="center">
  <img src="macos/Resources/demo.png" width="400" alt="Claude Usage Bar demo">
</p>

![macOS 14+](https://img.shields.io/badge/macOS-14%2B-blue)
![Swift 5.9](https://img.shields.io/badge/Swift-5.9-orange)

## Özellikler

- Menu bar'da 5 saatlik ve 7 günlük kullanımı gösteren mini çift çubuk
- Pencere bazlı kullanım, model dağılımı ve sıfırlanma zamanlayıcısı
- USD cinsinden ekstra kullanım takibi
- Kullanım geçmişi grafiği (1s / 6s / 1g / 7g / 30g)
- Grafik üzerinde hover ile anlık değerler
- Otomatik güncelleme — varsayılan olarak her **5 dakikada** bir
- Tarayıcı üzerinden OAuth ile giriş, API anahtarı gerekmez

## Kurulum

### Kaynaktan derleme

Xcode 15+ / Swift 5.9+ ve macOS 14 (Sonoma) veya üstü gereklidir.

```sh
git clone https://github.com/cannecee/Claude-Usage-for-Mac.git
cd Claude-Usage-for-Mac
make app            # .app bundle oluştur
make install        # /Applications klasörüne kur
```

## Kullanım

1. Uygulamayı başlat — menu bar'da ikon belirir
2. İkona tıkla → **Sign in with Claude** → tarayıcıda izin ver
3. Kodu uygulamaya yapıştır
4. İkon her 5 dakikada bir otomatik olarak güncellenir

İkona tıklayarak şunları görebilirsin:
- 5 saatlik ve 7 günlük kullanım ilerleme çubukları ve sıfırlanma süreleri
- Mevcut olduğunda model bazlı dağılım (Opus / Sonnet)
- Ekstra kullanım kredisi ve limitleri
- Ayarlanabilir zaman aralıklı kullanım geçmişi grafiği

## Veri depolama

Tüm veriler yerel olarak `~/.config/claude-usage-bar/` dizininde saklanır:

| Dosya | Amaç |
|-------|------|
| `token` | OAuth erişim token'ı (`0600` izni) |
| `history.json` | Grafik için kullanım geçmişi (30 günlük) |

Anthropic API dışında hiçbir yere veri gönderilmez.

## Proje yapısı

```
macos/
├── Sources/ClaudeUsageBar/
│   ├── ClaudeUsageBarApp.swift          # Uygulama giriş noktası
│   ├── UsageService.swift               # OAuth, polling, API çağrıları
│   ├── UsageModel.swift                 # API yanıt tipleri
│   ├── UsageHistoryModel.swift          # Geçmiş veri tipleri
│   ├── UsageHistoryService.swift        # Kalıcı depolama
│   ├── UsageChartView.swift             # Grafik görünümü
│   ├── PopoverView.swift                # Ana popover UI
│   ├── SettingsView.swift               # Ayarlar penceresi
│   ├── NotificationService.swift        # Kullanım eşik bildirimleri
│   └── MenuBarIconRenderer.swift        # Menu bar ikon çizimi
└── Package.swift
```

---

Bu proje [Blimp-Labs/claude-usage-bar](https://github.com/Blimp-Labs/claude-usage-bar) üzerinden fork edilmiştir.
