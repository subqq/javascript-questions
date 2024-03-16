# Список (просунутих) питань з JavaScript

Я публікую щодня завдання з JavaScript в моєму [Instagram](https://www.instagram.com/theavocoder), які також додаю тут!

Від базового до просунутого: перевірте, наскільки добре ви знаєте JavaScript, трохи оновіть свої знання або підготуйтеся до інтерв'ю! :muscle: :rocket: Щотижня я доповнюю цей репозиторій новими питаннями.

Відповіді знаходяться в згорнутій секції нижче питань. Просто натисни на відповідь, щоб розгорнути. Успіхів! :heart:

- [🇸🇦 العربية](../ar-AR/README_AR.md)
- [🇪🇬 اللغة العامية](../ar-EG/README_ar-EG.md)
- [🇧🇦 Bosanski](../bs-BS/README-bs_BS.md)
- [🇩🇪 Deutsch](../de-DE/README.md)
- [🇬🇧 English](../README.md)
- [🇪🇸 Español](../es-ES/README-ES.md)
- [🇫🇷 Français](../fr-FR/README_fr-FR.md)
- [🇮🇩 Indonesia](../id-ID/README.md)
- [🇮🇹 Italiano](../it-IT/README.md)
- [🇯🇵 日本語](../ja-JA/README-ja_JA.md)
- [🇰🇷 한국어](../ko-KR/README-ko_KR.md)
- [🇳🇱 Nederlands](../nl-NL/README.md)
- [🇵🇱 Polski](../pl-PL/README.md)
- [🇧🇷 Português Brasil](../pt-BR/README_pt_BR.md)
- [🇷o Română](../ro-RO/README.ro.md)
- [🇷🇺 Русский](../ru-RU/README.md)
- [🇽🇰 Shqip](../sq-KS/README_sq_KS.md)
- [🇹🇭 ไทย](../th-TH/README-th_TH.md)
- [🇹🇷 Türkçe](../tr-TR/README-tr_TR.md)
- [🇻🇳 Tiếng Việt](../vi-VI/README-vi.md)
- [🇨🇳 简体中文](../zh-CN/README-zh_CN.md)
- [🇹🇼 繁體中文](../zh-TW/README_zh-TW.md)

---

###### 1. Що буде в консолі?

```javascript
function sayHi() {
  console.log(name);
  console.log(age);
  var name = "Lydia";
  let age = 21;
}

sayHi();
```

- A: `Lydia` та `undefined`
- B: `Lydia` та `ReferenceError`
- C: `ReferenceError` та `21`
- D: `undefined` та `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

Всередині функції ми спершу визначаємо змінну `name` за допомогою ключового слова `var`. Це означає, що змінна буде знайдена (область пам'яті під змінну буде виділена під час створення) зі значенням `undefined` за замовчуванням, до тих пір поки виконання коду не дійде до рядка, де визначається змінна. Ми ще не визначили значення `name`, коли намагаємося вивести її в консоль, тому в консолі буде `undefined`.

Змінні, визначені за допомогою `let` (і `const`), також знаходяться, але на відміну від `var`, не <i>створюються</i>. Доступ до них неможливий до тих пір, поки не виконається рядок їх визначення (ініціалізації). Це називається "тимчасова мертва зона". Коли ми намагаємося звернутися до змінних до того моменту як вони визначені, JavaScript видає `ReferenceError`.

</p>
</details>

---

###### 2. Що буде в консолі?

```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}

for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}
```

- A: `0 1 2` та `0 1 2`
- B: `0 1 2` та `3 3 3`
- C: `3 3 3` та `0 1 2`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Через черги подій в JavaScript, функція `setTimeout` викликається _після того_ як цикл буде завершено. Так як змінна `i` в першому циклі була визначена за допомогою `var`, вона буде глобальною. У циклі ми кожен раз збільшуємо значення `i` на `1`, використовуючи унарний оператор `++.` До моменту виконання функції `setTimeout` значення `i` дорівнюватиме `3`, як показано в першому прикладі.

У другому циклі змінна `i` визначена за допомогою `let`. Такі змінні (а також `const`) мають блокову область видимості (блок це що завгодно між `{}`). З кожною ітерацією `i` матиме нове значення, і кожне значення буде замкнуто у своїй області видимості всередині циклу.

</p>
</details>

---

###### 3. Що буде в консолі?

```javascript
const shape = {
  radius: 10,
  diameter() {
    return this.radius * 2;
  },
  perimeter: () => 2 * Math.PI * this.radius
};

shape.diameter();
shape.perimeter();
```

- A: `20` та `62.83185307179586`
- B: `20` та `NaN`
- C: `20` та `63`
- D: `NaN` та `63`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Зауваж, що `diameter` це звичайна функція, в той час як `perimeter` це стрілкова функція.

У стрілкових функцій значення `this` вказує на навколишню область видимості, на відміну від звичайних функцій! Це означає, що при виклику `perimeter` значення `this` у цій функції вказує не на об'єкт `shape`, а на зовнішню область видимості (наприклад, window).

У цього об'єкта немає ключа `radius`, тому повертається `undefined`.

</p>
</details>

---

###### 4. Що буде в консолі?

```javascript
+true;
!"Lydia";
```

- A: `1` та `false`
- B: `false` та `NaN`
- C: `false` та `false`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Унарний плюс призводить операнд до числа. `true` це `1`, а `false` це `0`.

Строка `'Lydia'` це "справжнє" значення. Ми запитуємо "справжнє значення є помилковим"? Відповідь: `false`.

</p>
</details>

---

###### 5. Що з цього не є коректним?

```javascript
const bird = {
  size: "small"
};

const mouse = {
  name: "Mickey",
  small: true
};
```

- A: `mouse.bird.size` не є коректно
- B: `mouse[bird.size]` не є коректно
- C: `mouse[bird["size"]]` не є коректно
- D: Все варіант коректні

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

В JavaScript все ключі об'єкта є рядками (крім `Symbol`). І хоча ми не _набираємо_ їх як рядки, вони завжди перетворюються до рядків під капотом.

JavaScript інтерпретує (або розпаковує) оператори. При використанні квадратних дужок JS зауважує `[` і продовжує поки не зустріне `]`. Тільки після цього він вирахує то, що знаходиться всередині дужок.

`mouse[bird.size]`: Спершу визначається `bird.size`, що дорівнює `"small"`. `mouse["small"]` повертає `true`.

Але із записом через крапку так не відбувається. У `mouse` немає ключа `bird`. Таким чином, `mouse.bird` дорівнює `undefined`. Потім ми запитуємо ключ `size`, використовуючи крапкову нотацію: `mouse.bird.size`. Так як `mouse.bird` це `undefined`, ми запитуємо `undefined.size`. Це не є дійсним, тому ми отримуємо помилку типу: `Can not read property "size" of undefined`.

</p>
</details>

---

###### 6. Що буде в консолі?

```javascript
let c = { greeting: "Hey!" };
let d;

d = c;
c.greeting = "Hello";
console.log(d.greeting);
```

- A: `Hello`
- B: `Hey`
- C: `undefined`
- D: `ReferenceError`
- E: `TypeError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

В JavaScript всі об'єкти є _посилальними_ типами даних.

Спершу змінна `c` вказує на об'єкт. Потім ми вказуємо змінної `d` посилатися на той самий об'єкт, що і `c`.

<img src="https://i.imgur.com/ko5k0fs.png" width="200">

Коли ти змінюєш один об'єкт, то змінюються значення всіх посилань, що вказують на цей об'єкт.

</p>
</details>

---

###### 7. Що буде в консолі?

```javascript
let a = 3;
let b = new Number(3);
let c = 3;

console.log(a == b);
console.log(a === b);
console.log(b === c);
```

- A: `true` `false` `true`
- B: `false` `false` `true`
- C: `true` `false` `false`
- D: `false` `true` `true`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

`new Number()` це вбудований конструктор функції. І хоча він виглядає як число, це не справжнє число: у нього є ряд додаткових фіч і це об'єкт.

Оператор `==` призводить типи даних до якогось одного і перевіряє рівність _значень_. Обидва значення рівні `3`, тому повертається `true`.

При використанні оператора `===` значення і тип повинні бути однаковими. Але в нашому випадку це не так: `new Number()` це не число, це **об'єкт**. Тому обидва повертають `false`.

</p>
</details>

---

###### 8. Яким буде результат?

```javascript
class Chameleon {
  static colorChange(newColor) {
    this.newColor = newColor;
    return this.newColor;
  }

  constructor({ newColor = "green" } = {}) {
    this.newColor = newColor;
  }
}

const freddie = new Chameleon({ newColor: "purple" });
freddie.colorChange("orange");
```

- A: `orange`
- B: `purple`
- C: `green`
- D: `TypeError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

Функція `colorChange` є статичною. Статичні методи не мають доступу до екземплярів класу. Так як `freddie` це екземпляр, то статичний метод там не доступний. Тому результатом є помилка `TypeError`.

</p>
</details>

---

###### 9. Що буде в консолі?

```javascript
let greeting;
greetign = {}; // Typo!
console.log(greetign);
```

- A: `{}`
- B: `ReferenceError: greetign is not defined`
- C: `undefined`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

В консолі виведеться об'єкт, тому що ми щойно створили порожній об'єкт в глобальному об'єкті! Коли ми замість `greeting` написали `greetign`, інтерпретатор JS насправді виконав `global.greetign = {}` (або `window.greetign = {}` в браузері).

Потрібно використовувати `"use strict"`, щоб уникнути такої поведінки. Цей запис допоможе бути впевненим в тому, що змінна була визначена перед тим як їй присвоїли значення.

</p>
</details>

---

###### 10. Що станеться?

```javascript
function bark() {
  console.log("Woof!");
}

bark.animal = "dog";
```

- A: Нічого, все ок.
- B: `SyntaxError`. Не можна додавати властивості функцій таким способом.
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

В JavaScript це можливо, тому що функції це об'єкти! (Все є об'єктами крім примітивів).

Функція - це спеціальний тип об'єкта, який можна викликати. Крім того, функція - це об'єкт з властивостями. Властивість такого об'єкта не можна викликати, так як воно не є функцією.

</p>
</details>

---

###### 11. Що буде в консолі?

```javascript
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const member = new Person("Lydia", "Hallie");
Person.getFullName = function() {
  return `${this.firstName} ${this.lastName}`;
};

console.log(member.getFullName());
```

- A: `TypeError`
- B: `SyntaxError`
- C: `Lydia Hallie`
- D: `undefined` `undefined`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Не можна додавати властивості конструктору, як звичайному об'єкту. Якщо потрібно додати фічу до всіх об'єктів, то необхідно використовувати прототипи. В даному випадку,

```js
Person.prototype.getFullName = function() {
  return `${this.firstName} ${this.lastName}`;
};
```

зробить метод `member.getFullName()` чинним. У чому тут перевага? Припустимо, що ми додали цей метод до конструктора. Можливо, не кожному екземпляру `Person` потрібен цей метод. Це призведе до великих втрат пам'яті, тому що всі екземпляри будуть мати цю властивість. Навпаки, якщо ми додамо цей метод тільки до прототипу, у нас буде тільки одне місце в пам'яті, до якого зможуть звертатися всі екземпляри!

</p>
</details>

---

###### 12. Що буде в консолі?

```javascript
function Person(firstName, lastName) {
  this.firstName = firstName;
  this.lastName = lastName;
}

const lydia = new Person("Lydia", "Hallie");
const sarah = Person("Sarah", "Smith");

console.log(lydia);
console.log(sarah);
```

- A: `Person {firstName: "Lydia", lastName: "Hallie"}` та `undefined`
- B: `Person {firstName: "Lydia", lastName: "Hallie"}` та `Person {firstName: "Sarah", lastName: "Smith"}`
- C: `Person {firstName: "Lydia", lastName: "Hallie"}` та `{}`
- D:`Person {firstName: "Lydia", lastName: "Hallie"}` та `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Для `sarah` ми не використали ключове слово `new`. Використання `new` призводить до створення нового об'єкта. Але без `new` він вказує на **глобальний об'єкт**!

Ми вказали, що `this.firstName` дорівнює `"Sarah"` і `this.lastName` дорівнює `"Smith"`. Насправді ми визначили `global.firstName = 'Sarah'` і `global.lastName = 'Smith'`. `sarah` залишилася `undefined`.

</p>
</details>

---

###### 13. Назвіть три фази поширення подій

- A: Мета (Target) > Захоплення (Capturing) > Спливання (Bubbling)
- B: Спливання (Bubbling) > Мета (Target) > Захоплення (Capturing)
- C: Мета (Target) > Спливання (Bubbling) > Захоплення (Capturing)
- D: Захоплення (Capturing) > Мета (Target) > Спливання (Bubbling)

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

Під час фази **захоплення** подія поширюється від батьківського елемента до елемента мети. Після досягнення **мети** починається фаза **спливання**.

<img src="https://i.imgur.com/N18oRgd.png" width="200">

</p>
</details>

---

###### 14. Всі об'єкти мають прототипи?

- A: Так
- B: Ні

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Всі об'єкти мають прототипи, крім **базового об'єкта**. Базовий об'єкт має доступ до деяких методів і властивостей, таких як `.toString`. Саме тому ми можемо використовувати вбудовані методи JavaScript! Всі ці методи доступні в прототипі. Якщо JavaScript не може знайти метод безпосередньо у об'єкту, він продовжує пошук по ланцюжку прототипів поки не знайде.

</p>
</details>

---

###### 15. Результат коду?

```javascript
function sum(a, b) {
  return a + b;
}

sum(1, "2");
```

- A: `NaN`
- B: `TypeError`
- C: `"12"`
- D: `3`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

JavaScript це **динамічно типізована мова**: ми не визначаємо тип змінних. Змінні можуть автоматично бути перетворені з одного типу в інший без нашої участі, що називається _неявним приведенням типів_. **Приведення** це перетворення з одного типу в інший.

У цьому прикладі, JavaScript конвертувати число `1` в рядок, щоб операція всередині функції мала сенс і повернула значення. Під час складання числа (`1`) і рядки (`'2'`) число перетворюється до рядка. Ми можемо додавати рядки ось так: `"Hello" + "World"`. Таким чином, "`1"` + `"2"` повертає "`12"`.

</p>
</details>

---

###### 16. Що буде в консолі?

```javascript
let number = 0;
console.log(number++);
console.log(++number);
console.log(number);
```

- A: `1` `1` `2`
- B: `1` `2` `2`
- C: `0` `2` `2`
- D: `0` `1` `2`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

**Постфіксний** унарний оператор `++`:

1. Повертає значення (`0`)
2. Інкрементує значення (тепер число дорівнює `1`)

**Префіксний** унарний оператор `++`:

1. Інкрементує значення (тепер число дорівнює `2`)
2. Повертає значення (`2`)

Результат: `0 2 2`.

</p>
</details>

---

###### 17. Що буде в консолі?

```javascript
function getPersonInfo(one, two, three) {
  console.log(one);
  console.log(two);
  console.log(three);
}

const person = "Lydia";
const age = 21;

getPersonInfo`${person} is ${age} years old`;
```

- A: `"Lydia"` `21` `["", " is ", " years old"]`
- B: `["", " is ", " years old"]` `"Lydia"` `21`
- C: `"Lydia"` `["", " is ", " years old"]` `21`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

При використанні тегованих шаблонних літералів першим аргументом завжди буде масив строкових значень. Решта аргументів будуть значення мати переданих виразів!

</p>
</details>

---

###### 18. Що буде в консолі?

```javascript
function checkAge(data) {
  if (data === { age: 18 }) {
    console.log("You are an adult!");
  } else if (data == { age: 18 }) {
    console.log("You are still an adult.");
  } else {
    console.log(`Hmm.. You don't have an age I guess`);
  }
}

checkAge({ age: 18 });
```

- A: `You are an adult!`
- B: `You are still an adult.`
- C: `Hmm.. You don't have an age I guess`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

В операціях порівняння примітиви порівнюються за їх _значенням_, а об'єкти за _посиланнями_. JavaScript перевіряє, щоб об'єкти вказували на одну і ту ж область пам'яті.

Порівнювані об'єкти в нашому прикладі не такі: об'єкт, переданий як параметр, вказує на іншу область пам'яті, ніж об'єкти, що використовуються в порівнянні.

Тому `{age: 18} === {age: 18}` і `{age: 18} == {age: 18}` повертають `false`.

</p>
</details>

---

###### 19. Що буде в консолі?

```javascript
function getAge(...args) {
  console.log(typeof args);
}

getAge(21);
```

- A: `"number"`
- B: `"array"`
- C: `"object"`
- D: `"NaN"`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Оператор поширення (`... args`) повертає масив з аргументами. Масив це об'єкт, тому `typeof args` повертає `"object"`.

</p>
</details>

---

###### 20. Що буде в консолі?

```javascript
function getAge() {
  "use strict";
  age = 21;
  console.log(age);
}

getAge();
```

- A: `21`
- B: `undefined`
- C: `ReferenceError`
- D: `TypeError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Використовуючи `"use strict"`, можна бути впевненим, що ми помилково не оголосимо глобальні змінні. Ми раніше ніде не оголошували змінну `age`, тому з використанням `"use strict"` виникне ReferenceError. Без використання `"use strict"` помилки не виникне, а змінна `age` додасться в глобальний об'єкт.

</p>
</details>

---

###### 21. Чому дорівнюватиме sum?

```javascript
const sum = eval("10*10+5");
```

- A: `105`
- B: `"105"`
- C: `TypeError`
- D: `"10*10+5"`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

`eval` виконує код, переданий у вигляді рядка. Якщо це рядок (як в такому випадку), то обчислюється вираз. Вираз `10 * 10 + 5` поверне число `105`.

</p>
</details>

---

###### 22. Як довго буде доступний cool_secret?

```javascript
sessionStorage.setItem("cool_secret", 123);
```

- A: Завжди, дані не загубляться.
- B: Поки користувач не закриває вкладку.
- C: Поки користувач не закриє браузер, а не тільки вкладку.
- D: Поки користувач не вимикає комп'ютер.

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Дані, збережені в `sessionStorage` очищаються після закриття _вкладки_.

При використанні `localStorage` дані зберігаються назавжди. Очистити їх можна, наприклад, використовуючи `localStorage.clear()`.

</p>
</details>

---

###### 23. Що буде в консолі?

```javascript
var num = 8;
var num = 10;

