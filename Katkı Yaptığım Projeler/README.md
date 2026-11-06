# Katkı Yaptığım Projeler Geliştirme Durum ve Doğrulama Raporu

**Rapor dönemi:** 1-5 Kasım 2026

**Rapor tarihi:** 6 Kasım 2026

**Çalışma alanı:** `C:\Users\jagua\OneDrive\Masaüstü\Katkı Yaptığım Projeler`
**Ayrıntılı Word sürümü:** [Katki_Yaptigim_Projeler_Gelistirme_Durum_Raporu_2026-11-06.docx](Katki_Yaptigim_Projeler_Gelistirme_Durum_Raporu_2026-11-06.docx)

## Yönetici özeti

Çalışma alanında iki etkin tarihli kümede 15 repo, ayrı `Forkladığım Repolar` envanterinde 4 repo bulunuyor. Dokuz repoda yerel geliştirme yapıldığı doğrulandı. Bu geliştirmeler, mevcut yerel `origin` izleme referanslarına göre 12 commit, 55 farklı dosya, 2.527 ekleme ve 141 silme oluşturuyor.

Yedi repoda çalıştırılmış birim, host veya sözleşme testi kanıtı var. `80x86` ve `fpga_nes` değişiklikleri statik kontrollerle doğrulandı; gerekli eski araç zincirleri ve fiziksel FPGA bağlantısı bulunmadığı için yerel native derleme ve donanım testi çalıştırılmadı. FPGA, MCU, motor, servo, Unity/XR ve gerçek seri bağlantı davranışları için kalan fiziksel doğrulama sınırları raporlarda açıkça korunuyor.

Geliştirme commitleri kaynak repoların uzak dallarına gönderilmedi ve upstream pull request açılmadı. Dokuz geliştirme reposunun yerel dalı kendi izlenen `origin` dalından ileride. `irremoteesp8266` içinde commit dışı bir kullanıcı ortamı ayarı bulunuyor; diğer sekiz geliştirme reposunun çalışma ağacı temiz.

| Gösterge | Sonuç |
|---|---:|
| Etkin tarihli alanlardaki repo | 15 |
| Ayrı fork envanterindeki repo | 4 |
| Yerel geliştirme yapılan repo | 9 |
| Yerel katkı commitleri | 12 |
| Değişen dosya | 55 |
| Satır farkı | +2.527 / -141 |
| Çalıştırılmış test kanıtı bulunan geliştirme reposu | 7 |
| Kaynak repolara push veya PR | 0 |

## Kapsam ve yöntem

Ana geliştirme kapsamı `01.11.2026` ve `02.11.2026` klasörleridir. `Forkladığım Repolar/01.11.2026` ayrı bir repo ve upstream eşleme envanteri olarak değerlendirildi. `tmp` altındaki yanlış yedekler, geçici render çıktıları ve araç dosyaları geliştirme toplamlarına katılmadı. `irremoteesp8266/lib/googletest` iç içe bağımlılık reposu ayrıca sayılmadı.

Sonuçlar, çalışma alanındaki README ve manifestler, sprint kapanış raporları, test kanıtı dosyaları, mevcut Git logları, çalışma ağacı durumları ve yerel `origin` izleme referanslarına göre çıkarıldı. Kaynak repolarda bu denetim sırasında `git fetch` çalıştırılmadı; bu nedenle ileride veya geride olma değerlendirmesi mevcut yerel uzak dal kayıtlarının anlık görüntüsüdür.

## Çalışma alanı envanteri

| Alan | Repo sayısı | Geliştirme durumu | Açıklama |
|---|---:|---:|---|
| `01.11.2026` | 3 | 2 geliştirildi | `80x86` ve `fpga_nes` için Sprint 1 tamamlandı; `i2c-moisture-sensor` ertelendi. |
| `02.11.2026` | 12 | 7 geliştirildi | IRremoteESP8266 ve altı ek repo için test odaklı sprintler tamamlandı; beş repo yalnız entegre edildi. |
| `Forkladığım Repolar/01.11.2026` | 4 | Kod değişikliği yok | Fork ve upstream eşlemeleri doğrulandı; ana geliştirme toplamına katılmadı. |
| **Toplam** | **19** | **9 geliştirildi** | 12 yerel katkı commit'i doğrulandı. |

