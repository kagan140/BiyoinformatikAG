# Biyoinformatik Algoritmalara Giriş
## Hafta 12

[Gibbs Sampling ile Motif Bulma](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta11.md#gibbs-sampling-ile-motif-bulma) ilk başta bu konu tekrar işlendi.

### Random Projection ile Motif Bulma

İşlem yaparken mutasyonları da bertaraf edecek bir olasılıksal yöntem...

Elinizde bir sekans var diyelim, bütün karakterleri değil de rastgele seçtiğiniz karakterleri ele alıyorsunuz.

![image](https://user-images.githubusercontent.com/12685802/148338473-d14b57ac-7340-4087-a435-64a144eda9a2.png)

`ATGGCATTCAGATTC`'yi `TGCTGAT` bucketına atarız. 

Buradaki bucket sistemi hash fonksiyonuna benzer şekildedir: (aşağıda hash fonksiyonu kullanımını anlatıyorum, sadece konuyu daha iyi anlamak içindir)
 
- Hash fonksiyonumuz h(x) = x % 3 şeklinde olsun:
   - x: 1 --> x % 3 = 1, 1 bucketına atılır
   - x: 2 --> x % 3 = 2, 2 bucketına atılır
   - x: 3 --> x % 3 = 0, 0 bucketına atılır
   - x: 4 --> x % 3 = 1, 1 bucketına atılır
   - x: 5 --> x % 3 = 2, 2 bucketına atılır
   - x: 6 --> x % 3 = 0, 0 bucketına atılır
   - ...
   - x: 18 --> x % 3 = 0, 0 bucketına atılır
   - x: 19 --> x % 3 = 1, 1 bucketına atılır
   - ...
- Arama yapılacağı zaman h(x) işlemi yapılır ve işlem sonucundaki bucket içerisinde arama yapılır. 


![image](https://user-images.githubusercontent.com/12685802/148339662-9615b921-9f5b-4181-9248-e5768b7ef58f.png)

Bucketlardan biri TGCACCT bucket'ı, bu şekilde 4^7 (4: A,C,T,G, 7: motif uzunluğu(k)) bucket oluşturabiliriz.

Karşımıza çıkan her stringten rastgele seçtiğiniz karakterleri ele alıp bu bucketlara atsak, karşımızda hiç motif yoksa doluluk oranları aynıdır diye düşünülebilir.

Ama motif varsa bazı bucketlar daha dolu olur.

![image](https://user-images.githubusercontent.com/12685802/148341152-10ada6f8-7eb6-442a-a645-34c6302046be.png)

Gördüğümüz gibi ATGC bucketı, GCTC bucketına göre daha dolu bir bucket demek ki bir motif varsa ATGC'ye daha benzer bir şey olmalı.

Sonuçların daha gerçekçi olması için çok fazla deneme yapılmalı.

![image](https://user-images.githubusercontent.com/12685802/148341421-91ae1227-d1e6-4e8a-9073-ff3de4dd5866.png)

Yukarıda gördüğümüz gibi ATGC bucketı en dolu bucket. Bu bucket'ı üreten segmentleri buluyoruz ve bir sonuç elde ediyoruz. Bu sonucu Gibbs ile motif bulma kullanarak geliştirebiliriz.

![image](https://user-images.githubusercontent.com/12685802/148341485-a6c83a08-4841-4fcf-ae18-2a77804e0766.png)

### Gen Regülasyon Ağı

İnsan yaklaşık 25.000 genin ürettiği proteinden oluşuyor

A geninin azalması B geninin azalmasına sebep olabilir.

A geninin azalması C geninin azalmasına sebep olabilir.

Mikrodizi gen yoğunluğu örneği:

![image](https://user-images.githubusercontent.com/12685802/148402567-30b44885-4707-4734-903a-8e1c99193add.png)

Hasta ile sağlıklı bir bireyin mikrodizileri analiz edilerek proteinlerin birbirine etkileşimi incelenir.

Sonuç olarak böyle protein ağları oluşur:

![image](https://user-images.githubusercontent.com/12685802/148402761-b7680299-6d0e-4a66-a57d-314bb4478e90.png)

#### E. Coli 

Sensörü motoru olan bilgisayar gibi işleyen bir organizma

![image](https://user-images.githubusercontent.com/12685802/148402941-1a4b3433-858f-498e-a2dd-ac2054a48653.png)

![image](https://user-images.githubusercontent.com/12685802/148403149-11ef5f8c-f565-47a1-a75d-3976612ed6bc.png)

![image](https://user-images.githubusercontent.com/12685802/148403223-9d1a3a7f-c997-4012-9193-8243fa5534cb.png)


### Gen Regülasyonu

- Proteinlerin şifresi organizmaların DNA'sında yer alır.

- Proteinler DNA ile etkileşime girerek diğer proteinlerin ifade regülasyonunu yapar.

![image](https://user-images.githubusercontent.com/12685802/148403733-4bd763c4-6d7b-496a-b49d-aa5427fa9595.png)

#### Activorler gen üretimini hızlandırır

![image](https://user-images.githubusercontent.com/12685802/148403980-8ce60ad8-542f-43c2-9141-e89137a32574.png)

Activator bağlanınca Y üretimi başlıyor.

Buna X, Y'yi aktive eder diyoruz.

![image](https://user-images.githubusercontent.com/12685802/148404135-da7bac3f-7f67-43c6-b9bd-e99d6e817fb0.png)

#### Repressors gen üretimini azaltır

![image](https://user-images.githubusercontent.com/12685802/148404184-eb743385-7068-4ad5-8a10-1ce373634708.png)

Activator bağlanınca Y üretimi başlamıyor.

Buna X, Y'yi baskılar.

![image](https://user-images.githubusercontent.com/12685802/148404198-99077f21-cce6-460b-a8ba-dcf3671ec9ae.png)

#### Genel Sinyal Mekanizması

![image](https://user-images.githubusercontent.com/12685802/148411776-2bbf9ff7-a77e-4eed-b8e4-a62beaad8af0.png)

Xm olanlar Repressor ya da Activator.. İkisinden biri...

Bu x'lere göre üretilecek proteinler belli oluyor.

![image](https://user-images.githubusercontent.com/12685802/148411911-4c3c830c-df21-458d-8209-9369e24b3b7f.png)

![image](https://user-images.githubusercontent.com/12685802/148411928-900e08cf-ef8f-46d6-a870-dbf2cb179272.png)

#### Promoter boyut sıralaması nedeniyle asimetrik derece dağılımı

![image](https://user-images.githubusercontent.com/12685802/148412040-df5981c7-7f7c-4596-897a-cad58347c74a.png)

Mavi **ve** Yeşil bağlanınca Kırmızı kısım üretilir.

Bu olay AND kapısına benzer.

![image](https://user-images.githubusercontent.com/12685802/148412206-2532ac9a-5ce5-4f5c-bf73-f138e092715e.png)

### Örnek - Enerji Kaynak Kullanımı

![image](https://user-images.githubusercontent.com/12685802/148412289-ccdb9b98-8e65-42bf-b2a6-d763da19b237.png)

Enerji için 2 seçeneği var:

- Glukoz
- Laktoz

Glukozdan daha fazla enerji üretebileceği için glukozu tercih eder. Ama sistemde glukoz yoksa sadece laktoz varsa lakz enzimini üret.

Bu kadar katı olmasının sebebi kaynaklarının sınırlı olması. Gereksiz yere enzim üretemez.

### Protein ve DNA ile kodlanan AND kapısı

![image](https://user-images.githubusercontent.com/12685802/148412851-1e906367-aca9-404a-b7e8-18d414635997.png)

Glukoz varsa kullan, yoksa ama lactoz varsa laktozu kullan.

![image](https://user-images.githubusercontent.com/12685802/148412981-f189fcf1-4167-458b-83d8-da0d4ec6d4c0.png)

![image](https://user-images.githubusercontent.com/12685802/148413035-ffc7deb6-42f9-473c-886c-6a8db9b1d7f3.png)

![image](https://user-images.githubusercontent.com/12685802/148413054-74fc05fe-eb54-4310-b24f-ba9ee853eb29.png)

### Network Motif

Tesadüfen oluşabiliyorsa bu tip kendi kendine oluşmuştur.

Ama bu tesadüfler içinde bazıları çok sıksa tesadüf olmadığını düşünülebilir.

Network notifleri bu şekilde bulunur.

---

[<< Geri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta11.md)

[>> İleri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta13.md)
