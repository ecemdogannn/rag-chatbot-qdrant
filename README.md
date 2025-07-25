# Rag Chatbot

# Rag Chatbot 

#  RAG (Retrieval Augmented Generation) Chatbot Projeleri

Bu repository, n8n kullanılarak geliştirilmiş iki farklı **RAG tabanlı chatbot** workflow’unu barındırır. Her biri farklı bir veri kaynağı ile çalışır ve ayrı ayrı `branch`lerde konumlandırılmıştır. Her iki sistemde de veriler, vektör formuna getirilerek **Qdrant** vektör veritabanında saklanır. Kullanıcıdan gelen sorulara hem genel bilgi hem de bu özel veriler üzerinden **anlamlı ve bağlama uygun yanıtlar** üretilir.

---
##  Branch'ler

###  `main`  
**Form üzerinden PDF yüklemeli RAG Chatbot**

Bu branch’te kullanıcılar, bir form aracılığıyla PDF dosyaları yükler. Ardından bu dosyalar işlenerek aşağıdaki işlemler gerçekleştirilir:

#### Adımlar:
1. Kullanıcı formdan bir `.pdf` dosyası gönderir.
2. PDF içeriği okunur ve küçük metin parçalarına ayrılır.
3. Her metin parçası, Google Gemini Embeddings ile sayısal vektörlere dönüştürülür.
4. Vektörler, Qdrant vektör veritabanına aktarılır.
5. Kullanıcı sohbet başlattığında, soru embedding’i oluşturulur ve Qdrant’taki verilerle semantik arama yapılır.
6. Sonuçlar Gemini Chat Model ile doğal dilde bir cevap olarak döndürülür.

#### Kullanım Senaryosu:
- PDF dökümanları üzerinden etkileşimli bilgiye erişmek
- Kendi verilerinizle özel chatbot oluşturmak

---
###  `drive-integrated-chatbot`  
**Google Drive entegrasyonlu RAG Chatbot**

Bu branch’te chatbot, doğrudan Google Drive’daki `.txt` uzantılı belgeleri alır ve süreci aşağıdaki şekilde yürütür:

#### Adımlar:
1. Workflow elle başlatıldığında, Google Drive’da `.txt` uzantılı dosyalar aranır.
2. Seçilen dosya indirilir ve içeriği okunur.
3. Uzun metinler küçük parçalara bölünür.
4. Her parça Gemini Embeddings ile vektöre dönüştürülür.
5. Vektörler, Qdrant veritabanına eklenir.
6. Chat modülü, kullanıcının sorduğu sorular için Qdrant’ta arama yapar ve Gemini Model ile yanıt üretir.

#### Kullanım Senaryosu:
- Google Drive’daki metin dosyaları üzerinden akıllı sohbet
- Otomatik belge işleme ve semantik analiz

---
##  Kullanılan Teknolojiler
n8n (Low-code otomasyon platformu)
LangChain (Belge işleme, embedding, bellek modülleri)
Qdrant (Vektör veritabanı, semantik arama motoru)
Google Gemini / PaLM 2.5 (Büyük dil modeli ve embedding motoru)
Google Drive API (Google Drive’dan dosya alma)
n8n Forms (Kullanıcının PDF yükleyebildiği form arayüzü)


---
##  RAG Mimarisi Nedir?

RAG (Retrieval Augmented Generation), bir dil modeline (LLM) destekleyici veri sağlayarak daha doğru ve bağlamsal cevaplar üretmesini sağlar. Bu projelerde RAG şu şekilde işler:

1. Soru embedding’i oluşturulur.
2. Qdrant vektör veritabanında en ilgili veri parçaları bulunur.
3. Bu bilgilerle model, anlamlı ve desteklenmiş bir yanıt üretir.

---
##  Başlarken

Her branch kendi başına çalışan bağımsız bir workflow içerir. Başlamak için:

1. İlgili branch’e geçin (`pdf-upload-chatbot` veya `drive-integrated-chatbot`).
2. Gerekli `n8n credentials` (Google Drive API, Gemini API, Qdrant API) yapılandırmasını tamamlayın.
3. Workflow’u n8n’de import ederek çalıştırabilirsiniz.

---
##  Güvenlik

- API anahtarlarınızı kod içerisine yazmayın.
- n8n’de `Credentials` modülünü kullanarak güvenli anahtar yönetimi sağlayın.

---
##  Not

Bu repository, her biri farklı veri kaynağına sahip iki ayrı RAG sistemini göstermek amacıyla oluşturulmuştur. İki sistemin birbirinden izole olabilmesi adına ayrı `branch`lerde geliştirilmişlerdir.

---

