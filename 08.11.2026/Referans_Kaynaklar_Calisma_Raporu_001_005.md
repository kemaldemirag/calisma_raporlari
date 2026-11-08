# 08.11.2026 — Referans Kaynaklar Çalışma Raporu (001–005)

**Kapsam:** 08.11.2026 Model Raporları; RF-C, SCADA-01, RF-01, RF-02, RF-B, RF-03.

**Durum:** Araştırma envanteri; testler NOT_RUN. Yeni repo veya PR oluşturulmadı.

## 001 — Oynatma Listesi İçerikleri

- PL-01 RF-C: Spatial cross validation, blockCV ve leakage; uygulamalı kaynak: https://cran.r-project.org/web/packages/blockCV/index.html

- PL-02 SCADA-01: OpenPLC, FUXA, Modbus TCP. Video: https://www.youtube.com/watch?v=LIO0TZx3gHM ; FUXA/OpenPLC: https://www.youtube.com/watch?v=OQA5eVge0l8

- PL-03 RF-01: Sionna RT giriş eğitimi: https://nvlabs.github.io/sionna/rt/tutorials/Introduction.html

- PL-04 RF-02: OR-Tools https://developers.google.com/optimization ; pymoo https://pymoo.org/

- PL-05 RF-B: Imbalanced-learn kullanım örnekleri https://imbalanced-learn.org/stable/

- PL-06 RF-03: Sionna RT scattering: https://nvlabs.github.io/sionna/rt/tutorials/Scattering.html

Video süreleri ve zaman damgaları bağımsız yeniden doğrulama gerektirir.

## 002 — PDF'ler

- RF-C: Roberts et al. (2017), DOI https://doi.org/10.1111/ecog.02881 ; Valavi et al. (2019), DOI https://doi.org/10.1111/2041-210X.13107

- SCADA-01: NIST SP 800-82 Rev 3 https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-82r3.pdf

- RF-01: ITU-R P.1238 https://www.itu.int/rec/R-REC-P.1238/en

- RF-02: AP placement optimization (kentsel ağ yöntemi, doğrudan indoor eşdeğeri değil): https://www.comm.toronto.edu/~weiyu/yicheng_gc12.pdf

- RF-B: Saito & Rehmsmeier (2015) https://doi.org/10.1371/journal.pone.0118432

- RF-03: ITU-R P.2040 https://www.itu.int/rec/R-REC-P.2040 ; NIST AMS 300-4 https://doi.org/10.6028/NIST.AMS.300-4

PDF bölüm/sayfa düzeyinde iddia eşleştirmesi henüz yapılmadı.

## 003 — Repolar

- RF-C: https://github.com/rvalavi/blockCV ; https://github.com/scikit-learn/scikit-learn ; https://github.com/scikit-learn-contrib/imbalanced-learn ; https://github.com/scikit-learn-contrib/MAPIE

- SCADA-01: https://github.com/thiagoralves/OpenPLC_v3 ; https://github.com/frangoteam/FUXA ; https://github.com/pymodbus-dev/pymodbus ; https://github.com/eclipse-mosquitto/mosquitto ; https://github.com/FreeOpcUa/opcua-asyncio

- RF-01 ve RF-03: https://github.com/NVlabs/sionna

- RF-02: https://github.com/google/or-tools ; https://github.com/anyoptimization/pymoo

- RF-B: https://github.com/scikit-learn-contrib/imbalanced-learn

Repo SHA, lisans, API sürümü ve test çalıştırma durumu doğrulanmadan uygulama bağımlılığı olarak sabitlenmemeli. OpenPLC_v3 ana repo arşiv durumu kontrol edilmeli. 003-Repolar klasöründeki mevcut README korunmuştur.

## 004 — Müşteri Referansları

Klasör başlangıçta boştu. Bu kayıtlar gerçek müşteri referansı değildir; ilan gereksinimleri ve kamu vaka inceleme adaylarıdır.

- RF-C: GIS/POI veri doğrulama, PostGIS, Python spatial join; önerilen kanıt: leakage_audit.json ve validated_locations.geojson.

- SCADA-01: PLC tag eşleme, HMI ekranları, Modbus/OPC UA, reconnect ve alarm testleri; kanıt: tag_map.csv, alarm_test.json.

- RF-01/RF-02: Wi-Fi kapsama haritası, AP yerleşimi, BOM; lisanslı iBwave teslimatıyla eşdeğer değildir.

- Kamu vaka kaynakları: https://inductiveautomation.com/resources/casestudies ; https://www.esri.com/en-us/about/about-esri/customer-stories ; https://www.nist.gov/programs-projects/industrial-wireless-systems

Müşteri izni olmadan referans, isim veya teslimat iddiası oluşturulmamalı.

## 005 — İş İlanı

- Arşiv belgesi: https://docs.google.com/document/d/1-kVPmwgE0W5y0SRzQh0Xd2zCfEQmBs4kUXq-G9An0lg/edit

- RF-C: Python GIS Developer; GIS/POI Validation; PostGIS Data Engineer; UAV Sensor ML.

- SCADA-01: Ignition SCADA Developer — HMI Screens & PLC Tag Integration https://www.upwork.com/freelance-jobs/apply/Ignition-SCADA-Developer-HMI-Screens-PLC-Tag-Integration_~022115156959874981678/ ; PLC/SCADA Robotics Engineers https://www.upwork.com/freelance-jobs/apply/PLC-SCADA-Robotics-Engineers-Join-Our-Growing-Automation-Agency_~022118214301473609809/

- RF-01/RF-02: iBwave Wi-Fi Design Engineer (arşiv ekran görüntüleri; deneyim/lisans şartı). RF-B: UAV Sensor ML tematik eşleşme. RF-03: doğrudan ilan kanıtı eksik.

İlan aktifliği, ücret, şartlar ve başvuru uygunluğu güncel olarak doğrulanmadan kesin başvuru önerisi yapılmamalı.

## Öncelik ve Teslim Kapıları

- P1 RF-C: random/group/spatial CV, leakage audit, worst-zone metrics. P1 SCADA-01: Modbus simülasyon, HMI tag map, reconnect/alarm testleri.

- P2 RF-01: deterministik kapsama haritası; RF-02: baseline ve kısıtlı optimizasyon.

- P3 RF-B: eğitim içi yeniden örnekleme ve minority metrics; RF-03: sabit sahne/sürüm ile RF simülasyonu.

- Her kaynak için URL, tarih, lisans, sürüm/SHA, ürün, Sprint, gereksinim, test, kanıt durumu ve açık risk kaydı tutulmalı. PASS/FAIL/NOT_RUN ayrımı korunmalı.

**Kaynak raporlar:** https://drive.google.com/drive/folders/1R00DUQopUrjoYOmwHDT-swtZXWXkFkOz
