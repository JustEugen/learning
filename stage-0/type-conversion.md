# Type Conversion / Приведення типів
На разі ми розберемо тільки переведення таких типів як `string`, `number`, `null`, `undefined` в тип `boolean`.

## `Number` в `boolean`
Тут є цікава штука, в булевій математиці - `1` - це `true`, а `0` - це `false`, тому виходить наступна штука. Якщо число не дорівнює `0`, тоді воно `true`, якщо число дорівнює `0`, тоді воно `false`.

> як взагалі переводити значення в `boolean`. Інсує 2 способи, перший - це написати `Boolean(значення_чи_змінна)` і в результаті ти оримаєш `true` або `false`, або перед значенням чи змінною поставити два знаки оклику `!!`. В наступних 

Наведу приклад переведення числа в булеан:
```js
const age = 10;

console.log(Boolean(age)); // true
// або
console.log(!!age); // true

const randomNumber = -71;

console.log(Boolean(randomNumber)); // true
// або
console.log(!!randomNumber); // true

const zeroValue = 0;

console.log(Boolean(zeroValue)); // false 
// або
console.log(!!zeroValue); // false
```

Як ти можеш бачити, якщо значення більше чи менше за `0`, то воно `true`, а якщо значення `0`, то воно `false`

## `String` в `boolean`
Тут просто, якщо строка пуста, значить це `false`, якщо в строці щось є - це `true`

```js
console.log(!!"hello"); // true
console.log(!!""); // false
```

## `Null` або `Undefined` в `boolean`
Тут також просто, `null` та `undefined` завжди будуть `false`

```js
console.log(!!null); // false
console.log(!!undefined); // false
```
