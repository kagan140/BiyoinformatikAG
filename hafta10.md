# Biyoinformatik Algoritmalara Giriş
## Hafta 10

### Implanted Motif

![image](https://user-images.githubusercontent.com/12685802/148182388-dbd18e4e-7ddc-41d0-beaa-a3e004b891c0.png)

Hepsinde ortak bir motif var ve bunu bulmak gerekiyor.

![image](https://user-images.githubusercontent.com/12685802/148182476-5f368355-c7f6-4526-88f6-8f8c0c8dde12.png)

Tabii motifler (aşağıda TF diye açıkladığımız durumlar) mutasyona da uğramış olabilir. (4 karaktere kadarı kabul ediyoruz, 4 mutasyon sonrasında fiziksel özelliği sağlamazlar.) Bu da işi çok zorlaştırıyor çünkü aranacak bir pattern yok.

![image](https://user-images.githubusercontent.com/12685802/148182674-a30bbee5-a8d3-4321-a35c-8b2cf0ffd367.png)

### Combinatorial Gene Regulation - Ortaklanmış Gen Regülasyonu

![image](https://user-images.githubusercontent.com/12685802/148182828-79e50cf5-a41f-49b7-b108-ba8d579e7d20.png)

Bir dokuya ait genler ve ekspesyon oranları var. Her bir yuvarlak, belli bir genin dokudaki yoğunluğunu ifade eder.

Sarardıkça daha yoğun olduğunu ifade eder.

### Transcription Factors and Motifs

Diyelim ki 900 gen var, bu 900 genin 20 tanesi bir anda duruvermiş. Bu nasıl olabilir? 

- Bir protein durduğu zaman diğer proteinleri üreten bir protein ise diğer 20 proteini etkileyebilir.

mRNA üretim sürecinde kilidin açılması için bazı proteinlerin bağlanması gerek, o proteinlerden biri (TF - Transcription Factor) yoksa üretilecek proteinlerin hiçbiri üretilemez. 

![image](https://user-images.githubusercontent.com/12685802/148183907-9dca8a53-4b96-44b9-832e-78a0ae774c9c.png)

TF'lerin yeri tam bilinmiyor ama 100-1000 bp bir noktadadır. Bu yerlerin bulunması lazım çünkü TF durunca gene1, gene2, gene3... de duruyor.

![image](https://user-images.githubusercontent.com/12685802/148184360-853c8957-9b93-4d0d-994d-2ea0609d5661.png)

### Gold Bug Problem

[Hafta 9 - Gold Bug Problemi](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta9.md#gold-bug-problem)

Üsttekini tekrar işledik. Ardından işlediğimiz şeyler:

![image](https://user-images.githubusercontent.com/12685802/148185056-d48c51e2-f24b-43be-bce1-925e0fd44900.png)

Motif bulma problemi ile Gold bug problemi arasında bazı farklar var. En büyük fark motif bulma problemi çok daha zor.

### Motifs: Profiles and Consensus - Motifler: Profiller ve Karar

![image](https://user-images.githubusercontent.com/12685802/148185632-ba267bc6-3a1b-4740-b74d-169c30a2b077.png)

Sekansların sütun sayısı eşitse herhangi bir sütunun hangi karakter olduğunun analizine profil denir. Bu profilleri de analiz ederek bir karara varabiliriz.

Cümle biraz karmaşık ama yapılan işlem kısaca şu:

- A B C D
- A C C D
- A B C E

Böyle bir durumda:

- 1. sütun kesinlikle A çünkü 3 tane A gerisinden 0 tane var.
- 2. sütun muhtemelen B çünkü 2 tane B, 1 tane C gerisinden 0 tane var.
- 3. sütun kesinlikle C çünkü 3 tane c gerisinden 0 tane var.
- 4. sütun muhtemelen D çünkü 2 tane D, 1 tane E gerisinden 0 tane var.

### Motifi Skorlama

![image](https://user-images.githubusercontent.com/12685802/148209110-a2f9dbf5-b5eb-42eb-a838-3b346f75d315.png)

Sütun başına en çok kullanılan karakterlerin kullanılma sayıları toplanarak bir sonuç bulunur.

Mesela yukarıda uydurduğumuz örneği tekrar ele alalım:

- A B C D
- A C C D
- A B C E

İlk sütun için A:3, B:2, C:3, D:2, böylece 3 + 2 + 3 + 2 = **10**

### Entropi

Satırlardaki toplam uyumsuzluğu gösterir. Ne kadar yüksek olursa uyumsuzluk o kadar fazladır.

![image](https://user-images.githubusercontent.com/12685802/148210383-38ff229c-b318-480a-98bf-6908fddc14b6.png)

- Sınav sorusu: Verilen 4 sekansın entropisini bulunuz.

### Çoklu Sekans Hizalama

Derste bahsetmiş olmak istiyor sadece, sınavda bu başlığı sormayacaktır.

3 sekans hizalanacaksa 3. koordinata, 3. boyuta daha ihtiyacımız var. (?)

![image](https://user-images.githubusercontent.com/12685802/148210991-2c25edd8-b7d8-49f7-b95a-324b679e4f57.png)

Bu 2 boyutlu bir örnek: (smith-waterman)

![image](https://user-images.githubusercontent.com/12685802/148211090-099193fe-8d1b-41ce-93a4-f7a6ffd3798b.png)

#### Manhattan Kübü:

![image](https://user-images.githubusercontent.com/12685802/148211151-47987582-c310-4a71-ba99-c802d4658c25.png)

### Multiple Alignment: Dynamic Programming

![image](https://user-images.githubusercontent.com/12685802/148211310-4ba2ed81-9188-404c-932a-85f296396bcc.png)

### Multiple Alignment Induces Pairwise Alignments - Çoklu Hizalama, Çift Yönlü Hizalamaları İndükler (?)

Diyelim ki x, y ve z segmentimiz var. Ve diyelim ki x ve y çok benziyor. Onların ortalamasını alıp bu x ve y'yi temsil eder diyosunuz. Böylece boyutunuz üçten ikiye iniyor.

![image](https://user-images.githubusercontent.com/12685802/148213008-012f4290-0a4e-4c1a-a6e1-b2a6f50df5e3.png)

Çoklu hizalamada n sekans için dinamik programlamayı yapmak O(2^k * n^k)

- Sınav sorusu olabilir: O(2^k * n^k) olmasını kanıtlayınız. :D Nasıl kanıtlayacaksak artık... 

---

[<< Geri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta9.md)

[>> İleri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta11.md)
