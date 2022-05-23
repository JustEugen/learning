# Оператори зрівнювання

Тут майже все те ж саме як в математиці:
- `>` - більше
- `>=` - більше рівне
- `<` - менше
- `<=` - менше рівне 
- `===` - еквівалентний
- `!==` - не еквівалентний

Всі ці оператори в результаті своєї роботи будуть повертати `boolean`, тобто `true`, або `false`

### Порівнювання чисел
```js
const result = 18 < 10;

console.log(result); // false
```

```js
const result = 18 === 18;

console.log(result); // true 
```


### Порівнювання за допомогою потрійного `===`
Ця штука - це оператор еквівалентності, якщо значення зліва і справа еквівалентні, значить буде `true`, якщо ні, то `false`

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

Якщо ти захочеш порівняти значення, двох різних типів, ти завжди будеш отримувати `false`. Томущо для цього оператора типи та значення мають бути еквівалентні.


Для прикладу, якщо ми говоримо про `boolean`, де `true` - це по суті `1`, а `false` - це по суті `0`, якщо ми спробуємо порівняти їх, результати будуть наступні

```js
const result = true === true;

console.log(true);
```

```js
const result = 1 === true;

console.log(false); // томущо тип зліва - це number, а з права - це boolean
```

### Порівнювання використовуючи подвійне `==`
На разі в деталі вдаватися не бачу сенсу, все що потрібно розуміти зараз, це те, що подвійне `==` не використовується, і використовувати його не можна, так як він може давати різні результати

### Узагальнення
Тут на справді пдоволі мало прикладів можна дати, більшість з них будуть в подальших темах