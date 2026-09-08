# AI Systems — Showcase

Yedi projelik bir çalışmanın vitrini. Kod burada değil; **ne yapıldığı, neyin
kanıtlandığı ve neyin kanıtlanmadığı** burada.

> **Bu vitrinin tek kuralı:** hiçbir sayı, ölçülmeden yazılmaz. Ölçülmemiş her
> şey açıkça öyle etiketlenir. Bir projenin başarısız denemesi, başarılı
> denemesi kadar görünür.

## Önce bunu okuyun

**[Doğrulama ilkeleri](docs/verification-principles.md)** — bu projelerin ortak
tezi. Araçlar bu tezin farklı yüzleri; tez olmadan hiçbiri anlaşılmıyor.

**[Yapay zekâ ile çalışma yöntemi](docs/ai-workflow.md)** — bu sistemlerin nasıl
inşa edildiği: şartname, delegasyon, bağımsız doğrulama, mutasyonla kanıt.

## Projeler

| Proje | Ne yapar | Durum |
| --- | --- | --- |
| [SlopLab](projects/sloplab.md) | Zafiyet raporu triyaj değerlendiricilerini düşürmeye çalışan çekişmeli test çerçevesi | Public, CI + release |
| [MCP Guardian](projects/mcp-guardian.md) | MCP sunucuları için güvenlik tarayıcı ve doğrulama takımı | Geliştirilme aşamasında |
| [BackFlowFuzz](projects/backflowfuzz.md) | LLM model-çıktısı güven sınırı için deterministik, çevrimdışı fuzzer | Geliştirilme aşamasında |
| [Partitür](projects/partitur.md) | Çok modelli orkestrasyon: dondurulmuş kazanım sözleşmesi, kanıt zorunlu denetim | Geliştirilme aşamasında |
| [AI-OS](projects/ai-os.md) | Yapay zekâ destekli proje çalışması için katmanlı yönetişim ve kayıt motoru | Temel sürüm |

## Burada olmayanlar

**[Neden bazı şeyler burada yok](docs/what-is-not-here.md)** — açıklanmamış
güvenlik bulguları, doğrulanmamış projeler ve iç araçlar hakkında.