## Kronoloji

### 1 Kasım 2026

`01.11.2026` çalışma alanı `80x86`, `fpga_nes` ve `i2c-moisture-sensor` repolarıyla kuruldu; manifest, repo indeksi ve klonlama doğrulama kayıtları oluşturuldu. Aynı gün tamamlanan Sprint 1 kapsamında:

- `80x86` Core arayüzü ile Intel 80186 pin grupları arasında kaynaklı teknik eşleme belgelendi.
- `fpga_nes` NesDbg uygulamasındaki sabit COM5 bağımlılığı kaldırıldı; COM5 varsayılanı korunarak seri port seçimi güvenli ve test edilebilir hale getirildi.
- `i2c-moisture-sensor` Sprint 2 kapsamına bırakıldı ve kaynak kodu değiştirilmedi.

### 2 ve 3 Kasım 2026

`02.11.2026` alanı önce IRremoteESP8266 odaklı kuruldu. Daha önce yanlış kaynak listesinden alınan sekiz klon ve bunlara bağlı hatalı raporlar etkin alandan çıkarıldı; geri kazanılabilir yedek `tmp/02.11.2026-yanlis-yedek` altında korundu. Kullanıcının GitHub ekran görüntülerindeki kesin liste esas alınarak IRremoteESP8266 korundu ve 11 repo daha aynı çıktı alanına eklendi.

Entegrasyonda `altste.github.io` için Windows büyük-küçük harf çakışmaları belgelendi, `ELIZA/research/kit` alt modülü başlatılmadı, `gimble-motor-spring` LFS nesnesi alındı ve `Arduino-FOC` uzun yol desteğiyle klonlandı.

### 4 Kasım 2026

Dört geliştirme kapanışı tamamlandı:

- IRremoteESP8266 AC durum geçişleri, DAIKIN128 önceki durum çözümlemesi ve Windows test yakalama kararlılığı.
- GST deterministik durum makinesi, simülasyon, sensör ve Kalman sözleşmeleri.
- Motor sürücülerinde başlangıç, devre dışı bırakma, PWM sınırı, mirror ve VNH5019 pin sözleşmeleri.
- Omega3 disket sürücüsünde atomik ADF değiştirme, sınır kontrolleri, yaşam döngüsü ve DSKBYTR sözleşmeleri.

### 5 Kasım 2026

Üç yeni sprint ve bir ek build geliştirmesi kaydedildi:

- `inf1900-107111` AVR motor hız telafisindeki taşma düzeltildi ve diferansiyel sürüş modeli eklendi.
- `gimble-motor-spring` için Unity'den bağımsız sayısal yay çekirdeği ve kararlılık korumaları eklendi.
- `ch592-android-compiler` Servo API durumu, hata aktarımı ve darbe dönüşümü düzeltildi.
- `Omega3` için Windows altında SDL3 uygulama hedefi eklendi. Bu commit çalışma alanında mevcut, ancak bağımsız kapanış veya tam uygulama test kanıtı bulunmuyor.

## Repo bazlı geliştirmeler

### 80x86

**Commit:** `db6fd678ff094d8c07720344aa3cb343a91b166f`

**Değişiklik:** 1 dosya, +274 satır

`documentation/development-guide.asciidoc` içine Core arayüzündeki 26 portu Intel 80186 pin gruplarıyla karşılaştıran bölüm eklendi. Eşleme, doğrudan eşdeğer, adaptör gerektiren, desteklenmeyen ve belirsiz işlevleri ayırıyor. `irq[7:0]`, byte seçimi, instruction fetch erişimleri ve Core sınırında bulunmayan DRQ, TEST, timer, chip select ve HOLD/HLDA işlevleri açıklığa kavuşturuldu.

Statik port kapsamı ve `git diff --check` geçti. Docker, Asciidoctor ve ilgili build araçları bulunmadığından belge PDF üretimi çalıştırılmadı. Fiziksel 80186 bus adaptörü uygulanmadı.

### fpga_nes

**Commit:** `120f2204b2a39611f64ea6a21b31ffabf1c3c5d7`

