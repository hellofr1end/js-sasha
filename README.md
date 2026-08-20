```markdown
# Гайд по основам JavaScript

## Переменные

### Объявление

```javascript
let age = 25;       // можно переприсваивать
const name = "Ivan"; // нельзя переприсваивать
var old = 30;       // устаревший способ, не рекомендуется
```

### Правила

- `let` и `const` имеют блочную область видимости
- `const` не защищает от изменения содержимого объектов и массивов
- Имена переменных чувствительны к регистру

```javascript
const arr = [1, 2, 3];
arr.push(4); // допустимо
// arr = [1, 2]; // TypeError
```

---

## Типы данных

```javascript
let num = 42;           // number
let str = "text";       // string
let bool = true;        // boolean
let nothing = null;     // null
let notDefined;         // undefined
let obj = { key: 1 };   // object
let arr = [1, 2, 3];    // array (частный случай object)
```

Проверка типа:

```javascript
typeof 42;        // "number"
typeof "text";    // "string"
typeof true;      // "boolean"
typeof undefined; // "undefined"
typeof null;      // "object" (историческая ошибка)
typeof {};        // "object"
typeof [];        // "object"
```

---

## Условные операторы

### if / else

```javascript
const x = 10;

if (x > 5) {
    console.log("больше 5");
} else if (x === 5) {
    console.log("равно 5");
} else {
    console.log("меньше 5");
}
```

### Операторы сравнения

| Оператор | Значение |
|----------|----------|
| `===`    | строгое равенство (без приведения типов) |
| `!==`    | строгое неравенство |
| `==`     | нестрогое равенство (с приведением типов) |
| `!=`     | нестрогое неравенство |
| `>`, `<`, `>=`, `<=` | больше, меньше, больше или равно, меньше или равно |

Всегда использовать `===` и `!==`.

### Тернарный оператор

```javascript
const age = 20;
const status = age >= 18 ? "adult" : "minor";
```

### switch

```javascript
const day = "monday";

switch (day) {
    case "monday":
        console.log("Понедельник");
        break;
    case "tuesday":
        console.log("Вторник");
        break;
    default:
        console.log("Другой день");
}
```

---

## Массивы

### Создание

```javascript
const arr1 = [1, 2, 3, 4, 5];
const arr2 = new Array(1, 2, 3);
const arr3 = Array(5).fill(0); // [0, 0, 0, 0, 0]
```

### Доступ к элементам

```javascript
const arr = [10, 20, 30];
arr[0]; // 10
arr[arr.length - 1]; // последний элемент
```

### Основные методы

| Метод | Описание | Пример |
|-------|----------|--------|
| `push(item)` | добавить в конец | `[1,2].push(3)` → `[1,2,3]` |
| `pop()` | удалить последний | `[1,2,3].pop()` → `3` |
| `unshift(item)` | добавить в начало | `[2,3].unshift(1)` → `[1,2,3]` |
| `shift()` | удалить первый | `[1,2,3].shift()` → `1` |
| `indexOf(item)` | индекс первого вхождения | `[1,2,3].indexOf(2)` → `1` |
| `includes(item)` | проверка наличия | `[1,2,3].includes(2)` → `true` |
| `slice(start, end)` | срез (не изменяет массив) | `[1,2,3,4].slice(1,3)` → `[2,3]` |
| `splice(start, count)` | удалить/вставить (изменяет массив) | — |
| `concat(arr)` | объединение массивов | `[1].concat([2])` → `[1,2]` |
| `join(sep)` | массив → строка | `[1,2,3].join("-")` → `"1-2-3"` |
| `reverse()` | развернуть (изменяет массив) | `[1,2].reverse()` → `[2,1]` |
| `sort()` | сортировка (изменяет массив) | см. ниже |

### Перебор массива

```javascript
const arr = [1, 2, 3, 4, 5];

// for
for (let i = 0; i < arr.length; i++) {
    console.log(arr[i]);
}

// for...of
for (const item of arr) {
    console.log(item);
}

// forEach
arr.forEach((item, index) => {
    console.log(index, item);
});
```

### Методы перебора (функциональный стиль)

```javascript
const nums = [1, 2, 3, 4, 5];

// map — преобразовать каждый элемент
const doubled = nums.map(n => n * 2); // [2, 4, 6, 8, 10]

// filter — отфильтровать
const even = nums.filter(n => n % 2 === 0); // [2, 4]

// reduce — свернуть в одно значение
const sum = nums.reduce((acc, n) => acc + n, 0); // 15

// find — найти первый подходящий элемент
const first = nums.find(n => n > 3); // 4

