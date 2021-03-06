# Scope

Scope (зона видимості) - це спеціальний об'єкт, або ще можна сказати, спеціальне місце, в якому зберігаються всі змінні та функції, які були оголошені. Scope ще інколи називають lexical environment (лексичне оточення).

```js
let animal = 'cat';

console.log(animal);
```

В цьому прикладі, в нас є змінна `animal`, яку ми потім виводимо в `console.log`. І тут буде трохи неочевидне запитання, яким чином, Javascript знає що така змінна взагалі існує, і що в середині неї? Якраз для такої цілі, і був створенний Scope.

Тут я хочу сказати одну важливу штуку, scope створюється не під час того як виконується Javascript код. Javascript рушій, дуже розумна і потужна штука, і перед тим як запускати код, він проходиться по ньому декілька разів, грубо кажучи просто читає код (НЕ ВИКОНУЄ).

Якщо під час ЧИТАННЯ коду, Javascript рушій натикається на оголошення змінної (`let animal` в ншому випадку), він запише данні про неї в поточний scope. І вже під час ВИКОНАННЯ коду, якщо він натикнеться на використання цієї змінної (в прикладі зверху це `console.log`), він буде знати де знаходиться вся інформація про цю змінну, а саме в цьому спеціальному об'єкті scope.

Але scope не один єдиний на весь додаток, в нього є 3 вида:
- глобальний / global
- блочний / block
- локальний / local / function scope

### Глобальний scope
Глобальний scope охоплює всю html сторінку.

Для прикладу

```html
<body>
    <script>
      let myTestVariable = 'hello world';
    </script>
    <script>
      console.log(myTestVariable)
    </script>
</body>
```

Якщо запустити цей приклад, то в консолі ми побачимо 'hello world'. Хоч це і 2 різних javascript скрипта, це могли навіть бути 2 окремих файла, але вони все одно ділять один глобальний scope. Раніше таким чином підключалися різні бібліотеки

```html
<body>
    <script src="https://some-libray.com/code"></script>
    <script src="https://another-libray.com/code"></script>
    <script>
      // і тут ми маємо доступ до змінних які були оголошені в середині біліотек вище.
    </script>
</body>
```


А це, як би ми код розділили на 2 файли

`Структура проекта`
```
/my-project 
    |- index.html
    |- first.js
    |- second.js
```

`first.js`
```js
const userName = 'John';
```
`second.js`
```js
console.log(userName); // 'John'
```
`index.html`
```html
<body>
    <script src="./first.js"></script>
    <script src="./second.js"></script>
</body>
```

І так само, якщо ти відкриєш консоль розробника, ти побачиш в ній 'John'

Але не все так добре в такій структурі, тому що ти тепер зообов'язаний підключати файли в правильному порядку.

Якщо ти підключатимеш спочатку `./second.js`, а вже потім `./first.js`, то тоді в `./second.js` при спробі вивести змінну `userName` ти отримаєш помилку, так як на той момент, скрипт `./first.js`, в якому ця змінна створюється, не виконався, тому і змінна не створила, ну і в глобальному скоупі такої змінної не існує також.

### Локальний scope / функційний scope
Цей вид scope створюється для кожної функції, і існує лише в цій функції.

```js
function sayHello() {
  let test = 'I am inside function';
  
  console.log(test)
}

sayHello();
```

Розглянемо цей приклад:
1. Для функції `sayHello` буде створенний свій власний scope;
2. Змінна `test` буде записана в scope функції `sayHello`;
3. В `console.log` ми намагаємося вивести змінну `test`, тому javascript рушій почне шукати, чи є така змінна в поточному скоупі, а поточний скоуп, в даному випадку, це скоуп функції `sayHello`. В нашому випадку така змінна є, і в консоль нам виведеться: 'I am inside function'

### Блочний scope / block scope
Block scope існує в середині тіла if else, while, do while, for, try catch і працює він тільки для `let` та `const`, старий спосіб створення змінних через `var` ігнорує блочинй скоуп, і створюється або в глобальному, або в локальному. 

