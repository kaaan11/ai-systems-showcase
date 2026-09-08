# Yapay zekâ ile çalışma yöntemi

Bu vitrindeki sistemler bir kişi tarafından, birden çok modele iş dağıtılarak
inşa edildi. Aşağıdaki yöntem tasarlanarak değil, **hatalardan damıtılarak**
oluştu; her maddenin altında onu doğuran ölçüm var.

Tek cümlelik özeti: **modele iş yaptırmak ucuz, yaptığını doğrulamak pahalıdır —
ve yöntemin tamamı bu pahalı kısmı ehlileştirmekle ilgilidir.**

---

## Döngü

```
şartname  →  delegasyon  →  bağımsız doğrulama  →  mutasyonla kanıt  →  kayıt
```

Her adım bir öncekinin çıktısını **güvenilmeyen veri** olarak alır. Hiçbir
adımda "model öyle dedi" bir gerekçe değildir.

### 1. Şartname

Her iş, kendi kendine yeten bir şartname ile başlar: bağlam sıfırdan kurulur,
başka bir sohbete atıf yapılmaz. İçinde şunlar bulunur:

- **Bağlayıcı kurallar** — tercihler değil, projenin varlık sebebi olan kısıtlar.
- **Görevler**, her biri açık imza listesiyle. *Dönüş tipi tam verilir;
  düzyazıda anlatılıp imzada belirtilmeyen bir şey istenmemiş sayılır.*
- **Adı belli kabul kapıları** — "iyi çalışsın" değil, "bozuk JSON'da sessizce
  boş dönmüyor, hata veriyor".
- **Yapılmayacaklar listesi.**
- **Bitti sayılma koşulu**, ölçülebilir maddeler halinde.

### 2. Delegasyon

Ölçüt tek cümle:

> **Nesnel bir kabul kapısı yazabiliyorsan alt modele ver.
> Kapının kendisine karar vermek gerekiyorsa kendin yap.**

Bu ölçüt bazen "hiçbirini delege etme" der ve o zaman delege edilmez. 3172
satırlık bir kod taşımasında ölçüt uygulandığında sonuç şuydu: doğruluğu
kanıtlanmış kodu bir modele yeniden yazdırmak, çalışan koda **transkripsiyon
riski eklemekten** başka bir şey yapmaz.

### 3. İkili delegasyon

Saf, tek dosyalık, imzası açık görevler **aynı şartnameyle iki bağımsız modele**
gönderilir ve çıktılar önce birbirine karşı okunur.

> **İki bağımsız uygulamanın anlaştığı yer, şartnamenin sessiz kaldığı yerdir.**

*Doğuran ölçüm:* Bir modül iki modele verildi. İkisi de aynı kimlik için iki
çelişkili kayıt taşıyan bir girdiyi sessizce çözdü — biri ilkini aldı, diğeri
sonuncusunu. İkisinin de testleri geçiyordu; ikisi de yanlıştı. Tek çıktı
verildiğinde bu bir *tercih* gibi görünür; iki çıktı yan yana konduğunda
*boşluk* olduğu görülür. Birleştirilen modül artık o girdiyi reddediyor:
denetimin varmadığı bir hükmü modül icat edemez.

Aynı desen ikinci bir fazda tekrarlandı. Yöntem tesadüf değil.

### 4. Bağımsız doğrulama

Alt model çıktısı **yeşil koşuyla kabul edilmez**. Rapordaki her olgusal ve
sayısal iddia kaynağından doğrulanır: kod açılır, test koşturulur, hedef sayılır.

*Doğuran ölçüm:* Bir raporda üç kusurun üçü de "yapıldı" diye geçiyordu.
Belgede "en yaygın üç" yazan yer kodda rastgele seçim yapıyordu; adı
"determinizm" olan test ölçtüğü şey o değildi; "yalnız `.ts` dosyaları" denen
hedefte `.js` de vardı. Üçü de ancak bağımsız ölçümle çıktı.

### 5. Mutasyonla kanıt

Bir testin kusuru gerçekten yakaladığı, **kusurlu kodu geri koyup adı geçen
testin düştüğü görülerek** kanıtlanır. Kabul kapısı başına en az bir mutasyon,
listesi commit mesajında.

Bu disiplinin en değerli anı, mutasyonun **kırmızıya dönmediği** andır:

