# JavaScript Interview Savollar

- 1 Hoisting nima va qanday ishlaydi?
    
    Hoisting bu ko’tarish degani . U qanday ishlaydi deyishga misola biron bir o’zgaruvchi e’lon qilib uni o’zidan oldin chaqirish misol bo’ladi va shu tariqa ishlaydi. Bazi bir xatoliklar ham bo’lishimi mumkun o’zidan oldin chaqirishda.
    
    Example:
    
    1 const o’zgaruvchini yaratib uni hoisting qilsak u **ReferenceError** beradi
    
    ```jsx
    console.log(a)
    const a = 5
    ```
    
    2 let bilan ham huddi shu holat yuz beradi yani **ReferenceError**  bo’ladi
    
    ```jsx
    console.log(a)
    let a = 5
    ```
    
    3 var bilan esa biro boshqacha  error bermaydi lekin undefined qaytaradi bo’sh qiymat yani
    
    ```jsx
    console.log(a)
    var a = 5
    ```
    
- 2 Closure nima? Misol keltiring.
    
    Closure bu ichki function bo’lib tashqi function dagi o’zgaruvchilarni olish huquqiga ega. Yani tashqi function tugagandan kiyin ham ichki function  tashqi functionni o’zgaruvchilarini “eslab qoladi” . 
    
    Example:
    
    1 Oddiy misol
    
    ```jsx
    // Oddiy - har safar yangi 'son' yaratiladi
    function oddiyFunksiya() {
       let son = 0; // har safar 0 dan boshlaydi
       son++;       // 1 ga aylantiradi
       console.log(son); // 1 chiqaradi
    } // tugadi, 'son' yo'qoladi
    
    // Closure - bir xil 'son' saqlanadi
    function tashqiFunksiya() {
       let son = 0; // faqat bir marta yaratiladi
       
       function ichkiFunksiya() {
           son++; // shu bir xil 'son' ni oshiradi
           console.log(son);
       }
       
       return ichkiFunksiya; // ichki funksiya 'son' ni "eslab qoladi"
    }
    
    const natija = tashqiFunksiya(); // tashqi funksiya ishga tushdi, 'son=0' yaratildi
    natija(); // 1 (birinchi marta oshirildi)
    natija(); // 2 (ikkinchi marta oshirildi - bir xil 'son' ishlatildi)
    ```
    
    > Bu yerda ko’rishimiz mumkun oddiyFunksiya( ) o’zgaruvchini elsab qola olmayabdi shu sababli har safat natija 1 chiqayabdi.closure uslubida qilingani esa tashqi funksiyadagi o’zgaruvchilarni ichki funskiya yordamida xotira olinayabdi va har  safar chaqirilganda xotitadigi o’zgaruvchini oshirib borayabdi.
    > 
