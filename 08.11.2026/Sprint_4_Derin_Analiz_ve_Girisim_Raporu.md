# 09.11.2026 — Sprint-4 Derin Analiz ve Endüstriyel Köprü Girişimi Raporu

## 1) Yönetici Özeti
Bu rapor, `spatial-validation-audit` için başvuru odaklı farklılaşma ekseninde yapılan incelemenin çıktısını sunar. Ana karar, teknik olarak en güçlü ayrışmanın **SCADA/OT telemetri simülatörü + spatial validation** birleşimiyle elde edileceğidir.

Mevcut durum bir Sprint-1 baseline doğrulamasıdır: sözleşme kontrollü veri yükleme, deterministik split stratejileri, audit çıktıları ve CI çalışmaları mevcuttur; ürün kabul durumu bilinçli olarak `NOT_RUN` tutulmaktadır. Bu yaklaşım doğru, fakat başvuru etkisi için Sprint-4’te teknik doğrulamanın **kanıtlı ürün anlatısına** dönüştürülmesi gerekir.

## 2) Araştırma Kapsamı
İncelenen kaynaklar:
- Çalışma raporları: `08.11.2026/*`
- Uygulama deposu: `kemaldemirag/spatial-validation-audit`
- İlişkili referans ekosistemi:
  - Spatial CV: `rvalavi/blockCV`, `SamComber/spacv`, `geoai-lab/spatialCV`, `sowsalim01/spatialcvR`
  - Dengesiz veri: `scikit-learn-contrib/imbalanced-learn`
  - Belirsizlik/kalibrasyon: `scikit-learn-contrib/MAPIE`
  - Modelleme tabanı: `scikit-learn/scikit-learn`

## 3) Kritik Bulgular

### 3.1 Mevcut Teknik Güçlü Yanlar
- Sıkı veri sözleşmesi ve görünür hata davranışı (`dataset/contract.py`).
- Deterministik split politikaları: random/group/spatial block (`splits/*`).
- Audit çıktıları: group overlap, class distribution, minimum distance (`audit/*`).
- Makine-okunur CLI özeti ve CI ile temel doğrulama (`scripts/run_audit.py`, `.github/workflows/ci.yml`).
- Kapsam sınırları açık: saha/ürün kabul iddiası yapılmıyor (`NOT_RUN`).

### 3.2 Başvuru Açısından Ana Boşluk
- Sistem teknik olarak doğru bir baseline olsa da işe alım panelinin görmek istediği “etki + operasyon bağlamı + karar gerekçesi” üçlüsü tek akışta paketlenmiş değil.
- Referans metodolojiler belgede izlenebilir olsa da karşılaştırmalı entegrasyon çıktısı henüz sınırlı.

### 3.3 Farklılaşma Kararı
- En güçlü farklı girişim: **Endüstriyel köprü**
  - OT telemetri simülasyonu (Modbus/OPC-UA benzeşimi)
  - Spatial validation pipeline ile birleşik audit
  - Tek komutla kanıt üretimi

## 4) Sprint-4 Derin Hedef (Spesifik)
Sprint-4 amacı: çalışan teknik hattı, başvuru değerlendirmesinde hızlı güven üreten bir ürün anlatısına dönüştürmek.

### 4.1 Zorunlu Çıktılar
1. `README.md` üst akış: Problem → Neden önemli → Mimari → Demo komutu → Ölçülen sonuç.
2. Tek komut demo betiği: örnek audit çıktısı üretimi.
3. Run manifest: commit/config/input/output hash zinciri.
4. Etki özeti: leakage, class balance, minimum distance, worst-zone tek tabloda.
5. Scope boundary: doğrulanan/doğrulanmayan alanların açık beyanı.
6. Verification matrix: her gereksinime kanıt bağlantısı.
7. One-pager başvuru özeti.
8. 10 dakikalık görüşme anlatım script’i.

### 4.2 Kabul Kriterleri
- Temiz ortamda tek komut demo çalışır.
- Aynı seed ile tekrar üretilebilir sonuç alınır.
- Requirement satırlarının tamamı bir kanıt artifact’ine bağlanır.
- `NOT_RUN` kapsam sınırı görünür biçimde korunur.

## 5) İş Yükü ve Zaman
- Sprint-4 derin paket: **2–3 iş günü**
- Önkoşul: Sprint-1/2/3 çıktılarının stabilize olması.

Önerilen dağılım:
- Gün-1: README + demo komutu + scope boundary
- Gün-2: run manifest + impact summary + matrix linkleme
- Gün-3: one-pager + interview script + temiz ortam prova

## 6) Riskler ve Önlemler
- Risk: Teknik detay bolluğu, düşük hikâye netliği.
  - Önlem: README ilk ekranını karar ve etki odaklı tutmak.
- Risk: PASS sonuçlarının ürün kabulü gibi algılanması.
  - Önlem: Her ana belgede `NOT_RUN` kapsam satırı.
- Risk: Demo kırılması.
  - Önlem: Tek komut + deterministik seed + temiz ortam dry-run.

## 7) Sonuç
Bu portföyde teknik temel doğru kurulmuştur. Başvuru etkisini büyütecek kaldıraç, yeni model karmaşıklığından çok **endüstriyel bağlamlı uçtan uca kanıt paketi** üretmektir. Sprint-4’ün derinleşmesi, bu dönüşümün en kısa ve en yüksek getirili adımıdır.
