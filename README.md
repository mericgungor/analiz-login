# Login Analizi
Bir çok yazılımda, sadece yetkili kişilerin erişebildiği bir portal ihtiyacı olmuştur.\
Bu portala Admin Modülü de denilmektedir.\
Bu yazıda, yazılım dilinden ve teknolojiden (C#, Java, Php, Api, MVC …) bağımsız, bir admin modülünün giriş (login) analizi yapılmaktadır.


# Düşük Seviye Güvenlikli Giriş
Kullanıcı adı ve şifre alanları içermelidir.\
Kullanıcı adı: email, tc, ad.soyad, telefon gibi çeşitli biçimlerde olabilmelidir.\
Şifre: Belli uzunlukta, karmaşık karakterler içerebilen biçimlerde olabilmelidir.\
Şifreler veritabanında açık ve okunur şekilde saklanmamalıdır. Geri çözülemez şekilde şifrelenmiş olmalıdır.

## API
Kullanıcı doğrulandıktan sonra access token üretilmeli ve bütün portal işlemlerinde bu access token istenmelidir.

## UI
Mobil, tablet, bilgisayar ekranlarına uyumlu olmalıdır.\
Dikey ve yatay ekranlara uyumlu olmalıdır.\
Modern Js frameworks (Jquery) ve css frameworks (Bootstrap) kullanılmalıdır.\
Açılışta kullanıcı adına fokuslanmalıdır.\
Bazı kullanıcılar, kullanıcı adını yazdıktan sonra Enter tuşuna basabiliyorlar. Bu durumda şifre alanına geçilmesi sağlanmalıdır.\
Otomatik tamamlama (autocomplete) kapatılmalıdır.\
Kullanıcı adı ve şifre gönderilmeden önce kullanıcı tarafında ön kontroller yapılmalıdır. (required, min, max)\
Giriş (submit) butonlarına ard arda basılması engellenmelidir.

## Şifremi Unuttum
Sistemde email adresi veya telefonu kayıtlı olanlar kendi şifrelerini yeniden üretebilmelidirler. Email adresine (veya telefonuna SMS) 1 kullanımlık şifre sıfırlama linki gönderilir, linke tıklayan kullanıcı yeni şifresini oluşturabilir.

## Beni Hatırla
Kullanıcı, portalı kapatıp tekrar açtığında login olmadan direk portala girmek isteyebilir.






# Orta Seviye Güvenlikli Giriş
Bir önceki seviyedeki giriş maddelerini içermelidir.\
Şifre uzunluk ve karmaşıklık kontrolü yapılmalıdır.\
3 yanlış şifre girişinde kullanıcı adı ve ip adresi 1 dakika süreyle bloklanmalıdır. Sadece ip adresini bloklarsanız, hackerlar o binayı bloklayabilir. Sadece kullanıcı adını bloklarsanız, hackerler o kullanıcıyı bloklayabilir.\
Sisteme en son giriş zamanı, en son giriş ip adresi, en son şifre değiştirme tarihi, yanlış şifre giriş sayısı kaydedilmelidir.

## Web teknolojileri için;
Captcha (Resim Doğrulaması) ile bot kontrolü yapılmalıdır.\
https://www.google.com/recaptcha/about/ en çok kullanılan captchadır.\
Session bilgisi HttpOnly cookie ile tutulmalıdır.\
Kullanıcı IP adresi, HTTP_USER_AGENT bilgisi loglanmalıdır.\
Access token kullanım süreleri olmalıdır.

## Open ID (Google ile Login,Outlook ile Login,Facebook ile Login)
Kurumun ihtiyacına göre OpenId destekli kimlik doğrulaması yapılabilir. Bu durumda servis sağlayıcı tarafından sadece kullanıcı adı ve adı soyadı gibi bilgiler temin edilebilir. Ekstra bilgiler (telefon, adres …), ayrıca kullanıcıdan istenebilir.






# Yüksek Seviye Güvenlikli Giriş
Bir önceki seviyedeki giriş maddelerini içermelidir.\
Kullanıcı Id alanları benzersiz GUID (uniqueidentifier) biçiminde saklanmalıdır. Otomatik artan (Auto Increment) integer, tc kimlik no, id olarak kullanılmamalıdır.\
2 aşamalı güvenlik doğrulaması olmalıdır.\
SMS doğrulaması, Google Authenticator, Microsoft Authenticator kullanılabilir.\
Beni hatırla fonksiyonu kaldırılmalıdır.\
Şifrenin belli aralıklarla değiştirilmesi istenebilir.\
Birden fazla IP adresi üzerinden giriş kısıtlanabilmelidir.\
Portal içindeki hassas ayarları değiştirmek için ayrı bir şifre kullanılabilir.\
İlk tanımlanan ve portal üzerinden sıfırlanan şifreler bir defa kullanılmalı ve mutlaka kullanıcı tarafından değiştirilmelidir.

## Single Sign On (SSO) ve Single Log Out (SLO)
Eğer kurum içinde birden fazla portal varsa, SSO ve SLO birlikte düşünülmelidir. Her portala ayrı şifre verilmemelidir.\
Eğer kurum içinde birden fazla kimlik doğrulama sistemi varsa SSO gateway ve yetkilendirme tasarlanmalıdır. Örneğin Personel Yönetim portalına Active Directory kimlik doğrulaması ile girilebiliyorken, Müşteri İlişkileri portalına veritabanı form kimlik doğrulaması ile girilebilir. Bu durumda tek bir master şifre tanımlanabilir, diğer portallara geçiş yetkilendirmesi yapılabilir.
