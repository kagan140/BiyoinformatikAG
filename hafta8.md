# Biyoinformatik Algoritmalara Giriş
## Hafta 8

### Longest Common Subsequence (LCS)

![image](https://user-images.githubusercontent.com/12685802/144935187-fa01d558-9c82-4753-bac1-2ef5be1333eb.png)

v,w şeklinde iki string varsa, bu iki string arasındaki en uzun ortak benzerlik.

Bu sorunu çözmeyi sağlayabilmek için dinamik programlamayı kullanabiliriz.

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

Hamming distance, DNA'daki eklemeleri ve silmeleri ihmal eder. Bu yüzden verimli değildir.

![image](https://user-images.githubusercontent.com/12685802/144936373-bb960b01-d8f4-4840-b5a5-1b7b4599560a.png)

#### Edit Distance

Levenshtein (1966), iki dizi arasındaki düzenleme mesafesini, bir diziyi diğerine dönüştürmek için minimum sayıda temel işlem (ekleme, silme ve değiştirme) olarak tanımladı.

#### Hamming Distance

Hamming distance sadece iki metnin i. karakteriyle i. karakterleri arasındaki farkı söyler. 

![image](https://user-images.githubusercontent.com/12685802/144936952-910511e9-648f-4bc5-be77-05c1065c87b3.png)

#### Hamming Distance vs Edit Distance

![image](https://user-images.githubusercontent.com/12685802/144937086-c9e71b43-494b-4e3d-9575-7b4d1b61585e.png)

Edit distance daha verimlidir ama hesaplaması kolay değildir.

#### Edit Distance Örnek

![image](https://user-images.githubusercontent.com/12685802/144937299-7f3f372f-4d72-4565-b943-6d6a705cb200.png)

Aynı dönüştürmeyi 4 adımda da yapabiliriz. 

![image](https://user-images.githubusercontent.com/12685802/144984008-a3b60b9f-823a-4e84-83d0-adae0448daac.png)

Peki 3 adımda yapabilir miyiz? Hayır.

![image](https://user-images.githubusercontent.com/12685802/144984345-a47ceb9e-aa04-4c01-8ac1-84927cdb182d.png)

#### Alignment as a Path in the Edit Graph

![image](https://user-images.githubusercontent.com/12685802/144986083-28fe1296-0888-4eec-b9c3-e625f1fef433.png)

Aşağı ve yana oklar 0 skor. Çaprazlar (eşleşmeler) 1 skor.

![image](https://user-images.githubusercontent.com/12685802/144986115-5d80267f-827b-49fa-a37d-b023d254037f.png)

Farklı durumlar olabilir:

![image](https://user-images.githubusercontent.com/12685802/144986267-d464fdc7-7687-4ee4-b28a-83e12b95226f.png)

### Alignment: Dynamic Programming

İlk önce 0. satır ve sütunlar 0 ile doldurulur.

![image](https://user-images.githubusercontent.com/12685802/144986600-b2b7ceaf-1678-4c41-b12e-e7162128a389.png)

Başlangıç için 0 yapılanlar hariç her bir kutucuk şöyle hesaplanır:

![image](https://user-images.githubusercontent.com/12685802/144986821-21c15db2-4a5a-4307-a68e-364a324c5694.png)

Ve sonuç:

![image](https://user-images.githubusercontent.com/12685802/144986972-29ab0c62-f0c1-4e02-a334-7299f1d19ebf.png)

Sağ alt köşeden sol üst köşeye gidiş bize cevabı verir.

![image](https://user-images.githubusercontent.com/12685802/144987244-7c4006fc-a811-4271-b72e-96bd096cd73e.png)

Backtracking:

![image](https://user-images.githubusercontent.com/12685802/144987276-a961cb56-7c0b-4a1a-ba3a-d209b6068891.png)

Ama O(nm) işlemdir.

---

Skor matrisi oluşturma

PAM ve BLOSUM matrislerini, içeriklerini (ceza ve ödül puanları) biyologlar belirler. 

Nükleotid seviyesinde değişikliklerden anlam çıkarmak zor; özellikle kodlama yapılan kısımlarda.

Bunun yerine aminoasit seviyesi kullanılır, daha kolaydır.

---

Şimdiye kadar olan ızgara hesabı sonucunda iki sekans arasındaki benzerlik oranı bulunur. (Needleman Wunsch algoritması)

Peki iki sekansın bütünde benzerliği lazım değilse, içlerindeki benzer kısımlar lazımsa ne yapacağız?

Bu da Smith Waterman algoritması - Local Alignment ile çözülür.

### Local Alignment - Local Hizalama

![image](https://user-images.githubusercontent.com/12685802/144989790-a0bb7bbb-56d9-4067-9221-43d7a952c57a.png)

#### Tablonun Oluşturulması
Global Alignment'e göre 0'lar farklı duruyor.

![image](https://user-images.githubusercontent.com/12685802/144990138-42d44925-9eec-40d9-8f44-78b2c9386f15.png)

Hiçbir zaman negatife gitmediği için benzemeyen kısımlar ceza almıyor.

![image](https://user-images.githubusercontent.com/12685802/144990314-4f091793-fc44-4516-a928-ce9c410a7c3e.png)

Global Alignmentta backtracking için sağ alttaki değere bakılırken Local Alignmentta matristeki en yüksek rakama bakılır.

![image](https://user-images.githubusercontent.com/12685802/144990416-22288b50-fb91-4479-bf3e-b595f6120327.png)

![image](https://user-images.githubusercontent.com/12685802/144990528-fe50dec3-6457-4a20-9e31-ff01c6507bc2.png)

#### BLOSUM Matrix Örneği:
![image](https://user-images.githubusercontent.com/12685802/145000693-dc5bbda3-1548-4490-9861-4393ee41c968.png)

---
[<< Geri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta7.md)

[>> İleri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta9.md)
