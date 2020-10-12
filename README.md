#JS-Guide

# h1 JavaScript Style Guide

## h2 Объекты

Для создания объекта используйте литеральную нотацию. eslint: [no-new-object](https://eslint.org/docs/rules/no-new-object.html)

``` js
// плохо
const item = new Object();

// хорошо
const item = {};
```

Группируйте ваши сокращённые записи свойств в начале объявления объекта.

``` js
const anakinSkywalker = 'Anakin Skywalker';
const lukeSkywalker = 'Luke Skywalker';

// плохо
const obj = {
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  lukeSkywalker,
  episodeThree: 3,
  mayTheFourth: 4,
  anakinSkywalker,
};

// хорошо
const obj = {
  lukeSkywalker,
  anakinSkywalker,
  episodeOne: 1,
  twoJediWalkIntoACantina: 2,
  episodeThree: 3,
  mayTheFourth: 4,
};
```

## h2 Строки

Используйте одинарные кавычки `''` для строк. eslint: [quotes](https://eslint.org/docs/rules/quotes.html)

``` js
// плохо
const name = "Capt. Janeway";

// плохо - литерал шаблонной строки должен содержать интерполяцию или переводы строк
const name = `Capt. Janeway`;

// хорошо
const name = 'Capt. Janeway';
```

При создании строки программным путём используйте шаблоные строки вместо конкатенации.
eslint: [prefer-template](https://eslint.org/docs/rules/prefer-template.html) [template-curly-spacing](https://eslint.org/docs/rules/template-curly-spacing)

``` js
// плохо
function sayHi(name) {
  return 'How are you, ' + name + '?';
}

// плохо
function sayHi(name) {
  return ['How are you, ', name, '?'];
}

// плохо
function sayHi(name) {
  return `How are you, ${ name }?`;
}

// хорошо
function sayHi(name) {
  return `How are you, ${name}?`;
}
```

## h2 Функции

Функции с многостроным определением или запуском должны содержать такие же
отступы, как и другие многострочные списки в этом руководстве: с каждым элементом
на отдельной строке, с запятой в конце элемента. eslint: [function-paren-newline](https://eslint.org/docs/rules/function-paren-newline)

``` js
// плохо
function foo(bar,
            baz,
            quux) {
  // ...
}

// хорошо
function foo(
  bar,
  baz,
  quux,
) {
  // ...
}

// плохо
console.log(foo,
  bar,
  baz);

// хорошо
console.log(
  foo,
  bar,
  baz,
);
```

Избегайте схожести стрелочной функции (`=>`) с операторами сравнения (`<=`, `>=`).
eslint: [no-confusing-arrow](https://eslint.org/docs/rules/no-confusing-arrow)

``` js
// плохо
const itemHeight = (item) => item.height <= 256 ? item.largeSize : item.smallSize;

// плохо
const itemHeight = (item) => item.height >= 256 ? item.largeSize : item.smallSize;

// хорошо
const itemHeight = (item) => (item.height <= 256 ? item.largeSize : item.smallSize);

// хорошо
const itemHeight = (item) => {
  const {height, largeSize, smallSize} = item;
  return height <= 256 ? largeSize : smallSize;
};
```

## h2 Классы и конструкторы

Используйте `class`. Избегайте прямых манипуляций с prototype.

``` js
// плохо
function Queue(contents = []) {
  this.queue = [...contents];
}
Queue.prototype.pop = function () {
  const value = this.queue[0];
  this.queue.splice(0, 1);
  return value;
};

// хорошо
class Queue {
  constructor(contents = []) {
    this.queue = [...contents];
  }
  pop() {
    const value = this.queue[0];
    this.queue.splice(0, 1);
    return value;
  }
}
```

Используйте `extends` для наследования.

``` js
// плохо
const inherits = require('inherits');
function PeekableQueue(contents) {
  Queue.apply(this, contents);
}
inherits(PeekableQueue, Queue);
PeekableQueue.prototype.peek = function () {
  return this.queue[0];
};

// хорошо
class PeekableQueue extends Queue {
  peek() {
    return this.queue[0];
  }
}
```

## h2 Свойства

Используйте точечную нотацию для доступа к свойствам. eslint: [dot-notation](https://eslint.org/docs/rules/dot-notation.html)

``` js
const luke = {
  jedi: true,
  age: 28,
};

// плохо
const isJedi = luke['jedi'];

// хорошо
const isJedi = luke.jedi;
```

Используйте объявление `const` или `let` для каждой переменной или присвоения.
eslint: [one-var](https://eslint.org/docs/rules/one-var.html)

``` js
// плохо
const items = getItems(),
    goSportsTeam = true,
    dragonball = 'z';

// плохо
const items = getItems(),
    goSportsTeam = true;
    dragonball = 'z';

// хорошо
const items = getItems();
const goSportsTeam = true;
const dragonball = 'z';
```