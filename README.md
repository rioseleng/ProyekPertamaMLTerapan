# Laporan Proyek Machine Learning - Rio Rezky Seleng

## Domain Proyek
Cuaca adalah suatu keadaan udara yang berada di atmosfer yang terjadi pada suatu tempat dan waktu tertentu dan sifatnya dapat berubah bergantung pada kondisi. Kondisi tersebut sangat bervariasi dan memiliki kecenderungan untuk saling berkaitan satu dengan yang lainnya. Cuaca yang tidak dapat terduga seperti cloudy, rainy, snowy, and sunny dapat berdampak pada kehidupan manusia baik pada keselamatan manusia bahkan dapat menyebabkan kondisi kerugian ekonomi. Oleh karena itu, kemampuan untuk mengklasifikasikan cuaca secara akurat menjadi sngat penting untuk mencegah dampak yang besar. Dengan menggunakan data historis dan teknik machine learning, kita dapat mengembangkan model klasifikasi cuaca yang efektif yang dapat membantu dalam memprediksi kondisi cuaca dan langkah-langkah yang perlu dipersiapkan untuk meminimalisir dampak negatif yang dapat ditimbulkan.
## Business Understanding
### Problem Statements : Ketidakpastian kondisi cuaca.
Ketidakpastian klasifikasi kondisi cuaca saat ini dapat menghambat pengambilan keputusan yangn tepat dan efektif oleh masyarakat yang berkegiatan pada sektor-sektor yang begantung pada informasi cuaca. Oleh karena itu, dengan adanya sistem klasifikasi cuaca berdasarkan beberapa kondisi yang dapat diobservasi oleh masyarakat umum diharapkan mereka dapat meminimalisir dampak negatif yang akan ditimbulkan oleh cuaca buruk apabila hasil prediksi menghasilkan hal tersebut.
### Goals : Mengurangi ketidakpastian dan resiko
Ketika model machine learning untuk klasifikasi ini telah dibuat, diharapkan bahwa model ini dapat membantu masyarakat untuk mengurangi ketidakpastian dalam informasi cuaca dan mengurangi risiko yang terkait dalam keputusan yang didasarkan pada kondisi cuaca yang tidak akurat.
### Problem Statements
Pada implementasi model machine learning kali ini, saya akan menggunakan dua algoritma klasifikasi yang populer digunakan: KNN(K-Nearest Neighbors) dan SVM(Support Vector Machine) dan pada akhirnya akan dipilih satu model dengan akurasi terbaik setelah dilakukan proses evaluasi menggunakan metrik evaluasi.
## Data Understanding
Jumlah data yang digunakan pada saat ini ada 13200 records dengan 10 column independen dan 1 column dependen atau label data.\
Data yang digunakan diunduh dari [Kaggle](https://www.kaggle.com/datasets/nikhil7280/weather-type-classification). Penjelasan tentang 10 variable independent dan 1 variable dependent adalah sebagai berikut:
- Temperature: Variable ini bertipe data **float** dan digunakan untuk menyimpan data suhu yang diukur dengan satuan derajat celcius. Suhu yang diukur berada pada rentan *extreme cold* hingga *extreme heat*
- Humidity: Variable ini disimpan menggunakan tipe data **integer** dan variabel ini digunakan untuk menyimpan persentasi kelembapan udara termasuk nilai di atas 100% untuk memperkenalkan outlier pada pengguna dataset
- Wind speed: Variabel ini disimpan menggunakan tipe data **float** dan digunakan untuk menyimpan kecepatan angin dalam satuan kilometer per jam dengan rentang nilai yang sangat tinggi
- Precipitation: Variable ini disimpan menggunakan tipe data **float** dan digunakan untuk menyimpan persentase curah hujan dan di dalam data ini terdapat nilai outlier
- Cloud cover: Variable ini disimpan menggunakan tipe data **object** dan digunakan untuk menyimpan kondisi awan
- Atmospheric pressure: Variable ini disimpan menggunakan tipe data **float** dan digunakan untuk menyimpan data tekanan atmosfer dalam satuan hPa. Data ini mencakup rentang yang cukup besar
- UV Index: Variabel ini disimpan menggunakan tipe data **integer** dan digunakan untuk menyimpan data kekuatan radiasi ultraviolet.
- Season: Varibel ini disimpan menggunakan tipe data **object** dan digunakan untuk menyimpan data musim saat data dicatat
- Visibility: Variable ini disimpan menggunakan tipe data **float** dan digunakan untuk menyimpan data visibilitas dalam satuan kilometer termasuk data yang sangat rendah atau sangat tinggi.
- Location: Tipe data yang digunakan untuk menyimpan variable ini adalah **object**. Variable ini digunakan untuk menyimpan tipe lokasi di mana data dicatat atau diobservasi.
- Weather type: **Object** adalah tipe data yang digunakan untuk menyimpan variable ini. Variabel ini digunakan untuk menyimpan dependent variable yang mendindikasikan tipe cuaca. Tipe cuaca yang diobservasi adalah cloudy, rainy, snowy, dan sunny.
## Data Preparation
Pada tahap preparation, saya melakukan beberapa teknik untuk mempersiapkan data\ (dataoutlier,standarscaler,spliting,labelencoder)
1. Outlier Detection\
   Outlier detection adalah salah satu teknik yang digunakan untuk mempersiapkan data sebelum dilakukan pemodelan. Metode yang saya gunakan untuk mendeteksi outlier adalah *Interquartile Range(IQR)*.IQR bekerja dengan        menentukan Q1, Median, dan Q3.
   - Q1 merepresntasikan 25% percentile dari data
   - Median merepresentasikan 50% percentile dari data
   - Q3 merepresentasikan 75% percentile dari data
   IQR berada pada rentang Q1 dan Q3. IQR = Q3-Q1. Data yang berada di bawah Q1-1.5xIQR atau di atas Q3+1.5xIQR adalah outlier
2. Standard Scaler\
   Standard Scaler adalah metode normalisasi data yang digunakan dalam machine learning untuk memastikan bahwa setiap fitur dalam dataset memiliki skala yang sama, khususnya dengan rata-rata (mean) 0 dan standar deviasi (standard deviation) 1. Metode ini saya gunakan karena outlier yang ditemukan lebih dari 10% dan tidak memungkinkan untuk meghapus outlier tersebut karena dapat menghilangkan integritas dari data. Dengan menggunakan Standard Scaler, kita dapat memastikan bahwa model machine learning bekerja lebih efektif dan efisien, karena data berada dalam skala yang konsisten
3. Label Encoder\
   Komputer hanya dapat mengenali data dalam bentuk numerikal. Oleh karena itu, saya mengubah variabel yang disimpan dengan tipe data object menjadi numerikal menggunakan label encoder yang disediakan oleh library scikitlearn. Label Encoder adalah teknik dalam machine learning yang digunakan untuk mengubah data kategorikal menjadi data numerik
4. Splitting\
   Splitting dataset adalah salah satu metode yang digunakan dalam persiapan data sebelum dilakukan pemodelan machine learning. Pada percobaan kali ini, saya membagi data menjadi training dataset dan juga test dataset menggunakan library scikitlearn. Training data digunakan untuk melatih model dan training data digunakan untuk mengukur akurasi model.
## Modelling
Pada percobaan ini, saya menggunakan algoritma KNN(K-Nearest Neighbors) dan SVM(Support Vector Machine).
1. KNN(K-Nearest Neighbors)\
  Algoritma K-Nearest Neighbors (KNN) adalah metode machine learning untuk klasifikasi dan regresi yang mengandalkan jarak antara data baru dan data pelatihan, biasanya menggunakan jarak Euclidean. Algoritma ini     menentukan kelas atau nilai data baru berdasarkan mayoritas atau rata-rata dari K tetangga terdekat. Meskipun KNN mudah dipahami dan diimplementasikan, ia memiliki kekurangan seperti kinerja lambat pada dataset besar, sensitif terhadap data yang tidak relevan atau noise, dan masalah pada data dengan dimensi tinggi. Pemilihan nilai K yang tepat dan normalisasi data sangat penting untuk mengoptimalkan performa KNN.
2. SVM(Support Vector Machine)\
   Support Vector Machine (SVM) adalah algoritma machine learning yang digunakan untuk klasifikasi dan regresi dengan mencari hyperplane optimal yang memisahkan data dari berbagai kelas dengan margin maksimal. SVM bekerja dengan menemukan support vectors, yaitu titik-titik data yang berada paling dekat dengan hyperplane pembatas, untuk memaksimalkan margin antara kelas-kelas tersebut.

Pada percobaan ini, model dengan performa terbaik adalah model Support Vector Machine karena memiliki akurasi 90% dibandingkan dengan model KNN dengan akurasi 89%. Meskipun demikian, kedua algoritma ini dapat dikatakan memiliki kualitas yang baik karena memiliki nilai akurasi yang tinggi
## Evaluation
Pada pemodelan saat ini, saya menggunakan accuracy metrics, precission, recall, dan F1-Score.
- Accuracy metrics adalah sebuah ukuran yang digunakan untuk menilai kinerja model machine learning dengan membandingkan prediksinya dengan hasil yang sebenarnya. Metriks ini sangat penting untuk menentukan seberapa baik sebuah model dapat digeneralisasi pada data yang belum pernah dilihatnya
- Precission adalah sebuah rasio prediktif benar positif dengan keseluruhan hasil yang diprediksi positif
- Recall(sensitifitas) adalah rasio prediksi benar positif dibandingkan dengan keseluruhan data yang benar positif
- F1 score adalah perbandingan antara rata-rata presisi dengan recall yang dibobotkan.
