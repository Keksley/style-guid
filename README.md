- Используйте `const` для объявления переменных; избегайте `var`. eslint: [`prefer-const`](https://eslint.org/docs/rules/prefer-const.html), [`no-const-assign`](https://eslint.org/docs/rules/no-const-assign.html)

    > Почему? Это гарантирует, что вы не сможете переопределять значения, т.к. это может привести к ошибкам и к усложнению понимания кода.

    ```javascript
    // плохо
    var a = 1;
    var b = 2;

    // хорошо
    const a = 1;
    const b = 2;
    ```

- Если вам необходимо переопределять значения, то используйте `let` вместо `var`. eslint: [`no-var`](https://eslint.org/docs/rules/no-var.html)

    > Почему? Область видимости `let` — блок, у `var` — функция.

    ```javascript
    // плохо
    var count = 1;
    if (true) {
      count += 1;
    }

    // хорошо, используйте let.
    let count = 1;
    if (true) {
      count += 1;
    }
    ```

- Используйте сокращённую запись метода объекта. eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)

    ```javascript
    // плохо
    const atom = {
      value: 1,

      addValue: function (value) {
        return atom.value + value;
      },
    };

    // хорошо
    const atom = {
      value: 1,

      addValue(value) {
        return atom.value + value;
      },
    };
    ```

- Используйте сокращённую запись свойств объекта. eslint: [`object-shorthand`](https://eslint.org/docs/rules/object-shorthand.html)

    > Почему? Это короче и понятнее.

    ```javascript
    const lukeSkywalker = 'Luke Skywalker';

    // плохо
    const obj = {
      lukeSkywalker: lukeSkywalker,
    };

    // хорошо
    const obj = {
      lukeSkywalker,
    };
    ```

- Группируйте ваши сокращённые записи свойств в начале объявления объекта.

    > Почему? Так легче сказать, какие свойства используют сокращённую запись.

    ```javascript
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

- Используйте оператор расширения вместо [`Object.assign`](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Object/assign) для поверхностного копирования объектов. Используйте синтаксис оставшихся свойств, чтобы получить новый объект с некоторыми опущенными свойствами.

    ```javascript
    // очень плохо
    const original = { a: 1, b: 2 };
    const copy = Object.assign(original, { c: 3 }); // эта переменная изменяет `original` ಠ_ಠ
    delete copy.a; // если сделать так

    // плохо
    const original = { a: 1, b: 2 };
    const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1, b: 2, c: 3 }

    // хорошо
    const original = { a: 1, b: 2 };
    const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

    const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
    ```

- Для создания массива используйте литеральную нотацию. eslint: [`no-array-constructor`](https://eslint.org/docs/rules/no-array-constructor.html)

    ```javascript
    // плохо
    const items = new Array();

    // хорошо
    const items = [];
    ```

- Для добавления элемента в массив используйте [Array#push](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Array/push) вместо прямого присваивания.

    ```javascript
    const someStack = [];

    // плохо
    someStack[someStack.length] = 'abracadabra';

    // хорошо
    someStack.push('abracadabra');
    ```

- Для копирования массивов используйте оператор расширения `...`.

    ```javascript
    // плохо
    const len = items.length;
    const itemsCopy = [];
    let i;

    for (i = 0; i < len; i += 1) {
      itemsCopy[i] = items[i];
    }

    // хорошо
    const itemsCopy = [...items];
    ```

- Если массив располагается на нескольких строках, то используйте разрывы строк после открытия и перед закрытием скобок.

    ```javascript
    // плохо
    const arr = [
      [0, 1], [2, 3], [4, 5],
    ];

    const objectInArray = [{
      id: 1,
    }, {
      id: 2,
    }];

    const numberInArray = [
      1, 2,
    ];

    // хорошо
    const arr = [[0, 1], [2, 3], [4, 5]];

    const objectInArray = [
      {
        id: 1,
      },
      {
        id: 2,
      },
    ];

    const numberInArray = [
      1,
      2,
    ];
    ```

- При обращении к нескольким свойствам объекта используйте деструктуризацию объекта. eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

    > Почему? Деструктуризация избавляет вас от создания временных переменных для этих свойств.

    ```javascript
    // плохо
    function getFullName(user) {
      const firstName = user.firstName;
      const lastName = user.lastName;

      return `${firstName} ${lastName}`;
    }

    // хорошо
    function getFullName(user) {
      const { firstName, lastName } = user;
      return `${firstName} ${lastName}`;
    }

    // отлично
    function getFullName({ firstName, lastName }) {
      return `${firstName} ${lastName}`;
    }
    ```

- Используйте деструктуризацию массивов. eslint: [`prefer-destructuring`](https://eslint.org/docs/rules/prefer-destructuring)

    ```javascript
    const arr = [1, 2, 3, 4];

    // плохо
    const first = arr[0];
    const second = arr[1];

    // хорошо
    const [first, second] = arr;
    ```

- Используйте одинарные кавычки `''` для строк. eslint: [`quotes`](https://eslint.org/docs/rules/quotes.html)

    ```javascript
    // плохо
    const name = "Capt. Janeway";

    // плохо - литерал шаблонной строки должен содержать интерполяцию или переводы строк
    const name = `Capt. Janeway`;

    // хорошо
    const name = 'Capt. Janeway';
    ```

- Строки, у которых в строчке содержится более 100 символов, не пишутся на нескольких строчках с использованием конкатенации.

    > Почему? Работать с разбитыми строками неудобно и это затрудняет поиск по коду.

    ```javascript
    // плохо
    const errorMessage = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.';

    // плохо
    const errorMessage = 'This is a super long error that was thrown because ' +
      'of Batman. When you stop to think about how Batman had anything to do ' +
      'with this, you would get nowhere fast.';

    // хорошо
    const errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';
    ```

- При создании строки программным путём используйте шаблонные строки вместо конкатенации. eslint: [`prefer-template`](https://eslint.org/docs/rules/prefer-template.html) [`template-curly-spacing`](https://eslint.org/docs/rules/template-curly-spacing)

    > Почему? Шаблонные строки дают вам читабельность, лаконичный синтаксис с правильными символами перевода строк и функции интерполяции строки.

    ```javascript
    // плохо
    function sayHi(name) {
      return 'How are you, ' + name + '?';
    }

    // плохо
    function sayHi(name) {
      return ['How are you, ', name, '?'].join();
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

- Никогда не используйте `eval()`, т.к. это открывает множество уязвимостей. eslint: [`no-eval`](https://eslint.org/docs/rules/no-eval)

- Не используйте в строках необязательные экранирующие символы. eslint: [`no-useless-escape`](https://eslint.org/docs/rules/no-useless-escape)

    > Почему? Обратные слеши ухудшают читабельность, поэтому они должны быть только при необходимости.

    ```javascript
    // плохо
    const foo = '\'this\' \i\s \"quoted\"';

    // хорошо
    const foo = '\'this\' is "quoted"';
    const foo = `my name is '${name}'`;
    ```
- Используйте синтаксис записи аргументов по умолчанию, а не изменяйте аргументы функции.

    ```javascript
    // очень плохо
    function handleThings(opts) {
      // Нет! Мы не должны изменять аргументы функции.
      // Плохо вдвойне: если переменная opts будет ложной,
      // то ей присвоится пустой объект, а не то что вы хотели.
      // Это приведёт к коварным ошибкам.
      opts = opts || {};
      // ...
    }

    // всё ещё плохо
    function handleThings(opts) {
      if (opts === void 0) {
        opts = {};
      }
      // ...
    }

    // хорошо
    function handleThings(opts = {}) {
      // ...
    }
    ```
- Отступы при определении функции. eslint: [`space-before-function-paren`](https://eslint.org/docs/rules/space-before-function-paren) [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks)

    > Почему? Однородность кода — это хорошо. Вам не надо будет добавлять или удалять пробел при манипуляции с именем.

    ```javascript
    // плохо
    const f = function(){};
    const g = function (){};
    const h = function() {};

    // хорошо
    const x = function () {};
    const y = function a() {};
    ```

- Никогда не изменяйте параметры. eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign.html)

    > Почему? Манипуляция объектами, приходящими в качестве параметров, может вызывать нежелательные побочные эффекты в вызывающей функции.

    ```javascript
    // плохо
    function f1(obj) {
      obj.key = 1;
    }

    // хорошо
    function f2(obj) {
      const key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
    }
    ```

- Никогда не переназначайте параметры. eslint: [`no-param-reassign`](https://eslint.org/docs/rules/no-param-reassign.html)

    > Почему? Переназначенные параметры могут привести к неожиданному поведению, особенно при обращении к `arguments`. Это также может вызывать проблемы оптимизации, особенно в V8.

    ```javascript
    // плохо
    function f1(a) {
      a = 1;
      // ...
    }

    function f2(a) {
      if (!a) { a = 1; }
      // ...
    }

    // хорошо
    function f3(a) {
      const b = a || 1;
      // ...
    }

    function f4(a = 1) {
      // ...
    }
    ```

- Функции с многострочным определением или запуском должны содержать такие же отступы, как и другие многострочные списки в этом списке: с каждым элементом на отдельной строке, с запятой в конце элемента. eslint: [`function-paren-newline`](https://eslint.org/docs/rules/function-paren-newline)

    ```javascript
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

- Когда вам необходимо использовать анонимную функцию (например, при передаче встроенной функции обратного вызова), используйте стрелочную функцию. eslint: [`prefer-arrow-callback`](https://eslint.org/docs/rules/prefer-arrow-callback.html), [`arrow-spacing`](https://eslint.org/docs/rules/arrow-spacing.html)

    > Почему? Таким образом создаётся функция, которая выполняется в контексте `this`, который мы обычно хотим, а также это более короткий синтаксис.

    > Почему бы и нет? Если у вас есть довольно сложная функция, вы можете переместить эту логику внутрь её собственного именованного функционального выражения.

    ```javascript
    // плохо
    [1, 2, 3].map(function (x) {
      const y = x + 1;
      return x * y;
    });

    // хорошо
    [1, 2, 3].map((x) => {
      const y = x + 1;
      return x * y;
    });
    ```

- Если тело функции состоит из одного оператора, возвращающего [выражение](https://developer.mozilla.org/ru/docs/Web/JavaScript/Guide/Expressions_and_Operators#Выражения) без побочных эффектов, то опустите фигурные скобки и используйте неявное возвращение. В противном случае, сохраните фигурные скобки и используйте оператор `return`. eslint: [`arrow-parens`](https://eslint.org/docs/rules/arrow-parens.html), [`arrow-body-style`](https://eslint.org/docs/rules/arrow-body-style.html)

    > Почему? Синтаксический сахар. Когда несколько функций соединены вместе, то это лучше читается.

    ```javascript
    // плохо
    [1, 2, 3].map((number) => {
      const nextNumber = number + 1;
      `A string containing the ${nextNumber}.`;
    });

    // хорошо
    [1, 2, 3].map((number) => `A string containing the ${number + 1}.`);

    // хорошо
    [1, 2, 3].map((number) => {
      const nextNumber = number + 1;
      return `A string containing the ${nextNumber}.`;
    });

    // хорошо
    [1, 2, 3].map((number, index) => ({
      [index]: number,
    }));

    // Неявный возврат с побочными эффектами
    function foo(callback) {
      const val = callback();
      if (val === true) {
        // Сделать что-то, если функция обратного вызова вернёт true
      }
    }

    let bool = false;

    // плохо
    foo(() => bool = true);

    // хорошо
    foo(() => {
      bool = true;
    });
    ```


 - Избегайте схожести стрелочной функции (`=>`) с операторами сравнения (`<=`, `>=`). eslint: [`no-confusing-arrow`](https://eslint.org/docs/rules/no-confusing-arrow)

    ```javascript
    // плохо
    const itemHeight = (item) => item.height <= 256 ? item.largeSize : item.smallSize;

    // плохо
    const itemHeight = (item) => item.height >= 256 ? item.largeSize : item.smallSize;

    // хорошо
    const itemHeight = (item) => (item.height <= 256 ? item.largeSize : item.smallSize);

    // хорошо
    const itemHeight = (item) => {
      const { height, largeSize, smallSize } = item;
      return height <= 256 ? largeSize : smallSize;
    };
    ```

 - Зафиксируйте расположение тела стрелочной функции с неявным возвратом. eslint: [`implicit-arrow-linebreak`](https://eslint.org/docs/rules/implicit-arrow-linebreak)

    ```javascript
    // плохо
    (foo) =>
      bar;
    (foo) =>
      (bar);

    // хорошо
    (foo) => bar;
    (foo) => (bar);
    (foo) => (
       bar
    )
    ```
- Избегайте дублирующих членов класса. eslint: [`no-dupe-class-members`](https://eslint.org/docs/rules/no-dupe-class-members)

    > Почему? Если объявление члена класса повторяется, без предупреждения будет использовано последнее. Наличие дубликатов скорее всего приведёт к ошибке.

    ```javascript
    // плохо
    class Foo {
      bar() { return 1; }
      bar() { return 2; }
    }

    // хорошо
    class Foo {
      bar() { return 1; }
    }

    // хорошо
    class Foo {
      bar() { return 2; }
    }
    ```

- В модулях с единственным экспортом предпочтительнее использовать экспорт по умолчанию, а не экспорт по имени.
 eslint: [`import/prefer-default-export`](https://github.com/benmosher/eslint-plugin-import/blob/master/docs/rules/prefer-default-export.md)
    > Почему? Для того чтобы поощрять создание множества файлов, которые бы экспортировали одну сущность, т.к. это лучше для читабельности и поддержки кода.

    ```javascript
    // плохо
    export function foo() {}

    // хорошо
    export default function foo() {}
    ```

- Не используйте итераторы. Применяйте функции высшего порядка вместо таких циклов как `for-in` или `for-of`. eslint: [`no-iterator`](https://eslint.org/docs/rules/no-iterator.html) [`no-restricted-syntax`](https://eslint.org/docs/rules/no-restricted-syntax)

    > Почему? Это обеспечивает соблюдение нашего правила о неизменности переменных. Работать с чистыми функциями, которые возвращают значение, проще, чем с функциями с побочными эффектами.

    > Используйте `map()` / `every()` / `filter()` / `find()` / `findIndex()` / `reduce()` / `some()` / ... для итерации по массивам, а `Object.keys()` / `Object.values()` / `Object.entries()` для создания массивов, с помощью которых можно итерироваться по объектам.

    ```javascript
    const numbers = [1, 2, 3, 4, 5];

    // плохо
    let sum = 0;
    for (let num of numbers) {
      sum += num;
    }
    sum === 15;

    // хорошо
    let sum = 0;
    numbers.forEach((num) => {
      sum += num;
    });
    sum === 15;

    // отлично (используйте силу функций)
    const sum = numbers.reduce((total, num) => total + num, 0);
    sum === 15;

    // плохо
    const increasedByOne = [];
    for (let i = 0; i < numbers.length; i++) {
      increasedByOne.push(numbers[i] + 1);
    }

    // хорошо
    const increasedByOne = [];
    numbers.forEach((num) => {
      increasedByOne.push(num + 1);
    });

    // отлично (продолжайте в том же духе)
    const increasedByOne = numbers.map((num) => num + 1);
    ```
- В первую очередь группируйте `const`, а затем `let`.

    > Почему? Это полезно, когда в будущем вам понадобится создать переменную, зависимую от предыдущих.

    ```javascript
    // плохо
    let i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // плохо
    let i;
    const items = getItems();
    let dragonball;
    const goSportsTeam = true;
    let len;

    // хорошо
    const goSportsTeam = true;
    const items = getItems();
    let dragonball;
    let i;
    let length;
    ```
- Создавайте переменные там, где они вам необходимы, но помещайте их в подходящее место.

    > Почему? `let` и `const` имеют блочную область видимости, а не функциональную.

    ```javascript
    // плохо - вызов ненужной функции
    function checkName(hasName) {
      const name = getName();

      if (hasName === 'test') {
        return false;
      }

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }

    // хорошо
    function checkName(hasName) {
      if (hasName === 'test') {
        return false;
      }

      const name = getName();

      if (name === 'test') {
        this.setName('');
        return false;
      }

      return name;
    }
    ```
- Избегайте использования унарных инкрементов и декрементов (`++`, `--`). eslint [`no-plusplus`](https://eslint.org/docs/rules/no-plusplus)

    > Почему? Согласно документации eslint, унарные инкремент и декремент автоматически вставляют точку с запятой, что может стать причиной трудноуловимых ошибок при инкрементировании и декрементировании значений. Также нагляднее изменять ваши значения таким образом `num += 1` вместо `num++` или `num ++`. Запрет на унарные инкремент и декремент ограждает вас от непреднамеренных преждевременных инкрементаций/декрементаций значений, которые могут привести к непредсказуемому поведению вашей программы.

    ```javascript
    // плохо

    const array = [1, 2, 3];
    let num = 1;
    num++;
    --num;

    let sum = 0;
    let truthyCount = 0;
    for (let i = 0; i < array.length; i++) {
      let value = array[i];
      sum += value;
      if (value) {
        truthyCount++;
      }
    }

    // хорошо

    const array = [1, 2, 3];
    let num = 1;
    num += 1;
    num -= 1;

    const sum = array.reduce((a, b) => a + b, 0);
    const truthyCount = array.filter(Boolean).length;
    ```

- Используйте `===` и `!==` вместо `==` и `!=`. eslint: [`eqeqeq`](https://eslint.org/docs/rules/eqeqeq.html)

- Используйте сокращения для булевских типов, а для строк и чисел применяйте явное сравнение.

    ```javascript
    // плохо
    if (isValid === true) {
      // ...
    }

    // хорошо
    if (isValid) {
      // ...
    }

    // плохо
    if (name) {
      // ...
    }

    // хорошо
    if (name !== '') {
      // ...
    }

    // плохо
    if (collection.length) {
      // ...
    }

    // хорошо
    if (collection.length > 0) {
      // ...
    }
    ```

- При смешивании операторов, помещайте их в круглые скобки. Единственным исключением являются стандартные арифметические операторы: `+`, `-` и `**`, так как их приоритет широко известен. Мы рекомендуем заключить `/` и `*` в круглые скобки, поскольку их приоритет может быть неоднозначным, когда они смешиваются. eslint: [`no-mixed-operators`](https://eslint.org/docs/rules/no-mixed-operators.html)

    > Почему? Это улучшает читаемость и уточняет намерения разработчика.

    ```javascript
    // плохо
    const foo = a && b < 0 || c > 0 || d + 1 === 0;

    // плохо
    const bar = a ** b - 5 % d;

    // плохо
    // можно ошибиться, думая что это (a || b) && c
    if (a || b && c) {
      return d;
    }

    // плохо
    const bar = a + b / c * d;

    // хорошо
    const foo = (a && b < 0) || c > 0 || (d + 1 === 0);

    // хорошо
    const bar = a ** b - (5 % d);

    // хорошо
    if (a || (b && c)) {
      return d;
    }

    // хорошо
    const bar = a + (b / c) * d;
    ```


- Если блоки кода в условии `if` и `else` занимают несколько строк, расположите оператор `else` на той же строчке, где находится закрывающая фигурная скобка блока `if`. eslint: [`brace-style`](https://eslint.org/docs/rules/brace-style.html)

    ```javascript
    // плохо
    if (test) {
      thing1();
      thing2();
    }
    else {
      thing3();
    }

    // хорошо
    if (test) {
      thing1();
      thing2();
    } else {
      thing3();
    }
    ```
- Если в блоке `if` всегда выполняется оператор `return`, последующий блок `else` не нужен. `return`  внутри блока `else if`, следующем за блоком `if`, который содержит `return`, может быть разделён на несколько блоков `if`. eslint: [`no-else-return`](https://eslint.org/docs/rules/no-else-return)

    ```javascript
    // плохо
    function foo() {
      if (x) {
        return x;
      } else {
        return y;
      }
    }

    // плохо
    function cats() {
      if (x) {
        return x;
      } else if (y) {
        return y;
      }
    }

    // плохо
    function dogs() {
      if (x) {
        return x;
      } else {
        if (y) {
          return y;
        }
      }
    }

    // хорошо
    function foo() {
      if (x) {
        return x;
      }

      return y;
    }

    // хорошо
    function cats() {
      if (x) {
        return x;
      }

      if (y) {
        return y;
      }
    }

    // хорошо
    function dogs(x) {
      if (x) {
        if (z) {
          return y;
        }
      } else {
        return z;
      }
    }
    ```

- Если ваш управляющий оператор (`if`, `while` и т.д.) слишком длинный или превышает максимальную длину строки, то каждое (сгруппированное) условие можно поместить на новую строку. Логический оператор должен располагаться в начале строки.

    > Почему? Наличие операторов в начале строки приводит к выравниванию операторов и напоминает цепочку методов. Это также улучшает читаемость, упрощая визуальное отслеживание сложной логики.

    ```javascript
    // плохо
    if ((foo === 123 || bar === 'abc') && doesItLookGoodWhenItBecomesThatLong() && isThisReallyHappening()) {
      thing1();
    }

    // плохо
    if (foo === 123 &&
      bar === 'abc') {
      thing1();
    }

    // плохо
    if (foo === 123
      && bar === 'abc') {
      thing1();
    }

    // плохо
    if (
      foo === 123 &&
      bar === 'abc'
    ) {
      thing1();
    }

    // хорошо
    if (
      foo === 123
      && bar === 'abc'
    ) {
      thing1();
    }

    // хорошо
    if (
      (foo === 123 || bar === 'abc')
      && doesItLookGoodWhenItBecomesThatLong()
      && isThisReallyHappening()
    ) {
      thing1();
    }

    // хорошо
    if (foo === 123 && bar === 'abc') {
      thing1();
    }
    ```

- Ставьте 1 пробел перед открывающей фигурной скобкой у блока. eslint: [`space-before-blocks`](https://eslint.org/docs/rules/space-before-blocks.html)

    ```javascript
    // плохо
    function test(){
      console.log('test');
    }

    // хорошо
    function test() {
      console.log('test');
    }

    // плохо
    dog.set('attr',{
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });

    // хорошо
    dog.set('attr', {
      age: '1 year',
      breed: 'Bernese Mountain Dog',
    });
    ```

- Ставьте 1 пробел перед открывающей круглой скобкой в операторах управления (`if`, `while` и т.п.). Не оставляйте пробелов между списком аргументов и названием в объявлениях и вызовах функций. eslint: [`keyword-spacing`](https://eslint.org/docs/rules/keyword-spacing.html)

    ```javascript
    // плохо
    if(isJedi) {
      fight ();
    }

    // хорошо
    if (isJedi) {
      fight();
    }

    // плохо
    function fight () {
      console.log ('Swooosh!');
    }

    // хорошо
    function fight() {
      console.log('Swooosh!');
    }
    ```

- Разделяйте операторы пробелами. eslint: [`space-infix-ops`](https://eslint.org/docs/rules/space-infix-ops.html)

    ```javascript
    // плохо
    const x=y+5;

    // хорошо
    const x = y + 5;
    ```

- Используйте переносы строк и отступы, когда делаете длинные цепочки методов (больше 2 методов). Ставьте точку в начале строки, чтобы дать понять, что это не новая инструкция, а продолжение цепочки. eslint: [`newline-per-chained-call`](https://eslint.org/docs/rules/newline-per-chained-call) [`no-whitespace-before-property`](https://eslint.org/docs/rules/no-whitespace-before-property)

    ```javascript
    // плохо
    $('#items').find('.selected').highlight().end().find('.open').updateCount();

    // плохо
    $('#items').
      find('.selected').
        highlight().
        end().
      find('.open').
        updateCount();

    // хорошо
    $('#items')
      .find('.selected')
        .highlight()
        .end()
      .find('.open')
        .updateCount();

    // плохо
    const leds = stage.selectAll('.led').data(data).enter().append('svg:svg').classed('led', true)
        .attr('width', (radius + margin) * 2).append('svg:g')
        .attr('transform', `translate(${radius + margin},${radius + margin})`)
        .call(tron.led);

    // хорошо
    const leds = stage.selectAll('.led')
        .data(data)
      .enter().append('svg:svg')
        .classed('led', true)
        .attr('width', (radius + margin) * 2)
      .append('svg:g')
        .attr('transform', `translate(${radius + margin},${radius + margin})`)
        .call(tron.led);

    // хорошо
    const leds = stage.selectAll('.led').data(data);
    ```
- Оставляйте пустую строку между блоком кода и следующей инструкцией.

    ```javascript
    // плохо
    if (foo) {
      return bar;
    }
    return baz;

    // хорошо
    if (foo) {
      return bar;
    }

    return baz;

    // плохо
    const obj = {
      foo() {
      },
      bar() {
      },
    };
    return obj;

    // хорошо
    const obj = {
      foo() {
      },

      bar() {
      },
    };

    return obj;

    // плохо
    const arr = [
      function foo() {
      },
      function bar() {
      },
    ];
    return arr;

    // хорошо
    const arr = [
      function foo() {
      },

      function bar() {
      },
    ];

    return arr;
    ```


- Не добавляйте пробелы между квадратными скобками и их содержимым. eslint: [`array-bracket-spacing`](https://eslint.org/docs/rules/array-bracket-spacing.html)

    ```javascript
    // плохо
    const foo = [ 1, 2, 3 ];
    console.log(foo[ 0 ]);

    // хорошо
    const foo = [1, 2, 3];
    console.log(foo[0]);
    ```

- Добавляйте пробелы между фигурными скобками и их содержимым. eslint: [`object-curly-spacing`](https://eslint.org/docs/rules/object-curly-spacing.html)

    ```javascript
    // плохо
    const foo = {clark: 'kent'};

    // хорошо
    const foo = { clark: 'kent' };
    ```

- Старайтесь не допускать, чтобы строки были длиннее 100 символов (включая пробелы). Замечание: длинные строки с текстом освобождаются от этого правила и не должны разбиваться на несколько строк. eslint: [`max-len`](https://eslint.org/docs/rules/max-len.html)

    > Почему? Это обеспечивает удобство чтения и поддержки кода.

    ```javascript
    // плохо
    const foo = jsonData && jsonData.foo && jsonData.foo.bar && jsonData.foo.bar.baz && jsonData.foo.bar.baz.quux && jsonData.foo.bar.baz.quux.xyzzy;

    // плохо
    $.ajax({ method: 'POST', url: 'https://airbnb.com/', data: { name: 'John' } }).done(() => console.log('Congratulations!')).fail(() => console.log('You have failed this city.'));

    // хорошо
    const foo = jsonData
      && jsonData.foo
      && jsonData.foo.bar
      && jsonData.foo.bar.baz
      && jsonData.foo.bar.baz.quux
      && jsonData.foo.bar.baz.quux.xyzzy;

    // хорошо
    $.ajax({
      method: 'POST',
      url: 'https://airbnb.com/',
      data: { name: 'John' },
    })
      .done(() => console.log('Congratulations!'))
      .fail(() => console.log('You have failed this city.'));
    ```


- Избегайте пробелов между функциями и их вызовами. eslint: [`func-call-spacing`](https://eslint.org/docs/rules/func-call-spacing)

    ```javascript
    // плохо
    func ();

    func
    ();

    // хорошо
    func();
    ```

- Обеспечьте согласованное расстояние между ключами и значениями в свойствах литералов объекта. eslint: [`key-spacing`](https://eslint.org/docs/rules/key-spacing)

    ```javascript
    // плохо
    var obj = { "foo" : 42 };
    var obj2 = { "foo":42 };

    // хорошо
    var obj = { "foo": 42 };
    ```

- Избегайте пробелов в конце строки. eslint: [`no-trailing-spaces`](https://eslint.org/docs/rules/no-trailing-spaces)

- Добавляйте точку с запятой в конце инструкций. eslint: [`semi`](https://eslint.org/docs/rules/semi.html)

    > Почему? Когда JavaScript встречает перенос строки без точки с запятой, он использует правило под названием [Автоматическая Вставка Точки с запятой (Automatic Semicolon Insertion)](https://tc39.github.io/ecma262/#sec-automatic-semicolon-insertion), чтобы определить, стоит ли считать этот перенос строки как конец выражения и (как следует из названия) поместить точку с запятой в вашем коде до переноса строки. Однако, ASI содержит несколько странных форм поведения, и ваш код может быть сломан, если JavaScript неверно истолкует ваш перенос строки. Эти правила станут сложнее, когда новые возможности станут частью JavaScript. Явное завершение ваших выражений и настройка вашего линтера для улавливания пропущенных точек с запятыми помогут вам предотвратить возникновение проблем.

    ```javascript
    // плохо - выбрасывает исключение
    const luke = {}
    const leia = {}
    [luke, leia].forEach((jedi) => jedi.father = 'vader')

    // плохо - выбрасывает исключение
    const reaction = "No! That’s impossible!"
    (async function meanwhileOnTheFalcon() {
      // переносимся к `leia`, `lando`, `chewie`, `r2`, `c3p0`
      // ...
    }())

    // плохо - возвращает `undefined` вместо значения на следующей строке. Так всегда происходит, когда `return` расположен сам по себе, потому что ASI (Автоматическая Вставка Точки с запятой)!
    function foo() {
      return
        'search your feelings, you know it to be foo'
    }

    // хорошо
    const luke = {};
    const leia = {};
    [luke, leia].forEach((jedi) => {
      jedi.father = 'vader';
    });

    // хорошо
    const reaction = "No! That’s impossible!";
    (async function meanwhileOnTheFalcon() {
      // переносимся к `leia`, `lando`, `chewie`, `r2`, `c3p0`
      // ...
      }());

    // хорошо
    function foo() {
      return 'search your feelings, you know it to be foo';
    }
    ```

    [Читать подробнее](https://stackoverflow.com/questions/7365172/semicolon-before-self-invoking-function/7365214#7365214).


- Избегайте названий из одной буквы. Имя должно быть наглядным. eslint: [`id-length`](https://eslint.org/docs/rules/id-length)

    ```javascript
    // плохо
    function q() {
      // ...
    }

    // хорошо
    function query() {
      // ...
    }
    ```

- Используйте `camelCase` для именования объектов, функций и экземпляров. eslint: [`camelcase`](https://eslint.org/docs/rules/camelcase.html)

    ```javascript
    // плохо
    const OBJEcttsssss = {};
    const this_is_my_object = {};
    function c() {}

    // хорошо
    const thisIsMyObject = {};
    function thisIsMyFunction() {}
    ```

- Используйте `PascalCase` только для именования конструкторов и классов. eslint: [`new-cap`](https://eslint.org/docs/rules/new-cap.html)

    ```javascript
    // плохо
    function user(options) {
      this.name = options.name;
    }

    const bad = new user({
      name: 'nope',
    });

    // хорошо
    class User {
      constructor(options) {
        this.name = options.name;
      }
    }

    const good = new User({
      name: 'yup',
    });
    ```

- Не используйте `_` в начале или в конце названий. eslint: [`no-underscore-dangle`](https://eslint.org/docs/rules/no-underscore-dangle.html)

    > Почему? JavaScript не имеет концепции приватности свойств или методов. Хотя подчёркивание в начале имени является распространённым соглашением, которое показывает «приватность», фактически эти свойства являются такими же доступными, как и часть вашего публичного API. Это соглашение может привести к тому, что разработчики будут ошибочно думать, что изменения не приведут к поломке или что тесты не нужны. Итог: если вы хотите, чтобы что-то было «приватным», то оно не должно быть доступно извне.

    > Добавлю так же что у Vue могут быть проблемы со свойствами начинающимися с $ и _

    ```javascript
    // плохо
    this.__firstName__ = 'Panda';
    this.firstName_ = 'Panda';
    this._firstName = 'Panda';

    // хорошо
    this.firstName = 'Panda';

    // хорошо, в средах, где поддерживается WeakMaps
    // смотрите https://kangax.github.io/compat-table/es6/#test-WeakMap
    const firstNames = new WeakMap();
    firstNames.set(this, 'Panda');
    ```

- Не сохраняйте ссылку на `this`. Используйте стрелочные функции или [метод bind()](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Function/bind).

    ```javascript
    // плохо
    function foo() {
      const self = this;
      return function () {
        console.log(self);
      };
    }

    // плохо
    function foo() {
      const that = this;
      return function () {
        console.log(that);
      };
    }

    // хорошо
    function foo() {
      return () => {
        console.log(this);
      };
    }
    ```
- Сокращения или буквенные аббревиатуры всегда должны быть в верхнем или нижнем регистре.

    > Почему? Имена предназначены для удобства чтения.

    ```javascript
    // плохо
    import SmsContainer from './containers/SmsContainer';

    // плохо
    const HttpRequests = [
      // ...
    ];

    // хорошо
    import SMSContainer from './containers/SMSContainer';

    // хорошо
    const HTTPRequests = [
      // ...
    ];

    // также хорошо
    const httpRequests = [
      // ...
    ];

    // отлично
    import TextMessageContainer from './containers/TextMessageContainer';

    // отлично
    const requests = [
      // ...
    ];
    ```

- Если свойство/метод возвращает логический тип, то используйте названия `isVal()` или `hasVal()`.

    ```javascript
    // плохо
    if (!dragon.age()) {
      return false;
    }

    // хорошо
    if (!dragon.hasAge()) {
      return false;
    }
    ```

- Используйте `Number.isNaN` вместо глобального `isNaN`.
    eslint: [`no-restricted-globals`](https://eslint.org/docs/rules/no-restricted-globals)

    > Почему? Глобальная функция `isNaN` приводит не-числа к числам, возвращая `true` для всего, что приводится к `NaN`.
    > Если такое поведение необходимо, сделайте его явным.

    ```javascript
    // плохо
    isNaN('1.2'); // false
    isNaN('1.2.3'); // true

    // хорошо
    Number.isNaN('1.2.3'); // false
    Number.isNaN(Number('1.2.3')); // true
    ```

- Используйте `Number.isFinite` вместо глобального `isFinite`.
    eslint: [`no-restricted-globals`](https://eslint.org/docs/rules/no-restricted-globals)

    > Почему? Глобальная функция `isFinite` приводит не-числа к числам, возвращая `true` для всего, что приводится к конечному числу.
    > Если такое поведение необходимо, сделайте его явным.

    ```javascript
    // плохо
    isFinite('2e3'); // true

    // хорошо
    Number.isFinite('2e3'); // false
    Number.isFinite(parseInt('2e3', 10)); // true
    ```
