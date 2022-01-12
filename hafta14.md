# Biyoinformatik Algoritmalara Giriş
## Hafta 14

[Saklı Markov Modelleri Tekrar Edildi](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta13.md#saklı-markov-modelleri)

### Ayrık (Klasik) Markov Modeli 

Klasik markov modelinde 5 durum ve her durumun yönlendirmeleri var.

![image](https://user-images.githubusercontent.com/12685802/149080061-66d2524f-06a1-47ff-b3d3-a6ade2244313.png)

Otomatlara benzeyen bir sistem var:

![image](https://user-images.githubusercontent.com/12685802/149080126-944ac1e0-9e3c-44c7-bba6-9b245fd98f7f.png)

Bizim hesaplamaya çalıştığımız şey:

t+1 zamanında X'in olma ihtimali nedir?

![image](https://user-images.githubusercontent.com/12685802/149080189-3001bb88-98c8-42ce-b744-07f09aaf3d8a.png)

### Simple Minded Weather Example

#### Örnek

Elimizde `NNRNRRNRNNRNRRNN` şeklinde bir sekans olsun.

N: Güneşli, R: Yağmurlu günleri temsil eder.

- R: 7 - RR: 2, RN: 5
- N: 9 - NN: 3, NR: 5
 
 Yani:
 
 - Yağmurlu bir günden sonraki günün yağmurlu olma ihtimali Prr = 2/7, güneşli olma ihtimali Prn = 5/7
 - Güneşli bir günden sonraki günün güneşli olma ihtimali Pnn = 3/8, yağmurlu olma ihtimali Pnr = 6/8
 
#### Örnek

- Prr = 0.4
- Prn = 0.6
- Pnr = 0.2
- Prr = 0.8

Bunu şöyle gösterebiliriz:

![image](https://user-images.githubusercontent.com/12685802/149081262-d2baf9f4-af4f-4b57-ad52-53ae23fdfef0.png)

### Coke vs Pepsi

Şöyle bir modelimiz var:

![image](https://user-images.githubusercontent.com/12685802/149081380-6314072d-3d63-46ad-b4cd-b17b1efdaaca.png)

P tablomuz şu şekilde olur:

![image](https://user-images.githubusercontent.com/12685802/149081452-35c5004b-a0c8-462a-9d6a-5b369616b0fd.png)

- Pepsi alan birinin Coke alma ihtimali nedir?

p(CC | P) = 0.2 x 0.9

![image](https://user-images.githubusercontent.com/12685802/149081593-0763ba74-cb4f-4f6a-b452-db700270a55c.png)

- Herhangi bir şey içen birinin önce kendi içtiğini içip sonra Coke içme ihtimali nedir?

p(XC | P) = p(CC | P) + p(PC | P) = 0.2 x 0.9 + 0.8 x 0.2

- Pepsi içen birinin 2 adım sonra Coke içme ihtimali nedir?

![image](https://user-images.githubusercontent.com/12685802/149082630-a334a61a-9607-498b-8b66-6009d63bd709.png)

p(XC | P) = P(PC | P) + P(CC | P) = 0.8 x 0.2 + 0.2 x 0.9 = 0.34

- Coke içen birinin 3 adım sonra Pepsi içme ihtimali nedir?

p(XXP | P) = p(PPP | P) + p(CPP | P) + p(CCP | P) + p(PCP | P) = 0.219

![image](https://user-images.githubusercontent.com/12685802/149083178-fe78b6f8-fe5d-40a1-800e-7b3e1750f944.png)

Bu işlemlere Markov Zinciri denir.

#### Örnek

![image](https://user-images.githubusercontent.com/12685802/149083399-fc86eb9e-6603-4e9a-80e0-332ac57569b2.png)

![image](https://user-images.githubusercontent.com/12685802/149083504-4f394f64-a5a7-48aa-b163-cb0536301614.png)

### Örnek

Bir kumar oyununda, oyuncunun cebinde 10$ var.

- Her kazandığında 1$ kazanıyor, p ihtimalle
- Her kaybettiğinde 1$ kaybediyor, 1-p ihtimalle
- Oyun, oyuncunun parası bittiğinde veya 100$ sahibi olduğunda bitiyor.

Olası sorular:

- Bu oyuncunun iflas etme ya da 100$ kazanma ihtimalini hesaplayabilir misiniz?
- Kazancın zarardan çok olması için p değerinin kaç olması gerekir?

![image](https://user-images.githubusercontent.com/12685802/149084195-6f0d4fee-d805-4483-86c2-b4ad5f694619.png)

### CpG Adaları

![image](https://user-images.githubusercontent.com/12685802/149085494-799298f1-5d97-4b77-9619-9c6dae1daae4.png)

İnsan genomunda CG dinucleotitleri az. 

Promotor CG bölgeleri çok.

![image](https://user-images.githubusercontent.com/12685802/149085639-5a8d1b4a-cf31-412f-b7b9-d02d8bdf224a.png)

---

[<< Geri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta13.md)

[>> İleri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/README.md)
