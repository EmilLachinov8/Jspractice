# *JS Practice *

# 1.Всегда объявляй локальные переменные.
 Нужно всегда объявлять локальные переменные и постоянные также с помощью  let или const. В противном случае переменная будет объявлена как глобальная и как свойство объекта window.
   Плохо :
```
var x = 1;

function myFunction(x, y) {
  if (y === undefined) {
    y = x+1;
  }
}
```
  Хорошо:
```
const x = 1;

function myFunction(x, y) {
  if (y === undefined) {
    y = x+1;

  }
}
```

# 2. Инициализируй переменные наверху
+ Объявление переменных  вверху файла делает код чище.
+ Это помешает случайно ссылаться на переменные.
+ Уменьшает возможность нежелательных повторных объявлений.
  Плохо:
```
let x, y;
x = 1;
y = 1;
console.log(x, y);
```
  Хорошо:
```
let x = 1;
let y = 1;
console.log(x, y);
```

# 3.Не используй new Object()
+ Используйте {} вместо new Object()
+ Используйте 0 вместо new Number()
+ Используйте false вместо new Boolean()
+ Используйте [] вместо new Array()
+ Используйте /()/ вместо new RegExp()
+ Используйте function (){} вместо new Function()
  Хорошие примеры :
```
let x1 = {};           // new object
let x2 = "";           // new primitive string
let x3 = 0;            // new primitive number
let x4 = false;        // new primitive boolean
let x5 = [];           // new array object
let x6 = /()/;         // new regexp object
let x7 = function(){}; // new function object
```
Это упрощает код и повышает читабельность.

# 4. Для создания массива используйте литеральную нотацию. Это упростит код

 Хорошо:
 ```
const items = new Array();
```
 Плохо:
 ```
const items = [];
```

# 5. Не вызывай напрямую методы `Object.prototype`, такие как `hasOwnProperty`, `propertyIsEnumerable`, и `isPrototypeOf`.
 Эти методы могут быть переопределены в свойствах объекта, который мы проверяем `{ hasOwnProperty: false }`, или этот объект может быть `null` (`Object.create(null)`).

 Плохо:
 ```
console.log(object.hasOwnProperty(key));

```
 Хорошо:

 ```
console.log(Object.prototype.hasOwnProperty.call(object, key));

const has = Object.prototype.hasOwnProperty;

console.log(has.call(object, key));

```

#6. Избегай использования eval ()
+ Функция eval() используется для запуска текста как кода.
+ eval() - опасная функция, которая выполняет код, проходящий со всеми привилегиями вызывателя. Если вы запускаете eval() со строкой, на которую могут влиять злоумышленники, то вы можете запустить вредоносный код на устройство пользователя с правами вашей веб-страницы/расширения.
+ Наиболее важно, код третьей стороны может видеть область видимости, в которой был вызван eval().
+ eval(),как правило, медленнее альтернатив, так как вызывает интерпретатор JS, тогда как многие другие конструкции оптимизированы современными JS движками.
 Плохо:
```
let obj = { a: 20, b: 30 };
let propname = getPropName();  // возвращает "a" или "b"
eval( "let result = obj." + propname );
```
 Хорошо:
```
let obj = { a: 20, b: 30 };
let propname = getPropName();  // возвращает "a" или "b"
let result = obj[ propname ];  //  obj[ "a" ] то же, что и obj.a
```
#7. Используй === Сравнение

 Плохо:

Оператор ==с равнение всегда преобразуется перед сравнением

`0 == '';`

- Хороший код

Оператор === сравнивает значения и типы

`let 0==='';`

#8. Избегай автоматического преобразований типов
Помните, что числа могут быть случайно преобразованы в строки или NaN (не число).

JavaScript слабо типизирован. Переменная может содержать разные типы данных и изменять свой тип данных:
```
let x = "Hello";     // по типу x является строкой
x = 5;               // изменение типа x на число
```
При выполнении математических операций JavaScript может преобразовывать числа в строки:
```
let x = 5 + 7;       // x.valueOf() результат 12,  тип переменной x - число
let x = 5 + "7";     // x.valueOf() результат 57,  тип переменной x - строка
let x = "5" + 7;     // x.valueOf() результат 57,  тип переменной x - строка
let x = 5 - 7;       // x.valueOf() результат -2,  тип переменной x - число
let x = 5 - "7";     // x.valueOf() результат -2,  тип переменной x - число
let x = "5" - 7;     // x.valueOf() результат -2,  тип переменной x - число
let x = 5 - "x";     // x.valueOf() результат NaN, тип переменной x - число
```

#9. Не передавай строку в "SetInterval" или " SetTimeOut"
---
Если передавать само выражение функции в`SetInterval` или `SetTimeOut`, то это снижает эффективность и читабельность кода. Поэтому следует передавать только имя функции

 Плохо
```
setInterval(
"document.getElementById('container').textContent = 'Добро пожаловать!'", 3000
);
```
 Хорошо:
```
const writeContext = function() {
  const container = document.getElementById('container');
  container.textContent = 'Добро пожаловать!'
}
setInterval(writeContext, 3000);
```

#10. Производительность циклов for..
---
При выполнении длинных операторов `for` не заставляйте выполнять цикл дольше, чем он должен. Чтобы ускорить производительность и время работы цикла можно:
+ объявлять переменные вне оператора `for`
+ ограничить доступ к свойствам или переменным в цикле

Таким образом, на некоторые действия или свойства будут ссылаться один раз за цикл, а не обращаются к нему на каждой итерации.


 Плохо:
```
for (let i = 0; i < someArray.length; i++) {
   const container = document.getElementById('container');
   container.textContent = 'my number: ' + i;
   console.log(i);
}
```
 Хорошо:
```
const container = document.getElementById('container');
length = someArray.length;
for (let i = 0; i < length; i++) {
   container.textContent = 'my number: ' + i;
   console.log(i);
}
```
