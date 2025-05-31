<h1 align="center">
Burç API<a name="readme-top"></a>
</h1>

<div align="center">
  <img src="./Readme Resources/Burç API Logo.png" alt="Logo" width="120"/>
</div>

## **İçindekiler**

- [API Hakkında](#api-hakkında)
- [Dokümantasyon](#dokümantasyon)
- [İstek Örnekleri](#i̇stek-örnekleri)
- [Lisans](#lisans)
- [İletişim](#i̇letişim)


![-----------------------------------------------------](./Readme%20Resources/Line.png)

## API Hakkında

Bu repo, PHP diliyle geliştirilmiş olan burç yorumlarını ve bilgilerini sunan
API'nin dokümantasyonunu içerir.

HTTP GET istekleriyle `burc`, `tip` ve `api_key` parametrelerini alır ve bütün burçların
günlük, haftalık, aylık, yıllık yorumlarını JSON formatında sağlar.

JSON dosyasında her burç için burcu temsil eden 256 x 256 çözünürlüğünde png uzantılı resim barındıran url adresi de bulunmaktadır.

Ayrıca tip parametresine "genel" değeri yazılarak burçların detaylı karakter özellikleri öğrenilebilir.


![-----------------------------------------------------](./Readme%20Resources/Line.png)

## Dokümantasyon

Base URL: `https://toktasoft.com/api/burclar`

API 3 farklı parametre almaktadır.

| Parametre                     | Zorunlu Mu?                 | Değerler                                                                                               | Varsayılan Değer             | Açıklama                         |
| ----------------------------- | --------------------------- | ------------------------------------------------------------------------------------------------------ | ---------------------------- | -------------------------------- |
| <p align="center">api_key</p> | <p align="center">evet</p>  | API anahtarı                                                                                           |                              | Api key'ler aylık maksimum 100 istek ile sınırlandırılmıştır. Api key sahibi olabilmek veya ayrıcalıklı kullanıcı statüsüne geçip sınırsız istek hakkına sahip olabilmek için iletişime geçmeniz gerekmektedir. |
| <p align="center">burc</p>    | <p align="center">evet</p>  | oglak<br>boga<br>ikizler<br>yengec<br>aslan<br>basak<br>terazi<br>akrep<br>yay<br>koc<br>kova<br>balik |                              | Bilgileri istenen burcun değeri. |   
| <p align="center">tip</p>     | <p align="center">hayır</p> | gunluk<br>haftalik<br>aylik<br>yillik<br>genel                                                         | <p align="center">gunluk</p> | Yorumu istenilen burcun tip değeri. Burcun genel özellikleri için genel değeri yazılmalıdır.                                                                                                                    |


![-----------------------------------------------------](./Readme%20Resources/Line.png)

## İstek Örnekleri

İstek örnekleri `curl` komut satırı aracı kullanılarak gösterilmiştir.

✅**Oğlak burcunun günlük yorumu**

```sh
curl -X GET "https://toktasoft.com/api/burclar?api_key=myapikey&burc=oglak"
```

```json
{
  "status": 200,
  "monthly_request_count": 34,
  "result": {
    "burc": "oglak",
    "tip": "gunluk",
    "tarih": "2025-05-31",
    "hafta_numarasi": "22",
    "ay_numarasi": "5",
    "yil": "2025",
    "yorum": "Son zamanlarda içsel huzur...",
    "resim_url": "https://toktasoft.com/api/api-resources/burclar/oglak.png"
  },
  "error": null
}
```

✅**Oğlak burcunun haftalık yorumu**

```sh
curl -X GET "https://toktasoft.com/api/burclar?api_key=myapikey&burc=oglak&tip=haftalik"
```

```json
{
  "status": 200,
  "monthly_request_count": 67,
  "result": {
    "burc": "oglak",
    "tip": "haftalik",
    "tarih": "2025-05-31",
    "hafta_numarasi": "22",
    "ay_numarasi": "5",
    "yil": "2025",
    "yorum": "Bu hafta, iş ve kariyer alanında...",
    "resim_url": "https://toktasoft.com/api/api-resources/burclar/oglak.png"
  },
  "error": null
}
```

✅**Oğlak burcunun genel özellikleri**

```sh
curl -X GET "https://toktasoft.com/api/burclar?api_key=myapikey&burc=oglak&tip=genel"
```

```json
{
  "status": 200,
  "monthly_request_count": 81,
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
    "genel": "Toprak grubunun üyelerinden olan Oğlak burcu...",
    "is_hayati": "Aslında iş hayatının burçlardaki karşılığı Oğlak burcudur...",
    "saglik": "Dayanıklı Oğlak burçları...",
    "unluler": [
      "Burak Özçivit",
      "Barış Manço",
      "Diğer Ünlüler...",
    ],
    "iliskiler": "Duygularını göstermekte zorlanan...",
    "kadin": "Hayatının her alanında olduğu gibi...",
    "erkek": "Sevgisini belli edemeyen Oğlak erkeği...",
    "resim_url": "https://toktasoft.com/api/api-resources/burclar/oglak.png"
  },
  "error": null
}
```

❌**Yanlış istek**

`burc` parametresine tablodaki değerler dışında bir değer girilirse hata döndürülür.

```sh
curl -X GET "https://toktasoft.com/api/burclar?api_key=myapikey&burc=zurafa&tip=aylik"
```

```json
{
  "status": 400,
  "monthly_request_count": 105,
  "result": null,
  "error": "Geçersiz burç parametresi"
}
```

❌**Yanlış istek**

`tip` parametresine tablodaki değerler dışında bir değer girilirse hata döndürülür.

```sh
curl -X GET "https://toktasoft.com/api/burclar?api_key=myapikey&burc=oglak&tip=omurluk"
```

```json
{
  "status": 400,
  "monthly_request_count": 204,
  "result": null,
  "error": "Geçersiz tip parametresi"
}
```


![-----------------------------------------------------](./Readme%20Resources/Line.png)

<div align="center">
  <a href="https://github.com/mustafatoktas/W.BE_RepoVisitorCounterAPI"><img src="https://toktasoft.com/api/repo-visitor-counter?repo=ghb8jc6vnp4tmx7&show_repo_name=1&show_date=1&show_brand=0&txt_color=209,215,224&bg_color=45,52,58" alt="Repo Visitor Counter"/></a>
</div>

<br>
  
<div align="center">
  <a href="https://buymeacoffee.com/mustafatoktas"><img src="./Readme Resources/Communication/Buy Me a Coffee.png" alt="Buy Me a Coffee" height="64"/></a>
</div>


![-----------------------------------------------------](./Readme%20Resources/Line.png)

## Lisans

```
Copyright 2024-2025 Mustafa TOKTAŞ

Licensed under the GNU General Public License v3.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    https://www.gnu.org/licenses/gpl-3.0.html

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```


![-----------------------------------------------------](./Readme%20Resources/Line.png)

## İletişim

<a href="mailto:info@mustafatoktas.com"             ><img src="./Readme Resources/Communication/Mail.png"     alt="Mail"     width="64"/></a>
<a href="https://t.me/mustafatoktas00"              ><img src="./Readme Resources/Communication/Telegram.png" alt="Telegram" width="64"/></a>
<a href="https://www.linkedin.com/in/mustafatoktas/"><img src="./Readme Resources/Communication/LinkedIn.png" alt="LinkedIn" width="64"/></a>

<p align="center">
  <a href="#readme-top"><img src="./Readme Resources/Back to Top.png" alt="Back to Top" height="64"/></a>
</p>