**Değişiklik:** 11 dosya, +489 / -21 satır

NesDbg artık argümansız çalışmada COM5 varsayılanını koruyor; `7` veya `COM12` biçiminde `COM1` ile `COM9999` arasında bir seri port kabul ediyor. Girdi kanonik Windows aygıt yoluna çevriliyor, geçersiz argümanlar `CreateFile` öncesinde reddediliyor ve seri handle yaşam döngüsü güvenli hale getiriliyor. Proje dosyaları, README ve 27 parser vakasını içeren test kaynağı güncellendi.

Proje XML'i, protokol sabitleri ve parser kaynak kapsamı statik olarak doğrulandı. Visual Studio 2010 veya uyumlu MSBuild bulunmadığı için uygulama ve parser derlemesi çalıştırılmadı; gerçek USB-UART ve FPGA echo testi yapılmadı.

### irremoteesp8266

**Commitler:** `4c339fc8`, `1c8e1d2e`

**Değişiklik:** 4 dosya, +172 / -7 satır

Dokuz boole AC alanı için 36 geçiş senaryosu, MIDEA salınım senaryoları ve DAIKIN128 önceki güç durumu doğrulamaları eklendi. Birim test derlemelerinde IR gönderim frekansı ve yakalama metadata tamponları deterministik biçimde başlatıldı ve sıfırlandı.

IRac 89/89, Daikin 149/149, IRsend 28/28, Lego 5/5 ve tam paket 83/83 test ikilisi geçti. Seçilen dört mutasyonun tamamı testler tarafından yakalandı; cpplint ve `git diff --check` temizdi.

Çalışma ağacında commit dışı `.vscode/settings.json` değişikliği bulunuyor. Değişiklik, kullanıcı makinesindeki `lib/googletest` yolunu `cmake.sourceDirectory` olarak ekliyor ve sprint commitlerine dahil edilmedi.

### GST

**Commit:** `f4c06f2`

**Değişiklik:** 6 dosya, +235 / -2 satır

Durum makinesi için guard, ilk eşleşen geçiş, callback sırası, geçersiz hedef ve reset sözleşmeleri eklendi. Simülasyon ve sensörler seed edilebilir hale getirildi; stuck-at-zero arızası ve deterministik Kalman davranışı kapsandı.

Baseline derleme 30/30, temiz derleme 32/32, CTest 1/1 ve sözleşme senaryoları 8/8 geçti. Dört mutasyonun tamamı yakalandı. Fiziksel donanım testi yapılmadı.

### Motor

**Commitler:** `702e493`, `1052abb`

**Değişiklik:** 6 dosya, +305 / -21 satır

DualPWM, DualPWMEnable ve FourWire başlangıç durumları deterministik hale getirildi. Devre dışı bırakma sırası, PWM doygunluğu, mirror davranışı ve VNH5019 enable/PWM pin aktarımı düzeltildi ve sürücü sözleşmeleri belgelendi.

Temiz build, CTest 1/1 ve yedi sözleşme senaryosu geçti. PWM sınır matrisi 28 kombinasyonu kapsadı ve beş mutasyonun tamamı yakalandı. Testler yazılım pin aktarımını doğruluyor; fiziksel motor, akım ve güvenli duruş davranışını kanıtlamıyor.

### Omega3

**Commitler:** `59dcfc1`, `e447cf2`

**Değişiklik:** 9 farklı dosya, +407 / -27 satır

ADF replacement işlemi, yeni dosya doğrulanmadan mevcut diski değiştirmeyecek şekilde atomik hale getirildi. Track, side ve drive sınırları korundu; disk tamponu yaşam döngüsü ve kopyalama davranışı güvenli hale getirildi; DSKBYTR üretimi tek test edilebilir sözleşmede toplandı. Sonraki commit Windows altında SDL3 uygulama hedefi ve ilgili başlangıç düzenlemelerini ekledi.

Disk sürücüsü RED aşamasında 1/4 senaryodan GREEN aşamasında 5/5 senaryoya çıktı. CTest 1/1 ve beş mutasyonun tamamı geçti. Host testleri tam SDL uygulamasını, cycle accuracy'yi veya fiziksel disket davranışını kanıtlamıyor. `e447cf2` SDL3 build commit'i için ayrıca kaydedilmiş bağımsız kapanış testi bulunmuyor.

