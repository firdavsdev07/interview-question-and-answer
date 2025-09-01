# React Interview Savollar

- 1 Virtual DOM nima va nima uchun ishlatiladi?
    
    👉 Oddiy DOM bilan ishlash sekin, chunki har safar butun sahifa yangilanadi.
    
    👉 React esa **Virtual DOM** (ya’ni DOM’ning xotiradagi nusxasi)ni ishlatadi.
    
    ⚙️ Jarayon:
    
    1. O‘zgarishlar avval Virtual DOM’da hisoblanadi.
    2. React "oldingi Virtual DOM" va "yangi Virtual DOM"ni taqqoslaydi (diffing).
    3. Faqat o‘zgargan qismini haqiqiy DOM’ga qo‘yadi.
    
    ### Misol:
    
    Agar 1000 ta `<li>` bo‘lsa va faqat 1 tasi o‘zgarsa:
    
    - Oddiy DOM: butun `<ul>`ni qayta chizadi.
    - Virtual DOM: faqat o‘sha 1 `<li>`ni yangilaydi.
- 2 useState hook qanday ishlaydi?
    
    👉 State — componentning ichki holati.
    
    👉 `useState` — state yaratish va uni yangilash uchun hook.
    
    U ikkita narsani qaytaradi: `[state, setState]`.
    
    ### Kod:
    
    ```jsx
    import { useState } from "react";
    
    function Counter() {
      const [count, setCount] = useState(0);
    
      return (
        <div>
          <h2>Hisob: {count}</h2>
          <button onClick={() => setCount(count + 1)}>➕</button>
          <button onClick={() => setCount(count - 1)}>➖</button>
        </div>
      );
    }
    ```
    
    📌 Hayotiy misol: Xuddi **kalkulyator** yoki **savatcha soni** kabi — bosgan sari o‘zgaradi.
    
- 3 useEffect hook nima va qachon ishlatiladi?
    
    👉 Yon ta’sir (side effect)larni bajaradi:
    
    - API’dan data olish
    - Event listener qo‘shish
    - `setTimeout`, `setInterval`
    
    ### Kod:
    
    ```jsx
    import { useEffect, useState } from "react";
    
    function Users() {
      const [users, setUsers] = useState([]);
    
      useEffect(() => {
        fetch("https://jsonplaceholder.typicode.com/users")
          .then(res => res.json())
          .then(data => setUsers(data));
      }, []); // [] => faqat 1 marta bajariladi
    
      return <ul>{users.map(u => <li key={u.id}>{u.name}</li>)}</ul>;
    }
    
    ```
    
    📌 Hayotiy misol: Oshxonada ovqat pishirish → gazni yoqasiz (render), lekin **qozonni kuzatish** (side effect) `useEffect` bilan bo‘ladi.
    
- 4 Props va state orasidagi farq nima?
    - **Props** — tashqaridan componentga beriladi (o‘zgarmaydi).
    - **State** — component ichida saqlanadi va o‘zgaradi.
    
    ### Kod:
    
    ```jsx
    function Salom({ ism }) { // props
      return <h1>Salom, {ism}!</h1>;
    }
    
    function App() {
      const [name, setName] = useState("Ali"); // state
      return <Salom ism={name} />;
    }
    ```
    
    📌 Misol:
    
    - Props = ota-onangiz sizga ism qo‘yib beradi (siz o‘zgartira olmaysiz).
    - State = sizning kayfiyatingiz (o‘zgaradi).
- 5 Component lifecycle metodlari qaysilar?
    
    👉 Class componentlarda:
    
    - **Mounting**: `constructor`, `componentDidMount`
    - **Updating**: `componentDidUpdate`
    - **Unmounting**: `componentWillUnmount`
    
    👉 Function componentlarda esa barchasi `useEffect` orqali qilinadi.
    
    ### Kod:
    
    ```jsx
    useEffect(() => {
      console.log("Component mount bo‘ldi");
    
      return () => {
        console.log("Component unmount bo‘ldi");
      };
    }, []);
    
    ```
    
    📌 Misol: Xuddi uy qurilishi jarayoni: qurish (mount), ta’mirlash (update), buzish (unmount).
    
