# Node.js/Express Interview Savollar

### 1. Node.js event-driven architecture qanday ishlaydi?

👉 Node.js **event loop** orqali ishlaydi.

- Kodni bitta thread bajaradi, lekin I/O ishlar (file, DB, network) **asynchronous** ishlaydi.
- Callback yoki Promise orqali natija qaytadi.

📌 Ya’ni: **"kutib o‘tirma, event tugagach meni chaqir"** tamoyili.

---

### 2. Middleware nima va Express.js da qanday ishlatiladi?

👉 Middleware — Express’da request va response o‘rtasida ishlaydigan funksiyalar.

- Har bir `req` va `res` dan oldin yoki keyin ishlaydi.
- Masalan: log yozish, auth tekshirish, body parse qilish.

📌 Misol:

```jsx
app.use((req, res, next) => {
  console.log(req.method, req.url);
  next();
});

```

---

### 3. `require` va `import` orasidagi farq nima?

- **require** → CommonJS (Node.js eski standarti). Dynamic chaqirsa bo‘ladi.
- **import** → ES6 modules (zamonaviy). Static, transpiler (Babel, TypeScript) kerak bo‘lishi mumkin.

---

### 4. npm va yarn orasidagi farq nima?

- **npm** — Node.js bilan birga keladigan package manager.
- **yarn** — Facebook ishlab chiqqan tezroq va xavfsizroq package manager.

📌 Farqi:

- Yarn tezroq va offline cache ishlatadi.
- npm 7+ versiyalaridan keyin farq deyarli yo‘qoldi.

---

### 5. Express.js da routing qanday amalga oshiriladi?

👉 Routing — URL va HTTP method asosida handler yozish.

📌 Misol:

```jsx
app.get('/users', (req, res) => {
  res.send('Barcha userlar');
});

app.post('/users', (req, res) => {
  res.send('Yangi user qo‘shildi');
});

```

---

### 6. Error handling Express.js da qanday qilinadi?

👉 Maxsus error middleware ishlatiladi.

- Oddiy middlewaredan farqi: **4 ta parametri bo‘ladi** `(err, req, res, next)`.

📌 Misol:

```jsx
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Xatolik yuz berdi!');
});
```

---

### 7. CORS nima va qanday hal qilinadi?

👉 **CORS (Cross-Origin Resource Sharing)** — boshqa domenlardan kelgan requestlarga cheklov.

- Default bo‘yicha browser bloklaydi.

📌 Hal qilish:

```jsx
const cors = require('cors');
app.use(cors());
```

---

### 8. Environment variables qanday ishlatiladi?

👉 Config (port, DB URL, API key)ni `.env` faylda saqlaymiz.

📌 Misol:

`.env`

```
PORT=5000
DB_URL=mongodb://localhost:27017/test
```

`server.js`

```jsx
require('dotenv').config();
console.log(process.env.PORT);

```

---

### 9. `process.nextTick()` va `setImmediate()` farqi nima?

- **process.nextTick()** → callbackni **hozirgi event loop** tugagach darhol bajaradi.
- **setImmediate()** → callbackni **keyingi event loop iteration**da bajaradi.

📌 Ya’ni: `nextTick` tezroq, `setImmediate` biroz keyinroq.

---

### 10. Node.js da stream nima va qanday ishlatiladi?

👉 Stream — katta fayllarni yoki data’ni **bo‘lak-bo‘lak qilib oqimda** uzatish mexanizmi.

- Fayl, video, HTTP request-response ham stream bo‘lishi mumkin.

📌 Misol: faylni oqimda o‘qish:

```jsx
const fs = require('fs');
const readStream = fs.createReadStream('file.txt', 'utf8');

readStream.on('data', chunk => {
  console.log('Chunk:', chunk);
});

```

# Node.js/Express Interview Savollar 2-qism (10 ta)

### 1. Child process nima va qanday yaratiladi?

👉 **Child process** — Node.js’da boshqa jarayon (process)ni yaratish imkoniyati.

