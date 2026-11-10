# Genel Sohbet Araştırma Bulguları

Tarih: 10 Kasım 2026
Çalışma alanı: 08.11.2026
Kapsam: Bu sohbetin başlangıcından bu rapor taslağına kadar edinilen portföy, RSSI verisi, mekânsal doğrulama ve OpenFence bulguları.
Durum: Araştırma ve planlama kaydıdır; ürün/saha kabulü değildir. Yeni deneyler ve entegrasyonlar NOT_RUN.

## 1. Yönetici özeti
Öncelik RF-C'de gerçek veri kabulü, koordinat anlamı, grup/blok/buffer ayrımı ve yeniden üretilebilir kanıt zinciridir. SCADA-01 çekirdek Modbus/OpenPLC kabulü korunmalıdır. OpenFence yeni bir yedinci ürün yerine RF-C ve SCADA-01 için isteğe bağlı dış sistem örneği olarak değerlendirilebilir. Ham veri indirme, yeni test koşumu veya uygulama değişikliği bu sohbette yapılmadı.

## 2. İncelenen başlangıç belgeleri
GitHub klasörü: https://github.com/kemaldemirag/calisma_raporlari/tree/main/08.11.2026
Altı rapor: Calisma_Alani_Durum_ve_Dogrulama_Raporu.md; Gelistirme_Plani_Arastirma_Raporu.md; RSSI_Ham_Verisi_Arastirma_Raporu.md; Referans_Kaynaklar_Calisma_Raporu_001_005.md; Son_Calismalar_Durum_ve_Dogrulama_Raporu.md; Sprint_4_Derin_Analiz_ve_Girisim_Raporu.md.
Geliştirme planının araç çıktısı kısaltılmıştı; belgenin tamamının incelendiği iddia edilmiyor.

## 3. Başlangıç durumunun kronolojik ayrımı
8 Kasım raporu: 53 PASS, 255 dosyada hash eşleşmesi, 27 geçerli JSON, altı üründe NOT_RUN ve henüz uzak yayın yok.
9 Kasım son çalışmalar raporu: altı özel GitHub deposu, ilk altı başarılı CI koşusu; toplam 100 keşfedilen test, 98 PASS, 2 SKIP, 0 FAIL; 280 dosya ve 34 geçerli JSON. RF-C yerel değişiklikleri henüz commit/push edilmemiş; uzak depo baseline düzeyinde. RF-C örneği 12 sentetik kayıt, üç fold, seed 42, sıfır buffer ve audit_only politika kullanıyor; raporlama PASS_WITH_WARNINGS, ürün kabulü NOT_RUN.
Bu sayılar önceki raporların beyanıdır; bu sohbette testler, hashler ve altı canlı ürün deposu bağımsız yeniden doğrulanmadı. Tarihsel kayıtlar güncel canlı durum diye sunulmamalıdır.
Açık tutarsızlıklar: yayın durumunun README/manifest ile uzlaştırılması; 100 testin PASS/SKIP ayrımı; tekrarlanabilir komutlarda PYTHONPATH veya paket kurulumunun belirtilmesi.

## 4. Portföy bağımlılıkları ve önceki planın iddiaları
RF-C metodolojisi → RF-01 kapsama sözleşmesi → RF-02 optimizasyon zinciri korunmalı. RF-B için etiket kökeni; RF-03 için hesaplama ortamı ve yakınsama ayrı kabul kapılarıdır.
Geliştirme planı 160 iş günü nominal + 15 rezerv, OpenPLC v4 geçişi, güncel ITU sürümleri, exact optimizasyon referansı ve erken RF-B/RF-03 risk denemeleri öneriyor. Bu takvim ve sürüm iddiaları bu sohbette bağımsız doğrulanmadı; uygulama bağımlılığına dönüştürülmeden resmî kaynak ve temiz ortamla kontrol edilmeli.
Sprint-4 raporu endüstriyel telemetri + spatial validation birleşimi, tek komut demo, run-manifest, kanıt matrisi ve kapsam sınırı öneriyor. Bu bir planlama önerisidir; uygulanmış entegrasyon kanıtı değildir.

