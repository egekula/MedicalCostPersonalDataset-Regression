# Medical Cost Analysis and Prediction

Bu proje, kişisel verileri kullanarak sağlık sigortası maliyetlerini tahmin etmeye yönelik regresyon analizi çalışmalarını içermektedir.

### Projenin Amacı
Bu projenin amacı, yaş, cinsiyet, BMI, çocuk sayısı, sigara kullanımı ve bölge gibi demografik ve yaşam tarzı özelliklerini kullanarak bireylerin yıllık sağlık sigortası masraflarını (`charges`) en doğru şekilde tahmin eden makine öğrenmesi modelleri geliştirmektir.

### Yapılan İşlemler
1.  **Veri Keşfi (EDA) ve Görselleştirme:**
    *   Veri setindeki değişkenlerin tipleri ve eksik değer durumları incelendi.
    *   `charges` (ücretler) değişkeninin dağılımı görselleştirildi; verinin sağa çarpık olduğu gözlemlendi.
    *   Kategorik değişkenlerin hedef değişken üzerindeki etkileri analiz edildi.
2.  **Veri Ön İşleme:**
    *   `sex`, `smoker` ve `region` sütunları One-Hot Encoding yöntemiyle sayısal formata dönüştürüldü.
    *   IQR (Interquartile Range) yöntemi kullanılarak aykırı değerler (outliers) tespit edildi ve temizlendi.
    *   Veri seti eğitim (%75) ve test (%25) kümelerine ayrıldı.
    *   SVM gibi mesafe tabanlı modeller için `StandardScaler` kullanılarak özellik ölçeklendirme yapıldı.
3.  **Model Eğitimi ve Hiperparametre Optimizasyonu:**
    *   **Linear Regression:** Basit doğrusal regresyonun yanı sıra Ridge ve Lasso düzenlileştirme yöntemleri uygulandı.
    *   **Polynomial Regression:** Veriler polinomsal özelliklere dönüştürülerek model karmaşıklığı artırıldı.
    *   **Decision Tree Regressor:** Standart modelin yanı sıra GridSearchCV ile `max_depth` ve `min_samples_leaf` gibi parametreler optimize edildi.
    *   **SVM Regressor:** `C`, `gamma` ve `kernel` parametreleri GridSearchCV ile optimize edilerek model performansı artırıldı.
4.  **Model Değerlendirme:**
    *   Tüm modeller R2 Skoru, MAE (Mean Absolute Error) ve MSE (Mean Squared Error) metrikleri kullanılarak karşılaştırıldı.

### Sonuçlar
Proje kapsamında eğitilen modellerin test seti üzerindeki performans sonuçları aşağıdadır:

| Model | R2 Skoru | MAE | MSE |
| :--- | :--- | :--- | :--- |
| Linear Regression | 0.7759 | 3864.02 | 3.10e+07 |
| LassoCV Regression | 0.7768 | 3840.70 | 3.08e+07 |
| Polynomial Lasso Regression | 0.8621 | 2662.87 | 1.91e+07 |
| Decision Tree (Base) | 0.6799 | 3209.42 | 4.42e+07 |
| **Decision Tree (GridSearch)** | **0.8726** | **1747.21** | **1.76e+07** |
| SVM (Base) | -0.0799 | 7951.75 | 1.49e+08 |
| SVM (GridSearch) | 0.7310 | 2771.62 | 3.72e+07 |

*Analiz sonucunda, **Decision Tree (GridSearch)** modeli en yüksek R2 skoru ve en düşük hata payı ile en başarılı model olmuştur.*

### Kullanılan Dataset
[Medical Cost Personal Dataset (Kaggle)](https://www.kaggle.com/datasets/mirichoi0218/insurance/data)