// some / every — проверки
nums.some(n => n > 4);  // true (хотя бы один)
nums.every(n => n > 0); // true (все)
```

### Сортировка

```javascript
const nums = [3, 1, 4, 1, 5];

// По возрастанию
nums.sort((a, b) => a - b); // [1, 1, 3, 4, 5]

// По убыванию
nums.sort((a, b) => b - a); // [5, 4, 3, 1, 1]

// Строки (по умолчанию лексикографически)
["banana", "apple", "cherry"].sort(); // ["apple", "banana", "cherry"]
```

---

## Циклы

### for

```javascript
for (let i = 0; i < 5; i++) {
    console.log(i);
}
```

### while

```javascript
let i = 0;
while (i < 5) {
    console.log(i);
    i++;
}
```

### do...while

```javascript
let i = 0;
do {
    console.log(i);
    i++;
} while (i < 5);
```

### for...in (для объектов)

```javascript
const obj = { a: 1, b: 2, c: 3 };
for (const key in obj) {
    console.log(key, obj[key]);
}
```

### break и continue

```javascript
for (let i = 0; i < 10; i++) {
    if (i === 3) continue; // пропустить итерацию
    if (i === 7) break;    // выйти из цикла
    console.log(i);
}
```

---

## Объекты

### Создание и доступ

```javascript
const user = {
    name: "Ivan",
    age: 25,
    isAdmin: false
};

user.name;       // "Ivan"
user["age"];     // 25
user.city = "Moscow"; // добавить свойство
delete user.isAdmin;  // удалить свойство
```

### Перебор

```javascript
const obj = { a: 1, b: 2, c: 3 };

Object.keys(obj);    // ["a", "b", "c"]
Object.values(obj);  // [1, 2, 3]
Object.entries(obj); // [["a",1], ["b",2], ["c",3]]

for (const [key, value] of Object.entries(obj)) {
    console.log(key, value);
}
```

### Деструктуризация

```javascript
const user = { name: "Ivan", age: 25 };
const { name, age } = user;

const arr = [1, 2, 3];
const [first, second] = arr;
```

### Spread / Rest

```javascript
// Spread для массивов
const a = [1, 2];
const b = [3, 4];
const merged = [...a, ...b]; // [1, 2, 3, 4]

// Spread для объектов
const obj1 = { a: 1 };
const obj2 = { b: 2 };
const full = { ...obj1, ...obj2 }; // { a: 1, b: 2 }

// Rest в параметрах функции
function sum(...nums) {
    return nums.reduce((acc, n) => acc + n, 0);
}
```

---

## Map и Set

### Map

```javascript
const map = new Map();
map.set("key1", "value1");
map.set("key2", "value2");

map.get("key1");    // "value1"
map.has("key2");    // true
map.size;           // 2
map.delete("key1"); // true

for (const [key, value] of map) {
    console.log(key, value);
}
```

### Set

```javascript
const set = new Set([1, 2, 3, 2, 1]); // Set {1, 2, 3}
set.add(4);
set.has(3);    // true
set.size;      // 4

// Удаление дубликатов из массива
const arr = [1, 2, 2, 3, 3, 3];
const unique = [...new Set(arr)]; // [1, 2, 3]
```

---

## Функции

### Объявление

```javascript
// Function declaration
function add(a, b) {
    return a + b;
}

// Function expression
const subtract = function(a, b) {
    return a - b;
};

// Arrow function
const multiply = (a, b) => a * b;
```

### Параметры по умолчанию

```javascript
function greet(name = "Guest") {
    return `Hello, ${name}`;
}
```

---

## Задачи

### Задача 1. Найти наибольшее число в массиве

```javascript
const nums = [3, 7, 2, 9, 4];

// Вариант 1: через цикл
function findMax(arr) {
    let max = arr[0];
    for (let i = 1; i < arr.length; i++) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }
    return max;
}

// Вариант 2: Math.max + spread
const max = Math.max(...nums);

console.log(findMax(nums)); // 9
```

---

### Задача 2. Вывести только четные числа из массива

```javascript
const nums = [1, 2, 3, 4, 5, 6, 7, 8];

// Вариант 1: цикл
for (const n of nums) {
    if (n % 2 === 0) {
        console.log(n);
    }
}

// Вариант 2: filter
const even = nums.filter(n => n % 2 === 0);
console.log(even); // [2, 4, 6, 8]
```

---

### Задача 3. Найти сумму всех чисел в массиве

```javascript
const nums = [1, 2, 3, 4, 5];

// Вариант 1: цикл
let sum = 0;
for (const n of nums) {
    sum += n;
}

