# corona-virus-data-using-KNIME
Corona Virus Data Using KNIME


###Business Understanding
----------

Kemungkinan Proses yang dapat dilakukan pada data tersebut antara lain:
- penemuan jumlah kematian yang disebabkan virus corona berdasarkan negara atau region
- penemuan jumlah kematian yang disebabkan virus corona berdasarkan provinsi atau *state*
- penemuan jumlah orang yang teridentifikasi terkena virus corona berdasarkan negara atau *region*
- penemuan jumlah orang yang teridentifikasi terkena virus corona berdasarkan provinsi atau *state*
- dan masih banyak lagi 

###Data Understanding
----------

jumlah baris ada 1940, dan kolom yang terdapat pada data tersebut antara lain:
- **Province/State**: provinsi atau negara bagian
- **Country/Region**: negara atau wilayah
- **Last Update**: waktu Informasi terakhir
- **Confirmed**: jumlah orang yang sudah teridentifikasi virus corona
- **Suspected**: jumlah orang yang terduga terkena virus corona
- **Recovered**: jumlah orang yang telah sembuh dari virus corona
- **Death**: jumlah kematian yang disebabkan virus corona

###Data Preparation
----------

proses *spliting data* dilakukan untuk memisahkan data negara dari data corona virus. Proses ini dilakukan menggunakan script python yang dapat diakses pada repo saya di [https://github.com/metaufiq/split-data-big-data](https://github.com/metaufiq/split-data-big-data). hasil dari proses  *spliting data* tersebut terdapat pada folder [./output](https://github.com/metaufiq/split-data-big-data/tree/master/output).

###Modeling
----------

#####Proses Membaca Data
terdapat 2 proses membaca data disini yaitu:
- proses membaca data dari CSV
- proses membaca data dari Database MySQL
  
#####Membaca Data dari CSV
1.  Pilih CSV Reader dan *drag* ke project KNIME
   ![CSV Reader](./../documents/9.jpg)
2.  Klik kanan pada CSV Reader lalu tekan *Configure*  dan pilih file yang akan dibaca
3.  Klik kanan pada CSV Reader lalu tekan *Execute*

#####Membaca Data dari Database MySQL

1. Pilih DB Connector dan *drag* ke project KNIME
2. Klik kanan pada DB Connector lalu tekan *Configure*  dan atur koneksi database
3. Klik kanan pada DB Connector lalu tekan *Execute*
4. Pilih DB Table Selector dan *drag* ke project KNIME
5. Sambungkan DB Connector dan DB Table Selector
6. Klik kanan pada DB Table Selector lalu tekan *Configure*  dan pilih tabel yang akan dibaca
7. Klik kanan pada DB Table Selector lalu tekan *Execute*
8. Pilih DB Reader dan *drag* ke project KNIME
10. Sambungkan DB Table Selector dan DB Reader
11. Klik kanan pada DB Reader lalu tekan *Execute*
    
#####Proses Join

Tahap-tahap proses join data dari 2 sumber data yang berbeda(CSV dan MySQL) dijelaskan melalui langkah-langkah berikut:
1.  Pilih Joiner dan *drag* ke project KNIME
2. Sambungkan DB Reader dan CSV Reader yang telah kita buat pada **Proses Membaca Data** ke Joiner
3. Klik kanan pada Joiner lalu tekan *Configure* 
4. Pilih kolom yang akan menjadi acuan operasi *JOIN*
5. Buka tab *Column Selection* lalu pilih kolom yang akan menjadi hasil operasi *JOIN*
6. Klik kanan pada Joiner lalu tekan *Execute*


###Evaluation
----------
Untuk melihat hasil dari operasi join,  klik kanan pada Joiner lalu tekan *Joined Table* 

###Deployment
----------
#####Penambahan hasil Join ke Database MySQL
1.  Pilih DB Insert dan *drag* ke project KNIME
2. Sambungkan Joiner dan DB Insert
3.  Klik kanan pada DB Insert lalu tekan *Configure*  dan pilih tabel yang akan dimasukkan hasil dari operasi *JOIN*
4.  Klik kanan pada DB Insert lalu tekan *Execute*

#####Penambahan hasil Join ke CSV
1.  Pilih CSV Writer dan *drag* ke project KNIME
2. Sambungkan Joiner dan CSV Writer
3.  Klik kanan pada CSV Writer lalu tekan *Configure*  dan pilih lokasi file CSV  yang akan dimasukkan hasil dari operasi *JOIN*
4.  Klik kanan pada CSV Writer lalu tekan *Execute*