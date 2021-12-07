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

Derste anlatılan diğer konular haftaya daha ayrıntılı işlendi.

---

[<< Geri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta6.md)

[>> İleri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta8.md)
