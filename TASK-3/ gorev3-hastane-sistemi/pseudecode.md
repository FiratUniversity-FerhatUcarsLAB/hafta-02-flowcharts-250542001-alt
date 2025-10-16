Başla
    TC_No ← kullanıcıdan_al("TC Kimlik Numaranızı girin:")
    eğer TC_No geçerliyse:
        poliklinik_listesi_göster()
        poliklinik ← kullanıcıdan_al("Poliklinik seçin:")
        
        doktor_listesi ← doktorlari_getir(poliklinik)
        doktor_listesi_göster(doktor_listesi)
        doktor ← kullanıcıdan_al("Doktor seçin:")
        
        uygun_saatler ← saatleri_getir(doktor)
        uygun_saatler_göster(uygun_saatler)
        saat ← kullanıcıdan_al("Saat seçin:")
        
        randevu_onay ← kullanıcıdan_al("Randevuyu onaylıyor musunuz? (E/H):")
        eğer randevu_onay == 'E' ise:
            randevu_kaydet(TC_No, doktor, saat)
            SMS_gonder(TC_No, doktor, saat)
            yazdır("Randevunuz oluşturuldu ve SMS gönderildi.")
        değilse:
            yazdır("Randevu iptal edildi.")
    değilse:
        yazdır("Geçersiz TC Kimlik Numarası.")
Bitir
Başla
    TC_No ← kullanıcıdan_al("TC Kimlik Numaranızı girin:")
    eğer TC_No geçerliyse:
        tahlil_var_mi ← tahlil_kontrol(TC_No)
        eğer tahlil_var_mi:
            sonuc_hazir_mi ← sonuc_durumu(TC_No)
            eğer sonuc_hazir_mi:
                sonucu_goster(TC_No)
                indir ← kullanıcıdan_al("PDF indirmek ister misiniz? (E/H):")
                eğer indir == 'E':
                    PDF_indir(TC_No)
                değilse:
                    yazdır("İndirme işlemi atlandı.")
            değilse:
                yazdır("Tahlil sonucu henüz hazır değil. Lütfen sonra tekrar deneyin.")
        değilse:
            yazdır("Sistemde kayıtlı tahlil bulunmamaktadır.")
    değilse:
        yazdır("Geçersiz TC Kimlik Numarası.")
Bitir
Başla
    tekrar ← 'E'
    tekrar == 'E' iken:
        işlem ← kullanıcıdan_al("İşlem seçin: 1-Randevu Al, 2-Tahlil Sonucu Gör:")
        
        eğer işlem == 1:
            Randevu Alma modülünü çalıştır
        eğer işlem == 2:
            Tahlil Sonuçları modülünü çalıştır
        
        tekrar ← kullanıcıdan_al("Başka işlem yapmak ister misiniz? (E/H):")
    yazdır("Sistemden çıkılıyor...")
Bitir
