# 31 Haiku 5.5 vs Opus 5.5: istemler ve çekim akışı

İki modele birebir aynı istem, aynı anda. Effort ikisinde de varsayılan (medium). Her model kendi klasöründe çalışır.

## Kurulum (iki terminal yan yana, ekran kaydı açık)

Sol:  cd ~/Vibe-Code/haiku-opus/haiku && claude --model claude-haiku-5-5
Sağ:  cd ~/Vibe-Code/haiku-opus/opus  && claude --model claude-opus-5-5

Görev 1'i ikisine aynı anda yapıştır. İkisi de bitince her birinde `/cost` yaz ve ekranda tut.
Sonra `open istanbul.html` ile iki sonucu yan yana aç. Ardından görev 2 aynı şekilde (`/clear` ile temiz başla).

## Görev 1: İstanbul gün batımı

Tek bir `istanbul.html` dosyası yaz (harici kütüphane ya da görsel dosya yok, her şey kodla çizilecek). Gün batımında İstanbul Boğazı'nı gösteren, tam ekran, animasyonlu bir sahne: Asya ve Avrupa yakasının siluetleri, camiler ve minareler, Galata Kulesi, Boğaz Köprüsü, suyun üstünde ışığı yansıtan dalgalar, Boğaz'dan geçen bir vapur, uçuşan martılar. Gökyüzü birkaç dakika içinde gün batımından geceye yavaşça geçsin; güneş batarken renkler değişsin, köprünün ve evlerin ışıkları tek tek yansın, yıldızlar çıksın. Gerçekçi ve şiirsel görünsün; çocuksu ya da çizgi film gibi olmasın.

## Görev 2: Kaos, çift sarkaç

Tek bir `kaos.html` dosyası yaz (harici kütüphane yok). Ekranda aynı noktadan bırakılan 50 çift sarkaç olsun; başlangıç açıları birbirinden yalnızca milyonda bir radyan farklı. İlk saniyelerde hepsi tek bir sarkaç gibi birlikte hareket etsin, sonra kaos yüzünden birbirinden ayrılıp bir renk yelpazesi gibi açılsın. Fizik doğru olsun (çift sarkacın gerçek hareket denklemleri, kararlı bir sayısal yöntem, enerji zamanla patlamasın). Uçlarda solan iz çizgileri, koyu zemin, şık görünüm. Ekranda geçen süre ve toplam enerji görünsün; tıklayınca yeni bir başlangıç açısıyla yeniden başlasın.

## Ölçüm tablosu (çekimden sonra doldur)

| | Haiku 5.5 | Opus 5.5 |
| --- | --- | --- |
| G1 süre | 5 dk 51 sn | 22 dk 1 sn |
| G1 token (girdi/çıktı) | 1,6k + önbellek / 82,3k | 114 + önbellek / 129,8k |
| G1 maliyet ($) | 0,136 | 4,15 (~30 kat) |
| G1 sonuç (çalıştı mı, nasıl görünüyor) | 527 satır; yalnız sözdizimini denetledi, tarayıcıda açmadı | 1.174 satır; tarayıcıda 60 fps hatasız denedi; ek: ay, Venüs, kayan yıldız, Kız Kulesi |
| G2 süre | 1 dk 19 sn | 2 dk 8 sn |
| G2 token (girdi/çıktı) | ~186 bin toplam / 17,9k çıktı | ~165 bin toplam / 13,1k çıktı |
| G2 maliyet ($) | 0,017 | 0,51 (~30 kat) |
| G2 sonuç (fizik doğru mu, enerji sabit mi) | Denklemler doğru, RK4 1 ms; 60 sn'de enerji sapması ~2e-10 J; rastgele başlangıç bazen az kaotik (60 sn ayrışmadı), çoğunda 10-20 sn'de açılıyor | Denklemler doğru, RK4 0,5 ms; 40 sn'de sapma ~7e-9 J; başlangıç hep yüksek enerjili, 6/6 denemede ≤10-20 sn'de açılıyor; ekranda senkron → ayrışıyor → kaos etiketi |

Fiyat: Opus 5.5 girdi $4, çıktı $20 / 1M token; Haiku 5.5 girdi $0,10, çıktı $0,50 / 1M token (40 kat ucuz).

**G1 hükmü (Hakan, 9 Ekim ~20.00):** "İkisi de çok güzel ama Haiku çok daha worth." Kayıt kopyaları `kayit/` altında (`?sure=20`).

**Glamdring ölçümü (G2):** iki dosyanın fiziği tarayıcısız node ile koşturuldu (Haiku 6 başlangıç × 40 sn, 1 × 60 sn; Opus 6 × 40 sn).
