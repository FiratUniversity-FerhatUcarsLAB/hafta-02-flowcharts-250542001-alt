// Akıllı Ev Güvenlik Sistemi - Pseudocode

SistemAktif = TRUE
EvSahibiEvde = FALSE

FONKSİYON TehditSeviyesiniBelirle(hareket, kapiPencere, kamera):
    SEVİYE = 0
    EĞER hareket VEYA kapiPencere:
        SEVİYE = 1
        EĞER kamera:
            SEVİYE = 2
        EĞER NOT EvSahibiEvde:
            SEVİYE = 3
    DÖN SEVİYE

FONKSİYON BildirimGonder(seviye):
    GÖNDER "SMS" -> "Tehdit Seviyesi: " + seviye
    GÖNDER "App" -> "Tehdit Seviyesi: " + seviye
    GÖNDER "Email" -> "Tehdit Seviyesi: " + seviye

// Sürekli çalışan ana döngü
WHILE SistemAktif:  // Sürekli

    // Sensör verilerini oku
    hareket = HareketSensoruOku()
    kapiPencere = KapiPencereSensoruOku()
    kamera = KameraKontrolEt()

    // Tehdit seviyesi belirle
    seviye = TehditSeviyesiniBelirle(hareket, kapiPencere, kamera)

    // Alarm ve Bildirim
    EĞER seviye > 0:
        AlarmCal()
        BildirimGonder(seviye)

        // Alarm durdurulmazsa devam et
        ALARM_DURDURULDU = False
        WHILE NOT ALARM_DURDURULDU:
            ALARM_DURDURULDU = AlarmSifirlamaKontrol()
            BEKLE(5 saniye)

    // Bekle ve yeniden kontrol et
    BEKLE(1 saniye)