- 3 `let`, `const`, `var` orasidagi farq nima?
    
    > O’zgaruvchilar aslida nima ?
    > 
    
    > O’zgaruvchi bu ma’lum bir qiymatlarni kompyuter xotirasida saqlab turuvchi joy.O’zgaruvchi turli xil qiymatlarni o’z ichida saqlab turadi. Ularga misol **let , const , var**.
    > 
    - **var** - bu o’zgaruvchi javascriptda birinchi o’zgaruvchi hisoblanadi (1995-yilda). Bu o’zgaruvchi eski versiya hisobladan hozirda asosan const va let dan foydalanadi. Kamchiliklari o’zgaruvchini qayta qayta elon qilish mumkun bu katta xatolarga olib kelishi mumkun. JavaScript yaratuvchilari "qulay" bo'lsin deb o'ylashgan, lekin aslida **chalkash** bo'lib qolgan. Shuning uchun hozir **let/const** ishlatamiz!
    - **let** - bu o’zgaruvchi **ES6** versiyada chiqgan. Bu o’zgaruvchi **var** dagi hoisting va qayta qayta e’lon qilib ishlatish kabi muomolarni bar taraf qilgan yani uni qayta qayta e’lon qilib bo’lmaydi lekin o’zgartirish mumkun . Hoisting qilinsa **ReferenceError**  beradi.
    - **const** - bu constanda yani o’zgarmas qiyman uni o’zgartirib bo’lmaydi **let var** kabi o’zgaruvchilarda qiymatni o’zgartish mumkun edi **const** da buni iloji yo’q. Bu o’zgaruvchida ham hoisting qilinsa **ReferenceError** beradi yani o’zgaruvchidan oldin uni chaqirib bo’lmaydi
    
    ### Example:
    
    ```jsx
    // ============= HOISTING MISOLLARI =============
    
    console.log("=== HOISTING ===");
    
    // 1. VAR - hoisting bo'ladi
    console.log(varTest); // undefined
    var varTest = "var qiymati";
    console.log(varTest); // "var qiymati"
    
    // 2. LET - xatolik beradi
    // console.log(letTest); // ReferenceError
    let letTest = "let qiymati";
    console.log(letTest); // "let qiymati"
    
    // 3. CONST - xatolik beradi  
    // console.log(constTest); // ReferenceError
    const constTest = "const qiymati";
    console.log(constTest); // "const qiymati"
    
    console.log("--------------------");
    
    // ============= QAYTA E'LON QILISH =============
    
    console.log("=== QAYTA E'LON QILISH ===");
    
    // 1. VAR - qayta e'lon qilish mumkin
    var name1 = "Ali";
    console.log(name1); // "Ali"
    var name1 = "Vali"; // Muammo yo'q
    console.log(name1); // "Vali"
    var name1 = "Olim"; // Yana muammo yo'q
    console.log(name1); // "Olim"
    
    // 2. LET - qayta e'lon qilish mumkin EMAS
    let name2 = "Ali";
    console.log(name2); // "Ali"
    // let name2 = "Vali"; // SyntaxError: 'name2' has already been declared
    
    // 3. CONST - qayta e'lon qilish mumkin EMAS  
    const name3 = "Ali";
    console.log(name3); // "Ali"
    // const name3 = "Vali"; // SyntaxError: 'name3' has already been declared
    
    console.log("--------------------");
    
    // ============= QIYMATNI O'ZGARTIRISH =============
    
    console.log("=== QIYMATNI O'ZGARTIRISH ===");
    
    // 1. VAR - o'zgartirish mumkin
    var age1 = 20;
    console.log("var boshlang'ich:", age1); // 20
    age1 = 25;
    console.log("var o'zgartirildi:", age1); // 25
    age1 = 30;
    console.log("var yana o'zgartirildi:", age1); // 30
    
    // 2. LET - o'zgartirish mumkin
    let age2 = 20;
    console.log("let boshlang'ich:", age2); // 20
    age2 = 25;
    console.log("let o'zgartirildi:", age2); // 25
    age2 = 30;
    console.log("let yana o'zgartirildi:", age2); // 30
    
    // 3. CONST - o'zgartirish mumkin EMAS
    const age3 = 20;
    console.log("const boshlang'ich:", age3); // 20
    // age3 = 25; // TypeError: Assignment to constant variable
    // age3 = 30; // TypeError: Assignment to constant variable
    
    console.log("--------------------");
    
    // ============= XULOSA =============
    
    console.log("=== XULOSA ===");
    console.log("VAR: qayta e'lon ✅, o'zgartirish ✅, hoisting ✅");
    console.log("LET: qayta e'lon ❌, o'zgartirish ✅, hoisting ❌");
    console.log("CONST: qayta e'lon ❌, o'zgartirish ❌, hoisting ❌");
    ```
    
