# Biyoinformatik Algoritmalara Giriş
## Hafta 5

Genom bilgisini çıkarmak için insanlar Bowtie diye bir algoritma geliştiriyolar. Bowtie diye bir platform varmış vs... 

### Burrows-Wheeler Algoritması 

https://www.youtube.com/watch?v=Lc-ACiJIrnM

#### Transform İşlemi 

banana karakterleri şu şekilde yazılır -->
- banana$                   
- anana$b
- nana$ba
- ana$ban
- na$bana
- a$banan
- $banana

Ardından bu durumlar sıralanır.
- $banana
- a$banan
- ana$ban
- anana$b
- banana$                   
- na$bana
- nana$ba 

Son karakterlerin yan yana yazılmış hali BWT(banana) işlemninin sonucudur.

Yani BWT(banana) = annb$aa

#### Transform İşlemi Çözümleme İşlemi 1. Yöntem

Diyelim ki elimizde BWT transform hali var. Bundan kelimeye için geri dönmek için:

- Çözümleyeceğimiz kelimenin transform edilmiş hali 7 karakter olduğu için dolar karakterini çıkarırsak 6 karakterden oluştuğunu anlayabiliriz. Bunu akılda tutuyoruz.
- annb$aa karakterleri alfabetik sıraya göre yazılır ve transform hallerin yanlarına eklenir.

Yani:
- a$
- na
- na
- ba
- $b
- an
- an

Ardından tekrar sıralama yapılır.
- $b
- a$
- an
- an
- ba
- na
- na

Sonra yanlarına (sol yanlarına) tekrar transform form eklenir:
- a$b
- na$
- nan
- ban
- $ba
- ana
- ana

Tekrar sıralama yapılır.
- $ba
- a$b
- ana
- ana
- ban
- na$
- nan

Ardından yanlarına transform form eklenir:
- a$ba
- na$b
- nana
- bana
- $ban
- ana$
- anan

Bu iki işlem sürekli devam ettirilir:
- $ban
- a$ba
- ana$
- anan
- bana
- na$b
- nana
- ->
- a$ban
- na$ba
- nana$
- banan
- $bana
- ana$b
- anana
- ->
- $bana
- a$ban
- ana$b
- anana
- banan
- na$ba
- nana$
- ->
- a$bana
- na$ban
- nana$b
- banana
- $banan
- ana$ba
- anana$
- ->
- $banan
- a$bana
- ana$ba
- anana$
- banana
- na$ban
- nana$b
- ->
- a$banan
- na$bana
- nana$ba
- banana$
- **$banana**
- ana$ban
- anana$b

Ve burada dolarla başlayan kelime textimizdir. 6 karakterden oluştuğunu ilk başta nasıl anladığımızı söylemiştik.

#### Transform İşlemi Çözümleme İşlemi 2. Yöntem

Aslında yukarıdaki kadar uzun sürmesine gerek yoktu. Çünkü aslında her sıralanmışların yanına transform hali eklenilmiş stringler kelimenin içinde bulunan stringler. Dediğimi aşağıdaki örneği inceleyerek ne kadar koaly olduğunu anlayabilirsiniz, cümleyi toparlaması biraz zor.

- annb$aa karakterleri alfabetik sıraya göre yazılır ve transform hallerin yanlarına eklenir.

Yani:
- a$
- na
- na
- ba
- $b
- an
- an

Elde ettiğimiz bilgiler:
- Yedi satırdan oluşması kelimenin 6 karakterli olduğunu söylüyor. **------**
- İlk satır kelimenin a ile bittiğini söylüyor. **-----a**
- Beşinci satır kelimenin b ile başladığını söylüyor. **b----a**
- Dördüncü satır kelimenin bir yerinde b'den sonra a geldiğini söylüyor. **ba---a**
- Altıncı satır kelimenin bir yerinde a'den sonra n geldiğini söylüyor. **ban--a**
- İkinci satır kelimenin bir yerinde n'den sonra a geldiğini söylüyor. **bana-a**
- Yedinci satır kelimenin bir yerinde daha a'den sonra n geldiğini söylüyor. **banana**
- Üçüncü satır kelimenin bir yerinde daha n'den sonra a geldiğini söylüyor. **Bu da doğru yaptığımızı doğruluyor.**

---

DNA alfabesi = {A,T,G,C}, 1953.. Watson Crick modeli 

DNA metinlerinde örüntü yakalamamız gerekiyor

Veri kaynağımız var mı?
- FASTA formatlı dosyalar.

Tam benzerlik için:

- 1970'li yıllar Knuth Morris Pratt, Boyer Moore algoritmaları

- 1980'li yıllar: Shift AND algoritması ile bit seviyesinde hizalama (makine seviyesinde)

- 1990 sonrası: BNDM, hem bitwise hem de gereksiz frame atlıyor.

Sonuçta İnsanoğlu küçük hücreli canlıların DNA'sını çözüyor.

Bize fazlası lazım, insan genomunu çözme problemi (2000 yılı)

Burrows Wheeler'in veri sıkıştırma algoritmasını incelememiz lazım. (FM index)

Her zaman tam benzerlik bulamayabiliriz. Dinamik programlama

Bir dokunun DNA analizini yapılma süreci:

Olmayan şey: Dokuda 3 milyarlık DNA'yı olduğu gibi gören mikroskop 

Text: uzunluğu 3.2 milyar bp

Pattern: uzunluğu 150 bp

Tam benzerlik yetmiyor. DNA'ların tamamı aynı olamaz. Yaklaşık benzerlik bulma da yapmamız lazım. 

**Longest common subsequence problem**

Dinamik programlama
- Smith Waterman algoritması: İki sekans arasındaki küçük ve ortak özellikleri arar. Örnek: Bezelye ile Çam dna'sını aldınız diyelim ortak kısımları aramaya yarar.
- Needleman Wunsh algoritması:  İki sekansının yüzde kaç örtüştüğünü verebilir.

Haftaya ayrıntılı açıklanacak.

---

[<< Geri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta4.md)

[>> İleri](https://github.com/LIIIs4ma/BiyoinformatikAG/blob/main/hafta6.md)

