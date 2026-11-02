# Repo Discovery & System Map Protocol - Antigravity Skill

[![Antigravity Skill](https://img.shields.io/badge/Antigravity-Skill-blue.svg)](https://github.com/code-ex/repo-discovery)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Yapay zeka asistanlarının (Google Antigravity vb.) kod tabanında halihazırda var olan yardımcı sınıfları, servis katmanlarını veya mimari desenleri gözden kaçırıp **"Tembel Bağlam Arama" (Lazy Context Retrieval)** veya **"Üretim Önyargısı" (Generation Bias)** ile tekerleği sıfırdan icat etmesini önleyen **Antigravity Agent Skill**'idir.

---

## 🎯 Çözülen Temel Problem

Yapay zeka asistanları kod yazarken genellikle var olan kodu arayıp anlamaktansa sıfırdan bildikleri generic bir yöntemi üretmeyi daha "ucuz" ve kolay bulurlar:
- Kod tabanında özel bir `DateHelper` veya `ResilientHttpClient` varken standart kütüphane açarlar.
- Zaten tanımlı bir normalizasyon veya hata sınıfı varken generic regex / exception yazarlar.
- Kullanıcı *"Biz zaten bunu yapmıştık"* dediğinde *"Aa evet"* diyerek sonradan çark ederler.

**`repo-discovery`**, bu döngüyü kırmak için yapay zekayı kod yazmadan önce bir **Pre-Flight Check (Geliştirme Öncesi Denetim)** protokolü uygulamaya zorlar.

---

## 🚀 Temel Yetenekler

1. **Yaşayan Mimari Haritası (`SYSTEM_MAP.md`):**
   - Projenin kök dizininde yer alan, kod içermeyen; sadece modül, ortak yardımcı sınıf, veri sözleşmesi ve kuralları indeksleyen çok özet ve hafif bir harita tutar.
2. **Pre-Flight Keşif Beyanı (Integration Statement):**
   - Yapay zeka kod yazmaya başlamadan önce sohbette şu beyanda bulunmakla yükümlüdür:
     > 🔎 **Pre-Flight Keşif Özeti:**  
     > *Projede bu işlevle ilgili mevcut `[Modül/Sınıf]` yapısını tespit ettim. Yeni özelliği sıfırdan generic yazmak yerine bu altyapıyı kullanarak entegre edeceğim.*
3. **Sıfırdan Yazma Yasağı (Anti-Reinvention):**
   - Projede mevcut bir karşılık varsa asla bağımsız generic çözümler üretilmez; var olan yapı import edilir veya genişletilir.
4. **Çift Yönlü Harita Senkronizasyonu:**
   - Projeye yeni bir ortak yetenek veya yardımcı modül eklendiğinde `SYSTEM_MAP.md` tablosu otomatik güncellenir.
5. **Esnek Denetim:**
   - Projede `SYSTEM_MAP.md` yoksa kullanıcı bloklanmaz veya *"Neden harita yok?"* diye sorgulanmaz; mevcut dosyalarda hızlı arama yapılarak yola devam edilir.

---

## 📁 Dizin Yapısı

```text
repo-discovery/
├── SKILL.md                          # Ana skill talimatları ve iş akışı
├── README.md                         # Tanıtım ve kullanım rehberi
├── LICENSE                           # MIT Lisansı
└── resources/
    ├── SYSTEM_MAP_TEMPLATE.md        # Yaşayan mimari harita şablonu
    └── PRE_FLIGHT_RULE_SNIPPET.md    # AGENTS.md / kurallara eklenecek kural parçacığı
```

---

## 💻 Kurulum

### Yöntem 1: Global Kurulum (Tüm Projeler İçin - Önerilen)

Tüm Antigravity projelerinizde aktif olması için global yetenek dizinine klonlayın:

```bash
# Windows (PowerShell)
git clone https://github.com/code-ex/repo-discovery.git "$env:USERPROFILE\.gemini\config\skills\repo-discovery"

# Linux / macOS
git clone https://github.com/code-ex/repo-discovery.git ~/.gemini/config/skills/repo-discovery
```

### Yöntem 2: Çalışma Alanı (Workspace) Kurulumu

Yalnızca tek bir repoda geçerli olmasını isterseniz:

```bash
mkdir -p .agents/skills
git clone https://github.com/code-ex/repo-discovery.git .agents/skills/repo-discovery
```

---

## ⚙️ Kural Entegrasyonu (Pre-Flight Rule)

Yapay zekanın bu keşfi kod yazmadan önce zorunlu olarak yapması için projenizin `AGENTS.md` veya `GEMINI.md` dosyasına şu kuralı ekleyin (bkz: `resources/PRE_FLIGHT_RULE_SNIPPET.md`):

```markdown
## 🧭 Geliştirme Öncesi Denetim Protokolü (Pre-Flight Check & Anti-Reinvention)

1. **Harita Kontrolü:** Projede yeni bir özellik veya modül geliştirmeden önce kök dizinde `SYSTEM_MAP.md` var mı kontrol et. Varsa incele; yoksa neden yok diye sorma, ilgili dizinlerde hızlı arama yap.
2. **Mevcut Yapı Beyanı (Zorunlu):** Kod yazmaya başlamadan önce kullanıcıya tek paragrafta: *"Projede bu işlevle ilgili mevcut [Modül/Sınıf] yapısını tespit ettim. Yeni özelliği sıfırdan generic yazmak yerine bu altyapıyı kullanarak entegre edeceğim"* şeklinde açık beyanda bulun.
3. **Mevcut Modülü Kullanma Zorunluluğu:** Sistemde zaten var olan bir yetenek yerine asla generic alternatifler yazma; mevcut yapıyı genişlet.
4. **Harita Güncelleme:** Projeye yeni bir ortak yetenek eklendiğinde `SYSTEM_MAP.md` dosyasını senkronize güncelle.
```

---

## 📄 Lisans

Bu proje [MIT Lisansı](LICENSE) kapsamında lisanslanmıştır.