> Про var буде детальніше в прикладах внизу, але мушу сказати, що зараз ми не використовуємо `var` багатьох причинах, одна з них те, що вона не бачить block scope. 
> 
Прикладами:
```js
if (true) {
  // ми в середині тіла if else, тобто це блочний scope
  // ця змінна буде доступна тільки в середині цього блоку
  let hello = 'test variable';
  
  console.log(hello); // в консоль виведе: 'test variable'
}

// Error. А тут ми вже отримаємо помилку,
// тому що в даному скоупі такої змінної як hello не має
console.log(hello);
```

```js
for (let i = 0; i < 10; i++) {
  let someVariable = 'I am variable';
}

// Error. Якщо ми будемо намагатися доступитися до змінної someVariable
// ми отримаємо помилку, томущо в поточному скоупі такої
// змінної не має
console.log(someVariable);

// Error. Це також стосується і змінної i, томущо вона також була створенна середині блоку for.
console.log(i);
```

А от з `var` ситуація зовсім інша. Зайду на перед, відсутність у `var` розуміння блочного скоупу і сталол причиною того, що вони перестали використовуватися.

```js
if (true) {
  var hello = 'I am var';
}

console.log(hello); // I am var
```

Можливо на разі, ти не розумієш проблем, які буде створювати `var` і необхідності в блочному скоупі, але це розуміння прийде з досвідом.

### Scope Visibility 

Перш за все, мушу сказати одну річ, все що лежить в середині scope доступно тільки в середині цього scope.

На прикладі покажу, що я маю на увазі:
```js
function test() {
  let hello = 'I am hello variable';
}

// Error. Ми отримаємо помилку, томущо в поточному скоупі такої
// змінної не має
console.log(hello);
```

На цьому прикладі в середині функції `test` ми створили змінну `hello`, ця змінна існує тільки в середині scope цієї функції `test`.

Якщо ми будемо намагатися вивести `hello` ми отримаємо помилку, так як в скоупі, де ми робимо `console.log`, в нашому це глобальний скоуп, такої змінної не існує.

Ще один приклад;

```js
let animal = 'pig'

function test() {
  let animal = 'cow';
}

console.log(animal); // 'pig'
```

В даному прикладі, ми стоврили змінну `animal`, в яку ми запихнули слово "pig", а потім, ми створили змінну, з таким самим іменем в середині фукнції тест;

Якщо запустити цей код, то можна побачити, що в консолі нам виведеться слово 'pig'.

### Scope Chaining
Цей термін описує те, як шукається змінна між скоупами.

Приклад:

```js
let myAnimal = 'poni';

function parent() {
  
  function inner() {
     console.log(myAnimal);
  }
  
  inner();
}

parent();
```

Якщо запустити цей приклад, то в конослі ти побачиш, що виводиться "poni". Тепер розберемося як це все працює.

В нас є функція `parent`, всередені якої є ще одна функція `inner`, в якій ми виводимо в консоль змінну `myAnimal`. 

Коли ми намагаємося вивести цю змінню, спочатку, javascript шукає, чи в середині скоупа функції `inner` є змінна з такою назвою, в нашому випадку, такої змінною і функії `inner` не має, тому javascript йде по цепочці вверх по всім батьківським скоупам, аж до глобального. 

Батьківський скоуп для функції `inner` - це функція `parent`, тому javascript почне пошук змінної `myAnimal` в середині скоупу функційї `parent`, в нашому випадку такої змінної не має, тому рухаємся до батьківського скоупу функційї `parent`, батьківським скоупом для цієї функції біде глобальний скоуп. В глобальному скоупі ми знаходимо таку змінну і виводимо її в консолі.

Далі ще один приклад:

```js
let myAnimal = 'poni';

function parent() {
  let myAnimal = 'dog';
  
  function inner() {
     console.log(myAnimal);
  }
  
  inner();
}

parent();
```

Якщо запустити цей код, то в консолі в нас виведе 'dog', тому що javscript двигун, по ланцюгу батьківській скоупів, зміг знайти її в функції `parent`

І ще один приклад

```js
let myAnimal = 'poni';

function parent() {
  let myAnimal = 'dog';
  
  function inner() {
    let myAnimal = 'cat'
    console.log(myAnimal);
  }
  
  inner();
}

parent();
```

В даному прикладі в нас виведет 'cat', тому що javascript зміг знайти таку змінну, в тому самому скоупі, де і ми намагалися вивисте цю змінну, тобто в скоупі функції `inner`.
