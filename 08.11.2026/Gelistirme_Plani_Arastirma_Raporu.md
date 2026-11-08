# Geliştirme Planı Araştırma Raporu

*Araştırma tarihi 9 Kasım 2026 | Çalışma alanı 08.11.2026*

**Altı ürünlü RF ve SCADA portföyü için araştırmaya dayalı uygulama planı**

**Çalışma alanı:** 08.11.2026

**Araştırma ve kaynak doğrulama tarihi:** 9 Kasım 2026

**Kapsam:** RF-C, SCADA-01, RF-01, RF-02, RF-B ve RF-03

**Belge durumu:** Karar ve uygulama planıdır; ürün ya da saha kabulü değildir.

**Ana karar:** Mevcut 150 iş günü, portföy demonstrasyonu için iyimser alt sınırdır. Taahhüt tabanı bir geliştirici için 160 iş günü nominal + 15 iş günü program rezervi olarak güncellenmelidir. İki geliştiricide gerçekçi pencere 90–95 iş günü nominal + 10 iş günü rezervdir.

Çalışma alanındaki yapı ve JSON kontrolleri ile toplam 53 otomatik test başarılıdır. Ancak altı ürünün tamamında ürün kabulü NOT_RUN durumundadır. Bu rapor, “iskelet doğrulaması PASS” ile “ürün/saha kabulü PASS” ayrımını korur. [K2] [K3]

## Yönetici özeti

Araştırma, mevcut ürün sırasının genel yönünü doğruladı; fakat teknoloji sürümleri, veri kabulü, koordinat sözleşmesi, doğrulanabilir optimizasyon ve çalıştırma kanıtları açısından planın güncellenmesi gerektiğini gösterdi.

En kritik düzeltme SCADA-01 içindir. OpenPLC v3 resmî deposu 4 Nisan 2026'da arşivlenmiştir; yeni geliştirme OpenPLC Runtime v4 üzerinde başlamalıdır. Güncel aday kombinasyon Runtime v4.3.2 ve Editor v4.3.4'tür. Editor–Runtime uyumu temiz derleme, yükleme ve başlatma koşusuyla ilk 10 iş gününde doğrulanmalıdır. [K26] [K27] [K28]

RF tarafında iki normatif güncelleme zorunludur: bina içi yayılım için ITU-R P.1238-13, malzeme/strüktür etkileri için ITU-R P.2040-4. RF-B'de açık RF ölçüm verisinin doğrudan cihaz arıza etiketi olmadığı kabul edilmelidir; bakım doğrulamalı etiket yoksa ürün iddiası “girişim/bozulma sınıflandırması” olarak daraltılmalıdır. RF-03'te Sionna RT ortamı, GPU/işletim sistemi ve deterministik minimal sahne tam geliştirme sona bırakılmadan erken bir risk denemesiyle kanıtlanmalıdır. [K14] [K15] [K16] [K22] [K23]

| Karar | Araştırma sonucu | Plan etkisi |
| --- | --- | --- |
| Takvim | 150 gün iyimser alt sınır | 160 nominal + 15 rezerv |
| Python | 3.12 ve 3.13 olgun; 3.14 paket uyumuna bağlı | Ana 3.13, uyumluluk 3.12; 3.14 deneysel |
| Bağımlılık | Bağımsız depolar ortak uv workspace kilidine bağlanmamalı | Her depoda ayrı uv.lock ve SBOM |
| SCADA | OpenPLC v3 arşivlenmiş | Runtime 4.3.2 + Editor 4.3.4 |
| RF standartları | P.1238 ve P.2040 2025'te güncellendi | P.1238-13 + P.2040-4 |
| RF-B | NIST RF verisi doğrudan cihaz arıza etiketi değildir | Veri/etiket kapısı ve iddia sınırı |
| RF-03 | GPU/OS/sürüm uyumu yüksek risk | İlk 10 günde minimal ortam denemesi |
| RF-02 | Greedy sonuç optimalite kanıtlamaz | MILP/CP-SAT referans çözücü |
| Geometri | RFC 7946 yalnız WGS84 koordinatlarını tanımlar | Yerel metre koordinatları için ayrı sözleşme |
| Kabul | 53 test yalnız iskelet seviyesinde PASS | Gerçek kanıt koşusuna kadar ürün kabulü NOT_RUN |

## Önerilen uygulama sırası

1. Ortak temel ve üç erken risk denemesi: sürüm/lisans/koordinat/run-manifest kararları; SCADA v4 uyumluluğu; RF-B veri kabulü; RF-03 ortam kurulumu.

2. RF-C: mekânsal ve grup-temelli doğrulama metodolojisini sabitle.

3. SCADA-01: sanal Modbus laboratuvarını OpenPLC v4 üzerinde kanıtla.

4. RF-01 → RF-02: kapsama sözleşmesini üret, ardından yerleşim optimizasyonunu exact referansla doğrula.

5. RF-B: yalnız veri/etiket kapısı geçilirse arıza modeli; aksi durumda girişim/bozulma benchmark'ı.

6. RF-03: erken ortam denemesinden sonra, hafif ürün sözleşmeleri olgunlaşınca tam dijital ikiz.

7. Portföy kabulü: temiz kurulum, ham kanıt, hash, sınırlamalar ve ürün bazlı kabul raporları.