console.log(num);
```

- A: `8`
- B: `10`
- C: `SyntaxError`
- D: `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

За допомогою ключового слова `var`, можна визначати скільки завгодно змінних з одним і тим же ім'ям. Змінна зберігатиме останнє присвоєне значення.

Ви не можете зробити це з `let` або` const`, оскільки вони блочні.

</p>
</details>

---

###### 24. Що буде в консолі?

```javascript
const obj = { 1: "a", 2: "b", 3: "c" };
const set = new Set([1, 2, 3, 4, 5]);

obj.hasOwnProperty("1");
obj.hasOwnProperty(1);
set.has("1");
set.has(1);
```

- A: `false` `true` `false` `true`
- B: `false` `true` `true` `true`
- C: `true` `true` `false` `true`
- D: `true` `true` `true` `true`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Всі ключі об'єктів (крім `Symbols`) є рядками, навіть якщо задано не в вигляді рядків. Тому `obj.hasOwnProperty('1')` так само повертає `true`.

Але це не працює для `set`. Значення `"1"` немає в `set`: `set.has ('1')`, тому повертається `false`. Але `set.has(1)` поверне `true`.

</p>
</details>

---

###### 25. Що буде в консолі?

```javascript
const obj = { a: "one", b: "two", a: "three" };
console.log(obj);
```

- A: `{ a: "one", b: "two" }`
- B: `{ b: "two", a: "three" }`
- C: `{ a: "three", b: "two" }`
- D: `SyntaxError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Якщо є два ключі з однаковим ім'ям, то ключ буде перезаписаний. Його позиція збережеться, але значенням буде встановлено останнім.

</p>
</details>

---

###### 26. Глобальний контекст виконання створює дві речі: глобальний об'єкт і this

- A: Так
- B: Ні
- C: В залежності від ситуації

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Базовий контекст виконання це глобальний контекст виконання: це те, що є де завгодно у твоєму коді.

</p>
</details>

---

###### 27. Що буде в консолі?

```javascript
for (let i = 1; i < 5; i++) {
  if (i === 3) continue;
  console.log(i);
}
```

- A: `1` `2`
- B: `1` `2` `3`
- C: `1` `2` `4`
- D: `1` `3` `4`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Оператор `continue` пропускає ітерацію, якщо умова повертає `true`.

</p>
</details>

---

###### 28. Яким буде результат?

```javascript
String.prototype.giveLydiaPizza = () => {
  return "Just give Lydia pizza already!";
};

const name = "Lydia";

console.log(name.giveLydiaPizza())
```

- A: `"Just give Lydia pizza already!"`
- B: `TypeError: not a function`
- C: `SyntaxError`
- D: `undefined`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

`String` це вбудований конструктор, до якого можна додавати властивості. Я додала метод до його прототипу. Рядки-примітиви автоматично конвертуються до рядків-об'єктів. Тому всі рядки (строкові об'єкти) мають доступ до цього методу!

</p>
</details>

---

###### 29. Що буде в консолі?

```javascript
const a = {};
const b = { key: "b" };
const c = { key: "c" };

a[b] = 123;
a[c] = 456;

console.log(a[b]);
```

- A: `123`
- B: `456`
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Ключі об'єкта автоматично конвертуються в рядки. Ми збираємося додати об'єкт в якості ключа до об'єкта `a` зі значенням `123`.

Проте, коли ми наводимо об'єкт до рядка, він стає `"[object Object]"`. Таким чином, ми говоримо, що `a["object Object"] = 123`. Потім ми робимо те ж саме. `c` це інший об'єкт, який ми неявно наводимо до рядка. Тому `a["object Object"] = 456`.

Потім, коли ми виводимо `a[b]`, ми маємо на увазі `a["object Object"]`. Ми тільки що встановили туди значення `456`, тому в результаті отримуємо `456`.

</p>
</details>

---

###### 30. Яким буде результат?

```javascript
const foo = () => console.log("First");
const bar = () => setTimeout(() => console.log("Second"));
const baz = () => console.log("Third");

bar();
foo();
baz();
```

- A: `First` `Second` `Third`
- B: `First` `Third` `Second`
- C: `Second` `First` `Third`
- D: `Second` `Third` `First`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Ми викликаємо функцію `setTimeout` першою. Тим не менш, вона виводиться в консоль останньою.

Це відбувається через те, що в браузерах у нас є не тільки рантайм движок, але і `WebAPI`. `WebAPI` надає нам функцію `setTimeout` і багато інших можливостей. Наприклад, DOM.

Після того як _коллбек_ відправлений в `WebAPI`, функція `setTimeout` (але не коллбек!) виймається з стека.

<img src="https://i.imgur.com/X5wsHOg.png" width="200">

Тепер викликається `foo`, і `"First"` виводиться в консоль.

<img src="https://i.imgur.com/Pvc0dGq.png" width="200">

`foo` дістається з стека, і викликається `baz`. `"Third"` виводиться в консоль.

<img src="https://i.imgur.com/WhA2bCP.png" width="200">

`WebAPI` не може додавати вміст в стек коли захоче. Замість цього він відправляє коллбек-функцію в так звану _чергу_.

<img src="https://i.imgur.com/NSnDZmU.png" width="200">

Тут на сцену виходить цикл подій (event loop). **Event loop** перевіряє стек і черга завдань. Якщо стек порожній, то він бере перший елемент з черги і відправляє його в стек.

<img src="https://i.imgur.com/uyiScAI.png" width="200">

Викликається `bar`, в консоль виводиться `"Second"` і ця функція дістається з стека.

</p>
</details>

---

###### 31. Що буде в `event.target` після кліка на кнопку?

```html
<div onclick="console.log('first div')">
  <div onclick="console.log('second div')">
    <button onclick="console.log('button')">
      Click!
    </button>
  </div>
</div>
```

- A: Зовнішній `div`
- B: Внутрішній `div`
- C: `button`
- D: Масив з усіма вкладеними елементами

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Метою події є **найглибший** вкладений елемент. Зупинити поширення подій можна за допомогою `event.stopPropagation`

</p>
</details>

---

###### 32. Що буде в консолі після кліка по параграфу?

```html
<div onclick="console.log('div')">
  <p onclick="console.log('p')">
    Click here!
  </p>
</div>
```

- A: `p` `div`
- B: `div` `p`
- C: `p`
- D: `div`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Після кліка по `p` буде виведено `p` та `div`. У циклі життя події є три фази: **захоплення**, **мета** і **спливання**. За замовчуванням обробники подій виконуються на фазі спливання (якщо не встановлено параметр `useCapture` в `true`). Спливання йде з найглибшого елемента вгору.

</p>
</details>

---

###### 33. Що буде в консолі?

```javascript
const person = { name: "Lydia" };

function sayHi(age) {
  console.log(`${this.name} is ${age}`);
}

sayHi.call(person, 21);
sayHi.bind(person, 21);
```

- A: `undefined is 21` `Lydia is 21`
- B: `function` `function`
- C: `Lydia is 21` `Lydia is 21`
- D: `Lydia is 21` `function`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

В обох випадках ми передаємо об'єкт, на який буде вказувати `this`. Але `.call` виконується _відразу ж_!

`.bind` повертає _копію_ функції, але з прив'язаним контекстом. Вона не виконується негайно.

</p>
</details>

---

###### 34. Яким буде результат?

```javascript
function sayHi() {
  return (() => 0)();
}

typeof sayHi();
```

- A: `"object"`
- B: `"number"`
- C: `"function"`
- D: `"undefined"`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Функція `sayHi` повертає значення, що повертається з _негайно викликаного функціонального виразу_ (IIFE). Результатом є `0` типу `"number"`.

Для інформації: в JS 7 вбудованих типів: `null`, `undefined`, `boolean`, `number`, `string`, `object`, `symbol`, та `bigint`. `"Function"` не є окремим типом, тому що функції є об'єктами типу `"object"`.

</p>
</details>

---

###### 35. Які з цих значень є "помилковими"?

```javascript
0;
new Number(0);
("");
(" ");
new Boolean(false);
undefined;
```

- A: `0`, `''`, `undefined`
- B: `0`, `new Number(0)`, `''`, `new Boolean(false)`, `undefined`
- C: `0`, `''`, `new Boolean(false)`, `undefined`
- D: Всі значення.

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Є тільки шість "помилкових" значень:

- `undefined`
- `null`
- `NaN`
- `0`
- `''` (порожній рядок)
- `false`

Конструктори функцій, такі як `new Number` та `new Boolean` є "істинними".

</p>
</details>

---

###### 36. Що буде в консолі?

```javascript
console.log(typeof typeof 1);
```

- A: `"number"`
- B: `"string"`
- C: `"object"`
- D: `"undefined"`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

`typeof 1` повертає `"number"`.
`typeof "number"` повертає `"string"`

</p>
</details>

---

###### 37. Що буде в консолі?

```javascript
const numbers = [1, 2, 3];
numbers[10] = 11;
console.log(numbers);
```

- A: `[1, 2, 3, 7 x null, 11]`
- B: `[1, 2, 3, 11]`
- C: `[1, 2, 3, 7 x empty, 11]`
- D: `SyntaxError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Коли в масив додається значення, яке виходить за межі довжини масиву, JavaScript створює так звані "порожні клітинки". Насправді вони мають значення `undefined`, але в консолі виводяться так:

`[1, 2, 3, 7 x empty, 11]`

в залежності від місця використання (може відрізнятися для браузерів, Node, і т.д.).

</p>
</details>

---

###### 38. Що буде в консолі?

```javascript
(() => {
  let x, y;
  try {
    throw new Error();
  } catch (x) {
    (x = 1), (y = 2);
    console.log(x);
  }
  console.log(x);
  console.log(y);
})();
```

- A: `1` `undefined` `2`
- B: `undefined` `undefined` `undefined`
- C: `1` `1` `2`
- D: `1` `undefined` `undefined`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Блок `catch` отримує аргумент `x`. Це не той же `x`, який визначено в якості змінної перед рядком `try`.

Потім ми присвоюємо даному аргументу значення `1` та встановлюємо значення для змінної `y`. Потім виводимо в консоль значення аргументу `x`, що дорівнює `1`.

За межами блоку `catch` змінна `x` все ще `undefined`, а `y` дорівнює `2`. Коли ми викликаємо` console.log(x)` за межами блоку `catch`, цей виклик повертає `undefined`, а `y` повертає `2`.

</p>
</details>

---

###### 39. Все в JavaScript це...

- A: примітив або об'єкт
- B: функція або об'єкт
- C: питання з підступом! тільки об'єкти
- D: число або об'єкт

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

В JavaScript є тільки примітиви й об'єкти.

Типи примітивів: `boolean`, `null`, `undefined`, `bigint`, `number`, `string`, та `symbol`.

Відмінністю примітиву від об'єкта є те, що примітиви не мають властивостей або методів. Проте, `'foo'.toUpperCase()` перетворюється в `'FOO'` та не викликає `TypeError`. Це відбувається тому, що при спробі отримання властивості або методу у примітиву (наприклад, рядки), JavaScript неявно оберне примітив об'єктом, використовуючи один з класів-обгорток (наприклад, `String`), а потім відразу ж знищить обгортку після обчислення виразу. Всі примітиви крім `null` та `undefined` поводяться таким чином.

</p>
</details>

---

###### 40. Що буде в консолі?

```javascript
[[0, 1], [2, 3]].reduce(
  (acc, cur) => {
    return acc.concat(cur);
  },
  [1, 2]
);
```

- A: `[0, 1, 2, 3, 1, 2]`
- B: `[6, 1, 2]`
- C: `[1, 2, 0, 1, 2, 3]`
- D: `[1, 2, 6]`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

`[1, 2]` - початкове значення, з яким ініціалізується змінна `acc`. Після першого проходу `acc` дорівнюватиме `[1,2]`, а `cur` буде `[0,1]`. Після конкатенації результат буде `[1, 2, 0, 1]`.

Потім `acc` дорівнює `[1, 2, 0, 1]`, а cur `[2, 3]`. Після злиття отримаємо `[1, 2, 0, 1, 2, 3]`.

</p>
</details>

---

###### 41. Що буде в консолі?

```javascript
!!null;
!!"";
!!1;
```

- A: `false` `true` `false`
- B: `false` `false` `true`
- C: `false` `true` `true`
- D: `true` `true` `false`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

`null` "НЕправдивий". `!null` повертає `true`. `!true` повертає `false`.

`""` "НЕправдивий". `!""` повертає `true`. `!true` повертає `false`.

`1` "правдивий". `!1` повертає `false`. `!false` повертає `true`.

</p>
</details>

---

###### 42. Що повертає метод `setInterval`?

```javascript
setInterval(() => console.log("Hi"), 1000);
```

- A: унікальний id
- B: вказану кількість мілісекунд
- C: передану функцію
- D: `undefined`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Цей метод повертає унікальний id, який може бути використаний для очищення інтервалу за допомогою функції `clearInterval()`.

</p>
</details>

---

###### 43. Що повернеться?

```javascript
[..."Lydia"];
```

- A: `["L", "y", "d", "i", "a"]`
- B: `["Lydia"]`
- C: `[[], "Lydia"]`
- D: `[["L", "y", "d", "i", "a"]]`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Рядок є ітерабельною сутністю. Оператор поширення перетворює кожен символ в окремий елемент.

</p>
</details>

---

###### 44. Що буде в консолі?

```javascript
function* generator(i) {
  yield i;
  yield i * 2;
}

const gen = generator(10);

console.log(gen.next().value);
console.log(gen.next().value);
```

- A: `[0, 10], [10, 20]`
- B: `20, 20`
- C: `10, 20`
- D: `0, 10 and 10, 20`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Звичайні функції не можна зупинити "на півдорозі" після виклику. Однак функція-генератор може зупинитися "на півдорозі", а потім продовжити з того місця, де вона зупинилась. Кожного разу, коли функція-генератор зустрічає ключове слово `yield`, функція видає значення, що вказане після нього. Зауважте, що функція-генератор в цьому випадку не _повертає_ (return) значення, вона _дає_ (yields) значення.

Спочатку ми ініціалізуємо функцію-генератор з `i` рівним `10`. Ми викликаємо функцію-генератор за допомогою методу `next()`. Коли ми вперше викликаємо функцію генератора, `i` дорівнює `10`. Перше ключове слово `yield`: воно дає значення `i`. Генератор тепер "призупинено", і `10` записується у консоль.

Потім ми знову викликаємо функцію за допомогою методу `next()`. Виконання коду продовжується там, де зупинилося раніше, все ще з `i` що дорівнює `10`. Тепер функція зустрічає наступне ключове слово `yield` і дає `i * 2`. `i` дорівнює `10`, тож віддається `10 * 2`, що дорівнює `20`. У результаті: `10, 20`.

</p>
</details>


---

###### 45. Що повернеться?

```javascript
const firstPromise = new Promise((res, rej) => {
  setTimeout(res, 500, 'one');
});

const secondPromise = new Promise((res, rej) => {
  setTimeout(res, 100, 'two');
});

Promise.race([firstPromise, secondPromise]).then(res => console.log(res));
```

- A: `"one"`
- B: `"two"`
- C: `"two" "one"`
- D: `"one" "two"`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Коли ми передаємо кілька промісів методу `Promise.race`, він вирішує/відхиляє _перший_ проміс, яки вирішився/відхилився. Методу `setTimeout` ми передаємо таймер: 500 мс для першого промісу (`firstPromise`) та 100 мс для другого промісу (`secondPromise`). Це означає, що `secondPromise` вирішиться першим зі значенням `'two'`. `res` тепер містить значення `'two'`, яке буде зображено у консолі.

</p>
</details>

---

###### 46. Що буде на виході?

```javascript
let person = { name: 'Lydia' };
const members = [person];
person = null;

console.log(members);
```

- A: `null`
- B: `[null]`
- C: `[{}]`
- D: `[{ name: "Lydia" }]`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

Спочатку ми оголошуємо змінну `person` що містить об'єкта, який має властивість `name`.

<img src="https://i.imgur.com/TML1MbS.png" width="200">

Потім ми оголошуємо змінну `members`. Ми встановлюємо перший елемент масиву рівним значенню змінної `person`. Об'єкти взаємодіють за допомогою _посилання_, коли їх встановлюють рівними один одному. Коли ви призначаєте посилання з однієї змінної на іншу, ви робите _копію_ цього посилання. (зверніть увагу, що вони не мають _однакового_ посилання!)

<img src="https://i.imgur.com/FSG5K3F.png" width="300">

Далі ми встановлюємо змінну `person` рівною `null`.

<img src="https://i.imgur.com/sYjcsMT.png" width="300">

Ми лише змінюємо значення змінної `person`, а не перший елемент у масиві, оскільки цей елемент має інше (скопійоване) посилання на об’єкт.Перший елемент у `members` все ще містить своє посилання на вихідний об’єкт. Коли ми виводимо у консоль масив `members`, перший елемент усе ще містить значення об'єкта, який і показується у консолі.

</p>
</details>

---

###### 47. Що буде на виході?

```javascript
const person = {
  name: 'Lydia',
  age: 21,
};

for (const item in person) {
  console.log(item);
}
```

- A: `{ name: "Lydia" }, { age: 21 }`
- B: `"name", "age"`
- C: `"Lydia", 21`
- D: `["name", "Lydia"], ["age", 21]`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

За допомогою циклу `for-in` ми можемо перебирати ключі об’єктів, у цьому випадку `name` та `age`. Під капотом ключі об’єктів є рядками (якщо вони не є Cимволом). У кожному циклі ми встановлюємо значення `item` рівним поточному ключу, який він перебирає. Спочатку, `item` дорівнює `name` і логується. Тоді, `item` дорівнює `age`, який логується.

</p>
</details>

---

###### 48. Що буде на виході?

```javascript
console.log(3 + 4 + '5');
```

- A: `"345"`
- B: `"75"`
- C: `12`
- D: `"12"`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Асоціативність оператора — це порядок, у якому компілятор обчислює вирази, або зліва направо, або справа наліво. Це відбувається, лише якщо всі оператори мають _однаковий_ пріоритет. У нас є лише один тип оператора: `+`. Для додавання, асоціативність - зліва направо.