### inf1900-107111

**Commit:** `8ef1e0f`

**Değişiklik:** 7 dosya, +224 / -3 satır

AVR motor, tekerlek ve timer kodu sahte register modeliyle host ortamında test edilebilir hale getirildi. Sağ ve sol spin hız telafisinde `uint8_t` taşması 16 bit ara hesap ve 255 doygunluğuyla giderildi. Diferansiyel sürüş, Timer2 register izi ve PWM sınırları kapsandı.

AVR baseline derlemesi geçti; host build 6/6 ve CTest 1/1 tamamlandı. Fiziksel MCU flash, motor ve elektriksel güvenlik testi yapılmadı. Repoda açık lisans bildirimi bulunmadığı için değişiklikler yerel tutuldu.

### gimble-motor-spring

**Commit:** `d94ca26`

**Değişiklik:** 5 dosya, +211 / -27 satır

Unity'den bağımsız `SpringDynamics` çekirdeği oluşturuldu. Büyük frame delta değerleri kararlı alt adımlara bölündü; geçersiz veya sonlu olmayan parametreler reddedildi; sıfır `maxAngle` ve pasif-aktif mod geçişleri kontrollü hale getirildi.

PowerShell `Add-Type` ile aynı C# kaynak kodunu kullanan host testi geçti. Unity Editor, sahne, XR input, render frame ve fiziksel force-feedback doğrulanmadı. Repoda açık lisans bildirimi bulunmadığı için upstream yayın yapılmadı.

### ch592-android-compiler

**Commit:** `ed3600a`

**Değişiklik:** 6 dosya, +210 / -33 satır

Servo nesnesinin başlangıç ve attach durumları, backend hata aktarımı, açı ve darbe sınırları, mikrosaniye-zamanlayıcı tiki dönüşümü ve yinelenebilir `detach` davranışı düzeltildi. API belgeleri gerçek imzalarla uyumlu hale getirildi.

RED aşamasındaki başlangıç durumu hatasından sonra CTest 1/1 ve 18 Servo doğrulaması geçti. Testler host tabanlı sahte donanım arka ucunu kullanıyor; fiziksel CH592, PWM dalga şekli ve servo hareketi doğrulanmadı.

## Entegre edilen ancak geliştirilmeden kalan repolar

Etkin alanlarda `i2c-moisture-sensor`, `altste.github.io`, `Arduino-FOC`, `ELIZA`, `Hydro-Recomp` ve `Stepper` için bu dönemde yerel katkı commit'i yok. Bunlar klonlama, envanter ve platform istisnası kayıtlarıyla çalışma alanına dahil edildi.

Ayrı fork alanındaki `CNCU-01`, `FPGA-UART`, `stm32-can-modbus-gateway` ve `STM32F4-Eval-board` repolarında kod değişikliği yok. Origin ve upstream eşlemeleri doğrulandı.

## Yerel katkı özeti

| Repo | Yerel commitler | Dosya ve satır farkı | İzleme durumu |
|---|---|---:|---|
| `80x86` | `db6fd67` | 1 dosya, +274 | `origin/master` önünde 1 |
| `fpga_nes` | `120f220` | 11 dosya, +489 / -21 | `origin/master` önünde 1 |
| `irremoteesp8266` | `4c339fc`, `1c8e1d2` | 4 dosya, +172 / -7 | `origin/master` önünde 2; çalışma ağacı değişik |
| `GST` | `f4c06f2` | 6 dosya, +235 / -2 | `origin/master` önünde 1 |
| `Motor` | `702e493`, `1052abb` | 6 dosya, +305 / -21 | `origin/master` önünde 2 |
| `Omega3` | `59dcfc1`, `e447cf2` | 9 dosya, +407 / -27 | `origin/main` önünde 2 |
| `inf1900-107111` | `8ef1e0f` | 7 dosya, +224 / -3 | `origin/master` önünde 1 |
| `gimble-motor-spring` | `d94ca26` | 5 dosya, +211 / -27 | `origin/main` önünde 1 |
| `ch592-android-compiler` | `ed3600a` | 6 dosya, +210 / -33 | `origin/main` önünde 1 |

