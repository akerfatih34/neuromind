# NeuroMind — GitHub Pages ile Yayınlama ve Telefona Kurulum

Bu klasör yayınlanmaya hazır sürümdür. Google girişi ve PWA kurulumu **https** gerektirir;
GitHub Pages bunu ücretsiz sağlar.

## 1. GitHub Desktop ile yayınlama (~5 dk)

### Repoyu oluştur
1. GitHub Desktop'ı aç (yoksa desktop.github.com'dan indir) → GitHub hesabınla giriş yap
   (File → Options → Accounts → Sign in).
2. **File → New repository**:
   - Name: `neuromind`
   - Local path: istediğin bir klasör (ör. Belgeler)
   - Create repository.
3. **Repository → Show in Finder / Explorer** ile repo klasörünü aç → bu `NeuroMind-PWA`
   klasöründeki TÜM dosyaları oraya kopyala (`index.html` repo kökünde olmalı).
4. GitHub Desktop'a dön: değişiklikler sol tarafta listelenir → alta commit mesajı yaz
   (ör. "ilk sürüm") → **Commit to main**.
5. Üstteki **Publish repository** düğmesine bas → **"Keep this code private" kutusunun
   işaretini KALDIR** (Pages ücretsiz planda public repo ister) → Publish.

### GitHub Pages'i aç
6. GitHub Desktop'ta **Repository → View on GitHub** → sitede **Settings → Pages** →
   Source: **Deploy from a branch** → Branch: **main**, klasör: **/ (root)** → Save.
7. ⚠️ **Custom domain kutusunu BOŞ bırak** — orası kendi alan adı satın alanlar içindir;
   repo adı yazılırsa "not properly formatted" hatası verir.
8. 1-2 dk sonra sayfanın üstünde "Your site is live at ..." görünür:
   `https://KULLANICIADIN.github.io/neuromind/`

### Güncelleme yayınlama
Yeni `index.html`'i repo klasörüne kopyala → GitHub Desktop'ta commit mesajı yaz →
**Commit to main** → üstteki **Push origin**. 1-2 dk içinde site güncellenir.

## 2. Telefona ekleme
- **iPhone (Safari):** Adresi aç → Paylaş → **Ana Ekrana Ekle**.
- **Android (Chrome):** Adresi aç → çıkan **Yükle / Ana ekrana ekle** istemine dokun.

Uygulama tam ekran açılır ve çevrimdışı çalışır.

## 3. Google hesabı ile bulut senkronizasyonu (~5 dk, bir kez)
1. console.firebase.google.com → **Create project** (Analytics kapatılabilir).
2. Build → **Authentication** → Get started → Sign-in method → **Google** → Enable.
3. Authentication → Settings → **Authorized domains** → **Add domain** →
   `KULLANICIADIN.github.io` ekle.
4. Build → **Realtime Database** → Create database → **locked mode** → **Rules** sekmesine:
   ```
   {"rules":{"users":{"$uid":{".read":"auth.uid===$uid",".write":"auth.uid===$uid"}}}}
   ```
   yapıştır → Publish.
5. Project settings (⚙️) → General → Your apps → **Web app (</>)** → kayıt et →
   görünen **firebaseConfig**'i kopyala. İçinde `databaseURL` yoksa Realtime Database
   sayfasındaki `https://...firebasedatabase.app` adresini `databaseURL: "..."` olarak ekle.
6. Uygulamada (GitHub Pages adresinden aç!) sağ üst profil düğmesi → **Bulut Sync** →
   config'i yapıştır → **Google ile Giriş Yap**.
7. Bir cihazda **Buluta Gönder**, diğerinde aynı config ile giriş yapıp **Buluttan Al**.

Bu kurallarla verine yalnızca kendi Google hesabın erişebilir.

## Alternatifler
- **Sync kodu (hesapsız):** Realtime Database'i test mode ile aç; uygulamada
  "Alternatif: sync kodu ile" bölümüne adres + ürettiğin kodu gir (iki cihaza da aynısını).
- **Dosya yedeği (en basit):** Profil ekranı → Yedekleme → dosya indir / yükle.
  İnternet ve hesap gerektirmez; çift tıklanan yerel dosyada da çalışır.
