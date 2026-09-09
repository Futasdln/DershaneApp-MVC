# 🎓 EduSaaS — Çok Kiracılı (Multi-Tenant) Kurumsal Dershane & Kurs Yönetim Platformu

[![.NET 8](https://img.shields.io/badge/.NET-8.0-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)](https://dotnet.microsoft.com/)
[![ASP.NET Core MVC](https://img.shields.io/badge/ASP.NET_Core-MVC-blue?style=for-the-badge&logo=dotnet)](https://dotnet.microsoft.com/apps/aspnet)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![EF Core 8](https://img.shields.io/badge/EF_Core-8.0-purple?style=for-the-badge)](https://learn.microsoft.com/ef/core/)
[![Tests](https://img.shields.io/badge/Unit_Tests-57%20Passing-success?style=for-the-badge&logo=xunit)](https://xunit.net/)
[![License](https://img.shields.io/badge/License-Proprietary%20%2F%20All%20Rights%20Reserved-red?style=for-the-badge)](LICENSE)

> **Not:** Bu repo, **EduSaaS** projesinin mimarisini, teknik yeteneklerini ve modüllerini potansiyel müşterilere, yatırımcılara ve iş ortaklarına tanıtmak amacıyla hazırlanmış **kamuya açık vitrin (showcase)** dokümantasyonudur. Fikri mülkiyet ve ticari hakları korumak adına tam kaynak kodlar özel (private) depoda saklanmaktadır.

---

## 📌 Proje Özeti ve Değer Önerisi

**EduSaaS**, özel eğitim kurumları, dershaneler, kurs merkezleri ve etüt merkezleri için sıfırdan geliştirilmiş, uçtan uca kurumsal bir bulut yönetim platformudur. 

Geleneksel dershane yazılımlarının aksine, **modern Clean Architecture** prensipleri, **katı KVKK / Hukuki Uyum katmanı**, **yapay zeka destekli mesajlaşma denetimi** ve **tam otomatik finans/fatura motoru** ile kurumlara hem mali hem de operasyonel tam kontrol sağlar.

---

## 🚀 Öne Çıkan Temel Modüller

### 1. 💳 Muhasebe, Taksit & Otomatik Fatura Motoru
- **Taksitlendirme Sihirbazı:** Öğrenci kayıt ücretinin dinamik vade, faiz ve peşinat oranlarıyla otomatik taksitlere bölünmesi.
- **Otomatik Fatura Numaralandırma:** Yıl ve sayaç bazlı benzersiz fatura seri numaraları (`FAT-2026-000001`).
- **Türkçe Sayıyı Yazıya Çevirme:** Resmi fatura standardına uygun tutar metinleştirmesi (*"Yalnızca Dört Bin Beş Yüz Türk Lirası"*).
- **PDF Dekont & Raporlama:** QuestPDF entegrasyonu ile tek tıkla resmi onaylı, kurum logolu PDF tahsilat makbuzu ve fatura dökümü.
- **Finansal Analitik & Kasa:** Gelir-gider grafikleri, geciken ödemeler, tahsilat oranı ve nakit akışı göstergeleri.

### 2. ⚖️ KVKK & Hukuki Uyum Yönetim Merkezi
- **Zorunlu Rıza Onayı Middleware'i:** Kullanıcılar güncel KVKK Aydınlatma Metni ve Kullanım Koşullarını onaylamadan sisteme devam edemez.
- **Sözleşme Versiyonlama & İspat Yükümlülüğü:** Hangi kullanıcının hangi metin versiyonunu ne zaman onayladığına dair zaman damgalı loglama.
- **KVKK Veri Talep Portalı:** Velilerin/öğrencilerin verilerini talep etme, güncelleme veya silme/anonimleştirme taleplerini yönetebildiği idari akış.

### 3. 🛡️ Akıllı Mesajlaşma & İçerik Denetim Sistemi
- **Rol Tabanlı Güvenli İletişim:** Öğretmen, veli, öğrenci ve idare arasında izole mesajlaşma kanalları.
- **Otomatik İçerik Filtreleme:** Argo, küfür, taciz veya kurumsal iletişime aykırı ifadelerin anlık denetimi.
- **İdari Denetim Masası:** Şüpheli veya engellenen mesajların yöneticilerin onayına/denetimine düşmesi.

### 4. 📚 Akademik Süreçler & Öğrenci Takibi
- **Deneme Sınavı & Net Analizi:** Sınav sonuçları, sınıf içi ve okul geneli başarı grafikleri.
- **Devamsızlık & Yoklama Takibi:** Günlük yoklama ve veli anlık SMS/E-posta bildirim entegrasyonları.
- **Öğrenci & Veli Portalı:** Öğrencinin ödev, not, devamsızlık ve ödeme durumunu şeffaf izleyebildiği modern arayüzler.

---

## 🏗️ Mimari & Yazılım Standartları

Sistem, kurumsal standartlarda **N-Tier / Clean Architecture** modeline göre inşa edilmiştir:

```
┌─────────────────────────────────────────────────────────────┐
│                    DershaneApp.Web                          │
│     (Controllers, Razor Views, ViewModels, Middlewares)     │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│                  DershaneApp.Service                        │
│   (Business Logic, DTOs, Validations, PDF Engines, Mappers) │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│                   DershaneApp.Data                          │
│     (EF Core 8, DbContext, Repositories, Migrations)        │
└──────────────────────────────┬──────────────────────────────┘
                               │
┌──────────────────────────────▼──────────────────────────────┐
│                   DershaneApp.Core                          │
│      (Domain Entities, Enums, Interfaces, Domain Logic)     │
└─────────────────────────────────────────────────────────────┘
                               ▲
┌──────────────────────────────┴──────────────────────────────┐
│                   DershaneApp.Tests                         │
│            (xUnit, Moq, 57 Kapsamlı Test Senaryosu)         │
└─────────────────────────────────────────────────────────────┘
```

### Güvenlik & Dayanıklılık Önlemleri:
- **Çok Kiracılı (Multi-Tenancy) İzolasyon:** Her kurum `OkulId` ile izole edilir. EF Core `Global Query Filter` sayesinde bir kurum asla başka bir kurumun verisine erişemez.
- **IDOR Koruması:** Finansal işlemler, mesajlar ve belgeler çağrıyı yapan kullanıcının kurum kimliği ile doğrulanır.
- **CSRF & Rate Limiting:** Form gönderimlerinde Anti-Forgery Token zorunluluğu ve giriş noktalarında kaba kuvvet (brute-force) engelleme.
- **Güvenli Kimlik Doğrulama:** ASP.NET Core Identity & OTP çift aşamalı güvenlik desteği.

---

## 🧪 Test Kapsamı & Kalite Güvencesi

Proje, kritik finansal hesaplamalar ve güvenlik mekanizmaları için **57 adet birim ve entegrasyon testine** sahiptir:

```bash
Başarılı! - Başarısız: 0, Başarılı: 57, Atlanan: 0, Toplam: 57, Süre: 1 s
```
- Taksit hesaplama doğruluğu ve kuruş yuvarlama testleri
- IDOR güvenlik açığı denemeleri (Farklı okul verilerine erişim engeli)
- OTP Brute-Force deneme limitleri (5 hatalı denemede blokaj)
- Muhasebe kategori dağılımı ve nakit akış metrik hesaplamaları

---

## 💻 Kullanılan Teknolojiler

| Alan | Teknoloji |
|---|---|
| **Platform** | .NET 8.0 SDK / C# 12 |
| **Arayüz Katmanı** | ASP.NET Core MVC, Bootstrap 5, Chart.js, FontAwesome |
| **Veritabanı & ORM** | PostgreSQL, Entity Framework Core 8.0 |
| **Güvenlik** | ASP.NET Core Identity, BCrypt, RateLimiting Middleware |
| **Raporlama** | QuestPDF, EPPlus |
| **Test Çerçevesi** | xUnit, Moq, FluentAssertions |
| **Konteyner** | Docker, Docker Compose |

---

## 💼 Ticari Lisanslama & Satın Alma

Bu proje, anahtar teslim yazılım satışı veya SaaS abonelik modeli ile eğitim kurumlarına sunulmaya hazır durumdadır:

- **Kaynak Kod Satışı (Tam Mülkiyet Devri):** Projenin tüm telif hakları, kaynak kodları ve veritabanı şemaları ile birlikte devri.
- **Özelleştirilmiş Kurulum (White-Label):** Kendi markanız ve kurumsal kimliğiniz ile kurumunuza özel bulut dağıtımı.
- **Canlı Demo Talebi:** Yönetici, öğretmen ve veli panellerini canlı ortamda test etmek için demo hesabı talep edebilirsiniz.

📬 **İletişim & Ticari Teklifler:**
- **Geliştirici:** Furkan Taşdelen
- **E-posta:** furkantasdelen47@gmail.com
- **LinkedIn:** [Furkan Taşdelen](https://www.linkedin.com/in/furkan-tasdelen-11b244309/)
- **GitHub:** [@Futasdln](https://github.com/Futasdln)

---
*© 2026 Furkan Taşdelen. Tüm Hakları Saklıdır.*
