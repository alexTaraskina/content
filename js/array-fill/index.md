---
title: "`.fill()`"
description: "Заполняет элементы массива указанным значением."
authors:
  - vitya-ne
related:
  - js/arrays
  - js/array-splice
  - js/array-from
tags:
  - doka
---

## Кратко

Метод `fill()` заполняет часть или все элементы массива одним и тем же значением.

## Пример

Заменим все значения на 'purple':

```js
const colors = ['red', 'green', 'white']
colors.fill('purple')

console.log(colors)
// ['purple', 'purple', 'purple']
```

Заменим все значения, начиная с третьего элемента:

```js
const skills = ['HTML', 'CSS', 'JS', 'Python']
skills.fill(null, 2)

console.log(skills)
// ['HTML', 'CSS', null, null]
```

## Как пишется

`Array.fill()` принимает три аргумента:

- значение, которым будут заполняться элементы массива;
- необязательный параметр, определяющий индекс элемента с которого будет производиться заполнение массива новым значением;
- необязательный параметр, определяющий индекс элемента перед которым прекратится заполнение массива.

`Array.fill()` возвращает изменённый массив.

Метод `fill()` является изменяющим методом. После выполнения метода изменится сам массив, на котором он был вызван.

Если индекс начала изменений не указан, новое значение будет заполнять массив с начала. Если индекс конца изменений не указан, новое значение будет заполнять массив до конца.

Отрицательные индексы используются для отсчёта от последнего элемента массива.

Заменим значение двух последних элементов:

```js
const skills = ['HTML', 'CSS', 'JS', 'Python']
skills.fill('React', -2)

console.log(skills)
// ['HTML', 'CSS', 'React', 'React']
```

Если попытаться использовать диапазон изменений, несоответствующий размеру массива, никаких изменений не произойдёт:

```js
const fruits = ['яблоко', 'апельсин', 'банан', 'манго']
fruits.fill('лимон', -2, -3)

console.log(fruits)
// ['яблоко', 'апельсин', 'банан', 'манго']
```

## Как понять

Метод `fill()` — удобный способ заполнить массив одним и тем же значением. Обычно это необходимо при инициализации массива.

Напишем функцию для создания и заполнения массива нужной длины значением `null`:

```js
const createNullArr = (length) =>
{
  const array = Array(length)
  return array.fill(null)
}

console.log(createNullArr(5))
// [null, null, null, null, null]
```

Если значение, используемое для заполнения, является объектом, метод `fill()` будет использовать для заполнения ссылку на этот объект. Это важная особенность может привести к неожиданному поведению.

Создадим массив и заполним его объектом:

```js
const persons = Array(3)
persons.fill({name: 'имя', position: null})

console.log(persons)
// [
//  { name: 'имя', position: null },
//  { name: 'имя', position: null },
//  { name: 'имя', position: null }
// ]
```
Изменим первый элемент:

```js
persons[0].name = 'София'
console.log(persons)
// Ой, изменились все элементы!
// [
//   { name: 'София', position: null },
//   { name: 'София', position: null },
//   { name: 'София', position: null }
// ]
```

## Подсказки

💡 Для корректного заполнения массива значениями непримитивого типа можно воспользоваться методом `Array.from()`:

```js
const persons = Array.from( new Array(3), () => ({ name: 'имя', position: null }))
persons[0].name = 'София'

console.log(persons)
// [
//   { name: 'София', position: null },
//   { name: 'имя', position: null },
//   { name: 'имя', position: null }
// ]
```

💡 Для незаполненных элементов, которые находятся в диапазоне, подлежащем изменению, будет установлено значение:

```js
const books = []

books[4] = 'Колыбель для кошки'

console.log(books)
// [ <4 empty items>, 'Колыбель для кошки' ]

console.log(books.fill('неизвестно', 1, 4))
// [
//   <1 empty item>,
//   'неизвестно',
//   'неизвестно',
//   'неизвестно',
//   'Колыбель для кошки'
// ]
```