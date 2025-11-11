# n8n ile Akıllı E-posta Otomasyonları Projesi

Bu depo, e-posta yönetimini otomatikleştirmek için n8n ve Google Gemini AI kullanılarak oluşturulmuş workflow'ları içerir.

## 🎯 Projenin Amacı

Bu projenin temel amacı, [Şirket/Kişisel] e-posta hesabına gelen e-postaları manuel müdahale olmadan sınıflandırmak, ilgili kişilere yönlendirmek, verileri e-tablolara kaydetmek ve periyodik özetler oluşturmaktır.

---

##  Workflow'lar

### 1. Akıllı E-posta Sınıflandırıcı (`e-posta-siniflandirici.json`)

Bu workflow, bir Gmail hesabına gelen her yeni e-postayı okur, içeriğini Google Gemini ile analiz eder ve e-postayı kategorize eder.

* **Tetikleyici:** Yeni Gmail e-postası.
* **Yapay Zeka Modeli:** Google Gemini (Text Classifier)
* **İş Akışı:**
    1.  E-posta gelir (`Gmail Trigger`).
    2.  Metin, Gemini'ye gönderilerek `finans`, `sosyalmedya`, `reklam`, `güvenlik` olarak etiketlenir (`Text Classifier`).
    3.  **Finans ise:** E-postadaki fatura bilgileri (`Information Extractor`) ayıklanır ve bir Google E-Tablosuna (`Append row in sheet`) yazılır.
    4.  **Sosyal Medya ise:** Acil yanıt için ilgili ekibe bir mesaj gönderilir (`Send a message`).
    5.  Diğerleri (Reklam vb.) arşivlenir.

### 2. Günlük E-posta Özeti (`e-posta-ozetleyici.json`)

Bu workflow, her gün belirli bir saatte çalışarak son 24 saatte gelen önemli e-postaların bir özetini oluşturur ve bunu tek bir e-posta olarak gönderir.

* **Tetikleyici:** Zamanlanmış (`Schedule Trigger` - Her gün 08:00).
* **Yapay Zeka Modeli:** Google Gemini ve `Structured Output Parser`.
* **İş Akışı:**
    1.  Her sabah 08:00'de tetiklenir.
    2.  Son 24 saatin e-postalarını çeker (`Get many messages`).
    3.  Tüm e-postaları birleştirir (`Aggregate`).
    4.  Gemini AI, tüm metinleri okuyarak her birinden kısa bir özet ve gönderen bilgisi çıkarır (JSON formatında).
    5.  Bu yapılandırılmış özet, tarafıma tek bir e-posta olarak gönderilir (`Send a message`).

---

## 🔧 Nasıl Kullanılır?

1.  Bu depodaki `.json` dosyalarından birini indirin.
2.  Kendi n8n panelinizde "Import" (İçe Aktar) -> "Import from File" (Dosyadan Aktar) seçeneğini kullanın.
3.  Gmail, Google Sheets ve Google Gemini API'leri için kendi kimlik bilgilerinizi (credentials) ekleyin.
# n8n ile Akıllı E-posta Otomasyonları Projesi

Bu depo, e-posta yönetimini otomatikleştirmek için n8n ve Google Gemini AI kullanılarak oluşturulmuş workflow'ları içerir.

## 🎯 Projenin Amacı

Bu projenin temel amacı, [Şirket/Kişisel] e-posta hesabına gelen e-postaları manuel müdahale olmadan sınıflandırmak, ilgili kişilere yönlendirmek, verileri e-tablolara kaydetmek ve periyodik özetler oluşturmaktır.

---

##  Workflow'lar

### 1. Akıllı E-posta Sınıflandırıcı (`e-posta-siniflandirici.json`)

Bu workflow, bir Gmail hesabına gelen her yeni e-postayı okur, içeriğini Google Gemini ile analiz eder ve e-postayı kategorize eder.

* **Tetikleyici:** Yeni Gmail e-postası.
* **Yapay Zeka Modeli:** Google Gemini (Text Classifier)
* **İş Akışı:**
    1.  E-posta gelir (`Gmail Trigger`).
    2.  Metin, Gemini'ye gönderilerek `finans`, `sosyalmedya`, `reklam`, `güvenlik` olarak etiketlenir (`Text Classifier`).
    3.  **Finans ise:** E-postadaki fatura bilgileri (`Information Extractor`) ayıklanır ve bir Google E-Tablosuna (`Append row in sheet`) yazılır.
    4.  **Sosyal Medya ise:** Acil yanıt için ilgili ekibe bir mesaj gönderilir (`Send a message`).
    5.  Diğerleri (Reklam vb.) arşivlenir.

### 2. Günlük E-posta Özeti (`e-posta-ozetleyici.json`)

Bu workflow, her gün belirli bir saatte çalışarak son 24 saatte gelen önemli e-postaların bir özetini oluşturur ve bunu tek bir e-posta olarak gönderir.

* **Tetikleyici:** Zamanlanmış (`Schedule Trigger` - Her gün 08:00).
* **Yapay Zeka Modeli:** Google Gemini ve `Structured Output Parser`.
* **İş Akışı:**
    1.  Her sabah 07:00'de tetiklenir.
    2.  Son 24 saatin e-postalarını çeker (`Get many messages`).
    3.  Tüm e-postaları birleştirir (`Aggregate`).
    4.  Gemini AI, tüm metinleri okuyarak her birinden kısa bir özet ve gönderen bilgisi çıkarır (JSON formatında).
    5.  Bu yapılandırılmış özet, tarafıma tek bir e-posta olarak gönderilir (`Send a message`).

---

## 🔧 Nasıl Kullanılır?

1.  Bu depodaki `.json` dosyalarından birini indirin.
2.  Kendi n8n panelinizde "Import" (İçe Aktar) -> "Import from File" (Dosyadan Aktar) seçeneğini kullanın.
3.  Gmail, Google Sheets ve Google Gemini API'leri için kendi kimlik bilgilerinizi (credentials) ekleyin.
