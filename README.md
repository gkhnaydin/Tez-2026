# 30 ve 40 istemcili benzetim kayıtları

Bu depo, 6TiSCH üzerinde yayılım tabanlı dağıtık depolama ve mobil toplayıcı
çalışmasının 30 ve 40 istemcili Cooja benzetimlerine ait kayıtları içerir.

## Deney düzeni

| | 30 istemci | 40 istemci |
|---|---|---|
| Ağ | 1 sabit kök + 30 istemci; önerilen yapılandırmada ayrıca mobil toplayıcı (kimlik 32) | 1 sabit kök + 40 istemci; önerilen yapılandırmada ayrıca mobil toplayıcı (kimlik 42) |
| Izgara yerleşimi | 6 × 5, 171 m × 180 m | 8 × 5, 240 m × 180 m |
| Rastgele yerleşim | 225 m × 225 m | yaklaşık 260 m × 260 m |

Ortak ayarlar:

| | |
|---|---|
| Benzetim aracı | Cooja (MSPSim), arayüzsüz kip |
| Platform | exp5438 (MSP430F5438A + CC2420) |
| Radyo modeli | UDGM, 50 m iletim, 100 m girişim |
| Süre | 60 dakika (ilk 20 dakika ağ kurulum evresi) |
| Tekrar | Her birleşim için 5 koşu, tohumlar 11111, 22222, 33333, 44444, 55555 |
| Yayın periyodu / önbellek | 60 s / 50 kayıt |
| Rastgele konumlar | Her ağ boyutunda tüm koşularda aynı |

Her ağ boyutunda 20 koşu: 2 yapılandırma × 2 yerleşim × 5 tohum.

40 istemcili rastgele yerleşimde 36 numaralı düğüm en yakın komşusuna 51,2 m
uzaktadır; 50 m iletim menzilinde hiçbir düğüme bağlanamadığı için ağa katılmaz
ve paket üretmez.

## Klasör yapısı

```
30dugum/ ve 40dugum/
  referans/            yayılım katmanı kapalı
    izgara/
    rastgele/
  onerilen/            yayılım katmanı ve mobil toplayıcı
    izgara/
    rastgele/
  senaryolar/          dört Cooja senaryosu (.csc) ve mobil toplayıcının iki güzergâh dosyası (.dat)
```

Her yerleşim klasöründe beş koşu klasörü (`run_<tohum>`) ve beş koşunun
ortalama ile örneklem standart sapmasını veren `summary_mean.txt` bulunur.

## Koşu klasöründeki dosyalar

| Dosya | İçerik |
|---|---|
| `scenario.csc` | Koşuda kullanılan Cooja senaryosu (tohum dâhil) |
| `raw.log.gz` | Düğümlerin yazdırdığı tüm günlük satırları (gzip) |
| `summary.txt` | Koşunun özet ölçütleri |
| `packets_tx.csv`, `packets_rx.csv` | Üretilen ve kökte alınan uygulama paketleri |
| `energy.csv` | Energest sayaçları |
| `rpl_events.csv`, `parent_change.csv` | RPL kontrol mesajları ve ana düğüm değişiklikleri |
| `sixp_events.csv`, `tsch_join.csv`, `mac_tx.csv` | 6P işlemleri, TSCH'ye katılma zamanları, MAC iletimleri |
| `gossip_events.csv` | Yayılım çerçevelerinin iletim ve alımları (yalnızca önerilen) |
| `cache_snapshots.csv` | Düğümlerin önbellek dökümleri (yalnızca önerilen) |
| `mdc_events.csv` | Mobil toplayıcı olayları (yalnızca önerilen) |

Zaman sütunları (`sim_time_us`) benzetim saatine göre mikrosaniyedir.
