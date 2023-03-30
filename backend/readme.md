# Point of Sale Uygulaması (BACKEND)
#### Bu proje, Node.js, Express.js ve MongoDB kullanılarak geliştirilmiş bir Point of Sale uygulamasıdır.

##### Gereksinimler
- Node.js (v14 veya üzeri)
- MongoDB (v4 veya üzeri)

##### Kurulum
- Bu depoyu kopyalayın veya indirin.
- npm install komutunu kullanarak bağımlılıkları yükleyin.
- .env.sample dosyasını .env olarak kopyalayın ve değişkenleri ayarlayın.
- npm start komutuyla uygulamayı başlatın.

### KLASÖR YAPISI

```
├── controllers/
│   ├── products.js
│   ├── orders.js
│   ├── customers.js
│   ├── payments.js
│   └── users.js
│ 
├── models/
│   ├── product.js
│   ├── order.js
│   ├── customer.js
│   ├── payment.js
│   └── user.js
│ 
├── routes/
│   ├── products.js
│   ├── orders.js
│   ├── customers.js
│   ├── payments.js
│   └── users.js
│ 
├── app.js
├── config.js
├── package.json
└── README.md
```
- controllers: Bu klasör, tüm API endpoint'lerine ait fonksiyonları içerir.
- models: Bu klasör, veritabanı modellerini içerir.
- routes: Bu klasör, tüm API endpoint'lerine ait rotaları içerir.
- app.js: Bu dosya, uygulamanın ana dosyasıdır.
- config.js: Bu dosya, uygulamanın yapılandırma ayarlarını içerir.
- package.json: Bu dosya, uygulamanın bağımlılıklarını içerir.
- README.md: Bu dosya, uygulamanın açıklamalarını içerir.

## Olması Gereken Endpoint Listesi

-   `GET /api/products`: Tüm ürünleri listeler    
-   `GET /api/products/:id`: Belirli bir ürünü gösterir    
-   `POST /api/products`: Yeni bir ürün ekler    
-   `PUT /api/products/:id`: Belirli bir ürünü günceller    
-   `DELETE /api/products/:id`: Belirli bir ürünü siler    
-   `GET /api/orders`: Tüm siparişleri listeler    
-   `GET /api/orders/:id`: Belirli bir siparişi gösterir    
-   `POST /api/orders`: Yeni bir sipariş ekler    
-   `PUT /api/orders/:id`: Belirli bir siparişi günceller    
-   `DELETE /api/orders/:id`: Belirli bir siparişi siler    
-   `GET /api/customers`: Tüm müşterileri listeler    
-   `GET /api/customers/:id`: Belirli bir müşteriyi gösterir    
-   `POST /api/customers`: Yeni bir müşteri ekler    
-   `PUT /api/customers/:id`: Belirli bir müşteriyi günceller    
-   `DELETE /api/customers/:id`: Belirli bir müşteriyi siler    
-   `GET /api/payments`: Tüm ödemeleri listeler    
-   `GET /api/payments/:id`: Belirli bir ödemeyi gösterir    
-   `POST /api/payments`: Yeni bir ödeme ekler    
-   `PUT /api/payments/:id`: Belirli bir ödemeyi günceller    
-   `DELETE /api/payments/:id`: Belirli bir ödemeyi siler    
-   `POST /api/login`: Kullanıcı girişi yapar ve bir JWT döndürür

# JWT
JWT (**JSON Web Token**) kullanarak kimlik doğrulama ve yetkilendirme işlemlerini gerçekleştirmek mümkündür. JWT, JSON formatında bir token olup, kullanıcıların yetkilendirme bilgilerini depolamak için kullanılır.

JWT kullanarak uygulamada kullanıcıların kimlik doğrulama ve yetkilendirme işlemlerini gerçekleştirmek için aşağıdaki adımlar izlenebilir:

1.  Kullanıcı, uygulamaya giriş yapar ve kimlik bilgilerini girer.
2.  Kullanıcının kimlik bilgileri, sunucu tarafından doğrulanır ve bir JWT token oluşturulur.
3.  JWT token, kullanıcının tarayıcısına gönderilir ve her istek için bu token gönderilir.
4.  Sunucu, JWT token'ı doğrular ve kullanıcının kimlik bilgilerini kullanarak işlemi gerçekleştirir.

Bunun için projeye `jsonwebtoken` modülünü ekleyerek JWT oluşturma ve doğrulama işlemlerini gerçekleştirebilirsiniz.

