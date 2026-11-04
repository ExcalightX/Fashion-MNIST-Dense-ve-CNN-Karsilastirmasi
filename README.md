# Fashion-MNIST Üzerinde Sinir Ağı Mimari ve Düzenlileştirme Karşılaştırması

TensorFlow/Keras ile Fashion-MNIST veri seti üzerinde; epoch sayısı, Dropout, Batch Normalization, optimizer ve mimari (Dense / CNN) seçimlerinin sınıflandırma başarımına etkisini inceleyen karşılaştırmalı bir çalışma.

**Hazırlayan:** Göktuğ Vefa Uysal  
**Ders:** Yapay Sinir Ağları ve Derin Öğrenme

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](COLAB_LINKINIZI_BURAYA_YAPISTIRIN)

---

## Araştırma Sorusu
Epoch sayısı, Dropout, Batch Normalization, optimizer ve mimari seçimi, bir sinir ağının görüntü sınıflandırma başarımını ve aşırı öğrenme (overfitting) davranışını nasıl etkiler?

## Yöntem
- **Veri Seti:** Fashion-MNIST (60.000 eğitim, 10.000 test), piksel değerleri 0-1 aralığına normalize edilmiştir; eğitimin %15'i doğrulama için ayrılmıştır.
- **Temel Model:** Dense (256-128) + softmax.
- **Değerlendirme:** Her konfigürasyon 3 farklı seed (42, 7, 123) ile 20 epoch eğitilmiş, sonuçlar ortalama ± standart sapma olarak raporlanmıştır.

---

## Sonuçlar

| Model | Test Accuracy (ort ± std) | Test Loss (ort) |
| :--- | :---: | :---: |
| **CNN (Dropout 0.3)** | **%91.56 ± 0.10** | **0.2522** |
| Dense + Dropout 0.3 | %88.62 ± 0.07 | 0.3270 |
| Dense + Dropout + BatchNorm | %88.25 ± 0.48 | 0.3505 |
| Dense temel (Adam) | %87.59 ± 0.21 | 0.4235 |
| Dense + RMSprop | %87.19 ± 0.53 | 0.4806 |
| Dense + BatchNorm | %84.74 ± 0.79 | 0.6550 |
| Dense + SGD | %84.13 ± 1.00 | 0.4402 |

---

## Ana Bulgular
- **Dropout:** Dense ağda aşırı öğrenmeyi büyük ölçüde kapatarak en etkili düzenlileştirme yöntemi olmuştur.
- **Batch Normalization:** Küçük ölçekli bu Dense ağda beklenenin aksine ezberlemeyi artırarak performansı düşürmüştür.
- **CNN Üstünlüğü:** Piksel komşuluk ilişkilerini kullanan basit CNN mimarisi, en iyi Dense konfigürasyonuna göre yaklaşık **2.9 puan** daha yüksek başarı elde etmiştir.
- **Sınıf Bazlı Zorluk:** "Gömlek" (Shirt) sınıfı, tüm model varyasyonlarında ayırt edilmesi en zor kategori olarak öne çıkmıştır.

## Sınırlılıklar
- Yalnızca 3 seed kullanılmıştır.
- Hiperparametre optimizasyonu ve erken durdurma (early stopping) uygulanmamıştır.
- Çalışma yalnızca Fashion-MNIST veri setiyle sınırlıdır.

---

## Nasıl Çalıştırılır?
1. Yukarıdaki **"Open In Colab"** rozetine tıklayın (Google Colab paylaşım izninin "Bağlantıya sahip olan herkes" olduğundan emin olun).
2. Colab ortamında **Çalışma zamanı → Tümünü çalıştır** seçeneğini kullanarak tüm kodları ve deneyleri çalıştırabilirsiniz (T4 GPU önerilir).