Першим обчислюється `3 + 4`. Це призводить до числа `7`.

`7 + '5'` призводить до `"75"` через перетворення типу. JavaScript перетворює число `7` на рядок, див. запитання 15. Ми можемо об'єднати два рядки за допомогою оператора `+`. `"7"` + `"5"` призводить до `"75"`.

</p>
</details>

---

###### 49. Яке значення `num`?

```javascript
const num = parseInt('7*6', 10);
```

- A: `42`
- B: `"42"`
- C: `7`
- D: `NaN`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Повертаються лише перші числа в рядку. Базуючись на _розряді числа_ (другий аргумент, який вказує, до якого типу числа ми хочемо розібрати його: з основою 10, шістнадцяткове, вісімкове, двійкове тощо), `parseInt` перевіряє, чи дійсні символи в рядку.  Як тільки він зустрічає символ, який не є дійсним числом у основі, він припиняє аналіз та ігнорує наступні символи.

`*` не є дійсним числом. Він розбирає лише `"7"` до десяткового `7`. `num` тепер містить значення `7`.

</p>
</details>

---

###### 50. Що буде на виході?

```javascript
[1, 2, 3].map(num => {
  if (typeof num === 'number') return;
  return num * 2;
});
```

- A: `[]`
- B: `[null, null, null]`
- C: `[undefined, undefined, undefined]`
- D: `[ 3 x empty ]`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Під час перебирання масиву значення `num` дорівнює елементу, який він наразі перебирає. У цьому випадку елементи є числами, тому умова оператора `typeof num === "number"` повертає `true`. Функція map створює новий масив і вставляє значення, повернуті функцією.

Однак ми не повертаємо значення. Якщо ми не повертаємо значення з функції, функція повертає `undefined`. Для кожного елемента в масиві викликається функція, тому для кожного елемента ми повертаємо `undefined`.

</p>
</details>

---

###### 51. Що буде на виході?

```javascript
function getInfo(member, year) {
  member.name = 'Lydia';
  year = '1998';
}

const person = { name: 'Sarah' };
const birthYear = '1997';

getInfo(person, birthYear);

console.log(person, birthYear);
```

- A: `{ name: "Lydia" }, "1997"`
- B: `{ name: "Sarah" }, "1998"`
- C: `{ name: "Lydia" }, "1998"`
- D: `{ name: "Sarah" }, "1997"`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Аргументи передаються за _значенням_, хіба що їх значення це об’єкт, тоді вони передаються за _посиланням_. `birthYear` передається за значенням, оскільки це рядок, а не об’єкт. Коли ми передаємо аргументи за значенням, створюється _копія_ цього значення (див. запитання 46).

Змінна `birthYear` має значення `"1997"`. Аргумент `year` також має значення `"1997"`, але це не те саме значення, на яке посилається `birthYear`. Коли ми оновлюємо значення `year`, встановлюючи `year` рівним `"1998"`, ми оновлюємо лише значення `year`. `birthYear` дорівнює `"1997"`.

Значення `person` є об'єктом. Аргумент `member` має (скопійоване) посилання на _той самий_ об’єкт. Коли ми змінюємо властивість об’єкта `member`, значення `person` також буде змінено, оскільки вони обидва мають посилання на той самий об’єкт. Властивість `name` об’єкта `person` тепер дорівнює значенню `"Lydia"`.

</p>
</details> 

---

###### 52. Що буде на виході?

```javascript
function greeting() {
  throw 'Hello world!';
}

function sayHi() {
  try {
    const data = greeting();
    console.log('It worked!', data);
  } catch (e) {
    console.log('Oh no an error:', e);
  }
}

sayHi();
```

- A: `It worked! Hello world!`
- B: `Oh no an error: undefined`
- C: `SyntaxError: can only throw Error objects`
- D: `Oh no an error: Hello world!`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

За допомогою оператора `throw` ми можемо створювати власні помилки. За допомогою цього оператора ви можете створювати винятки. Винятком може бути <b>рядок</b>, <b>число</b>, <b>логічне значення</b> або <b>об'єкт</b>. У цьому випадку нашим винятком є рядок `'Hello world!'`.

За допомогою оператора `catch` ми можемо вказати, що робити, якщо в блоці `try` виникне виняток. Викидається виняток: рядок `'Hello world!'`. `e` тепер дорівнює цьому рядку, який ми логуємо. Це призводить до повідомлення `'Oh an error: Hello world!'`.

</p>
</details>

---

###### 53. Що буде на виході?

```javascript
function Car() {
  this.make = 'Lamborghini';
  return { make: 'Maserati' };
}

const myCar = new Car();
console.log(myCar.make);
```

- A: `"Lamborghini"`
- B: `"Maserati"`
- C: `ReferenceError`
- D: `TypeError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Коли функція-конструктор викликається з ключовим словом `new`, вона створює об’єкт і встановлює ключове слово `this` для посилання на цей об’єкт. За замовчуванням, якщо функція-конструктор нічого явно не повертає, вона повертає щойно створений об’єкт.

У цьому випадку функція-конструктор `Car` явно повертає новий об’єкт із `make`, встановленим на `"Maserati"`, що замінює поведінку за замовчуванням. Таким чином, коли викликається `new Car()`, об’єкт _який повертається_ призначається `myCar`, у результаті чого виводиться `"Maserati"`, коли здійснюється доступ до `myCar.make`.

</p>
</details>

---

###### 54. Що буде на виході?

```javascript
(() => {
  let x = (y = 10);
})();

console.log(typeof x);
console.log(typeof y);
```

- A: `"undefined", "number"`
- B: `"number", "number"`
- C: `"object", "number"`
- D: `"number", "undefined"`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

`let x = (y = 10);` насправді є скороченням для:

```javascript
y = 10;
let x = y;
```

Коли ми встановлюємо `y` рівним `10`, ми фактично додаємо властивість `y` до глобального об’єкта (`window` у браузері, `global` у Node). У браузері `window.y` тепер дорівнює `10`.

Потім ми оголошуємо змінну `x` зі значенням `y`, яке дорівнює `10`. Змінні, оголошені за допомогою ключового слова `let`, є _блоковими_, вони визначені лише в блоці, в якому вони оголошені; вираз негайно викликаної функції (IIFE) у цьому випадку. Коли ми використовуємо оператор `typeof`, операнд `x` не визначено: ми намагаємося отримати доступ до `x` поза межами блоку, у якому він оголошений. Це означає, що `x` не визначено. Значення, яке не було оголошено, або не було присвоєно значення, належать до типу `"undefined"`. `console.log(typeof x)` повертає `"undefined"`.

Однак ми створили глобальну змінну `y`, коли встановили `y` рівним `10`. Це значення доступне будь-де в нашому коді. `y` визначено та містить значення типу `"number"`. `console.log(typeof y)` повертає `"number"`.

</p>
</details>

---

###### 55. Що буде на виході?

```javascript
class Dog {
  constructor(name) {
    this.name = name;
  }
}

Dog.prototype.bark = function() {
  console.log(`Woof I am ${this.name}`);
};

const pet = new Dog('Mara');

pet.bark();

delete Dog.prototype.bark;

pet.bark();
```

- A: `"Woof I am Mara"`, `TypeError`
- B: `"Woof I am Mara"`, `"Woof I am Mara"`
- C: `"Woof I am Mara"`, `undefined`
- D: `TypeError`, `TypeError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Ми можемо видалити властивості з об’єктів за допомогою ключового слова `delete`, також у прототипі. Якщо видалити властивість у прототипі, вона більше не буде доступною в ланцюжку прототипів. У цьому випадку функція `bark` більше не доступна в прототипі після `delete Dog.prototype.bark`, але ми все одно намагаємося отримати до неї доступ.

Коли ми намагаємося викликати щось, що не є функцією, видається `TypeError`. У цьому випадку `TypeError: pet.bark is not a function`, оскільки `pet.bark` є `undefined`.

</p>
</details>

---

###### 56. Що буде на виході?

```javascript
const set = new Set([1, 1, 2, 3, 4]);

console.log(set);
```

- A: `[1, 1, 2, 3, 4]`
- B: `[1, 2, 3, 4]`
- C: `{1, 1, 2, 3, 4}`
- D: `{1, 2, 3, 4}`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

Об’єкт `Set` — це набір _унікальних_ значень: значення може зустрічатися лише один раз.

Ми передали масив, який перебирається `[1, 1, 2, 3, 4]` з повторюваним значенням `1`. Оскільки в множині Set не може бути двох однакових значень, одне з них видаляється. У результаті виходить `{1, 2, 3, 4}`.

</p>
</details>

---

###### 57. Що буде на виході?

```javascript
// counter.js
let counter = 10;
export default counter;
```

```javascript
// index.js
import myCounter from './counter';

myCounter += 1;

console.log(myCounter);
```

- A: `10`
- B: `11`
- C: `Error`
- D: `NaN`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Імпортований модуль доступний лише для _читання_: ви не можете змінити імпортований модуль. Лише модуль, який його експортує, може змінити його значення.

Коли ми намагаємося збільшити значення `myCounter`, це видає помилку: `myCounter` доступний лише для читання і не може бути змінений.

</p>
</details>

---

###### 58. Що буде на виході?

```javascript
const name = 'Lydia';
age = 21;

console.log(delete name);
console.log(delete age);
```

- A: `false`, `true`
- B: `"Lydia"`, `21`
- C: `true`, `true`
- D: `undefined`, `undefined`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Оператор `delete` повертає логічне значення: `true` у разі успішного видалення, інакше він поверне `false`. Однак змінні, оголошені за допомогою ключового слова `var`, `const` або `let`, не можна видалити за допомогою оператора `delete`.

Змінну `name` було оголошено з ключовим словом `const`, тому її видалення не вдалося: повертається `false`. Коли ми встановлюємо `age` рівним `21`, ми фактично додаємо властивість під назвою `age` до глобального об'єкта. Таким способом ми можемо успішно видаляти властивості об’єктів, в тому числі з глобального об’єкта, тому `delete age` повертає `true`.

</p>
</details>

---

###### 59. Що буде на виході?

```javascript
const numbers = [1, 2, 3, 4, 5];
const [y] = numbers;

console.log(y);
```

- A: `[[1, 2, 3, 4, 5]]`
- B: `[1, 2, 3, 4, 5]`
- C: `1`
- D: `[1]`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Ми можемо розпаковувати значення з масивів або властивості з об’єктів за допомогою деструктуризації. Наприклад:

```javascript
[a, b] = [1, 2];
```

<img src="https://i.imgur.com/ADFpVop.png" width="200">

Значення `a` тепер дорівнює `1`, а значення `b` тепер дорівнює `2`. Що ми насправді зробили в питанні, це:

```javascript
[y] = [1, 2, 3, 4, 5];
```

<img src="https://i.imgur.com/NzGkMNk.png" width="200">

Це означає, що значення `y` дорівнює першому значенню в масиві, яке є числом `1`. Коли ми логуємо `y`, повертається `1`.

</p>
</details>

---

###### 60. Що буде на виході?

```javascript
const user = { name: 'Lydia', age: 21 };
const admin = { admin: true, ...user };

console.log(admin);
```

- A: `{ admin: true, user: { name: "Lydia", age: 21 } }`
- B: `{ admin: true, name: "Lydia", age: 21 }`
- C: `{ admin: true, user: ["Lydia", 21] }`
- D: `{ admin: true }`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Можна об'єднувати об'єкти за допомогою оператора розширення `...`. Він дозволяє створювати копії пар ключ/значення одного об’єкта та додавати їх до іншого об’єкта. У цьому випадку ми створюємо копії об’єкта `user` і додаємо їх до об’єкта `admin`. Об’єкт `admin` тепер містить скопійовані пари ключ/значення, що призводить до `{ admin: true, name: "Lydia", age: 21 }`.

</p>
</details>

---

###### 61. Що буде на виході?

```javascript
const person = { name: 'Lydia' };

Object.defineProperty(person, 'age', { value: 21 });

console.log(person);
console.log(Object.keys(person));
```

- A: `{ name: "Lydia", age: 21 }`, `["name", "age"]`
- B: `{ name: "Lydia", age: 21 }`, `["name"]`
- C: `{ name: "Lydia"}`, `["name", "age"]`
- D: `{ name: "Lydia"}`, `["age"]`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

За допомогою методу `defineProperty` ми можемо додавати нові властивості до об’єкта або змінювати наявні. Коли ми додаємо властивості до об’єкта за допомогою методу `defineProperty`, вони за замовчуванням _не перелічуються_. Метод `Object.keys` повертає всі _перелічувані_ імена властивостей об’єкта, у цьому випадку лише `"name"`.

Властивості, додані за допомогою методу `defineProperty`, незмінні за умовчанням. Ми можемо змінити цю поведінку за допомогою властивостей `writable`, `configurable` і `enumerable`. Таким чином, метод `defineProperty` дає нам набагато більше контролю над властивостями, які ми додаємо до об’єкта.

</p>
</details>

---

###### 62. Що буде на виході?

```javascript
const settings = {
  username: 'lydiahallie',
  level: 19,
  health: 90,
};

const data = JSON.stringify(settings, ['level', 'health']);
console.log(data);
```

- A: `"{"level":19, "health":90}"`
- B: `"{"username": "lydiahallie"}"`
- C: `"["level", "health"]"`
- D: `"{"username": "lydiahallie", "level":19, "health":90}"`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Другим аргументом `JSON.stringify` є _замінник_. Замінник може бути або функцією, або масивом, і дозволяє нам контролювати, які та як значення слід перетворити в рядок.

Якщо замінник є _масивом_, до рядка JSON буде додано лише назви властивостей, які входять до масиву. У цьому випадку включено лише властивості `"level"` та `"health"`, `"username"` виключено. `data` тепер дорівнює `"{"level":19, "health":90}"`.

Якщо замінник є _функцією_, ця функція викликається для кожної властивості в об’єкті, який ми перетворюємо в рядок. Значення, яке повертається цією функцією, буде значенням властивості, коли воно додається до рядка JSON. Якщо значення `undefined`, ця властивість виключається з рядка JSON.

</p>
</details>

---

###### 63. Що буде на виході?

```javascript
let num = 10;

const increaseNumber = () => num++;
const increasePassedNumber = number => number++;

const num1 = increaseNumber();
const num2 = increasePassedNumber(num1);

console.log(num1);
console.log(num2);
```

- A: `10`, `10`
- B: `10`, `11`
- C: `11`, `11`
- D: `11`, `12`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Унарний оператор `++` _спочатку повертає_ значення операнда, _потім збільшує_ значення операнда. Значення `num1` дорівнює `10`, оскільки функція `increaseNumber` спочатку повертає значення `num`, яке дорівнює `10`, і лише потім збільшує значення `num`.

`num2` дорівнює `10`, оскільки ми передали `num1` до `increasePassedNumber`. `number` дорівнює `10` (значення `num1`). Знову ж таки, унарний оператор `++` _спочатку повертає_ значення операнда, _потім збільшує_ значення операнда. Значення `number` дорівнює `10`, тому `num2` дорівнює `10`.

</p>
</details>

---

###### 64. Що буде на виході?

```javascript
const value = { number: 10 };

const multiply = (x = { ...value }) => {
  console.log((x.number *= 2));
};

multiply();
multiply();
multiply(value);
multiply(value);
```

- A: `20`, `40`, `80`, `160`
- B: `20`, `40`, `20`, `40`
- C: `20`, `20`, `20`, `40`
- D: `NaN`, `NaN`, `20`, `40`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

В ES6 ми можемо ініціалізувати параметри з значенням за замовчуванням. Значення параметра буде значенням за замовчуванням, якщо жодне інше значення не було передано до функції або якщо значення параметра `"undefined"`. У цьому випадку ми поширюємо властивості об’єкта `value` на новий об’єкт, тому `x` має стандартне значення `{ number: 10 }`.

Аргумент за замовчуванням обчислюється під час _виклику_! Щоразу, коли ми викликаємо функцію, створюється _новий_ об’єкт. Перші два рази ми викликаємо функцію `multiply`, не передаючи значення: `x` має стандартне значення `{ number: 10 }`. Далі ми логуємо помножене значення цього числа, яке дорівнює `20`.

Третій раз, коли ми викликаємо `multiply`, ми передаємо аргумент: об’єкт під назвою `value`. Оператор `*=` насправді є скороченням для `x.number = x.number * 2`: ми змінюємо значення `x.number` і логуємо помножене значення `20`.

Четвертого разу ми знову передаємо об’єкт `value`. `x.number` було раніше змінено на `20`, тому `x.number *= 2` логує `40`.

</p>
</details>

---

###### 65. Що буде на виході?

```javascript
[1, 2, 3, 4].reduce((x, y) => console.log(x, y));
```

- A: `1` `2` та `3` `3` та `6` `4`
- B: `1` `2` та `2` `3` та `3` `4`
- C: `1` `undefined` та `2` `undefined` та `3` `undefined` та `4` `undefined`
- D: `1` `2` та `undefined` `3` та `undefined` `4`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

Першим аргументом, який отримує метод `reduce`, є _акумулятор_, у цьому випадку `x`. Другим аргументом є _поточне значення_, `y`. За допомогою методу `reduce` ми викликаємо колбек функцію для кожного елемента в масиві, що в кінцевому підсумку може призвести до єдиного значення.

У цьому прикладі ми не повертаємо жодних значень, ми просто логуємо значення акумулятора та поточне значення.

Значення акумулятора дорівнює попередньо повернутому значенню колбек функції. Якщо ми не передаємо додатковий аргумент `initialValue` методу `reduce`, акумулятор дорівнюватиме першому елементу під час першого виклику.

Під час першого виклику акумулятор (`x`) дорівнює `1`, а поточне значення (`y`) — `2`. Ми нічого не повертаємо із колбек функції, ми логуємо акумулятор і поточне значення: `1` і `2`.

Якщо ми не повертаємо значення з функції, вона повертає `undefined`. Під час наступного виклику акумулятор має значення `undefined`, а поточне значення — `3`. `undefined` та `3` логуються.

Під час четвертого виклику ми знову нічого не повертаємо із колбек функції. Акумулятор знову `undefined`, а поточне значення `4`. `undefined` та `4` логуються.

</p>
</details>
  
---

###### 66. За допомогою якого конструктора ми можемо успішно розширити клас `Dog`?

