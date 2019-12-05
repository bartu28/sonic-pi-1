4 Rasgeleleştirme

# Rastgeleleştirme

Müziğinizi ilgi çekici yapma yollarından biri de bazı rastgele sayılar
kullanmaktır. Sonic Pi, müziğinize rastgele sayılar koymanızı sağlayan
fonksiyonlar bulundurur, ama bunu kullanmaya başlamadan önce sizi şok
edebilecek bir gerçek: Sonic Pi ’de *rasgele tamamen rastgele değil*.
Ama bu ne demek oluyor? Tamam, bir göz atalım.
A great way to add some interest into your music is using some random
numbers. Sonic Pi has some great functionality for adding randomness to
your music, but before we start we need to learn a shocking truth: in
Sonic Pi *random is not truly random*. What on earth does this mean?
Well, let's see.

## Tekrarlanabilirlik

`rrand` fonksiyonu çok işlevsel bir rasgele fonksiyonudur. Bu fonksiyon
2 değer arasında rastgele bir değer verir. Bir minimum min ve bir
maksimum max. (rrand rasgele için bir kısaltmadır). Şimdiki değer
arasında rasgele bir nota çalmayı deneyelim:

```
play rrand(50, 95)
```

Vay canına! Rasgele bir nota çaldı!`83.7527` notasını çaldı. 50 ve 95
arasında güzel rasgele bir nota... Vay canına. Bir saniye, az önce
senin de aldığın rasgele nota aynı mı? Burada bir gariplik var. Kodu
tekrar dene. Ne? tekrar 83.7527? Bu rasgele olamaz!

Cevap şudur ki bu rasgele değil, bu pseudo-random(“random” rasgele
demek). Sonic Pi sana rasgele bir numarayı tekrarlanabilir bir şekilde
verir. Bu senin kodladığın bir müziği herkesin aynı şekilde dinlemesini
sağlar. Rasgele bir değer kullanmış olsan bile.

Tabiki eğer ‘rasgele’ bir şey her zaman `83.7527` olacaksa bu ilgi çekici
olmaz. Neyseki bu bunun için geçerli değil:

```
loop do
  play rrand(50, 95)
  sleep 0.5
end 
```

Evet! Sonunda rasgele bir şey. *run* içindeki bir rasgele fonksiyonu hep
rasgele değerler vermeye değer verir. Ama bir sonraki çalıştırmada
yine aynı değerleri verir ve aynı duyulur. Bu her "run" tuşuna
bastığımızda zamanda geri gidip tekrar basmışız gibi olur.
Yes! It finally sounds random. Within a given *run* subsequent calls
to random functions will return random values. However, the next run
will produce exactly the same sequence of random values and sound
exactly the same. It's as if all Sonic Pi code went back in time to
exactly the same point every time the Run button was pressed. It's the
Groundhog Day of music synthesis!

## Lanetli Ziller

Rasgeleleştirmenin güzel başka bir örneği de `:perc_bell` sesini rasgele
bekleme ve hız değerleri ile tekrarlayan lanetli ziller örneğidir:

```
loop do
  sample :perc_bell, rate: (rrand 0.125, 1.5)
  sleep rrand(0.2, 2)
end
```

## Random cutoff

Eğlenceli başka bir rastgeleleştirme örneği ise bir synth 'in
sesinin kesme zamanını değiştirmektir. Bunu deneyebileceğimiz
güzel synthlerden biri `:tb303` emulatörüdür.

```
use_synth :tb303

loop do
  play 50, release: 0.1, cutoff: rrand(60, 120)
  sleep 0.125
end
```

## Rastgele seed ‘ler

Peki Sonic Pi ın size sunduğu bu sıralanmış rastgele numaraları
beğenmezseniz ne olacak? Tamam, `use_random_seed` ile başka bir
başlangıç noktası seçebilmemiz tamamen mümkün. Varsayılan
seediniz 0 dır, yani farklı bir seed seçerseniz başka bir
deneyiminiz olur!

