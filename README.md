<h1 align="center">Burç API</h1>

<div align=center>
  <img src="./Readme%20Resources/Burç API Logo.png" alt="Logo" width="120" heigh="120"/>
</div>

## **İçindekiler**

- [API Hakkında](#api-hakkında)
- [Dokümantasyon](#dokümantasyon)
- [İstek Örnekleri](#i̇stek-örnekleri)
- [Lisans](#lisans)
- [İletişim](#i̇letişim)

![-----------------------------------------------------](./Readme%20Resources/Çizgi.png)


## API Hakkında

Bu repo, Php diliyle geliştirmiş olduğum burç yorumlarını ve bilgilerini sunan
API'nin dokümantasyonunu içerir.

HTTP GET istekleriyle `burc`, `tip` ve `api_key` parametrelerini alır ve bütün burçların
günlük, haftalık, aylık, yıllık yorumlarını JSON formatında sağlar.

JSON dosyasında her burç için burcu temsil eden 256 x 256 çözünürlüğünde png uzantılı resim barındıran url adresi de bulunmaktadır.

Ayrıca tip parametresine "genel"değeri yazılarak burçların detaylı karakter özellikleri öğrenilebilir.

![-----------------------------------------------------](./Readme%20Resources/Çizgi.png)


## Dokümantasyon

Base URL: `https://toktasoft.com/api/burclar.php`

API sadece 3 parametre almaktadır.

| Parametre | Zorunlu Mu? | Değerler | Varsayılan Değer | Açıklama |
|      -------     |      -------     |      -------     |      -------     |      -------     |
| <p align="center">`burc`</p> | <p align="center">evet</p> | `oglak`<br>`boga`<br>`ikizler`<br>`yengec`<br>`aslan`<br>`basak`<br>`terazi`<br>`akrep`<br>`yay`<br>`koc`<br>`kova`<br>`balik` |  | Bilgileri istenen burcun değeri. |   
| <p align="center">`tip`</p> |  <p align="center">hayır</p>  | `gunluk`<br>`haftalik`<br>`aylik`<br>`yillik`<br>`genel` | <p align="center">gunluk</p> | Yorumu istenilen burcun tip değeri. Burcun genel özellikleri için genel değeri yazılmalıdır. |
| <p align="center">`api_key`</p> | <p align="center">evet</p> | API anahtarı |  | Api key'ler aylık maksimum 100 istek ile sınırlandırılmıştır. Api key sahibi olabilmek veya ayrıcalıklı kullanıcı statüsüne geçip sınırsız istek hakkına sahip olabilmek için iletişime geçmeniz gerekmektedir. |

![-----------------------------------------------------](./Readme%20Resources/Çizgi.png)


## İstek Örnekleri

✅Oğlak burcunun günlük yorumu:

`https://toktasoft.com/api/burclar.php?burc=oglak&api_key=myapikey`

```json
{
  "success": true,
  "result": {
    "burc": "oglak",
    "tip": "gunluk",
    "tarih": "2024-07-02",
    "hafta_numarasi": "27",
    "ay_numarasi": "7",
    "yil": "2024",
    "yorum": "Merhaba! Bugün Oğlak burcu için ...",
    "resim_url": "https://toktasoft.com/..."
  },
  "monthly_request_count": 34
}
```

✅Oğlak burcunun haftalık yorumu:

`https://toktasoft.com/api/burclar.php?burc=oglak&tip=haftalik&api_key=myapikey`

```json
{
  "success": true,
  "result": {
    "burc": "oglak",
    "tip": "haftalik",
    "tarih": "2024-08-05",
    "hafta_numarasi": "32",
    "ay_numarasi": "8",
    "yil": "2024",
    "yorum": "Bu hafta, iş ve kariyer alanında ...",
    "resim_url": "https://toktasoft.com/..."
  },
  "monthly_request_count": 67
}
```

✅Oğlak burcunun genel özellikleri:

`https://toktasoft.com/api/burclar.php?burc=oglak&tip=genel&api_key=myapikey`

```json
{
  "success": true,
  "result": {
    "yonetici_gezegeni_yildizi": "Satürn",
    "gruplar": [
      "Toprak",
      "Öncü",
      "Negatif",
      "Dişi"
    ],
    "temsil_ettigi_ev": "10. Ev",
    "vucutta_temsil_ettigi_yer": [
      "Diz",
      "Diş",
      "Kemikler"
    ],
    "genel": "Toprak grubunun üyelerinden olan Oğlak burcu ...",
    "is_hayati": "Aslında iş hayatının burçlardaki karşılığı Oğlak burcudur ...",
    "saglik": "Dayanıklı Oğlak burçları ...",
    "unluler": [
      "Muhammad Ali",
      "Barış Manço",
      "Burak Özçivit",
    ],
    "iliskiler": "Duygularını göstermekte zorlanan ...",
    "kadin": "Hayatının her alanında olduğu gibi ...",
    "erkek": "Sevgisini belli edemeyen Oğlak erkeği ...",
    "resim_url": "https://toktasoft.com/..."
  },
  "monthly_request_count": 81
}
```

❌Yanlış istek:

`https://toktasoft.com/api/burclar.php?burc=zurafa&tip=aylik&api_key=myapikey`

```json
{
  "success": false,
  "error": "Geçersiz burç parametresi.",
  "monthly_request_count": 105
}
```

❌Yanlış istek:

`https://toktasoft.com/api/burclar.php?burc=oglak&tip=omurluk&api_key=myapikey`

```json
{
  "success": false,
  "error": "Geçersiz tip parametresi.",
  "monthly_request_count": 204
}
```

![-----------------------------------------------------](./Readme%20Resources/Çizgi.png)


## Lisans
    Copyright 2024 Mustafa TOKTAŞ

    Licensed under the GNU General Public License v3.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        https://www.gnu.org/licenses/gpl-3.0.html

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

![-----------------------------------------------------](./Readme%20Resources/Çizgi.png)


## İletişim

<a href="mailto:info@mustafatoktas.com"              target="_blank"> <img src="./Readme Resources/İletişim/Mail.png"     alt="Mail"     width="64" heigh="64"/> </a>
<a href="https://t.me/mustafatoktas00"               target="_blank"> <img src="./Readme Resources/İletişim/Telegram.png" alt="Telegram" width="64" heigh="64"/> </a>
<a href="https://www.linkedin.com/in/mustafatoktas/" target="_blank"> <img src="./Readme Resources/İletişim/LinkedIn.png" alt="LinkedIn" width="64" heigh="64"/> </a>
