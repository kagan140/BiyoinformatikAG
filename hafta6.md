# Biyoinformatik Algoritmalara Giriş
## Hafta 6

İkiz kardeşler hariç sekanslarda tam benzerlik bulamayız.

![image](https://user-images.githubusercontent.com/12685802/144854053-30ea1e72-1169-4765-a0ed-943a723763cf.png)

Sekanslara öyle boşluklar ("-" işareti) atacağım ki maksimum eşleşmeyi sağlayacağım, peki nereye boşluk atacağımı nasıl hesaplayabilirim?

---

### Hamming Distance
https://bilgisayarkavramlari.com/2008/08/05/hamming-mesafesi-hamming-distance/

![image](https://user-images.githubusercontent.com/12685802/144856822-5efc99ad-e2e6-4306-bd85-06f249637473.png)

Hamming mesafesi aynı uzunluktaki iki string arasında, birbirine dönüşmesi için gerekli olan yer değiştirme sayısını verir.

Yani basitçe bir dizginin diğer dizgiden ne kadar farklı olduğunu gösterir.

- 100011101 <-> 100101101 = 2
- düğün <-> düşün = 1

---

### Edit Distance: Recursive

#### Sözde Kod:

![image](https://user-images.githubusercontent.com/12685802/144857224-3dd10198-bf76-4e63-bb65-aa40548bc86e.png)

#### Python Örneği:

![image](https://user-images.githubusercontent.com/12685802/144857376-f609a65b-c514-4e48-be0a-62c4e15141a8.png)

Formüllerde veya kodda kastedilen şey şudur:

- Kırmızı çarpının değeri 
  - Yeşil oklardan gelirken ceza/ödül alarak
  - Diagonelden (mavi ok) gelerek
 en küçük sonuç hangisi olduğuna göre belirlenir.
 
![image](https://user-images.githubusercontent.com/12685802/144857749-ada7effe-ba9b-4b1c-8aa1-f00ee41e5968.png)

Bazı alt ağaçlar tekrarlanır. Bu istenilen bir durum değildir.

![image](https://user-images.githubusercontent.com/12685802/144859500-ef5d4f6f-7754-4baa-9072-52c94c3d796d.png)

Tekrar hesaplamadan kaçınmak için veriler hafızada tutulur. Bu da verilerin hafızada tutunulmasının örneği, evet dinamik programlamayla aynı. 🙂

![image](https://user-images.githubusercontent.com/12685802/144859865-cc3b1d3e-bf5f-45a5-86ca-036ad2a5c3e6.png)


### Edit Distance: Dynamic Programming

#### Sözde Kod:

![image](https://user-images.githubusercontent.com/12685802/144860032-a77adc36-5569-43ae-8e1f-e7debede2a15.png)

#### Python Örneği:

![image](https://user-images.githubusercontent.com/12685802/144860241-1e88adae-03e4-4710-b385-7b8efa38022d.png)

#### Örnek:

![image](https://user-images.githubusercontent.com/12685802/144860671-e7eb7654-3cb3-4c64-9276-575e4087c0b1.png)

D[6,6] kutucuğunun hesaplanması için:
- D[5,6]+1
- D[6,5]+1
- D[5,5]+ delta(x[i-1],y[j-1]) = yani diyagonele bak diyor.

Minimum değer kutucuğa yazılır.

#### Örnek:

![image](https://user-images.githubusercontent.com/12685802/144863256-d92fd8f2-57c3-4e3b-ad36-40b064c64bc0.png)

G=G olduğundan, delta = 0.

D[1,1] = min(
- D[1,0]+1 = 2
- D[0,1]+1 = 2
- D[0,0]+ delta = 0

) = 0

Böylece D[1,1] kutucuğuna 0 yazılır.

Bu şekilde her kutucuk dolduruldutkan sonraki tablonun görseli:

![image](https://user-images.githubusercontent.com/12685802/144863748-a7896dfc-057a-4bf5-8665-e94273a766b3.png)


---

[<< Geri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta5.md)

[>> İleri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta7.md)