## 5. Mekânsal doğrulama bulguları
blockCV kaynakları blok, grup ve tamponlu doğrulamayı ayrı yaklaşımlar olarak ele alıyor. Ayrı blokların sınırlarında eğitim ve test noktaları yakın kalabilir; sıfır blok örtüşmesi minimum fiziksel mesafeyi garanti etmez.
Ayrı raporlanacaklar: sample/group/block overlap; en yakın train-test mesafesi; buffer uygulanması ve ihlal sayısı; çıkarılan kayıt sayısı; kalan eğitim büyüklüğü; fold dağılımı.
Buffer mesafesi yalnız skoru iyileştirdiği için seçilmemeli; hedef kullanım ve mekânsal bağımlılık ölçeğiyle gerekçelendirilmeli. Otokorelasyon analizi başlangıç araştırmasıdır, tek başına evrensel kabul eşiği değildir.
Group ayrımı görülmemiş grup, spatial ayrım görülmemiş bölge sorusunu yanıtlar. En düşük/yüksek skor tek başına yöntemin üstünlüğünü göstermez.
Kaynaklar: https://cran.r-project.org/web/packages/blockCV/blockCV.pdf ; https://cran.r-project.org/web/packages/blockCV/vignettes/tutorial_1.html ; https://github.com/rvalavi/blockCV

## 6. RSSI veri adayları
### 6.1 Kadir Has — kaynak sayfası düzeyinde kontrol
https://data.mendeley.com/datasets/dh7j28t5kg/1
DOI: 10.17632/dh7j28t5kg.1
Kaynak açıklaması: 4 × 5 m alan, dört AP, 50 cm ölçüm aralığı, XML/NetSurveyor, Lenovo bilgisayar ve Intel Wireless-AC 8260; CC BY 4.0.
Önerilen kullanım: ilk XML adaptörü, ölçüm-konum eşleştirmesi ve fold görseli. Küçük alan bina/cihaz/tesis genellemesini kanıtlamaz. Ham arşiv ve XML alanları incelenmedi; konum eşleştirmesi açık iş.
### 6.2 UJIIndoorLoc — kaynak sayfası düzeyinde kontrol
https://archive.ics.uci.edu/dataset/310/ujiindoorloc
Kaynak açıklaması: 19.937 eğitim/referans ve 1.111 doğrulama/test kaydı, 520 WAP, üç bina, bina başına dört veya daha fazla kat, kullanıcı/telefon/zaman metadata'sı; CC BY 4.0.
RSSI -104 ile 0 dBm; 100 algılanmayan AP kodudur, +100 dBm değildir. Algılanmama durumu ile fiziksel RSSI ayrı ele alınmalı.
Longitude/Latitude adlı sütunların örnek değerleri yaklaşık -7.700 ve 4.865.000 düzeyinde; yalnız sütun adından WGS84 derece varsayılmamalı. Kaynak CRS ve birim açıklığa kavuşmadan metre tabanlı buffer kabulü verilmemeli.
Ham CSV sayımı, SHA-256, cihaz/grup dağılımı ve lisans dosyası kontrolü yapılmadı.
### 6.3 Yalnız önceki rapordan devralınan adaylar
Tampere TIE1/SAH1: https://zenodo.org/records/5174851
Long-Term Wi-Fi: https://zenodo.org/records/3748719
UVIndoorLoc-RTT&RSSI: https://zenodo.org/records/20051265
Bu üç aday bu sohbette bağımsız doğrulanmadı; nicelikleri ve CV uygunluğu kesin kabul edilmemeli.

## 7. Önerilen ilk RF-C deneyi
Soru: Aynı ölçüm verisinde random, device-group, spatial block ve buffered spatial ayrımlar hangi farklı değerlendirme koşullarını oluşturuyor?
Önce veri kabulü, sentinel, koordinat ve grup envanteri; ardından split/leakage raporu. Model performansı için hedef, özellikler, eğitim içi ön işleme ve metrikler ayrıca tanımlanmalı. Yalnız fold üretimi performans kıyası değildir.
Önerilen çıktılar: dataset_manifest.json, data_dictionary.md, sentinel_audit.json, coordinate_audit.json, group_inventory.csv, split_manifest.json, leakage_audit.json, cv_comparison.csv, spatial_folds.png. Tümü plan düzeyinde; üretilmedi.

