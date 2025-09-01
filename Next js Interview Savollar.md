# Next.js Interview Savollar

### 1. Next.js nima va u React’dan qanday farq qiladi?

👉 Next.js — React ustida qurilgan framework.

- **React** faqat frontend library.
- **Next.js** esa SSR (Server-Side Rendering), SSG (Static Site Generation), API routes va SEO-friendly imkoniyatlarni beradi.

---

### 2. SSR (Server-Side Rendering) nima?

👉 Har bir request kelganda sahifa **serverda render qilinib**, to‘liq HTML qaytariladi.

- SEO uchun yaxshi.
- Dinamik ma’lumotlarda ishlatiladi.

📌 Misol:

```jsx
export async function getServerSideProps() {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();
  return { props: { data } };
}

```

---

### 3. SSG (Static Site Generation) nima?

👉 Build paytida HTML fayllar tayyorlab qo‘yiladi va CDN orqali tez yetkaziladi.

- Blog, dokumentatsiya, statik content uchun ideal.

📌 Misol:

```jsx
export async function getStaticProps() {
  const data = await getData();
  return { props: { data } };
}

```

---

### 4. ISR (Incremental Static Regeneration) nima?

👉 SSG + revalidation.

- Build qilgandan keyin ham sahifalar **ma’lum vaqtda yangilanadi**.

📌 Misol:

```jsx
export async function getStaticProps() {
  return {
    props: { data },
    revalidate: 60, // har 60 soniyada yangilanadi
  };
}

```

---

### 5. `getServerSideProps`, `getStaticProps`, `getStaticPaths` farqi nima?

- **getServerSideProps** → har requestda ishlaydi (SSR).
- **getStaticProps** → build vaqtida ishlaydi (SSG).
- **getStaticPaths** → dinamik route’larda ishlatilib, qaysi sahifalar build qilinishini belgilaydi.

---

### 6. API routes nima va qanday ishlatiladi?

👉 Next.js ichida **backend API** yozish mumkin.

📌 Misol: `/pages/api/hello.js`

```jsx
export default function handler(req, res) {
  res.status(200).json({ message: 'Hello API' });
}

```

---

### 7. Image optimization qanday ishlaydi?

👉 Next.js `next/image` komponenti orqali rasmni optimallashtirib beradi:

- Lazy loading, resizing, format optimization.

📌 Misol:

```jsx
import Image from 'next/image';

<Image src="/photo.png" alt="rasm" width={500} height={500} />

```

---

### 8. Next.js da routing qanday ishlaydi?

👉 File-based routing.

- `/pages/about.js` → `/about` route.
- `[id].js` → dynamic routing.

📌 Misol: `/pages/products/[id].js` → `/products/123`

---

### 9. Next.js da SEO qanday yaxshilanadi?

- Server-side rendering orqali to‘liq HTML beriladi.
- `next/head` orqali meta teg qo‘shish mumkin.

📌 Misol:

```jsx
import Head from 'next/head';

<Head>
  <title>My Page</title>
  <meta name="description" content="SEO optimized page" />
</Head>

```

---

### 10. Middleware nima va qachon ishlatiladi?

👉 Middleware — request kelganda sahifaga yetmasdan oldin ishlaydi.

- Auth check, redirect, logging uchun ishlatiladi.

📌 Misol: `/middleware.js`

```jsx
import { NextResponse } from 'next/server';

export function middleware(req) {
  if (!req.cookies.token) {
    return NextResponse.redirect('/login');
  }
}

```