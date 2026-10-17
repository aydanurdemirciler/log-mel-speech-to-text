# log-mel-speech-to-text
Log-Mel Tabanlı Ses Analizi ve CNN-BiLSTM-CTC ile Metne Dönüştürme 
# 🎙️ Log-Mel Tabanlı Ses Analizi ve CNN-BiLSTM-CTC ile Metne Dönüştürme

  Bu proje, Karadeniz Teknik Üniversitesi (KTÜ) Bilgisayar Mühendisliği Bölümü Sinyaller ve Sistemler Dersi Dönem Projesi kapsamında geliştirilmektedir.

---

## 🎯 Projenin Amacı ve Problem Tanımı

### ❓ Problem
Ses sinyalleri zaman içinde sürekli değişen, çok sayıda frekans bileşeni barındıran ham dalga formlarıdır. Bilgisayarlar ve yapay zeka modelleri ham ses verilerini doğrudan işleyemez. Ayrıca insan kulağı frekansları doğrusal (linear) bir ölçekte değil, logaritmik olarak algılar. Ses verilerinin doğru analizi ve metne dönüştürülmesi için insan işitme sistemini taklit eden etkili öznitelik çıkarım yöntemlerine ihtiyaç vardır.

### 💡 Çözüm ve Amaç
Bu projede, Türkçe konuşma ses kayıtlarından **herhangi bir hazır ses kütüphanesi (Librosa vb.) kullanılmaksızın** saf matematiksel/matris işlemleriyle **Log-Mel Spektrumu** üretilmektedir. Elde edilen bu 2 boyutlu ses matrisleri/görüntüleri; **CNN (Convolutional Neural Network)**, **BiLSTM (Bidirectional LSTM)** ve **CTC (Connectionist Temporal Classification) Loss** mimarisi kullanılarak metne dönüştürülmektedir (Speech-to-Text / ASR).

---

## 🛠️ Kullanılan Yöntemler ve Algoritmalar

### 1. Sinyal İşleme (Sıfırdan Log-Mel Spektrum Çıkarımı)
- **Pre-emphasis (Ön Vurgulama):** Yüksek frekansların gücünü artırma.
- **Framing & Windowing (Çerçeveleme ve Pencereme):** Hamming/Hanning pencereleri ile sinyali durağan parçalara bölme.
- **FFT (Hızlı Fourier Dönüşümü):** Zaman ortamından frekans ortamına geçiş.
- **Mel Filterbank:** Frekansları insan kulağının duyma ölçeğine (Mel Scale) dönüştüren filtre matrisi.
- **Log Dönüşümü:** Spektrogram değerlerinin logaritmik ölçeğe getirilmesi.

### 2. Yapay Zeka Mimarisi (Speech-to-Text)
- **CNN:** Log-Mel spektrum resimlerinden yerel ses özelliklerini çıkarır.
- **BiLSTM:** Konuşma akışındaki zaman serisi bağımlılıklarını ileri ve geri yönde öğrenir.
- **CTC Loss:** Ses zamansal hizalaması bulunmayan verilerde harf/dizi eşleştirmesini sağlar.

---

## 📁 Proje Yapısı

```text
log-mel-speech-to-text/
│
├── data/                  # Kendi kaydettiğimiz .wav ses dosyaları (Temiz, Gürültülü, Hızlı vb.)
├── src/
│   ├── log_mel.py         # Sıfırdan kodlanmış Log-Mel spektrum modülü (NumPy)
│   ├── model.py           # CNN + BiLSTM + CTC model mimarisi
│   └── visualize.py       # Sinyal ve spektrum görselleştirme kodları
├── notebooks/
│   └── signal_processing.ipynb  # Google Colab analiz defteri
├── docs/
│   └── Ön_Rapor.pdf       # Dönem Ön Raporu
└── README.md              # Proje dokümantasyonu
