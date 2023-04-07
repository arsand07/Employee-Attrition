# Employee-Attrition
## Stage 0 : Problem Statement
1. Problem Statement
Jumlah attrition rate mencapai 16.12%. hal tersebut melebihi batas ideal attrition rate yaitu 10%. mengakibatkan kinerja perusahaan menurun dikarenakan karyawan yang memiliki kinerja yang baik berpotensi meninggalkan perusahaan dan meningkatkan pengeluaran perusahaan dalam rekrutmen karyawan baru. Sehingga, project perusahaan yang berkaitan dengan mantan karyawan tertunda, sehingga dapat mempengaruhi timeline yang dapat berdampak langsung pada reputasi perusahaan terhadap konsumen ataupun partner perusahaan.
2. Objective
__membuat model machine learning untuk memprediksi karyawan yang berpotensi untuk resign__. jadi diharapkan dari model ini tingkat attrition dapat mencapai dibawah 10%. action item yang dapat digunakan untuk mengurangi tingkat attrition rate adalah : 
- mengapresiasi kinerja karyawan
- Gaji dan Fasilitas yang Kompetitif
- Jam Kerja yang Seimbang dan Jobdesk yang rasional
- Menyusun Strategi Engagement Karyawan
- menawarkan dan memberikan tunjangan lain yang menarik
- mengadakan acara kumpul Bersama dan olahraga Bersama
- memberikan kesempatan untuk berkembang
3. Goals
- menurunkan persentase attrition rate
- Memprediksi potensi karyawan yang akan resign
4. Business Metrics
- Attrition Rate

## Stage 1: EDA(Explanatory Data Analysis) Employee-Attrition
### Descriptive Statistics
Terdapat beberapa point yang didapat:
- Kolom employee count hanya bernilai 1 pada semua data,
- Kolom employee number masing-masing row bernilai unik,
- Kolom StandardHour juga hanya memiliki value 80,
- Kolom over18 hanya memiliki value 'yes', jadi tidak akan berguna dalam model dan akan dihapus 
- Dataset tidak memiliki Duplicate Value dan Missing Value

