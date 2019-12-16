10 Time State

# Time State

Genellikle, birden fazla işte  veya canlı döngüde paylaşılan bilgilerin olması yararlıdır. Örneğin, mevcut anahtar, BPM veya mevcut 'karmaşıklık' (hatta farklı başlıklar arasında farklı şekillerde potansiyel olarak yorumlayacağınız) gibi daha soyut kavramları paylaşmak isteyebilirsiniz. Aynı zamanda mevcut "determinizmimizi" de kaybetmek istemiyoruz, bunu yaparken de garanti veriyoruz. Başka bir deyişle, kodu başkalarıyla paylaşabilmeyi ve çalıştırdıklarında tam olarak ne duyacaklarını bilmek istiyoruz. Bu eğitimin yani 5.6'ıncı bölümünün sonunda, determinizm kaybı nedeniyle (yarış koşulları nedeniyle), konuları paylaşmak için değişkenleri neden kullanmamamız gerektiğine kısaca değindik.

Sonic Pi'nin küresel değişkenlerle belirleyici bir şekilde kolayca çalışabilme problemine çözümü, "Time State" adını verdiği yeni bir sistemdir. Bu kulağa karmaşık ve zor gelebilir (aslında, İngiltere'de birden fazla iş için ve paylaşılan hafıza ile programlama tipik olarak üniversite düzeyinde bir konudur). Ancak, göreceğiniz gibi, ilk notunuzu çalmak gibi, Sonic Pi, programlarınızı güvenli ve kararlı bir şekilde tutarken aynı zamanda konuları paylaşmayı inanılmaz derecede kolaylaştırıyor.
Meet `get` and `set`...
