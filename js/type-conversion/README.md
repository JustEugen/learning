# Перетворення типів в інші типи

### Перетворення в `string`
Для прикладу, якщо нам потрібно число перетворити в строку.
```js
const age = 10;

const ageAsString = String(age);

console.log(ageAsString); // '10'
console.log(typeof ageAsString); // 'string'

const someBool = true;

const someBoolAsString = String(someBool);

console.log(someBoolAsString); // 'true'
console.log(typeof someBoolAsString); // 'string' 
```

Є ще декілька способів, але чесно кажучи це найадекватніший зі всіх. Якщо розібрати цей приклад, то нам потрібно в `String(...сюди...)` передати значення, яке ми хочемо конвертувати в строку, після чого нам повернеться це значення в вигляді строки.

### Перетворення в `boolean`
З перетворенням в `boolean` є декілька нюансів. Перший з них - це те, що в двійковій системі числення `true` - `1`, `false` - `0`. Другий, якщо ми захочемо перевести строку в `boolean`, пуста строка - `false`, а не пуста `true`
```js
console.log(Boolean(1)); // true
console.log(Boolean(0)); // false

console.log(Boolean("hello")); // true
console.log(Boolean("")); // false

// Хоч і в середині строки 0, це все одно строка, і вона не пуста, тому true
console.log(Boolean("0")); // true
// А тут просто пробіл, що також не рахується пустою строкою, пробіл тоже ж значення
console.log(Boolean(" ")); // false
```

### Перетворення в `number`
Є 2 основних способи перетворити строку в `number`

````js
// Використати Number(...значення...)ж
console.log(Number('12')); // 12
// Перед строкою поставити +
console.log(+'100'); // 100
````

В реальному коді, ми використовуємо тільки спосіб з `+`, так як він найбільш простий на вигляд, і не займає багато місця.
