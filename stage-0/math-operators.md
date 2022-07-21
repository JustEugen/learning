# Math operators / Математичні оператори
Тут все як в математиці:
- `+` - додати
- `-` - відняти 
- `*` - помножити
- `/` - поділити

Приклади:
```js
const result = 10 + 20;

console.log(result); // 30
```

```js
const result = 100 - 30;

console.log(result); // 70
```

```js
const result = 10 * 5;

console.log(result); // 50
```

```js
const result = 10 / 2;

console.log(result); // 5
```

Окрім того, всі ці оператори, можна комбінувати з присвоєнням

```js
let count = 10;

count += 20;

console.log(count); // 30

// По суті - це скорочення до
let count = 10;

count = count + 20;

console.log(count); // 30
```

Це працює зі всіма математичними операторами, нижче приклад для множення

```js
let count = 10;

count *= 8;

console.log(count); // 80
```

Особисто для мене, простіше не використовувати математичні оператори з присвоєнням, їх трохи важче читати очима чим просто `count = count + 10;`, але можливо це більше справа смаку.

Ще є така штука як `increment`, і `decrement`. Якщо коротко - `increment` додає 1 до числа, а `decrement` віднімає 1 від числа.

Щоб використати `increment`, ми після числа чи змінної повинні написати два плюси `++`

```js
let count = 10;

count++;

console.log(count); // 11
```

Ми можемо використовувати `increment` стільки разів, скільки ми хочемо

```js
let count = 10;

count++;
count++;
count++;
count++;
count++;

console.log(count); // 15
```

Щоб використати `decrement`, ми після числа чи змінної повинні написати два мінуси `--`. Використання не відрізняється від `increment`

```js
let count = 10;

count--;
count--;
count--;
count--;
count--;

console.log(count); // 5
```

