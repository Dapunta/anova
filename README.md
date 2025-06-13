# ANALYSIS OF VARIANCE (ANOVA)

Mata Kuliah : Probabilitas & Statistik  
Kelas : B  
Kelompok : 3

| NRP        | Nama                         |
|------------|------------------------------|
| 5025231024 | Nixon Castroman              |
| 5025231031 | Nicholas                     |
| 5025231046 | Dustin Felix                 |
| 5025231187 | Dapunta Adyapaksi Ratyanasja |

### Table of Content
- [Materi 1 : Konsep Dasar](#materi-1--konsep-dasar)
    - [1.1. Pengertian](#11-pengertian)
    - [1.2. Sejarah](#12-sejarah)
    - [1.3. Distribusi F](#13-distribusi-f)
    - [1.4. Distribusi t](#14-distribusi-t)
    - [1.5. Distribusi t vs Distribusi F](#15-distribusi-t-vs-distribusi-f)
    - [1.6. P-Value dalam ANOVA](#16-p-value-dalam-anova)
    - [1.7. Jenis-jenis ANOVA](#17-jenis-jenis-anova)
- [Materi 2 : Studi Kasus One-Way ANOVA](#materi-2--studi-kasus-one-way-anova)
    - [Notebook Materi 2](/model/one_way/anova_one_way.ipynb)
- [Materi 3 : Studi Kasus Two-Way ANOVA](#materi-3--studi-kasus-two-way-anova)
    - [Notebook Materi 3](/model/two_way/anova_two_way.ipynb)
- [Materi 4 : Pengujian Asumsi & Alternatif ANOVA](#materi-4--pengujian-asumsi--alternatif-anova)
    - [4.1. Pengujian Asumsi Sebelum Anova](#41-pengujian-asumsi-sebelum-anova)
    - [4.2. Jika Asumsi Tidak Terpenuhi](#42-jika-asumsi-tidak-terpenuhi)
    - [4.3. Checklist Implementasi Anova](#43-checklist-implementasi-anova)
    - [4.4. Library Python](#44-library-python)

## Materi 1 : Konsep Dasar

### 1.1. Pengertian

**ANOVA** *(Analysis of Variance)* adalah metode statistik untuk membandingkan rata-rata lebih dari dua kelompok.

Metode ini bertujuan untuk mengetahui apakah perbedaan rata-rata yang terjadi karena faktor perlakuan atau hanya kebetulan.

### 1.2. Sejarah

Dikembangkan dan diperkenalkan oleh Ronald A. Fisher pada 1920-an.

### 1.3. Distribusi F
ANOVA menggunakan F-statistic untuk mengukur apakah variansi antar grup lebih besar dari variansi dalam grup.
- Distribusi F digunakan untuk menguji rasio antara dua variansi *(misalnya, variansi antar grup vs dalam grup)*.
- Distribusi F hanya bernilai positif dan berbentuk asimetris ke kanan

### 1.4. Distribusi t
- Distribusi t digunakan untuk membandingkan dua rata-rata populasi.
- Merupakan distribusi simetris, berbentuk seperti distribusi normal tetapi dengan ekor yang lebih tebal *(heavy-tailed)*.
- Semakin besar derajat kebebasan *(df)*, distribusi t akan semakin mendekati distribusi normal.
- Distribusi t memperhitungkan variansi sampel yang lebih kecil sehingga cocok untuk data dengan ukuran sampel kecil.

### 1.5. Distribusi t vs Distribusi F

![t_vs_f](/assets/t_vs_f.png)

| **Distribusi t**                          | **Distribusi F**                                    |
| ----------------------------------------- | --------------------------------------------------- |
| Digunakan untuk **menguji dua rata-rata** | Digunakan untuk **>2 grup** atau **rasio variansi** |
| Bentuk **simetris** seperti lonceng       | Bentuk **positif skewed** (asimetris kanan)         |
| Nilai bisa **negatif atau positif**       | Hanya bernilai **positif**                          |
| Dipengaruhi oleh **derajat bebas** (df)   | Dipengaruhi oleh dua df: df1 dan df2                |

### 1.6. P-Value dalam ANOVA

P-Value (nilai probabilitas) adalah peluang memperoleh hasil seperti yang diamati (atau lebih ekstrem) jika hipotesis nol (H₀) benar.

Dalam konteks ANOVA, P-Value mengukur seberapa besar kemungkinan bahwa perbedaan rata-rata antar grup terjadi secara kebetulan.

Interpretasi umum :
- Jika P-Value < 0.05 : Tolak H₀ → ada perbedaan yang signifikan secara statistik antar grup.
- Jika P-Value ≥ 0.05 : Gagal tolak H₀ → tidak cukup bukti untuk menyatakan ada perbedaan signifikan.

P-Value dihitung dari distribusi F berdasarkan F-statistic dan derajat kebebasan antar dan dalam grup.
Semakin kecil P-Value, semakin besar keyakinan bahwa perbedaan rata-rata yang diamati bukan karena kebetulan.

### 1.7. Jenis-Jenis ANOVA

**One-Way ANOVA**
ANOVA yang digunakan untuk menguji satu faktor atau variabel bebas *(independen)* terhadap satu variabel terikat *(dependen)*.
- Tujuan : Mengetahui apakah terdapat perbedaan rata-rata antar lebih dari dua grup dari satu faktor.
- Contoh : Menguji apakah rata-rata nilai mahasiswa berbeda antara jurusan A, B, dan C.
- Rumus :  
    ![anova_one_way](/assets/anova_one_way.png)

**Two-Way ANOVA (ANOVA Dua Arah)**
ANOVA yang digunakan untuk menguji dua faktor secara bersamaan, dan dapat menganalisis interaksi antar faktor.
- Tujuan : 
    Untuk mengetahui:
    - Apakah faktor A berpengaruh terhadap hasil?
    - Apakah faktor B berpengaruh terhadap hasil?
    - Apakah interaksi antara A dan B juga berpengaruh?

- Contoh : Menguji pengaruh jenis pupuk (A, B) dan jenis tanah (1, 2, 3) terhadap hasil panen.
- Rumus :  
    ![anova_two_way](/assets/anova_two_way.png)

**Repeated Measures ANOVA**
ANOVA yang digunakan ketika satu subjek diukur berulang kali dalam kondisi atau waktu yang berbeda.
- Tujuan : Mengukur perubahan hasil dari subjek yang sama dalam kondisi yang bervariasi.
- Contoh : Mengukur tekanan darah pasien sebelum, sesudah 1 minggu, dan setelah 1 bulan terapi.
- Karakteristik : Data saling tergantung (dependen) karena berasal dari subjek yang sama → tidak bisa pakai One-Way biasa.

## Materi 2 : Studi Kasus One-Way ANOVA

[Notebook Materi 2](/model/one_way/anova_one_way.ipynb)

## Materi 3 : Studi Kasus Two-Way ANOVA

[Notebook Materi 3](/model/two_way/anova_two_way.ipynb)

## Materi 4 : Pengujian Asumsi & Alternatif ANOVA

### 4.1. Pengujian Asumsi Sebelum ANOVA

Sebelum menerapkan ANOVA, pastikan beberapa asumsi berikut dipenuhi :

- **Normalitas Residual**

    Digunakan untuk memastikan bahwa sisa (residual) dari model terdistribusi normal.

    ```python
    from scipy import stats
    stats.shapiro(model.resid)
    ```

    Jika nilai p-value > 0.05 → Residual bisa dianggap normal.

- **Homogenitas Varians *(Levene Test)***

    Digunakan untuk menguji apakah varians antar grup setara.

    ```python
    stats.levene(df1, df2, df3)
    ```

    Jika p-value > 0.05 → varians antar grup dianggap homogen.

- **Visualisasi Residual**

    - Histogram : distribusi residual
    - QQ Plot : kesesuaian dengan distribusi normal
    - Residual vs Fitted : mengecek pola yang tidak normal

        ```py
        import matplotlib.pyplot as plt
        import seaborn as sns
        import statsmodels.api as sm

        # Histogram Residual
        sns.histplot(model.resid, kde=True)
        plt.title('Histogram of Residuals')
        plt.show()

        # QQ Plot
        sm.qqplot(model.resid, line='s')
        plt.title('QQ Plot of Residuals')
        plt.show()

        # Residual vs Fitted
        fitted = model.fittedvalues
        residual = model.resid
        sns.scatterplot(x=fitted, y=residual)
        plt.axhline(0, linestyle='--', color='red')
        plt.title('Residual vs Fitted Values')
        plt.xlabel('Fitted values')
        plt.ylabel('Residuals')
        plt.show()
        ```

### 4.2. Jika Asumsi Tidak Terpenuhi
Jika data tidak memenuhi asumsi normalitas atau homogenitas varians:

- Gunakan uji **non-parametrik** :
  - **One-Way ANOVA alternatif** : `Kruskal-Wallis Test`
  - **Two-Way ANOVA alternatif** : `Friedman Test`

- Lakukan **transformasi data** untuk menormalkan distribusi :
  - Logarithmic : `np.log(data)`
  - Square Root : `np.sqrt(data)`
  - Box-Cox (hanya untuk data > 0) : `scipy.stats.boxcox(data)`

### 4.3. Checklist Implementasi ANOVA
- [ ] Apakah data terdistribusi normal?
- [ ] Apakah grup memiliki variansi yang serupa?
- [ ] Apakah jumlah data tiap grup mencukupi? (idealnya ≥ 30)
- [ ] Apakah outlier telah ditangani?

### 4.4. Library Python
Untuk analisis ANOVA dan visualisasi :

- `pandas` : manipulasi dan pemrosesan data
- `seaborn` : visualisasi statistik
- `matplotlib` : plotting umum
- `statsmodels` : model statistik termasuk ANOVA
- `scipy` : pengujian statistik (Shapiro, Levene, dll)