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

###### 85. Яка інформація буде залогована?

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