```javascript
class Dog {
  constructor(name) {
    this.name = name;
  }
};

class Labrador extends Dog {
  // 1
  constructor(name, size) {
    this.size = size;
  }
  // 2
  constructor(name, size) {
    super(name);
    this.size = size;
  }
  // 3
  constructor(size) {
    super(name);
    this.size = size;
  }
  // 4
  constructor(name, size) {
    this.name = name;
    this.size = size;
  }

};
```

- A: 1
- B: 2
- C: 3
- D: 4

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

У похідному класі ми не можемо отримати доступ до ключового слова `this` до виклику `super`. Якщо ми спробуємо це зробити, це викличе `ReferenceError`: `1` і `4` викинуть помилку.

За допомогою ключового слова `super` ми викликаємо конструктор батьківського класу з заданими аргументами. Батьківський конструктор отримує аргумент `name`, тому нам потрібно передати `name` в `super`.

Клас `Labrador` отримує два аргументи: `name`, оскільки він розширює `Dog`, і `size` як додаткову властивість у класі `Labrador`. Їх обох потрібно передати функції конструктор `Labrador`, що правильно робиться за допомогою конструктора `2`.

</p>
</details>

---

###### 67. Що буде на виході?

```javascript
// index.js
console.log('running index.js');
import { sum } from './sum.js';
console.log(sum(1, 2));

// sum.js
console.log('running sum.js');
export const sum = (a, b) => a + b;
```

- A: `running index.js`, `running sum.js`, `3`
- B: `running sum.js`, `running index.js`, `3`
- C: `running sum.js`, `3`, `running index.js`
- D: `running index.js`, `undefined`, `running sum.js`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

За допомогою ключового слова `import` усі імпортовані модулі _попередньо аналізуються_. Це означає, що імпортовані модулі запускаються _спочатку_, а код у файлі, який імпортує модуль, виконується _після_.

Це різниця між `require()` у CommonJS та `import`! За допомогою `require()` ми можемо завантажувати залежності на вимогу під час виконання коду. Якби ми використали `require` замість `import`, `running index.js`, `running sum.js`, `3` було б залоговано в консолі.

</p>
</details>

---

###### 68. Що буде на виході?

```javascript
console.log(Number(2) === Number(2));
console.log(Boolean(false) === Boolean(false));
console.log(Symbol('foo') === Symbol('foo'));
```

- A: `true`, `true`, `false`
- B: `false`, `true`, `false`
- C: `true`, `false`, `true`
- D: `true`, `true`, `true`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Кожен Символ абсолютно унікальний. Метою аргументу, який передається Символу, є надання йому опису. Значення Символу не залежить від переданого аргументу. Перевіряючи рівність, ми створюємо два абсолютно нові Символи: перший `Symbol('foo')` та другий `Symbol('foo')`. Ці два значення унікальні й не дорівнюють одне одному, `Symbol('foo') === Symbol('foo')` повертає `false`.

</p>
</details>

---

###### 69. Що буде на виході?

```javascript
const name = 'Lydia Hallie';
console.log(name.padStart(13));
console.log(name.padStart(2));
```

- A: `"Lydia Hallie"`, `"Lydia Hallie"`
- B: `" Lydia Hallie"`, `" Lydia Hallie"` (`"[13x whitespace]Lydia Hallie"`, `"[2x whitespace]Lydia Hallie"`)
- C: `" Lydia Hallie"`, `"Lydia Hallie"` (`"[1x whitespace]Lydia Hallie"`, `"Lydia Hallie"`)
- D: `"Lydia Hallie"`, `"Lyd"`,

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

За допомогою методу `padStart` ми можемо додати відступ до початку рядка. Значення, яке передається в цей метод, є _загальною_ довжиною рядка разом із відступом. Рядок `"Lydia Hallie"` має довжину `12`. `name.padStart(13)` вставляє 1 пробіл на початку рядка, оскільки `12 + 1` дорівнює `13`.

Якщо аргумент, переданий методу `padStart`, менший за довжину рядка, відступ не буде додано.

</p>
</details>

---

###### 70. Що буде на виході?

```javascript
console.log('🥑' + '💻');
```

- A: `"🥑💻"`
- B: `257548`
- C: Рядок, що містить їхні кодові точки
- D: Помилка

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

За допомогою оператора `+` ми можемо об'єднувати рядки. У цьому випадку ми об’єднуємо рядок `"🥑"` із рядком `"💻"`, у результаті чого отримуємо `"🥑💻"`.

</p>
</details>

---

###### 71. Як ми можемо отримати значення, які закоментовані після оператора console.log?

```javascript
function* startGame() {
  const answer = yield 'Do you love JavaScript?';
  if (answer !== 'Yes') {
    return "Oh wow... Guess we're done here";
  }
  return 'JavaScript loves you back ❤️';
}

const game = startGame();
console.log(/* 1 */); // Do you love JavaScript?
console.log(/* 2 */); // JavaScript loves you back ❤️
```

- A: `game.next("Yes").value` та `game.next().value`
- B: `game.next.value("Yes")` та `game.next.value()`
- C: `game.next().value` та `game.next("Yes").value`
- D: `game.next.value()` та `game.next.value("Yes")`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Функція-генератор "призупиняє" своє виконання, коли бачить ключове слово `yield`. Для початку, ми маємо дозволити функції видавати рядок "Do you love JavaScript?", що можна зробити, викликавши `game.next().value`.

Кожен рядок виконується, доки не знайде перше ключове слово `yield`. У першому рядку функції є ключове слово `yield`: виконання припиняється з першим yield! _Це означає, що змінна `answer` ще не визначена!_

Коли ми викликаємо `game.next("Yes").value`, попередній `yield` замінюється значенням параметрів, переданих у функцію `next()`, у цьому випадку `"Yes"`. Значення змінної `answer` тепер дорівнює `"Yes"`. Умова оператора if повертає `false` і логується `JavaScript loves you back ❤️`.

</p>
</details>

---

###### 72. Що буде на виході?

```javascript
console.log(String.raw`Hello\nworld`);
```

- A: `Hello world!`
- B: `Hello` <br />&nbsp; &nbsp; &nbsp;`world`
- C: `Hello\nworld`
- D: `Hello\n` <br /> &nbsp; &nbsp; &nbsp;`world`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

`String.raw` повертає рядок, у якому екрановані символи (`\n`, `\v`, `\t`, тощо) ігноруються! Зворотні косі риски можуть бути проблемою, оскільки ви можете отримати щось на кшталт:

`` const path = `C:\Documents\Projects\table.html` ``

Що призведе до:

`"C:DocumentsProjects able.html"`

За допомогою `String.raw` ми просто ігноруємо екранування і повертаємо:

`C:\Documents\Projects\table.html`

У цьому випадку це рядок `Hello\nworld`, який логується.

</p>
</details>

---

###### 73. Що буде на виході?

```javascript
async function getData() {
  return await Promise.resolve('I made it!');
}

const data = getData();
console.log(data);
```

- A: `"I made it!"`
- B: `Promise {<resolved>: "I made it!"}`
- C: `Promise {<pending>}`
- D: `undefined`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Асинхронна функція завжди повертає проміс. `Await` все ще має чекати виконання проміса: незавершений проміс повертається, коли ми викликаємо `getData()`, щоб встановити `data` рівним йому.

Якби ми хотіли отримати доступ до завершеного значення `"I made it"`, ми могли б використати метод `.then()` для `data`

`data.then(res => console.log(res))`

Це повернуло б `"I made it!"`

</p>
</details>

---

###### 74. Що буде на виході?

```javascript
function addToList(item, list) {
  return list.push(item);
}

const result = addToList('apple', ['banana']);
console.log(result);
```

- A: `['apple', 'banana']`
- B: `2`
- C: `true`
- D: `undefined`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Метод `.push()` повертає _довжину_ нового масиву! Раніше масив містив один елемент (рядок `"banana"`) і мав довжину `1`. Після додавання рядка `"apple"` масив містить два елементи та має довжину `2`. Це й повертається з функції `addToList`.

Метод `push` змінює оригінальний масив. Якщо ми хотіли повернути _масив_ із функції, а не _довжину масиву_, нам слід було повернути `list` після додавання `item` до нього.

</p>
</details>

---

###### 75. Що буде на виході?

```javascript
const box = { x: 10, y: 20 };

Object.freeze(box);

const shape = box;
shape.x = 100;

console.log(shape);
```

- A: `{ x: 100, y: 20 }`
- B: `{ x: 10, y: 20 }`
- C: `{ x: 100 }`
- D: `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

`Object.freeze` унеможливлює додавання, видалення або зміну властивостей об’єкта (якщо значення властивості не є іншим об’єктом).

Коли ми створюємо змінну `shape` і встановлюємо для неї значення `box` замороженого об’єкта, `shape` також посилається на заморожений об’єкт. Ми можемо перевірити, чи об’єкт заморожений, використовуючи `Object.isFrozen`. У цьому випадку `Object.isFrozen(shape)` поверне true, оскільки змінна `shape` містить посилання на заморожений об’єкт.

Оскільки `shape` заморожено, а значення `x` не є об'єктом, ми не можемо змінити його. `x` досі дорівнює `10` та `{ x: 10, y: 20 }` логується.

</p>
</details>

---

###### 76. Що буде на виході?

```javascript
const { firstName: myName } = { firstName: 'Lydia' };

console.log(firstName);
```

- A: `"Lydia"`
- B: `"myName"`
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

За допомогою [присвоєння деструктуризації](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) ми можемо розпакувати значення з масивів або властивості з об’єктів у окремі змінні:

```javascript
const { firstName } = { firstName: 'Lydia' };
// ES5 version:
// var firstName = { firstName: 'Lydia' }.firstName;

console.log(firstName); // "Lydia"
```

Крім того, властивість можна розпакувати з об’єкта та призначити змінній з іменем, відмінним від властивості об’єкта:

```javascript
const { firstName: myName } = { firstName: 'Lydia' };
// ES5 version:
// var myName = { firstName: 'Lydia' }.firstName;

console.log(myName); // "Lydia"
console.log(firstName); // Uncaught ReferenceError: firstName is not defined
```

Отже, `firstName` не існує як змінна, тому спроба отримати доступ до її значення призведе до `ReferenceError`.

**Примітка:** Майте на увазі властивості `глобальної області видимості`:

```javascript
const { name: myName } = { name: 'Lydia' };

console.log(myName); // "lydia"
console.log(name); // "" ----- Browser e.g. Chrome
console.log(name); // ReferenceError: name is not defined  ----- NodeJS

```

Щоразу, коли Javascript не може знайти змінну в _поточній області видимості_, він підіймається вгору [ланцюжком області видимості](https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch3.md) й шукає її, і якщо він досягає області видимості верхнього рівня, відомої як **Глобальна область видимості**, і все одно не знаходить її, викине `ReferenceError`.

- У **браузерах**, таких як _Chrome_, `name` є _застарілою глобальною властивістю області видимості_. У цьому прикладі код виконується всередині _глобальної області видимості_ й немає визначеної користувачем локальної змінної для `name`, тому він шукає попередньо визначені _змінні/властивості_ в глобальній області видимості, яка у випадку браузерів виконує пошук в об’єкті `window` і він витягне значення [window.name](https://developer.mozilla.org/en-US/docs/Web/API/Window/name), яке дорівнює **порожньому рядку**.

- У **NodeJS** немає такої властивості у `global` об’єкта, тому спроба отримати доступ до відсутньої змінної призведе до [ReferenceError](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Errors/Not_defined).

</p>
</details>

---

###### 77. Це чиста функція?

```javascript
function sum(a, b) {
  return a + b;
}
```

- A: Yes
- B: No

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Чиста функція — це функція, яка _завжди_ повертає той самий результат, якщо передано однакові аргументи.

Функція `sum` завжди повертає той самий результат. Якщо ми передаємо `1` і `2`, вона _завжди_ повертатиме `3` без побічних ефектів. Якщо ми передаємо `5` і `10`, _завжди_ повертатиметься `15` і так далі. Це і є визначення чистої функції.

</p>
</details>

---

###### 78. Що буде на виході?

```javascript
const add = () => {
  const cache = {};
  return num => {
    if (num in cache) {
      return `From cache! ${cache[num]}`;
    } else {
      const result = num + 10;
      cache[num] = result;
      return `Calculated! ${result}`;
    }
  };
};

const addFunction = add();
console.log(addFunction(10));
console.log(addFunction(10));
console.log(addFunction(5 * 2));
```

- A: `Calculated! 20` `Calculated! 20` `Calculated! 20`
- B: `Calculated! 20` `From cache! 20` `Calculated! 20`
- C: `Calculated! 20` `From cache! 20` `From cache! 20`
- D: `Calculated! 20` `From cache! 20` `Error`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Функція `add` є _мемоїзованою_ функцією. За допомогою мемоїзації ми можемо кешувати результати функції, щоб пришвидшити її виконання. У цьому випадку ми створюємо об’єкт `cache`, який зберігає попередньо повернуті значення.

Якщо ми знову викликаємо функцію `addFunction` з тим самим аргументом, вона спочатку перевіряє, чи вже отримала це значення в кеші. Якщо це так, буде повернено значення кешу, що заощадить час виконання. Інакше, якщо воно не кешоване, вона обчислить значення та збереже його.

Ми викликаємо функцію `addFunction` тричі з тим самим значенням: під час першого виклику значення функції, коли `num` дорівнює `10` ще не кешується. Умова оператора `num in cache` повертає `false`, і виконується блок: `Calculated! 20`, а значення результату додається до об’єкта кешу. `cache` тепер виглядає як `{ 10: 20 }`.

Другого разу об’єкт `cache` містить значення, яке повертається для `10`. Умова оператора if `num in cache` повертає `true`, та `'From cache! 20'` логується.

Третього разу ми передаємо `5 * 2`, що перетворюється у `10`. Об’єкт `cache` містить значення, яке повертається для `10`. Умова оператора if `num in cache` повертає `true`, та `'From cache! 20'` логується.

</p>
</details>

---

###### 79. Що буде на виході?

```javascript
const myLifeSummedUp = ['☕', '💻', '🍷', '🍫'];

for (let item in myLifeSummedUp) {
  console.log(item);
}

for (let item of myLifeSummedUp) {
  console.log(item);
}
```

- A: `0` `1` `2` `3` та `"☕"` `"💻"` `"🍷"` `"🍫"`
- B: `"☕"` `"💻"` `"🍷"` `"🍫"` та `"☕"` `"💻"` `"🍷"` `"🍫"`
- C: `"☕"` `"💻"` `"🍷"` `"🍫"` та `0` `1` `2` `3`
- D: `0` `1` `2` `3` та `{0: "☕", 1: "💻", 2: "🍷", 3: "🍫"}`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

За допомогою циклу _for-in_ ми можемо перебирати **перелічувані** властивості. У масиві перелічувані властивості є "ключами" елементів масиву, які насправді є їхніми індексами. Ви можете побачити масив як:

`{0: "☕", 1: "💻", 2: "🍷", 3: "🍫"}`

Де ключі - це перелічувані властивості. `0` `1` `2` `3` логується.

За допомогою циклу _for-of_, ми можемо проходитись властивостями, які **перебираються**. Масив можна перебирати. Коли ми перебираємо масив, змінна "item" дорівнює елементу, який вона зараз обробляє, `"☕"` `"💻"` `"🍷"` `"🍫"` логується.

</p>
</details>

---

###### 80. Що буде на виході?

```javascript
const list = [1 + 2, 1 * 2, 1 / 2];
console.log(list);
```

- A: `["1 + 2", "1 * 2", "1 / 2"]`
- B: `["12", 2, 0.5]`
- C: `[3, 2, 0.5]`
- D: `[1, 1, 1]`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Елементи масиву можуть містити будь-яке значення. Числа, рядки, об’єкти, інші масиви, null, логічні значення, undefined та інші вирази, такі як дати, функції та обчислення.

Елемент дорівнюватиме поверненому значенню. `1 + 2` повертає `3`, `1 * 2` повертає `2`, а `1 / 2` повертає `0.5`.

</p>
</details>

---

###### 81. Що буде на виході?

```javascript
function sayHi(name) {
  return `Hi there, ${name}`;
}

console.log(sayHi());
```

- A: `Hi there,`
- B: `Hi there, undefined`
- C: `Hi there, null`
- D: `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

За замовчуванням аргументи мають значення `undefined`, якщо значення не було передано функції. У цьому випадку ми не передали значення для аргументу `name`. `name` дорівнює `undefined`, який логується.

У ES6 ми можемо замінити `undefined` значення за замовчуванням параметрами за замовчуванням. Наприклад:

`function sayHi(name = "Lydia") { ... }`

У цьому випадку, якщо ми не передали значення або передали `undefined`, `name` завжди дорівнюватиме рядку `Lydia`.

</p>
</details>

---

###### 82. Що буде на виході?

```javascript
var status = '😎';

setTimeout(() => {
  const status = '😍';

  const data = {
    status: '🥑',
    getStatus() {
      return this.status;
    },
  };

  console.log(data.getStatus());
  console.log(data.getStatus.call(this));
}, 0);
```

- A: `"🥑"` та `"😍"`
- B: `"🥑"` та `"😎"`
- C: `"😍"` та `"😎"`
- D: `"😎"` та `"😎"`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Значення ключового слова `this` залежить від того, де ми його використовуємо. У **методі**, подібному до методу `getStatus`, ключове слово `this` посилається на _об'єкт, якому належить метод_. Метод належить об’єкту `data`, тому `this` належить до об’єкта `data`. Коли ми логуємо `this.status`, властивість `status` об’єкта `data` логується, тобто `"🥑"`.

За допомогою методу `call` ми можемо змінити об’єкт, на який посилається ключове слово `this`. У **функціях** ключове слово `this` посилається на _об’єкт, якому належить функція_. Ми оголосили функцію `setTimeout` у _глобальному об’єкті_, тому в `setTimeout` ключове слово `this` посилається на _глобальний об’єкт_. У глобальному об’єкті є змінна під назвою _status_ зі значенням `"😎"`. Коли виконується `this.status`, `"😎"` логується.

</p>
</details>

---

###### 83. Що буде на виході?

```javascript
const person = {
  name: 'Lydia',
  age: 21,
};

let city = person.city;
city = 'Amsterdam';

console.log(person);
```

