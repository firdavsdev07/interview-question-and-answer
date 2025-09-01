# TypeScript Interview Savollar

### 0. TypeScript nima?

👉 TypeScript — bu **JavaScript + qo‘shimcha "type" (tur) tekshiruvlari**.

Ya’ni **JavaScript o‘zi qanday ishlasa**, TypeScript ham shunday ishlaydi, faqat oldindan turini belgilab qo‘yish imkoniyati bor.

⚡️ Foydasi:

- Katta loyihalarda xato qilmaslikka yordam beradi.
- IDE (VS Code) avtomatik yordam beradi (`autocompletion`, xato chizib ko‘rsatish).
- Kodni boshqalarga o‘qish osonlashadi.

📌 Oddiy misol:

```tsx
// JavaScript
let age = 25;
age = "yigirma besh"; // XATO, lekin JS jim yuradi

// TypeScript
let age: number = 25;
age = "yigirma besh"; // ❌ xato, kompilyator ogohlantiradi
```

---

### 1. TypeScript JavaScript dan qanday farq qiladi?

👉 JavaScript — **hamma narsaga ruxsat beradigan** til. Xatoni faqat brauzerda ishga tushganda ko‘rasiz.

👉 TypeScript esa — **qoidali**: kim nima yozishini oldindan tekshiradi.

💡 Misol:

```tsx
// JavaScript
function add(a, b) {
  return a + b;
}

add(5, "10"); // natija: "510" 🤯

// TypeScript
function add(a: number, b: number): number {
  return a + b;
}

add(5, 10); // ✅ 15
add(5, "10"); // ❌ xato, string emas son kerak

```

---

### 2. Interface va type alias orasidagi farq nima?

👉 `interface` va `type` ikkalasi ham **ma’lumot strukturasi**ni belgilaydi.

- `interface` → faqat obyektlar uchun ishlatiladi va kengaytirish (`extends`) uchun qulay.
- `type` → hamma narsaga ishlaydi: obyekt, primitive, union, function va h.k.

📌 Misol:

```tsx
// Interface bilan
interface User {
  id: number;
  name: string;
}

// Type bilan
type ID = number | string;

```

👉 Oddiy qilib aytganda:

- **interface** – "ob’ektning shakli".
- **type** – "hamma narsaga nom qo‘yish".

---

### 3. Generics nima va qanday ishlatiladi?

👉 Generics — bu **universal type yozish**.

Ya’ni funksiyani bir marta yozasiz, keyin turli type bilan ishlataverasiz.

📌 Misol:

```tsx
function box<T>(value: T): T {
  return value;
}

let a = box<number>(5);       // son bilan ishlaydi
let b = box<string>("salom"); // string bilan ishlaydi

```

👉 Oddiy qilib: `T` bu — **“keyinchalik aniqlanadigan tur”**.

---

### 4. Union types va intersection types farqi nima?

- **Union (`|`)** → "yoki bu, yoki u".
- **Intersection (`&`)** → "ikkalasi ham bo‘lishi shart".

📌 Misol:

```tsx
// Union
let id: number | string;
id = 5;
id = "abc"; // ikkalasi ham mumkin

// Intersection
type Person = { name: string };
type Employee = { id: number };

type Worker = Person & Employee;
// { name: string, id: number }

```

👉 Oddiy qilib:

- Union = variantlar ichidan biri.
- Intersection = hammasi birlashtiriladi.

---

### 5. Optional chaining nima?

👉 JavaScript’da ko‘p xato chiqadi: `Cannot read property of undefined`.

Optional chaining (`?.`) esa: **“agar bo‘lsa ishlat, bo‘lmasa undefined qaytar”** degani.

📌 Misol:

```tsx
let user = { profile: { name: "Ali" } };

console.log(user.profile?.name);  // Ali
console.log(user.address?.city);  // undefined (xato emas)

```

👉 Oddiy qilib: `?.` — "bor bo‘lsa, foydalan; yo‘q bo‘lsa jim yur".

---

