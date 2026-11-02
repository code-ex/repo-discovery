---
name: repo-discovery
description: >-
  Proje geliştirme süreçlerinde 'Tembel Bağlam Arama' ve sıfırdan gereksiz kod üretme (tekerleği yeniden icat etme) eğilimini önlemek için SYSTEM_MAP.md ve kod tabanı üzerinde keşif yapar; mevcut modül ve yardımcıları tespit ederek entegrasyon planı çıkarır ve yeni ortak bileşenler eklendiğinde SYSTEM_MAP.md haritasını günceller. Kullanıcı mimari haritayı sorguladığında, 'bunun benzeri var mı', 'mevcut yapıyı incele', 'SYSTEM_MAP oluştur/güncelle' dediğinde bu skilli kullanın.
---

# Repo Discovery & System Map Management

Geliştiricilerin ve yapay zeka asistanlarının bir projede halihazırda var olan yardımcı sınıfları, servis katmanlarını, tasarım desenlerini veya ortak araçları gözden kaçırmasını engelleyen; kod yazmadan önce projeyi tarayarak mevcut altyapıyı tespit eden ve yaşayan mimari haritayı (`SYSTEM_MAP.md`) güncel tutan iş akışıdır.

---

## Ne Zaman Kullanılır (When to Use)

1. **Geliştirme Öncesi Keşif (Pre-Flight Discovery):**
   - Yeni bir özellik veya servis yazılmadan önce projenin mevcut araç setini (`SYSTEM_MAP.md` veya ilgili dizinler) inceleyip benzer bir fonksiyonun varlığını tespit etmek için.
2. **Mimari Harita Oluşturma ve Başlatma:**
   - Projede henüz bir `SYSTEM_MAP.md` yoksa ve kullanıcı bir mimari indeks/harita oluşturulmasını istediğinde.
3. **Mimari Senkronizasyon (Map Sync):**
   - Yeni bir modül, ortak helper, repository sınıfı veya middleware eklendiğinde `SYSTEM_MAP.md` tablosunu güncellemek için.
4. **Kullanıcı Sorgusu:**
   - Kullanıcı "Bu projede X işi nerede yapılıyor?", "Bunun benzeri bir yardımcı sınıf var mı?", "Mevcut mimari haritayı güncelle" dediğinde.

---

## Adım Adım İş Akışı (Workflow Steps)

### Adım 1: Harita ve Kod Taraması (Discovery)
1. Çalışma alanı kökünde `SYSTEM_MAP.md` var mı kontrol et.
   - **Varsa:** Tabloyu oku ve aranan yeteneğin (örn. HTTP retry, DateFormatter, ExceptionHandler, Normalizer) mevcut modülünü bul.
   - **Yoksa:** Kod tabanında ilgili klasörlerde (`utils/`, `core/`, `common/`, `pipeline/`, `services/`) dosya ve sembol araması yap.
2. Benzer bir sınıf veya fonksiyon bulunduysa:
   - Bu modülün import yolunu ve kullanım kuralını not et.

### Adım 2: Pre-Flight Beyanı (Integration Statement)
Kullanıcıya veya çalışma planına açık bir şekilde beyanda bulun:
> 🔎 **Pre-Flight Keşif Özeti:**  
> *Projede bu işlevle ilgili mevcut `[Modül/Sınıf/Fonksiyon Adı]` (`dosya/yolu.py`) yapısını tespit ettim. Yeni özelliği sıfırdan generic yazmak yerine bu mevcut altyapıyı kullanarak entegre edeceğim.*

### Adım 3: Haritanın Güncellenmesi (Senkronizasyon)
Eğer yapılan geliştirmede projeye yeni bir ortak bileşen, temel model veya servis katmanı kazandırıldıysa:
1. `SYSTEM_MAP.md` dosyasındaki **Yetenek ve Yardımcı Modül Haritası** tablosuna yeni satır ekle:
   - Yetenek / Sorumluluk Alanı
   - Mevcut Modül / Sınıf
   - Dosya Konumu (tıklanabilir `file:///...` bağlantısıyla)
   - Dikkat Edilmesi Gereken Kural / Standart
2. Dosyayı kaydet ve kullanıcıya haritanın güncellendiğini bildir.

---

## Şablon: SYSTEM_MAP.md Formatı

Yeni bir projede `SYSTEM_MAP.md` oluşturulurken şu asgari yapı kullanılmalıdır:

```markdown
# 🗺️ [Proje Adı] Mimari & Yetenek Haritası (System Map)

> [!IMPORTANT]
> **AI Asistan Talimatı (Pre-Flight Check):** Yeni bir sınıf, fonksiyon, yardımcı modül (utility) veya endpoint eklemeden önce bu haritayı incele. Benzer bir mantık projede zaten varsa sıfırdan yazma; mevcut altyapıyı genişleterek veya entegre ederek kullan.

## 🏛️ 1. Mimari Katmanlar ve Çekirdek Akış
[Kısa Mermaid akış şeması]

## 🧭 2. Yetenek ve Yardımcı Modül Haritası
| Yetenek / Sorumluluk Alanı | Mevcut Modül / Sınıf | Dosya Konumu | Dikkat Edilmesi Gereken Kural / Standart |
| :--- | :--- | :--- | :--- |
| [Örn: Loglama] | Logger | [logger.py](file:///...) | Standart format |

## 🚫 3. Yasaklı / Kaçınılması Gereken Yaklaşımlar (Do-Not-Reinvent)
- [Örn: Doğrudan harici client açma, mevcut X sınıfını kullan]
```
