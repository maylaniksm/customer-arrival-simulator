# ⏱️ Simulasi Waktu Kedatangan Pelanggan di Loket Pelayanan

<div align="center">

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-11557c?style=for-the-badge&logo=python&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-8CAAE6?style=for-the-badge&logo=scipy&logoColor=white)

**Pemodelan Stokastik untuk Optimasi Sistem Antrian Pelayanan Publik**

[📓 Lihat Notebook](https://colab.research.google.com/drive/14a3z5B1CyCqLtgX7MB86sNHLlpzk3pNr?usp=sharing) • [🎯 Studi Kasus](#-studi-kasus) • [📊 Hasil Analisis](#-hasil-dan-analisis)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/14a3z5B1CyCqLtgX7MB86sNHLlpzk3pNr?usp=sharing)

</div>

---

## 📋 Daftar Isi

- [Tentang Proyek](#-tentang-proyek)
- [Studi Kasus](#-studi-kasus)
- [Teori dan Konsep](#-teori-dan-konsep)
- [Distribusi Eksponensial](#-distribusi-eksponensial)
- [Implementasi Simulasi](#-implementasi-simulasi)
- [Hasil dan Analisis](#-hasil-dan-analisis)
- [Perbandingan Distribusi](#-perbandingan-distribusi)
- [Kesimpulan](#-kesimpulan)
- [Penulis](#-penulis)

---

## 🎯 Tentang Proyek

Proyek ini merupakan **simulasi stokastik** untuk memodelkan dan menganalisis pola kedatangan pelanggan di sistem antrian loket pelayanan. Menggunakan pendekatan **distribusi eksponensial**, simulasi ini memberikan insight tentang:

- ⏰ **Pola waktu kedatangan pelanggan** yang acak dan independen
- 📊 **Validasi model matematis** dengan data simulasi
- 🔧 **Optimasi sistem pelayanan** berbasis data
- 📈 **Prediksi beban kerja** pada loket pelayanan

### 🎓 Konteks Akademik

**Mata Kuliah:** Pemodelan dan Simulasi Data C  
**Institusi:** Universitas Muhammadiyah Malang  
**Fokus:** Stochastic Modeling & Probability Distribution

---

## 🏢 Studi Kasus

### Permasalahan

Dalam dunia pelayanan publik, berbagai fasilitas menghadapi tantangan dalam mengelola antrian pelanggan:

| 🏥 **Rumah Sakit** | 🚉 **Stasiun** | 🏛️ **Kantor Pemerintah** | 🏦 **Bank** |
|-------------------|---------------|-------------------------|------------|
| Loket pendaftaran | Loket tiket | Loket administrasi | Teller |
| Pola kedatangan acak | Peak hours | Variasi harian | Rush hour |

### Objektif

Memahami dan memodelkan pola kedatangan pelanggan untuk:

1. **Mengoptimalkan jumlah loket** yang dibuka
2. **Memprediksi waktu tunggu** pelanggan
3. **Meningkatkan efisiensi** operasional
4. **Mengurangi antrian** dan komplain
5. **Perencanaan SDM** yang lebih baik

### Variabel Penelitian

```
📊 Variabel Acak: Waktu antar kedatangan pelanggan
🔢 Jenis Variabel: Kontinu (continuous random variable)
📈 Satuan: Menit
🎲 Karakteristik: Acak, Independen, Memoryless
```

---

## 📚 Teori dan Konsep

### Mengapa Distribusi Eksponensial?

Distribusi eksponensial adalah pilihan ideal untuk memodelkan waktu antar kedatangan karena memiliki sifat-sifat khusus:

#### 🔑 Sifat Memoryless (Tanpa Memori)

```
P(T > s + t | T > s) = P(T > t)
```

**Artinya:** Probabilitas pelanggan berikutnya datang dalam waktu *t* menit **tidak bergantung** pada berapa lama kita sudah menunggu.

#### ✨ Karakteristik Penting

- **Acak dan Independen**: Kedatangan satu pelanggan tidak mempengaruhi kedatangan berikutnya
- **Tingkat Kejadian Konstan**: Rate (λ) tetap sepanjang waktu
- **Non-negative**: Waktu selalu bernilai positif
- **Right-skewed**: Sebagian besar kedatangan dalam interval pendek

---

## 📐 Distribusi Eksponensial

### Formula Matematis

#### Probability Density Function (PDF)

```
f(x; λ) = λe^(-λx)    untuk x ≥ 0
```

Dimana:
- `λ` (lambda) = rate parameter (tingkat kejadian per satuan waktu)
- `x` = waktu antar kedatangan
- `e` = konstanta Euler (≈ 2.71828)

#### Cumulative Distribution Function (CDF)

```
F(x; λ) = 1 - e^(-λx)    untuk x ≥ 0
```

### Parameter Simulasi

Dalam simulasi ini:

| Parameter | Simbol | Nilai | Keterangan |
|-----------|--------|-------|------------|
| **Mean Arrival Time** | μ | 5 menit | Rata-rata waktu antar kedatangan |
| **Rate Parameter** | λ | 0.2 per menit | λ = 1/μ = 1/5 |
| **Jumlah Iterasi** | n | 30 | Sample size simulasi |

### Interpretasi

```python
# Jika λ = 0.2 (atau μ = 5 menit)
# Maka rata-rata: Setiap 5 menit ada 1 pelanggan datang
# Atau: Dalam 1 jam, rata-rata ada 12 pelanggan
```

### Visualisasi Distribusi

```
Probability Density Function (PDF)

    |
0.20|█
    |██
0.15|███
    |████
0.10|█████
    |██████▄
0.05|████████▄▄▄
    |████████████▄▄▄▄▄▄
0.00|________________________▄▄▄▄▄▄▄▄▄
    0  2  4  6  8 10 12 14 16 18 20
         Waktu (menit)
```

**Insight:**
- Probabilitas tertinggi pada waktu dekat 0
- Semakin lama waktu tunggu, semakin kecil probabilitasnya
- Tail panjang menunjukkan kemungkinan ada gap yang panjang (jarang tapi mungkin)

---

## 💻 Implementasi Simulasi

### Requirements

```python
import numpy as np
import matplotlib.pyplot as plt
from scipy import stats
```

### Code Implementation

#### 1. Setup Parameter

```python
# Parameter distribusi eksponensial
mean_interarrival_time = 5  # menit
lambda_param = 1 / mean_interarrival_time  # λ = 0.2
num_simulations = 30  # jumlah iterasi
```

#### 2. Generate Random Process

```python
# Generate waktu antar kedatangan menggunakan distribusi eksponensial
np.random.seed(42)  # untuk reproducibility
interarrival_times = np.random.exponential(
    scale=mean_interarrival_time, 
    size=num_simulations
)

print(f"Simulasi {num_simulations} kedatangan pelanggan:")
print(f"Waktu antar kedatangan (menit): {interarrival_times}")
```

#### 3. Analisis Statistik

```python
# Statistik deskriptif
simulated_mean = np.mean(interarrival_times)
simulated_std = np.std(interarrival_times)
theoretical_mean = mean_interarrival_time
theoretical_std = mean_interarrival_time  # Untuk eksponensial: std = mean

print(f"\n{'='*50}")
print(f"HASIL ANALISIS STATISTIK")
print(f"{'='*50}")
print(f"Rata-rata Simulasi    : {simulated_mean:.2f} menit")
print(f"Rata-rata Teoritis    : {theoretical_mean:.2f} menit")
print(f"Selisih               : {abs(simulated_mean - theoretical_mean):.2f} menit")
print(f"Std Dev Simulasi      : {simulated_std:.2f} menit")
print(f"Std Dev Teoritis      : {theoretical_std:.2f} menit")
```

#### 4. Visualisasi

```python
# Histogram waktu antar kedatangan
plt.figure(figsize=(14, 5))

# Subplot 1: Histogram dengan PDF teoritis
plt.subplot(1, 2, 1)
plt.hist(interarrival_times, bins=10, density=True, 
         alpha=0.7, color='skyblue', edgecolor='black', 
         label='Data Simulasi')

# Overlay PDF teoritis
x = np.linspace(0, max(interarrival_times), 100)
pdf_theoretical = lambda_param * np.exp(-lambda_param * x)
plt.plot(x, pdf_theoretical, 'r-', linewidth=2, 
         label='PDF Teoritis (λ=0.2)')

plt.axvline(simulated_mean, color='blue', linestyle='--', 
            linewidth=2, label=f'Mean Simulasi ({simulated_mean:.2f})')
plt.axvline(theoretical_mean, color='red', linestyle='--', 
            linewidth=2, label=f'Mean Teoritis ({theoretical_mean:.2f})')

plt.xlabel('Waktu Antar Kedatangan (menit)', fontsize=12)
plt.ylabel('Density', fontsize=12)
plt.title('Distribusi Waktu Antar Kedatangan Pelanggan', fontsize=14, fontweight='bold')
plt.legend()
plt.grid(alpha=0.3)

# Subplot 2: Time series kedatangan
plt.subplot(1, 2, 2)
arrival_times = np.cumsum(interarrival_times)
plt.plot(range(num_simulations), arrival_times, 
         marker='o', linestyle='-', color='green', 
         linewidth=2, markersize=8)
plt.xlabel('Nomor Pelanggan', fontsize=12)
plt.ylabel('Waktu Kedatangan Kumulatif (menit)', fontsize=12)
plt.title('Time Series Kedatangan Pelanggan', fontsize=14, fontweight='bold')
plt.grid(alpha=0.3)

plt.tight_layout()
plt.show()
```

---

## 📊 Hasil dan Analisis

### Hasil Simulasi

Berdasarkan **30 iterasi** simulasi dengan parameter λ = 0.2 (μ = 5 menit):

```
╔════════════════════════════════════════════════╗
║          RINGKASAN HASIL SIMULASI              ║
╚════════════════════════════════════════════════╝

📊 Statistik Deskriptif:
   • Rata-rata Simulasi      : 5.66 menit
   • Rata-rata Teoritis      : 5.00 menit
   • Selisih (Error)         : 0.66 menit (13.2%)
   
📈 Variabilitas:
   • Standar Deviasi         : ~5.00 menit
   • Varians                 : ~25.00 menit²
   • Coefficient of Variation: ~100%
   
⏱️ Range Waktu:
   • Minimum                 : ~0.5 menit
   • Maksimum                : ~18.5 menit
   • Median                  : ~4.2 menit
```

### Interpretasi Hasil

#### ✅ Validitas Model

1. **Konvergensi ke Mean Teoritis**
   - Rata-rata simulasi (5.66 menit) mendekati teoritis (5.00 menit)
   - Selisih 13.2% masih dalam toleransi untuk n=30
   - Dengan n lebih besar, akan semakin konvergen (Law of Large Numbers)

2. **Distribusi Sesuai Ekspektasi**
   - Histogram menunjukkan pola right-skewed khas eksponensial
   - Mayoritas nilai di bawah mean (karakteristik eksponensial)
   - Overlay PDF teoritis cocok dengan data simulasi

3. **Variabilitas Realistis**
   - Standar deviasi ≈ mean (ciri khas distribusi eksponensial)
   - Range lebar menunjukkan variasi alami dalam sistem real

#### 🎯 Insight Bisnis

**Untuk Sistem Pelayanan:**

```
Skenario dengan λ = 0.2 (1 pelanggan per 5 menit)

🕐 Dalam 1 jam (60 menit):
   • Ekspektasi pelanggan: 12 orang
   • Range realistis: 8-16 orang
   
📅 Dalam 1 hari kerja (8 jam):
   • Ekspektasi pelanggan: 96 orang
   • Peak bisa mencapai: 120+ orang
   
⏳ Implikasi Waktu Tunggu:
   • Jika waktu layanan < 5 menit → Antrian stabil
   • Jika waktu layanan > 5 menit → Antrian bertambah
```

---

## ⚖️ Perbandingan Distribusi

### Mengapa Bukan Distribusi Lain?

#### 1. 🚫 Distribusi Normal

```python
# Masalah dengan Normal Distribution
X ~ N(μ=5, σ²=4)

❌ Dapat menghasilkan nilai NEGATIF
   P(X < 0) > 0  # Waktu negatif tidak masuk akal!
   
❌ Simetris - tidak realistis untuk waktu kedatangan
   Real: Banyak kedatangan cepat, sedikit yang lama
   Normal: Sama banyak di kiri dan kanan mean
```

**Visualisasi Perbandingan:**

```
Normal Distribution         Exponential Distribution
      
      ╱╲                          █╲
     ╱  ╲                         ██╲___
    ╱    ╲                        ████████╲______
   ╱      ╲                       ██████████████████╲____
__╱________╲___              ____█████████████████████████___
  ↑                              ↑
Bisa negatif!                 Selalu positif ✓
```

#### 2. 🚫 Distribusi Uniform

```python
# Masalah dengan Uniform Distribution
X ~ U(a=0, b=10)

❌ Semua waktu punya probabilitas SAMA
   P(0-1 menit) = P(5-6 menit) = P(9-10 menit)
   
❌ Tidak realistis - kejadian acak cenderung clustered
   Real: Pelanggan lebih sering datang berdekatan
```

**Contoh Tidak Realistis:**

```
Uniform: [2.1, 5.3, 7.8, 3.4, 8.9, 1.2, 6.5]
         Terlalu teratur, seperti dijadwalkan

Exponential: [0.5, 0.8, 3.2, 0.3, 8.1, 1.5, 0.7]
             Lebih banyak interval pendek, sesekali panjang ✓
```

#### 3. 🚫 Distribusi Poisson

```python
# Masalah dengan Poisson Distribution
X ~ Poisson(λ=12)

❌ Model untuk JUMLAH kejadian, bukan WAKTU
   Poisson: "Berapa pelanggan dalam 1 jam?"
   Exponential: "Berapa lama sampai pelanggan datang?"
   
✅ Namun, ada hubungan:
   Jika antar-kedatangan ~ Exp(λ), 
   maka jumlah per satuan waktu ~ Poisson(λ)
```

### Tabel Perbandingan Komprehensif

| Aspek | Eksponensial ✓ | Normal ✗ | Uniform ✗ | Poisson ✗ |
|-------|---------------|----------|-----------|-----------|
| **Nilai Negatif** | Tidak mungkin ✓ | Bisa terjadi ✗ | Tidak mungkin ✓ | Tidak mungkin ✓ |
| **Tipe Variabel** | Kontinu, Waktu ✓ | Kontinu | Kontinu | Diskrit, Count ✗ |
| **Memoryless** | Ya ✓ | Tidak | Tidak | Tidak |
| **Skewness** | Right-skewed ✓ | Simetris ✗ | Simetris ✗ | Right-skewed ✓ |
| **Realistis untuk Waktu** | Sangat ✓✓✓ | Tidak ✗ | Tidak ✗ | N/A ✗ |
| **Kompleksitas** | Sederhana ✓ | Sederhana | Sederhana | Sederhana |

---

## 💡 Kesimpulan

### Ringkasan Hasil

Berdasarkan simulasi yang telah dilakukan, dapat disimpulkan bahwa:

1. **Distribusi Eksponensial Sesuai**
   - Model yang paling tepat untuk waktu antar kedatangan pelanggan
   - Mencerminkan sifat acak dan independen dari kedatangan
   - Memiliki properti memoryless yang realistis

2. **Validasi Model Berhasil**
   - Rata-rata simulasi (5.66 menit) mendekati nilai teoritis (5.00 menit)
   - Hasil menunjukkan model berjalan dengan baik
   - Variabilitas data sesuai dengan karakteristik distribusi eksponensial

3. **Aplikasi Praktis**
   - Model dapat digunakan untuk prediksi beban kerja loket
   - Membantu optimasi jumlah petugas pelayanan
   - Dasar untuk analisis sistem antrian yang lebih kompleks

### Keunggulan Distribusi Eksponensial

- ✅ **Tidak menghasilkan nilai negatif** (seperti Normal)
- ✅ **Mencerminkan pola acak yang realistis** (tidak seperti Uniform)
- ✅ **Sesuai untuk variabel waktu kontinu** (bukan count seperti Poisson)
- ✅ **Sederhana namun powerful** untuk modeling

### Rekomendasi

Distribusi eksponensial sangat direkomendasikan untuk:
- Sistem pelayanan publik (rumah sakit, bank, kantor pemerintah)
- Analisis antrian dan waktu tunggu
- Perencanaan kapasitas dan resource allocation
- Studi simulasi sistem stokastik

---

## 🚀 Instalasi dan Penggunaan

### Prerequisites

```bash
Python 3.7+
pip (Python package manager)
```

### Installation

#### 1. Clone Repository

```bash
git clone https://github.com/username/customer-arrival-simulation.git
cd customer-arrival-simulation
```

#### 2. Install Dependencies

```bash
pip install numpy matplotlib scipy
```

#### 3. Jalankan Simulasi

**Opsi A: Google Colab** (Recommended)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/14a3z5B1CyCqLtgX7MB86sNHLlpzk3pNr?usp=sharing)

**Opsi B: Jupyter Notebook**

```bash
jupyter notebook simulation.ipynb
```

**Opsi C: Python Script**

```bash
python simulate_arrivals.py
```

### Kustomisasi Parameter

```python
# Edit parameter sesuai kebutuhan
mean_interarrival_time = 5    # dalam menit
num_simulations = 30           # jumlah sampel
random_seed = 42               # untuk reproducibility
```

---

## 👤 Penulis

**Maylani Kusuma Wardhani**

- 🎓 **NIM**: 202210370311123
- 📚 **Kelas**: Pemodelan dan Simulasi Data C
- 🏫 **Institusi**: Universitas Muhammadiyah Malang

---

## 📄 Lisensi

Proyek ini dibuat untuk keperluan akademik dan pembelajaran.

---

## 🔗 Links Penting

- 📓 **Google Colab Notebook**: [Buka Simulasi](https://colab.research.google.com/drive/14a3z5B1CyCqLtgX7MB86sNHLlpzk3pNr?usp=sharing)

---

<div align="center">

### ⭐ Jika proyek ini bermanfaat, berikan star!

**Made with 💙 and ☕ by Maylani Kusuma Wardhani**

`Simulasi • Analisis • Optimasi`

---

![Footer](https://img.shields.io/badge/Status-Active-success?style=for-the-badge)
![Academic](https://img.shields.io/badge/Purpose-Academic-orange?style=for-the-badge)

</div>
