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
- Needleman Wunsh algoritması:  İki sekansının yüzde kaç benzeştiğini verebilir.