İşte örnek bir kullanım:
```
const jwt = require('jsonwebtoken');

// Kullanıcı bilgileri
const user = {
  username: 'kullaniciadi',
  password: 'sifre'
};

// Token oluşturma
const token = jwt.sign(user, 'gizli anahtar');

// Token doğrulama
jwt.verify(token, 'gizli anahtar', (err, decoded) => {
  if (err) {
    console.log('Token doğrulama hatası:', err);
  } else {
    console.log('Token doğrulandı:', decoded);
  }
});
```
Bu örnekte `jwt.sign()` fonksiyonu kullanıcı bilgilerini şifreleyerek bir token oluşturur ve `jwt.verify()` fonksiyonu oluşturulan token'ın doğruluğunu kontrol eder. `jwt.sign()` fonksiyonunda kullanılan `gizli anahtar`, token'ın şifrelenmesi için kullanılan özel bir anahtardır ve uygulama tarafından saklanması gereken gizli bir bilgidir.

Uygulamanın JWT kullanarak kimlik doğrulama ve yetkilendirme işlemlerini gerçekleştirmesi için, öncelikle `jsonwebtoken` modülünü yüklemeniz ve JWT oluşturma ve doğrulama fonksiyonlarını uygun şekilde kullanmanız gerekmektedir. Ayrıca, kullanıcıların kimlik bilgilerini doğru şekilde saklamak ve güvenli bir şekilde işlem yapmak için HTTPS protokolü kullanmanız önerilir.

# .ENV DOSYASI KULLANMAK
`.env` dosyası kullanarak uygulamada kullanılan özel bilgileri saklamak ve korumak mümkündür. Örneğin, veritabanı bağlantı bilgileri, kimlik doğrulama anahtarları gibi hassas bilgiler bu dosyada saklanabilir.

`.env` dosyasını kullanmak için şu adımları izleyebilirsiniz:

1.  Öncelikle, `dotenv` modülünü yüklemeniz gerekmektedir. `dotenv` modülü, `.env` dosyasındaki değişkenleri okumak için kullanılır.

`npm install dotenv`

2.  `.env` dosyasını projenizin ana dizinine ekleyin ve gizli bilgileri burada tanımlayın. Örneğin, veritabanı bağlantı bilgileri için aşağıdaki değişkenleri tanımlayabilirsiniz:

```
DB_HOST=localhost 
DB_USER=root DB_PASSWORD=password123
```

3.  `.env` dosyasındaki değişkenlere erişmek için `process.env` değişkenini kullanabilirsiniz. Örneğin, `DB_HOST` değişkenine erişmek için şu kodu kullanabilirsiniz:

`const  dbHost = process.env.DB_HOST;`

4.  `.env` dosyasındaki değişkenleri kullanmak için öncelikle `dotenv` modülünü yüklemeniz gerekmektedir. Uygulamanın ana giriş dosyasında (genellikle `app.js` veya `index.js` gibi) aşağıdaki kodu kullanarak `dotenv` modülünü yükleyin:

`require('dotenv').config();`

Bu kod, projenin ana dizinindeki `.env` dosyasını yükler ve `process.env` değişkenine `.env` dosyasındaki değişkenleri ekler.

5.  `.env` dosyasında tanımlanan değişkenlere erişmek için, uygulamanın diğer dosyalarında `process.env` değişkenini kullanabilirsiniz.

Örneğin, `.env` dosyasında tanımlanan `PORT` değişkenine erişmek için aşağıdaki kodu kullanabilirsiniz:

`const  port = process.env.PORT  ||  3000;`

Yukarıdaki kod, `PORT` değişkeni tanımlıysa, `.env` dosyasındaki değeri kullanır, aksi takdirde 3000 değerini kullanır.

`.env` dosyası kullanarak gizli bilgileri saklamak ve korumak, uygulamayı daha güvenli hale getirir. Ancak, `.env` dosyasındaki bilgilerin de güvenli bir şekilde saklanması gerekmektedir. Bu nedenle, `.env` dosyasının sızdırılmaması için dikkatli olunması önemlidir.

# ÖNE ÇIKARACAK ADIMLAR

- Swagger Dokümantasyonu olmalı
- UNIT testler yazılmalı
- Veritabanı parolası gibi bilgiler bir .env dosyasından gelmeli.
- JWT Kullanılmalı
- JWT ile autH
- .env file kullanımı




