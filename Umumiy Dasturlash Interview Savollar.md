# Umumiy Dasturlash Interview Savollar

### 1. Refactoring nima va nima uchun muhim?

👉 Refactoring — kodni **funksionallikni o‘zgartirmasdan** yaxshilash jarayoni.

- Kodni o‘qish va tushunish osonlashadi.
- Xatolarni topish yengillashadi.
- Keyinroq qo‘shimcha qilish qulay bo‘ladi.

📌 Misol: uzun `if` kodini alohida funksiya qilib chiqarish.

---

### 2. Syntactic sugar nima? Misollar keltiring.

👉 Bu kodni **o‘qish va yozishni qulaylashtiradigan sintaksis**. Aslida u oddiy kodga aylanadi.

📌 Misol (JavaScript):

```jsx
// Oddiy
let arr = [1,2,3];
for (let i = 0; i < arr.length; i++) {
  console.log(arr[i]);
}

// Syntactic sugar (forEach)
arr.forEach(num => console.log(num));

```

---

### 3. DRY principle nima?

👉 **Don’t Repeat Yourself** – bir xil kodni qayta-qayta yozmaslik.

- Takrorlanuvchi kodni funksiya yoki modulga ajratish kerak.

---

### 4. SOLID principles qaysilar?

OOP uchun 5 asosiy qoida:

1. **S** – Single Responsibility → bitta klass/funksiyaning faqat bitta vazifasi bo‘lishi kerak.
2. **O** – Open/Closed → kod kengaytirishga ochiq, lekin mavjudini o‘zgartirishga yopiq.
3. **L** – Liskov Substitution → child klass ota klass o‘rnida ishlashi kerak.
4. **I** – Interface Segregation → katta interfeysni kichiklarga bo‘lish kerak.
5. **D** – Dependency Inversion → yuqori darajadagi modul pastkiga qattiq bog‘lanmasin.

---

### 5. Code review nima uchun muhim?

👉 Code review — boshqa dasturchilar sizning kodni ko‘rib chiqishi.

- Xatolar tezroq aniqlanadi.
- Kod sifati oshadi.
- Team ichida bilim almashiladi.

---

### 6. Git workflow qanday ishlaydi? (merge, rebase farqi)

👉 Git workflow — **branchlar orqali ishlash usuli**.

- **merge** → branchni qo‘shadi, tarixni saqlab qoladi.
- **rebase** → branch tarixini "tozalaydi", bitta liniya kabi ko‘rsatadi.

---

### 7. API versioning qanday amalga oshiriladi?

👉 API o‘zgarsa eski foydalanuvchilarni buzmaslik uchun versiyalash qilinadi.

📌 Usullar:

- URL orqali: `/api/v1/users`
- Header orqali: `Accept: application/vnd.myapi.v2+json`

---

### 8. Caching strategies qaysilar?

👉 Cache — ma’lumotni vaqtincha saqlab, tezroq olish usuli.

Turlari:

- **Browser cache**
- **CDN cache**
- **Server-side cache** (Redis, Memcached)
- **Client-side cache** (React Query, SWR)

---

### 9. Database indexing nima va nima uchun muhim?

👉 Index — ma’lumotni tez topish uchun qo‘shimcha strukturasi.

- Kitobdagi **mundarija**ga o‘xshaydi.
- `SELECT` tez ishlaydi.
- Lekin `INSERT`/`UPDATE` sekinlashishi mumkin (chunki index ham yangilanadi).

---

### 10. Microservices va monolith architecture farqi nima?

- **Monolith** → butun dastur bitta kod bazada. Oddiy, lekin katta loyihada murakkablashadi.
- **Microservices** → dastur kichik mustaqil servislar to‘plami. Har biri alohida ishlaydi. Skalalash va qo‘llash oson, lekin boshqarish murakkab.

# Umumiy Dasturlash Interview Savollar (10 ta)

### 1. RESTful API design principles qaysilar?

👉 REST API quyidagi qoidalarga asoslanadi:

- **Stateless** → har bir request mustaqil bo‘lishi kerak (server session saqlamaydi).
- **Resource-based** → URL resursni ifodalaydi: `/users/1`.
- **HTTP methods** → CRUD uchun ishlatiladi:
    - GET (o‘qish), POST (yaratish), PUT/PATCH (yangilash), DELETE (o‘chirish).
- **Proper status codes** ishlatish kerak.
- **Versioning** → `/api/v1/...`.

---

### 2. HTTP status codes: 200, 201, 400, 401, 403, 404, 500 nima degani?

- **200 OK** → hammasi joyida.
- **201 Created** → yangi resurs yaratildi.
- **400 Bad Request** → noto‘g‘ri so‘rov.
- **401 Unauthorized** → login qilinmagan.
- **403 Forbidden** → login qilingan, lekin ruxsat yo‘q.
- **404 Not Found** → topilmadi.
- **500 Internal Server Error** → serverda xato.

---

### 3. Authentication va Authorization farqi nima?

- **Authentication** → foydalanuvchi kimligini tekshirish (login, parol, token).
- **Authorization** → foydalanuvchiga qanday ruxsat borligini tekshirish (rol: admin, user).

👉 Ya’ni: avval kimligini tekshiramiz (authN), keyin nima qila olishini (authZ).

---

### 4. SQL injection qanday oldini olinadi?

👉 SQL injection — foydalanuvchi kiritgan malumotni to‘g‘ridan-to‘g‘ri query ichida ishlatganda yuzaga keladigan xujum.

📌 Himoya:

- **Prepared statements** ishlatish (`?` yoki `$1` placeholder bilan).
- ORM kutubxonalaridan foydalanish.
- Inputni tozalash.

---

### 5. XSS attack nima va qanday himoyalanadi?

👉 XSS (Cross-Site Scripting) — foydalanuvchi kiritgan kod (masalan `<script>`) brauzerda ishlashi.

📌 Himoya:

- Input/outputni sanitize qilish.
- HTML escape qilish (`<` → `&lt;`).
- HTTP-only cookie ishlatish.

---

### 6. CSRF attack nima?

👉 CSRF (Cross-Site Request Forgery) — foydalanuvchi login bo‘lib turganda boshqa sayt uning nomidan so‘rov yuborishi.

📌 Himoya:

- **CSRF token** ishlatish.
- **SameSite cookie**.
- **Double submit cookie** texnikasi.

---

### 7. Docker container nima va nima uchun ishlatiladi?

👉 Docker container — dasturni ishlashi uchun kerak bo‘lgan **hamma narsa (kod, kutubxonalar, konfiguratsiya)**ni bitta paketga joylab beradi.

✅ Afzalligi:

- Har joyda bir xil ishlaydi.
- Deploy qilish oson.
- Resurslardan samarali foydalanadi.

---

### 8. Load balancing nima?

👉 Load balancing — kelayotgan so‘rovlarni bir nechta serverga **teng taqsimlash**.

- Serverlar ishdan chiqsa ham xizmat to‘xtab qolmaydi.
- Ishlash tezligi oshadi.

---

### 9. CDN (Content Delivery Network) nima?

👉 CDN — dunyo bo‘ylab joylashgan serverlar tarmog‘i, ular statik fayllarni (rasm, video, CSS, JS) foydalanuvchiga yaqin joydan beradi.

✅ Natija:

- Yuklanish tezroq.
- Serverga yuk kamayadi.
- DDOS hujumdan himoya.

---

### 10. Database normalization nima va nima uchun kerak?

👉 Normalization — ma’lumotlar bazasida takrorlanuvchi ma’lumotni kamaytirish va tartibga solish jarayoni.

📌 Maqsad:

- Takroriy ma’lumot bo‘lmasin.
- O‘qish va yozish qulay bo‘lsin.
- Ma’lumot yaxlitligi (integrity) saqlansin.

Misol: `users` va `orders`ni alohida jadval qilish, `user_id` orqali bog‘lash.