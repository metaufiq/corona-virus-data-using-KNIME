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
   ![CSV Reader](/documents/1.jpg)
2.  Klik kanan pada CSV Reader lalu tekan *Configure*  dan pilih file yang akan dibaca
   ![CSV Reader Configure](/documents/2.jpg) 
3.  Klik kanan pada CSV Reader lalu tekan *Execute*
    ![CSV Reader Execute](/documents/3.jpg) 

#####Membaca Data dari Database MySQL

1. Pilih DB Connector dan *drag* ke project KNIME
   ![DB Connector](/documents/4.jpg) 
2. Klik kanan pada DB Connector lalu tekan *Configure*  dan atur koneksi database
   ![DB Connector Configure](/documents/5.jpg) 
3. Klik kanan pada DB Connector lalu tekan *Execute*
   ![DB Connector Execute](/documents/6.jpg) 
4. Pilih DB Table Selector dan *drag* ke project KNIME
   ![DB Table Selector](/documents/7.jpg) 
5. Sambungkan DB Connector dan DB Table Selector
   ![DB Connector dan DB Table Selector](/documents/8.jpg) 
6. Klik kanan pada DB Table Selector lalu tekan *Configure*  dan pilih tabel yang akan dibaca
   ![DB Table Selector Configure](/documents/9.jpg) 
7. Klik kanan pada DB Table Selector lalu tekan *Execute*
   ![DB Table Selector Execute](/documents/10.jpg) 
8. Pilih DB Reader dan *drag* ke project KNIME
   ![DB Reader](/documents/11.jpg) 
9.  Sambungkan DB Table Selector dan DB Reader
    ![DB Table Selector dan DB Reader](/documents/12.jpg) 
10. Klik kanan pada DB Reader lalu tekan *Execute*
    ![DB Reader Execute](/documents/13.jpg) 
    
#####Proses Join

Tahap-tahap proses join data dari 2 sumber data yang berbeda(CSV dan MySQL) dijelaskan melalui langkah-langkah berikut:
1.  Pilih Joiner dan *drag* ke project KNIME
   ![Joiner](/documents/14.jpg) 
2. Sambungkan DB Reader dan CSV Reader yang telah kita buat pada **Proses Membaca Data** ke Joiner
   ![DB Reader dan CSV Reader](/documents/15.jpg) 
3. Klik kanan pada Joiner lalu tekan *Configure* 
   ![Joiner Configure](/documents/16.jpg) 
4. Pilih kolom yang akan menjadi acuan operasi *JOIN*
   ![Kolom yang terpilih](/documents/17.jpg) 
5. Buka tab *Column Selection* lalu pilih kolom yang akan menjadi hasil operasi *JOIN*
   ![Column Selection dan Join](/documents/18.jpg) 
6. Klik kanan pada Joiner lalu tekan *Execute*
   ![Joiner Execute](/documents/19.jpg) 


###Evaluation
----------
Untuk melihat hasil dari operasi join,  klik kanan pada Joiner lalu tekan *Joined Table* 
![Joined Table](/documents/20.jpg) 

###Deployment
----------
#####Penambahan hasil Join ke Database MySQL
1.  Pilih DB Insert dan *drag* ke project KNIME
   ![DB Insert](/documents/21.jpg) 
2. Sambungkan Joiner dan DB connector ke DB Insert
   ![Joiner dan DB Connector ke DB Insert](/documents/22.jpg) 
3.  Klik kanan pada DB Insert lalu tekan *Configure*  dan pilih tabel yang akan dimasukkan hasil dari operasi *JOIN*
   ![DB Insert Configure](/documents/23.jpg) 
4.  Klik kanan pada DB Insert lalu tekan *Execute*
   ![DB Insert Execute](/documents/24.jpg) 

#####Penambahan hasil Join ke CSV
1.  Pilih CSV Writer dan *drag* ke project KNIME
   ![CSV Writer](/documents/25.jpg) 
2. Sambungkan Joiner dan CSV Writer
   ![Joiner dan CSV Writer](/documents/26.jpg) 
3.  Klik kanan pada CSV Writer lalu tekan *Configure*  dan pilih lokasi file CSV  yang akan dimasukkan hasil dari operasi *JOIN*
   ![CSV Writer Configure](/documents/27.jpg) 
4.  Klik kanan pada CSV Writer lalu tekan *Execute*
   ![CSV Writer Execute](/documents/28.jpg) 