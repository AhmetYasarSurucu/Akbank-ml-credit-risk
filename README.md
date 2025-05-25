# 💳 Credit Risk Prediction & Customer Segmentation – Akbank ML Bootcamp

Bu proje, **HMEQ veri seti** üzerinden kredi başvurusunda bulunan müşterilerin **geri ödeme yapıp yapmayacağını tahmin etmek** ve **müşteri segmentasyonu gerçekleştirmek** amacıyla hazırlanmıştır.

Geliştirilen modeller, eksik veri yönetimi, ölçekleme, encoding, modelleme ve hiperparametre optimizasyonu adımlarıyla desteklenmiştir. Ayrıca, KMeans ile gözetimsiz müşteri segmentasyonu yapılmıştır. En başarılı model olarak **XGBoost (RandomizedSearchCV)** belirlenmiştir.

## 📌 İnteraktif Notebook (Kaggle'da Çalıştır)

[![Kaggle](https://img.shields.io/badge/Notebook-Kaggle-blue?logo=kaggle&logoColor=white)](https://www.kaggle.com/code/ahmetsrc/credit-risk-customer-clustering-hmeq)

🔗 [Credit Risk & Customer Clustering – HMEQ (Kaggle)](https://www.kaggle.com/code/ahmetsrc/credit-risk-customer-clustering-hmeq)

---

## 📁 İçindekiler

* [🎯 Proje Hedefi](#🎯-proje-hedefi)
* [📊 Veri Seti ve Yapısı](#📊-veri-seti-ve-yapısı)
* [🧼 Veri Ön İşleme](#🧼-veri-ön-işleme)
* [📈 İstatistiksel Analizler](#📈-istatistiksel-analizler)
* [🤖 Makine Öğrenmesi Modelleri](#🤖-makine-öğrenmesi-modelleri)
* [📊 Model Performans Karşılaştırması](#📊-model-performans-karşılaştırması)
* [🧩 Müşteri Segmentasyonu (KMeans)](#🧩-müşteri-segmentasyonu-kmeans)
* [✅ Sonuç ve Öneriler](#✅-sonuç-ve-öneriler)

---

## 🎯 Proje Hedefi

* Müşterilerin kredi borçlarını geri ödeyip ödemeyeceğini tahmin etmek.
* Riskli müşteri profillerini önceden belirlemek.
* Kredi politikalarını destekleyecek müşteri kümelerini tanımlamak.

---

## 📊 Veri Seti ve Yapısı

* Toplam **5960 gözlem**, **13 değişken**.
* Hedef değişken: `BAD` (1 = borcunu ödeyemedi, 0 = ödedi)

![image](https://github.com/user-attachments/assets/6316c0b6-2db8-41cd-830a-71c443d2bd5b)


* Eksik veriler en çok `DEBTINC` (%21.26) sütununda yer almakta.
* Sayısal ve kategorik sütunlara dair özet istatistikler çıkarıldı.

---

## 🧼 Veri Ön İşleme

* **Eksik Veriler**: `IterativeImputer` (BayesianRidge) + "Unknown" kategorisi
* **Label Encoding**: `REASON`, `JOB`
* **Ölçekleme**: `StandardScaler`
* **Veri Ayrımı**: %80 eğitim / %20 test, stratified

---

## 📈 İstatistiksel Analizler

### Korelasyon Matrisi:

![image](https://github.com/user-attachments/assets/7d44d0c4-f207-4e5f-b1c1-89734e0506bb)


### Sayısal Değişken Dağılımları:

![image](https://github.com/user-attachments/assets/7f8618a9-d327-4d3f-9573-83dfb8a05829)


### Kategorik Değişken Dağılımı:

* REASON:

  ![image](https://github.com/user-attachments/assets/41b109b7-8713-4b95-b373-129b5fae8ccb)


* JOB:

  ![image](https://github.com/user-attachments/assets/9b0e13d6-c518-46be-87e3-589f7fa3bdc9)


---

## 🤖 Makine Öğrenmesi Modelleri

### Logistic Regression

* ROC Eğrisi:

  ![image](https://github.com/user-attachments/assets/5d3bb4f4-900b-4a35-80e5-1300ee72ae8c)


* Confusion Matrix:

  ![image](https://github.com/user-attachments/assets/f305120e-14fd-4b2c-819a-274e006fd296)


### Random Forest

* ROC Eğrisi:

  ![image](https://github.com/user-attachments/assets/88c3dcab-95f6-46ef-b6e9-c56bb4069e5b)


* Confusion Matrix:

  ![image](https://github.com/user-attachments/assets/f762630d-4ec1-4285-932a-f96a990cf308)


### XGBoost (Base)

* ROC Eğrisi:

  ![image](https://github.com/user-attachments/assets/cd3c749d-1200-49ad-a36b-b55ee8dc1880)


* Confusion Matrix:

  ![image](https://github.com/user-attachments/assets/2726e064-769f-41e0-8ccf-18a431bfb4ad)


### XGBoost (RandomizedSearchCV)

* ROC Eğrisi:

  ![image](https://github.com/user-attachments/assets/844fcc6c-f93d-484b-8089-3e187301fc97)


* Confusion Matrix:

  ![image](https://github.com/user-attachments/assets/eadeb358-330c-405d-a531-30187a6c1e57)


---

## 📊 Model Performans Karşılaştırması

| Model               | Accuracy | Precision | Recall   | F1 Score | ROC AUC  |
| ------------------- | -------- | --------- | -------- | -------- | -------- |
| Logistic Regression | 0.737    | 0.391     | 0.567    | 0.463    | 0.761    |
| Random Forest       | 0.913    | 0.947     | 0.597    | 0.732    | 0.964    |
| XGBoost             | 0.918    | 0.912     | 0.651    | 0.760    | 0.946    |
| XGBoost (Optimized) | 🥇 0.928 | 🥇 0.958  | 🥇 0.668 | 🥇 0.787 | 🥇 0.958 |

---

## 🧩 Müşteri Segmentasyonu (KMeans)

* KMeans ile 3 segment tespit edildi
* PCA ile 2 boyuta indirgenerek görselleştirildi:

![image](https://github.com/user-attachments/assets/25fa4f83-04fd-4f0f-ba34-94aedd2ecf49)

---

## ✅ Sonuç ve Öneriler

* XGBoost optimize modeli, hem **doğruluk hem duyarlılık** açısından en güçlü sonuçları vermiştir.
* Gözetimsiz öğrenme ile müşteri segmentasyonu başarıyla gerçekleştirilmiştir.
* Bu modelleme stratejisi:

  * Kredi verme süreçlerinde karar destek sistemi olarak
  * Pazarlama ve hedefleme stratejilerinde segmentasyon amaçlı kullanılabilir

### 📌 Geliştirme Önerileri

* SHAP ile model yorumlanabilirliği artırılabilir
* FastAPI/Flask ile model REST API olarak sunulabilir
* Zaman serisi veya müşteri davranış geçmişi eklenerek performans geliştirilebilir

---
## 🌐 Proje Bağlantıları

- 🔎 Kaggle Notebook: [Credit Risk & Customer Clustering – HMEQ](https://www.kaggle.com/code/ahmetsrc/credit-risk-customer-clustering-hmeq)

## 👤 Geliştirici

**Ahmet Yaşar Sürücü**  
Akbank ML Bootcamp – 2025  

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Profile-blue?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/ahmetyasarsurucu/)

