# React основи

React - це бібліотека для рендеру і контролю стейта

Основа React - це компоненти.

Компоненти - це будівельні блоки, використовуючи які, ми будуємо наш додаток, все зав'язано на них. 

Як тільки ти створиш свій додаток, там буде тільки одна компонента App, яка знаходиться в середині файлу App.js. Компонента сама по собі - це функція, що повертає React елемент, на основі яких, React будує DOM дерево, тобто будує html сторінку.

> Правило! Компоненти повинні називатися з великої літери.

Задача: потрібно в компоненті App, вивести на екран div, в якій буде кнопка і текст в <span />

```jsx
export default function App() {
  return React.createElement('div', {}, [
    React.createElement('button', {}, 'click on me'),
    React.createElement('span', {}, 'hello'),
  ]);
}
```
От що ми побачимо в html
```html
<div>
  <button>click on me</button>
  <span>hello</span>
</div>
```
Тепер давай розберемо цей приклад по частинам. Перш за все, як я і казав, компоненти повинні повертати react елемент, використовуючи функцію `createElement` ми можемо створювати елементи.

`createElement` - приймає 3 параметри
1. Назву тегу, тобто якщо передасиш 'div' він створить `<div></div>`
2. Об'єкт атрибутів, ми про це ще пізніше поговоримо детальніше, тобто для прикладу className, id, якщо наприклад це тег `<a></a>`, то наприклад `href
3. Діти, у вигляді масиву react елементів. Якщо звернути увагу на приклад, то ми створили div, в якості дітей якого button і span, і якщо ти відкриєш html сторінки, то побачиш, що вони в середині цього div

Я думаю з назвою тегів в загальному все зрозуміло, давай на прикладі глянемо що таке об'єкт атрибутів

```jsx
export default function App() {
  return React.createElement('div', { className: 'wrapper' }, [
    React.createElement('button', { type: 'submit' }, 'click on me'),
    React.createElement('span', { id: '4' }, 'hello'),
    React.createElement(
      'a',
      { href: 'https://www.google.com' },
      'link to google'
    ),
  ]);
}
```

І ось що нам поверне ось такий код
```html
<div class="wrapper">
  <button type="submit">click on me</button>
  <span id="4">hello</span>
  <a href="https://www.google.com">link to google</a>
</div>
```

Тобто звичайні атрибути в html, єдине на що я хочу звернути увагу, так це на `CSS` класи, якщо в html атрибут називався просто `class`, то в реакт ти маєш писати замість нього `className`, це все через те, що слово `class` в javascript зарезервоване, і тобі треба буде писати костилі, щоб його використовувати 
