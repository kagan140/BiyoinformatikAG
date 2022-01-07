# Biyoinformatik Algoritmalara Giriş
## Hafta 13

[E.Coli Organizması tekrar işlendi.](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta12.md#e-coli)

### Network Motif

Tesadüfen oluşabiliyorsa bu tip kendi kendine oluşmuştur.

Ama bu tesadüfler içinde bazıları çok sıksa tesadüf olmadığını düşünülebilir.

Network notifleri bu şekilde bulunur.

![image](https://user-images.githubusercontent.com/12685802/148547479-1138275f-e91b-4fcb-81c2-7f67f548cfbf.png)

İşaretli mavi protein bağlandığı zaman kırmızı genin üretimini arttıyor diyelim. Bu şekilde kurallar var, kuralları grafa bağladığımızda şöyle graflar oluşur:

#### 3-node subgraph: (kırmızıyla çizilmiş)

![image](https://user-images.githubusercontent.com/12685802/148547412-9b8463fa-0902-46b6-b465-3c8560d68b8a.png)

#### 4-node subgraph: (kırmızıyla çizilmiş)

![image](https://user-images.githubusercontent.com/12685802/148547817-406cb27c-1239-4347-ad58-78b0db9f43c9.png)

### Subgraph Örnekleri

![image](https://user-images.githubusercontent.com/12685802/148547876-060e14ab-569d-416e-b0fb-b3c857465f74.png)

#### 3-node kaç tane Subgraph üretebiliriz?

13 tane.

![image](https://user-images.githubusercontent.com/12685802/148547934-0b71b935-d922-4a3e-afab-066b1b25b655.png)

#### 4-node kaç tane Subgraph üretebiliriz?

199 tane.

![image](https://user-images.githubusercontent.com/12685802/148548467-9d2e59b7-a00c-4fce-b7ae-d78f484e7f8f.png)

#### 5-node kaç tane Subgraph üretebiliriz?

9364 tane.

Rakamlar hızla artıyor...

**Bizden istenen** 25 bin Node içeren bir grafta 4 nodetan oluşan yönlü grafları bulacaksınız ve bunlar sık tekrar edecek.

![image](https://user-images.githubusercontent.com/12685802/148548849-012a219e-1b9a-463d-a790-eb2b3ebe2b96.png)

E. Coli transcription networkü... (Kırmızılar gen)

### Bir Network Motifi Nasıl Bulunur?

Karşımıza çıkan ağlar tesadüfen mi oluştu? Yoksa tekrar eden bir durum mu var onu anlamaya çalışıyoruz.  

#### Algoritma

1. Gerçek networkü alıyoruz ve oradaki subgraphlara bakıyoruz.
2. Bunları sınırlandırıyoruz.
3. Derecelendirme yapıyoruz.
4. Çok sayıda örnekle 1 ve 2'yi sürekli tekrar ediyoruz.

![image](https://user-images.githubusercontent.com/12685802/148549290-169dfbe5-ed09-4f66-a00b-fec0cc412bfb.png)

Bunun sonucunda gerçek bir Network ve rastgele Networkü, rastgele Networkteki bazı parametreleri kullanarak bir Z skoru üretiyoruz. Bu şekilde motifin tesadüfen olup olmadığını anlıyoruz.

Mesela sağ taraftaki gibi motifler resimde gösterilmiştir:

![image](https://user-images.githubusercontent.com/12685802/148557006-874c3d9c-813b-468e-b1d0-d6e927f3bace.png)

### FFL Devre Benzetmeleri

![image](https://user-images.githubusercontent.com/12685802/148557142-78d404c0-1b5e-45a2-9bbf-7b1d43159787.png)

X, Y'yi etkiler. Y'de Z'yi etkiler ama X aynı zamanda tek başına da Z'yi etkiler...

#### Örnek

Bu durumu FFL devresinde benzetebiliriz.

![image](https://user-images.githubusercontent.com/12685802/148557190-d77cb117-c60c-4115-b6a2-7f08634927d6.png)

Dokuya X pompalarsak, Y ve Z değerleri nasıl değişir bunu inceliyoruz:

![image](https://user-images.githubusercontent.com/12685802/148557249-546d230c-e018-41ad-8b9c-eba4496f5c0d.png)

X mesela Y'yi biraz kaldırdı ama zamanla söndü...

Ama X ve Y eş zamanlı artmadığı için Z değeri sürekli 0 kalır.

![image](https://user-images.githubusercontent.com/12685802/148557386-a813c989-603a-443d-9050-e89bc4eacdd2.png)

X sürekli verilirse, Y yavaş yavaş sürekli artmaya başlar. X 0'a indiğinde Y ve Z söner... 

Ama ikisi de 0'a inmez. Zamanla düşer. Ama tabii ki daha fazla Z üretimi olmaz.

![image](https://user-images.githubusercontent.com/12685802/148557509-2a68b50d-52d2-48a3-8e98-6d9f5d1a96fb.png)

#### Örnek:

![image](https://user-images.githubusercontent.com/12685802/148557774-b391378d-1cc5-4f0b-80af-b103a50f9bc8.png)

0'dan sinyal verilir. Verdiğimiz anda Y artmaya başlıyor.

Y belli bir seviyeye geldiği zaman üretim duruyor... Z Threshold (eşlik) seviyesine kadar düşer.

#### Motif Örneği

![image](https://user-images.githubusercontent.com/12685802/148558106-bc2991b7-b1cb-44e6-a45b-85458ffc0ad6.png)

Sensör X ve Y'yi arttırır. Z ve W bunlara göre değişir.

#### Motif Örneği

![image](https://user-images.githubusercontent.com/12685802/148558215-288af663-e990-4adf-bf1f-abf45dd5c903.png)

Sinyal okuyucu X artınca Z1, Z2, ..., Zn artıyor/azalıyor.

#### Motif ve FFL Devresi 

![image](https://user-images.githubusercontent.com/12685802/148558373-2220f031-d3bb-4834-9338-9199233a5478.png)

X dediğimiz aslında promoter bölge.

![image](https://user-images.githubusercontent.com/12685802/148558546-17af28bc-a3ea-4c1b-bfc1-59f36378f940.png)

Mesela kuyruktaki motorla ilgili proteinlerin üretilmesini sağlar. Mesela dışarıda tehdit yok, kamçı proteini üretmesini istemeyiz çünkü enerjisi sınırlı. Ama yakında gıda varsa proteini üretmeli. Bu durumda protein üretilir ve canlı harekete geçer.

![image](https://user-images.githubusercontent.com/12685802/148558672-2a84c135-52ae-4bc0-9a92-b1688dbaf3f4.png)

...

![image](https://user-images.githubusercontent.com/12685802/148558822-3202fa1c-2079-4342-93c0-9ac0c2d83360.png)


### Saklı Markov Modelleri

Leonard E. Baum ve Ted Petrie tarafından geliştirilmiş istatistiksel model.
 
- Gözlemlerimizden öğrenme yaparak geleceğe ilişkin öngörülerde bulunmak.
- Sinyallerden öğrenme yaparak geleceğe ilişkin öngörülerde bulunmak.

Sıcaklığın zaman içinde artıp azaldığı bir örüntü var. Gözlemler (sinyaller) bunu gösteriyor. Sıcaklığın artıp azalmasına sebep olan faktörler illaki var. 

Bu faktörleri bilmesek dahi sıcaklık hakkında öngörüde bulunabiliyoruz.

Herhangi bir zaman serisini düşünün:

- ..67 66 69...75... önümüzdeki yıl ortalama petrol fiyatı 80 dolar olacak?

Problemi bu şekilde çözmeyi 1970lerde düşünmüşler. Ve başarmışlar. Sadece elimizdeki verilere bakarak, faktörlerin ne olduğunu bilmeden faktörlerin yaptığı etkilerden tahmin yürütmek.

Yapay (makine) öğrenme yöntemidir.

Karşımızda çok uzun DNA sekansları var. `ATGCGTAACGA` bu sekanslara ait öngörüler yapılması gerekiyor. 

- **Örnek:** CGP adası problemi

### Örnek: The Dishonest Casino

Karşımızda atılan zarlar varmış gibi düşünelim.

![image](https://user-images.githubusercontent.com/12685802/148567794-218b65a1-81a7-4348-9b6b-e4883ce6f408.png)

Yöntemimiz atılan zarlar hileli zarla mı yoksa düz bir zarla mı atıldı diye kontrol etmek için kullanılır.

Sinyalleri görüyorum ama etki eden faktörleri görmüyorum. 

Dürüst zardaki olasılıklar:

![image](https://user-images.githubusercontent.com/12685802/148568160-28f2776e-440d-4927-925a-6be3d66d7f5c.png)

Hileli zardaki olasılıklar:

![image](https://user-images.githubusercontent.com/12685802/148568191-0197a453-6abf-430e-8486-9bd694086851.png)

Leonard E. Baum ve ekibi gözlemlerden bir model oluşturuyolar:

![image](https://user-images.githubusercontent.com/12685802/148568370-d004bddc-daa4-48fb-bd4f-d3d34e76a7b7.png)

#### İnceleme - 1 

Sonuçlar: `1, 2, 1, 5, 6, 2, 1, 5, 2, 4`

Hilesiz bir zarda bu sonuçların çıkma olasılığı nedir?

(Hileli veya hilesiz bir zarı seçme olasılığı 1/2)

1/2 * P(1 | Adil Zar) * P(Adil Zar | Adil Zar) (adil zarken adil zar kalma olasılığı, yukarıdaki görselden)  * P(2 | Adil Zar) * P(Adil Zar | Adil Zar) * P(1 | Adil Zar) * P(Adil Zar | Adil Zar) ...  P(4 | Adil Zar) =

1/2 * 1/6 * 0.95 * 1/6 * 0.95 * 1/6 * 0.95 * 1/6 * 0.95 * 1/6 * 0.95 * 1/6 * 0.95 * 1/6 * 0.95 * 1/6 * 0.95 * 1/6 * 0.95 * 1/6 =  

1/2 * (1/6)^10 * (0.95)^9 ~= (0.50)^(-9)

#### İnceleme - 2

Sonuçlar: `1, 2, 1, 5, 6, 2, 1, 5, 2, 4`

Hileli bir zarda bu sonuçların çıkma olasılığı nedir?

(Hileli veya hilesiz bir zarı seçme olasılığı 1/2)

1/2 * P(1 | Hileli) * P(Hileli | Hileli) * P(2 | Hileli) * P(Hileli | Hileli) * P(1 | Hileli) * P(Hileli | Hileli) ...  P(4 | Hileli) =

1/2 * 1/10 * 0.95 * 1/10 * 0.95 * 1/10 * 0.95 * 1/10 * 0.95 * 1/10 * 0.95 * 1/2 * 0.95 * 1/10 * 0.95 * 1/10 * 0.95 * 1/10 * 0.95 * 1/10 =  

1/2 * (1/10)^9 * 1/2 * (0.95)^9 ~= (0.16)^(-9)

Sonuç az önceki incelemeden küçük çıktı. Hileyi yakalamış olduk.

#### İnceleme - 3

Sonuçlar: `1, 6, 6, 5, 6, 2, 6, 6, 3, 6`

Hilesiz bir zarda bu sonuçların çıkma olasılığı nedir?

1/2 * P(1 | Hilesiz) * P(Hilesiz | Hilesiz) * P(6 | Hilesiz) * P(Hilesiz | Hilesiz) * P(6 | Hilesiz) * P(Hilesiz | Hilesiz) ...  P(6 | Hilesiz) =

1/2 * 1/6 * 0.95 * 1/6 * 0.95 * 1/6 * 0.95 * 1/6 * 0.95 * 1/6 * 0.95 * 1/6 * 0.95 * 1/6 * 0.95 * 1/6 * 0.95 * 1/6 * 0.95 * 1/6 =  

1/2 * (1/6)^10 * (0.95)^9 ~= (0.50)^(-9)

_**İnceleme - 1'deki sonuçla aynı.**_

Hileli bir zarda bu sonuçların çıkma olasılığı nedir?

1/2 * P(1 | Hileli) * P(Hileli | Hileli) * P(6 | Hileli) * P(Hileli | Hileli) * P(6 | Hileli) * P(Hileli | Hileli) ...  P(6 | Hileli) =

1/2 * 1/10 * 0.95 * 1/2 * 0.95 * 1/2 * 0.95 * 1/10 * 0.95 * 1/2 * 0.95 * 1/10 * 0.95 * 1/2 * 0.95 * 1/2 * 0.95 * 1/10 * 0.95 * 1/2 =  

1/2 * (1/10)^4 * (1/2)^6 * (0.95)^9 ~= (0.50)^(-7)

Bir üsttekine göre (_(0.50)^(-9)_) 100 kat daha büyük bir olasılık çıktı 😳😳


### Diğer İncelemeler / Problemler

#### 1 - Evaluation/Değerlendirme 

Elimizde bu şekilde sekanslar var:

![image](https://user-images.githubusercontent.com/12685802/148570382-c66ea537-94f0-4803-a3a3-a3dd52adb388.png)

Bu sekanslar her şey olabilir: DNA sekansı, atılan zarların değerleri, petrol fiyatları

Bu sekanstaki içeriğin dürüstlüğü incelenir. Tesadüfen oluşma şansları?

#### 2 - Decoding

![image](https://user-images.githubusercontent.com/12685802/148571094-f59d4fd0-3dea-467a-992a-63ae7d7bc7fb.png)

Bu sekansın hangi kısımları hileli zar ile hangi kısımları düz zar ile atılmış bunu belirlemeliyiz.  

#### 3 - Learning/Öğrenme

![image](https://user-images.githubusercontent.com/12685802/148571281-b8a8c2a4-72c8-4b2c-bfc0-7ce09671e019.png)

Karşımdaki sekanslarda belli aralıklardaki değişikliği bulma:

Yani aslında şu modeli bulmam gerek:

![image](https://user-images.githubusercontent.com/12685802/148571396-82822033-6fb5-43fe-8abf-bca51e05e34c.png)

![image](https://user-images.githubusercontent.com/12685802/148571524-f0bac631-2c0b-4c48-9b4b-3e6f0498bed6.png)

Bu modeller kişilerin karakter yazma ve biyoinformatikte sekansların sonuçlarıyla ilgili müthiş bir kullanım alanı var.

---

[<< Geri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta12.md)

[>> İleri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta14.md)
