# Biyoinformatik Algoritmalara Giriş
## Hafta 7

### The Change Problem - Bozuk Para Problemi: Recurrence
http://www.cs.bilkent.edu.tr/~calkan/teaching/cs481/pdfslides/06-alignment-lcs.pdf

Hedefimiz mümkün olan en az sayıda madeni para kullanarak, bir miktar parayı temsil etmek.

Elimizde 1, 3 ve 5 kuruş var. 

1'den 10'a kadarki kuruşları minimum kaç madeni para kullanarak temsil edebiliriz?

![image](https://user-images.githubusercontent.com/12685802/144930893-5124efc8-02bb-4682-9ea2-d206eca4b957.png)

1, 3 ve 5 kuruşları 1 madeni para kullanarak temsil edebiliriz. Tablomuza yazalım.

![image](https://user-images.githubusercontent.com/12685802/144930994-30656422-cf52-400a-af76-3634a1c34db7.png)

Tablomuzda olan kuruşların yanındaki kuruşları 1'er kuruş ekleyerek daha temsil edebileceğimiz için (mesela 2 kuruşu 1 kuruş + 1 kuruş olarak temsil edebiliriz) tablodaki değerlerine 2 yazıyoruz.

Bu işlemi aynı zamanda 3'er ve 5'er kuruş ekleyerek de hesaplayadıklarımıza da işleyelim.

- 2 = 1,1 (aslında 1, üstüne 1)
- 4 = 3,1 (aslında 3, üstüne 1)
- 6 = 5,1 ya da 3,3 (aslında 5, üstüne 1 ya da 3 üstüne 3)
- 8 = 5,3 (aslında 5, üstüne 3)
- 10 = 5,5 (aslında 5, üstüne 5)

![image](https://user-images.githubusercontent.com/12685802/144931135-cf2d2d15-56ba-4654-a7f8-e9273ed85dd9.png)

Tekrar tabloların boş olan kısımlarına erişmeye çalışalım.

- 3 = 1,1,1 (aslında 2, üstüne 1)
- 7 = 5,1,1 (aslında 6, üstüne 1)
- 9 = 5,3,1 (aslında 8, üstüne 1)

![image](https://user-images.githubusercontent.com/12685802/144932003-d95e30ab-c41c-4a88-a125-f88145fb3572.png)

Bu işlemler aslında şu recurrence ilişkisinden sonuçlanır:

![image](https://user-images.githubusercontent.com/12685802/144932089-5de9057c-2691-4439-8434-0845b727529d.png)

Ama bu işlem yeterince verimli değildir. Çünkü çok fazla tekrar içerir.

Mesela 77'den 1'e hesaplama yaparsak ağacın ilk kısımlarında bile 70'i defalarca hesaplamak zorunda kalırız.

![image](https://user-images.githubusercontent.com/12685802/144932366-b4988fa1-a565-4538-b124-95887ab875c6.png)

Daha iyisini yapmak için sonuçları kaydedebiliriz.

### The Change Problem - Bozuk Para Problemi: Dynamic Programming

![image](https://user-images.githubusercontent.com/12685802/144933032-24c6a19a-7a85-4fd6-b94f-9c7a8ac9a010.png)

Basamaklar adım adım hesaplanır, hafıza vardır böylece veri tekrarı önlenir.

---

### Manhattan Tourist Problem - Manhattan Turist Problemi (MTP)

![image](https://user-images.githubusercontent.com/12685802/144933524-c0008e17-1c3e-49b4-a2ac-15a076b6744f.png)

Kaynaktan varış noktasına kadar maksimum atraksiyon (*) yaşayarak hangi yoldan gidebiliriz?

Yukarıdaki örnekte 5 atraksiyon yaşanmış. Alttaki örnekte ise 7 tane, hesaplama nasıl yapılır?

![image](https://user-images.githubusercontent.com/12685802/144933750-d82fd0d3-a077-4b36-b788-096f4a449b94.png)

Kırmızı işaretli yol, greedy (aç gözlü) algoritmasıyla hesaplanmıştır. Bu algoritma iki karar arasında en yüksek olanı seçerek toplam yol yerine anlık karar veren bir algoritmadır.

Mavi işaretli ise kırmızı işaretliden daha iyi bir yoldur. Greedy algoritmasının işlevsizliğini göstermektedir.

![image](https://user-images.githubusercontent.com/12685802/144933863-16e10f96-cb6f-4b2f-9b91-bb86afbb4225.png)

İyi yolu hesaplama iki seçenekli durumda şöyle yapılır:

![image](https://user-images.githubusercontent.com/12685802/144934436-0cf995f0-a633-4535-a16c-89c9fdb300a4.png)

![image](https://user-images.githubusercontent.com/12685802/144934514-d5839da0-2ce9-4ab8-9c77-85340cbb8e77.png)

![image](https://user-images.githubusercontent.com/12685802/144934567-dbfa747e-58d7-456c-a589-8638cb6bd4b4.png)

Ama diagoneller yani çarpaz durumlar olursa ne olucak? Aslında çok basit, duruma bir koşul daha eklenir.

![image](https://user-images.githubusercontent.com/12685802/144934636-8dc2910d-80d2-437c-9a9b-db1a42c7b931.png)

---

### Longest Common Subsequence (LCS)

![image](https://user-images.githubusercontent.com/12685802/144935187-fa01d558-9c82-4753-bac1-2ef5be1333eb.png)

Maksimum eşleşmeyi sağlayabilmek için dinamik programlamayı kullanabiliriz.

#### Longest common subsequence problem as MTP

![image](https://user-images.githubusercontent.com/12685802/144935248-58015a35-eee9-44b7-9588-d8ee430e51c0.png)

#### Edit Graph for LCS problem

![image](https://user-images.githubusercontent.com/12685802/144935357-b2781a8f-94f0-4cb0-8799-f58158f32a0e.png)

Eğer satır ve sütunlarda taranan karakterler aynı ise diagonel kullanılabilir.

![image](https://user-images.githubusercontent.com/12685802/144935641-1aead100-131a-4b09-9f45-47602ebab3f1.png)

Diagoneller eşleşme işaretini, yatay hareketler ilk metinde (v) (satırdaki karakterler) boşluk atılmasını, dik hareketler ikinci metinde (w) (sütundaki karakterler) boşluk atılmasını gösterir. 

![image](https://user-images.githubusercontent.com/12685802/144935792-5ed18175-7786-4862-b54e-6693c7681aa9.png)

Böylece maksimum eşleşmeyi (3) sağladık. 

---

### Distance Between Strings - Metinler Arası Fark

Şu şekilde iki sekans verildi diyelim, normalde aralarındaki fark çok azken Hamming distance 8'dir.

![image](https://user-images.githubusercontent.com/12685802/144936211-dbcda6ac-2072-47a6-b560-ac2a9837aaf1.png)

Her bir sekans bir karakter shiftlenince durum:

Hamming distance, DNA'daki eklemeleri ve silmeleri ihmal eder.

![image](https://user-images.githubusercontent.com/12685802/144936373-bb960b01-d8f4-4840-b5a5-1b7b4599560a.png)

#### Edit Distance

Levenshtein (1966), iki dizi arasındaki düzenleme mesafesini, bir diziyi diğerine dönüştürmek için minimum sayıda temel işlem (ekleme, silme ve değiştirme) olarak tanımladı.

#### Hamming Distance

Hamming distance sadece iki metnin i. karakteriyle i. karakterleri arasındaki farkı söyler.

![image](https://user-images.githubusercontent.com/12685802/144936952-910511e9-648f-4bc5-be77-05c1065c87b3.png)

#### Hamming Distance vs Edit Distance

![image](https://user-images.githubusercontent.com/12685802/144937086-c9e71b43-494b-4e3d-9575-7b4d1b61585e.png)

#### Edit Distance Örnek

![image](https://user-images.githubusercontent.com/12685802/144937299-7f3f372f-4d72-4565-b943-6d6a705cb200.png)


---

[<< Geri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta6.md)

[>> İleri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta8.md)
