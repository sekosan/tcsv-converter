Elbette — yukarıdaki tüm gereksinimleri derleyip tam, profesyonel bir README.md oluşturdum.
Bu dosya bir GitHub projesi için hazırdır.

⸻

README.md

TCSV Converter & Preview

JSON / TONL / toon → TCSV dönüştürücü ve TCSV tablo önizleme aracı
TCSV Specification v1.2 · Client-side · Zero-dependencies

⸻

📌 Özet

TCSV Converter, JSON / TONL / toon benzeri veri formatlarını kolayca TCSV (Typed CSV) formatına dönüştüren, tamamen tarayıcıda çalışan bir web uygulamasıdır. Ayrıca:
	•	TCSV çıktısını düz metin olarak üretir
	•	TCSV’yi satır/sütun şeklinde tablo olarak önizler
	•	Fonksiyon seviyesinde çalışan yerleşik bir hata raporlama (debug logger) içerir
	•	Hiçbir backend veya framework gerektirmez

UI, dark-theme ve iki panel yapısından oluşur:
Sol: Input + Debug
Sağ: TCSV Output + Preview

⸻

🚀 Özellikler

Özellik	Açıklama
JSON → TCSV dönüşümü	Tip çıkarımı yaparak otomatik TCSV üretir
TONL / toon normalize	Tırnaksız key’leri ve tek tırnaklı değerleri otomatik JSON formatına dönüştürür
TCSV önizleme	Satırları tablo olarak render eder
Escape-aware parser	TCSV içinde |, \,, \\, \', \n gibi kaçışları doğru işler
Hata raporlama paneli	Fonksiyon adı, zaman, hata mesajı, stack satırı
Auto detect format	Input’a göre format tahmini
Zero dependencies	Sadece HTML + CSS + JS


⸻

📁 Proje Yapısı

/ (root)
├─ index.html        # Uygulamanın tamamı (UI + parser + converter + debug logger)
├─ README.md         # Bu dosya
└─ (opsiyonel) assets/


⸻

🖥️ Kullanım

1. Input alanına veri yapıştır

Desteklenen formatlar:
	•	JSON
	•	TONL / toon (basit anahtar: değer söz dizimi)
	•	TCSV

2. Format seçiciyi ayarla
	•	auto: otomatik tanıma
	•	json: zorla JSON davranışı
	•	tonl: TONL / toon normalize
	•	tcsv: TCSV parse + preview

3. Convert butonuna bas
	•	Sağ panelde TCSV text oluşur
	•	Alt panelde tablo önizleme çıkar
	•	Hata olursa sol panelde Debug Log’a düşer

⸻

🧠 TCSV Format Özeti (v1.2)

✔ Header yapısı

TableName | field1:type1 | field2:type2 | ...

✔ Veri satırları

TableName | value1 | value2 | value3

✔ Tip kuralları
	•	Basit tipler:
	•	str, u32, i32, f64, bool
	•	Liste: list[str], list[u32]
	•	Objeler:

obj{email:str,phone:str}



✔ String literal

TCSV’de stringler tek tırnak '...' ile yazılır.

✔ Escape karakterleri

Kaçış	Anlam
\\	Backslash
\'	Tek tırnak
|	Pipe
\,	Virgül
\=	Eşittir
\n	Newline


⸻

🪲 Hata Raporlayıcı

Her fonksiyon bir wrapper ile izlenir:

const safeJsonToTcsv   = reporter.wrap('jsonToTcsv', jsonToTcsv);
const safeTonlToJson   = reporter.wrap('tonlLikeToJson', tonlLikeToJson);
const safeParsePreview = reporter.wrap('parseTcsvForPreview', parseTcsvForPreview);

Hata durumunda:
	•	Debug Log paneline şu örnek formatla düşer:

[13:02:41.155] [jsonToTcsv] JSON parse error
    at jsonToTcsv (...)

	•	Dönüşüm durur
	•	UI kırmızı uyarıyla kullanıcıyı bilgilendirir

⸻

🔍 Format Tespiti

Input metni üzerinde heuristik:
	•	{ veya [ ile başlıyorsa → JSON
	•	İlk satırda | varsa → TCSV
	•	Satır başı key: ise → TONL/toon
	•	Bulunamazsa → varsayılan JSON

⸻

🗂️ Örnek JSON → Örnek TCSV

Input (JSON)

[
  {
    "id": 1,
    "name": "Sekoya",
    "active": true,
    "contact": {
      "email": "sekoya@example.com",
      "phone": "+90 555 000 00 00"
    }
  }
]

Output (TCSV)

Data | id:u32 | name:str | active:bool | contact:obj{email:str,phone:str}
Data | 1 | 'Sekoya' | true | email='sekoya@example.com',phone='+90 555 000 00 00'


⸻

🧪 Gömülü Test Case (Uygulama açılışında)

Açılışta input alanına otomatik olarak iki satırlı örnek JSON yüklenir.
Bu, JSON → TCSV dönüşümünün çalıştığını ve hata üretmediğini doğrular.

⸻

📦 Derleme / Kurulum

Bu proje tamamen statik çalışır.

✔ index.html dosyasını açman yeterli.
✔ Sunucu gerekmez.
✔ Her tarayıcıda çalışır.

GitHub Pages’a deploy etmek için:

repo settings → pages → source: main / root


⸻

🤝 Katkı Rehberi

Pull request açmadan önce:
	•	Lütfen tüm format kurallarını (TCSV v1.2) koruyun
	•	Kodda debug logger’ın bozulmadığını doğrulayın
	•	Preview tablosunun escape-aware çalıştığını test edin

⸻

📄 Lisans

MIT License
© 2025 — TCSV Converter

⸻

Hazır!
Eğer istersen:
	•	README’ye görseller ekleyebilirim
	•	TCSV spesifikasyonunu ayrı bir SPEC.md dosyasına çıkarabilirim
	•	Ya da GitHub Issues / Milestones şeklinde görev listesi oluşturabilirim

Ne yapmak istersin?
