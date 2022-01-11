# Biyoinformatik Algoritmalara Giriş
## Hafta 3

### SimpleStringSearch:

Direkt adım adım (shift ile kayarak) pattern'e göre karşılaştırma yapar. Atlama gibi hiçbir yöntem kullanmaz.

![image](https://user-images.githubusercontent.com/12685802/144748669-a09e4876-be7d-4b19-ac38-0c2a065a9c81.png)

![image](https://user-images.githubusercontent.com/12685802/144748692-687d189f-9b74-4763-909c-0bbc0b5e0c42.png)

len(pattern) = 4 = m

len(text) = 18 = n

Problemin çözümü: O(nm)

String matchingi SSS ile yaparsak vaktimiz yetmez. Bu yüzden yeni algoritmalar üretilir:

---

### Knuth-Morris-Pratt:

https://www.youtube.com/watch?v=5i7oKodCRJo

https://bilgisayarkavramlari.com/2009/04/11/knuth-morris-prat-algoritmasi-kmp-algorithm/

O(m+n)

Bazı atlamalar üretebilmek için zaten bleli olan patternde ön bir tarama yapılır. 

Bu tarama sonrası prefix table adı verilen bir tablo üretilir. Atlamalar bu tabloya göre yapılır.

#### Prefix table oluşturma:

![image](https://user-images.githubusercontent.com/12685802/144749802-62bb4624-aa77-4e9c-9553-1d7d4e8cc807.png)

![image](https://user-images.githubusercontent.com/12685802/144749817-2aea2c6f-400a-4068-9ee2-1cfc91afa19a.png)

İlk karakterimiz A, ne bir prefix (ön ek) ne de bir suffix (son ek) üretme şansımız var. Bu yüzden prefix değeri 0. Aslında pattern'in ilk karakterinin değeri her zaman 0dır.

![image](https://user-images.githubusercontent.com/12685802/144749873-af7d7c99-ed90-4b7a-9b4f-016598a2b2ce.png)

AC, prefix = A, suffix = C, ama bir eşleşme (ikisinde de bulunması gerekiyor) yok o yüzden değeri 0.

![image](https://user-images.githubusercontent.com/12685802/144749936-eac72809-01cb-4407-b74c-0de1109033e0.png)

ACA, olası prefixler A ve AC. Olası suffixler CA ve A. Bir eşleme var (ikisinde de A var) ve bu eşleşmenin uzunluğu 1 bu yüzden değeri 1.  

![image](https://user-images.githubusercontent.com/12685802/144750002-8f7dce83-18e3-47b5-bc13-92852c98c752.png)

ACAC, olası prefixler A, AC, ACA. Olası suffixler CAC, AC, C. Bir eşleşme var (AC) ve uzunluğu 2 (len(AC)) prefix tablosunda değeri 2

![image](https://user-images.githubusercontent.com/12685802/144750108-b4c03c6e-77ee-4285-9f42-7ada465ab3a0.png)

ACACA, olası prefixler A, AC, ACA, ACAC. Olası suffixler CACA, ACA, CA, A. İki eşleşme var, biri A diğeri ACA. Uzunluğu yüksek olanı alıyoruz. Prefix tablosundaki değerimiz 3.

ACACAG ve ACACAGT durumlarında eşleşme yok değerleri bu yüzden 0.

![image](https://user-images.githubusercontent.com/12685802/148974477-43282b43-8e86-4e76-a5a1-f40138c9501e.png)

#### Şimdi algoritmayı kullanalım:

![image](https://user-images.githubusercontent.com/12685802/144750370-0e4bb84e-80d6-444d-8ef4-d3ff1e6d7c3d.png)

ACAT ACGACACAGT içerisinde ACACAGT arıyoruz.

Eşleşme olmayan karakterden önceki karakterin (örneğimizde C'den önce A geliyor) prefix değerine (A'nın prefix değeri 1) bakıp eşleşen karakter sayısı (3) kadar çıkarıyoruz. Bulduğumuz sonuç ilerleme sayımızdır. 

- Eşleşme olmayan karakter: Örneğimizde C
- Eşleşme olmayan karakterden önceki karakter: A
- Eşleşme olmayan karakterden önceki karakterin prefix değeri: 1
- Eşleşen karakter sayısı ACA -> `3`
- İlerleme sayımız: 3 - 1 = `2`

Örneklere bakalım:

İlk üç karakter eşleşiyor.

![image](https://user-images.githubusercontent.com/12685802/148977124-ff36cb98-48af-456e-a621-fd4bafa43cf1.png)

Ama 4. karakter eşleşmediği için 3. karakterin (A) prefix tablosundaki değerine bakıyoruz. 

Değeri 1. 

Eşleşen karakter sayısı 3 (ACA). 

3-1 = 2, bu sayede 2 adet atlama yapabiliriz.

![image](https://user-images.githubusercontent.com/12685802/144750451-e4d9099d-dc34-41f3-94fa-4796d669060d.png)

2 sağa kaydık ve şimdi kontrol ediyoruz. 1. karakter eşleşti 2. karakter eşleşmedi, prefix tablosundaki değerimiz 0, eşleşmemiz 1 bu yüzden normal shift (1 ilerleme) atıyoruz.

![image](https://user-images.githubusercontent.com/12685802/144750550-58c1c74b-50ee-4000-92c7-4106d988fa28.png)

Eşleşme yok devam ediyoruz.

![image](https://user-images.githubusercontent.com/12685802/144750612-60493040-74fb-4cb3-b0c1-fa52863b686b.png)

![image](https://user-images.githubusercontent.com/12685802/144750631-6a16928f-995e-47d1-98fa-1932a6646c91.png)

Ve bir eşleşme bulduk.

![image](https://user-images.githubusercontent.com/12685802/144750644-1105b644-734e-41b1-adb7-989fd792b6b5.png)

![image](https://user-images.githubusercontent.com/12685802/144750651-43cc4fe5-ce6b-4c01-9a23-bd2b11a9b0d4.png)

Bu sefer 3. karakter eşleşmedi. 2. karakterimizin (C) prefix tablosundaki değeri 0. Eşleşme uzunluğumuz (AC) 2, 2-0=2. Böylece 2 atlama yapabiliriz.

![image](https://user-images.githubusercontent.com/12685802/144750656-8cf1670b-401d-4e15-8b70-c4965a0d34aa.png)

![image](https://user-images.githubusercontent.com/12685802/144750723-a867edf0-3095-4347-96bf-5ac9dcb0db61.png)

Eşleşme yok.

![image](https://user-images.githubusercontent.com/12685802/144750737-e829c8c6-de17-4dbd-bba2-3e940149f70c.png)

Ve şimdi hepsi eşleşti.

![image](https://user-images.githubusercontent.com/12685802/144750752-c47f44d0-2e3d-4c84-8ccb-669855b9adec.png)

#### Dersteki Örnek:

![image](https://user-images.githubusercontent.com/12685802/144750892-fde73e97-53fc-4643-8d44-fdd10aa33929.png)

5-2 = 3 shift yapar.

#### Dersteki Örnek:

![image](https://user-images.githubusercontent.com/12685802/144751718-98558422-8a3e-4043-90aa-49a6e23167a4.png)

5 (acaca) - 1 (a'nın prefix tablosundaki değeri) = 4 adım ilerler. 

Ardından böyle devam eder.

---

### Boyer Moore Algoritması:

https://www.youtube.com/watch?v=PHXAOKQk2dw

KMP algoritması soldan ilerler. Ama sağdan okuyarak ilerlersek daha hızlı gideriz.

Bad match tablosu kullanılır. Eşleşme olmadığında tablodaki değer kadar ilerleme yapılır.

#### Bad Match Tablosunu Oluşturma

![image](https://user-images.githubusercontent.com/12685802/144755070-f0006386-53ae-4e67-b821-d8e1dc571788.png)

Pattern'deki karakterler, bir kere yazılmak üzere bir tabloya yazılır. Aynı zamanda * karakteri de yazılır, bu karakter patternde olmayan karakterler içindir.

Tabloların altına veriler *value = length - index - 1* kuralıyla eklenir.

- T = 5 - 0 - 1 = 4, tablodaki T'nin değeri 4 olarak değişti.
- O = 5 - 1 - 1 = 3, tablodaki O'nin değeri 3 olarak değişti.
- O = 5 - 2 - 1 = 2, tablodaki O'nin değeri 2 olarak değişti.
- T = 5 - 3 - 1 = 1, tablodaki T'nin değeri 1 olarak değişti.
- H = 5 - 4 - 1 = 0, tablodaki H'nin değeri 0 olarak değişmesi gerekirken değişim yapılmaz çünkü son işlem yapınılmamış gibi davranılır.
- En sona da * karakterinin değeri olarak uzunluk (len("TOOTH") yani 5) yazılır.

Böylece tablo şu hale gelmiş oldu:

![image](https://user-images.githubusercontent.com/12685802/144755274-d95a92ec-95ca-445f-a502-c0cddb4ca754.png)

#### Şimdi algoritmayı kullanalım:

Pattern'in son karakteri karşılaştırılır. Eşleşme olmadı, T karakterinin tablodaki değerine bakılır (1) ve bu kadar ilerleme yapılır.

![image](https://user-images.githubusercontent.com/12685802/144755325-af3b76c5-b973-4c08-aa57-afda379e5351.png)

Şimdi bir eşleşme yakaladık. H=H, şimdi bir soldaki karakter ile eşleşme yapacağız.

![image](https://user-images.githubusercontent.com/12685802/144755391-95bf4939-ca5a-49ae-99cd-39e2bd0dee0d.png)

Tekrar eşleşti.

![image](https://user-images.githubusercontent.com/12685802/144755413-fad74f8c-82fd-4c42-92ba-e09e28ef5855.png)

Ama daha sonraki eşleşme sağlanmadı. Şimdi ilk eşleşme yakaladığımız karakterin değerine bakıp o kadar atlama yapacağız. Yani H=5 kadar.

![image](https://user-images.githubusercontent.com/12685802/144755436-329a8e07-e2b8-4fda-97cc-b5fbb65640b3.png)

Tekrar eşleşmeyi sağlayamadık. O=H değil bu yüzden O'nun tablodaki değeri (2) kadar gideeceğiz.

![image](https://user-images.githubusercontent.com/12685802/144755482-996c832d-48cc-4e25-85d6-875718fe78c7.png)

Ardından bir süre sonra böyle ilerledikten sonra eşleşmeyi yakaladık.

![image](https://user-images.githubusercontent.com/12685802/144755533-35928a16-9e4f-4375-8241-37c63971203a.png)

#### Dersteki Örnek

Textte okuduğumuz E karakteri patternimizin içinde bulunmuyor. Bu yüzden 4 adım ilerleyebiliriz.

![image](https://user-images.githubusercontent.com/12685802/144751926-41cfcfea-9e7a-488f-822e-d71685432d83.png)

#### Dersteki Örnek - 2

![image](https://user-images.githubusercontent.com/12685802/144752165-ab82c492-bf7d-45ab-a4b6-a44f2a74fdd1.png)

---

Makine seviyesinde işlem yapabilmek için Bit Paralel String Matching'e geçildi. Shift-AND ve Shift-OR yöntemleri geliştirildi.

### Shift-AND algoritması:

Pattern: ATGAG

DNA alfabemde 4 eleman var. O zaman 4 adet maske üretelim:

- M(A) = 10010 (A--A-)
- M(C) = 00000 (-----)
- M(G) = 00101 (--G-G)
- M(T) = 01000 (-T---)

**Text:** ATGCTGACCT

5 karakter okumak yerine tek karakter okuyor.

A'yı aldık diyelim. Onun maskesini alıyor (10010) ve bir sağa kaydırıyor. 01001.

Sonra T'yi al maskesiyle işleme tabii tut ve böyle devam et... Haftaya işleyeceğiz.

---

[<< Geri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta2.md)

[>> İleri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta4.md)
