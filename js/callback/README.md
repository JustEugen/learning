# Callback / функції зворотнього виклику

В javascript багато що зав'язане на callback функціях, особливо асинхронність, але в даному уроці ця тема не буде підійматися.

Грубо кажучи callback - це функція, що передається в аргументи іншої функції, і виконується коли щось сталося.

Найпростіший приклад:
```js
function hello(callMeWhenSomethingHappen) {
  callMeWhenSomethingHappen(); // 'hello'
}

hello(() => {
  console.log('hello');
});
```

Розберемо приклад:
1. Ми створили функцію hello, яка приймає в якості першого аргументу функцію, після чого одразу її викликає
2. Далі ми викликаємо функцію hello(), і в якості першого аргументу передаємо функцію, в якій ми робимо `console.log

Що також потрібно розуміти, функції - це також значення, тобто функції ми можемо записувати в змінні, константи та передавати їх як аргументи.

Ще один цікавіший приклад:
```js
function canBuyAlchocol(age) {
  if (age < 18) {
    alert('you cannot buy')
  } else {
    alert('take your alchocol')
  }
}

canBuyAlchocol(10);
```
Ось в нас є така функція, яка приймає вік, і перевіряє чи з таким віком можна купити алкоголь, після чого виводить так чи ні, але що, якщо ми б хотіли самі визначати, що потрібно робити в вадку якщо не можна купувати, і в випадку якщо можна купувати. Ключове поняття тут, визначати самі, з зовні, не міняючи код функції `canBuyAlchocol`.

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
  () => {
    alert('Hopefully you can buy');
  },
  () => {
    alert('You cannot buy this, you are little shit');
  }
);
```
Ми змінили код нашої функції `canBuyAlchocol()`, тепер ця функція приймає 3 аргументи:
1. Вік
2. Функція, яку ми будемо викликати в випадку, якщо можна купити алкоголь
3. Функція, яку ми будемо викликати в випадку, якщо не можна купити алкоголь

Ну і надалі, ми викликаємо нашу функції `canBuyAlchocol` і передаємо всі необіхдні параметри.

Єдиа пробелма цього прикладу в тому, що він все одно не розкриває всі можливості `callback` функцій, тому показую наступний 

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
  () => {
    alert('Hopefully you can buy');
  },
  () => {
    alert('You cannot buy this, you are little shit');
  }
);

// Варіант 2
canBuyAlchocol(
  age,
  () => {
    alert('You did it');
  },
  () => {
    alert('Go home boy');
  }
);

// Варіант 3
canBuyAlchocol(
  age,
  () => {
    alert('You are good');
  },
  () => {
    alert('Sorry, you cannot do this');
  }
);
```

І в цьому прикладі, суть колбеків розкривається ще більше, по перше, ми створили змінну `age`, яка зберігає вік, уявимо що вона приходить з серверу. І далі, ми 3 рази викликаємо нашу функцію, і в кожному разі, ми по різному визначаємо, що буде відбуватися на ту, чи іншу дію

Окрім цього, є ще прикольна штука з тим, що callback функції, можуть повертати значення

```js
function testing(callback) {
  const result = callback();
  
  console.log(result); // 'hello world, yopta'
}

testing(() => {
  return 'hello world, yopta';
})
```

Також, callback функції можуть приймати якісь значення

```js
function greeting(callback) {
  const result = callback('john');
  
  console.log(result); // 'Hello john'
}

testing((name) => {
  return 'Hello ' + name;
})
```
В даному випадку, наша колбек функція приймає один аргумент, і повертає строку яка каже привіт для якогось імені

Але на справді, ми не так часто зараз використовуємо колбек функції, єдине місце, де ми постійно це робимо - це робота з масивами.

Давай спробуємо вирішити наступну задачу, в тебе є масив користувачів, в кожного користувача є вік, тобі потрібно відфільрувати його так, щоб ти в кінці отримав тільки тих користувачів, яким є 18 років.

```js
const users = [
  {
    id: 1,
    fullname: 'John Carter',
    age: 40
  },
  {
    id: 2,
    fullname: 'Samara Ramos',
    age: 10
  },
  {
    id: 3,
    fullname: 'Talon French',
    age: 15
  },
  {
    id: 4,
    fullname: 'Shelby Fowler',
    age: 20
  },
  {
    id: 5,
    fullname: 'Octavio Norman',
    age: 32
  }
]

