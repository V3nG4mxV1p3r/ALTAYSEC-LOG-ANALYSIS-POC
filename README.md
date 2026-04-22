# 🛡️ AltaySec Blue Team Lab - Proof of Concept (PoC)

Bu repository, siber güvenlik eğitim platformları için tasarlanmış, **sıfır kurulum gerektiren (zero-setup)** ve tarayıcı üzerinden çalışan bir Blue Team / Adli Bilişim laboratuvar konseptidir.

## 🎯 Konsept: "Log Detective"
Kullanıcılar, zafiyetli bir makineyi ayağa kaldırmak yerine, daha önceden saldırıya uğramış bir makinenin loglarını analiz ederek siber tehdit avcılığı (Threat Hunting) yaparlar. 

Bu PoC, **Gotty** aracı kullanılarak Docker konteyneri içindeki bash terminalini doğrudan `80` portu üzerinden web tarayıcısına yansıtır. Kullanıcı SSH bağlantısı veya herhangi bir araç kurulumu yapmadan `grep`, `awk`, `cat` gibi araçlarla anında analize başlayabilir.

## 🚀 Lab Nasıl Çalıştırılır?

Herhangi bir Docker yüklü sistemde aşağıdaki komutları çalıştırmak yeterlidir:

1. İmajı indirin/inşa edin:
docker build -t altaysec/blue-level-1 .

2. Konteyneri başlatın:
docker run -d -p 8081:80 altaysec/blue-level-1

3. Tarayıcınızdan terminale erişin:
http://localhost:8081

## 📋 Senaryo: Gece Vardiyası (LFI Sızıntısı)
Şirketin ana web sunucusuna gece saatlerinde bir saldırı gerçekleşti. Saldırganın Local File Inclusion (LFI) zafiyetini kullanarak kritik bir sistem dosyasını okuduğundan şüpheleniyoruz.

**Görev:** `access.log` dosyasını analiz et ve bayrağı bul.
* Saldırganın IP Adresi?
* Kullanılan zafiyet parametresi?
* Okunan kritik dosya?

**Flag Formatı:** `ALTAYSEC{IP_PARAMETRE_DOSYA}`

---

# 🛡️ Level 2: BASE64 (Intermediate)

**Senaryo:** Bir saldırgan `/admin` paneline girmeye çalışıyor. IP engeline takılmamak için sürekli proxy değiştiriyor ancak arkasında kritik bir iz bırakıyor. Sisteme sızdıktan sonra çalıştırdığı zararlı komutu ise Base64 ile şifrelemiş.

**Görevler:**
1. Saldırganın sabit kalan User-Agent'ını bul.
2. Başarılı giriş yapılan (302 Redirect) IP'yi tespit et.
3. cmd parametresindeki Base64 komutu decode et.

**Öğrenim Çıktıları:**
* Karmaşık log dosyalarında `awk` ve `grep` kombinasyonları ile anomali tespiti.
* User-Agent analizi ve Brute-Force tespiti.
* Terminal üzerinden Base64 şifre çözümü (Deobfuscation).

*Developed by Emir - AltaySec Lab Researcher*
