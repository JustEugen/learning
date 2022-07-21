# Comparison operators / Оператори зрівнювання

Тут майже все те ж саме як в математиці:
- `>` - більше
- `>=` - більше рівне
- `<` - менше
- `<=` - менше рівне
- `===` - еквівалентний
- `!==` - не еквівалентний

Всі ці оператори в результаті своєї роботи будуть повертати `boolean`, тобто `true`, або `false`

Набір прикладів на `>`, `>=`, `<`, `<=`
```js
const result = 18 < 10;

console.log(result); // false
```

```js
const result = 18 > 10;

console.log(result); // true
```

```js
const result = 10 <= 10;

console.log(result); // true 
```

```js
const result = 10 >= 10;

console.log(result); // true 
```

## Оператор еквівалентності `===`
Якщо значення зліва і справа еквівалентні, і вони мають однаковий тип, значить буде `true`, якщо ні, то `false`

```js
const result = 'a' === 'a';

console.log(result); // true
```

```js
const result = 'a' !== 'a';

console.log(result); // false 
```

```js
const result = 'my name is' === 'hello world';

console.log(result); // false 
```

А ось ще один приклад, пов'язаний на типах:
```js
const result1 = 1 === 1;
console.log(result1); // true

const result2 = 1 === '1';
console.log(result2); // false
```

Як ти можеш бачити, коли ми порівнюємо два однакових числа ми отримуємо `true`, але якщо ми порівняємо число 1, і строку, в якій в середині цифра 1, то ми отримаємо `false`, тому що хоч вони й здаються однаковими, але вони відрізняються типами.

## Два слова про `==`
Для порівняння двох значень в javascript є ще подвійне `==`, але воно не використовується, бо має багато проблем.