- A: `{ name: "Lydia", age: 21 }`
- B: `{ name: "Lydia", age: 21, city: "Amsterdam" }`
- C: `{ name: "Lydia", age: 21, city: undefined }`
- D: `"Amsterdam"`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Ми встановлюємо змінну `city` рівну значенню властивості під назвою `city` об’єкта `person`. Для цього об’єкта немає властивості під назвою `city`, тому змінна `city` має значення `undefined`.

Зауважте, що ми _не_ посилаємося на сам об’єкт `person`! Ми просто встановлюємо змінну `city` рівною поточному значенню властивості `city` об’єкта `person`.

Потім ми встановлюємо `city` рівним рядку `"Amsterdam"`. Це не змінює об’єкт person: немає посилання на цей об’єкт.

Під час логування об’єкта `person` повертається незмінений об’єкт.

</p>
</details>

---

###### 84. Що буде на виході?

```javascript
function checkAge(age) {
  if (age < 18) {
    const message = "Sorry, you're too young.";
  } else {
    const message = "Yay! You're old enough!";
  }

  return message;
}

console.log(checkAge(21));
```

- A: `"Sorry, you're too young."`
- B: `"Yay! You're old enough!"`
- C: `ReferenceError`
- D: `undefined`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Змінні з ключовими словами `const` і `let` є _блоковими_. Блок — це все, що знаходиться у фігурних дужках (`{ }`). У цьому випадку фігурні дужки операторів if/else. Ви не можете посилатися на змінну поза межами блоку, у якому вона оголошена, викидається ReferenceError.

</p>
</details>

---

###### 85. Яка інформація буде залогованою?

```javascript
fetch('https://www.website.com/api/user/1')
  .then(res => res.json())
  .then(res => console.log(res));
```

- A: Результат методу `fetch`.
- B: Результат другого виклику методу `fetch`.
- C: Результат колбеку в попередньому `.then()`. 
- D: Завжди undefined.

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Значення `res` у другому `.then` дорівнює поверненому значенню попереднього `.then`. Таким чином ми можемо продовжувати ланцюжок `.then`, де значення передається наступному обробнику.

</p>
</details>

---

###### 86. Яким способом можна встановити `hasName` рівним `true`, якщо ви не можете передати `true` як аргумент?

```javascript
function getName(name) {
  const hasName = //
}
```

- A: `!!name`
- B: `name`
- C: `new Boolean(name)`
- D: `name.length`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

За допомогою `!!name` ми визначаємо, чи значення `name` true чи false. Якщо `name` є значенням true, `!name` повертає `false`. `!false` (що фактично є `!!name`) повертає `true`.

Встановлюючи `hasName` рівним `name`, ми встановлюємо `hasName` рівним будь-якому значенню, яке ми передали функції `getName`, а не логічному значенню `true`.

`new Boolean(true)` повертає обгортку об’єкта, а не саме булеве значення.

`name.length` повертає довжину переданого аргументу, а не те, чи є він `true`.

</p>
</details>

---

###### 87. Що буде на виході?

```javascript
console.log('I want pizza'[0]);
```

- A: `"""`
- B: `"I"`
- C: `SyntaxError`
- D: `undefined`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Щоб отримати символ за певним індексом рядка, ми можемо використовувати позначення в дужках. Перший символ у рядку має індекс 0 і так далі. У цьому випадку ми хочемо отримати елемент з індексом 0, символ `"I"`, який логується.

Зауважте, що цей метод не підтримується в IE7 і нижче. У такому випадку використовуйте `.charAt()`.

</p>
</details>

---

###### 88. Що буде на виході?

```javascript
function sum(num1, num2 = num1) {
  console.log(num1 + num2);
}

sum(10);
```

- A: `NaN`
- B: `20`
- C: `ReferenceError`
- D: `undefined`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Ми можемо встановити значення параметра за замовчуванням рівним іншому параметру функції, якщо вони були визначені _перед_ параметром за замовчуванням. Ми передаємо значення `10` у функцію `sum`. Якщо функція `sum` отримує лише 1 аргумент, це означає, що значення `num2` не передається, а значення `num1` у цьому випадку дорівнює переданому значенню `10`. Значенням за замовчуванням `num2` є значення `num1`, яке дорівнює `10`. `num1 + num2` повертає `20`.

Якщо ми намагаємося встановити значення параметра за замовчуванням, що дорівнює параметру, визначеному _після_ (праворуч), значення параметра ще не ініціалізовано, що викличе помилку.

</p>
</details>

---

###### 89. Що буде на виході?

```javascript
// module.js
export default () => 'Hello world';
export const name = 'Lydia';

// index.js
import * as data from './module';

console.log(data);
```

- A: `{ default: function default(), name: "Lydia" }`
- B: `{ default: function default() }`
- C: `{ default: "Hello world", name: "Lydia" }`
- D: Глобальний об’єкт `module.js`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

За допомогою синтаксису `import * as name` ми імпортуємо _всі експорти_ з файлу `module.js` у файл `index.js`, коли створюється новий об’єкт під назвою `data`. У файлі `module.js` є два експорти: експорт за замовчуванням і іменований експорт. Експорт за замовчуванням — це функція, яка повертає рядок `"Hello World"`, а іменований експорт — це змінна `name`, яка має значення рядка `"Lydia"`.

Об’єкт `data` має властивість `default` для експорту за замовчуванням, інші властивості мають назви іменованих експортів та їхні відповідні значення.

</p>
</details>

---

###### 90. Що буде на виході?

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
}

const member = new Person('John');
console.log(typeof member);
```

- A: `"class"`
- B: `"function"`
- C: `"object"`
- D: `"string"`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Класи є синтаксичним цукром для конструкторів функцій. Еквівалентом класу `Person` як конструктора функції буде:

```javascript
function Person(name) {
  this.name = name;
}
```

Виклик конструктора функції з `new` призводить до створення екземпляра `Person`, ключове слово `typeof` повертає `"object"` для екземпляра. `typeof member` повертає `"object"`.

</p>
</details>

---

###### 91. Що буде на виході?

```javascript
let newList = [1, 2, 3].push(4);

console.log(newList.push(5));
```

- A: `[1, 2, 3, 4, 5]`
- B: `[1, 2, 3, 5]`
- C: `[1, 2, 3, 4]`
- D: `Error`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

Метод `.push` повертає _нову довжину_ масиву, а не сам масив! Встановлюючи `newList` рівним `[1, 2, 3].push(4)`, ми встановлюємо `newList` рівним новій довжині масиву: `4`.

Потім ми намагаємося використати метод `.push` для `newList`. Оскільки `newList` є числом `4`, ми не можемо використовувати метод `.push`: викидається TypeError.

</p>
</details>

---

###### 92. Що буде на виході?

```javascript
function giveLydiaPizza() {
  return 'Here is pizza!';
}

const giveLydiaChocolate = () =>
  "Here's chocolate... now go hit the gym already.";

console.log(giveLydiaPizza.prototype);
console.log(giveLydiaChocolate.prototype);
```

- A: `{ constructor: ...}` `{ constructor: ...}`
- B: `{}` `{ constructor: ...}`
- C: `{ constructor: ...}` `{}`
- D: `{ constructor: ...}` `undefined`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

Звичайні функції, такі як функція `giveLydiaPizza`, мають властивість `prototype`, яка є об’єктом (об’єктом-прототипом) із властивістю `constructor`. Однак стрілкова функція, така як функція `giveLydiaChocolate`, не має цієї властивості `prototype`. `undefined` повертається під час спроби отримати доступ до властивості `prototype` за допомогою `giveLydiaChocolate.prototype`.

</p>
</details>

---

###### 93. Що буде на виході?

```javascript
const person = {
  name: 'Lydia',
  age: 21,
};

for (const [x, y] of Object.entries(person)) {
  console.log(x, y);
}
```

- A: `name` `Lydia` та `age` `21`
- B: `["name", "Lydia"]` та `["age", 21]`
- C: `["name", "age"]` та `undefined`
- D: `Error`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

`Object.entries(person)` повертає масив вкладених масивів, що містить ключі та об’єкти:

`[ [ 'name', 'Lydia' ], [ 'age', 21 ] ]`

Використовуючи цикл for-of, ми можемо перебирати кожен елемент у масиві, у такому випадку підмасиви. Ми можемо миттєво деструктурувати підмасиви в циклі for-of, використовуючи `const [x, y]`. `x` дорівнює першому елементу підмасиву, `y` дорівнює другому елементу підмасиву.

Перший підмасив – це `[ "name", "Lydia" ]`, де `x` дорівнює `"name"`, а `y` дорівнює `"Lydia"`, які логуються.
Другий підмасив – це `[ "age", 21 ]`, де `x` дорівнює `"age"`, а `y` дорівнює `21`, які логуються.

</p>
</details>

---

###### 94. Що буде на виході?

```javascript
function getItems(fruitList, ...args, favoriteFruit) {
  return [...fruitList, ...args, favoriteFruit]
}

getItems(["banana", "apple"], "pear", "orange")
```

- A: `["banana", "apple", "pear", "orange"]`
- B: `[["banana", "apple"], "pear", "orange"]`
- C: `["banana", "apple", ["pear"], "orange"]`
- D: `SyntaxError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

`...args` є rest параметром. Значення rest параметра — це масив, що містить усі аргументи, що залишилися, **і може бути лише останнім параметром**! У цьому прикладі rest параметр був другим параметром. Це неможливо, і викличе синтаксичну помилку.

```javascript
function getItems(fruitList, favoriteFruit, ...args) {
  return [...fruitList, ...args, favoriteFruit];
}

getItems(['banana', 'apple'], 'pear', 'orange');
```

Наведений вище приклад працює. Він повертає масив`[ 'banana', 'apple', 'orange', 'pear' ]`

</p>
</details>

---

###### 95. Що буде на виході?

```javascript
function nums(a, b) {
  if (a > b) console.log('a is bigger');
  else console.log('b is bigger');
  return
  a + b;
}

console.log(nums(4, 2));
console.log(nums(1, 2));
```

- A: `a is bigger`, `6` та `b is bigger`, `3`
- B: `a is bigger`, `undefined` та `b is bigger`, `undefined`
- C: `undefined` та `undefined`
- D: `SyntaxError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

У JavaScript нам _не потрібно_ явно писати крапку з комою (`;`), однак рушій JavaScript все одно додає їх після інструкцій. Це називається **Автоматична вставка крапки з комою**. інструкції можуть бути, наприклад, змінні або ключові слова, як-от `throw`, `return`, `break` тощо.

Тут ми написали оператор `return` і ще одне значення `a + b` у _новому рядку_. Однак, оскільки це новий рядок, рушій не знає, що це насправді значення, яке ми хотіли повернути. Замість цього він автоматично додає крапку з комою після `return`. Ми можемо побачити це як:

```javascript
return;
a + b;
```

Це означає, що `a + b` ніколи не досягається, оскільки функція припиняє роботу після ключового слова `return`. Якщо значення не повертається, як тут, функція повертає `undefined`. Зауважте, що автоматичної вставки після операторів `if/else` немає!

</p>
</details>

---

###### 96. Що буде на виході?

```javascript
class Person {
  constructor() {
    this.name = 'Lydia';
  }
}

Person = class AnotherPerson {
  constructor() {
    this.name = 'Sarah';
  }
};

const member = new Person();
console.log(member.name);
```

- A: `"Lydia"`
- B: `"Sarah"`
- C: `Error: cannot redeclare Person`
- D: `SyntaxError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Ми можемо встановити класи рівними іншим класам/конструкторам функцій. У цьому випадку ми встановлюємо `Person` рівним `AnotherPerson`. Властивість name цього конструктора – `Sarah`, тому властивість name нового екземпляра `Person` теж `"Sarah"`.

</p>
</details>

---

###### 97. Що буде на виході?

```javascript
const info = {
  [Symbol('a')]: 'b',
};

console.log(info);
console.log(Object.keys(info));
```

- A: `{Symbol('a'): 'b'}` та `["{Symbol('a')"]`
- B: `{}` та `[]`
- C: `{ a: "b" }` та `["a"]`
- D: `{Symbol('a'): 'b'}` та `[]`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

Символ не є _перелічуваним_. Метод Object.keys повертає всі ключі об’єкта, які _перелічуються_. Символ буде невидимим, і буде повернуто порожній масив. Під час логування всього об’єкта всі властивості будуть видимі, навіть ті, що не перелічуються.

Це одна з багатьох властивостей символу: окрім представлення цілком унікального значення (що запобігає випадковій колізії імен об’єктів, наприклад, під час роботи з двома бібліотеками, які хочуть додати властивості до того самого об’єкта), ми також можемо "приховати" властивості об’єктів таким чином (хоча не повністю. Ми все ще можемо отримати доступ до символів за допомогою методу `Object.getOwnPropertySymbols()`).

</p>
</details>

---

###### 98. Що буде на виході?

```javascript
const getList = ([x, ...y]) => [x, y]
const getUser = user => { name: user.name, age: user.age }

const list = [1, 2, 3, 4]
const user = { name: "Lydia", age: 21 }

console.log(getList(list))
console.log(getUser(user))
```

- A: `[1, [2, 3, 4]]` та `SyntaxError`
- B: `[1, [2, 3, 4]]` та `{ name: "Lydia", age: 21 }`
- C: `[1, 2, 3, 4]` та `{ name: "Lydia", age: 21 }`
- D: `Error` та `{ name: "Lydia", age: 21 }`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Функція `getList` отримує масив як аргумент. Між дужками функції `getList` ми одразу деструктуруємо цей масив. Ви можете побачити це як:

`[x, ...y] = [1, 2, 3, 4]`

За допомогою параметра rest `...y` ми поміщаємо всі "залишкові" аргументи в масив. Решта аргументів у цьому випадку – це `2`, `3` та `4`. Значення `y` є масивом, що містить усі інші параметри. У цьому випадку значення `x` дорівнює `1`, тому, коли ми логуємо `[x, y]`, отримуємо `[1, [2, 3, 4]]`.

Функція `getUser` отримує об’єкт. З стрілковими функціями нам не _потрібно_ писати фігурні дужки, якщо ми повертаємо лише одне значення. Однак, якщо ми хочемо миттєво повернути _об’єкт_ зі стрілкової функції, ми повинні записати його в круглих дужках, інакше все, що знаходиться між двома дужками, буде інтерпретовано як інструкція блоку. У цьому випадку код у фігурних дужках не є дійсним кодом JavaScript, тому викидається `SyntaxError`.

Наступна функція повернула б об’єкт:

`const getUser = user => ({ name: user.name, age: user.age })`

</p>
</details>

---

###### 99. Що буде на виході?

```javascript
const name = 'Lydia';

console.log(name());
```

- A: `SyntaxError`
- B: `ReferenceError`
- C: `TypeError`
- D: `undefined`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Змінна `name` містить значення рядка, який не є функцією, тому її не можна викликати.

Помилки TypeErrors викидаються, коли значення не відповідає очікуваному типу. JavaScript очікував, що `name` буде функцією, оскільки ми намагаємося її викликати. Однак це був рядок, тому викидається TypeError: name is not a function!

Помилки SyntaxErrors виникають, коли ми написали щось, що не є дійсним JavaScript, наприклад, коли ми написали слово `return` як `retrun`.

Помилки ReferenceErrors викидаються, коли JavaScript не може знайти посилання на значення, до якого ми намагаємося отримати доступ.

</p>
</details>

---

###### 100. Яке значення output?

```javascript
// 🎉✨ This is my 100th question! ✨🎉

const output = `${[] && 'Im'}possible!
You should${'' && `n't`} see a therapist after so much JavaScript lol`;
```

- A: `possible! You should see a therapist after so much JavaScript lol`
- B: `Impossible! You should see a therapist after so much JavaScript lol`
- C: `possible! You shouldn't see a therapist after so much JavaScript lol`
- D: `Impossible! You shouldn't see a therapist after so much JavaScript lol`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

`[]` є значенням true. За допомогою оператора `&&` буде повернено значення справа, якщо значення ліворуч є true. У цьому випадку ліве значення `[]` є true, тому повертається `"Im"`.

`""` є значенням false. Якщо ліве значення є false, нічого не повертається. `n't` не повертається.

</p>
</details>

---

###### 101. Що буде на виході?

```javascript
const one = false || {} || null;
const two = null || false || '';
const three = [] || 0 || true;

console.log(one, two, three);
```

- A: `false` `null` `[]`
- B: `null` `""` `true`
- C: `{}` `""` `[]`
- D: `null` `null` `true`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

За допомогою оператора `||` ми можемо повернути перший правдивий операнд. Якщо всі значення хибні, повертається останній операнд.

`(false || {} || null)`: порожній об’єкт `{}` є значенням true. Це перше (і єдине) значення true, яке повертається. `one` дорівнює `{}`.

`(null || false || "")`: усі операнди є значеннями false. Це означає, що повертається останній операнд `""`. `two` дорівнює `""`.

`([] || 0 || "")`: порожній масив `[]` є значенням true. Це перше значення true, яке повертається. `three` дорівнює `[]`.

</p>
</details>

---

###### 102. Що буде на виході?

```javascript
const myPromise = () => Promise.resolve('I have resolved!');

function firstFunction() {
  myPromise().then(res => console.log(res));
  console.log('second');
}

async function secondFunction() {
  console.log(await myPromise());
  console.log('second');
}

firstFunction();
secondFunction();
```

- A: `I have resolved!`, `second` та `I have resolved!`, `second`
- B: `second`, `I have resolved!` та `second`, `I have resolved!`
- C: `I have resolved!`, `second` та `second`, `I have resolved!`
- D: `second`, `I have resolved!` та `I have resolved!`, `second`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

З промісами ми говоримо _я хочу виконати цю функцію, але поки що я відкладу її, поки вона працює, оскільки це може зайняти деякий час. Лише коли певне значення resolved (або rejected) і коли стек викликів порожній, я хочу використовувати це значення._

Ми можемо отримати це значення за допомогою ключового слова `.then` і `await` у функції `async`. Хоча ми можемо отримати значення проміса як за допомогою `.then`, так і `await`, вони працюють дещо інакше.

У `firstFunction` ми (начебто) відклали функцію myPromise, поки вона працювала, але продовжили виконувати інший код, у цьому випадку `console.log('second')`. Потім функція resolved з рядком `I have resolved`, який залогувався після того, як стек викликів спорожнів.

