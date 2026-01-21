# BISINDO Translator

**Pengenalan Huruf Bahasa Isyarat Indonesia (BISINDO) Menggunakan CNN dan LSTM Berbasis Web**

## Deskripsi Proyek

Proyek ini bertujuan untuk membangun sistem penerjemah **Bahasa Isyarat Indonesia (BISINDO)** menggunakan pendekatan **Deep Learning** dengan dua model utama yang berjalan *secara terpisah*:

* **CNN (MobileNet)** untuk klasifikasi citra BISINDO (berbasis gambar)
* **LSTM** untuk pengenalan urutan gerakan (sequence-based, real-time)

Sistem ini dilengkapi dengan *aplikasi web berbasis Flask* yang memungkinkan pengguna:

* Menerjemahkan BISINDO secara *real-time*
* Menerjemahkan BISINDO dari *gambar yang diunggah*

---

## Arsitektur Model

* **CNN (MobileNet)**
  Digunakan untuk klasifikasi citra hasil ekstraksi frame dari video BISINDO.
* **LSTM (Landmark Sequence)**
  Digunakan untuk mengenali pola gerakan tangan secara berurutan (sequence) untuk kebutuhan real-time.

---

## Struktur Proyek (Lengkap)

```
├── CNN
│   ├── Video_BISINDO
│   ├── Citra_BISINDO
│   ├── dataset_raw
│   ├── dataset_balanced
│   ├── BISINDO_split_aug
│   ├── BISINDO_FINAL
│   ├── sanity_check
│   ├── test_images
│   ├── model_bisindo_mobilenet.h5
│   ├── classification_report_final.txt
│   ├── confusion_matrix_final.png
│   ├── training_history.json
│   ├── step_1_ekstrak_frame.py
│   ├── step_2_balance_dataset.py
│   ├── step_3_split_dataset.py
│   ├── step_4_offlineaug_hist_equalization.py
│   ├── step_5_visual_sanity_check.py
│   ├── step_6_final_split_dataset.py
│   ├── step_7_final_checksplit.py
│   ├── step_8_data_generator_zscore.py
│   ├── step_9_model_mobilenet.py
│   ├── step_10_final_train_mobilenet.py
│   ├── step_11_final_confusion_matrix.py
│   ├── step_12_final_classification_report.py
│   ├── step_13_history.py
│   ├── step_14_akurasi_loss.py
│   └── step_15_test_single_image.py
│
├── LSTM
│   ├── landmark_sequence_dataset2
│   ├── evaluation_plots
│   │   ├── confusion_matrix_all_classes.png
│   │   ├── confusion_matrix_huruf_mirip.png
│   │   ├── accuracy_curve.png
│   │   └── loss_curve.png
│   ├── model_bisindo_landmark_lstm.h5
│   ├── class_index_lstm.json
│   ├── history_lstm2.json
│   ├── step_1_record_sequence.py
│   ├── step_2_train_lstm.py
│   ├── step_3_evaluation.py
│   ├── step_4_accuracy_loss.py
│   └── step_5_realtime_bisindo.py
│
├── Web_app
│   ├── UJI_Upload
│   ├── models
│   │   ├── cnn_mobilenet.h5
│   │   ├── lstm_predict.h5
│   │   ├── class_indices.json
│   │   └── class_index_lstm.json
│   ├── static
│   │   └── style.css
│   ├── templates
│   │   ├── index.html
│   │   ├── translate_realtime.html
│   │   ├── translate_upload.html
│   │   └── tutorial.html
│   ├── uploads
│   ├── utils
│   │   ├── cnn_preprocess.py
│   │   └── lstm_predict.py
│   ├── app.py
│   └── requirements.txt

```

---

##  Dataset

### 1. Dataset Publik (Kaggle)
Dataset BISINDO Publik digunakan sebagai data tambahan lalu ditambahkan ke folder Citra_BISINDO/ bersama Dataset Pribadi.  

[Dataset BISINDO Kaggle](https://www.kaggle.com/datasets/achmadnoer/alfabet-bisindo)

---

### 2. Dataset Pribadi
- Data dikumpulkan melalui **perekaman video BISINDO**
- Disimpan pada folder:
```

Video_BISINDO/

```
- Video diekstrak menjadi frame menggunakan:
```

step_1_ekstrak_frame.py

```
- Output:
```

Citra_BISINDO/

```

---

## Pipeline CNN (MobileNet)

1. Ekstraksi Frame (`step_1_ekstrak_frame.py`)
2. Balancing Dataset (`step_2_balance_dataset.py`)
3. Split Dataset (`step_3_split_dataset.py`)
4. Offline Augmentation & Histogram Equalization (`step_4_offlineaug_hist_equalization.py`)
5. Visual Sanity Check (`step_5_visual_sanity_check.py`)
6. Final Split Dataset (`step_6_final_split_dataset.py`)
7. Final Check Split (`step_7_final_checksplit.py`)
8. Data Generator Z-Score (`step_8_data_generator_zscore.py`)
9. Model MobileNet (`step_9_model_mobilenet.py`)
10. Training (`step_10_final_train_mobilenet.py`)
11. Confusion Matrix (`step_11_final_confusion_matrix.py`)
12. Classification Report (`step_12_final_classification_report.py`)
13. History (`step_13_history.py`)
14. Akurasi & Loss Plot (`step_14_akurasi_loss.py`)
15. Test Single Image (`step_15_test_single_image.py`)

---

## Pipeline LSTM

1. Record Sequence (`step_1_record_sequence.py`)
2. Training LSTM (`step_2_train_lstm.py`)
3. Evaluasi (`step_3_evaluation.py`)
4. Accuracy & Loss (`step_4_accuracy_loss.py`)
5. Realtime BISINDO (`step_5_realtime_bisindo.py`)

---

## Aplikasi Web (Flask)

### Struktur Web App
```

Web_app/
├── UJI_Upload
├── models
│   ├── cnn_mobilenet.h5
│   ├── lstm_predict.h5
│   ├── class_indices.json
│   └── class_index_lstm.json
├── static
│   └── style.css
├── templates
│   ├── index.html
│   ├── translate_realtime.html
│   ├── translate_upload.html
│   └── tutorial.html
├── uploads
├── utils
│   ├── cnn_preprocess.py
│   └── lstm_predict.py
├── app.py
└── requirements.txt

````

### Penjelasan Singkat
- **UJI_Upload**: gambar uji coba manual
- **models/**: model CNN & LSTM yang digunakan website
- **utils/**: preprocessing dan prediksi ML
- **uploads/**: penyimpanan input user
- **app.py**: Flask API

---

## Menjalankan Aplikasi Web
```bash
pip install -r requirements.txt
python app.py
````

Akses melalui browser:

```
http://127.0.0.1:5000/
```

---

## Output Akhir

* Model CNN & LSTM
* Confusion Matrix
* Classification Report
* Grafik Accuracy & Loss
* Website Translator BISINDO

---

## Catatan

Proyek ini dikembangkan untuk keperluan **UAS PENGOLAHAN CITRA DIGITAL** dan masih dapat dikembangkan lebih lanjut.