## 8. OpenFence ön incelemesi
Kaynak: https://github.com/plyalex/OpenFence
README projeyi GPS konumu, stereo ses uyarısı, LoRa üzerinden sınır aktarımı ve web hareket kaydı kullanan sanal hayvancılık çiti sistemi olarak tanımlıyor. Arduino, TinyGPS++ ve RTCZero belirtiliyor. GPL v3 beyanı var; LICENSE metni bağımsız okunmadı.
İncelenen yapı: hardware/pcbs, hardware/solidworks, software/collar, software/examples, software/repeater, software/web; kökte openfence-report.pdf ve LICENSE.
Firmware, PCB ve PDF içeriği ayrıntılı incelenmedi. Commit SHA sabitlenmedi; derleme, donanım/saha testi yapılmadı. Hazır RSSI veri kümesi, arıza etiketi, teslim garantisi veya doğrulanmış radyo performansı bulunduğu kabul edilmiyor.

## 9. OpenFence'in mevcut repolarda kullanımı
| Repo | Önerilen katkı | Sınır / öncelik |
| --- | --- | --- |
| spatial-validation-audit | Konum izlerinde cihaz/oturum/spatial ayrım örneği | Metadata doğrulanmalı; yüksek öncelik |
| industrial-telemetry-validation | Örnek adaptör, stale/gecikme/tekrar/kesinti testleri | Modbus/OpenPLC kabulünün yerine geçmez; çekirdek kabulden sonra |
| indoor-coverage-prediction | Ayrı dış ortam LoRa araştırma örneği | Indoor doğruluğunu kanıtlamaz; düşük öncelik |
| ap-placement-optimizer | Baz istasyonu yerleşimi senaryosu | Doğrulanmış coverage matrix ve amaç fonksiyonu gerekir; sonraki aşama |
| wireless-fault-detection-benchmark | Kontrollü iletişim bozulması | Paket/GPS kaybı otomatik arıza etiketi değildir; düşük öncelik |
| warehouse-radio-digital-twin | Mimari karşılaştırma | Sionna sahnesi ve malzeme verisi sağlamaz; çok düşük öncelik |
Önerilen ortak akış: sentetik/ doğrulanmış konum kaydı → adaptör → RF-C audit; aynı kayıttan SCADA telemetri/historian kalite örneği. Yeni yedinci ürün önerilmiyor.
Önerilen alanlar: record_id, device_id, session_id, timestamp_utc, x_m, y_m, position_valid, position_age_ms; label yalnız kökeni varsa. Bunlar OpenFence'in doğrulanmış kayıt alanları değil, önerilen sözleşmedir.

## 10. OpenFence açık inceleme soruları
Geçersiz/eski GPS; sınır sürümü ve yarım güncelleme; timeout ve bağlantısız davranış; yeniden başlatmada kalıcılık; tekrarlı/sıra dışı mesaj; web'de güncel/son bilinen veri ayrımı. Bunlar tespit edilmiş kusurlar değildir.
Kod/donanım dosyası kopyalamadan önce lisans ve bağımlılık koşulları incelenmeli. Ayrı klasör kullanmak lisans değerlendirmesinin yerine geçmez. İlk aşamada referans gösterme, bağımsız gereksinim/test ve açıkça sentetik fixture öneriliyor.
Canlı hayvan, fiziksel uyarı etkinliği ve saha güvenliği bu çalışmanın dışında. Sentetik ve tezgâh testinden hayvan güvenliği iddiası çıkarılmamalı.

## 11. Öncelikli takip işleri
1. Canlı RF-C kod durumu ile önceki rapor beyanlarını ayır; commit SHA kaydet.
2. İki SKIP testin koşullarını ve temiz ortam komutunu doğrula.
3. Veri kaynağı, lisans, SHA-256, sentinel, CRS ve grup envanterini tamamla.
4. Blok/grup/buffer negatif testlerini ayrı tasarla.
5. İlk veri kümesinde tekrarlanabilir audit ve gerekiyorsa model kıyası üret.
6. OpenFence commit/lisans ve gerçek mesaj şemasını incele.
7. RF-C örneğini küçük tut; SCADA çekirdek kabulünü geciktirmeden isteğe bağlı adaptörü değerlendir.
8. Her iddiayı gereksinim → kaynak → test → artefakt bağlantısıyla izle.

## 12. Durum ve kapsam sınırı
Bu rapor kaynak açıklaması kontrollerini, önceki belgelerin beyanlarını ve araştırma önerilerini ayırır. Deneyler, ham veri denetimi, yeniden derleme, entegrasyon, saha ve ürün kabulü NOT_RUN. Önceki konuşmada onaya sunulan yalnız OpenFence raporu için henüz oluşturma işlemi yapılmadı; bu genel rapor onun yerine öneriliyor. Bu belge mevcut README/manifest/test durumlarını değiştirmez.