### 6. Enum nima va qachon ishlatiladi?

👉 `enum` — bu **nomlangan qiymatlar to‘plami**. Doimiy (constant) qiymatlarni tartib bilan saqlashga qulay.

📌 Misol:

```tsx
enum Direction {
  Up,
  Down,
  Left,
  Right
}

let move: Direction = Direction.Up;

```

👉 Oddiy qilib: `enum` — bu **katta harflarda yozilgan sozlamalar ro‘yxati**.

---

### 7. `any`, `unknown`, `never` types farqi nima?

- **any** → “hammaga ruxsat” (nazorat yo‘q).
- **unknown** → “hamma narsani saqlash mumkin, lekin ishlatishdan oldin tekshir”.
- **never** → “hech qachon qiymat qaytarmaydi”.

📌 Misol:

```tsx
let a: any = 5;
a = "matn"; // mumkin

let u: unknown = "text";
// let x: string = u; ❌ xato
if (typeof u === "string") {
  let x: string = u; ✅
}

function error(): never {
  throw new Error("Xato");
}

```

👉 Oddiy qilib:

- any = "qoidalarsiz".
- unknown = "balki bu, balki u (tekshirish kerak)".
- never = "bu hech qachon bo‘lmaydi".

---

### 8. Type assertion nima?

👉 Type assertion — TypeScript’ga: **"ishon, bu type to‘g‘ri"** deb aytish.

📌 Misol:

```tsx
let value: unknown = "hello";
let strLength: number = (value as string).length;

```

👉 Oddiy qilib: assertion — **majburiy tur ko‘rsatish**.

---

⚡️ Xullas, TypeScript — bu **JavaScriptni yanada tartibli, xavfsizroq** qiladigan til.

- Interface vs type → obyekt uchun interface, boshqa joyda type.
- Generics → kodni universal qiladi.
- Union va Intersection → yoki bu, yoki ikkalasi ham.
- Optional chaining → "undefined xato bermasin".
- Enum → nomlangan constantlar.
- Any / Unknown / Never → nazorat darajasi farqli.
- Assertion → TypeScriptga "ishon, bu to‘g‘ri" deyish.

# 🚀 TypeScript Interview Savollar – 2-qism

### 1. Mapped types nima va qanday ishlatiladi?

👉 Mapped types — bu mavjud type asosida **yangi type yasash**.

Ya’ni, mavjud obyektning propertylarini aylanib chiqib, ularga o‘zgarish kiritish mumkin.

📌 Misol:

```tsx
type User = {
  id: number;
  name: string;
};

// Har bir property readonly bo‘lsin
type ReadonlyUser = {
  [K in keyof User]: User[K];
};
```

👉 Oddiy qilib: Mapped types = **“mavjud type’ni qayta ishlash”**.

---

### 2. Conditional types nima?

👉 Conditional types — bu type’lar orasida **if/else** yozish imkoniyati.

📌 Misol:

```tsx
type IsString<T> = T extends string ? "Yes" : "No";

type A = IsString<string>; // "Yes"
type B = IsString<number>; // "No"
```

👉 Oddiy qilib: Conditional types = **"agar shunaqa bo‘lsa → bu type, bo‘lmasa → boshqa type"**.

---

### 3. Utility types qaysilar? (Pick, Omit, Partial)

👉 Utility types — bu TypeScript’da **tayyor yozilgan yordamchi turlar**.

- **Partial** → barcha property optional bo‘ladi.
- **Pick** → faqat kerakli propertylarni oladi.
- **Omit** → berilgan propertyni olib tashlaydi.

📌 Misol:

```tsx
type User = { id: number; name: string; age: number };

type P = Partial<User>; // { id?: number; name?: string; age?: number }
type X = Pick<User, "id" | "name">; // { id: number; name: string }
type Y = Omit<User, "age">; // { id: number; name: string }

```

👉 Oddiy qilib: Utility types = **tayyor “shablonlar”**.

---

### 4. Type guards nima va qanday yoziladi?