- 6 Controlled va uncontrolled components farqi nima?
    
    ### Controlled (state orqali boshqariladi):
    
    Bu — React’da **form elementining qiymati** (masalan, `input`, `textarea`, `select`) **React state orqali boshqariladigan** holat.
    
    - Ya’ni, qiymat DOM ichida emas, balki **React state** ichida saqlanadi.
    - Har safar foydalanuvchi biror narsa yozsa → React state yangilanadi → input qiymati shu state’dan qayta o‘qiladi.
    
    ➡️ Oddiy qilib aytganda: **React komponenti inputning xo‘jayini bo‘ladi.**
    
    ```jsx
    const [value, setValue] = useState("");
    <input value={value} onChange={e => setValue(e.target.value)} />;
    ```
    
    ### Uncontrolled (DOM orqali boshqariladi):
    
    ### 🔹 Uncontrolled Component (boshqarilmaydigan komponent)
    
    Bu — **form elementining qiymati DOM ichida saqlanadigan** holat.
    
    - React state’dan foydalanmaydi, input o‘zining “ichki qiymatini” o‘zi boshqaradi.
    - Qiymatni olish uchun `ref` orqali DOM’dan o‘qib olish kerak bo‘ladi.
    
    ➡️ Oddiy qilib aytganda: **input o‘zining xo‘jayini, React esa faqat kuzatuvchi.**
    
    ```jsx
    const inputRef = useRef();
    
    <input ref={inputRef} />
    <button onClick={() => alert(inputRef.current.value)}>Ko‘rsat</button>
    ```
    
    📌 Misol:
    
    - Controlled = sizning daftarni siz yozib borasiz (hammasi nazorat ostida).
    - Uncontrolled = o‘qituvchi daftarini sizdan so‘rab ko‘radi (siz nazorat qilmaysiz).
    
    ### 📝 Xulosa
    
    - **Controlled** → React orqali boshqariladi, hamma narsa state’da.
    - **Uncontrolled** → DOM o‘zi boshqaradi, React faqat kerak bo‘lsa qiymatini olib beradi.
- 7 useContext hook nima uchun ishlatiladi?
    
    `useContext` bizga **prop drilling** muammosini hal qilishda yordam beradi.
    
    **Prop drilling** – ota komponentdan bola komponentga **har doim props yuborish kerakligi**. Bu ko‘p qatlam bo‘lsa, bosh og‘riq.
    
    `useContext` esa – **"hamma joydan olish mumkin bo‘lgan umumiy ombor"**.
    
    📌 Misol:
    
    ```jsx
    import React, { createContext, useContext } from "react";
    
    const UserContext = createContext();
    
    function App() {
      return (
        <UserContext.Provider value="Javohir">
          <Profile />
        </UserContext.Provider>
      );
    }
    
    function Profile() {
      return <UserInfo />;
    }
    
    function UserInfo() {
      const user = useContext(UserContext); 
      return <h1>Salom, {user}!</h1>; // props berib o'tirmaymiz
    }
    ```
    
    👉 Ko‘rdingizmi, `App` → `Profile` → `UserInfo` bo‘lsa ham, props yubormadik. `UserContext` orqali istalgan joydan foydalanyapmiz.
    
- 8 Key prop nima uchun muhim?
    
    👉 `key` – React'ga **qaysi element o‘zgargan, qaysi biri o‘sha-o‘sha** ekanini aytib turadigan belgi.
    
    Agar `key` bo‘lmasa, React **butun ro‘yxatni qayta chizadi** → bu sekin va noto‘g‘ri ishlashi mumkin.
    
    📌 Misol:
    
    ```jsx
    const fruits = ["Olma", "Banan", "Uzum"];
    
    function FruitList() {
      return (
        <ul>
          {fruits.map((fruit, index) => (
            <li key={index}>{fruit}</li>
          ))}
        </ul>
      );
    }
    ```
    
    👉 `key={index}` yoki `id` ishlatamiz. Shunda React biladi: "Ha, bu element avvalgisi, yangisini chizma, faqat o‘zgarganini yangila".
    
- 9 React.memo nima va qachon ishlatiladi?
    
    `React.memo` komponentni **faqat kerak bo‘lganda qayta chizish** uchun ishlatiladi.
    
    Oddiy qilib aytganda: **agar props o‘zgarmasa → komponentni qayta chizma!**
    
    📌 Misol:
    
    ```jsx
    import React from "react";
    
    const Child = React.memo(({ name }) => {
      console.log("Child render bo‘ldi");
      return <h2>Salom, {name}</h2>;
    });
    
    function App() {
      const [count, setCount] = React.useState(0);
      return (
        <>
          <Child name="Javohir" />
          <button onClick={() => setCount(count + 1)}>+ {count}</button>
        </>
      );
    }
    ```
    
    👉 Agar React.memo bo‘lmasa, har safar tugma bosilganda Child qayta render bo‘ladi. Ammo memo bo‘lsa, **faqat `props` o‘zgarsa**gina qayta render qiladi.
    