- CPU-intensiv yoki boshqa dasturlarni ishga tushirish uchun ishlatiladi.

📌 Misol:

```jsx
const { exec } = require('child_process');

exec('ls', (err, stdout, stderr) => {
  if (err) throw err;
  console.log(stdout);
});
```

---

### 2. Clustering Node.js da qanday ishlaydi?

👉 Node.js **bitta thread** ishlatadi, lekin **clustering** orqali bir nechta CPU core’dan foydalanish mumkin.

- Har bir core uchun alohida process yaratiladi.
- Load balancer orqali so‘rovlar taqsimlanadi.

📌 Misol:

```jsx
const cluster = require('cluster');
const http = require('http');
const numCPUs = require('os').cpus().length;

if (cluster.isMaster) {
  for (let i = 0; i < numCPUs; i++) cluster.fork();
} else {
  http.createServer((req, res) => res.end('Hello!')).listen(3000);
}
```

---

### 3. Session va JWT authentication farqi nima?

- **Session** → serverda saqlanadi (cookie orqali session ID yuboriladi).
- **JWT (JSON Web Token)** → token clientda saqlanadi, server tokenni tekshiradi, lekin session saqlamaydi.

✅ JWT — stateless, microservices uchun qulay.

✅ Session — oddiy loyihalar uchun qulayroq.

---

### 4. Rate limiting qanday implement qilinadi?

👉 Rate limiting — foydalanuvchi ko‘p so‘rov yuborib serverni yiqitmasligi uchun **cheklash**.

📌 Express misol:

```jsx
const rateLimit = require("express-rate-limit");

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 daqiqa
  max: 100 // maksimal 100 request
});

app.use(limiter);

```

---

### 5. Multer middleware nima uchun ishlatiladi?

👉 **Multer** — Express’da fayl upload qilish uchun ishlatiladigan middleware.

- FormData orqali yuborilgan fayllarni serverga saqlaydi.

📌 Misol:

```jsx
const multer = require('multer');
const upload = multer({ dest: 'uploads/' });

app.post('/upload', upload.single('file'), (req, res) => {
  res.send('Fayl yuklandi!');
});

```

---

### 6. Morgan middleware nima qiladi?

👉 **Morgan** — Express uchun log middleware.

- Har bir request haqida log chiqaradi (method, url, status, vaqt).

📌 Misol:

```jsx
const morgan = require('morgan');
app.use(morgan('dev'));

```

---

### 7. Helmet.js nima va nima uchun kerak?

👉 **Helmet** — Express’da xavfsizlik uchun ishlatiladigan middleware.

- HTTP header’larni sozlab, **XSS, Clickjacking, MIME sniffing** hujumlardan himoya qiladi.

📌 Misol:

```jsx
const helmet = require('helmet');
app.use(helmet());

```

---

### 8. Database connection pooling nima?

👉 **Connection pooling** — DB bilan har safar yangi ulanish ochmasdan, mavjud ulanishlarni qayta ishlatish.

- Performance oshadi.
- Resource tejaydi.

📌 Misol (Postgres):

```jsx
const { Pool } = require('pg');
const pool = new Pool({ connectionString: process.env.DB_URL });

pool.query('SELECT * FROM users', (err, res) => {
  console.log(res.rows);
});

```

---

### 9. PM2 nima va nima uchun ishlatiladi?

👉 **PM2** — Node.js process manager.

- App crash bo‘lsa qayta ishga tushiradi.
- Cluster mode qo‘llab-quvvatlaydi.
- Monitoring va log saqlaydi.

📌 Ishlatish:

```bash
pm2 start app.js
pm2 list
pm2 logs
```

---

### 10. Graceful shutdown qanday implement qilinadi?

👉 Graceful shutdown — serverni to‘xtatayotganda **ochiq connectionlarni tugatib**, keyin yopish.

📌 Misol:

```jsx
const server = app.listen(3000);

process.on('SIGTERM', () => {
  console.log('Server to‘xtayapti...');
  server.close(() => {
    console.log('Barcha connection yopildi');
    process.exit(0);
  });
});

```