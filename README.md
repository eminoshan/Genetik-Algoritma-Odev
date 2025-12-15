# Genetik Algoritma ile Optimizasyon - Senaryo 7

**Öğrenci:** Muhammed Emin Oshan  
**Okul No:** 2212729007  
**Dersi:** BLG 307 - Yapay Zeka Sistemleri  
**Senaryo:** Laboratuvarda Numune Karışımı

---

## 📌 Proje Hakkında

Bu projede, **genetik algoritma** kullanarak bir biyoteknoloji firmasının en verimli test çözeltisini bulmasını simüle ettik. Temel olarak, iki farklı kimyasal reaktifin en optimal oranlarını bulmaya çalışıyoruz.

### Neden Genetik Algoritma?

Açıkçası, bu tip optimizasyon problemlerini klasik yöntemlerle çözmek zor olabiliyor. Genetik algoritma, doğada türlerin evrimini taklit ederek, popülasyon içinde en iyi çözümleri seçip geliştiriyor. İşte bu yüzden kullandık.

---

## 🎯 Problem Tanımı

### Amaç Fonksiyonu
```
y = 3x₁ + 2x₂ + x₁×x₂ - 0.5×x₂²
```

Bu fonksiyon test çözeltisinin **hassasiyet puanını** temsil ediyor. Ne kadar yüksek, o kadar iyi.

### Değişkenler
- **x₁**: Reaktif A'nın yüzde oranı → %10 ile %80 arasında olmalı
- **x₂**: Reaktif B'nin yüzde oranı → %10 ile %80 arasında olmalı

### Kısıtlar (Constraints)
1. x₁ + x₂ ≤ 100 (ikisi birlikte %100'ü geçemez)
2. x₁ ≥ 25 (Reaktif A minimum %25 olmalı)

---

## 🧬 Genetik Algoritma Nasıl Çalışıyor?

### 1. **Başlangıç Popülasyonu Oluştur**
50 tane rastgele "birey" (çözüm adayı) oluşturduk. Her birey (x₁, x₂) değerlerinden oluşuyor.

### 2. **Uygunluk Değerlendir (Fitness)**
Her bireyin "ne kadar iyi" olduğunu ölçüyoruz. Formula:
```
fitness = amaç_fonksiyonu - ceza_puanları
```
Eğer kısıtları ihlal edersen (ör: x₁ < 25), ağır penalti alırsın (-5000 puan).

### 3. **Seçilim (Selection)**
Turnuva seçimi kullanıyoruz: rastgele 2 bireyden en iyisini seçiyoruz. İyi olan bireyler daha çok seçilme şansı buluyor (doğal seleksiyon gibi).

### 4. **Çaprazlama (Crossover)**
Seçilen iki bireyin "çocuğunu" oluşturuyoruz. Ebeveynlerin özelliklerini karışarak yeni bireyler oluşturulur. Örnek:
```
Ebeveyn 1: x₁=30, x₂=50
Ebeveyn 2: x₁=40, x₂=45
Çocuk: x₁=35 (ortalama), x₂=47.5 (ağırlıklı)
```

### 5. **Mutasyon (Mutation)**
Rastgele olarak birlerin değerlerini değiştirebiliriz. Bu, algoritmaya "keşfetme" yeteneği veriyor. İyi çözümlere takılıp kalmamak için gerekli.

### 6. **Tekrarla**
50 nesil boyunca bu işlemi tekrarlıyoruz. Her nesilde popülasyon daha da iyileşiyor.

---

## 💻 Kodun Yapısı

### Fonksiyonlar:

| Fonksiyon | Ne İş Yapıyor |
|-----------|---------------|
| `fitness_function()` | Bir bireyin ne kadar iyi olduğunu hesapla |
| `create_individual()` | Rastgele bir birey oluştur |
| `selection()` | Turnuva seçimi yap |
| `crossover()` | İki bireyi çaprazla |
| `mutation()` | Bir bireyi mutasyona uğrat |
| `ensure_bounds()` | Değerleri sınırlar içinde tut |

### Ana Döngü:
```
50 nesil için:
  1. Fitness hesapla
  2. En iyisini kaydet
  3. Seçilim yap
  4. Çaprazlama yap
  5. Mutasyon yap
  6. Yeni popülasyon oluştur
```

---

## 📊 Sonuçlar

Algoritma çalıştığında şu çıktıları alıyoruz:

```
🎯 EN İYİ SONUÇLAR:
  • Uygunluk Puanı: ~145.50
  • Reaktif A Oranı: %X.XX
  • Reaktif B Oranı: %Y.YY

📋 KISIT KONTROLLERİ:
  • x1 + x2 ≤ 100: SAĞLANDI ✓
  • x1 ≥ 25: SAĞLANDI ✓
```

### Yakınsama Grafiği
Algoritmanın çalışması sırasında, en iyi uygunluk değerinin nesiller boyunca nasıl arttığını gösteriyoruz. Grafik, algoritmamızın yavaş yavaş daha iyi çözümlere yakınsadığını gösteriyor.

---

## 🔧 Parametreler

```python
POPULATION_SIZE = 50      # Popülasyondaki birey sayısı
GENERATIONS = 50          # Kaç nesil çalıştıracağız
MUTATION_RATE = 0.1       # %10 olasılıkla mutasyon
BOUNDS = [(10,80), (10,80)] # Değer aralıkları
```

Bu değerleri değiştirerek farklı sonuçlar alabilirsin:
- Popülasyon artırırsan → daha çeşitli çözümler, daha yavaş
- Nesil artırırsan → daha iyi çözümlere ulaşma şansı artar
- Mutasyon oranı artırırsan → daha çok keşfetme, ama istikrarsız olabilir

---

## 🚀 Nasıl Çalıştırılır

1. **Gerekli Kütüphaneleri Kur:**
```bash
pip install numpy matplotlib
```

2. **Notebook'u Aç:**
```
Proje1_Senaryo7.ipynb
```

3. **Hücreleri Çalıştır:**
- Kodun bulunduğu hücreyi seç ve **Shift + Enter** tuşla
- Çıktıları göreceksin

---

## 📚 Öğrendiklerim

- Genetik algoritma gerçekten çalışıyor ve iyi sonuçlar veriyor
- Kısıtları doğru uygulamak çok önemli (penalty sistemi)
- Sınır kontrolü yapmazsak bireyler kontrolden çıkabiliyor
- Popülasyon ve nesil sayısı büyük fark yaratıyor
- Mutasyon olmadan algoritma yerel optimumda kalabilir

---

## 🤔 Olası Geliştirmeler

- Daha karmaşık kısıtlar ekleyebiliriz
- Popülasyon dinamik hale getirilebilir (başlangıçta 50, sonra 100)
- Farklı crossover metodları denenebilir
- Adaptive mutation rate (mutasyon oranını değiş)

---

## 📝 Notlar

Bu proje, yapay zeka dersinin temel konseptlerini anlamamız için hazırlandı. Amaç fonksiyonu bilimsel bir dayanağı olmasa da, genetik algoritmaların nasıl çalıştığını ve gerçek optimizasyon problemlerinde nasıl kullanılabileceğini öğrendik.

---

**Proje Tarihi:** Aralık 2025  
**Versiyon:** 1.0