- 4 Event loop nima ? va u qanday ishlaydi?
    
    # JavaScript Event Loop - To'liq Tushuntirish
    
    ## JavaScript'ning tabiati
    
    Event loop nima ekanini bilishdan oldin JavaScript'ning tabiati biroz gapirsak. JavaScript **single-threaded** holatda ishlaydi yani JavaScript bir vaqtda 1 ta ish qila oladi. Lekin biz bir vaqtni o'zida bir nechta ish qilayotganini ko'ramiz. Bu qanday? Bunga sabab Sinxron va Asinxron "Bajarilish modeli" (***Execution model***).
    
    ## Sinxron (Synchronous) Bajarilish Modeli
    
    **Sinxron – bitta ishni tugatib keyin boshqasiga o'tadi.**
    
    Bunga misol keltirsak biz har yili bir yoshga ulg'ayamiz. 20 yosh bo'lsak bir yildan keyin 21 yosh bo'lamiz, birdaniga 22 yoshga o'ta olmaymiz yani biz navbatma-navbat yoshimiz o'sib boradi. Biz 21 yoshga to'lmasi 22 yoshga o'ta olmaymiz mana shu Sinxron Bajarish moduli hisoblanadi.
    
    javascript
    
    ```jsx
    console.log("2025-yil 20-yosh")
    console.log("2026-yil 21-yosh")  
    console.log("2027-yil 22-yosh")
    *//natija
    // 2025-yil 20-yosh
    // 2026-yil 21-yosh 
    // 2027-yil 22-yosh*
    ```
    
    ## Asinxron (Asynchronous) Bajarilish Modeli
    
    **Asinxron – bir vaqtni o'zida bir nechta ishni bajara oladi.**
    
    Biz oshxonada ovqat qilayabmiz. Birinchi bo'lib tuxum qaytanmoqchimiz u 10 daqiqa vaqt oladi deylik. Ikkinchi ish dasturxon tuzashga 2 daqiqa deylik. Uchinchi bo'lib choy damlash bunga 5 daqiqa ketadi. Bunda Asinxron bajarish modeli qaysi biri tezroq bo'lsa o'sha birinchi deb ish yuritadi. Natijada 1-dasturxon tuzash, 2-choy damlash, 3-tuxum tayyor bo'ladi.
    
    javascript
    
    ```jsx
    setTimeout(() => console.log("Tuxum tayyor"), 10_000);
    setTimeout(() => console.log("Choy qaynadi"), 5000);
    setTimeout(() => console.log("Dasturxon tuzaldi"), 2000);
    console.log("Ish boshlandi") 
    *// bu sinxron modul bo'lgani uchun 1-chi chiqadi
    // Natija:
    // Ish boshlandi
    // Dasturxon tuzaldi
    // Choy qaynadi 
    // Tuxum tayyor*
    ```
    
    ## Event Loop nima uchun kerak?
    
    Endi o'ylashimiz mumkun Event Loop nima uchun kerak?
    
    **"JavaScript bir vaqtda faqat 1 ta ish qila oladi, lekin u qanday qilib 3 ta ishni bir vaqtda kuzatib turadi?"**
    
    **Javob: Event Loop - bu "Boshqaruvchi"**
    
    Event Loop xuddi **oshxonada bosh oshpaz** kabi:
    
    javascript
    
    ```jsx
    setTimeout(() => console.log("Tuxum tayyor"), 10_000);  *// 10 daqiqa*
    setTimeout(() => console.log("Choy qaynadi"), 5000);    *// 5 daqiqa*  
    setTimeout(() => console.log("Dasturxon tuzaldi"), 2000); *// 2 daqiqa*
    console.log("Ish boshlandi");
    ```
    
    ### Event Loop-siz bo'lsa nima bo'lardi?
    
    JavaScript shunday qilardi:
    
    1. "Tuxum tayyor" uchun **10 daqiqa kutadi** (hech narsa qilmaydi!)
    2. Keyin "Choy qaynadi" uchun **5 daqiqa kutadi**
    3. Keyin "Dasturxon tuzaldi" uchun **2 daqiqa kutadi**
    
    **Jami: 17 daqiqa!** 
    
    ### Event Loop bilan:
    
    1. **JavaScript:** "Men kutolmayman! Timer'larni Web API'ga topshiraman!"
    2. **Web API:** "Men vaqtni kuzataman!"
    3. **JavaScript:** "Men boshqa ishlarni qilaman!"
    4. **Event Loop:** "Qaysi timer tugasa, men JavaScript'ga xabar beraman!"
    
    **Jami: 10 daqiqa!** 
    
    ## Call Stack va Callback Queue
    
    Endi Event Loop qanday ishlashini tushunish uchun **Call Stack** va **Callback Queue** tushunchalarini bilishimiz kerak.
    
    ### Call Stack = Oshpazning qo'llari
    
    **Bir vaqtda faqat 1 ta ish qila oladi!**
    
    Sizning oshxona misolingizda Call Stack'da nima bo'ladi:
    
    1. `setTimeout(Tuxum)` → **"Timer o'rnat"** → Web API'ga beradi → **Qo'ldan ketdi**
    2. `setTimeout(Choy)` → **"Timer o'rnat"** → Web API'ga beradi → **Qo'ldan ketdi**
    3. `setTimeout(Dasturxon)` → **"Timer o'rnat"** → Web API'ga beradi → **Qo'ldan ketdi**
    4. `console.log("Ish boshlandi")` → **"Darhol yoz"** → **"Ish boshlandi"** → **Tugadi**
    
    **Call Stack endi bo'sh! Qo'llar bo'sh!**
    
    ### Web API = Avtomatik jihozlar
    
    - **Tuxum timer:** 10 daqiqa ishlaydi
    - **Choy timer:** 5 daqiqa ishlaydi
    - **Dasturxon timer:** 2 daqiqa ishlaydi
    
    **JavaScript kutmaydi! Boshqa ishlarni qila oladi!**
    
    ### Callback Queue = Tayyor ovqatlar stoli
    
    Timer tugaganda callback'lar **navbatga tushadi:**
    
    **2 daqiqa o'tdi:**
    
    `Callback Queue: ["Dasturxon tuzaldi"] ← Birinchi keldi`
    
    **5 daqiqa o'tdi:**
    
    `Callback Queue: ["Dasturxon tuzaldi", "Choy qaynadi"] ← Ikkinchi keldi`
    
    **10 daqiqa o'tdi:**
    
    `Callback Queue: ["Dasturxon tuzaldi", "Choy qaynadi", "Tuxum tayyor"] ← Uchinchi keldi`
    
    ### Event Loop = Bosh oshpaz
    
    **Doimiy tekshiradi:**
    
    `Event Loop: "Qo'llar bo'shmi?" → Call Stack'ga qaradi
     Event Loop: "Tayyor ovqat bormi?" → Callback Queue'ga qaradi
     Event Loop: "Bo'sh qo'llarga tayyor ovqat beraman!"`
    
    ## Xulosa:
    
    - **Call Stack** = Hozir qilayotgan ish (1 ta)
    - **Web API** = Kutilayotgan ishlar (ko'p ta)
    - **Callback Queue** = Tayyor bo'lgan ishlar navbati
    - **Event Loop** = Navbatdan Call Stack'ga o'tkazuvchi
    
    **Shunday qilib JavaScript 1 ta qo'l bilan ko'p ishlarni boshqaradi!**
    
    **Event Loop** aynan shu "boshqaruvchi" vazifasini bajaradi - tayyor bo'lgan ishlarni to'g'ri vaqtda, to'g'ri tartibda JavaScript'ning qo'liga beradi! 
    
- 5. Promise va async/await orasidagi farq nima?
    - **Promise** — bu **asinxron operatsiyaning natijasi** (muvaffaqiyat yoki xato) kelajakda tayyor bo‘lishini bildiradigan obyekt.
    - Ya’ni, “Vada”: **Hozir emas, keyin** natijani beraman.
    - Promise’ning **uchta holati** bor:
        1. **pending** — jarayon davom etmoqda (hali natija yo‘q).
        2. **fulfilled** — muvaffaqiyatli bajarildi (natija bor).
        3. **rejected** — xatolik bilan tugadi.
    - **async/await** → Promise’ni **o‘qishni osonlashtiradigan** shakar sintaksis.
    
    👉 Promise bilan kod chalkashroq chiqadi, async/await bilan silliqroq.
    
    ### Misol:
    
    ```jsx
    // Promise bilan
    function tuxumQaynat() {
      return new Promise(res => setTimeout(() => res("Tuxum tayyor"), 2000));
    }
    
    tuxumQaynat().then(result => console.log(result));
    
    // Async/await bilan
    async function ovqat() {
      let result = await tuxumQaynat();
      console.log(result);
    }
    ovqat();
    
    ```
    
    ✅ Ikki xil, lekin bir xil natija beradi.
    
- 6. Arrow function va regular function farqlari?
    1. **`this`** — Arrow function’da `this` tashqaridan olinadi, regular’da esa kim chaqirsa o‘sha bo‘ladi.
    2. **`arguments`** — Regular’da mavjud, arrow’da yo‘q.
    3. **Sintaksis** — Arrow qisqaroq.
    
    ### Misol:
    
    ```jsx
    let obj = {
      name: "Ali",
      regular: function() {
        console.log("Regular:", this.name);
      },
      arrow: () => {
        console.log("Arrow:", this.name);
      }
    };
    
    obj.regular(); // Regular: Ali
    obj.arrow();   // Arrow: undefined (global this’dan)
    
    ```
    
- 7 `this` keyword qanday ishlaydi?
    
    JavaScript’da `this` — bu **funksiya ichida kim chaqirganini ko‘rsatuvchi kalit so‘z**.
    
    - **Global scope’da** → `window` (browserda) yoki `global` (Node.js’da).
    - **Objekt ichida** → o‘sha obyektni bildiradi.
    - **Arrow function’da** → tashqi `this` ni oladi.
    - **`call`, `apply`, `bind`** yordamida majburan o‘zgartirish mumkin.
    
    ### Misol:
    
    ```jsx
    console.log(this); // Browserda: window
    
    let obj = {
      name: "Ali",
      salom() {
        console.log(this.name);
      }
    };
    
    obj.salom(); // "Ali"
    
    ```
    
- 8 **Destructuring** → array yoki object ichidan qiymatlarni “ajratib olish” usuli.
    - **Destructuring** — object yoki array ichidagi qiymatlarni **qisqa va qulay** ajratib olish usuli.
    - Katta obyekt yoki massivlar bilan ishlaganda **ko‘p yozishdan qutqaradi**.
    
    ### Object:
    
    ```jsx
    let person = {name: "Ali", age: 20};
    let {name, age} = person;
    console.log(name, age); // Ali 20
    
    ```
    
    ### Array:
    
    ```jsx
    let arr = [10, 20, 30];
    let [a, b, c] = arr;
    console.log(a, b, c); // 10 20 30
    
    ```
    
- 9 Spread operator va rest parameter farqi nima?
    - **Spread (`...`)** → array yoki object’ni yoyib yuboradi.
    - **Rest (`...`)** → bir nechta argumentlarni yig‘ib oladi.
    
    ### Misol:
    
    ```jsx
    // Spread
    let arr1 = [1,2,3];
    let arr2 = [...arr1, 4, 5];
    console.log(arr2); // [1,2,3,4,5]
    
    // Rest
    function sum(...numbers) {
      return numbers.reduce((a,b) => a+b, 0);
    }
    console.log(sum(1,2,3,4)); // 10
    
    ```
    
- 10  `map`, `filter`, `reduce` qanday ishlaydi?
    - **map** → har elementni o‘zgartiradi → yangi array beradi.
    - **filter** → faqat shartga mos elementlarni oladi.
    - **reduce** → bitta umumiy qiymatga qisqartiradi.
    
    ### Misol:
    
    ```jsx
    let arr = [1,2,3,4,5];
    
    // map
    let kvadrat = arr.map(x => x*x);
    console.log(kvadrat); // [1,4,9,16,25]
    
    // filter
    let juft = arr.filter(x => x % 2 === 0);
    console.log(juft); // [2,4]
    
    // reduce
    let yigindi = arr.reduce((a,b) => a+b, 0);
    console.log(yigindi); // 15
    
    ```
    
- 11 `setTimeout` va `setInterval` farqi nima?
    
    Bular **JavaScript timer funksiyalari** bo‘lib, **Web API** tomonidan taqdim etiladi (JSning o‘zi emas).
    
    - JS **bir oqimli (single-threaded)** bo‘lgani uchun, bu funksiyalar orqa fon (`Web API`)da ishlaydi va **Event Loop** orqali navbatga qo‘shiladi.
    - **setTimeout** → faqat **bir marta** bajaradi.
    - **setInterval** → belgilangan vaqtda **takror-takror** bajaradi.
    
    ### Misol:
    
    ```jsx
    setTimeout(() => console.log("Bir marta!"), 2000);
    
    setInterval(() => console.log("Har 2 sekundda!"), 2000);
    ```
    
- 12 Event bubbling va capturing nima?
    - **Bubbling** → event ichkaridan tashqariga ko‘tariladi (default).
    - **Capturing** → tashqaridan ichkariga tushadi.
    
    ### Misol:
    
    ```html
    <div id="parent">
      <button id="child">Click me</button>
    </div>
    
    <script>
    document.getElementById("parent").addEventListener("click", () => {
      console.log("Parent");
    }, true); // capturing
    
    document.getElementById("child").addEventListener("click", () => {
      console.log("Child");
    }); // bubbling
    </script>
    
    ```
    
    👉 `true` qo‘ysak capturing, qo‘ymasak bubbling ishlaydi.
    
- 13 `call`, `apply`, `bind` farqi nima?
    
    **`call`, `apply`, `bind`** – bu **JavaScript function methodlari**, ular orqali **`this`** kontekstini qo‘lda boshqaramiz va funksiyani chaqirish uslubini o‘zgartiramiz.
    
    ## 🧩 Qisqa jadval:
    
    | Method | Nima qiladi? | Farqi nima? |
    | --- | --- | --- |
    | **`call`** | Funksiyani **darhol** chaqiradi, `this`ni beramiz va **argumentlarni vergul bilan** uzatamiz. | Arg. vergul bilan |
    | **`apply`** | Funksiyani **darhol** chaqiradi, `this`ni beramiz va **argumentlarni massiv** sifatida uzatamiz. | Arg. massivda |
    | **`bind`** | Funksiyani **darhol chaqirmaydi**, yangi funksiya qaytaradi, `this` va argumentlarni eslab qoladi. | Keyinroq chaqiriladi |
    
    ---
    
    ## 🧩 Misol bilan tushuntirish
    
    ```jsx
    const person = {
      name: "Ali",
    };
    
    function greet(age, city) {
      console.log(`Salom, ${this.name}! Siz ${age} yoshdasiz va ${city}da yashaysiz.`);
    }
    ```
    
    ### 🔹 `call`
    
    ```jsx
    greet.call(person, 25, "Toshkent");
    // this = person
    // Argumentlar vergul bilan
    ```
    
    ⏩ Natija:
    
    ```
    Salom, Ali! Siz 25 yoshdasiz va Toshkentda yashaysiz.
    ```
    
    ---
    
    ### 🔹 `apply`
    
    ```jsx
    greet.apply(person, [25, "Toshkent"]);
    // this = person
    // Argumentlar massivda
    ```
    
    Natija xuddi shu:
    
    ```
    Salom, Ali! Siz 25 yoshdasiz va Toshkentda yashaysiz.
    ```
    
    ---
    
    ### 🔹 `bind`
    
    ```jsx
    const boundGreet = greet.bind(person, 25, "Toshkent");
    boundGreet(); // endi keyin chaqiramiz
    ```
    
    Natija:
    
    ```
    Salom, Ali! Siz 25 yoshdasiz va Toshkentda yashaysiz.
    ```
    
    ---
    
    📌 **Xotirada saqlash uchun super qisqa:**
    
    - `call` → chaqir (vergul)
    - `apply` → chaqir (massiv)
    - `bind` → bog‘la (keyin chaqir)
    
    JavaScript’da **`this` kim chaqirsa, o‘sha obyektni ko‘rsatadi.**
    
    Lekin ba’zan biz `this`ni **qo‘lda boshqarishimiz** yoki **funksiyani boshqa obyektga qarz berishimiz** kerak bo‘ladi.
    
    Mana shu vaziyatlarda `call`, `apply`, `bind` ishlatiladi.
    
    ---
    
    - 🔹 **call** → `this`ni qo‘lda berib, **darhol chaqirasan**.
    - 🔹 **apply** → xuddi shu, lekin argumentlar **massiv** bo‘ladi.
    - 🔹 **bind** → `this`ni qo‘lda berib, **keyin chaqirish uchun** yangi funksiya tayyorlaysan.
    
    ✅ **Kerakligi:**
    
    - `this`ni boshqarish
    - Funksiyani boshqa obyektga qarz berish
    - Argumentlarni tayyorlab qo‘yish (currying)
    - DOM eventlarda `this` yo‘qolmasligi uchun
    
    ---
    
    🔑 Qisqasi:
    
    > call, apply, bind = Funksiyani istagan obyekt kontekstida ishlatish va thisni boshqarish usullari.
    > 
- 14 `==` va `===` farqi nima?
    - **`==`** → qiymatni solishtiradi (tipni tekshirmaydi).
    - **`===`** → qiymat + tipni solishtiradi.
    
    ### Misol:
    
    ```jsx
    console.log(5 == "5");  // true
    console.log(5 === "5"); // false
    
    ```
    
    ✅ Har doim `===` ishlatish xavfsizroq.
    
- 15 Template literals nima va qanday ishlatiladi?
    
    **Template literals** — `` `` (backtick) bilan yoziladi.
    
    - Ichida `${}` bilan o‘zgaruvchilarni yozish mumkin.
    - Multi-line (ko‘p qatorli) qo‘llab-quvvatlaydi.
    
    ### Misol:
    
    ```jsx
    let ism = "Ali";
    let yosh = 20;
    
    console.log(`Salom, men ${ism}, yoshim ${yosh}`);
    
    // Multi-line
    console.log(`
    Qator 1
    Qator 2
    Qator 3
    `);
    
    ```
    
- 16 Object (obyekt) nima?
    
    **Object** — kalit-qiymat juftligi.
    
    👉 Xuddi lug‘atdek: so‘z = izoh.
    
    ### Misol:
    
    ```jsx
    let odam = {
      ism: "Ali",
      yosh: 20,
      salom: function() {
        console.log("Salom, mening ismim " + this.ism);
      }
    };
    
    console.log(odam.ism); // Ali
    odam.salom(); // Salom, mening ismim Ali
    
    ```
    
    ✅ `odam` obyektida `ism`, `yosh` — property, `salom` — method.
    
- 17 Class nima?
    
    **Class** — bu obyekt yaratish uchun **shablon (qolip)**.
    
    👉 Xuddi “pechene qolipi” kabi: qolip bitta, lekin undan ko‘p pechene yasash mumkin.
    
    ### Misol:
    
    ```jsx
    class Odam {
      constructor(ism, yosh) {
        this.ism = ism;
        this.yosh = yosh;
      }
    
      salom() {
        console.log(`Salom, men ${this.ism}, yoshim ${this.yosh}`);
      }
    }
    
    // Class’dan obyekt yaratamiz
    let ali = new Odam("Ali", 20);
    let vali = new Odam("Vali", 25);
    
    ali.salom();  // Salom, men Ali, yoshim 20
    vali.salom(); // Salom, men Vali, yoshim 25
    
    ```
    
    ✅ `class` → qolip, `object` → qolipdan chiqqan mahsulot.
    
- 18 OOP prinsiplari
    
    ### 🔹 Encapsulation (yashirish)
    
    Obyektning ichki qismini tashqaridan yashirish.
    
    ```jsx
    class Bank {
      #balans = 0; // private (faqat ichkaridan ko‘rinadi)
    
      deposit(summa) {
        this.#balans += summa;
      }
    
      getBalans() {
        return this.#balans;
      }
    }
    
    let acc = new Bank();
    acc.deposit(100);
    console.log(acc.getBalans()); // 100
    // console.log(acc.#balans); ❌ xato (private)
    
    ```
    
    ---
    
    ### 🔹 Inheritance (meros olish)
    
    Bitta class’dan boshqasini yaratish.
    
    ```jsx
    class Hayvon {
      yurish() {
        console.log("Men yurayapman...");
      }
    }
    
    class It extends Hayvon {
      vov() {
        console.log("Vov-vov!");
      }
    }
    
    let dog = new It();
    dog.yurish(); // Men yurayapman...
    dog.vov();    // Vov-vov!
    
    ```
    
    ---
    
    ### 🔹 Polymorphism (ko‘p shakllilik)
    
    Bir xil nomdagi method har xil ishlaydi.
    
    ```jsx
    class Hayvon {
      ovoz() {
        console.log("Noma’lum ovoz...");
      }
    }
    
    class It extends Hayvon {
      ovoz() {
        console.log("Vov-vov!");
      }
    }
    
    class Mushuk extends Hayvon {
      ovoz() {
        console.log("Miyov!");
      }
    }
    
    new It().ovoz();     // Vov-vov!
    new Mushuk().ovoz(); // Miyov!
    
    ```
    
    ---
    
    ### 🔹 Abstraction (faqat kerakli qismini ko‘rsatish)
    
    Murakkab narsalarni oddiy interfeys orqali ishlatish.
    
    👉 Masalan, telefon ichida juda murakkab kod bor, lekin biz faqat **“call” tugmasi** ni bosamiz.
    
- 19 Array nima?
    
    **Array** — tartiblangan ro‘yxat.
    
    👉 Odamlar ro‘yxati, raqamlar, mahsulotlar...
    
    ### Misol:
    
    ```jsx
    let sonlar = [10, 20, 30, 40];
    console.log(sonlar[0]); // 10
    console.log(sonlar.length); // 4
    
    ```
    
    ### Asosiy metodlar:
    
    ```jsx
    let arr = [1,2,3];
    
    // push - oxiriga qo‘shadi
    arr.push(4);
    console.log(arr); // [1,2,3,4]
    
    // pop - oxiridan o‘chiradi
    arr.pop();
    console.log(arr); // [1,2,3]
    
    // shift - boshidan o‘chiradi
    arr.shift();
    console.log(arr); // [2,3]
    
    // unshift - boshiga qo‘shadi
    arr.unshift(0);
    console.log(arr); // [0,2,3]
    
    // map - har bir elementni o‘zgartiradi
    let kvadrat = arr.map(x => x*x);
    console.log(kvadrat); // [0,4,9]
    
    ```
    

# JavaScript Interview Savollar 2-qism (10 ta)

- 1. Scope chain nima va qanday ishlaydi?
    
    **Scope chain** — bu o‘zgaruvchilarni qayerdan qidirishni ko‘rsatadigan tizim.
    
    👉 Agar funksiya ichida o‘zgaruvchi chaqirilsa, JavaScript avval **ichkaridan** qidiradi, topmasa **tashqariga** chiqadi. Oxirigacha chiqib ham topolmasa `ReferenceError` beradi.
    
    ### Misol:
    
    ```jsx
    let a = "Tashqi";
    
    function tashqi() {
      let b = "O‘rta";
    
      function ichki() {
        let c = "Ichki";
        console.log(a); // Tashqi scope’dan oldi
        console.log(b); // O‘rta scope’dan oldi
        console.log(c); // Ichki scope’dan oldi
      }
    
      ichki();
    }
    
    tashqi();
    ```
    
    ✅ Demak scope chain — bu “ichkaridan tashqariga qarab qidirish”.
    

---

- 2. `setTimeout(fn, 0)` nima uchun darhol ishlamaydi?
    
    `setTimeout(fn, 0)` desak ham **darhol ishlamaydi**. Sababi:
    
    - JavaScript avval **Call Stack** dagi ishlarni tugatadi
    - Keyin **Callback Queue** dagi funksiyalarni ishlatadi
    
    Shuning uchun `0 ms` bo‘lsa ham navbat kutadi.
    
    ### Misol:
    
    ```jsx
    console.log("1");
    setTimeout(() => console.log("2"), 0);
    console.log("3");
    
    // Natija:
    // 1
    // 3
    // 2
    
    ```
    

---

- 3. Pure function nima? Misol keltiring.
    
    **Pure function** — bu **faqatgina o‘z argumentlariga bog‘liq** bo‘lgan va **hech qanday yon ta’sir qilmaydigan** funksiya.
    
    👉 Ya’ni: tashqi o‘zgaruvchini o‘zgartirmaydi, faqat kirgan qiymat → chiqqan qiymat.
    
    ### Misol:
    
    ```jsx
    // Pure function
    function qo‘sh(x, y) {
      return x + y;
    }
    
    console.log(qo‘sh(2, 3)); // 5
    console.log(qo‘sh(2, 3)); // 5 (har doim bir xil)
    
    ```
    
    **Not pure function:**
    
    ```jsx
    let count = 0;
    function oshir() {
      count++;
      return count;
    }
    
    console.log(oshir()); // 1
    console.log(oshir()); // 2 (har safar natija o‘zgaradi)
    
    ```
    
    ---
    
- 4. Immutability nima va nima uchun muhim?
    
    **Immutability** — bu ma’lumotni **o‘zgartirmaslik**, balki **yangi nusxa yaratish** degani.
    
    👉 Bu juda muhim, chunki **bug‘larni kamaytiradi**, dastur barqaror bo‘ladi.
    
    ### Misol:
    
    ```jsx
    // O‘zgartirish (mutable)
    let arr1 = [1, 2, 3];
    arr1.push(4);
    console.log(arr1); // [1,2,3,4]
    
    // Immutability (immutable)
    let arr2 = [1, 2, 3];
    let newArr = [...arr2, 4];
    console.log(arr2);   // [1,2,3] (eski o‘zgarmagan)
    console.log(newArr); // [1,2,3,4]
    ```
    

---

- 5. `null` va `undefined` farqi nima?
    - `undefined` → o‘zgaruvchi **yaratilgan**, lekin **qiymat berilmagan**.
    - `null` → o‘zgaruvchi **atayin bo‘sh qiymat** qilingan.
    
    ### Misol:
    
    ```jsx
    let a;
    console.log(a); // undefined
    
    let b = null;
    console.log(b); // null
    
    ```
    

---

- 6. Prototype inheritance qanday ishlaydi?
    
    JavaScript’da obyektlar **inheritance** (meros olish) ni **prototype** orqali qiladi.
    
    👉 Ya’ni: agar obyekt ichida xususiyat topilmasa, **prototypeda qidiradi**.
    
    ### Misol:
    
    ```jsx
    function Person(name) {
      this.name = name;
    }
    
    Person.prototype.salom = function() {
      console.log("Salom, men " + this.name);
    };
    
    let ali = new Person("Ali");
    ali.salom(); // "Salom, men Ali"
    
    ```
    
    ✅ `salom()` aslida `ali` ichida yo‘q, lekin `prototype` dan topiladi.
    

---

- 7. `for...in` va `for...of` orasidagi farq nima?
    - `for...in` → **objektning kalitlarini** aylanadi
    - `for...of` → **iterable (array, string...) qiymatlarni** aylanadi
    
    ### Misol:
    
    ```jsx
    let obj = {a: 1, b: 2};
    for (let key in obj) {
      console.log(key); // a, b
    }
    
    let arr = [10, 20, 30];
    for (let val of arr) {
      console.log(val); // 10, 20, 30
    }
    
    ```
    

---

- 8. Shallow copy va deep copy farqi nima?
    - **Shallow copy** → faqat **birinchi qatlam** ko‘chadi
    - **Deep copy** → hamma **ichki obyektlar ham** ko‘chadi
    
    ### Misol:
    
    ```jsx
    let obj = {name: "Ali", info: {age: 20}};
    
    // Shallow copy
    let copy1 = {...obj};
    copy1.info.age = 25;
    console.log(obj.info.age); // 25 (asosiy obyekt ham o‘zgardi!)
    
    // Deep copy (JSON usuli bilan)
    let copy2 = JSON.parse(JSON.stringify(obj));
    copy2.info.age = 30;
    console.log(obj.info.age); // 25 (asosiy obyekt o‘zgarmadi)
    
    ```
    

---

- 9. Currying nima? Misol bilan tushuntiring.
    
    **Currying** — funksiya ko‘p argument o‘rniga **bitta-bittadan** qabul qiladi.
    
    👉 Juda ko‘p ishlatiladi: qayta foydalanish uchun.
    
    ### Misol:
    
    ```jsx
    function sum(a) {
      return function(b) {
        return function(c) {
          return a + b + c;
        };
      };
    }
    
    console.log(sum(2)(3)(4)); // 9
    
    ```
    
    ✅ Buni arrow function bilan ham yozsa bo‘ladi.
    

---

- 10. `Array.from()` va `Array.of()` farqi nima?
    - **`Array.from()`** → iterable (masalan string, Set, arguments) ni arrayga aylantiradi.
    - **`Array.of()`** → berilgan qiymatlarni arrayga yig‘adi.
    
    ### Misol:
    
    ```jsx
    // Array.from
    console.log(Array.from("salom"));
    // ["s","a","l","o","m"]
    
    // Array.of
    console.log(Array.of(1,2,3));
    // [1,2,3]
    ```