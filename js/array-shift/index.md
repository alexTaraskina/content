---
title: "`.shift()`"
description: "Удаляет первый элемент массива и возвращает значение удалённого элемента."
authors:
  - vitya-ne
related:
  - js/array-pop
  - js/array-splice
  - js/array-unshift
tags:
  - doka
---

## Кратко

Метод `shift()` удаляет из массива элемент с индексом 0 и возвращает значение удалённого элемента.

## Пример

Удалим из массива цифр элемент с индексом 0:

```js
const numbers = [8, 16, 32, 64]
const firstItem = numbers.shift()

console.log(numbers)
// [16, 32, 64]

console.log(firstItem)
// 8
```

## Как пишется

`Array.shift` не имеет аргументов.

`Array.shift` возвращает удалённый элемент.

Если массив не имеет элементов, метод вернёт `undefined`:

```js
const numbers = []
const firstItem = numbers.shift()
console.log(firstItem)
// undefined
```

## Как понять

Для нумерации элементов в массиве используются индексы. Первый элемент массива имеет индекс 0.

Метод `shift()` позволяет удалить из массива первый элемент или, говоря иначе, элемент с индексом 0, выполняя сдвиг всех элементов влево.

<details>
  <summary>
    Подробнее о сдвиге
  </summary>

  Согласно спецификации ECMAScript, алгоритм работы метода `shift()` включает цикл, предназначенный для сдвига элементов.

  Для наглядности выполним метод `shift()` для массивоподобного объекта. Для этого необходимо, чтобы объект имел поле `length`, определяющее количество элементов. Порядок следования полей-элементов в объекте не влияет на работу метода, потому что доступ к значениям осуществляется по ключам-индексам:

  ```js
  const arrayLike = {
    2: 'two',
    1: 'one',
    0: 'zero',
    length: 3
  }

  console.log(arrayLike)
  // {'0': 'zero', '1': 'one', '2': 'two', length: 3}

  Array.prototype.shift.call(arrayLike)

  console.log(arrayLike)
  // {'0': 'one', '1': 'two', length: 2}
  ```

  В результате работы метода все оставшиеся поля-элементы были записаны с новыми ключами-индексами и изменилось поле `length`.

</details>

Для удаления первого элемента также может быть использован метод `splice()`:

```js
const colors = ['red', 'green', 'blue']
colors.splice(0, 1)
console.log(colors)
// ['green', 'blue']
```