За допомогою ключового слова await у `secondFunction` ми буквально призупиняємо виконання асинхронної функції, доки значення не буде resolved перед переходом до наступного рядка.

Це означає, що вона чекала, поки `myPromise` resolved зі значенням `I have resolved`, і лише коли це сталося, ми перейшли до наступного рядка: `second` залогувався.

</p>
</details>

---

###### 103. Що буде на виході?

```javascript
const set = new Set();

set.add(1);
set.add('Lydia');
set.add({ name: 'Lydia' });

for (let item of set) {
  console.log(item + 2);
}
```

- A: `3`, `NaN`, `NaN`
- B: `3`, `7`, `NaN`
- C: `3`, `Lydia2`, `[object Object]2`
- D: `"12"`, `Lydia2`, `[object Object]2`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Оператор `+` використовується не тільки для додавання числових значень, але ми також можемо використовувати його для об'єднання рядків. Щоразу, коли рушій JavaScript бачить, що одне чи кілька значень не є числом, він перетворює число в рядок.

Перше це число `1`. `1 + 2`повертає число 3.

Однак другий — рядок `"Lydia"`. `"Lydia"` є рядком, а `2` — числом: `2` перетворюється на рядок. `"Lydia"` і `"2"` конкатенуються, що призводить до рядка `"Lydia2"`.

`{ name: "Lydia" }` є об’єктом. Ані число, ані об’єкт не є рядком, тому він об’єднує обидва. Кожного разу, коли ми перетворюємо звичайний об’єкт у рядок, він перетворюється на `"[object Object]"`. `"[object Object]"` об'єднаний з `"2"` стає `"[object Object]2"`.

</p>
</details>

---

###### 104. Яким буде його значення?

```javascript
Promise.resolve(5);
```

- A: `5`
- B: `Promise {<pending>: 5}`
- C: `Promise {<fulfilled>: 5}`
- D: `Error`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Ми можемо передати в `Promise.resolve` значення будь-якого типу, проміс чи не проміс. Сам метод повертає проміс з resolved значенням (`<fulfilled>`). Якщо ми передаємо звичайну функцію, це буде resolved проміс зі звичайним значенням. Якщо ми передаємо проміс, це буде resolved проміс з resolved значенням цього переданого проміса.

У цьому випадку ми просто передали числове значення `5`. Він повертає resolved проміс зі значенням `5`.

</p>
</details>

---

###### 105. Що буде на виході?

```javascript
function compareMembers(person1, person2 = person) {
  if (person1 !== person2) {
    console.log('Not the same!');
  } else {
    console.log('They are the same!');
  }
}

const person = { name: 'Lydia' };

compareMembers(person);
```

- A: `Not the same!`
- B: `They are the same!`
- C: `ReferenceError`
- D: `SyntaxError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Об'єкти передаються за посиланням. Коли ми перевіряємо об’єкти на точну рівність (`===`), ми порівнюємо їхні посилання.

Ми встановили значення за замовчуванням для `person2` рівним об’єкту `person` і передали об’єкт `person` як значення для `person1`.

Це означає, що обидва значення мають посилання на одне й те саме місце в пам’яті, отже, вони рівні.

Блок коду в операторі `else` виконується і `They are the same!` логується.

</p>
</details>

---

###### 106. Яке його значення?

```javascript
const colorConfig = {
  red: true,
  blue: false,
  green: true,
  black: true,
  yellow: false,
};

const colors = ['pink', 'red', 'blue'];

console.log(colorConfig.colors[1]);
```

- A: `true`
- B: `false`
- C: `undefined`
- D: `TypeError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

У JavaScript є два способи доступу до властивостей об’єкта: нотація в дужках або нотація з крапками. У цьому прикладі ми використовуємо крапкову нотацію (`colorConfig.colors`) замість нотації в дужках (`colorConfig["colors"]`).

За допомогою крапкової нотації JavaScript намагається знайти властивість об’єкта з таким іменем. У цьому прикладі JavaScript намагається знайти властивість під назвою `colors` в об’єкті `colorConfig`. Немає властивості під назвою `colors`, тому повертається `undefined`. Потім ми намагаємося отримати доступ до значення першого елемента за допомогою `[1]`. Ми не можемо зробити це для значення, яке є `undefined`, тому викидається `TypeError`: `Cannot read property '1' of undefined`.

JavaScript інтерпретує (або розпаковує) інструкції. Коли ми використовуємо нотацію в дужках, він бачить першу дужку, яка відкривається `[` і продовжує, доки не знайде дужку, яка закривається `]`. Тільки після цього він виконає інструкцію. Якби ми використали `colorConfig[colors[1]]`, він повернув би значення властивості `red` об'єкта `colorConfig`.

</p>
</details>

---

###### 107. Що буде на виході?

```javascript
console.log('❤️' === '❤️');
```

- A: `true`
- B: `false`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Під капотом емодзі — це юнікоди. Юнікод для емодзі серця: `"U+2764 U+FE0F"`. Вони завжди однакові для одних і тих самих емодзі, тому ми порівнюємо два однакові рядки один з одним, що повертає true.

</p>
</details>

---

###### 108. Які із цих методів змінюють масив?

```javascript
const emojis = ['✨', '🥑', '😍'];

emojis.map(x => x + '✨');
emojis.filter(x => x !== '🥑');
emojis.find(x => x !== '🥑');
emojis.reduce((acc, cur) => acc + '✨');
emojis.slice(1, 2, '✨');
emojis.splice(1, 2, '✨');
```

- A: `Усі`
- B: `map` `reduce` `slice` `splice`
- C: `map` `slice` `splice`
- D: `splice`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

За допомогою методу `splice` ми змінюємо оригінальний масив, видаляючи, замінюючи або додаючи елементи. У цьому випадку ми видалили 2 елементи з 1 індексу (ми видалили `'🥑'` і `'😍'`) і натомість додали емодзі ✨.

`map`, `filter` і `slice` повертають новий масив, `find` повертає елемент, а `reduce` повертає одне значення.

</p>
</details>

---

###### 109. Що буде на виході?

```javascript
const food = ['🍕', '🍫', '🥑', '🍔'];
const info = { favoriteFood: food[0] };

info.favoriteFood = '🍝';

console.log(food);
```

- A: `['🍕', '🍫', '🥑', '🍔']`
- B: `['🍝', '🍫', '🥑', '🍔']`
- C: `['🍝', '🍕', '🍫', '🥑', '🍔']`
- D: `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Ми встановлюємо значення властивості `favoriteFood` об’єкта `info` рівним рядку з емодзі піци `'🍕'`. Рядок є примітивним типом даних. У JavaScript примітивні типи даних не працюють за посиланням.

У JavaScript примітивні типи даних (все, що не є об’єктами) працюють за _значенням_. У цьому випадку ми встановлюємо значення властивості `favoriteFood` для об’єкта `info` що дорівнює значенню першого елемента в масиві `food`, у цьому випадку це рядок з емодзі піци (`'🍕'`). Рядок є примітивним типом даних і взаємодіє за значенням (перегляньте мій [допис](https://www.theavocoder.com/complete-javascript/2018/12/21/by-value-vs-by-reference) якщо вам цікаво дізнатися більше).

Потім ми змінюємо значення властивості `favoriteFood` в об’єкті `info`. Масив `food` не змінився, оскільки значення `favoriteFood` є лише _копією_ значення першого елемента в масиві та не має посилання на те саме місце в пам’яті, що й елемент у `food[0]`. Коли ми логуємо food, це все ще оригінальний масив, `['🍕', '🍫', '🥑', '🍔']`.

</p>
</details>

---

###### 110. Що робить цей метод?

```javascript
JSON.parse();
```

- A: Розбирає JSON до JavaScript значення
- B: Розбирає об’єкт JavaScript до JSON
- C: Розбирає будь-яке значення JavaScript у JSON
- D: Розбирає JSON лише до об’єкта JavaScript

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

За допомогою методу `JSON.parse()` ми можемо розбирати рядок JSON до значення JavaScript.

```javascript
// Перетворення числа в коректний JSON, а потім розбір рядка JSON до значення JavaScript:
const jsonNumber = JSON.stringify(4); // '4'
JSON.parse(jsonNumber); // 4

// Перетворення масиву в коректний JSON, а потім розбір рядка JSON до значення JavaScript:
const jsonArray = JSON.stringify([1, 2, 3]); // '[1, 2, 3]'
JSON.parse(jsonArray); // [1, 2, 3]

// Перетворення об’єкта у коректний JSON, а потім розбір рядка JSON до значення JavaScript:
const jsonArray = JSON.stringify({ name: 'Lydia' }); // '{"name":"Lydia"}'
JSON.parse(jsonArray); // { name: 'Lydia' }
```

</p>
</details>

---

###### 111. Що буде на виході?

```javascript
let name = 'Lydia';

function getName() {
  console.log(name);
  let name = 'Sarah';
}

getName();
```

- A: Lydia
- B: Sarah
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

Кожна функція має власний _контекст виконання_ (або _scope_). Функція `getName` спочатку шукає у своєму власному контексті (scope) щоб перевірити, чи містить вона змінну `name`, до якої ми намагаємося отримати доступ. У цьому випадку функція `getName` містить власну змінну `name`: ми оголошуємо змінну `name` за допомогою ключового слова `let` зі значенням `'Sarah'`.

Змінні з ключовим словом `let` (як і `const`) підіймаються (hoist), але, на відміну від `var`, не _ініціалізуються_. Вони недоступні до рядка, в якому ми їх оголошуємо (ініціалізуємо). Це називається "тимчасова мертва зона". Коли ми намагаємося отримати доступ до змінних до їх оголошення, JavaScript викидає `ReferenceError`.

Якби ми не оголосили змінну `name` у функції `getName`, рушій JavaScript переглянув би _ланцюжок області видимості_. Зовнішня область видимості має змінну під назвою `name` зі значенням `Lydia`. У цьому випадку було б залоговано `Lydia`.

```javascript
let name = 'Lydia';

function getName() {
  console.log(name);
}

getName(); // Lydia
```

</p>
</details>

---

###### 112. Що буде на виході?

```javascript
function* generatorOne() {
  yield ['a', 'b', 'c'];
}

function* generatorTwo() {
  yield* ['a', 'b', 'c'];
}

const one = generatorOne();
const two = generatorTwo();

console.log(one.next().value);
console.log(two.next().value);
```

- A: `a` та `a`
- B: `a` та `undefined`
- C: `['a', 'b', 'c']` та `a`
- D: `a` та `['a', 'b', 'c']`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

За допомогою ключового слова `yield` ми `повертаємо` значення у функції-генератор. За допомогою ключового слова `yield*` ми можемо отримати значення з іншої функції-генератора або об’єкта, який перебирається (наприклад, масиву).

У `generatorOne` ми повертаємо весь масив `['a', 'b', 'c']` за допомогою ключового слова `yield`. Значення властивості `value` об’єкта, повернутого методом `next` у `one` (`one.next().value`) дорівнює всьому масиву `['a', 'b', 'c']`.

```javascript
console.log(one.next().value); // ['a', 'b', 'c']
console.log(one.next().value); // undefined
```

У `generatorTwo` ми використовуємо ключове слово `yield*`. Це означає, що перше отримане значення `two` дорівнює першому отриманому значенню в ітераторі. Ітератором є масив `['a', 'b', 'c']`. Першим отриманим значенням є `a`, тому під час першого виклику `two.next().value` повертається `a`.

```javascript
console.log(two.next().value); // 'a'
console.log(two.next().value); // 'b'
console.log(two.next().value); // 'c'
console.log(two.next().value); // undefined
```

</p>
</details>

---

###### 113. Що буде на виході?

```javascript
console.log(`${(x => x)('I love')} to program`);
```

- A: `I love to program`
- B: `undefined to program`
- C: `${(x => x)('I love') to program`
- D: `TypeError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Вирази в шаблонних літералах виконуються першими. Це означає, що рядок міститиме повернуте значення виразу, у цьому випадку негайно викликану функцію `(x => x)('I love')`. Ми передаємо значення `'I love'` як аргумент стрілкової функції `x => x`. `x` дорівнює `'I love'`, яке повертається. Це призводить до `I love to program`.

</p>
</details>

---

###### 114. Що станеться?

```javascript
let config = {
  alert: setInterval(() => {
    console.log('Alert!');
  }, 1000),
};

config = null;
```

- A: `setInterval` колбек не буде викликано
- B: `setInterval` колбек викликається один раз
- C: `setInterval` колбек буде викликатися щосекунди
- D: Ми ніколи не викликали `config.alert()`, config має значення `null`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Зазвичай, коли ми встановлюємо об’єкти рівними `null`, ці об’єкти витираються _збирачем сміття_, оскільки на цей об’єкт більше немає посилань. Однак, оскільки колбек функція в `setInterval` є стрілковою функцією (таким чином пов’язана з об’єктом `config`), колбек функція все ще містить посилання на об’єкт `config`.
Поки є посилання, об’єкт не витирається збирачем сміття.
Оскільки це інтервал, встановлення `config` на `null` або `delete` `config.alert` не зітре інтервал, тому інтервал усе одно буде викликано.
Його слід очистити за допомогою `clearInterval(config.alert)`, щоб видалити його з пам’яті.
Оскільки його не було очищено, колбек функція `setInterval` все одно буде викликатися кожні 1000 мс (1 с).

</p>
</details>

---

###### 115. Який метод(и) поверне значення `'Hello world!'`?

```javascript
const myMap = new Map();
const myFunc = () => 'greeting';

myMap.set(myFunc, 'Hello world!');

//1
myMap.get('greeting');
//2
myMap.get(myFunc);
//3
myMap.get(() => 'greeting');
```

- A: 1
- B: 2
- C: 2 та 3
- D: Усі

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Під час додавання пари ключ/значення за допомогою методу `set` ключ буде значенням першого аргументу, переданого функції `set`, а значенням буде другим аргументом, переданим функції `set`. Ключем є _функція_ `() => 'greeting'` та значення `'Hello world'`. `myMap` тепер `{ () => 'greeting' => 'Hello world!' }`.

1 неправильний, оскільки ключ не `'greeting'`, а `() => 'greeting'`.

3 є неправильним, оскільки ми створюємо нову функцію, передаючи її як параметр методу `get`. Об’єкт взаємодіє за _посиланням_. Функції — це об’єкти, тому дві функції ніколи не бувають рівними, навіть якщо вони ідентичні: вони мають посилання на різне місце в пам’яті.

</p>
</details>

---

###### 116. Що буде на виході?

```javascript
const person = {
  name: 'Lydia',
  age: 21,
};

const changeAge = (x = { ...person }) => (x.age += 1);
const changeAgeAndName = (x = { ...person }) => {
  x.age += 1;
  x.name = 'Sarah';
};

changeAge(person);
changeAgeAndName();

console.log(person);
```

- A: `{name: "Sarah", age: 22}`
- B: `{name: "Sarah", age: 23}`
- C: `{name: "Lydia", age: 22}`
- D: `{name: "Lydia", age: 23}`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Обидві функції `changeAge` і `changeAgeAndName` мають параметр за замовчуванням, а саме _новостворений_ об’єкт `{ ...person }`. Цей об’єкт містить копії всіх ключів/значень в об’єкті  `person`.

Спочатку ми викликаємо функцію `changeAge` і передаємо об’єкт `person` як її аргумент. Ця функція збільшує значення властивості `age` на 1. `person` тепер `{ name: "Lydia", age: 22 }`.

Потім ми викликаємо функцію `changeAgeAndName`, однак ми не передаємо параметр. Натомість значення `x` дорівнює _новому_ об’єкту: `{ ...person }`. Оскільки це новий об’єкт, він не впливає на значення властивостей об’єкта `person`. `person` досі дорівнює `{ name: "Lydia", age: 22 }`.

</p>
</details>

---

###### 117. Який із наведених нижче варіантів поверне `6`?

```javascript
function sumValues(x, y, z) {
  return x + y + z;
}
```

- A: `sumValues([...1, 2, 3])`
- B: `sumValues([...[1, 2, 3]])`
- C: `sumValues(...[1, 2, 3])`
- D: `sumValues([1, 2, 3])`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

За допомогою оператора поширення `...` ми можемо _поширювати_ об’єкти, які перебираються на окремі елементи. Функція `sumValues` отримує три аргументи: `x`, `y` та `z`. `...[1, 2, 3]` призведе до `1, 2, 3`, яке ми передаємо функції `sumValues`.

</p>
</details>

---

###### 118. Що буде на виході?

```javascript
let num = 1;
const list = ['🥳', '🤠', '🥰', '🤪'];

console.log(list[(num += 1)]);
```

- A: `🤠`
- B: `🥰`
- C: `SyntaxError`
- D: `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

За допомогою оператора `+=` ми збільшуємо значення `num` на `1`. `num` мало початкове значення `1`, тому `1 + 1` дорівнює `2`. Елемент у другому індексі в масиві `list` — це 🥰, `console.log(list[2])` логує 🥰.

</p>
</details>

---

###### 119. Що буде на виході?

```javascript
const person = {
  firstName: 'Lydia',
  lastName: 'Hallie',
  pet: {
    name: 'Mara',
    breed: 'Dutch Tulip Hound',
  },
  getFullName() {
    return `${this.firstName} ${this.lastName}`;
  },
};

console.log(person.pet?.name);
console.log(person.pet?.family?.name);
console.log(person.getFullName?.());
console.log(member.getLastName?.());
```

- A: `undefined` `undefined` `undefined` `undefined`
- B: `Mara` `undefined` `Lydia Hallie` `ReferenceError`
- C: `Mara` `null` `Lydia Hallie` `null`
- D: `null` `ReferenceError` `null` `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

За допомогою оператора опціонального ланцюжка `?.`, нам більше не потрібно явно перевіряти, чи дійсні глибші вкладені значення. Якщо ми намагаємося отримати доступ до властивості зі значенням `undefined` або `null` (_nullish_), вираз замикається і повертає `undefined`.

`person.pet?.name`: `person` має властивість під назвою `pet`: `person.pet` не є значенням nullish. Він має властивість під назвою `name` і повертає `Mara`.

`person.pet?.family?.name`: `person` має властивість під назвою `pet`: `person.pet` не є значенням nullish. `pet` _не_ має властивості під назвою `family`, `person.pet.family` є значенням nullish. Вираз повертає `undefined`.

`person.getFullName?.()`: `person` має властивість під назвою `getFullName`: `person.getFullName()` не є значенням nullish і його можна викликати, що повертає `Lydia Hallie`.

`member.getLastName?.()`: змінна `member` не існує, тому викидається `ReferenceError`!

</p>
</details>

---

###### 120. Що буде на виході?

```javascript
const groceries = ['banana', 'apple', 'peanuts'];

if (groceries.indexOf('banana')) {
  console.log('We have to buy bananas!');
} else {
  console.log(`We don't have to buy bananas!`);
}
```

- A: `We have to buy bananas!`
- B: `We don't have to buy bananas`
- C: `undefined`
- D: `1`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Ми передали умову `groceries.indexOf("banana")` оператору if. `groceries.indexOf("banana")` повертає `0`, що є значенням false. Оскільки умова в операторі if є false, виконується код у блоці `else`, і логується `We don't have to buy bananas!`.