Metindeki [K#] işaretleri rapor sonundaki doğrulanmış kaynaklara gider. Kaynaktan doğrudan çıkan olgular ile raporun planlama çıkarımları ayrılmıştır.

## 1. Araştırma kapsamı ve yöntem

Araştırma; yerel 08.11.2026 çalışma alanı, önceki zaman dağılımı raporu, ürün iskeletleri ve bunların test kanıtlarıyla başladı. Ardından her ürün için yürürlükteki standartlar, resmî sürüm notları, resmî API/dokümantasyon ve birincil yöntem kaynakları incelendi. İnternet kaynakları 9 Kasım 2026 tarihinde doğrulandı. [K1] [K2] [K3]

| Kanıt sınıfı | Bu raporda kullanımı |
| --- | --- |
| Yerel kanıt | Manifest, doğrulama JSON'u, ürün sözleşmeleri ve mevcut plan |
| Normatif kaynak | ITU-R, IETF RFC, OPC Foundation ve NIST yayımları |
| Resmî ürün kaynağı | Proje deposu, sürüm notu, kurulum ve API belgeleri |
| Birincil yöntem | Mekânsal çapraz doğrulama makalesi ve NIST ölçüm verileri |
| Planlama çıkarımı | Kaynakların mevcut iskelete etkisinden türetilen sıra, süre ve kapılar |

### 1.1 Başlangıç durumu

Çalışma alanında altı ürün iskeleti bulunuyor. Yapı ve JSON doğrulamaları PASS; toplam 53 otomatik test başarılı. Buna karşın manifestte tüm ürünlerin kabul durumu NOT_RUN ve uzaktan depo, push, pull request, deployment ya da saha işlemi yapılmamış. Bu ayrım korunmalıdır: iskeletin test edilebilir olması, model veya saha kabulü değildir. [K2] [K3]

| Ürün | Test | İskelet | Ürün kabulü | Bir sonraki gerçek kanıt |
| --- | --- | --- | --- | --- |
| RF-C | 8 | PASS | NOT_RUN | Gerçekçi koordinatlı veriyle sızıntı denetimi |
| SCADA-01 | 7 | PASS | NOT_RUN | OpenPLC v4 ve gerçek Modbus hata enjeksiyonu |
| RF-01 | 10 | PASS | NOT_RUN | P.1238-13 ve ölçüm karşılaştırması |
| RF-02 | 9 | PASS | NOT_RUN | Exact çözücü ve küçük problem oracle karşılaştırması |
| RF-B | 10 | PASS | NOT_RUN | Lisanslı, etiket kökeni belgeli grup-zamansal veri |
| RF-03 | 9 | PASS | NOT_RUN | Sionna RT 2.2 ortamı, yakınsama ve ölçüm ayrımı |

### 1.2 Araştırmanın sınırları

Saha keşfi, RF ölçüm kampanyası, gerçek PLC/aktüatör bağlantısı ve tesis ağı değişikliği yapılmadı.

Yazılım sürümleri resmî kaynağa göre güncel adaylardır; üretim kilidi hedef işletim sistemi ve donanım üzerinde smoke test sonrası yazılmalıdır.

Takvim, tek geliştiricinin günde bir iş günü kapasitesini ve kritik kararların zamanında alınmasını varsayar.

Lisans değerlendirmesi teknik ön taramadır; dağıtım modeline göre hukuki inceleme gerekebilir.

## 2. Revize program planı

Mevcut 150 iş günlük plan ürün geliştirme bloklarını kapsıyor; araştırmada ortaya çıkan OpenPLC v4 geçiş rezervi, RF-B veri kabulü ve ortak kararların genişletilmesi ayrı görünmüyor. Aşağıdaki plan bu işleri açıkça gösterir. Ayrıntılı toplam 158 iş günüdür; taahhüt kolaylığı için 160 güne yuvarlanır. 15 günlük program rezervi ürün işlerine dağıtılmaz, yalnız kanıtlı risk gerçekleşirse kullanılır.

| İş paketi | Mevcut | Önerilen | Farkın gerekçesi | Ana çıkış kapısı |
| --- | --- | --- | --- | --- |
| Ortak temel | 8 gün | 10 gün | Sürüm, lisans, CRS, run-manifest ve üç risk denemesi | G0 karar paketi |
| RF-C | 18 gün | 18 gün | Süre yeterli; çıktılar sıkılaştırılıyor | Sızıntısız split raporu |
| SCADA-01 | 22 gün | 25 gün | v3→v4 uyumluluk ve image/digest kanıtı | 100 hata çevrimi |
| RF-01 | 23 gün | 23 gün | Standart yükseltmesi sprintlere gömülür | Ölçüm/standart sapma raporu |
| RF-02 | 17 gün | 17 gün | Exact oracle mevcut işe gömülür | Optimal/bound durumu |
| RF-B | 20 gün | 23 gün | Lisans, etiket kökeni ve prevalans kabulü | Veri kabul tutanağı |
| RF-03 | 32 gün | 32 gün | Erken spike bu sürenin öne çekilmiş parçasıdır | Yakınsama ve iddia sınırı |
| Son QA | 10 gün | 10 gün | Temiz kurulum, kanıt ve çapraz sözleşme | Portföy kabul paketi |
| Toplam | 150 gün | 158 gün | Taahhüt tabanı 160 gün | +15 gün program rezervi |

### 2.1 Kaynak senaryoları

| Senaryo | Nominal geçen süre | Rezerv | Planlama notu |
| --- | --- | --- | --- |
| 1 geliştirici | 160 iş günü | 15 gün | Yaklaşık 35 hafta; ürünler ağırlıkla ardışık |
| 2 geliştirici | 90–95 iş günü | 10 gün | RF zinciri ve SCADA/RF-B paralel; RF-03 son bölümde ortak |
| Saha entegrasyonu | +10–30 gün | Ayrı | Gerçek PLC, tesis ağı, fiziksel I/O veya ölçüm kampanyası için keşif sonrası |

İki geliştirici tahmini bir verim varsayımıdır: ortak temel 10 gün; ardından RF-C→RF-01→RF-02 zinciri ile SCADA-01→RF-B paralel; RF-03'ün kalan işi iki geliştirici tarafından paylaşılır. Entegrasyon ve son QA tamamen paralelleştirilemediği için matematiksel alt sınır taahhüt olarak kullanılmamalıdır.

### 2.2 Tek geliştirici için teslim sırası

| İş günü | Paket | Teslim kararı |
| --- | --- | --- |
| 1–10 | Ortak temel ve risk denemeleri | G0 geçmeden ürün kodu genişletilmez |
| 11–28 | RF-C | Mekânsal doğrulama politikası sabitlenir |
| 29–53 | SCADA-01 | OpenPLC v4 laboratuvarı ve kanıt historian'ı |
| 54–76 | RF-01 | Sürümlemeli kapsama çıktısı |
| 77–93 | RF-02 | Greedy + exact doğrulama |
| 94–116 | RF-B | Veri kapısı geçtiyse model; geçmediyse iddia daraltma |
| 117–148 | RF-03 | Dijital ikiz, yakınsama ve limitler |
| 149–158 | Portföy QA | Temiz kurulum, kanıt ve dokümantasyon |
| 159–173 | Program rezervi | Yalnız risk gerçekleşirse; otomatik tüketilmez |

### 2.3 İlk 30 iş günü

| Gün | Faaliyet | Somut çıktı | Dur/kalk koşulu |
| --- | --- | --- | --- |
| 1–2 | Kapsam, lisans, depo ve iddia sınırı | ADR paketi ve sahiplik matrisi | Dağıtım/lisans belirsizse dur |
| 3–4 | Python, uv, işletim sistemi ve CI | Her depo için ayrı lock; 3.12/3.13 matrisi | Temiz sync başarısızsa dur |
| 5 | CRS, birim ve run-manifest | Sözleşme şemaları | Yerel koordinat GeoJSON diye yayımlanmaz |
| 6 | SCADA v4 uyumluluk spike | Editor derle→Runtime yükle→başlat kanıtı | Uyumsuzlukta 3–5 gün rezerv kararı |
| 7 | RF-B veri/etiket spike | Lisans, prevalans ve etiket kökeni özeti | Arıza etiketi yoksa iddiayı daralt |
| 8–9 | RF-03 ortam spike | Sionna RT 2.2 minimal scene ve donanım kaydı | GPU yolu yoksa CPU limitini yaz |
| 10 | G0 gözden geçirme | İmzalanabilir karar tutanağı | Kritik karar açık kalırsa sprint başlamaz |
| 11–18 | RF-C Sprint 1 | Veri şeması ve random/group/spatial split | Grup ve blok kesişimi sıfır |
| 19–24 | RF-C Sprint 2 | Fold mesafesi, class distribution ve novelty | Leakage uyarıları açıklanır |
| 25–28 | RF-C Sprint 3 | Raporlama, tekrarlanabilirlik ve kabul | Aynı seed aynı çıktı |
| 29–30 | SCADA Sprint 1 başlangıcı | Compose ağ, volume ve health taslağı | Portlar yalnız lab iç ağı |

## 3. Ortak teknik temel

### 3.1 Python ve bağımlılık politikası

Python 3.13 ana geliştirme sürümü, 3.12 destek matrisi ve 3.14 yalnız uyumluluk işi olarak önerilir. Python 3.15 ön-sürüm olduğundan taahhüt tabanına alınmamalıdır. [K4]

Her ürün bağımsız depo yaşam döngüsüne sahip olduğundan kendi pyproject.toml ve uv.lock dosyasını taşır. uv workspace tek kilit dosyası üretir; altı bağımsız ürün için ortak workspace lock kullanılmaz. [K5] [K6]

Kilide yalnız paket çözümlemesi değil Python sürümü, platform ve harici araç sürümleri de run manifest içinde eklenir.

CI ana matrisi 3.12/3.13'tür. 3.14 uyumluluk işi başlangıçta hata toleranslıdır; bağımlılıklar desteklediğinde zorunlu kapıya çevrilir.

Sionna RT ağır GPU/renderer bağımlılıkları ayrı ortamda tutulur; RF-03 bağımlılıkları ortak temel pakete taşınmaz.

### 3.2 Run-manifest ve kanıt sözleşmesi

| Alan grubu | Zorunlu alanlar |
| --- | --- |
| Kimlik | run_id, product_code, schema_version, created_at_utc, operator |
| Girdi | dataset/source id, lisans kaydı, input checksum, config checksum |
| Kod | commit veya source hash, dirty flag, komut satırı |
| Ortam | Python, lock hash'i, OS, CPU/GPU, driver/backend |
| Rastgelelik | seed, split policy, determinism flag |
| Sonuç | status, start/end, duration, metrics, warnings, claim boundary |
| Artefakt | dosya yolu, tür, SHA-256 ve üretici adımı |

### 3.3 CI, tedarik zinciri ve yayın

Her commit: format/lint, unit, sözleşme, negatif test ve determinism smoke.

Pull request: Python 3.12/3.13 matrisi, dependency review ve lisans politikası. GitHub'ın güncel Python örnekleri actions/checkout@v6 ve actions/setup-python@v5 gösterir; eylemler mümkünse commit SHA ile sabitlenir. [K7] [K8]

Haftalık/gecelik: büyük fixture, entegrasyon, RF-03 GPU ve SCADA hata enjeksiyonu. Donanımsız ortamda bu işler başarı gibi gösterilmez.

Yayın: lock, CycloneDX SBOM, kaynak/artefakt hash'i ve uygun olduğunda GitHub artifact attestation. Attestation test geçişinin yerine değil, köken kanıtı olarak kullanılır. [K9]

NIST SSDF, güvenli geliştirme görevlerini ayrı bir son kontrol yerine yaşam döngüsüne gömmeyi önerir. Tehdit modeli, bağımlılık ve yayın kanıtı sprintlerin içinde tutulur. [K10]

### 3.4 Coğrafi ve yerel koordinat kararı

RFC 7946 GeoJSON koordinatlarını WGS84 boylam/enlem ekseninde tanımlar ve alternatif CRS mekanizmasını kaldırır. Bina içindeki metre tabanlı yerel x/y/z noktaları GeoJSON diye etiketlenmemelidir. [K17]

| Kullanım | Önerilen sözleşme |
| --- | --- |
| Yerel bina koordinatı | local-frame.json: origin, axes, unit=metre, handedness, floor/elevation |
| Dünya koordinatı | RFC 7946 GeoJSON; lon/lat sırası ve WGS84 |
| Dönüşüm | Açık georeferencing transform, sürüm ve doğrulama noktaları |
| Gizlilik | Hassas tesis koordinatını yayımlamadan sentetik veya ötelenmiş fixture |

## 4. Ürün bazlı geliştirme planı

### 4.1 RF-C — Mekânsal doğrulama ve dengesizlik denetimi

RF-C, RF-01 ve dolaylı olarak RF-02 için metodoloji temeli olmalıdır. Random split tek başına iyimser sonuç üretebilir; grup ve mekânsal blok ayrımı, eğitim/test yakınlığı ve sınıf prevalansı birlikte raporlanmalıdır. scikit-learn GroupKFold, aynı grubun train ve testte bulunmasını engeller; fakat zaman yönünü çözmez. [K11] [K12]

Üç split ailesi: seeded random, group ve spatial block. Her fold için sample/group/block kesişimleri otomatik denetlenir.

Fold raporu: train/test sayıları, sınıf dağılımı, en yakın train–test mesafesi, hedef bölge benzerliği ve uyarılar.

blockCV, mekânsal değerlendirme yaklaşımı için yöntem referansı olabilir; GPL-3+ lisans kararı verilmeden Python runtime bağımlılığı yapılmaz. [K13]

GroupKFold shuffle/random_state davranışı sürüme bağlı olduğundan scikit-learn sürümü ve seed birlikte kilitlenir. [K11]

| Sprint | Süre | Çıktı | Kabul kapısı |
| --- | --- | --- | --- |
| 1 | 7 gün | Şema, random/group/spatial split ve determinism | Sıfır grup/blok kesişimi |
| 2 | 6 gün | Mesafe, novelty ve class/prevalence audit | Her fold için makine-okunur audit |
| 3 | 5 gün | Rapor, CLI, paketleme ve gerçekçi fixture | Temiz koşuda aynı manifest/hash |

### 4.2 SCADA-01 — Endüstriyel telemetri doğrulama laboratuvarı

Zorunlu değişiklik: OpenPLC v3 ile yeni geliştirme başlatılmamalıdır. Resmî depo 4 Nisan 2026'da arşivlenmiştir. [K26]

Güncel aday kombinasyon OpenPLC Runtime v4.3.2 ve Editor v4.3.4'tür. Runtime v4, v3 web arayüzünün devamı değil; headless ve HTTPS/JWT yönetimli yeni bir mimaridir. Editor/Runtime için yayımlanmış kesin uyumluluk matrisi bulunmadığından ilk kapı temiz derleme→yükleme→başlatma testidir. [K27] [K28]

MVP veri yolu Modbus TCP'dir; OPC UA Sprint 3'te isteğe bağlı profil olur. Yönetim REST API'si veri yolu olarak kullanılmaz.

FUXA 1.3.5; PyModbus 3.16.2; OPC UA gerekiyorsa asyncua==2.1.0 tam sürüm kilidi. [K29] [K30] [K31]

Tek tag/register sözleşmesi; tip, signedness, word/byte order, ölçek, birim, yazılabilirlik ve kalite tüm bileşenleri besler.

Gateway tek kanıt historian'ını yazar. SQLite yerel kalıcı hacim, tek yazıcı, WAL, ölçülmüş busy_timeout, düzenli checkpoint ve restore testi kullanır. WAL ağ dosya sisteminde kullanılmaz. [K32]

Compose “running” durumunu hazır olma saymaz; gerçek protokol healthcheck ve service_healthy bağımlılığı gerekir. [K33]

| Sprint | Süre | Çıktı | Ölçülebilir kapı |
| --- | --- | --- | --- |
| 1 | 9,5 gün | Sürüm/digest, Compose, tag map, simülatör ve Modbus | Editor→Runtime akışı ve tam register sözleşmesi |
| 2 | 8 gün | Gateway, SQLite historian ve FUXA ekran/alarm/stale | Eski veri Good gösterilmez; restore başarılı |
| 3 | 4,5 gün | 100 kesinti çevrimi, güvenlik ve kabul paketi | Stale/reconnect/alarm p95 ve max raporu |
| Risk | 3 gün | v4 uyumluluk rezervi | Yalnız spike başarısızsa tüketilir |

Bir saniyelik çevrim için geçici başlangıç hedefleri: stale p95 ≤4 sn ve maksimum ≤5 sn; servis healthy olduktan ilk Good örneğe reconnect p95 ≤6 sn ve maksimum ≤10 sn; alarm p95 ≤2,5 sn ve maksimum ≤4 sn; 30 dakikalık nominal koşuda poll başarısı ≥%99,9. Bunlar standart zorunluluğu değil, ilk 100 kontrollü kesinti sonunda yeniden tabanlanacak proje kabul hedefleridir.

Önerilen laboratuvar veri akışı şöyledir:

deterministik sensor simulator → OpenPLC Runtime v4.3.2 → Modbus TCP 5020 → FUXA 1.3.5 ve PyModbus gateway → SQLite historian

İsteğe bağlı OPC UA profili asyncua==2.1.0 kullanır. OpenPLC yönetimi 8443, FUXA 1881, Modbus 5020 ve OPC UA 4840 portları yalnız belirlenmiş localhost veya iç OT-lab ağına bağlanır. Tek Modbus okumasında alınabilecek bitişik telemetri zarfı en az run_id, artan sequence, UTC source_timestamp_ms, quality ve değerleri taşımalıdır. Değer değişmedi diye otomatik stale kararı verilmemeli; sequence ve kaynak zamanı birlikte izlenmelidir. OPC UA profili açılırsa DataValue içindeki value, StatusCode, sourceTimestamp ve serverTimestamp birlikte saklanmalıdır. [K34]

### 4.3 RF-01 — Bina içi kapsama kestirimi

RF-01'in mevcut serbest uzay yol kaybı çekirdeği yalnız oracle/smoke olarak kalmalıdır. Ürün modeli ITU-R P.1238-13 bina içi yayılım yaklaşımını ve P.2040-4 malzeme özelliklerini referans almalıdır. Her iki tavsiye de Eylül 2025 sürümleriyle güncellenmiştir; P.1238-13 300 MHz–450 GHz, P.2040-4 1 MHz–450 GHz aralığını kapsar. [K14] [K15]

Kat planı, duvar ve malzeme sözleşmesi; local-frame koordinatları, metre birimi, kat yüksekliği ve geometri toleransı içerir.

Malzeme parametresinin kökeni standard, datasheet, measured, calibrated veya assumption olarak etiketlenir.

RF-C split ve audit çıktısı, kalibrasyon ve validation bölgelerini ayırmak için kullanılır.

Çıktı sözleşmesi RF-02 için sürümlenir: grid/point id, local frame, frequency, threshold, predicted power/loss, uncertainty, model/run id ve hash.

FSPL smoke, bir metrelik bilinen değer ve mesafe monotonluğu için kalır; bina içi doğruluk iddiasının kanıtı sayılmaz.

| Sprint | Süre | Ana iş | Kapı |
| --- | --- | --- | --- |
| 1 | 9 gün | Geometri, CRS/birim ve P.1238-13 tabanı | Bilinen senaryo ve sınır testleri |
| 2 | 8 gün | Duvar/malzeme ve ölçüm veri adaptörü | Malzeme kökeni ve RF-C ayrımı |
| 3 | 6 gün | Uncertainty, rapor ve RF-02 export | Sürümlemeli coverage contract |

### 4.4 RF-02 — Erişim noktası yerleşim optimizasyonu

Greedy yöntem hızlı bir baseline sağlar fakat optimalite kanıtı vermez. Aynı coverage matrix girdisinde greedy ile exact/verifiable çözüm karşılaştırılmalıdır. Doğrusal model için SciPy milp; mantıksal ve tamsayılı kısıtlar için OR-Tools CP-SAT uygundur. CP-SAT katsayıları tamsayı olmalıdır; ağırlıklar kontrollü ölçeklenmelidir. [K18] [K19]

Coverage matrix sürümlenir; RF-01 run id, koordinat çerçevesi, eşik, grid/candidate id ve checksum taşır.

Çözücü sonucu OPTIMAL, FEASIBLE, INFEASIBLE, MODEL_INVALID veya UNKNOWN statüsüyle yazılır; bound ve gap varsa kaydedilir.

Küçük problemler brute-force oracle ile, orta problemler CP-SAT/MILP ile, büyük problemler greedy/heuristic ile kıyaslanır.

Aynı girdi, seed ve zaman limiti aynı seçimi veya eşdeğer objective'i üretmelidir; eşitlik kırma kuralı açıktır.

“Çözüm bulundu” ile “optimal çözüm kanıtlandı” aynı rapor alanında birleştirilmez.

| Sprint | Süre | Ana iş | Kapı |
| --- | --- | --- | --- |
| 1 | 6 gün | Coverage contract, greedy ve constraint doğrulama | Geçersiz çözüm hiçbir zaman raporlanmaz |
| 2 | 7 gün | MILP/CP-SAT referans ve oracle testleri | Statü, bound ve gap kanıtı |
| 3 | 4 gün | Trade-off raporu, CLI ve tekrar üretim | Aynı inputta karşılaştırmalı çıktı |

### 4.5 RF-B — Kablosuz arıza ve bozulma benchmark'ı

İddia sınırı: Bakım doğrulamalı arıza etiketi yoksa ürün, “cihaz arızası” değil “girişim/bozulma sınıflandırması” olarak adlandırılmalıdır.

NIST endüstriyel kablosuz ölçümleri ve elektromanyetik girişim veri setleri gerçek RF koşullarını sağlar; ancak doğrudan cihaz arıza etiketi oldukları varsayılamaz. Arıza iddiası için etiketin bakım kaydı, kontrollü enjeksiyon veya doğrulanmış olay prosedürüyle kökeni gösterilmelidir. [K16] [K22]

Ön kabul alanları: lisans, kaynak/checksum, site/device/run, zaman dilimli UTC timestamp, band/frequency, anten zinciri, class, label provenance, confidence ve procedure.

Özel group-temporal split: aynı site/device/run train ve testte bulunmaz; test zamanı train sonrasındadır. GroupKFold zaman yönünü, TimeSeriesSplit grup izolasyonunu tek başına sağlamaz. [K11] [K12]

Resampling yalnız training fold içinde ve imbalanced-learn Pipeline üzerinden yapılır; test prevalansı doğal kalır. Split öncesi resampling sızıntı ve iyimser metrik üretir. [K21]

Ana metrikler Average Precision/PR, azınlık recall/precision, balanced accuracy, false alarm per hour/run ve calibration'dır. Accuracy tek başına kabul metriği değildir.

Metrik raporu sınıf prevalansını, confusion counts ve ham tahmin artefaktını birlikte taşır.

| Aşama | Süre | Çıktı | Dur/kalk kapısı |
| --- | --- | --- | --- |
| Sprint 0 | 3 gün | Lisans, etiket kökeni, prevalans ve iddia | Arıza etiketi yoksa kapsamı daralt |
| Sprint 1 | 8 gün | Şema, group-temporal split ve baseline | Grup kesişimi sıfır; zaman yönü doğru |
| Sprint 2 | 7 gün | Pipeline, imbalance yöntemleri ve kalibrasyon | Resampling yalnız training fold |
| Sprint 3 | 5 gün | PR, false-alarm raporu ve tekrar üretim | Ham tahmin ve prevalansla kanıt |

### 4.6 RF-03 — Depo radyo dijital ikizi

Önerilen çalışma tabanı sionna-rt==2.2.0 sürümüdür. Güncel Sionna RT çekirdeği Mitsuba/Dr.Jit tabanlıdır; TensorFlow bağımlılığı eski varsayımla ortak ortama eklenmemelidir. GPU, driver, LLVM ve işletim sistemi yolu ilk 10 iş gününde minimal sahneyle doğrulanmalıdır. [K23] [K24]

Ayrı ortam: Sionna RT 2.2.0 ve doğrulanmış Mitsuba/Dr.Jit sürümleri lock içinde; Linux veya WSL2 öncelikli. Tam Sionna PHY/SYS gerekiyorsa ayrı profile alınır.

Scene contract: local frame, axes/metre, mesh checksum, object id/transform, material coverage, frequency, TX/RX/antenna, solver flags, max_depth, samples/cell size ve yazılım sürümleri.

PathSolver(deterministic=True), seed, donanım/driver/backend kaydı ve çapraz donanımda sayısal tolerans kullanılır. Determinizm fiziksel doğruluğun kanıtı değildir. [K25]

Mekanizma sırası: LoS ve specular; sonra refraction/diffraction; en son diffuse scattering. Her genişletmede convergence study tekrarlanır.

Calibration ve validation sahaları ayrılır. Ölçüm yoksa çıktı simulation-only; ölçüm varsa prosedüre göre measurement-compared olarak etiketlenir.

Malzeme parametrelerinin kaynağı P.2040-4, üretici datasheet'i, ölçüm, kalibrasyon veya varsayım olarak ayrı tutulur. [K15]

| Sprint | Süre | Ana iş | Kapı |
| --- | --- | --- | --- |
| 1 | 12 gün | Ortam, scene/material contract ve deterministic baseline | Minimal sahne iki temiz koşuda tolerans içinde |
| 2 | 11 gün | Radio map, mekanizma ve yakınsama çalışması | Depth/samples/cell hassasiyeti raporu |
| 3 | 9 gün | Kalibrasyon ayrımı, rapor ve artefakt paketleme | Claim boundary ve tam provenance |

## 5. Kabul kapıları ve kanıt matrisi

Kabul test sayısına değil, kanıtın ürün iddiasıyla uyumuna bağlanmalıdır. Bütün ürünler aynı statü dilini kullanır: NOT_RUN, RUNNING, PASS, FAIL ve BLOCKED. Başarısız ya da koşturulmamış adım PASS olarak miras alınmaz.

| Kapı | Kapsam | Geçiş kanıtı |
| --- | --- | --- |
| G0 Karar | Sürüm, lisans, iddia, veri, CRS ve ortam | ADR'ler, sahiplik ve açık kritik karar bulunmaması |
| G1 Sözleşme | Şema, tag/register, coverage ve scene | Şema testleri ve checksum eşitliği |
| G2 Determinizm | Seed, split, simulator ve solver | İki temiz koşunun kanonik karşılaştırması |
| G3 Bilimsel/Protokol | Model standardı veya gerçek protokol | Oracle, standard veya protokol test paketi |
| G4 Entegrasyon | Bileşenler arası veri akışı | Uçtan uca run manifest ve artefakt hash'leri |
| G5 Negatif/Hata | Bozuk girdi, timeout, leakage ve infeasible | Beklenen hata statüsü; sessiz başarı yok |
| G6 Performans | Latency, solver ve RF convergence | Önceden yazılmış eşikler ve ham ölçümler |
| G7 Güvenlik/Tedarik | Bağımlılık, port, secret ve SBOM | Dependency review, port listesi, lock ve SBOM |
| G8 Teslim | Temiz kurulum ve iddia sınırı | Bağımsız yeniden üretim ve sınırlamalar |

### 5.1 Ürün kabul ölçütleri

| Ürün | Asgari PASS koşulu | PASS olmayan ama yararlı sonuç |
| --- | --- | --- |
| RF-C | Sıfır group/block overlap; fold mesafe ve dağılım; aynı seed | Leakage bulunduysa FAIL ama değerli teşhis |
| SCADA-01 | 100 kesinti; p95/max; stale Good değil; restore; beklenen portlar | Lab çalışır fakat metrik eksikse NOT_RUN veya FAIL |
| RF-01 | Güncel ITU kökeni; ayrı calibration/validation; RF-02 contract | FSPL smoke yalnız baseline |
| RF-02 | Feasible/optimal statüsü; oracle; constraint; gap/bound | Greedy çözüm yalnız heuristic sonucu |
| RF-B | Lisanslı etiket; group-temporal split; doğal prevalans; PR/false alarm | Etiket yoksa interference benchmark olarak kabul |
| RF-03 | Kilitli ortam; scene/material provenance; convergence; iddia sınırı | Ölçümsüz sonuç simulation-only |

### 5.2 SCADA-01 ayrıntılı kapıları

1. G0 — Sürüm, lisans ve kapsam: Runtime v4.3.2, Editor v4.3.4, FUXA 1.3.5, PyModbus 3.16.2 ve asyncua 2.1.0 kaydedilir. latest yoktur; image digest çekildikten sonra kilitlenir.

2. G1 — Tag/register sözleşmesi: Çakışmasız adres, tip, signedness, word/byte order, ölçek, birim, min/max, yazılabilirlik ve kalite. Bütün bileşenlerde sözleşme checksum'u aynıdır.

3. G2 — Deterministik simülatör: Aynı seed, adım sayısı ve hata takvimi aynı sequence, değer ve zaman çizelgesini üretir.

4. G3 — OpenPLC/Modbus: Editor projesi derlenir, Runtime v4.3.2'ye yüklenir ve başlatılır. Gerekli function code'lar, geçersiz adres, word order ve restart denenir.

5. G4 — Gateway/historian: Timeout, sınırlı exponential backoff, reconnect, duplicate ve out-of-order; SQLite WAL, migration, UTC, backup ve restore.

6. G5 — FUXA: Kalıcı proje hacmi, tag binding, alarm active/normal/ack, stale görselleştirme ve yazma hatası kullanıcı bildirimi.

7. G6 — Hata enjeksiyonu: OpenPLC kill/restart, ağ kopması, donmuş sequence, illegal Modbus cevap, gateway/FUXA restart, SQLite lock ve kontrollü disk-dolu. En az 100 çevrim.

8. G7 — Güvenlik ve tekrar üretim: Temiz makine/volume, digest doğrulama, healthcheck, backup/restore ve yalnız beklenen localhost yüzeyleri.

9. G8 — Son kabul: Sürüm çıktıları, Compose, tag map checksum, ham log/CSV/DB, ölçüm özeti, ekran görüntüsü ve bilinen sınırlamalar birlikte arşivlenir.

### 5.3 Güvenlik sınırı

SCADA laboratuvarı internetten erişilebilir yapılmamalı ve gerçek tesis ağına bağlanmamalıdır. NIST SP 800-82 Rev.3 final rehberdir; Rev.4 ise 21 Eylül 2026 tarihli ilk kamu taslağıdır ve kabul standardı değil izleme girdisidir. [K35] [K36]

Modbus 5020 ve isteğe bağlı OPC UA 4840 yalnız iç OT-lab ağına açılır. OpenPLC yönetimi 8443 ve FUXA 1881 yalnız localhost veya mühendislik profiline bağlanır.

FUXA yazma yetkisi varsayılan kapalıdır; rol ve allowlist olmadan PLC yazması yoktur.

--privileged, host network, Docker socket ve geniş host mount kullanılmaz. Secret'lar Compose veya depoda düz metin değildir.

OpenPLC resmî Docker örneğindeki gerekli capability'ler dışında ek yetki verilmez; image etiketi ve mimariye özgü digest kaydedilir.

Gerçek PLC veya fiziksel aktüatöre yazma ayrı risk değerlendirmesi, değişiklik onayı, yedek ve geri dönüş planı gerektirir.

CISA'nın ICS önerileri doğrultusunda gereksiz port ve protokoller kapatılır; izleme, yedek ve olay müdahale planı test edilir. [K37]

## 6. Risk kaydı

| Risk | Olasılık / etki | Erken gösterge | Azaltım | Karar zamanı |
| --- | --- | --- | --- | --- |
| OpenPLC v3 EOL | Kesin / Kritik | v3 bağımlılığı veya web UI varsayımı | v4.3.2 + Editor 4.3.4 spike | Gün 6 |
| RF-B etiketi geçersiz | Yüksek / Kritik | Bakım/olay kökeni yok | İddiayı girişim/bozulmaya daralt | Gün 7 |
| RF-03 GPU/driver uyumsuz | Orta-Yüksek / Yüksek | Minimal sahne kurulamıyor | Linux/WSL2, CPU yolu ve süre limiti | Gün 8–9 |
| Mekânsal sızıntı | Yüksek / Yüksek | Random sonuç group/spatial'dan aşırı iyi | RF-C kapısı ve fold mesafe raporu | RF-C Sprint 1 |
| Yerel koordinatın GeoJSON sanılması | Orta / Yüksek | x/y metre lon/lat gibi tüketiliyor | local-frame şeması ve dönüşüm testi | Gün 5 |
| Greedy optimal sanılması | Orta / Yüksek | Objective gap bilinmiyor | Exact oracle, statü ve bound/gap | RF-02 Sprint 2 |
| SCADA stale değeri Good | Orta / Kritik | Değer donuyor fakat kalite değişmiyor | sequence, source time, quality ve hata enjeksiyonu | SCADA Sprint 2 |
| Bağımlılık sürüklenmesi | Orta / Orta | Temiz sync farklı paket çözüyor | Per-repo lock, digest ve SBOM | Gün 3–4 |
| Kanıt yerine ekran görüntüsü | Orta / Yüksek | Ham log veya run manifest yok | Makine-okunur kanıt paketi | Her sprint sonu |
| Saha kapsamı gizlice eklenir | Orta / Kritik | Gerçek PLC veya ölçüm talebi | Ayrı change request ve 10–30 gün keşif | Talep anı |

### 6.1 Yönetim için haftalık göstergeler

| Gösterge | Hedef | Kötü sinyal |
| --- | --- | --- |
| Kabul kapısı | Planlanan kapıların kanıtlı geçiş oranı | Test sayısı artıyor, kapı NOT_RUN |
| Tekrar üretim | Temiz koşu başarı oranı ve hash uyumu | Yalnız geliştirici makinesinde çalışıyor |
| Risk rezervi | Neden, karar ve harcama kaydı | Rezerv normal işlere tüketiliyor |
| İddia sınırı | Her raporda açık iddia ve sınırlama | Simulation-only sonuç saha doğrulanmış sunuluyor |
| Veri kökeni | Lisans, provenance ve checksum yüzde 100 | Kaynak veya etiket prosedürü eksik |
| Bağımlılık | Lock/digest drift sıfır | latest veya sınırsız üst sürüm |

## 7. Uygulanacak dosya ve süreç değişiklikleri

Aşağıdaki liste kod değişikliği teslimi değil, geliştirme sprintlerinin ilk uygulanabilir backlog'udur. Yol adları mevcut ürün köklerine göredir.

| Kapsam | Önerilen değişiklik |
| --- | --- |
| Tüm depolar | pyproject.toml + uv.lock; schemas/run-manifest.schema.json; evidence README; CI 3.12/3.13; SBOM/release iş akışı |
| RF-C | Split policy'ye fold distance, novelty ve prevalence; gerçekçi grup/koordinat fixture; leakage report |
| SCADA-01 | OpenPLC v3 referanslarını v4.3.2 ve Editor 4.3.4'e çevir; Compose profile/health; tag map tek otorite; gateway historian |
| RF-01 | local-frame şeması; P.1238-13; P.2040-4 material provenance; RF-02 coverage export |
| RF-02 | Solver adapter; CP-SAT/MILP status ve gap; brute-force oracle fixture; deterministic tie-break |
| RF-B | Data-acceptance report; label provenance; group-temporal split; Pipeline; PR/false-alarm/calibration raporu |
| RF-03 | Ayrı uv environment; scene/material şeması; determinism/convergence harness; hardware/driver manifest |
| Portföy kökü | Karar kayıtları; ürün kapısı özeti; ortak kaynak envanteri; gerçek kabul gelene kadar NOT_RUN |

### 7.1 Başlamadan önce verilecek 12 karar

1. Teslim hedefi portföy demonstrasyonu mu, saha/üretim kabulü mü?

2. Her ürün ayrı depo ve ayrı sürüm yaşam döngüsü mü taşıyacak?

3. Python ana sürümü 3.13, destek sürümü 3.12 olarak onaylanıyor mu?

4. Bağımlılık ve konteynerlerde latest yasağı ile lock/digest politikası kabul ediliyor mu?

5. OpenPLC v4.3.2 + Editor v4.3.4 kombinasyonu erken spike ile doğrulanacak mı?

6. SCADA MVP yalnız Modbus, OPC UA opsiyonel profil mi?

7. RF-B için bakım doğrulamalı arıza etiketi gerçekten mevcut mu?

8. RF-03 için Linux/WSL2 ve uygun GPU/driver sağlanabiliyor mu?

9. Yerel koordinat sözleşmesi GeoJSON'dan ayrılacak mı?

10. RF-02'de exact çözücü optimalite veya bound referansı olarak zorunlu mu?

11. Veri, model ve sahne lisansları ile dağıtım biçimini kim onaylayacak?

12. Uzak depo oluşturma, push, PR ve release yetkileri ne zaman açılacak?

### 7.2 Nihai öneri

GO önerisi: 160 + 15 günlük planla başlayın; ancak G0 karar paketini ilk 10 günde tamamlamadan ürün kabul takvimini taahhüt etmeyin.

Bu yaklaşım mevcut iskeleti korur ve araştırmanın ortaya çıkardığı kırılganlıkları görünür iş paketlerine dönüştürür. En önemli yönetim disiplini, PASS kelimesini yalnız ürün iddiasını destekleyen ham ve tekrarlanabilir kanıt oluştuğunda kullanmaktır.

## Kaynakça

Tüm internet kaynaklarına erişim tarihi 9 Kasım 2026'dır. Yerel kaynaklar 08.11.2026 çalışma alanındadır.

1. [K1] Yerel plan: 08.11.2026/Model Raporları/08.11.2026_Urun_Paketi_Repo_Iskeletleri_ve_Zaman_Dagilimi.docx. Temel ürün sırası ve 150 günlük plan.

2. [K2] Yerel manifest: 08.11.2026/PROJECT-MANIFEST.json. Ürünler, bağımlılıklar ve NOT_RUN durumu.

3. [K3] Yerel doğrulama: 08.11.2026/VALIDATION-RESULTS.json. Toplam 53 test, yapı ve JSON kontrolleri.

4. [K4] Python Developer's Guide — Status of Python versions: https://devguide.python.org/versions/

5. [K5] uv — Workspaces: https://docs.astral.sh/uv/concepts/projects/workspaces/

6. [K6] uv — Locking and syncing: https://docs.astral.sh/uv/concepts/projects/sync/

7. [K7] GitHub Docs — Building and testing Python: https://docs.github.com/en/actions/tutorials/build-and-test-code/python

8. [K8] GitHub Docs — Dependency review action: https://docs.github.com/en/code-security/how-tos/secure-your-supply-chain/manage-your-dependency-security/configure-dependency-review-action

9. [K9] GitHub Docs — Artifact attestations: https://docs.github.com/en/actions/concepts/security/artifact-attestations

10. [K10] NIST SP 800-218 — Secure Software Development Framework: https://csrc.nist.gov/pubs/sp/800/218/final

11. [K11] scikit-learn — GroupKFold: https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.GroupKFold.html

12. [K12] scikit-learn — Cross-validation and common pitfalls: https://scikit-learn.org/stable/modules/cross_validation.html

13. [K13] Valavi et al. — blockCV: https://doi.org/10.1111/ecog.02881

14. [K14] ITU-R P.1238-13: https://www.itu.int/rec/R-REC-P.1238-13-202509-I/en

15. [K15] ITU-R P.2040-4: https://www.itu.int/rec/R-REC-P.2040-4-202509-I/en

16. [K16] NIST — Industrial Wireless Systems Radio Propagation Measurements: https://www.nist.gov/publications/industrial-wireless-systems-radio-propagation-measurements

17. [K17] IETF RFC 7946 — The GeoJSON Format: https://datatracker.ietf.org/doc/html/rfc7946

18. [K18] SciPy — `scipy.optimize.milp`: https://docs.scipy.org/doc/scipy/reference/generated/scipy.optimize.milp.html

19. [K19] Google OR-Tools — CP-SAT Solver: https://developers.google.com/optimization/cp/cp_solver

20. [K20] MAPIE documentation: https://mapie.readthedocs.io/en/stable/

21. [K21] imbalanced-learn — Common pitfalls: https://imbalanced-learn.org/stable/common_pitfalls.html

22. [K22] NIST — Electromagnetic interference dataset from TIG arc welding: https://www.nist.gov/news-events/news/2025/02/nist-publishes-electromagnetic-interference-dataset-tig-arc-welding

23. [K23] NVIDIA Sionna RT — Releases: https://github.com/NVlabs/sionna-rt/releases

24. [K24] NVIDIA Sionna — Installation: https://nvlabs.github.io/sionna/installation.html

25. [K25] NVIDIA Sionna RT — Radio materials: https://nvlabs.github.io/sionna/rt/api/radio_materials.html

26. [K26] OpenPLC Runtime v3 — Archived repository: https://github.com/thiagoralves/OpenPLC_v3

27. [K27] OpenPLC Runtime v4 — Releases: https://github.com/Autonomy-Logic/openplc-runtime/releases

28. [K28] OpenPLC Editor v4.3.4: https://github.com/Autonomy-Logic/openplc-editor/releases/tag/v4.3.4

29. [K29] FUXA v1.3.5: https://github.com/frangoteam/FUXA/releases/tag/v1.3.5

30. [K30] PyModbus 3.16.2 documentation: https://pymodbus.readthedocs.io/en/stable/

31. [K31] opcua-asyncio v2.1.0: https://github.com/FreeOpcUa/opcua-asyncio/releases/tag/v2.1.0

32. [K32] SQLite — Write-Ahead Logging: https://www.sqlite.org/wal.html

33. [K33] Docker Docs — Compose startup order: https://docs.docker.com/compose/how-tos/startup-order/

34. [K34] OPC UA Part 4 — DataValue: https://reference.opcfoundation.org/specs/OPC-10000-4/7.11

35. [K35] NIST SP 800-82 Rev.3: https://csrc.nist.gov/pubs/sp/800/82/r3/final

36. [K36] NIST SP 800-82 Rev.4 Initial Public Draft: https://csrc.nist.gov/pubs/sp/800/82/r4/ipd

37. [K37] CISA — Recommended Cybersecurity Practices for Industrial Control Systems: https://www.cisa.gov/sites/default/files/publications/Cybersecurity_Best_Practices_for_Industrial_Control_Systems.pdf

### Kaynak kullanım notu

Sürüm numaraları ve yayımlanma tarihleri erişim anındaki resmî sayfalardan alınmıştır. Kütüphane ve araç sürümleri doğrudan üretim zorunluluğu değil, smoke test ve kilit işlemi için araştırılmış adaylardır. Nihai üretim kilidi hedef işletim sistemi ve donanım üzerinde doğrulanmalıdır.