## Açık riskler ve önerilen sonraki adımlar

1. Kaynak repolara yayın kararı repo bazında verilmelidir. Her repo için önce uzak dallar yenilenmeli, yerel commitler yeniden gözden geçirilmeli ve ayrı PR hazırlanmalıdır.
2. `inf1900-107111` ve `gimble-motor-spring` için lisans veya maintainer izni netleşmeden upstream yayın yapılmamalıdır.
3. FPGA, USB-UART, AVR/CH592 kartları, motor/servo düzenekleri ve Unity/XR sahnesiyle fiziksel doğrulama tamamlanmalıdır. Host testlerinin kanıt sınırı korunmalıdır.
4. `fpga_nes` Visual Studio uyumlu araç zincirinde, `80x86` belge çıktısı proje Docker ortamında derlenmelidir.
5. `Omega3` içindeki `e447cf2` Windows SDL3 uygulama commit'i için temiz build ve uygulama başlangıç testi ayrı kanıtla kapatılmalıdır.
6. `irremoteesp8266/.vscode/settings.json` değişikliğinin kullanıcıya özel kalıp kalmayacağı belirlenmeli; otomatik olarak sprint commitlerine eklenmemelidir.

## Kanıt kaynakları

Başlıca yerel kanıtlar:

- `01.11.2026/README.md`
- `01.11.2026/003-Proje Kayıtları/002-Teknik Çıktı Kayıtları/CLONE_REPORT.md`
- `01.11.2026/003-Proje Kayıtları/002-Teknik Çıktı Kayıtları/SPRINT_1_GELISTIRME_RAPORU.docx`
- `02.11.2026/README.md`
- `02.11.2026/NEXT-TASKS.md`
- `02.11.2026/003-Proje Kayıtları/002-Teknik Çıktı Kayıtları/CLONE_REPORT.md`
- `02.11.2026/003-Proje Kayıtları/002-Teknik Çıktı Kayıtları/BASELINE-REPORT.md`
- `02.11.2026/003-Proje Kayıtları/002-Teknik Çıktı Kayıtları/04.11.2026-SPRINT-1-KAPANIS-RAPORU.docx`
- `02.11.2026/003-Proje Kayıtları/002-Teknik Çıktı Kayıtları/04.11.2026-SPRINT-2-KAPANIS-RAPORU.docx`
- `02.11.2026/003-Proje Kayıtları/002-Teknik Çıktı Kayıtları/04.11.2026-SPRINT-3-KAPANIS-RAPORU.docx`
- `02.11.2026/003-Proje Kayıtları/002-Teknik Çıktı Kayıtları/04.11.2026-SPRINT-4-KAPANIS-RAPORU.docx`
- `02.11.2026/003-Proje Kayıtları/002-Teknik Çıktı Kayıtları/05.11.2026-SPRINT-5-KAPANIS-RAPORU.docx`
- `02.11.2026/003-Proje Kayıtları/002-Teknik Çıktı Kayıtları/05.11.2026-SPRINT-6-KAPANIS-RAPORU.docx`
- `02.11.2026/003-Proje Kayıtları/002-Teknik Çıktı Kayıtları/05.11.2026-SPRINT-7-KAPANIS-RAPORU.docx`
- Aynı teknik kayıt klasörlerindeki `*-TEST-KANITI.txt` dosyaları
- 6 Kasım 2026 tarihinde alınan yerel Git log, status ve diff istatistikleri

## Sonuç

Çalışma alanı yalnız repo toplama aşamasında kalmadı. Dokuz repoda izlenebilir yerel geliştirme, yedi repoda çalıştırılmış test kanıtı ve iki repoda statik doğrulama üretildi. En güçlü ortak yaklaşım, davranış sözleşmelerini host ortamında deterministik testlere dönüştürmek ve donanım kanıtı bulunmayan sonuçları açıkça sınırlamak oldu. Bir sonraki aşama, kalan fiziksel doğrulamaları tamamlamak ve yayınlanması uygun katkıları repo bazında upstream incelemeye hazırlamaktır.
