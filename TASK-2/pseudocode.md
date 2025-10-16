BEGIN

// 1. Kullanıcı Girişi
DISPLAY "Giriş yapınız"
IF user.login() == TRUE THEN
    DISPLAY "Hoş geldiniz, [kullanıcı adı]"
ELSE
    DISPLAY "Giriş başarısız, tekrar deneyiniz"
    RETURN TO login
END IF

// 2. Ürün Kategorilerinde Gezinme
DO
    DISPLAY categoryList
    category = user.selectCategory()
    productList = getProducts(category)
    DISPLAY productList

    product = user.selectProduct()
    IF product != NULL THEN

        // 3. Stok Kontrolü
        IF product.stock > 0 THEN
            quantity = user.selectQuantity()
            IF quantity <= product.stock THEN
                cart.add(product, quantity)
                DISPLAY "Ürün sepete eklendi"
            ELSE
                DISPLAY "Yeterli stok yok"
            END IF
        ELSE
            DISPLAY "Ürün stokta yok"
        END IF

    END IF

    choice = user.select("Alışverişe devam etmek istiyor musunuz? (Evet/Hayır)")
WHILE choice == "Evet"

// 4. Sepet Görüntüleme ve Düzenleme
DO
    DISPLAY cart.view()
    editChoice = user.select("Sepeti düzenlemek istiyor musunuz? (Evet/Hayır)")
    IF editChoice == "Evet" THEN
        action = user.select("Sil / Miktar Güncelle")
        product = user.selectProductFromCart()
        IF action == "Sil" THEN
            cart.remove(product)
        ELSE IF action == "Miktar Güncelle" THEN
            newQuantity = user.inputQuantity()
            cart.update(product, newQuantity)
        END IF
    END IF
UNTIL editChoice == "Hayır"

// 5. İndirim Kodu Uygulama
discountCode = user.enterDiscountCode()
IF discountCode != "" THEN
    IF isValid(discountCode) THEN
        cart.applyDiscount(discountCode)
        DISPLAY "İndirim kodu uygulandı"
    ELSE
        DISPLAY "Geçersiz indirim kodu"
    END IF
END IF

// 6. Minimum Tutar Kontrolü
IF cart.total < 50 THEN
    DISPLAY "Sepet tutarı minimum 50 TL olmalı"
    RETURN TO cart.view()
END IF

// 7. Kargo Ücreti Hesaplama
IF cart.total >= 200 THEN
    shippingCost = 0
    DISPLAY "Kargo ücretsiz"
ELSE
    shippingCost = 29.90
    DISPLAY "Kargo ücreti: 29.90 TL"
END IF
cart.total = cart.total + shippingCost

// 8. Ödeme Yöntemi Seçimi
paymentMethod = user.selectPaymentMethod()
IF paymentMethod == NULL THEN
    DISPLAY "Lütfen ödeme yöntemi seçiniz"
    RETURN TO payment selection
END IF

// 9. Sipariş Onayı
DISPLAY cart.summary()
confirm = user.select("Siparişi onaylıyor musunuz? (Evet/Hayır)")
IF confirm == "Evet" THEN
    placeOrder(cart, paymentMethod)
    DISPLAY "Siparişiniz alınmıştır. Teşekkür ederiz!"
ELSE
    DISPLAY "Sipariş iptal edildi"
END IF

END