// Вариант 2: reduce
const sum2 = nums.reduce((acc, n) => acc + n, 0);

console.log(sum);  // 15
console.log(sum2); // 15
```

---

### Задача 4. Развернуть строку

```javascript
const str = "hello";

// Вариант 1: split + reverse + join
const reversed = str.split("").reverse().join("");

// Вариант 2: цикл
let result = "";
for (let i = str.length - 1; i >= 0; i--) {
    result += str[i];
}

console.log(reversed); // "olleh"
```

---

### Задача 5. Проверить, является ли строка палиндромом

```javascript
function isPalindrome(str) {
    const cleaned = str.toLowerCase().replace(/[^a-z0-9]/g, "");
    const reversed = cleaned.split("").reverse().join("");
    return cleaned === reversed;
}

console.log(isPalindrome("racecar"));  // true
console.log(isPalindrome("A man a plan a canal Panama")); // true
console.log(isPalindrome("hello"));    // false
```

---

### Задача 6. Подсчитать количество вхождений каждого элемента

```javascript
const arr = ["apple", "banana", "apple", "cherry", "banana", "apple"];

function countOccurrences(arr) {
    const counts = {};
    for (const item of arr) {
        counts[item] = (counts[item] || 0) + 1;
    }
    return counts;
}

console.log(countOccurrences(arr));
// { apple: 3, banana: 2, cherry: 1 }
```

---

### Задача 7. Удалить дубликаты из массива

```javascript
const arr = [1, 2, 2, 3, 4, 4, 5];

// Вариант 1: Set
const unique = [...new Set(arr)];

// Вариант 2: filter
const unique2 = arr.filter((item, index) => arr.indexOf(item) === index);

console.log(unique);  // [1, 2, 3, 4, 5]
console.log(unique2); // [1, 2, 3, 4, 5]
```

---

### Задача 8. Найти общие элементы двух массивов

```javascript
const arr1 = [1, 2, 3, 4, 5];
const arr2 = [3, 4, 5, 6, 7];

// Вариант 1: filter + includes
const common = arr1.filter(item => arr2.includes(item));

// Вариант 2: Set
const set2 = new Set(arr2);
const common2 = arr1.filter(item => set2.has(item));

console.log(common);  // [3, 4, 5]
console.log(common2); // [3, 4, 5]
```

---

### Задача 9. Преобразовать массив объектов по заданному критерию

```javascript
const users = [
    { name: "Ivan", age: 25 },
    { name: "Maria", age: 17 },
    { name: "Petr", age: 30 }
];

// Получить имена совершеннолетних
const adults = users
    .filter(user => user.age >= 18)
    .map(user => user.name);

console.log(adults); // ["Ivan", "Petr"]
```

---

### Задача 10. Сгруппировать элементы массива по условию

```javascript
const nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// Разбить на четные и нечетные
function partition(arr) {
    const even = [];
    const odd = [];
    for (const n of arr) {
        if (n % 2 === 0) {
            even.push(n);
        } else {
            odd.push(n);
        }
    }
    return { even, odd };
}

// Вариант через reduce
function partition2(arr) {
    return arr.reduce((acc, n) => {
        (n % 2 === 0 ? acc.even : acc.odd).push(n);
        return acc;
    }, { even: [], odd: [] });
}

console.log(partition(nums));
// { even: [2, 4, 6, 8, 10], odd: [1, 3, 5, 7, 9] }
```

---

## Шпаргалка: полезные приемы

### Обмен значений

```javascript
let a = 1, b = 2;
[a, b] = [b, a]; // a = 2, b = 1
```

### Проверка на NaN

```javascript
Number.isNaN(NaN); // true
isNaN("text");     // true (приводит к числу)
```

### Преобразование типов

```javascript
String(42);       // "42"
Number("42");     // 42
parseInt("42px"); // 42
Boolean(0);       // false
Boolean("");      // false
Boolean("text");  // true
Boolean([]);      // true
Boolean({});      // true
```

### Копирование массива

```javascript
const original = [1, 2, 3];
const copy1 = [...original];
const copy2 = original.slice();
```

### Копирование объекта (поверхностное)

```javascript
const original = { a: 1, b: { c: 2 } };
const copy = { ...original };
```

---

## Falsy значения

В JavaScript следующие значения приводятся к `false`:

- `false`
- `0`
- `""` (пустая строка)
- `null`
- `undefined`
- `NaN`

Все остальные значения — truthy.

```javascript
if (0) {
    // не выполнится
}

if ("") {
    // не выполнится
}

if ([]) {
    // выполнится (пустой массив — truthy)
}
```
```
