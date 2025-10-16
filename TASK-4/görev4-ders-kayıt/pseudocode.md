Başla
    ÖğrenciNo, Şifre ile giriş yap
    Eğer giriş başarılıysa:
        DersListesiniGöster()
        SeçilenDersler = []
        ToplamKredi = 0

        Tekrar:
            Ders = DersSeç()
            Eğer Ders == 'Çık':
                DÖNGÜDEN ÇIK
            Eğer Ders zaten SeçilenDersler içinde:
                Uyarı("Ders zaten seçildi")
                Devam et

            Eğer Ders.kontenjan == 0:
                Uyarı("Kontenjan dolu")
                Devam et

            Eğer !ÖnKoşullarTamamlandı(Ders):
                Uyarı("Ön koşullar sağlanmamış")
                Devam et

            Eğer ZamanÇakışıyor(Ders, SeçilenDersler):
                Uyarı("Zaman çakışması var")
                Devam et

            Eğer ToplamKredi + Ders.kredi > 35:
                Uyarı("Kredi limiti aşıldı")
                Devam et

            SeçilenDersler.append(Ders)
            ToplamKredi += Ders.kredi

        GPA = ÖğrenciNotOrt()
        Eğer GPA < 2.5:
            DanışmanOnayı = OnayAl("Danışman onayı gerekli")
            Eğer DanışmanOnayı == False:
                Uyarı("Danışman onayı alınamadı")
                Bitir

        KayıtÖzetiGörüntüle(SeçilenDersler)
        Onay = KullanıcıdanOnayAl()
        Eğer Onay:
            Kaydet(SeçilenDersler)
            Mesaj("Kayıt tamamlandı")
        Aksi halde:
            Mesaj("Kayıt iptal edildi")

    Aksi halde:
        Uyarı("Giriş başarısız")
Bitir