- 10 Custom hook qanday yaratiladi?
    
    👉 Custom hook – bu **hooklarni qayta foydalanish uchun o‘zingiz yozgan funksiya**.
    
    📌 Misol: `useWindowWidth` hook
    
    ```jsx
    import { useState, useEffect } from "react";
    
    function useWindowWidth() {
      const [width, setWidth] = useState(window.innerWidth);
    
      useEffect(() => {
        function handleResize() {
          setWidth(window.innerWidth);
        }
        window.addEventListener("resize", handleResize);
        return () => window.removeEventListener("resize", handleResize);
      }, []);
    
      return width;
    }
    
    function App() {
      const width = useWindowWidth();
      return <h1>Oynaning eni: {width}px</h1>;
    }
    ```
    
    👉 Shunaqa qilib `useWindowWidth` ni istalgan joyda ishlatish mumkin.
    
- 11 useCallback va useMemo farqi nima?
    - **`useCallback`** → funksiyani **eslab qoladi**, qayta yaratmaydi.
    - **`useMemo`** → hisoblangan **natijani eslab qoladi**, qayta hisoblamaydi.
    
    📌 Misol:
    
    ```jsx
    import React, { useState, useCallback, useMemo } from "react";
    
    function App() {
      const [count, setCount] = useState(0);
    
      // useCallback -> funksiyani qayta yaratmaslik uchun
      const logCount = useCallback(() => {
        console.log("Count:", count);
      }, [count]);
    
      // useMemo -> hisoblangan natijani qayta ishlatish uchun
      const double = useMemo(() => {
        console.log("Hisoblanmoqda...");
        return count * 2;
      }, [count]);
    
      return (
        <>
          <h1>{count} | Double: {double}</h1>
          <button onClick={() => setCount(count + 1)}>+</button>
          <button onClick={logCount}>Log Count</button>
        </>
      );
    }
    
    ```
    
    👉 Oddiy qilib:
    
    - `useCallback` → funksiyani saqlab qolish.
    - `useMemo` → qiymatni saqlab qolish.
- 12 Lifting state up nima degani?
    
    👉 **State ni pastdagi bolalardan olib, yuqoriga ko‘tarish** – shunda boshqa bolalar ham ishlata oladi.
    
    📌 Misol:
    
    ```jsx
    function App() {
      const [value, setValue] = React.useState("");
    
      return (
        <>
          <Input value={value} setValue={setValue} />
          <Display value={value} />
        </>
      );
    }
    
    function Input({ value, setValue }) {
      return <input value={value} onChange={(e) => setValue(e.target.value)} />;
    }
    
    function Display({ value }) {
      return <h2>Kiritilgan: {value}</h2>;
    }
    ```
    
    👉 Agar stateni har bir komponentda alohida saqlasak, ular **bir-birini bilmaydi** . Shu sabab "state"ni ota komponentga ko‘tarib qo‘yamiz → **hammasi bitta joydan boshqariladi**
    

# React Interview Savollar 2-qism (10 ta)

- 1 React.StrictMode nima va nima uchun ishlatiladi ?
    
    👉 `React.StrictMode` – bu faqat **development vaqtida** ishlaydigan "tekshiruvchi".
    
    - Potensial xatolarni ko‘rsatadi.
    - Masalan, ikki marta `useEffect`ni chaqirishi mumkin (faqat dev modeda).
    
    📌 Misol:
    
    ```jsx
    <React.StrictMode>
      <App />
    </React.StrictMode>
    ```
    
    👉 Production’da ishlamaydi, faqat ogohlantirish uchun.
    
- 2 Class component vs Function component
    
    ### **Class Component**
    
    - Oldin React’da komponent yozish uchun ko‘proq ishlatilgan.
    - `class` yoziladi, `render()` metodi bo‘ladi, `this.state` va `this.setState` ishlatiladi.
    
    📌 Misol:
    
    ```jsx
    import React, { Component } from "react";
    
    class Counter extends Component {
      state = { count: 0 };
    
      increment = () => {
        this.setState({ count: this.state.count + 1 });
      };
    
      render() {
        return (
          <div>
            <h1>{this.state.count}</h1>
            <button onClick={this.increment}>+</button>
          </div>
        );
      }
    }
    ```
    
    ### **Function Component**
    
    - Hozirgi kunda **hooklar bilan ishlash uchun asosiy usul**.
    - `function` orqali yoziladi, `useState`, `useEffect` kabi hooklar ishlatiladi.
    
    📌 Misol:
    
    ```jsx
    import React, { useState } from "react";
    
    function Counter() {
      const [count, setCount] = useState(0);
    
      return (
        <div>
          <h1>{count}</h1>
          <button onClick={() => setCount(count + 1)}>+</button>
        </div>
      );
    }
    ```
    
    👉 Hozirgi zamonaviy usul – **function + hooklar**. Class komponentlar deyarli ishlatilmaydi.
    
