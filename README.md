# 🚗 Kanada Araç Veri Seti ile CO2 Emisyon Tahmini

Bu proje, Kanada hükümeti tarafından sağlanan 6282 satırlık araç veri setini kullanarak, araç özelliklerine dayalı olarak **CO2 emisyonlarını (g/km)** tahmin etmeyi amaçlayan bir uçtan uca makine öğrenmesi çalışmasıdır.

## 🎯 Projenin Amacı

Yüksek R² ve düşük RMSE değerlerine sahip sağlam bir regresyon modeli geliştirmek. Bu süreçte özellik mühendisliği (feature engineering), çoklu doğrusal bağlantı (multicollinearity) tespiti ve Lasso ile özellik eleme (feature selection) adımları uygulanmıştır.

## 🛠️ Kullanılan Teknolojiler

* **Veri Manipülasyonu:** `pandas`, `numpy`
* **Görselleştirme:** `matplotlib`, `seaborn`
* **Makine Öğrenmesi & İstatistik:** `scikit-learn`, `statsmodels`

## 🧠 Analiz ve Modelleme İş Akışı

1. **Keşifçi Veri Analizi (EDA):** Veri setinde eksik değere rastlanmamıştır. Hedef değişken ile en yüksek korelasyona sahip özelliğin karma yakıt tüketimi (`fuel_consumption_comb_l_100_km` -> 0.916) olduğu tespit edilmiştir.
2. **Çoklu Doğrusal Bağlantı (Multicollinearity) Kontrolü:** * **VIF (Variance Inflation Factor)** analizi sonucunda silindir sayısı (68.87) ve motor hacmi (45.80) gibi değişkenlerde VIF > 10 bulunarak yüksek çoklu doğrusal bağlantı tespit edilmiştir.
3. **Özellik Seçimi ve Düzenlileştirme:** * LassoCV (optimal alpha: 0.0544) kullanılarak 3 özellik modelden tamamen düşürülmüş (sıfırlanmış) ve en anlamlı 26 özellik ile yola devam edilmiştir.
4. **Modelleme:** Temel regresyon modellerinden ağaç tabanlı topluluk modellerine kadar çeşitli algoritmalar test edilmiştir.

## 📊 Sonuçlar ve Model Performansları

Yapılan testler sonucunda en düşük hata payını (RMSE) Polinom (Derece 2) destekli Lineer Regresyon sağlarken, hiperparametre optimizasyonu yapılmış (tuned) ağaç tabanlı modeller de literatürle yarışır düzeyde yüksek performans göstermiştir.

**Hiperparametre Optimizasyonlu Modeller:**
* **HistGradientBoosting (Tuned):** Test R² Skoru: 0.9958 | Test RMSE: 3.88 g/km
* **Gradient Boosting:** Test R² Skoru: 0.9975 | Test RMSE: 3.00 g/km
* **Poly(2) + Linear Reg.:** Test R² Skoru: 0.9976 | Test RMSE: 2.93 g/km

**Özellik Önemi (Feature Importance):**
Modele en büyük katkıyı sağlayan özellik **~%93.3** ağırlık ile karma yakıt tüketimi (`fuel_consumption_comb_l_100_km`) olmuştur. Onu co2_factor ve yakıt tipi (E) takip etmektedir.

## 📚 Literatür Karşılaştırması

Bu çalışmada elde edilen sonuçlar, literatürdeki benzer CO2 emisyon tahmini çalışmaları ile karşılaştırıldığında rekabetçi ve geçerli bir seviyededir:

| Kaynak | Model | R² Skoru | RMSE (g/km) |
| :--- | :--- | :--- | :--- |
| Gurcan Fatih | XGBoost | 0.9979 | 2.66 |
| Natarajan et al. | CatBoost | 0.9960 | 1.90 |
| Guo et al. | GBM | 0.9973 | 3.36 |
| **BU ÇALIŞMA** | **HistGradientBoosting (Tuned)** | **0.9958** | **3.88** |
| Saraswat et al. | MLP + GAO optimizer | 0.9881 | 6.48 |

## 🚀 Nasıl Çalıştırılır?

Projeyi bilgisayarınızda çalıştırmak için:

## 🚀 Nasıl Çalıştırılır?

Projeyi bilgisayarınızda çalıştırmak için:

1. Repoyu klonlayın:
   ```bash
   git clone [https://github.com/omerfarukturkmen/Kanada-Arac-Veri-Seti-ile-CO2-Emisyon-Tahmini.git](https://github.com/omerfarukturkmen/Kanada-Arac-Veri-Seti-ile-CO2-Emisyon-Tahmini.git)
