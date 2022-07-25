### Функція myMap()
**Етап: 0** 

Створити функцію `myMap`, вона повинна приймати 2 аргументи:
- перший - масив
- другий - колбек функцію

В результаті виконання функції `myMap` ми маємо отримати новий масив, кожен елемент якого дорівнює результату виконання колбек функції. Приклад нижче.

```js
const arr = [1, 2, 4, 5, 6]

const arrayAfterMap = myMap(arr, function(element) {
  return element * 2;
})

console.log(arr); [2, 4, 8, 10, 12]
```

Як ти можеш бачити, в нас є масив чисел, далі ми викликаємо `myMap` з цим масивом, а другим параметром, ми передаємо функцію, яка повертає результат множення числа 2 і першого аргумента функції. На виході ми маємо масив, де кожен елемент помножений на число `2`.

**Етап: 1**
Використовуючи попередню задачку, ти повинен зробити наступне: якщо при множенні на `2`, число більше чи рівне 10, воно повинно таким і залишитися.

```js
const arr = [1, 2, 4, 5, 6, 7, 4, 1, 3, 12, 5]

const arrayAfterMap = myMap(arr, function(element) {
  // твій код
})

console.log(arr); [2, 4, 8, 5, 6, 7, 8, 2, 6, 12, 5]
```

### Фільтрування
**Етап: 0**

Це до речі задача, яка дуже схожа на реальні робочі завдання. В тебе є масив користувачів, тобі потрібно використати метод `filter` і вибрати тільки тих користувачів, які мають 18 років, або більше.

```js
const users = [
  {
    id: 0,
    firstName: "John",
    lastName: "Carter",
    age: 10
  },
  {
    id: 1,
    firstName: "Leanne",
    lastName: "Graham",
    age: 18
  },
  {
    id: 2,
    firstName: "Ervin",
    lastName: "Howell",
    age: 30 
  },
  {
    id: 2,
    firstName: "Clementine",
    lastName: "Bauch",
    age: 15 
  }
]

const usersOlderThan18 = users.filter(...твій код...);
```

**Етап: 1**
Примітка для ментора:
- На цьому етапі потрібно показати що таке метод `map` (по суті це те, що було в першій задачці)
- Після того як задачка буде зробленна, потрібно показати про можливість використання \`\` (string literals / template literals)

Використовуючи метод `map`, тобі потрібно до кожного юзера додати поле `fullName`, яке буде сформоване конкатенацією полів `firstName` та `lastName`