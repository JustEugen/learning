# Components and props
В основах реакту, я казав, що компоненти - це будівельні блоки, з яких ми будуємо наш додаток.

Для того щоб створити компоненту, потрібно просто створити файл, з великою літерою, і з цього файлу експортувати цю компоненту

В нас буде наступна задача - уяви, що ми праюцємо над блог додатком, і нам потрібно виводити статті, давай нашої статті, створимо окрему компоненету, яка буде займатися суто роботою, потрібною для виводу цієї статті.

Наша стаття буде показувати не багато, `title`, `date` і `description`

`./Article.js`
```jsx
export const Article = () => {
  return React.createElement('div', {}, [
    React.createElement('div', {}, 'How to code?'),
    React.createElement('div', {}, '2022/05/15'),
    React.createElement('div', {}, 'This is test description, and I have not idea what coding is'),
  ])
}
```

Тепер, нам потрібно якось цю компоненту використати. Ми будемо виводити її в середині 

`App.js`
```js
export default function App() {
  return React.createElement('div', {}, [
    React.createElement(Article, {}, null),
  ]);
}
```

Для того щоб використати комопненту, ми так само використовуємо `React.createElement`, тільки тут, деякі моменти будуть відрізнятися від звичайних html тегів. По перше, в якості першого параметру ми передаємо нашу компоненту, на місці атрибутів, ми поки залишаємо звичайний об'єкт, і на місці дітей, ми ставимо null, томущо в нашої компоненти не має ніяких дітей, я потім поясню детальніше що це, томущо діти компоненти і діти html тега різняться трішки.

Якщо ти подивишся на екран, то ти побачиш цю компоненту, і як казалося раніше, компоненти - це будівельні блоки, тому ми будемо використовувати її стільки разів, скільки хочемо 

`App.js`
```js
export default function App() {
  return React.createElement('div', {}, [
    React.createElement(Article, {}, null),
    React.createElement(Article, {}, null),
    React.createElement(Article, {}, null),
    React.createElement(Article, {}, null),
    React.createElement(Article, {}, null),
  ]);
}
```

Тепер питання номер 2, на разі, всі наші статті виводять ту ж саму інформацію, тому в принципі від цієї компоненти не має особо і толку, давай тоді розберемося яким чином ми можемо передавати щось, в середину нашої компоненти.

Якщо ти пам'ятаєш, коли ми створювали `div`, ми передавали туди якісь атрибути, наприклд `className`,

```jsx
React.createElement('div', { className: 'some-div' }, null)
```

Таким самим чином, ми можемо передавати якісь данні в нашу компоненту, єдине що, тепер це буде називатися не об'єкт атрибутів, а пропси (props) від слова properties.

Давай спробуємо передати туди`title`, `date` і `description`

`App.js`
```js
export default function App() {
  return React.createElement('div', {}, [
    React.createElement(
      Article, 
      { titlte: "How watch anime", date: "2022/01/14", description: 'some Description'},
      null
    ),
  ]);
}
```

Отже, в цьому прикладі, ми використали компоненту `Article` і передали в неї об'єкт просів, тепер нам треба переписати нашу комопненту `Article` так, щоб вона використовували пропси, щоб показувати певну інформацію, робиться це дуже просто.

Кожна компонента першим аргументом приймає об'єкт пропсів
`./Article.js`
```jsx
export const Article = (props) => {
  return React.createElement('div', {}, [
    React.createElement('div', {}, props.title),
    React.createElement('div', {}, props.date),
    React.createElement('div', {}, props.description),
  ])
}
```

Якщо запустити приклад, ти побачеш, що тепер наша компонента виводить те, що їй приходить з пропсів. Спробуй трохи поексперементувати, і побачиш що воно дійсно працює.

Тепер один нюанс, який я хотів обговорити. Коли ми проходили функції, я казав, що функції вони самодостаточні, вони можуть приймати якісь аргументи, і ти не можеш гарантувати, що якийсь інший розробник, передасть туди саме те що треба, і він сам має зайти, і подивитися, що має приймати функція, яку він хоче використовувати. Тут така сама хєрня. От диви, в нас є компонента Article, і вона використовує пропси, щоб щось виводити на екран. Інший розробник, або навіть ти, який буде використовувати цю компоненту, повинен передати сюди title, date і description, і це буде його проблема, якщо він сюди нічого не передасть, або передасть щось не то, він має зайти, перевірити, і вже тоді зробити, а не пуляти наугад, ну а ми, в свою чергу, маємо писати код так, щоб було зрозуміло що відбувається в середині.

### Array render
Давай тепер зробимо наступне, всі наші `article` ми будемо зберігати в масиві, і будемо виводити всі статті які є в масиві

`App.js`
```js
export default function App() {
  const articles = [
    {
      id: 1,
      title: 'Some random stuff 1',
      description: 'Some random description 1',
      date: 'Some random date 1'
    },
    {
      id: 2,
      title: 'Some random stuff 3',
      description: 'Some random description 2',
      date: 'Some random date 2'
    },
    {
      id: 3,
      title: 'Some random stuff 3',
      description: 'Some random description 3',
      date: 'Some random date 3'
    },
  ]
  
  return React.createElement('div', {}, [
  ]);
}
```

Тепер ми зберігаємо всі наші статті в середині масива, тепер потрібно їх якось вивести. Для цього ми можемо застосувати функцію `map` на масиві `articles` і на його основі створити масив react elements і вже будемо виводити його

`App.js`
```js
export default function App() {
  const articles = [
    {
      id: 1,
      title: 'Some random stuff 1',
      description: 'Some random description 1',
      date: 'Some random date 1'
    },
    {
      id: 2,
      title: 'Some random stuff 3',
      description: 'Some random description 2',
      date: 'Some random date 2'
    },
    {
      id: 3,
      title: 'Some random stuff 3',
      description: 'Some random description 3',
      date: 'Some random date 3'
    },
  ]
  
  const articlesElements = articles.map(article => {
    return React.createElement(
      Article,
      { 
        titlte: article.title,
        date: article.date,
        description: article.description
      },
      null
    );
  })
  
  return React.createElement('div', {}, articlesElements);
}
```

Але тут є один нюанс, якщо ти виводиш, в масиві елементи, теги яких повторються, ти повинен передати їм пропсу key, це до речі також стосуюється компоненти `Article` де ми в ряд виводимо 3 `div`, тому це потрібно виправити. Головна вимога до цього `key` - він повинен бути унікальний поміж сусідів.

`App.js`
```js
export default function App() {
  const articles = [
    {
      id: 1,
      title: 'Some random stuff 1',
      description: 'Some random description 1',
      date: 'Some random date 1'
    },
    {
      id: 2,
      title: 'Some random stuff 3',
      description: 'Some random description 2',
      date: 'Some random date 2'
    },
    {
      id: 3,
      title: 'Some random stuff 3',
      description: 'Some random description 3',
      date: 'Some random date 3'
    },
  ]
  
  const articlesElements = articles.map(article => {
    return React.createElement(
      Article,
      { 
        key: article.id,
        titlte: article.title,
        date: article.date,
        description: article.description
      },
      null
    );
  })
  
  return React.createElement('div', {}, articlesElements);
}
```

`./Article.js`
```jsx
export const Article = (props) => {
  return React.createElement('div', {}, [
    React.createElement('div', {key: 1}, props.title),
    React.createElement('div', {key: 2}, props.date),
    React.createElement('div', {key: 3}, props.description),
  ])
}
```
