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
## Descriptive Statistics
Terdapat beberapa point yang didapat:
- Kolom employee count hanya bernilai 1 pada semua data,
- Kolom employee number masing-masing row bernilai unik,
- Kolom StandardHour juga hanya memiliki value 80,
- Kolom over18 hanya memiliki value 'yes', jadi tidak akan berguna dalam model dan akan dihapus 
- Dataset tidak memiliki Duplicate Value dan Missing Value

## Univariate Analysis
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

## Multivariate Analysis

Pada kolom TotalWorkingYears, YearsAtCompany dan YearsInCurrentRole memiliki korelasi dengan kolom lain > 0.7 sehingga bisa menyebabkan multikolinearity, oleh karena itu kolom ini akan di hapus
![image](https://user-images.githubusercontent.com/98078080/204129045-10c22bfb-bb14-4f5a-a1a2-72d6ebf58653.png)

## Business Insight
![image](https://user-images.githubusercontent.com/98078080/204129084-ef6d2cfb-53ca-4645-ae20-5f85c32b6e7a.png)

- Kayawan yang melakukan Overtime cenderung lebih banyak yang Attrition daripada yang tidak, rekomendasi berdasarkan Insight ini adalah mengimbau karyawan supaya tidak melakukan Overtime dan membereskan pekerjaan sesuai jadwal.
- Karyawan yang memiliki Performance Rating 3 cenderung Attrition, rekomendasi berdasarkan insight ini adalah megoptimalkan performa karyawan dengan memberikan apresiasi atas prestasi yang telah dicapai selama bekerja, bisa dengan memberikan bonus supaya karyawan lebih semangat dalam bekerja
- JobRole seperti Sales Executive, Sales Representative, Laboratory Technician dan Research Scientist banyak terjadi Attrition, rekomendasi dari insight ini adalah pada list JobRole tersebut bisa diadakan evaluasi lebih lanjut mengenai kepuasan dan tingkat stress serta tekanan yang didapat oleh karyawan.

