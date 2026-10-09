# Haiku 5.5 vs Opus 5.5

Aynı iki işi iki modele, birebir aynı istemle, aynı anda verdim. Claude Code'da iki terminal yan yana; effort ikisinde de varsayılan (medium). Ölçümler `/cost` çıktısından.

| | Haiku 5.5 | Opus 5.5 |
| --- | --- | --- |
| **İstanbul gün batımı:** süre | 5 dk 51 sn | 22 dk 1 sn |
| maliyet | $0,14 | $4,15 |
| toplam token | ~337 bin | ~1,6 milyon |
| **Kaos, 50 çift sarkaç:** süre | 1 dk 19 sn | 2 dk 8 sn |
| maliyet | $0,017 | $0,51 |
| toplam token | ~186 bin | ~165 bin |

Maliyet farkı iki görevde de yaklaşık 30 kat (liste fiyatı farkı 40 kat; önbellek farkı kapatıyor).

- **İstanbul:** ikisi de istenen her şeyi kurdu (iki yaka, Galata, köprü, vapur, martılar, geceye geçiş, ışıklar, yıldızlar). Opus daha gerçekçi ve ayrıntılı; sahneyi tarayıcıda açıp kendini test etti. Haiku daha stilize, açmadan bıraktı.
- **Sarkaç:** ikisinin fiziği de doğru (RK4; enerji sapması milyarda bir joule düzeyinde). Opus başlangıcı her zaman kaotik bölgeden seçiyor; Haiku'nunki bazen az kaotik, tıklayıp yenilemek gerekebilir.

Benim sonucum: iş yatıracağım zaman Opus orkestratör olur, ama Haiku ile subagent kurup çalışılabilir.

## Dosyalar

- `haiku/` ve `opus/`: modellerin yazdığı dosyalar, dokunulmadı. Tarayıcıda doğrudan açılır.
- `kayit/`: video kaydı için kopyalar. Opus kopyasına yalnız `?sure=` hız parametresi eklendi (Haiku'da zaten vardı), görüntüye dokunulmadı. Örnek: `kayit/opus-istanbul.html?sure=20`
- `ISTEMLER.md`: iki istem, çekim akışı ve ölçüm tablosu.
