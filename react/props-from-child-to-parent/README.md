# Як передати якісь данні від дитини до батька?

Ми вже проходили як можна передавати проси з батьківської компоненти в дитячу, але що, якщо нам потрібно інформувати батьківську компоненту про те що сталося в дитячій.

Для прикладу, в батьківській компоненті ми відображали масив статтів, а що якщо, кожна стаття мала би кнопку видалення, при натисканні на яку, нам потрібно цю статтю видаляти з масиву? 

Тут насправді все дуже просто, для цього, батьківська компонента повинна в пропси покласти функцію, яку вже буде викликати дитяча компонента

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
        description: article.description,
        onDelete: () => {
          console.log('delete article with id: ', article.id);
        }
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
    React.createElement('button', {key: 4, onClick: props.onDelete}, 'Delete'),
  ])
}
```

Якщо ми запустимо цей приклад, то ми побачимо, що якщо ми будемо натискати на кнопку, то буде виводится id статті.

Тепер нам потрібно зробити видалення статті, і після того як стаття буде видалена, потрібно щоб реакт перемалював компоненту. Для цього нам потрібно статті запихнути в `state`, тоді при змінну цього масиву, буде і ререндиритися компонента

`App.js`
```js
export default function App() {
  const [articles, setArticles] = useState([
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
  ]);
  
  const articlesElements = articles.map(article => {
    return React.createElement(
      Article,
      { 
        key: article.id,
        titlte: article.title,
        date: article.date,
        description: article.description,
        onDelete: () => {
          console.log('delete article with id: ', article.id);
        }
      },
      null
    );
  })
  
  return React.createElement('div', {}, articlesElements);
}
```

Тепер нюанс, раніше я вже говорив, що якщо ми хочемо змінити `state`, то нам потрібно викликати функцію, і в неї передати новий стейт, тут я хочу зауважити, що коли ми працюємо з об'єтками чи з масивами, ми в цю функцію повинні передавати новий масив, тобто скопіювати існуючий, змінити, і вставити.

В нашому випадку, нам потрібно видалити статтю, для цього найкраще підходить функція filter, окрім цього, функція filter не міняє оригінальний масив, а створює новий на основі оригінального

`App.js`
```js
export default function App() {
  const [articles, setArticles] = useState([
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
  ]);
  
  const articlesElements = articles.map(article => {
    return React.createElement(
      Article,
      { 
        key: article.id,
        titlte: article.title,
        date: article.date,
        description: article.description,
        onDelete: () => {
          const filteredArticle = articles.filter(element => element !== article.id)
          
          setArticles(filteredArticle);
        }
      },
      null
    );
  })
  
  return React.createElement('div', {}, articlesElements);
}
```
