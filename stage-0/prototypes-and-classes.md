# Prototype and Classes / Прототипи і Класи

В попередній статті про [this](./this.md) ми розглядали 2 методи створення об'єктів, і зупинилася на функціях конструктора, внизу я продублював приклад: 
```js
function User(firstName, lastName, age) {
  this.firstName = firstName;
  this.lastName = lastName;
  this.age = age;

  this.getFullName = function() {
    return this.firstName + ' ' + this.lastName;
  }
}

const user = new User('John', 'Carter', 20);
```

На цей час, ми вже не використовуємо функції конструктори в тому вигляді, в якому ти їх бачиш в прикладі вище, в 2016 році, в Javascript з'явився так званий синтаксичний цукор, який спрощує роботу з функціями конструкторами, він не приніс нічого нового, окрім синтаксису створення.

```js
class Cat {
  constructor(nickname, age) {
    this.nickname = nickname;
    this.age = age;
    
    this.say = function() {
      return 'мяу'
    }
  }
}

const cat = new Cat('Oni-chan', 1);
```

По-перше, різниці між `User` і `Cat` не має, вони всі роблять те ж саме, створюють об'єкти певного типу, спосіб створення `Cat` базується на тому способі, що ми робили в `User`. Тобто `Cat` - це сучасний спосіб, `User` - застарілий.

По-друге, `User` - це функція, яка і є конструктором, вона повертає об'єкт, у випадку з `Cat` - в нас тут новий синтаксис, і коли створюючи нового юзера ми викликали `new User()` і в нас спрацьовувала функція `User`, то у випадку з `class` при написанні `new Cat()` в нас буде спрацьовувати метод `constructor`.

По-третє, коли ти пишеш `new Cat('Oni-chan', 1)` всі аргументи передаються в метод `constructor`, і далі відбувається все те ж саме, що і в старому синтаксисі, тобто створюється пустий об'єкт, далі `this` в цій функції (в нашому випадку це конструктор) буде посилатися на цей пустий об'єкт, і в кінці він поверне його.

По-четверте, тепер якщо твій об'єкт повинен мати якийсь метод, якщо говорити про наш `Cat`, в конструкторі ми створювали метод `say`
```js
    this.say = function() {
      return 'мяу'
    }
```

Тепер якщо ти хочеш мати якийсь метод, його потрібно писати просто в середині нашого класу, таким чином:

```js
class Cat {
  constructor(nickname, age) {
    this.nickname = nickname;
    this.age = age;
  }
  
  say() {
    return 'мяу'
  }
}

const cat = new Cat('Oni-chan', 1);

cat.say(); // 'мяу'
```


> Уважно. В старому синтаксисі, до класів, методи записувалися так як в `User`:
>
> `this.methodName = function() {}`
>
> В новому синтаксисі, як в `Cat`, ти просто в середині класу пишеш:
>
> `methodName() {}`