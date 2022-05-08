# Function Hoisting / Піднесення функцій

Підесення фукнцій, працює схожим чином, з піднесенням змінних через `var`, але є відмінності.

По-перше, в Javascript ми маємо 3 різні можливості для створення функцій:
- function declaration;
- function expression;
- arrow function;

Піднесення функцій працює **ТІЛЬКИ** для `function declaration` **!**.

Яка відмінність піднесення між `var` та `function declaration` - вона лише одна, якщо у випадку з `var` підносилося тільки оголошення змінної, і їй присвоювалося `undefined`, то у випадку з `function declaration` підноситься цілком вся функція.
```js
sayHello(); 

function sayHello() {
  console.log('hello world');
}
```
В цьому прикладі ми викликаємо функцію до її оголошення, томущо Javascript двигун, автоматично, перед виконанням, перенесе її в самий-самий верх нашого коду.

Ось невеликий приклад в комбінації з піднесенням `var`

```js
// Початок: Твій реальний код
console.log(a); // undefined

var a = 'Hello, world!';
const b = 'Some text here';
var yopta = 'I need semki';
var moskal = 'Dead';
let city = 'Lviv';

function sayHello() {
  console.log('hello world');
}
// Кінець: Твій реальний код
// =================

// Початок: Те що відбувається під капотом 
function sayHello() {
  console.log('hello world');
}

var a = undefined;
var yopta = undefined;
var moskal = undefined;

console.log(a); // undefined
console.log(yopta); // undefined
console.log(moskal); // undefined

a = 'Hello, world!';
const b = 'Some text here';
yopta = 'I need semki';
moskal = 'Dead';
let city = 'Lviv';

sayHello();
// Кінець: Те що відбувається під капотом
```

Як можеш бачити, функції будуть підніматися в самий-самий верх, і будуть доступні до їх оголошення.