Mesela bu örneğe bir bakın:

```
5.times do
  play rrand(50, 100)
  sleep 0.5
end
```

Bu kodu her çalıştırdığınızda, sıralanmış aynı 5 notayı
duyarsınız. Farklı bir sıra duymak için basit bir şekilde
seed imizi değiştirebiliriz:

```
use_random_seed 40
5.times do
  play rrand(50, 100)
  sleep 0.5
end
```

Bu bize farklı bir sıra verir. Seed leri değiştirerek ve
dinleyerek bir seed de karar kılabilirsiniz ve bu kodu biri
ile paylaştığınızda o da aynı şeyi duyar.

Bir de diğer işe yarayan rastgele fonksyonlarına bakalım.


## choose     (seç)

Çok yaygın şeylerden biri bir listeden bir şey seçmektir. Mesela,
bu notalardan birini seçmek isteyebilirim: 60, 65 veya 72. Bir
listeden bir şey seçmemi yarayan `choose` fonksiyonu ile bunu
yapabilirim. İlk olarakbir liste oluşturmalıyım. Bunu köşeli
parantezlerin içine değerler koyup bu değerleri virgül ile
ayırarak yapabilirim:`[60, 65, 72]`. Sonrasında ise basitçe bunları
`choose` fonksiyonuna vermeliyim:

```
choose([60, 65, 72])
```

Nasıl duyuluyor bir dinleyelim:

```
loop do
  play choose([60, 65, 72])
  sleep 1
end
```

## rrand

`rrand` ı çoktan görmüştük ama bir daha bakalım. Sadece iki değer arasında
bir değer veriyor. Bu max değeri veya min değeri asla vermeyeceği
anlamına geliyor(sadece iki değer arasındaki değerleri veriyor).
Numaralar her zaman küsüratlı yani tam bir sayı olmadığı anlamına
geliyor. `rrand(20, 110)` fonksiyonunun verdiği küsüratlı sayılar
örnekleri:

* 87.5054931640625
* 86.05255126953125
* 61.77825927734375

## rrand_i

Bazen küsüratsız bir sayı elde etmek isteyebiliriz. Bu durumda
`rrand_i` fonksiyonu bizi kurtarıyor. `rrand` fonksiyonu gibi çalışıyor
ama min ve max değerlerini de rastgele numaralar olacak şekilde
verebiliyor. `rrand_i(20, 110)` fonksiyonunun verdiği değerler örneğin
bunlar olabiliyor:

* 88
* 86
* 62

## rand

Bu, 0 (dahil) ile belirttiğiniz maksimum değer (hariç) arasında
rastgele bir değişken döndürür. Varsayılan olarak 0 ile 1 arasında
bir değer verir. Bu yüzden rastgele `amp:`değerlerini almak için
kullanışlıdır:

```
loop do
  play 60, amp: rand
  sleep 0.25
end
```

## rand_i

Similar to the relationship between `rrand_i` and `rrand`, `rand_i` will
return a random whole number between 0 and the max value you specify.

## dice

Sometimes you want to emulate a dice throw - this is a special case of
`rrand_i` where the lower value is always 1. A call to `dice` requires
you to specify the number of sides on the dice. A standard dice has 6
sides, so `dice(6)` will act very similarly - returning values of either
1, 2, 3, 4, 5, or 6. However, just like fantasy role-play games, you
might find value in a 4 sided dice, or a 12 sided dice, or a 20 sided
dice - perhaps even a 120 sided dice!

## one_in

Finally you may wish to emulate throwing the top score of a dice such
as a 6 in a standard dice. `one_in` therefore returns true with a
probability of one in the number of sides on the dice. Therefore
`one_in(6)` will return true with a probability of 1 in 6 or false
otherwise. True and false values are very useful for `if` statements
which we will cover in a subsequent section of this tutorial.

Now, go and jumble up your code with some randomness!
