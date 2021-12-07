# Biyoinformatik Algoritmalara Giriş
## Hafta 9

### Sınav Soruları
- İki sekans, ceza ve gap koşullarını verecek needleman wunsch ya da smith watermann ile çöz
- Needleman Wunsch ile Smith Watermann farkı, bu kavramları niye kullanıyoruz
- Problemi çözerken algoritma analiz mantığını bilmen gerek. Mesela Boyer-Moore gibi algoritmaların karmaşıklıklarını bilmen gerek.
- Burrows-Wheeler dönüşümü
- DNA'nın bunlarla ne ilişkisi vardır bilmen gerek
- Uzunluğu 4 olan kaç farklı DNA stringi yazılabilir? - - - - ( 4.4.4.4 = 256 ) 

---

**Smith Watermann algoritması:** İki sekans arasınadki örtüşen kısımları bulur. Local Alignment olarak da bilinir.

**Needleman Wunsch algoritması** İki sekans arasınadki benzerliği bulur. Global Alignment olarak da bilniir. Longest common subsequence probleminin aynısı. Eşleşme, eşleşmeme ve gap durumlarında skor koşulları ayrıca belirlenir. (PAM, BLOSUM matrisleri gibi)

Her şey klasik dinamik programlama ile icra ediliyor.

---

### K-mer Index (L-mer Index)

![image](https://user-images.githubusercontent.com/12685802/145002314-d1e2a040-2d5d-4555-b9fc-006d0cc4c411.png)


ACTCGAATGCTCAATG..

AATG aranacak olsa: FM index (burrows-wheeler) işe yarar.

İkili arama benim için daha kolay. FM Index ikili arama nedeniyle avantajlı.

k-mer için k değerimiz 4

- ACTC 0
- CTCG 1
- TCGA 2
- ...
- AATG 12

Bu verileri işleme tabii tutmadan önce sıralasam, ikili aramayı kolayca yapabilirim.

Varsayım A=0, T=1, G=2, C=3 olsun.

- AAAA: 0
- AAAT: 1
- AAAG: 2
- AAAC: 3
- AATA: 4
- ...
- AATG: 6
- ...
- ACTC: 0 * 4^3 + 3 * 4^2 + 1 * 4^1 + 3 * 4^0  = 0 + 48 + 4 + 3 = 55 ==> 0, 16, 55 (nerelerde bulunduğu)
- ...

---

### Blast Algoritması
Bu algoritmanın mantığı referans genomun 4-mer, 6-mer, 7-mer, 8-mer, 9-mer, 10-mer....,16-mer uzunluğu olarak sakla.

Sorgu: Q: TGCAT için 4-mer sorgusu nasıl yapılır?
- **ql1:** TGCA
- **ql2:** GCAT

Her birisi için veri referans gende 4-mer sorgulanır.

Cevaplar geldi:
- **ql1 için:** 400, 600, 799, 900
- **ql2 için:** 300, 596, 601, 800, 950

799 ql1 = TGCA, 800 ql2 = GCAT, birbirini ardına gelirler ve TGCAT yazar bu yüzden bu konumda vardır.

600 ql1 = TGCA, 601 ql2 = GCAT, birbirini ardına gelirler ve TGCAT yazar bu yüzden bu konumda vardır.
 
---

Şimdiye kadar kısa bir pattern'i uzun bir text içinde arıyorduk. 

Çözüm tekniği: Ön işleme ile text'i daha kolay erişilir hale getir.

Boyer Moore, KMP gibi algoritmalar ise pattern'i önişlemeye tabi tutuyolardı..

### Motif Bulma Problemi:

Elimde metin var. Bu metinde tekrar eden örüntü var. Onu bulmalıyım. Ama ne aradığımızı dahi bilmiyoruz bu yüzden zor.

Aradığımızı bilmeme sebebimiz mutasyonlar. 600 nükleotid uzunluğnuda olan 20 rastgele sekans arasında uzunluğu 15 olan implant örüntü var. Her örüntü en fazla 4 mutasyon içeriyor.

![image](https://user-images.githubusercontent.com/12685802/145005642-e95ed05f-0bf9-4c44-87d6-4bca324083d6.png)

Üstte yazdığımız örnek için (15,4) motif problemi denir.

### Gold Bug Problem

---

[<< Geri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta8.md)

[>> İleri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta10.md)