const usersOlderThan18 = [];

for (let i = 0; i < users.length; i++) {
  if (users[i].age >= 18) {
    usersOlderThan18.push(users[i]);
  }
}

console.log(usersOlderThan18); // ...
```

І ось ми відфільтрували наш масив, а що якщо нам потрібно буде відфільтрувати ще якйись масив, і навіть з різною умовою, наприклад, тут ми відфільтровували всіх користувачів які старші 18, а що якщо нам буде потрібен масив користувачів, ім'я яких розпочинається з букви `S`, доведеться дублювати цей код постійно. Завдяки колбекам, ми можемо зробити доволі прикольну штуку, для початку, давай винесемо цей цикл в окрему функцію, яка в якості першого аргументу буде приймати масив який потрібно перебирати, і буде повертати відфільрований масив
```js
const users = [
  {
    id: 1,
    fullname: 'John Carter',
    age: 40
  },
  {
    id: 2,
    fullname: 'Samara Ramos',
    age: 10
  },
  {
    id: 3,
    fullname: 'Talon French',
    age: 15
  },
  {
    id: 4,
    fullname: 'Shelby Fowler',
    age: 20
  },
  {
    id: 5,
    fullname: 'Octavio Norman',
    age: 32
  }
]

function myFilter(arr) {
  const filteredArray = [];

  for (let i = 0; i < users.length; i++) {
    if (users[i].age >= 18) {
      filteredArray.push(users[i]);
    }
  }
  
  return filteredArray;
}

const usersOlderThan18 = myFilter(users);

console.log(usersOlderThan18)
```
Якщо запустити приклад в консолі, то можна побачити, що він працює так як перед цим, тепер наступний крок, потрібно зробити так, щоб ми могли цю функцію перевикористовувати, тобто потрібно якось передавати з зовні умову в середину нашого фільтра. Для цього нам якраз і потрібно колбеки. Для цього ми маємо домовитися про 2 речі:
1. Колбек в якості першого аргументу буде приймати поточний елемент масива
2. Якщо колбек поверне true, то поточний елемент масива ми будемо додавати в відфільтрований масив, якщо ні, то не будемо додавати 

```js
const users = [
  {
    id: 1,
    fullname: 'John Carter',
    age: 40
  },
  {
    id: 2,
    fullname: 'Samara Ramos',
    age: 10
  },
  {
    id: 3,
    fullname: 'Talon French',
    age: 15
  },
  {
    id: 4,
    fullname: 'Shelby Fowler',
    age: 20
  },
  {
    id: 5,
    fullname: 'Octavio Norman',
    age: 32
  }
]

function myFilter(arr, conditionCallback) {
  const filteredArray = [];

  for (let i = 0; i < users.length; i++) {
    const meetCondition = conditionCallback(users[i]);
    
    if (meetCondition) {
      filteredArray.push(users[i]);
    }
  }
  
  return filteredArray;
}

const usersOlderThan18 = myFilter(users, (elementOfArray) => {
  if (elementOfArray.age >= 18) {
    return true
  }
  
  return false
});

console.log(usersOlderThan18)
```

Що відбувається:
1. Тепер ми передаємо колбек функцію
2. Колбек функція викликається на кожній ітерації масива, і в якості першого аргумента приймає поточний елемент масива
3. Якщо колбек функція поверне tryu, то ми цей елемент додаємо до кінцевого масива

І от тепер самий сік, такого підходу, ми цей фільтр можемо викоритовувати як нам завгодно
```js
const usersStartsWithS = myFilter(users, (elementOfArray) => {
  if (elementOfArray.fullname.startsWith('S')) {
    return true
  }

  return false
});

console.log(usersStartsWithS)
```

Задача, тобі треба зробити похожу штуку, тільки вона повинна перебирати масив, так само викликати колбек і передавати туди поточний елемент маисива, і те що верне той колбек, то і попаде в новий масив. Аналог функції map