👉 Type guard — bu **qiymatning aniq turini tekshiradigan funksiya yoki shart**.

📌 Misol:

```tsx
function isString(x: unknown): x is string {
  return typeof x === "string";
}

let value: unknown = "hello";

if (isString(value)) {
  console.log(value.toUpperCase()); // bu yerda value aniq string
}

```

👉 Oddiy qilib: Type guard = **“shart bilan turini aniqlash”**.

---

### 5. Declaration merging nima?

👉 Bitta nomdagi `interface` yoki `namespace` **birlashtiriladi**.

📌 Misol:

```tsx
interface User {
  id: number;
}

interface User {
  name: string;
}

// Natija: { id: number; name: string }
const u: User = { id: 1, name: "Ali" };

```

👉 Oddiy qilib: Declaration merging = **bir xil nomli type’lar qo‘shilib ketadi**.

---

### 6. Namespace va module farqi nima?

- **Namespace** → eski usul, bitta faylda kodni guruhlash uchun ishlatilgan.
- **Module** → zamonaviy usul, `import/export` orqali fayllar o‘rtasida kod bo‘linadi.

👉 Hozirgi kunda asosan **module** ishlatiladi.

📌 Misol (module):

```tsx
// user.ts
export const name = "Ali";

// app.ts
import { name } from "./user";

```

---

### 7. Abstract classes va interfaces farqi nima?

- **Interface** → faqat **strukturani** belgilaydi. (metodlar, property nomlari).
- **Abstract class** → metodlarni qisman yozib qo‘yishi mumkin, boshqa class’lar undan meros oladi.

📌 Misol:

```tsx
interface Animal {
  sound(): void; // faqat tuzilma
}

abstract class Bird {
  abstract fly(): void; // yozilmagan
  eat() { console.log("eating"); } // yozilgan
}

```

👉 Oddiy qilib:

- Interface = “qoidalar ro‘yxati”.
- Abstract class = “yarim tayyor class”.

---

### 8. Decorator pattern TypeScript da qanday?

👉 Decorator — bu **class yoki metodga qo‘shimcha xatti-harakat qo‘shadigan funksiya**.

⚠️ `experimentalDecorators` flagini yoqish kerak.

📌 Misol:

```tsx
function Logger(constructor: Function) {
  console.log("Class yaratilmoqda:", constructor.name);
}

@Logger
class Person {}

```

👉 Oddiy qilib: Decorator = **“@ bilan yoziladigan qo‘shimcha imkoniyat”**.

---

### 9. tsconfig.json da strict mode nima beradi?

👉 `strict: true` → TypeScript’da barcha qat’iy qoidalarni yoqadi:

- `noImplicitAny`
- `strictNullChecks`
- `strictBindCallApply` va boshqalar

👉 Oddiy qilib: Strict mode = **“hamma joyda qattiq tekshir”**.

---

### 10. Type narrowing qanday ishlaydi?

👉 Type narrowing — kengroq type (masalan, union) ni **shartlar yordamida toraytirish**.

📌 Misol:

```tsx
function printId(id: number | string) {
  if (typeof id === "string") {
    console.log(id.toUpperCase()); // endi string
  } else {
    console.log(id + 1); // endi number
  }
}

```

👉 Oddiy qilib: Type narrowing = **“avval katta doira, keyin faqat keraklisini olish”**.

---

⚡️ Xullas:

- Mapped types → mavjud type’dan yangisini yaratish.
- Conditional types → if/else type’lar.
- Utility types → tayyor shablonlar (`Pick`, `Omit`, `Partial`).
- Type guards → shart bilan turini aniqlash.
- Declaration merging → bir xil nomli type’lar qo‘shilib ketadi.
- Namespace vs Module → namespace eski, module yangi.
- Abstract vs Interface → biri qoidalar, biri yarim tayyor class.
- Decorator → class/metodga qo‘shimcha imkoniyat.
- Strict mode → qattiq tekshiruvlar.
- Type narrowing → union’dan faqat kerakli turini olish.