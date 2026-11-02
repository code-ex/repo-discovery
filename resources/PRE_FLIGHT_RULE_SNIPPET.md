# 🧭 Pre-Flight Check Rule Template

Add the following block to your project's `AGENTS.md`, `GEMINI.md`, or global agent rules (`~/.gemini/config/rules/pre-flight-check.md`) to enforce anti-reinvention discovery before any code modification:

```markdown
## 🛫 Geliştirme Öncesi Denetim Protokolü (Pre-Flight Check & Anti-Reinvention)

1. **Harita Kontrolü:** Projede yeni bir özellik, modül veya yardımcı araç geliştirmeden önce kök dizinde `SYSTEM_MAP.md` var mı kontrol et. Varsa incele; yoksa neden yok diye sorma, ilgili dizinlerde hızlı arama yap.
2. **Mevcut Yapı Beyanı (Zorunlu):** Kod yazmaya başlamadan önce kullanıcıya tek paragrafta:
   > 🔎 **Pre-Flight Keşif Özeti:**  
   > *Projede bu işlevle ilgili mevcut `[Modül/Sınıf]` yapısını tespit ettim. Yeni özelliği sıfırdan generic yazmak yerine bu altyapıyı kullanarak entegre edeceğim.*
3. **Mevcut Modülü Kullanma Zorunluluğu:** Sistemde zaten var olan bir yetenek yerine asla generic alternatifler yazma; mevcut yapıyı genişlet.
4. **Harita Güncelleme:** Projeye yeni bir ortak yetenek veya yardımcı modül eklendiğinde `SYSTEM_MAP.md` dosyasındaki modül haritasını senkronize güncelle.
```
