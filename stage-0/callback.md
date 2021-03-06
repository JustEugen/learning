# Callback functions / Функції зворотнього виклику
callback функції, це функції які ми передаємо в інші функції, і викликаємо в середині тих інших функціїй 

Найпростіший приклад:
```js
function hello(callbackFunctionForExample) {
  callbackFunctionForExample(); // 'hello'
}

hello(function() {
  console.log('helo');
});
```

Розберемо приклад:
1. Ми створили функцію `hello`, ця функція приймає лише один аргумент, і ми вирішили, що цей аргумент, має бути функція.
2. Далі ми викликаємо функцію `hello()`, і в якості першого аргументу передаємо функцію, в якій ми робимо `console.log`

Якщо виконати цей код, то в консолі ми побачимо `'hello'`.

Що також потрібно розуміти, функції - це також значення, тобто функції ми можемо записувати в змінні, константи та передавати їх як аргументи.

Ще один цікавіший приклад:
```js
function canBuyAlchocol(age) {
  if (age < 18) {
    console.log('you cannot buy')
  } else {
    console.log('take your alchocol')
  }
}

canBuyAlchocol(10);
```
Ось в нас є така функція, яка приймає вік, і перевіряє чи з таким віком можна купити алкоголь, після чого виводить так чи ні, але що, якщо ми б хотіли визначати ззовні, що має статися у випадку якщо не можна купувати, і в випадку якщо можна купувати. Ключове поняття тут, визначати самі, з зовні, не міняючи код функції `canBuyAlchocol`.

```js
function canBuyAlchocol(age, onCanBuy, onCannotBuy) {
  if (age < 18) {
    onCannotBuy();
  } else {
    onCanBuy()
  }
}

canBuyAlchocol(
  10, 
  function() {
    alert('Hopefully you can buy');
  },
  function() {
    alert('You cannot buy this, you are little shit');
  }
);
```
Ми змінили код нашої функції `canBuyAlchocol()`, тепер ця функція приймає 3 аргументи:
1. Вік
2. Функція, яку ми будемо викликати в випадку, якщо можна купити алкоголь
3. Функція, яку ми будемо викликати в випадку, якщо не можна купити алкоголь

Ну і надалі, ми викликаємо нашу функції `canBuyAlchocol` і передаємо всі необіхдні параметри.

Єдина проблема цього прикладу в тому, що він все одно не розкриває всі можливості `callback` функцій, тому показую наступний

```js
function canBuyAlchocol(age, onCanBuy, onCannotBuy) {
  if (age < 18) {
    onCannotBuy();
  } else {
    onCanBuy()
  }
}
// уяви, що цей age буде приходити з серверу, і буде мінятися в залежності
// від користувача, який зайшов в магазин
let age = 20;

// Варіант 1
canBuyAlchocol(
  age, 
  function() {
    alert('Hopefully you can buy');
  },
  function() {
    alert('You cannot buy this, you are little shit');
  }
);

// Варіант 2
canBuyAlchocol(
  age,
  function() {
    alert('You did it');
  },
  function() {
    alert('Go home boy');
  }
);

// Варіант 3
canBuyAlchocol(
  age,
  function() {
    alert('You are good');
  },
  function() {
    alert('Sorry, you cannot do this');
  }
);
```

В цьому прикладі, суть колбеків розкривається ще більше, по перше, ми створили змінну `age`, яка зберігає вік, уявимо що вона приходить з серверу. І далі, ми 3 рази викликаємо нашу функцію, і в кожному разі, ми по різному визначаємо, що буде відбуватися на той, чи інший випадок

Окрім цього, є ще прикольна штука з тим, що callback функції, можуть повертати значення

```js
function testing(callback) {
  const result = callback();
  
  console.log(result); // 'hello world, yopta'
}

testing(function() {
  return 'hello world, yopta';
})
```

Також, callback функції можуть приймати якісь значення

```js
function greeting(callback) {
  const result = callback('john');
  
  console.log(result); // 'Hello john'
}

testing(function(name) {
  return 'Hello ' + name;
})
```
В даному випадку, наша колбек функція приймає один аргумент, і повертає строку яка каже привіт для якогось імені

## Важливо
Тут потрібно розуміти одну річ, колбеки доволі важка тема, і зрозуміти їх можна тільки в процесі роботи і навчання, на разі, сприймай цю тему як ознайомчу і не зациклюйся дуже сильно на ній.
