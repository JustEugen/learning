### Логічні оператори
Це прям дуже крута штука, які ми використовуємо постійно, вони є наступні:
- `||` ( OR / АБО ) - якщо хоча б одна з умов `true`, то і вся умова рахується `true`
- `&&` (AND / І ) - якщо всі умови `true`, тоді і вся умова рахується `true`, а якщо хоча би якась з умов `false`, тоді і вся умова `false` 
- `!` (NOT / НІ ) - `true`, перетворює в `false`, і навпаки `false` перетворює в `true`

Приклад з OR:
```js
const result =  false || true || false;

// Томущо ми маємо хоча би один true, тому і вся умова true
console.log(result); // true
```
Приклад з AND:
```js
const result = true && false && true;

// Томущо для && всі умови мають бути true, щоб в результаті вийшло true
console.log(result); // false 
```
```js
const result = true && true && true;

// Томущо тут все true
console.log(result); // true 
```
Приклад з NOT:
```js
const result = !false;

// томущо перетворює в зворотнє
console.log(result); // true
```
```js
const result = !true;

// томущо перетворює в зворотнє
console.log(result); // false 
```

Перейдемо до більш реальних прикладів, і скомбінуємо їх, використовуючи `if`. В нас є наступна задача, якщо для користувача є 18 років, зараз не пізніше 22 вечора і не раніше 8 ранку, ми продамо алкоголь, в іншому випадку ні.

```js
// Так само, уявляємо, що ці данні ми беремо звідкись, наприклад їх вводить користувач
const currentHour = 14;
const age = 19;

if (age >= 18 && currentHour < 22 && currentHour >= 8) {
  console.log('I can sell you an alcohol');
} else {
  console.log('I cannot sell you');
}

// Що ми отримаємо в консолі:
// 1. 'I can sell you an alcohol'
```

А тепер давай розберемо цей `if`. В нас є 3 умови, які повинні виконатися одночасно, а саме вік, година має бути менша ніж 22, і більша ніж 8, і всі 3 умови повинні бути вірні, для того щоб ми щось зробили. В загальному, це вся суть логічного оператора `&&` 

Ще одна зхожа задачка з використанням `||`. Уявимо ситуацію, що не має часових обмежень по продажу алкоголю, і основна вимога - це або вік, або записка від батьків. Якщо ти старший 18, то тобі можна продатаи, якщо ти менший 18, то ти маєш мати записку. Таке можна реалізувати наступним чином

```js
// Так само, уявляємо, що ці данні ми беремо звідкись, наприклад їх вводить користувач
const hasNoteFromParent = true;
const age = 10;

if (age >= 18 || hasNoteFromParent) {
console.log('I can sell you an alcohol');
} else {
console.log('I cannot sell you');
}

// Що ми отримаємо в консолі:
// 1. 'I can sell you an alcohol'
```

Розберемо наш `if`. В цьому випадку, `age >= 18` поверне нам `false`, томущо `age` в нас `10`, але, спрацює друга умова, `hasNoteFromParent` в нас `true`, а як ми знаємо, для логічного або `||` потрібно щоб виконалася хоча би одна з умов.

Ці два приклади можна об'єднати:
```js
// Так само, уявляємо, що ці данні ми беремо звідкись, наприклад їх вводить користувач
const hasNoteFromParent = true;
const currentHour = 14;
const age = 19;

if ((age >= 18 || hasNoteFromParent) && currentHour < 22 && currentHour >= 8) {
  console.log('I can sell you an alcohol');
} else {
  console.log('I cannot sell you');
}

// Що ми отримаємо в консолі:
// 1. 'I can sell you an alcohol'
```
Але тут потрібно зауважити один дуже важливий момент, логічні оператори мають пріорітет виконання, особисто я цього пріорітету не знаю, і в мене ніколи з цим не було проблем

Для того щоб в нас не виникали проблеми з пріорітетами, ми можемо зробити те ж саме, що ми і робимо в математиці. В математиці, ділення і множення мають пріорітет над додаванням і відніманням, тому деякі операції, ми огортаємо в дужки.

В нашому випадку, в дужки ми огорнули нашу операцію з `||`, вона собі в цих дужках виконається, поверне `true` або `false`, а далі вже цей результат буде використовуватися в `&&`

### Останнє правдиве
Тут діє така ж сама штука як з `if`, в логічних операторах, нам не обов'язково використовувати `true` або `false`, ми можемо просто використовувати значення, які самі будуть конвертуватися в `boolean`, але тут є один нюанс. Значення перетвориться в `boolean` тільки для порівнювання, після чого, якщо ми використовуємо `||` нам повернеться останнє правдиве значення.

Для прикладу
```js
const reuslt = '' || 0 || 'hello world' || true

console.log(reuslt); // 'hello world' 
```
В константу `result` в нас запишеться `'hello wordld'`. Розберемося крок за кроком.
1. В нас спочатку йде пуста строка `''`, як ми пам'ятаємо, якщо перетворити пусту строку в `boolean`, ми отримаємо `false`, тому код піде далі
2. В нас йде число `0`, нуль при перетворенні в `boolean` також видасть `false`, йдемо далі
3. **Не** пуста строка, при перетворенні в `boolean` видасть `true`, а для `||` потрібно хоча би одне `true`, щоб рахувати що все `true`, тому на цьому виконання закінчиться, і з цього виразу повернеться останнє правдиве значення, тобто ця строка `'hello world'`

Пізніше ми ще розглянемо більш реальні способи використання, але на разі по більшій мірі теорія

Схожа штука і з `&&`, тільки в цьому випадку, вона поверне найперше правдиве значення:
```js
const result = true && 'hello';

console.log(result); // 'hello'
```

Реальні приклади використання будуть в подальших темах, коли ми будемо мати більше інформації і ми зможемо мутити цікаві речі.