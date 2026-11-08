# 08.11.2026 — RSSI Ham Verisi Araştırma Raporu

**Kapsam:** 08.11.2026 Araştırma Kayıtları ve RF-C / RF-01 / RF-B teknik veri gereksinimleri.

**Durum:** Kaynak adayı ve veri açıklaması düzeyinde araştırma. Ham arşivler indirilip şema, lisans ve ölçüm protokolü dosya düzeyinde henüz doğrulanmadı. Deneyler NOT_RUN.

## 1. Araştırma sorusu

Gerçek RSSI ham gözlemlerinin ölçüm değeri, konum, erişim noktası, cihaz, zaman, bina/kat ve oturum bilgileriyle birlikte bulunması; Random/Group/Spatial/Temporal CV karşılaştırmalarını desteklemesi.

Önerilen standart alanlar: `rssi_dbm`, `x`, `y`, `floor`, `ap_id`, `device_id`, `timestamp`, `site_id`, `session_id`. Her veri kümesinde hepsi bulunmayabilir.

## 2. Veri kümesi adayları

### D01 — Kadir Has Üniversitesi, Indoor Environment WiFi-RSSI

Mendeley Data DOI 10.17632/dh7j28t5kg; https://data.mendeley.com/datasets/dh7j28t5kg/1

Kaynak açıklamasına göre İstanbul'da yaklaşık 4×5 m alanda, dört AP ile 50 cm aralıklı ölçümler; Raw RSSI Data.rar / XML. Lisans açıklamasında CC BY 4.0. RF-C mekânsal ayrım için ilk aday; küçük alan ve veri yoğunluğu genelleme sınırıdır.

### D02 — Tampere University TIE1 / SAH1

Zenodo DOI 10.5281/zenodo.5174851; https://zenodo.org/records/5174851

İki bina; açıklamada TIE1 10.633 eğitim ölçümü / 613 AP, SAH1 9.291 eğitim ölçümü / 775 AP; RSSI ve X/Y/Z koordinat CSV. RF-C bina bazlı ayrım ve RF-01 modelleme adayı.

### D03 — UJIIndoorLoc

UCI https://archive.ics.uci.edu/dataset/310/ujiindoorloc

Açıklamada 19.937 eğitim, 1.111 doğrulama kaydı, üç bina, 520 Wi-Fi AP, koordinat, bina/kat, kullanıcı, telefon ve zaman alanları. Random / Group / bina bazlı CV için aday.

### D04 — Long-Term Wi-Fi Fingerprinting Dataset

Zenodo https://zenodo.org/records/3748719

Açıklamada 25 ay ve toplam 103.584 fingerprint kaydı; zamansal dağılım kayması ve Temporal CV için aday.

### D05 — UVIndoorLoc-RTT&RSSI (2026)

Zenodo DOI 10.5281/zenodo.20051265; https://zenodo.org/records/20051265

Kaynak açıklamasında 228 referans konumu, üç senaryo, 20 AP, üç Android cihazı; RSSI/RTT, CC BY 4.0 ve baseline paketi. Cihazlar arası doğrulama için aday.

Bu nicelikler kaynak açıklamalarından alınmıştır; dosya bazında sayım yapılmadı.

## 3. CV uygunluk ön değerlendirmesi

- Kadir Has: Spatial güçlü aday; Group sınırlı; Temporal belirsiz.

- Tampere: Spatial güçlü aday; bina bazlı Group olası; Temporal belirsiz.

- UJIIndoorLoc: Spatial ve Group aday; Temporal sınırlı.

- Long-Term Wi-Fi: Temporal güçlü aday; kampanya bazlı Group değerlendirilmeli.

- UVIndoorLoc: Spatial ve cihaz bazlı Group aday; Temporal incelenmeli.

Uygunluk, gerçek ayrım protokolü ve grup bağımsızlığı doğrulanana kadar kesin kabul değildir.

## 4. Veri kalitesi ve sızıntı riskleri

UJIIndoorLoc ve Tampere türü Wi-Fi fingerprint verilerinde 100 gibi özel değerler 'AP algılanmadı' anlamına gelebilir; gerçek +100 dBm gibi işlenmemeli. Her veri kümesinin sentinel tanımı ayrıca doğrulanmalı.

Koordinat referans sistemi, kat ve bina ID, tekrar ölçümleri, AP sıralaması, oturum zamanları, eksik RSSI, ölçüm sansürü ve lisans koşulları incelenmeli.

Ön işleme (imputation, scaling, resampling, feature selection) yalnız eğitim fold'unda öğrenilmeli. GroupKFold coğrafi tamponu otomatik garanti etmez. Sentetik ve gerçek ölçümler ayrı etiketlenmeli.

## 5. Ürün / sprint / mühendislik kanıtı

- RF-C Sprint 1: data dictionary, şema dönüştürme, sentinel audit, koordinat ve grup envanteri.

- RF-C Sprint 2: Random KFold / GroupKFold / Spatial Block / Buffered CV; grup örtüşmesi, minimum train-test mesafesi ve fold başına nadir RSSI örnek sayısı.

- RF-C Sprint 3: `cv_comparison.csv`, `leakage_audit.json`, `spatial_folds.png`, `worst_zone_metrics.csv`, `validation_report.pdf`.

- RF-01: ölçümden RSSI haritası ve gerçek/sentetik ayrımı; RF-B: ancak uygun arıza etiketi varsa benchmark, RSSI fingerprint tek başına arıza etiketi değildir.

## 6. Öncelik sırası

1. P1: Kadir Has Raw RSSI Data.rar arşivindeki XML alanlarını, ölçüm konumu eşleştirmesini ve lisansı doğrula.

2. P2: Tampere ve UJIIndoorLoc dosyalarını indirip koordinat, grup, sentinel ve tekrarlı ölçüm şemasını karşılaştır.

3. P3: Long-Term Wi-Fi ile Temporal CV ve UVIndoorLoc ile cihazlar arası aktarım protokolünü değerlendir.

4. P4: E01–E08 deney matrisine veri kümesi uygunluk tablosu hazırla; yalnız çalıştırılmış deneylere PASS/FAIL ata.

## 7. İzlenebilirlik ve sınırlar

Kaynaklar veri kümesi adayıdır. Ham dosyaların bütünlüğü (SHA256), lisans sürümü, DOI versiyonu, erişim durumu ve veri sözlüğü henüz dosya bazında denetlenmedi.

Gerçek veri olmadan fiziksel performans iddiası kurulmaz. Yeni GitHub reposu, upstream PR veya mevcut çalışma alanında değişiklik yapılmadı.

Bağlam: https://drive.google.com/drive/folders/1V0ozIsZtSU0wLCt6NDh_vnJ7u6-sFd42