</p>
</details>

---

###### 121. Що буде на виході?

```javascript
const config = {
  languages: [],
  set language(lang) {
    return this.languages.push(lang);
  },
};

console.log(config.language);
```

- A: `function language(lang) { this.languages.push(lang }`
- B: `0`
- C: `[]`
- D: `undefined`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

Метод `language` — це `сетер`. Сетери не зберігають фактичне значення, їхнє призначення — _змінювати_ властивості. Під час виклику `сетеру` повертається `undefined`.

</p>
</details>

---

###### 122. Що буде на виході?

```javascript
const name = 'Lydia Hallie';

console.log(!typeof name === 'object');
console.log(!typeof name === 'string');
```

- A: `false` `true`
- B: `true` `false`
- C: `false` `false`
- D: `true` `true`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

`typeof name` повертає `"string"`. Рядок `"string"` є значенням true, тому `!typeof name` повертає булеве значення `false`. `false === "object"` і `false === "string"` повертають `false`.

(Якщо ми хотіли перевірити, чи тип (не)відповідає певному типу, ми повинні були написати `!==` замість `!typeof`)

</p>
</details>

---

###### 123. Що буде на виході?

```javascript
const add = x => y => z => {
  console.log(x, y, z);
  return x + y + z;
};

add(4)(5)(6);
```

- A: `4` `5` `6`
- B: `6` `5` `4`
- C: `4` `function` `function`
- D: `undefined` `undefined` `6`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Функція `add` повертає стрілкову функцію, яка повертає стрілкову функцію, яка повертає стрілкову функцію (все ще зі мною?). Перша функція отримує аргумент `x` зі значенням `4`. Ми викликаємо другу функцію, яка отримує аргумент `y` зі значенням `5`. Потім ми викликаємо третю функцію, яка отримує аргумент `z` зі значенням `6`. Коли ми намагаємося отримати доступ до значення `x`, `y` та `z` в останній стрілковій функції, рушій JS підіймається вгору по ланцюжку області видимості, щоб знайти значення для `x` та `y`. Це повертає `4` `5` `6`.

</p>
</details>

---

###### 124. Що буде на виході?

```javascript
async function* range(start, end) {
  for (let i = start; i <= end; i++) {
    yield Promise.resolve(i);
  }
}

(async () => {
  const gen = range(1, 3);
  for await (const item of gen) {
    console.log(item);
  }
})();
```

- A: `Promise {1}` `Promise {2}` `Promise {3}`
- B: `Promise {<pending>}` `Promise {<pending>}` `Promise {<pending>}`
- C: `1` `2` `3`
- D: `undefined` `undefined` `undefined`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Функція-генератор `range` повертає асинхронний об’єкт із промісами для кожного елемента діапазону, який ми передаємо: `Promise{1}`, `Promise{2}`, `Promise{3}`. Ми встановлюємо змінну `gen` рівною асинхронному об’єкту, після чого виконуємо цикл, використовуючи `for await ... of`. Ми встановлюємо змінну `item` рівною поверненим значенням промісу: спочатку `Promise{1}`, потім `Promise{2}`, потім `Promise{3}`. Оскільки ми _await_ на значення `item`, закінчений (resolved) проміс зі _значеннями_ повертається: `1`, `2`, та `3`.

</p>
</details>

---

###### 125. Що буде на виході?

```javascript
const myFunc = ({ x, y, z }) => {
  console.log(x, y, z);
};

myFunc(1, 2, 3);
```

- A: `1` `2` `3`
- B: `{1: 1}` `{2: 2}` `{3: 3}`
- C: `{ 1: undefined }` `undefined` `undefined`
- D: `undefined` `undefined` `undefined`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

`myFunc` очікує об’єкт із властивостями `x`, `y` і `z` як аргумент. Оскільки ми передаємо лише три окремі числові значення (1, 2, 3) замість одного об’єкта з властивостями `x`, `y` та `z` ({x: 1, y: 2, z: 3}), `x`, `y` та `z` мають значення за замовчуванням `undefined`.

</p>
</details>

---

###### 126. Що буде на виході?

```javascript
function getFine(speed, amount) {
  const formattedSpeed = new Intl.NumberFormat('en-US', {
    style: 'unit',
    unit: 'mile-per-hour'
  }).format(speed);

  const formattedAmount = new Intl.NumberFormat('en-US', {
    style: 'currency',
    currency: 'USD'
  }).format(amount);

  return `The driver drove ${formattedSpeed} and has to pay ${formattedAmount}`;
}

console.log(getFine(130, 300))
```

- A: The driver drove 130 and has to pay 300
- B: The driver drove 130 mph and has to pay \$300.00
- C: The driver drove undefined and has to pay undefined
- D: The driver drove 130.00 and has to pay 300.00

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

За допомогою методу `Intl.NumberFormat` ми можемо форматувати числові значення до будь-якої локалі. Ми форматуємо числове значення `130` до локалі `en-US` як `unit` в `mile-per-hour`, що призводить до `130 mph`. Числове значення `300` для локалі `en-US` як `currency` в `USD` призводить до `$300.00`.

</p>
</details>

---

###### 127. Що буде на виході?

```javascript
const spookyItems = ['👻', '🎃', '🕸'];
({ item: spookyItems[3] } = { item: '💀' });

console.log(spookyItems);
```

- A: `["👻", "🎃", "🕸"]`
- B: `["👻", "🎃", "🕸", "💀"]`
- C: `["👻", "🎃", "🕸", { item: "💀" }]`
- D: `["👻", "🎃", "🕸", "[object Object]"]`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Деструктуруючи об’єкти, ми можемо розпаковувати значення з правого об’єкта та призначати це розпаковане значення значенню властивості з таким самим іменем у лівому об’єкті. У цьому випадку ми присвоюємо значення "💀" для `spookyItems[3]`. Це означає, що ми змінюємо масив `spookyItems`, ми додаємо до нього "💀". Коли ми логуємо `spookyItems`, дістаємо `["👻", "🎃", "🕸", "💀"]`.

</p>
</details>

---

###### 128. Що буде на виході?

```javascript
const name = 'Lydia Hallie';
const age = 21;

console.log(Number.isNaN(name));
console.log(Number.isNaN(age));

console.log(isNaN(name));
console.log(isNaN(age));
```

- A: `true` `false` `true` `false`
- B: `true` `false` `false` `false`
- C: `false` `false` `true` `false`
- D: `false` `true` `false` `true`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

За допомогою методу `Number.isNaN` ми можемо перевірити, чи значення, яке ми передаємо, є _числовим значенням_ і дорівнює `NaN`. `name` не є числовим значенням, тому `Number.isNaN(name)` повертає `false`. `age` — це числове значення, але не дорівнює `NaN`, тому `Number.isNaN(age)` повертає `false`.

За допомогою методу `isNaN` ми можемо перевірити, чи значення, яке ми передаємо, не є числом. `name` не є числом, тому `isNaN(name)` повертає `true`. `age` є числом, тому `isNaN(age)` повертає `false`.

</p>
</details>

---

###### 129. Що буде на виході?

```javascript
const randomValue = 21;

function getInfo() {
  console.log(typeof randomValue);
  const randomValue = 'Lydia Hallie';
}

getInfo();
```

- A: `"number"`
- B: `"string"`
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

Змінні, оголошені за допомогою ключового слова `const` не можуть використовуватись до їх ініціалізації: це називається _тимчасова мертва зона_. У функції `getInfo` змінна `randomValue` знаходиться у області видимості `getInfo`. У рядку, де ми хочемо залогувати значення `typeof randomValue`, змінна `randomValue` ще не ініціалізована: викидається `ReferenceError`! Рушій JavaScript не шукав у ланцюжку області видимості, оскільки ми оголосили змінну `randomValue` у функції `getInfo`.

</p>
</details>

---

###### 130. Що буде на виході?

```javascript
const myPromise = Promise.resolve('Woah some cool data');

(async () => {
  try {
    console.log(await myPromise);
  } catch {
    throw new Error(`Oops didn't work`);
  } finally {
    console.log('Oh finally!');
  }
})();
```

- A: `Woah some cool data`
- B: `Oh finally!`
- C: `Woah some cool data` `Oh finally!`
- D: `Oops didn't work` `Oh finally!`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

У блоці `try` ми логуємо await значення змінної `myPromise`: `"Woah some cool data"`. Оскільки в блоці `try` не виникло помилок, код у блоці `catch` не виконується. Код у блоці `finally` _завжди_ виконується, `"Oh finally!"` логується у консоль.

</p>
</details>

---

###### 131. Що буде на виході?

```javascript
const emojis = ['🥑', ['✨', '✨', ['🍕', '🍕']]];

console.log(emojis.flat(1));
```

- A: `['🥑', ['✨', '✨', ['🍕', '🍕']]]`
- B: `['🥑', '✨', '✨', ['🍕', '🍕']]`
- C: `['🥑', ['✨', '✨', '🍕', '🍕']]`
- D: `['🥑', '✨', '✨', '🍕', '🍕']`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

За допомогою методу `flat` ми можемо створити новий плоский масив з багатовимірного. Глибина плоского масиву залежить від значення, яке ми передаємо. У цьому випадку ми передали значення `1` (чого ми могли б не робити, це значення за замовчуванням), що означає, що лише масиви на першій глибині будуть об’єднані. `['🥑']` та `['✨', '✨', ['🍕', '🍕']]` в цьому випадку. Об’єднання цих двох масивів призводить до `['🥑', '✨', '✨', ['🍕', '🍕']]`.

</p>
</details>

---

###### 132. Що буде на виході?

```javascript
class Counter {
  constructor() {
    this.count = 0;
  }

  increment() {
    this.count++;
  }
}

const counterOne = new Counter();
counterOne.increment();
counterOne.increment();

const counterTwo = counterOne;
counterTwo.increment();

console.log(counterOne.count);
```

- A: `0`
- B: `1`
- C: `2`
- D: `3`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

`counterOne` є екземпляром класу `Counter`. Клас `Counter` містить властивість `count` у своєму конструкторі та метод `increment`. Спочатку ми двічі викликали метод `increment`, виконавши `counterOne.increment()`. Наразі `counterOne.count` дорівнює `2`.

<img src="https://i.imgur.com/KxLlTm9.png" width="400">

Потім ми створюємо нову змінну `counterTwo` і встановлюємо їй значення `counterOne`. Оскільки об’єкти взаємодіють за посиланням, ми просто створюємо нове посилання на те саме місце в пам’яті, на яке вказує `counterOne`. Оскільки він має те саме місце в пам’яті, будь-які зміни, внесені до об’єкта, на який посилається `counterTwo`, також застосовуються до `counterOne`. Наразі `counterTwo.count` дорівнює `2`.

Ми викликаємо `counterTwo.increment()`, який змінює `count` на `3`. Потім ми логуємо count у `counterOne`, який повертає `3`.

<img src="https://i.imgur.com/BNBHXmc.png" width="400">

</p>
</details>

---

###### 133. Що буде на виході?

```javascript
const myPromise = Promise.resolve(Promise.resolve('Promise'));

function funcOne() {
  setTimeout(() => console.log('Timeout 1!'), 0);
  myPromise.then(res => res).then(res => console.log(`${res} 1!`));
  console.log('Last line 1!');
}

async function funcTwo() {
  const res = await myPromise;
  console.log(`${res} 2!`)
  setTimeout(() => console.log('Timeout 2!'), 0);
  console.log('Last line 2!');
}

funcOne();
funcTwo();
```

- A: `Promise 1! Last line 1! Promise 2! Last line 2! Timeout 1! Timeout 2!`
- B: `Last line 1! Timeout 1! Promise 1! Last line 2! Promise2! Timeout 2! `
- C: `Last line 1! Promise 2! Last line 2! Promise 1! Timeout 1! Timeout 2!`
- D: `Timeout 1! Promise 1! Last line 1! Promise 2! Timeout 2! Last line 2!`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Спочатку ми викликаємо `funcOne`. У першому рядку `funcOne` ми викликаємо _асинхронну_ функцію `setTimeout`, з якої колбек надсилається до Web API. (перегляньте мою статтю про event loop <a href="https://dev.to/lydiahallie/javascript-visualized-event-loop-3dif">тут</a>.)

Потім ми викликаємо `myPromise` проміс, який є _асинхронною_ операцією.

І проміс, і тайм-аут є асинхронними операціями, функція продовжує працювати, поки виконується проміс та обробляється колбек `setTimeout`. Це означає, що `Last line 1!` логується першим, оскільки це не асинхронна операція.

Оскільки стек викликів ще не порожній, функцію `setTimeout` і проміс в `funcOne` ще не можна додати до стеку викликів.

У `funcTwo` змінна `res` отримує `Проміс`, тому що `Promise.resolve(Promise.resolve('Promise'))` еквівалентна `Promise.resolve('Promise')`, оскільки Promise.resolve просто resolve його значення. `await` у цьому рядку зупиняє виконання функції, доки проміс не вирішиться, а потім продовжує працювати синхронно до завершення, тому `Promise 2!`, а потім `Last line 2!` логуються, а `setTimeout` надсилається до Web API.

Далі стек викликів стає порожнім. Проміси є _мікрозадачами_, тому вони вирішуються першими, коли стек викликів порожній, `Promise 1!` логується.

Тепер, оскільки `funcTwo` не в стеку викликів, стек викликів порожній. Колбеки, які очікують у черзі (`() => console.log("Timeout 1!")` з `funcOne`, і `() => console.log("Timeout 2!")` з `funcTwo`) додалися до стеку викликів один за одним. Перший колбек логує `Timeout 1!` і очищається зі стеку. Потім другий колбек логує `Timeout 2!` і теж видаляється зі стеку.

</p>
</details>

---

###### 134. Як ми можемо викликати `sum` з `sum.js` у `index.js?`

```javascript
// sum.js
export default function sum(x) {
  return x + x;
}

// index.js
import * as sum from './sum';
```

- A: `sum(4)`
- B: `sum.sum(4)`
- C: `sum.default(4)`
- D: Експорти за замовчуванням не імпортуються з `*`, лише іменовані експорти

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Із зірочкою `*` ми імпортуємо всі експортовані значення з цього файлу, як за замовчуванням, так і іменовані. Якби у нас був такий файл:

```javascript
// info.js
export const name = 'Lydia';
export const age = 21;
export default 'I love JavaScript';

// index.js
import * as info from './info';
console.log(info);
```

Буде залоговано наступне:

```javascript
{
  default: "I love JavaScript",
  name: "Lydia",
  age: 21
}
```

Для прикладу `sum` це означає, що імпортоване значення `sum` виглядає так:

```javascript
{ default: function sum(x) { return x + x } }
```

Ми можемо викликати цю функцію за допомогою `sum.default`

</p>
</details>

---

###### 135. Що буде на виході?

```javascript
const handler = {
  set: () => console.log('Added a new property!'),
  get: () => console.log('Accessed a property!'),
};

const person = new Proxy({}, handler);

person.name = 'Lydia';
person.name;
```

- A: `Added a new property!`
- B: `Accessed a property!`
- C: `Added a new property!` `Accessed a property!`
- D: Нічого не буде залоговано

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

За допомогою об’єкта `Proxy` ми можемо додати спеціальну поведінку до об’єкта, який ми передаємо йому як другий аргумент. У цьому випадку ми передаємо об’єкт `handler`, який містить дві властивості: `set` і `get`. `set` викликається щоразу, коли ми _встановлюємо_ значення властивості, `get` викликається щоразу, коли ми _отримуємо_ (доступаємося до) значення властивості.

Перший аргумент – це порожній об’єкт `{}`, який є значенням `person`. До цього об’єкта додається спеціальна поведінка, вказана в об’єкті `handler`. Якщо ми додамо властивість до об’єкта `person`, буде викликано `set`. Якщо ми доступаємося до властивості об’єкта `person`, буде викликано `get`.

Спочатку ми додали нову властивість `name` до проксі-об’єкта (`person.name = "Lydia"`). Викликається `set` і логується `"Added a new property!"`.

Потім ми доступаємося до значення властивості проксі-об’єкта, викликається властивість `get`. Логується `"Accessed a property!"`.

</p>
</details>

---

###### 136. Що з цього змінить об’єкт `person`?

```javascript
const person = { name: 'Lydia Hallie' };

Object.seal(person);
```

- A: `person.name = "Evan Bacon"`
- B: `person.age = 21`
- C: `delete person.name`
- D: `Object.assign(person, { age: 21 })`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

За допомогою `Object.seal` ми можемо запобігти _додаванню_ нових властивостей або _видаленню_ тих, що вже існують.

Однак ми все ще можемо змінити значення наявних властивостей.

</p>
</details>

---

###### 137.  Що з цього змінить об’єкт `person`?

```javascript
const person = {
  name: 'Lydia Hallie',
  address: {
    street: '100 Main St',
  },
};

Object.freeze(person);
```

- A: `person.name = "Evan Bacon"`
- B: `delete person.address`
- C: `person.address.street = "101 Main St"`
- D: `person.pet = { name: "Mara" }`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Метод `Object.freeze` _заморожує_ об'єкт. Жодні властивості не можна додавати, змінювати чи видаляти.

