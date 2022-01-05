# Biyoinformatik Algoritmalara Giriş
## Hafta 11

### NP-Hard vs NP-Complete

#### NP-Hard

Çoklu hizalama probleminde hücre hesabında 2^n-1 işlem yapılacak.

2 sekans hizalarken 3 hücre bilgisine bakılır. Kaç hücre için bu tekrarlanır? n^2 hücre

3 sekans hizalarken 7 hücre bilgisine bakılır. Kaç hücre için bu tekrarlanır? n^3 hücre

Hesap zamanımız O(2^n) olacak. Bu tür problemlere **NP-HARD** denir.

#### NP-Complete

Zaten tanımlı olan NP-Complete problemler var, bu tanımlılara indirgeyebiliyorsak (dönüştürebiliyorsak) problemimize **NP-Complete** tür problem denir.
 
### Yapay Zeka'nın Temel Prensipleri

#### Makine Öğrenmesi (Yapay Öğrenme): 

Elimizdeki veriden öğrenme işlemi.

İstatistiksel araçlardan faydalanmalıyız.
 
### Randomized QuickSort

c = {6, 3, 2, 8, 4, 5, 1, 7, 0, 9}

- Adım 1: İlk önce bir pivot (m) seçilir (doğal durumda listenin ilk elemanı seçilir)
  - m = 6
- Adım 2: Pivottan küçük ve büyük olanları csmall ve clarge olarak ikiye ayırır.
  - csmall = {3,2,4,5,1,0}, clarge= {8, 7, 9}
- Adım 3: csmall kendi içinde, clarge kendi içinde özyinelemeli olarak tekrar QuickSort işlemine tâbi tutulur.
  - ![image](https://user-images.githubusercontent.com/12685802/148225712-9458d962-010d-478a-afa2-3b43024dde9d.png)

Tek eleman kaldığı zaman işlem biter.

Peki pivot seçiminde ilk karakteri almak ne kadar doğru? 

Pivotu listenin içinden rastgele bir seçim ile belirlersek en iyi seçimi yapamayabiliriz ama en kötü seçimi yapmaktan korur. Ve bu durum QuickSort'un en iyi durumunu verir.

Sekanslarda motif bulurken de rastgelelikten fayda sağlayabilir miyiz? 

### Gibbs Sampling ile Motif Bulma

Elimizde sekanslara ait şöyle bir profil olsa:

![image](https://user-images.githubusercontent.com/12685802/148226931-53de8c24-26c0-4afe-9012-e627e6a94f24.png)

P profiline göre AAACCT'nin oluşma olasılığı nedir:

![image](https://user-images.githubusercontent.com/12685802/148227012-3aab0810-6621-471b-bd9d-380df5d6b71a.png)

Pr(AAACCT | P) = 1/2 * 7/8 * 3/8 * 5/8 * 3/8 * 7/8 = 0.033646 ~= %3.36

Pr(ATACAG | P) = 1/2 * 1/8 * 3/8 * 5/8 * 1/8 * 1/8 = 0.001602 ~= %0.16

Peki elimizde `CTATAAACCTTACATC` gibi bir sekans varsa, P'nin gelme olasılığının muhtemel yer (? :D) - P-Most Probable 6-mer değeri nedir? Bunu bulmak için parçalara böleriz: (P profili 6 uzunluğundaydı)

- `CTATAA`
- `TATAAA`
- `ATAAAC`
- `TAAACC`
- `AAACCT`
- `AACCTT`
- `ACCTTA`
- `CCTTAC`
- `CTTACA`
- `TTACAT`
- `TACATC`

Yukarıdaki parçaların hepsinin hesabı yapıldığında şöyle bir tablo ortaya çıkar:

![image](https://user-images.githubusercontent.com/12685802/148228679-2de6f844-2dfc-4af8-ae14-8764497134b6.png)

En yüksek ihtimalli olan `AAACCT`, P-Most Probable 6-mer değeridir.

### P-Most Probable l-mers in Many Sequences - Çoklu Sekanslarda P-Most Probable l-mer

![image](https://user-images.githubusercontent.com/12685802/148273032-ad55e238-795b-4723-9bcd-0f7c9e6cd90f.png)

Her bir sekans için P-Most Probable 6-mer bulunur.

Ardından bu sekanslar için bulunan P-Most Probable 6-merler ile yeni bir profil oluşturulur:

![image](https://user-images.githubusercontent.com/12685802/148273125-6088672a-683a-4867-aaf0-c07a95c4883d.png)

#### Yeni ve Eski Profilin Karşılaştırılması

![image](https://user-images.githubusercontent.com/12685802/148273331-907e5932-3083-491e-adea-8d3be30e9998.png)

Kırmızılar frekansın arttığını, mavi frekansın azaldığını gösterir.

### Gibbs Sampling

Farz edelim ki elimizde 5 (t) sekansımız var, motif uzunluğu (l) da 8

![image](https://user-images.githubusercontent.com/12685802/148274092-8ce8eacf-86db-4e65-9f64-41fe4f0f3732.png)

Bu 5 sekans içinden, bilmediğimiz motifi arayacağız... 🤔

1. Her sekans için rastgele bir başlama pozisyonu seçilir: `s = (s1, s2, s3, s4, s5)`

![image](https://user-images.githubusercontent.com/12685802/148274430-deb5cc35-fd0b-4a38-ad66-24700cb9aec8.png)

Bu stringler bizim için profile kaynağı olarak kullanılacaktır.

2. Rastgele olarak bir sekans (bizim örneğimizde 2. sekans, bu sekansa a sekansı diyelim) kenara alınır. 

3. Kalan sekanslar üzerinde profil çıkarılır. Bu profile P diyelim.

![image](https://user-images.githubusercontent.com/12685802/148274831-eb7d9aec-a68a-423f-88d4-9aa360b25561.png)

4. Kenara alınan sekans üzerinde Pr(a | P) hesabı yapılır.

![image](https://user-images.githubusercontent.com/12685802/148275035-0b9619ed-9c8c-4327-b1c7-41800346ae45.png)

İlk konum `AAAATTTA` en şanslı konum olduğundan değer bu kabul edilir.

5. l-mers Pr(a|P) olasılıklarının bir dağılımını oluşturup ve bu dağılıma dayalı olarak rastgele yeni bir başlangıç pozisyonu seçilir. (0.000122 az önceki listede en küçük olasılıktı)

![image](https://user-images.githubusercontent.com/12685802/148275955-fe745d24-eee0-4f22-92e5-1c3afa7d62d5.png)

Hesaplanan oranlara göre başlangıç pozisyonlarının olasılıklarını tanımlarız. 

![image](https://user-images.githubusercontent.com/12685802/148276300-a08527c8-fe16-449f-8c45-d4cf13798e59.png)

![image](https://user-images.githubusercontent.com/12685802/148276682-ee4b1c4a-c73e-4aa0-b11d-1c44fbe52eb0.png)

6. Entropi oranı belli bir seviyeye gelene kadar bu işlemi tekrar yaparız.

---

[<< Geri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta10.md)

[>> İleri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta12.md)