### Univariate Analysis
![image](https://user-images.githubusercontent.com/98078080/204129056-67bd545a-c1cc-48dd-9070-d2cc2aee23ba.png)

Numerikal
- Usia terbanyak ada di kisaran 30-40 tahun
- Banyak karyawan yang jarak rumah ke kantor cukup dekat
- Monthly income karyawan berpusat di angka 3000 - 5000, sementara daily rate, hourly rate dan monthly rate cenderung menyebar
- Kebanyakan karyawan hanya bekerja dalam 1 company
- Persentase kenaikan gaji paling tinggi berkisar di angka 0-15%
- Total tahun bekerja paling banyak berada di angka 3 - 10 Tahun
- Total training terbanyak adalah 2-3 kali dalam tahun lalu
- Total bekerja pada company kebanyakan 0-10 tahun
- Banyak karyawan yang baru saja mendapat kenaikan jabatan

Kategorikal
- Attrition rate pada company ini cenderung tinggi (>10%) yakni 16% Source
- Karyawan pada company ini kebanyakan jarang melakukan travelling
- Kebanyakan karyawan berada pada department Research & Development dan sangat sedikit pada department HR
- Tingkat pendidikan karyawan didominasi oleh S1 (Sarjana)
- Bidang pendidikan didominasi oleh Life Science, dan paling sedikit di bidang HR
- Ada indikasi ketidakpuasan terhadap lingkungan kerja
- Tingkat keterlibatan kerja karwan kebanyakan berada di level high

### Multivariate Analysis

Pada kolom TotalWorkingYears, YearsAtCompany dan YearsInCurrentRole memiliki korelasi dengan kolom lain > 0.7 sehingga bisa menyebabkan multikolinearity, oleh karena itu kolom ini akan di hapus
![image](https://user-images.githubusercontent.com/98078080/204129045-10c22bfb-bb14-4f5a-a1a2-72d6ebf58653.png)

### Business Insight
![image](https://user-images.githubusercontent.com/98078080/204129084-ef6d2cfb-53ca-4645-ae20-5f85c32b6e7a.png)

- Kayawan yang melakukan Overtime cenderung lebih banyak yang Attrition daripada yang tidak, rekomendasi berdasarkan Insight ini adalah mengimbau karyawan supaya tidak melakukan Overtime dan membereskan pekerjaan sesuai jadwal.
- Karyawan yang memiliki Performance Rating 3 cenderung Attrition, rekomendasi berdasarkan insight ini adalah megoptimalkan performa karyawan dengan memberikan apresiasi atas prestasi yang telah dicapai selama bekerja, bisa dengan memberikan bonus supaya karyawan lebih semangat dalam bekerja
- JobRole seperti Sales Executive, Sales Representative, Laboratory Technician dan Research Scientist banyak terjadi Attrition, rekomendasi dari insight ini adalah pada list JobRole tersebut bisa diadakan evaluasi lebih lanjut mengenai kepuasan dan tingkat stress serta tekanan yang didapat oleh karyawan.

## Stage 2 : Data Pre-Processing
### Data Cleaning
a. Missing Value
Dataset ini tidak memiliki missing value, sehingga tidak perlu dilakukan penanganan
b. Duplicated Data
Dataset ini tidak memiliki Duplicated Data
c. Handle Outliers
Karena outlier mencapai 35.71% dari total data, maka kami melakukan replace value dengan median
![image](https://user-images.githubusercontent.com/98078080/230534685-46e00f14-4631-4a7e-9f78-9e54726631ee.png)
![image](https://user-images.githubusercontent.com/98078080/230534966-92fd509e-4dce-4254-988c-10918f8d42e1.png)
d. Feature Transformation
Karena semua kolom tidak memiliki distribusi normal, maka data discaling menggunakan normalisasi. Dalam menentukan distribusi data, kita menggunakan pengujian `Sharpio`
e. Feature Encoding
Kolom kategorical yg memiliki unique value 2 dan bertipe ordinal akan menggunakan Label Encoding, sementara yang bertipe nominal akan menggunakan one hot encoding 
	- Kolom `EducationField`, `JobRole`, `BusinessTravel`.`Department`,`MaritalStatus` akan 	menggunakan OneHots encoding 
	- Kolom  `Attrition`, `Gender`, `Overtime` akan menggugnakan label encoding
f. Handle class imbalance
Pada dataset ini kolom Attrition memiliki perbandingan 16:84. Menurut sumber 16% termasuk dalam kategori moderate. Oleh karena itu kita akan melakukan balancing data dengan menggunakan oversampling `SMOTE`

### Feature Engineering
a. Feature selection (membuang feature yang kurang relevan atau redundan) 
Pada tahap ini kami akan membuang salah satu kolom yang memiliki korelasi > 0.7 yang kemungkinan akan redundan dan menyebabkan multikolinearity. `PercentSallaryHike`, `JobRole_Human Resources`, `JobRole_Sales Executive`, `Department_Sales` adalah kolom yang berkorelasi lebih dari 0.7 dengan kolom lain dan akan di drop
b. Feature extraction (membuat feature baru dari feature yang sudah ada)
Tidak ada Feature baru yang ditambahkan, data yang dimiliki dirasa cukup untuk melakukan Model
* Feature Tambahan:
`Stress Level` akan sangat membantu ketika mengetahui tingkat stress karyawan dalam melakukan pekerjaan, sehingga kita bisa paham, apakah perusahaan ini memiliki tingkat stress yang tinggi atau tidak
`Health` alasan kesehatan biasanya menjadi salah satu faktor pergi atau tidaknya seorang karyawan
`Companyinfrastructure` biasanya hal ini juga jadi pertimbangan karyawan untuk menetap atau pindah kantor
`Appreciation` kadang hal seperti apresiasi menajdi hal yang membuat betah di suatu lingkungan. 

## Stage 3 : Modeling and Evaluation
Hasil dari proses eksperimen menggunakan beberapa skenario dan jenis model, kami mendapatkan hasil akhir model dengan performa terbaik. XGBoost yang telah dilakukan Hyperparameter Tunning memberikan hasil terbaik diantara model lainnya.
### XGBoost: Modeling and Evaluation
ROC-AUC dipilih sebagai matriks evaluasi ntuk mengetahui sejauh mana model klasifikasi memisahkan pengunjung mana yang diprediksi membeli dan tidak. Metrik ROU-AUC ini diplot dengan dua matriks yang dibandingkan satu sama lain yaitu TPR (True Positive Rate atau Recall) dan FPR (False Positive Rate).
![image](https://user-images.githubusercontent.com/98078080/230536094-e99ed2df-920c-48a6-a72a-d64ad12e6d2d.png)
![image](https://user-images.githubusercontent.com/98078080/230536185-13dcad33-1590-4e3b-b1b6-5759437a9630.png)

### XGBoost: Feature Importance
Untuk mengetahui Feature yang memiliki pengaruh terhadap model yang kita buat, dilakukan analisis menggunakan `Shap` untuk mengetahui Feature important yang berpengaruh terhadap model yang kita build
![image](https://user-images.githubusercontent.com/98078080/230536424-975ab4f7-fa87-4470-be49-9d1b61b05862.png)
- 3 Feature yang memiliki pengaruh terbesar adalah : `YearWithCurrentManager`, `JobLevel`, dan `OverTime`
- Nilai `Shap` yang ada pada grafik tersebut bernilai absolut, jadi baik itu memiliki pengaruh positif atau negatif tidak akan diketahui.
oleh karena itu, kita bisa melihat jenis pengaruhnya dengan menggunakan grafik `Shap Tree Explainer`
![image](https://user-images.githubusercontent.com/98078080/230536756-ea60da7c-08e9-4e4e-a870-77dd505cb8b0.png)
- ternyata `YearWithCurrentManager` dominan berada pada nilai negatif, artinya banyak karyawan yang resign dengan waktu dengan manager yang masih sebentar
- `JobLevel` yang tinggi cenderung tidak resign
- karyawan yang sering `OverTime` cenderung resign

## Stage 4: Business Recomendation
![image](https://user-images.githubusercontent.com/98078080/230537706-2726842d-d8bf-4ddd-b63d-47e13c9a4a7c.png)
![image](https://user-images.githubusercontent.com/98078080/230537811-599acd2c-882b-497c-a187-201d58219ca4.png)
![image](https://user-images.githubusercontent.com/98078080/230537846-86528a68-1095-48d4-94a8-4f98fec185f0.png)
![image](https://user-images.githubusercontent.com/98078080/230537894-f25fdf69-36c0-46e9-aeed-02a3d74b34c5.png)

Dengan memberikan treatment yang tepat kepada employee, diharapkan tingkat Employee Attrition dapat menurun dan seimbang berada di tingkat yang ideal. 
Akan tetapi, banyak faktor-faktor eksternal lainnya yang membuat Employee pergi dari suatu perusahaan, terlepas dari faktor internal perusahaan.
Malik, 2020












