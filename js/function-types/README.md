# Види функцій

В Javascript є 3 типи функцій:
- function declaration
- function expression
- arrow function

### function declaration
З цим типом функцій ми вже стикалися, коли розбиралися з основами функцій [тут](../functions-basic/README.md).

Приклад створення функції такого типу:
```js
function hello() {
  console.log('hi');
}

hello();
```

### function expression
Це функції які ми можемо присвоїти для змінних і констант

Приклад створення функції такого типу:
```js
const hello = function() {
  console.log('hi');
}

hello();
```

Тут варто зазначити один момент, якщо коли ми створювали `function declaration` ми одразу після слова `function` писали ім'я функції, але у випадку з `function expression` наша функція безіменна, або як прийнято говорити - анонімна, а для того щоб викликати функціїю, ми зветаємося до змінної чи константи в якій знаходиться ця функції.

### arrow function 
Функції стрілки з'явилися в 2015 році для вирішення певних проблем, про які ми будемо говорити в майбутніх темах:

Приклад створення функції такого типу:
```js
const hello = () => {
  console.log('hi');
}
```

По своїй суті вони дуже схожі на `function expression` бо також не мають ім'я і ми присвоюємо її в змінну чи константу.

В `arrow function` є одна різниця між `function declaration` і `function expression`, в ній не має `arguments`. Ми не можемо використовувати `arguments` щоб доступатися до значень з якими була викликана функція.

```js
const hello = () => {
 console.log(arguments); // undefined
}

hello('John');
```
Якщо ми спробуємо вивести в консоль `arguments` ми отримаємо `undefined`, тому ми завжди використовуємо `()` щоб доступатися до аргументів з якими була викликана функція

```js
const sayHello = (name) => {
  console.log('Hello ' + name); 
}

sayHello('Van'); // 'Hello Van'
```