Однак він лише _неглибоко_ заморожує об’єкт, тобто заморожуються лише _прямі_ властивості об’єкта. Якщо властивість є іншим об’єктом, як-от `address` у цьому випадку, властивості цього об’єкта не заморожуються та можуть бути змінені.

</p>
</details>

---

###### 138. Що буде на виході?

```javascript
const add = x => x + x;

function myFunc(num = 2, value = add(num)) {
  console.log(num, value);
}

myFunc();
myFunc(3);
```

- A: `2` `4` та `3` `6`
- B: `2` `NaN` та `3` `NaN`
- C: `2` `Error` та `3` `6`
- D: `2` `4` та `3` `Error`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Спочатку ми викликали `myFunc()` без жодних аргументів. Оскільки ми не передавали аргументи, `num` і `value` отримали значення за замовчуванням: num дорівнює `2`, а `value` — це значення, яке повертає функція `add`. До функції `add` ми передаємо `num` як аргумент, який мав значення `2`. `add` повертає `4`, яке є значенням `value`.

Потім ми викликали `myFunc(3)` і передали значення `3` як значення для аргументу `num`. Ми не передали аргумент для `value`. Оскільки ми не передали значення для аргументу `value`, він отримав значення за замовчуванням: значення, яке повертає функція `add`. До `add`, ми передаємо `num`, яке має значення `3`. `add` повертає `6`, яке є значенням `value`.

</p>
</details>

---

###### 139. Що буде на виході?

```javascript
class Counter {
  #number = 10

  increment() {
    this.#number++
  }

  getNum() {
    return this.#number
  }
}

const counter = new Counter()
counter.increment()

console.log(counter.#number)
```

- A: `10`
- B: `11`
- C: `undefined`
- D: `SyntaxError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

У ES2020 ми можемо додавати приватні змінні в класи за допомогою `#`. Ми не можемо отримати доступ до цих змінних поза класом. Коли ми намагаємося залогувати `counter.#number`, ми не можемо отримати до неї доступ поза класом `Counter`!

</p>
</details>

---

###### 140. Чого не вистачає?

```javascript
const teams = [
  { name: 'Team 1', members: ['Paul', 'Lisa'] },
  { name: 'Team 2', members: ['Laura', 'Tim'] },
];

function* getMembers(members) {
  for (let i = 0; i < members.length; i++) {
    yield members[i];
  }
}

function* getTeams(teams) {
  for (let i = 0; i < teams.length; i++) {
    // ✨ ТУТ ЧОГОСЬ БРАКУЄ ✨
  }
}

const obj = getTeams(teams);
obj.next(); // { value: "Paul", done: false }
obj.next(); // { value: "Lisa", done: false }
```

- A: `yield getMembers(teams[i].members)`
- B: `yield* getMembers(teams[i].members)`
- C: `return getMembers(teams[i].members)`
- D: `return yield getMembers(teams[i].members)`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Щоб перебирати `members` у кожному елементі масиву `teams`, нам потрібно передати `teams[i].members` у функцію-генератор `getMembers`. Функція-генератор повертає об’єкт-генератор. Щоб ітерувати по кожному елементу в цьому об’єкті, нам потрібно використовувати `yield*`.

Якби ми написали `yield`, `return yield` або `return`, уся функція-генератор була б повернута під час першого виклику методу `next`.

</p>
</details>

---

###### 141. Що буде на виході?

```javascript
const person = {
  name: 'Lydia Hallie',
  hobbies: ['coding'],
};

function addHobby(hobby, hobbies = person.hobbies) {
  hobbies.push(hobby);
  return hobbies;
}

addHobby('running', []);
addHobby('dancing');
addHobby('baking', person.hobbies);

console.log(person.hobbies);
```

- A: `["coding"]`
- B: `["coding", "dancing"]`
- C: `["coding", "dancing", "baking"]`
- D: `["coding", "running", "dancing", "baking"]`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Функція `addHobby` отримує два аргументи, `hobby` та `hobbies` зі значенням за замовчуванням масиву `hobbies` в об’єкті `person`.

Спочатку ми викликаємо функцію `addHobby` і передаємо `"running"` як значення для `hobby` і порожній масив як значення для `hobbies`. Оскільки ми передаємо порожній масив як значення для `hobbies`, `"running"` додається до цього порожнього масиву.

Потім ми викликаємо функцію `addHobby` і передаємо `"dancing"` як значення для `hobby`. Ми не передали значення для `hobbies`, тому воно отримує значення за замовчуванням, властивість `hobbies` об’єкта `person`. Ми додаємо хобі `dancing` в масив `person.hobbies`.

Нарешті, ми викликаємо функцію `addHobby` і передаємо `"baking"` як значення для `hobby`, а масив `person.hobbies` як значення для `hobbies`. Ми додаємо хобі `baking` в масив `person.hobbies`.

Після додавання `dancing` і `baking` значення `person.hobbies` буде `["coding", "dancing", "baking"]`

</p>
</details>

---

###### 142. Що буде на виході?

```javascript
class Bird {
  constructor() {
    console.log("I'm a bird. 🦢");
  }
}

class Flamingo extends Bird {
  constructor() {
    console.log("I'm pink. 🌸");
    super();
  }
}

const pet = new Flamingo();
```

- A: `I'm pink. 🌸`
- B: `I'm pink. 🌸` `I'm a bird. 🦢`
- C: `I'm a bird. 🦢` `I'm pink. 🌸`
- D: Нічого, ми не викликали жодного методу

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Ми створюємо змінну `pet`, яка є екземпляром класу `Flamingo`. Коли ми створюємо цей екземпляр, викликається `constructor` у `Flamingo`. Спочатку логується `"I'm pink. 🌸"`, після чого ми викликаємо `super()`. `super()` викликає конструктор батьківського класу `Bird`. Викликається конструктор у `Bird` і логується `"I'm a bird. 🦢"`.

</p>
</details>

---

###### 143. Який із варіантів призводить до помилки?

```javascript
const emojis = ['🎄', '🎅🏼', '🎁', '⭐'];

/* 1 */ emojis.push('🦌');
/* 2 */ emojis.splice(0, 2);
/* 3 */ emojis = [...emojis, '🥂'];
/* 4 */ emojis.length = 0;
```

- A: 1
- B: 1 та 2
- C: 3 та 4
- D: 3

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

Ключове слово `const` просто означає, що ми не можемо _переоголосити_ значення цієї змінної, вона _лише для читання_. Однак саме значення не є незмінним. Властивості масиву `emojis` можна змінювати, наприклад, додаючи нові значення, об’єднуючи їх або встановлюючи довжину масиву 0.

</p>
</details>

---

###### 144. Що нам потрібно додати до об’єкта `person`, щоб отримати `["Lydia Hallie", 21]` як результат `[...person]`?

```javascript
const person = {
  name: "Lydia Hallie",
  age: 21
}

[...person] // ["Lydia Hallie", 21]
```

- A: Нічого, об’єкт перебирається за замовчуванням
- B: `*[Symbol.iterator]() { for (let x in this) yield* this[x] }`
- C: `*[Symbol.iterator]() { yield* Object.values(this) }`
- D: `*[Symbol.iterator]() { for (let x in this) yield this }`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

За замовчуванням об’єкти не перебираються. Ітератор є ітератором, якщо присутній протокол ітератора. Ми можемо додати це вручну, додавши символ ітератора `[Symbol.iterator]`, який має повертати об’єкт-генератор, наприклад, зробивши його функцією-генератором `*[Symbol.iterator]() {}`. Ця функція-генератор має повертати `Object.values` об’єкта `person` якщо ми хочемо, щоб вона повертала масив `["Lydia Hallie", 21]`: `yield* Object.values(this)`.

</p>
</details>

---

###### 145. Що буде на виході?

```javascript
let count = 0;
const nums = [0, 1, 2, 3];

nums.forEach(num => {
  if (num) count += 1
})

console.log(count)
```

- A: 1
- B: 2
- C: 3
- D: 4

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Умова `if` у циклі `forEach` перевіряє, чи значення `num` є true чи false. Оскільки перше число в масиві `nums` дорівнює `0`, значення false, блок коду оператора `if` не буде виконано. `count` збільшується лише для інших 3 чисел у масиві `nums`, `1`, `2` і `3`. Оскільки `count` збільшується на `1` 3 рази, значення `count` дорівнює `3`.

</p>
</details>

---

###### 146. Що буде на виході?

```javascript
function getFruit(fruits) {
  console.log(fruits?.[1]?.[1])
}

getFruit([['🍊', '🍌'], ['🍍']])
getFruit()
getFruit([['🍍'], ['🍊', '🍌']])
```

- A: `null`, `undefined`, 🍌
- B: `[]`, `null`, 🍌
- C: `[]`, `[]`, 🍌
- D: `undefined`, `undefined`, 🍌

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

`?` дозволяє нам опціонально отримати доступ до глибших вкладених властивостей в об'єктах. Ми намагаємося залогувати елемент з індексом `1` у підмасиві з індексом `1` масиву `fruits`. Якщо підмасив з індексом `1` в масиві `fruits` не існує, він просто поверне `undefined`. Якщо підмасив з індексом `1` в масиві `fruits` існує, але цей підмасив не має елемента з індексом `1`, він також поверне `undefined`.

Спочатку, ми намагаємося залогувати другий елемент у підмасиві `['🍍']` масиву `[['🍊', '🍌'], ['🍍']]`. Цей підмасив містить лише один елемент, що означає відсутність елемента з індексом `1`, і повертає `undefined`.

Потім ми викликаємо функцію `getFruits` без передачі значення, що означає, що `fruits` має значення `undefined` за замовчуванням. Оскільки ми умовно об’єднуємо елемент з індексом `1` у `fruits`, він повертає `undefined`, оскільки цей елемент з індексом `1` не існує.

Нарешті, ми намагаємося залогувати другий елемент у підмасиві `['🍊', '🍌']` масиву `['🍍'], ['🍊', '🍌']`. Елемент з індексом `1` у цьому підмасиві є `🍌`.

</p>
</details>

---

###### 147. Що буде на виході?

```javascript
class Calc {
  constructor() {
    this.count = 0 
  }

  increase() {
    this.count++
  }
}

const calc = new Calc()
new Calc().increase()

console.log(calc.count)
```

- A: `0`
- B: `1`
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Ми встановлюємо змінну `calc` рівною новому екземпляру класу `Calc`. Потім ми створюємо новий екземпляр `Calc` і викликаємо метод `increase` для цього екземпляру. Оскільки властивість count знаходиться в конструкторі класу `Calc`, властивість count не є спільною для прототипу `Calc`. Це означає, що значення count не було оновлено для екземпляра, на який вказує calc, count досі дорівнює `0`.

</p>
</details>

---

###### 148. Що буде на виході?

```javascript
const user = {
  email: "e@mail.com",
  password: "12345"
}

const updateUser = ({ email, password }) => {
  if (email) {
    Object.assign(user, { email })
  }

  if (password) {
    user.password = password
  }

  return user
}

const updatedUser = updateUser({ email: "new@email.com" })

console.log(updatedUser === user)
```

- A: `false`
- B: `true`
- C: `TypeError`
- D: `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Функція `updateUser` оновлює значення властивостей `email` і `password` для user, якщо їх значення передано функції, після чого функція повертає об’єкт `user`. Поверненим значенням функції `updateUser` є об’єкт `user`, що означає, що значення updatedUser є посиланням на той самий об’єкт `user`, на який вказує змінна `user`. `updatedUser === user` дорівнює `true`.

</p>
</details>

---

###### 149. Що буде на виході?

```javascript
const fruit = ['🍌', '🍊', '🍎']

fruit.slice(0, 1)
fruit.splice(0, 1)
fruit.unshift('🍇')

console.log(fruit)
```

- A: `['🍌', '🍊', '🍎']`
- B: `['🍊', '🍎']`
- C: `['🍇', '🍊', '🍎']`
- D: `['🍇', '🍌', '🍊', '🍎']`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Спочатку ми викликаємо метод `slice` для масиву `fruit`. Метод slice не змінює оригінальний масив, але повертає значення, яке він вирізав із масиву: `'🍌'`.
Потім ми викликаємо метод `splice` для масиву `fruit`. Метод splice змінює оригінальний масив, що означає, що масив fruit тепер складається з `['🍊', '🍎']`.
Нарешті, ми викликаємо метод `unshift` для масиву `fruit`, який змінює оригінальний масив, додаючи передане значення, у цьому випадку ‘🍇’, як перший елемент у масиві. Масив fruit тепер складається з `['🍇', '🍊', '🍎']`.

</p>
</details>

---

###### 150. Що буде на виході?

```javascript
const animals = {};
let dog = { emoji: '🐶' }
let cat = { emoji: '🐈' }

animals[dog] = { ...dog, name: "Mara" }
animals[cat] = { ...cat, name: "Sara" }

console.log(animals[dog])
```

- A: `{ emoji: "🐶", name: "Mara" }`
- B: `{ emoji: "🐈", name: "Sara" }`
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Ключі об'єктів конвертуються у рядки.

Оскільки значення `dog` є об’єктом, `animals[dog]` насправді означає, що ми створюємо нову властивість під назвою `"[object Object]"`, що дорівнює новому об’єкту. `animals["[object Object]"]` тепер дорівнює `{ emoji: "🐶", name: "Mara"}`.

`cat` також є об’єктом, `animals[cat]` означає, що ми перезаписуємо значення `animals["[object Object]"]` новими властивостями cat.

 Логування `animals[dog]`, або насправді `animals["[object Object]"]`, оскільки перетворення об’єкта `dog` на рядок призводить до `"[object Object]"`, повертає `{ emoji: "🐈", name: "Sara" }`.

</p>
</details>

---

###### 151. Що буде на виході?

```javascript
const user = {
  email: "my@email.com",
  updateEmail: email => {
    this.email = email
  }
}

user.updateEmail("new@email.com")
console.log(user.email)
```

- A: `my@email.com`
- B: `new@email.com`
- C: `undefined`
- D: `ReferenceError`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: A

Функція `updateEmail` — це стрілкова функція, яка не прив’язана до об’єкта `user`. Це означає, що ключове слово `this` не посилається на об’єкт `user`, а посилається на глобальну область видимості. Значення `email` в об’єкті `user` не оновлюється. Під час логування значення `user.email` повертається початкове значення `my@email.com`.

</p>
</details>

---

###### 152. Що буде на виході?

```javascript
const promise1 = Promise.resolve('First')
const promise2 = Promise.resolve('Second')
const promise3 = Promise.reject('Third')
const promise4 = Promise.resolve('Fourth')

const runPromises = async () => {
  const res1 = await Promise.all([promise1, promise2])
  const res2  = await Promise.all([promise3, promise4])
  return [res1, res2]
}

runPromises()
  .then(res => console.log(res))
  .catch(err => console.log(err))
```

- A: `[['First', 'Second'], ['Fourth']]`
- B: `[['First', 'Second'], ['Third', 'Fourth']]`
- C: `[['First', 'Second']]`
- D: `'Third'`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: D

Метод `Promise.all` запускає передані проміси паралельно. Якщо один проміс не виконується, метод `Promise.all` _відхиляється (rejects)_ з цим значенням. У цьому випадку `promise3` відхиляється зі значенням `"Third"`. Ми перехоплюємо відхилене значення у методі `catch` під час виклику `runPromises`, щоб виявити будь-які помилки у функції `runPromises`. Логується лише `"Third"`, оскільки `promise3` відхиляється з цим значенням.

</p>
</details>

---

###### 153. Яким має бути значення `method` для логування `{ name: "Lydia", age: 22 }`?

```javascript
const keys = ["name", "age"]
const values = ["Lydia", 22]

const method = /* ?? */
Object[method](keys.map((_, i) => {
  return [keys[i], values[i]]
})) // { name: "Lydia", age: 22 }
```

- A: `entries`
- B: `values`
- C: `fromEntries`
- D: `forEach`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Метод `fromEntries` перетворює двовимірний масив на об’єкт. Перший елемент у кожному підмасиві буде ключем, а другий елемент буде значенням. У цьому випадку ми ітеруємо масив `keys`, який повертає масив, у якому перший елемент є елементом у масиві keys за поточним індексом, а другим елементом є елемент масиву values за поточним індексом.

Це створює масив підмасивів, що містить правильні ключі та значення, що призводить до `{ name: "Lydia", age: 22 }`

</p>
</details>

---

###### 154. Що буде на виході?

```javascript
const createMember = ({ email, address = {}}) => {
  const validEmail = /.+\@.+\..+/.test(email)
  if (!validEmail) throw new Error("Valid email pls")

  return {
    email,
    address: address ? address : null
  }
}

const member = createMember({ email: "my@email.com" })
console.log(member)
```

- A: `{ email: "my@email.com", address: null }`
- B: `{ email: "my@email.com" }`
- C: `{ email: "my@email.com", address: {} }`
- D: `{ email: "my@email.com", address: undefined }`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: C

Значенням за замовчуванням `address` є порожній об’єкт `{}`. Коли ми встановлюємо змінну `member` рівною об’єкту, який повертає функція `createMember`, ми не передаємо значення для address, що означає, що значенням address є порожній об’єкт за замовчуванням `{}`. Порожній об’єкт є значенням true, що означає, що умова `address ? address : null` повертає `true`. Значенням address є порожній об’єкт `{}`.

</p>
</details>

---

###### 155. Що буде на виході?

```javascript
let randomValue = { name: "Lydia" }
randomValue = 23

if (!typeof randomValue === "string") {
  console.log("It's not a string!")
} else {
  console.log("Yay it's a string!")
}
```

- A: `It's not a string!`
- B: `Yay it's a string!`
- C: `TypeError`
- D: `undefined`

<details><summary><b>Відповідь</b></summary>
<p>

#### Відповідь: B

Умова оператора `if` перевіряє, чи значення `!typeof randomValue` дорівнює `"string"`. Оператор `!` перетворює значення на булеве значення. Якщо значення true, повернене значення буде `false`, якщо значення false, повернене значення буде `true`. У цьому випадку значення, яке повертає `typeof randomValue` є значенням true `"number"`, тобто значення `!typeof randomValue` є булевим значенням `false`.

`!typeof randomValue === "string"` завжди повертає false, оскільки ми насправді перевіряємо `false === "string"`. Оскільки умова повернула `false`, блок коду оператора `else` запускається та логується `Yay it's a string!`.

</p>
</details>