- 3 Hook nima ?
    
    👉 **Hook** – bu function komponentlarga qo‘shimcha imkoniyat beradigan funksiya.
    
    Masalan: `useState`, `useEffect`, `useContext` va hokazo.
    
    - Classda bo‘lgan `state`, `lifecycle` metodlarini functionda ishlatish imkonini beradi.
- 4 Error boundaries nima va qanday ishlaydi ?
    
    👉 React’da **JS error chiqqanda butun UI yiqilib ketmasligi** uchun ishlatiladi.
    
    Faqat **class component** orqali yoziladi.
    
    📌 Misol:
    
    ```jsx
    class ErrorBoundary extends React.Component {
      state = { hasError: false };
    
      static getDerivedStateFromError() {
        return { hasError: true };
      }
    
      render() {
        if (this.state.hasError) {
          return <h1>Nimadir xato ketdi...</h1>;
        }
        return this.props.children;
      }
    }
    
    // Foydalanish:
    <ErrorBoundary>
      <SomeComponent />
    </ErrorBoundary>
    ```
    
    👉 Agar `SomeComponent` ichida error bo‘lsa, UI butunlay yiqilmaydi, "xato" xabari chiqadi.
    
- 5 React.lazy va Suspense qanday ishlatiladi ?
    
    👉 Kodni **chunk**larga bo‘lib yuklash uchun ishlatiladi (lazy loading).
    
    📌 Misol:
    
    ```jsx
    import React, { Suspense, lazy } from "react";
    
    const About = lazy(() => import("./About"));
    
    function App() {
      return (
        <Suspense fallback={<h2>Yuklanmoqda...</h2>}>
          <About />
        </Suspense>
      );
    }
    ```
    
    👉 `About` komponenti faqat kerak bo‘lganda yuklanadi.
    
- 6 useRef hook qanday ishlatiladi va nima uchun kerak ?
    
    👉 `useRef` – DOM element yoki qiymatni **saqlash uchun** ishlatiladi.
    
    - `state`dan farqi → o‘zgarganda **rerender qilmaydi**.
    
    📌 Misol: **inputga fokus qo‘yish**
    
    ```jsx
    import { useRef } from "react";
    
    function App() {
      const inputRef = useRef();
    
      const focusInput = () => {
        inputRef.current.focus();
      };
    
      return (
        <>
          <input ref={inputRef} />
          <button onClick={focusInput}>Fokus</button>
        </>
      );
    }
    ```
    
- 7 Synthetic events nima ?
    
    👉 React’dagi eventlar – bu **JavaScript native event’ining o‘rab qo‘yilgan versiyasi**.
    
    Masalan: `onClick`, `onChange`.
    
    - **Cross-browser** ishlashini ta’minlaydi.
    
    📌 Misol:
    
    ```jsx
    <button onClick={(e) => console.log(e.type)}>Click</button>
    ```
    
    👉 React **ikkita render qilmaydi**, bitta qilib optimallashtiradi.
    
- 8 State batching nima degani ?
    
    👉 Bir nechta `setState` larni **bitta render**da bajarish
    
- 9 Portals nima va qachon ishlatiladi ?
    
    👉 React elementni **DOMning boshqa joyiga chiqarish** uchun ishlatiladi.
    
    Masalan: modal oynani `root`dan tashqarida chiqarish.
    
    📌 Misol:
    
    ```jsx
    import ReactDOM from "react-dom";
    
    function Modal({ children }) {
      return ReactDOM.createPortal(
        <div className="modal">{children}</div>,
        document.getElementById("modal-root")
      );
    }
    ```
    
- 10 useReducer hook qachon ishlatiladi ?
    
    👉 `useState`ning "kattaroq versiyasi".
    
    - Ko‘p logika kerak bo‘lsa, reducer yozib boshqariladi.
    
    ```jsx
    import { useReducer } from "react";
    
    function reducer(state, action) {
      switch (action.type) {
        case "plus":
          return { count: state.count + 1 };
        default:
          return state;
      }
    }
    
    function App() {
      const [state, dispatch] = useReducer(reducer, { count: 0 });
    
      return (
        <>
          <h1>{state.count}</h1>
          <button onClick={() => dispatch({ type: "plus" })}>+</button>
        </>
      );
    }
    ```
    
- 12 React.Fragment nima uchun kerak ?
    
    👉 Bir nechta elementni **ortiqcha div**siz qaytarish uchun ishlatiladi.
    
    📌 Misol:
    
    ```jsx
    return (
      <><h1>Salom</h1>
        <p>React</p>
      </>
    );
    ```
    
    👉 Agar `div` qo‘ysak, keraksiz DOM ko‘payadi.