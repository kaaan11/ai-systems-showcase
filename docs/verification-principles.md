# Doğrulama ilkeleri

Bu vitrindeki projelerin ortak tezi tek cümleyle:

> **Bir etiket, altındaki işin yapıldığının kanıtı değil, yalnızca iddiasıdır.**

Aşağıdaki ilkelerin her biri bir tercihten değil, **bir hatadan** doğdu. Her
maddenin altında onu doğuran ölçüm var.

## 1. Etiket kanıt değildir

`DONE`, `PASS`, `RESOLVED`, `IN_PROGRESS` — hepsi iddiadır. Aktarmadan önce
içeriğinin o etiketi hak ettiği doğrulanır.

*Doğuran ölçüm:* Üç ayrı yerde aynı gün: `DONE` işaretli bir görevin değişiklik
listesi boştu; `DONE` işaretli iki tasarım kaydının üretimde çağıranı yoktu;
`IN_PROGRESS` bir görevin gövdesi şablon metniydi. Üçünü de ölçüm yakaladı,
hiçbirini etiket yakalamadı.

## 2. Geçen test, doğru şeyi ölçtüğünün kanıtı değildir

Bir testin kusuru gerçekten yakaladığı, **kusurlu kodu geri koyup testin
düştüğü görülerek** kanıtlanır.

*Doğuran ölçüm:* Bir determinizm testi aynı süreçte tekrar çağrı yapıyordu; hash
tohumu süreç başına sabit olduğu için bozuk kodda da geçiyordu. Başka bir vakada
bir test, yakaladığını iddia ettiği kusuru değil, kusurun **yan etkisini**
ölçüyordu.

## 3. Bir modelin çıktısı, kendi iddiasının kanıtı olamaz

Bir modelin "yaptım" demesi, yapıldığının kanıtı değildir. Kanıt bir
`dosya:satır`, bir test kimliği veya bir komut logudur.

*Uygulanışı:* Partitür'ün denetim şemasında `worker_says` diye bir kanıt tipi
yoktur ve eklenmeyecektir. Bir worker'ın özeti, kayıt sisteminde
`MODEL_ASSERTION` sınıfına girer — yani *o iddianın yapıldığının* kanıtıdır,
iddianın doğruluğunun değil.

## 4. Yokluk kanıt değildir

Sıfır bulgu, güvenlik kanıtı değildir. Sınır çalıştırılmadan alınan temiz sonuç,
yalnızca sınırın çalıştırılmadığını gösterir.

*Uygulanışı:* "Kıramadım" bir iddiadır ve kanıtı **denemelerin logudur**. Bir
tarama aracının çökmesi, `could-not-scan` sonucu üretmeli ve sıfırdan farklı bir
çıkış kodu döndürmelidir — yoksa çağıran onu "temiz" sanar.

## 5. Tespit ile doğrulama aynı şey değildir

`detection` bir adaydır. `confirmed` bir kanıttır. İkisi tek sayıda birleşmez.

*Doğuran ölçüm:* Bir tarayıcı kendi geliştirme setinde **15/15 detection** ve
**0/15 confirmed** verdi. İki sayıyı da yazmak, ilkini yazıp ikincisini
atlamaktan daha az etkileyici ve daha doğrudur.

## 6. Kendi türetme setindeki sonuç doğrulama sayılmaz

Bir politikayı üreten veri, o politikayı doğrulayamaz. Held-out set olmadan
genelleme yapılmaz.

*Doğuran ölçüm:* Bir yönlendirme politikası kendi türetme setinde tutarlı
sonuçlar verdi. Held-out bir hedefte ölçüldüğünde, politikanın dayandığı temel
gözlem **tersine döndü** — çünkü türetme setindeki görev metinleri, ölçülen
davranışı yapay olarak gereksiz kılıyordu.

## 7. Çökme, tek başına güvenlik bulgusu değildir

Bir bulgu için üç şart birden gerekir: **yasak etki adlandırılmış**, etki
**tekrar üretilmiş**, ve **normal kontrol** aynı yolda çalışıp etkiyi
üretmemiş. Üçü yoksa elde bir gözlem vardır, bulgu yoktur.

## 8. Bir düzeltme, sözü değiştiremez

Bir iş başarısız olduğunda düzeltilen şey **nasıl yapıldığıdır**, ne söz
verildiği değil. Sınavı geçemeyince soruyu değiştirmek, düzeltme değildir.

*Uygulanışı:* Partitür'de kazanım listesi dondurulur ve karması kaydedilir.
Düzeltme turu görevleri değiştirebilir; kazanımlara dokunan bir öneri
**tümüyle reddedilir**, ayıklanmaz.

## 9. Ölçüm sırasında ölçüm aleti tamir edilmez

Bir kampanya sırasında bulunan kusur kaydedilir, düzeltilmez. Aleti çalışırken
onarmak, ölçtüğü şeyi değiştirir.

## 10. Başarısızlık da yayımlanır

Bu vitrinin en somut örneği: Partitür ilk gerçek kampanyasında kendi motoruna
koşturuldu ve **işi bitiremedi** — üç kazanımın üçü de kanıtlanmadı, birleştirme
reddedildi, ve kampanyanın dayandığı öncül ölçüm sonucu çürüdü.

Ayrıntısı: [başarısız kampanya](../examples/failed-campaign.md).
