# BS 0.2 — Rambo

Java menü ve C++ ARM64 bileşeninin kaynak paketi. Oyun profili: 69.230.

## İçerik

- Animasyonlu sekmeli menü ve kaydedilen görünüm ayarları.
- Normal saldırı ve ulti için ayrı menzil seçimi, otomatik saldırı.
- Görüş hattı kontrolü; ESP çizgi, kutu, can ve mesafe seçenekleri.
- Mermi hareketinden kaçış yönü hesaplayan Dodge bileşeni.

## Windows üzerinde derleme

Python 3.10+, JDK 25 ve Android SDK gerekir. SDK bileşenleri:
build-tools 36.0.0, platform android-37.0, NDK 30.0.16248370, CMake 4.1.2.

PowerShell'de kendi kurulum yollarını ayarla:

```powershell
$env:JAVA_HOME = 'C:\Program Files\Java\jdk-25'
$env:ANDROID_SDK_ROOT = "$env:LOCALAPPDATA\Android\Sdk"
python build.py
```

Kendi 69.230 ARM64 temel APK dosyanı `input/base.apk` olarak koy.
Alternatif yol için `BSTOOLS_INPUT_APK` ortam değişkenini kullan.
`libg.so` doğrudan APK içinden okunur; SHA-256 eşleşmezse derleme durur.
Oyun APK'sı, oyun kütüphaneleri, görseller ve imzalama anahtarı bu depoda yoktur.

Çıktı: `base-autofire-69.230.apk`. İlk derlemede yerel geliştirme anahtarı
üretilir. Anahtarı paylaşma; aynı anahtarı saklamak sonraki APK güncellemeleri için gereklidir.
Derleme kurulum yapmaz. Farklı imzayla yüklenmiş uygulamayı doğrudan güncelleyemez.

## Yerel C++ testleri

Visual Studio x64 Native Tools terminalinde:

```bat
mkdir build
cl /nologo /std:c++17 /EHsc native\test_dodge_planner.cpp /Febuild\test_dodge_planner.exe /Fobuild\test_dodge_planner.obj
build\test_dodge_planner.exe
cl /nologo /std:c++17 /EHsc native\test_skill_metadata.cpp /Febuild\test_skill_metadata.exe /Fobuild\test_skill_metadata.obj
build\test_skill_metadata.exe
```

Mevcut kaynak üzerinde 15 Dodge ve 16 veri/menzil testi geçmiştir.
Bu taşınabilir kaynak paketiyle tam APK derlemesi yeniden çalıştırılmamıştır.
Son 0.2 değişiklikleri VM kapalı olduğundan canlı oyunda doğrulanmamıştır.

## Bilinen sınırlar

Her savaşta ilk normal atış bağlamı yakalar. Dodge yalnızca desteklenen
hareket modunda çalışır; her saldırıdan kaçış garantisi yoktur.
Gizlenen hedef aktif nesne listesinden çıkarsa ESP kaybolabilir.
Tam özellik eşitliği veya tüm karakterler için doğrulanmış destek iddiası yoktur.

## Üçüncü taraf

Dobby kaynakları yerel düzeltmeleriyle birlikte dahil edilmiştir.
Lisansı ve değişiklikleri için `THIRD-PARTY-NOTICE.md` dosyasına bak.
Bu proje Supercell ile bağlantılı değildir. Projenin kendi kodu için bu
pakette ayrıca bir açık kaynak lisansı seçilmemiştir.