> Bir çıktı redaksiyon katmanında "önce redakte et, sonra kırp" mutasyonu
> uygulandı ve test geçmeye devam etti. Sebep, mutasyonun doğru sıra olmasıydı;
> kod yanlıştı. Çıktı sondan saklandığı için kesim sınırını aşan bir sır
> `api_key=` önekini kaybediyor, redaksiyon deseni de tam o öneke bakıyordu.
> Ölçüldü: `önce kırp → sızıntı var`, `önce redakte → sızıntı yok`.

Mutasyon disiplini böylece ters yönde de çalışır: testin zayıflığını değil,
kodun yanlışlığını gösterir.

---

## Şartname, zincirin en zayıf halkasıdır

Dört fazlık bir çalışmanın sonunda ölçülen şey şu oldu: **kusurların çoğu koddan
değil, şartnameden çıktı.** Üç örnek, üçü de aynı yazarın:

| Hata | Sonucu |
| --- | --- |
| Envanter eksik bir aramayla çıkarıldı ve *"ölçüldü, tahmin değil"* diye sunuldu | Dört ifade gerçeğe dayanmadı; uygulayan taraf kaynağa karşı ölçüp düzeltti |
| İmza `-> str` dedi, düzyazı "hüküm ve gerekçe" istedi | Çözüm bir `str` alt sınıfı oldu; `json.dumps` etiketi koruyup gerekçeyi **sessizce** düşürüyordu |
| Şartname, ürünün **yapamadığı** bir akışı "atlanmayacak" ilan etti | İki adımın komut satırı karşılığı yoktu; akış elle bağlanmak zorunda kalındı |

Çıkarılan kural: şartname yazan taraf da doğrulanır, ve şartnamenin kendisi bir
kabul kapısına tabidir.

### Ve şartname ölçümü kirletebilir

Bir kampanyada üç olası politika şekli şartnameye yazılıp biri önerildi. Sonuçta
planlayıcı modelin **muhakeme mi ettiği yoksa öneriyi mi tekrarladığı**
ayrılamaz hale geldi. Aynı şey kanıt tipi tercihi için de oldu: kural prompt'a
konduğu için ölçülen şey alışkanlık değil **itaat** oldu.

> Ölçmek istediğin şeyi şartnameye yazarsan, ölçemezsin.

---

## Ölçüm hijyeni

Sonuç, alındığı ortam kadar geçerlidir.

- **Temiz kabuk.** Testler `PYTHONPATH` ayarlı bir kabukta koşturulmaz. Bir
  paket taşınırken geride kalan tek bir `import` yüzünden suite yeşil göründü;
  temiz kabukta düşüyordu.
- **Konsol komutu ayrıca denenir.** "pytest yeşil" ile "kurulu komut çalışıyor"
  aynı şey değildir. Bir fazın tamamlandığı sanıldı, oysa paket sanal ortama
  hiç kurulmamıştı; testler yalnızca kök dizin eklendiği için geçiyordu.
- **Doğrulayan da ortamı kirletebilir.** Bir doğrulama sırasında `/tmp` altında
  bırakılan bir dizin, yukarı doğru yürüyen bir kök arayıcısını yanılttı ve üç
  test düştü. Kusur kodda değil, ölçende idi.

---

## Kayıt

**Şartname, ne istendiğinin kaydıdır ve yapılana uydurulmaz.** Bir uygulama
şartnameden saparsa, sapma raporlanır; şartname geriye dönük düzeltilmez.
Kaydı yapılana uydurmak, kaydı tahrif etmektir.

Her anlamlı iş bir iz bırakır: ya bir karar kaydı, ya bir kanıt kaydı, ya
güncellenmiş bir durum dosyası. Kararlar gerekçeleriyle donar, böylece altı
hafta sonra "bu neden böyle" sorusunun cevabı kalır.

---

## Bu yöntemin bedeli

Dürüst olmak gerekirse: **bu yöntem hızlandırmaz.**

Doğrulama maliyeti insan zamanıdır ve otomatikleşene kadar yok olmaz. Delege
edilen bir modülde iki gerçek kusur bulundu — ikisini de yakalayan şey testler
değil, elle inceleme oldu. "Delege et ve doğrula" çalışan kod üretti; ucuz
üretmedi.

Kazanç başka yerde: **yanlış işe harcanan zaman azalır.** Bir kazanım
kanıtlanmadığında bunu altı hafta sonra değil, aynı gün öğrenirsiniz.
