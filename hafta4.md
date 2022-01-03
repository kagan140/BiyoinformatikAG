# Biyoinformatik Algoritmalara Giriş
## Hafta 4

### Shift-AND ve Shift-OR Algoritması:

Pattern: ATGAG

DNA alfabemde 4 eleman var. O zaman 4 adet maske üretelim:

- M(A) = 10010 (A--A-)
- M(C) = 00000 (-----)
- M(G) = 00101 (--G-G)
- M(T) = 01000 (-T---)
- Text: ATGCTGACCT

5 karakter okumak yerine tek karakter okuyor.

A'yı aldık diyelim. Onun maskesini alıyor (10010) ve bir sağa kaydırıyor. 01001.

Sonra T'yi al maskesiyle işleme tabii tut ve böyle devam et.

https://www.youtube.com/watch?v=uJezLnFUZ48

Paralel çalıştırmayı sağlar.

#### Bitmask table oluşturma.
Shift-OR algoritması içindir.

![image](https://user-images.githubusercontent.com/12685802/147957316-9a05bb14-750d-49fb-bb26-699be49155cf.png)

#### Algoritmanın İşleyişi

![image](https://user-images.githubusercontent.com/12685802/144756838-4aedc6f4-1aa9-4d3c-b8fd-292e8d18f106.png)

![image](https://user-images.githubusercontent.com/12685802/144756835-43b8725e-9626-48d4-853a-923c1a6f01b4.png)

![image](https://user-images.githubusercontent.com/12685802/144756762-1dea3479-9577-4366-be78-bb48594c4e20.png)

![image](https://user-images.githubusercontent.com/12685802/144756776-51aabf25-3855-4e3b-86f9-7c8e08902c73.png)

#### Örnek

![image](https://user-images.githubusercontent.com/12685802/144767843-153918c4-3c62-47bf-b520-ac81884af6d3.png)

Aranan Pattern: aaba

- a'nın maskesi: 0100
- b'nin maskesi: 1011

State (başlangıç), D: 1111 

Kontrol edilen karakter: a

Kontrol edilen karakterin maskesi: 0100

D << 1: State'e 1 karakter left shiftliyoruz. 1110 oluyor.

Ve D << 1 ile karakterimizin maskesini OR işlemine tutuyoruz. 0100 | 1110 = 1110, bu yeni stateimiz olucak.

![image](https://user-images.githubusercontent.com/12685802/144767989-70ffde27-f50b-48d8-a848-a431a4f8296c.png)

State: 1110

Kontrol edilen karakter: a

Kontrol edilen karakterin maskesi: 0100

D << 1: State'e 1 karakter left shiftliyoruz. 1100 oluyor.

Ve D << 1 ile karakterimizin maskesini OR işlemine tutuyoruz. 0100 | 1100 = 1100

![image](https://user-images.githubusercontent.com/12685802/144768036-08754a87-8874-458d-9058-2f8b7f340887.png)

State: 1100

Kontrol edilen karakter: b

Kontrol edilen karakterin maskesi: 1011

D << 1: 1000

Ve 1011 | 1000 = 1011

![image](https://user-images.githubusercontent.com/12685802/144768062-f23ea633-44b5-413a-b305-380c53d87f91.png)

State: 1011

Kontrol edilen karakter: a

Kontrol edilen karakterin maskesi: 0100

D << 1: 0110

Ve 0100 | 0110 = 0110

State'te en soldaki karakterin 0 olması patternin bulunduğu anlamına gelir.

#### Örnek

![image](https://user-images.githubusercontent.com/12685802/144768253-644b5250-4295-40e1-aaf6-579a5baf9d89.png)

- a: 0 0 1 --> Maskesi 100
- b: 1 1 0 --> Maskesi 011

State (başlangıç), D: 111

Kontrol edilen karakter: a

Kontrol edilen karakterin maskesi: 100

D << 1: State'e 1 karakter left shiftliyoruz. 110 oluyor.

Ve D << 1 ile karakterimizin maskesini OR işlemine tutuyoruz. 100 | 110 = 110, bu yeni stateimiz olucak.

State, D: 110

Kontrol edilen karakter: a

Kontrol edilen karakterin maskesi: 100

D << 1: State'e 1 karakter left shiftliyoruz. 100 oluyor.

Ve 100 | 100 = 100, yeni state olucak.

State, D: 100

Kontrol edilen karakter: a

Kontrol edilen karakterin maskesi: 100

D << 1: State'e 1 karakter left shiftliyoruz. 000 oluyor.

Ve 100 | 000 = 100, yeni state olucak.

State, D: 100

Kontrol edilen karakter: b

Kontrol edilen karakterin maskesi: 011

D << 1: State'e 1 karakter left shiftliyoruz. 000 oluyor.

Ve 011 | 000 = 011, en soldaki bit 0 olduğundan eşleşme var.

---

BNDM algoritması

Rabin-Karp/Fingerprint

---

[<< Geri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta3.md)

[>> İleri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta5.md)
