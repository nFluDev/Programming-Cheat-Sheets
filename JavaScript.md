# Nihai JavaScript Cheatsheet'i

## İçindekiler Tablosu

1. [Temel Kavramlar](#temel-kavramlar)
   - [Değişkenler](#değişkenler)
   - [Veri Türleri](#veri-türleri)
   - [Operatörler](#operatörler)
   - [Tür Zorlaması ve Dönüşümü](#tür-zorlaması-ve-dönüşümü)
   - [Kapsam ve Hoisting](#kapsam-ve-hoisting)
2. [Kontrol Akışı](#kontrol-akışı)
   - [Koşullu İfadeler](#koşullu-ifadeler)
   - [Döngüler](#döngüler)
3. [Fonksiyonlar](#fonksiyonlar)
   - [Fonksiyon Bildirimleri](#fonksiyon-bildirimleri)
   - [Arrow Fonksiyonları](#arrow-fonksiyonları)
   - [IIFE](#iife)
4. [Nesneler ve Diziler](#nesneler-ve-diziler)
   - [Nesne Manipülasyonu](#nesne-manipülasyonu)
   - [Dizi Metodları](#dizi-metodları)
   - [Destructuring](#destructuring)
   - [Spread ve Rest Operatörleri](#spread-ve-rest-operatörleri)
5. [Asenkron JavaScript](#asenkron-javascript)
   - [Promises](#promises)
   - [Async/Await](#asyncawait)
6. [Nesne Yönelimli Programlama](#nesne-yönelimli-programlama)
   - [Class Sözdizimi](#class-sözdizimi)
   - [Inheritance](#inheritance)
7. [ES6+ Özellikleri](#es6-özellikleri)
   - [Template Literals](#template-literals)
   - [Modüller](#modüller)
8. [DOM Manipülasyonu](#dom-manipülasyonu)
   - [Element Seçme](#element-seçme)
   - [Element Manipülasyonu](#element-manipülasyonu)
   - [Olay Yönetimi](#olay-yönetimi)
9. [Sık Kullanılan Dahili Nesneler](#sık-kullanılan-dahili-nesneler)
   - [String Metodları](#string-metodları)
   - [Number Metodları](#number-metodları)
   - [Math Nesnesi](#math-nesnesi)
   - [Date Nesnesi](#date-nesnesi)

---

## Temel Kavramlar

### Değişkenler

**var, let, const** arasındaki farklar ve kapsam özellikleri:

```javascript
// var - Fonksiyon kapsamlı, hoisting var
var name = "JavaScript";

// let - Blok kapsamlı, hoisting yok
let age = 25;

// const - Blok kapsamlı, değişmez, hoisting yok
const PI = 3.14159;
```

**Kapsam Örnekleri:**

```javascript
function scopeExample() {
  var varVariable = "Function scoped";
  let letVariable = "Block scoped";
  const constVariable = "Block scoped";
  
  if (true) {
    var varVariable2 = "Still function scoped";
    let letVariable2 = "Block scoped only";
    const constVariable2 = "Block scoped only";
  }
  
  console.log(varVariable2); // Erişilebilir
  // console.log(letVariable2); // ReferenceError
}
```

### Veri Türleri

**Primitif Türler:**

```javascript
// String
let text = "Hello World";

// Number
let number = 42;
let decimal = 3.14;

// Boolean
let isTrue = true;
let isFalse = false;

// Undefined
let undefinedVariable;

// Null
let nullValue = null;

// Symbol (ES6)
let symbol = Symbol('unique');

// BigInt (ES2020)
let bigNumber = 123n;
```

**Non-Primitif Türler:**

```javascript
// Object
let person = {
  name: "John",
  age: 30
};

// Array
let numbers = [1, 2, 3, 4, 5];

// Function
function greet() {
  return "Hello!";
}
```

### Operatörler

**Aritmetik Operatörler:**

```javascript
let a = 10, b = 3;

console.log(a + b); // 13 (Toplama)
console.log(a - b); // 7 (Çıkarma)
console.log(a * b); // 30 (Çarpma)
console.log(a / b); // 3.33 (Bölme)
console.log(a % b); // 1 (Modül)
console.log(a ** b); // 1000 (Üs alma)
console.log(++a); // 11 (Pre-increment)
console.log(b--); // 3, sonra 2 (Post-decrement)
```

**Karşılaştırma Operatörleri:**

```javascript
let x = 5, y = "5";

console.log(x == y);  // true (Tür dönüşümü ile)
console.log(x === y); // false (Sıkı eşitlik)
console.log(x != y);  // false
console.log(x !== y); // true
console.log(x > 3);   // true
console.log(x <= 5);  // true
```

**Mantıksal Operatörler:**

```javascript
let t = true, f = false;

console.log(t && f); // false (VE)
console.log(t || f); // true (VEYA)
console.log(!t);     // false (DEĞİL)
```

**Ternary Operatör:**

```javascript
let age = 20;
let message = age >= 18 ? "Yetişkin" : "Çocuk";
console.log(message); // "Yetişkin"
```

### Tür Zorlaması ve Dönüşümü

**Otomatik Tür Zorlaması:**

```javascript
console.log("5" + 3);    // "53" (string concatenation)
console.log("5" - 3);    // 2 (numeric subtraction)
console.log("5" * "2");  // 10 (numeric multiplication)
console.log(true + 1);   // 2 (boolean to number)
```

**Manuel Tür Dönüşümü:**

```javascript
// String'e dönüştürme
String(123);        // "123"
(123).toString();   // "123"

// Number'a dönüştürme
Number("123");      // 123
parseInt("123px");  // 123
parseFloat("12.34"); // 12.34

// Boolean'a dönüştürme
Boolean(0);         // false
Boolean(1);         // true
!!("hello");        // true
```

### Kapsam ve Hoisting

**Hoisting Örneği:**

```javascript
console.log(hoistedVar); // undefined (not error)
var hoistedVar = "I'm hoisted";

// console.log(notHoisted); // ReferenceError
let notHoisted = "I'm not hoisted";

// Fonksiyon hoisting
sayHello(); // Çalışır

function sayHello() {
  console.log("Hello!");
}

// Arrow fonksiyonlar hoist edilmez
// sayGoodbye(); // TypeError
var sayGoodbye = () => console.log("Goodbye!");
```

---

## Kontrol Akışı

### Koşullu İfadeler

**if/else Yapısı:**

```javascript
let score = 85;

if (score >= 90) {
  console.log("A Grade");
} else if (score >= 80) {
  console.log("B Grade");
} else if (score >= 70) {
  console.log("C Grade");
} else {
  console.log("F Grade");
}
```

**switch Yapısı:**

```javascript
let day = "Monday";

switch (day) {
  case "Monday":
    console.log("Pazartesi");
    break;
  case "Tuesday":
    console.log("Salı");
    break;
  case "Wednesday":
    console.log("Çarşamba");
    break;
  default:
    console.log("Bilinmeyen gün");
}
```

### Döngüler

**for Döngüsü:**

```javascript
// Klasik for döngüsü
for (let i = 0; i < 5; i++) {
  console.log(i); // 0, 1, 2, 3, 4
}

// for...in (nesne özellikleri için)
let person = {name: "John", age: 30, city: "New York"};
for (let key in person) {
  console.log(key + ": " + person[key]);
}

// for...of (iterable öğeler için)
let colors = ["red", "green", "blue"];
for (let color of colors) {
  console.log(color);
}
```

**while Döngüsü:**

```javascript
let i = 0;
while (i < 3) {
  console.log(i);
  i++;
}

// do...while
let j = 0;
do {
  console.log(j);
  j++;
} while (j < 3);
```

---

## Fonksiyonlar

### Fonksiyon Bildirimleri

**Function Declaration:**

```javascript
function add(a, b) {
  return a + b;
}

console.log(add(5, 3)); // 8
```

**Function Expression:**

```javascript
const multiply = function(a, b) {
  return a * b;
};

console.log(multiply(4, 6)); // 24
```

**Varsayılan Parametreler:**

```javascript
function greet(name = "Dünya") {
  return `Merhaba ${name}!`;
}

console.log(greet());       // "Merhaba Dünya!"
console.log(greet("Ali"));  // "Merhaba Ali!"
```

**Rest Parametreleri:**

```javascript
function sum(...numbers) {
  return numbers.reduce((total, num) => total + num, 0);
}

console.log(sum(1, 2, 3, 4)); // 10
```

### Arrow Fonksiyonları

**Temel Arrow Fonksiyon Sözdizimi:**

```javascript
// Tek satır, otomatik return
const square = x => x * x;

// Çoklu parametreler
const add = (a, b) => a + b;

// Blok body
const complexFunction = (x, y) => {
  let result = x * y;
  return result + 10;
};

// this binding farkı
const obj = {
  name: "JavaScript",
  regular: function() {
    console.log(this.name); // "JavaScript"
  },
  arrow: () => {
    console.log(this.name); // undefined (global scope)
  }
};
```

### IIFE

**Immediately Invoked Function Expression:**

```javascript
// IIFE Klasik Syntax
(function() {
  console.log("IIFE çalışıyor!");
})();

// IIFE Arrow Function
(() => {
  console.log("Arrow IIFE çalışıyor!");
})();

// Parametreli IIFE
(function(name) {
  console.log(`Merhaba ${name}!`);
})("JavaScript");
```

---

## Nesneler ve Diziler

### Nesne Manipülasyonu

**Nesne Oluşturma ve Erişim:**

```javascript
// Nesne literal
let person = {
  name: "John",
  age: 30,
  "full-name": "John Doe" // Boşluklu özellik adı
};

// Nokta notasyonu
console.log(person.name); // "John"

// Köşeli parantez notasyonu
console.log(person["age"]); // 30
console.log(person["full-name"]); // "John Doe"

// Dinamik özellik erişimi
let property = "name";
console.log(person[property]); // "John"

// Özellik ekleme
person.city = "Istanbul";
person["country"] = "Turkey";
```

**Nesne Metodları:**

```javascript
let person = {
  name: "John",
  age: 30,
  greet: function() {
    return `Merhaba, ben ${this.name}`;
  },
  // ES6 method syntax
  introduce() {
    return `${this.name}, ${this.age} yaşında`;
  }
};

console.log(person.greet()); // "Merhaba, ben John"
```

### Dizi Metodları

**Temel Dizi Metodları:**

```javascript
let fruits = ["apple", "banana", "orange"];

// Ekleme/Çıkarma
fruits.push("grape");      // Sona ekle
fruits.unshift("mango");   // Başa ekle
let last = fruits.pop();   // Sondan çıkar
let first = fruits.shift(); // Baştan çıkar

// Splice ve Slice
let numbers = [1, 2, 3, 4, 5];
numbers.splice(2, 1, 10); // Index 2'den 1 eleman sil, 10 ekle
console.log(numbers); // [1, 2, 10, 4, 5]

let sliced = numbers.slice(1, 4); // Index 1-4 arası kopyala
console.log(sliced); // [2, 10, 4]
```

**Yüksek Seviye Dizi Metodları:**

```javascript
let numbers = [1, 2, 3, 4, 5];

// map - her elemana işlem uygula
let doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8, 10]

// filter - koşula uyan elemanları filtrele
let evens = numbers.filter(num => num % 2 === 0);
console.log(evens); // [2, 4]

// reduce - tek değere indirge
let sum = numbers.reduce((acc, curr) => acc + curr, 0);
console.log(sum); // 15

// find - koşula uyan ilk elemanı bul
let found = numbers.find(num => num > 3);
console.log(found); // 4

// forEach - her eleman için işlem yap
numbers.forEach((num, index) => {
  console.log(`Index ${index}: ${num}`);
});

// every - tüm elemanlar koşulu sağlıyor mu?
let allPositive = numbers.every(num => num > 0);
console.log(allPositive); // true

// some - en az bir eleman koşulu sağlıyor mu?
let hasEven = numbers.some(num => num % 2 === 0);
console.log(hasEven); // true
```

### Destructuring

**Dizi Destructuring:**

```javascript
let colors = ["red", "green", "blue", "yellow"];

// Temel destructuring
let [first, second] = colors;
console.log(first);  // "red"
console.log(second); // "green"

// Elemanları atlama
let [, , third] = colors;
console.log(third); // "blue"

// Rest ile kalan elemanlar
let [primary, ...others] = colors;
console.log(primary); // "red"
console.log(others);  // ["green", "blue", "yellow"]

// Varsayılan değerler
let [a, b, c, d, e = "purple"] = colors;
console.log(e); // "purple"
```

**Nesne Destructuring:**

```javascript
let person = {
  name: "John",
  age: 30,
  city: "Istanbul",
  country: "Turkey"
};

// Temel destructuring
let {name, age} = person;
console.log(name); // "John"
console.log(age);  // 30

// Yeniden adlandırma
let {name: fullName, age: years} = person;
console.log(fullName); // "John"
console.log(years);    // 30

// Varsayılan değerler
let {name, age, profession = "Developer"} = person;
console.log(profession); // "Developer"

// Rest ile kalan özellikler
let {name, ...details} = person;
console.log(details); // {age: 30, city: "Istanbul", country: "Turkey"}
```

### Spread ve Rest Operatörleri

**Spread Operatörü (...):**

```javascript
// Dizi spread
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];
let combined = [...arr1, ...arr2];
console.log(combined); // [1, 2, 3, 4, 5, 6]

// Nesne spread
let obj1 = {a: 1, b: 2};
let obj2 = {c: 3, d: 4};
let merged = {...obj1, ...obj2};
console.log(merged); // {a: 1, b: 2, c: 3, d: 4}

// Fonksiyon argümanları
function sum(a, b, c) {
  return a + b + c;
}
let numbers = [1, 2, 3];
console.log(sum(...numbers)); // 6
```

**Rest Operatörü (...):**

```javascript
// Fonksiyon parametrelerinde
function multiply(multiplier, ...numbers) {
  return numbers.map(num => num * multiplier);
}
console.log(multiply(2, 1, 2, 3, 4)); // [2, 4, 6, 8]

// Destructuring'de
let [first, ...rest] = [1, 2, 3, 4, 5];
console.log(first); // 1
console.log(rest);  // [2, 3, 4, 5]
```

---

## Asenkron JavaScript

### Promises

**Promise Oluşturma:**

```javascript
// Temel Promise
let promise = new Promise((resolve, reject) => {
  let success = true;
  
  if (success) {
    resolve("İşlem başarılı!");
  } else {
    reject("İşlem başarısız!");
  }
});

// Promise kullanımı
promise
  .then(result => {
    console.log(result); // "İşlem başarılı!"
  })
  .catch(error => {
    console.log(error);
  })
  .finally(() => {
    console.log("İşlem tamamlandı");
  });
```

**Promise Metodları:**

```javascript
// Promise.all - Tüm promise'ler tamamlanana kadar bekle
let promise1 = Promise.resolve(3);
let promise2 = new Promise(resolve => setTimeout(() => resolve('foo'), 1000));
let promise3 = Promise.resolve(42);

Promise.all([promise1, promise2, promise3])
  .then(values => {
    console.log(values); // [3, "foo", 42]
  });

// Promise.race - İlk tamamlanan promise'i döndür
Promise.race([promise1, promise2, promise3])
  .then(value => {
    console.log(value); // 3 (en hızlı tamamlanan)
  });

// Promise.allSettled - Tüm sonuçları döndür (başarılı/başarısız)
Promise.allSettled([promise1, promise2, Promise.reject("error")])
  .then(results => {
    console.log(results);
    // [
    //   {status: "fulfilled", value: 3},
    //   {status: "fulfilled", value: "foo"},
    //   {status: "rejected", reason: "error"}
    // ]
  });
```

### Async/Await

**Async Function Sözdizimi:**

```javascript
// Temel async function
async function fetchData() {
  return "Veri alındı!";
}

fetchData().then(data => console.log(data)); // "Veri alındı!"
```

**Await Kullanımı:**

```javascript
// Promise'leri await ile bekle
async function processData() {
  try {
    let data1 = await fetch('/api/data1');
    let data2 = await fetch('/api/data2');
    
    let result1 = await data1.json();
    let result2 = await data2.json();
    
    return {result1, result2};
  } catch (error) {
    console.error('Hata:', error);
  }
}

// Paralel işlemler için
async function parallelRequests() {
  try {
    let [data1, data2] = await Promise.all([
      fetch('/api/data1'),
      fetch('/api/data2')
    ]);
    
    let results = await Promise.all([
      data1.json(),
      data2.json()
    ]);
    
    return results;
  } catch (error) {
    console.error('Hata:', error);
  }
}
```

**Hata Yönetimi:**

```javascript
async function handleErrors() {
  try {
    let response = await fetch('/api/data');
    
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    
    let data = await response.json();
    return data;
  } catch (error) {
    if (error instanceof TypeError) {
      console.error('Network error:', error);
    } else {
      console.error('Other error:', error);
    }
    throw error; // Hatayı üst seviyeye ilet
  } finally {
    console.log('Cleanup işlemleri');
  }
}
```

---

## Nesne Yönelimli Programlama

### Class Sözdizimi

**Temel Class:**

```javascript
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  
  // Method
  greet() {
    return `Merhaba, ben ${this.name}`;
  }
  
  // Getter
  get info() {
    return `${this.name} - ${this.age} yaş`;
  }
  
  // Setter
  set age(newAge) {
    if (newAge > 0) {
      this._age = newAge;
    }
  }
  
  get age() {
    return this._age;
  }
  
  // Static method
  static species() {
    return 'Homo sapiens';
  }
}

let john = new Person('John', 30);
console.log(john.greet()); // "Merhaba, ben John"
console.log(john.info);    // "John - 30 yaş"
console.log(Person.species()); // "Homo sapiens"
```

### Inheritance

**Class Inheritance:**

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }
  
  speak() {
    return `${this.name} bir ses çıkarıyor`;
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name); // Parent constructor'ı çağır
    this.breed = breed;
  }
  
  speak() {
    return `${this.name} havlıyor: Woof!`;
  }
  
  // Ek method
  wagTail() {
    return `${this.name} kuyruğunu sallıyor`;
  }
}

let myDog = new Dog('Buddy', 'Golden Retriever');
console.log(myDog.speak());   // "Buddy havlıyor: Woof!"
console.log(myDog.wagTail()); // "Buddy kuyruğunu sallıyor"
```

**Private Fields (ES2022):**

```javascript
class BankAccount {
  #balance = 0; // Private field
  
  constructor(initialBalance) {
    this.#balance = initialBalance;
  }
  
  deposit(amount) {
    this.#balance += amount;
    return this.#balance;
  }
  
  withdraw(amount) {
    if (amount <= this.#balance) {
      this.#balance -= amount;
      return this.#balance;
    }
    throw new Error('Yetersiz bakiye');
  }
  
  get balance() {
    return this.#balance;
  }
}

let account = new BankAccount(1000);
console.log(account.deposit(500)); // 1500
// console.log(account.#balance); // SyntaxError: Private field
```

---

## ES6+ Özellikleri

### Template Literals

**Temel Template Literals:**

```javascript
let name = 'JavaScript';
let version = 'ES6';

// String interpolation
let message = `Merhaba ${name}! ${version} kullanıyoruz.`;
console.log(message); // "Merhaba JavaScript! ES6 kullanıyoruz."

// Çok satırlı string
let multiline = `
  Bu bir
  çok satırlı
  string örneğidir.
`;

// Expression'lar
let a = 5, b = 10;
let result = `${a} + ${b} = ${a + b}`;
console.log(result); // "5 + 10 = 15"

// Function call'lar
function greet(name) {
  return `Merhaba ${name}!`;
}
let greeting = `${greet('Ali')} Nasılsın?`;
console.log(greeting); // "Merhaba Ali! Nasılsın?"
```

**Tagged Template Literals:**

```javascript
function highlight(strings, ...values) {
  return strings.reduce((result, string, i) => {
    let value = values[i] ? `<mark>${values[i]}</mark>` : '';
    return result + string + value;
  }, '');
}

let name = 'JavaScript';
let type = 'programming language';
let highlighted = highlight`${name} is a ${type}`;
console.log(highlighted); // "<mark>JavaScript</mark> is a <mark>programming language</mark>"
```

### Modüller

**Export Örnekleri:**

```javascript
// math.js - Named exports
export function add(a, b) {
  return a + b;
}

export function multiply(a, b) {
  return a * b;
}

export const PI = 3.14159;

// Default export
export default function subtract(a, b) {
  return a - b;
}

// Alternative export syntax
function divide(a, b) {
  return a / b;
}

function power(a, b) {
  return a ** b;
}

export { divide, power };
```

**Import Örnekleri:**

```javascript
// app.js - Import kullanımı

// Default import
import subtract from './math.js';

// Named imports
import { add, multiply, PI } from './math.js';

// Import with alias
import { divide as div, power as pow } from './math.js';

// Import everything
import * as MathUtils from './math.js';

// Mixed import
import subtract, { add, multiply } from './math.js';

console.log(add(5, 3));        // 8
console.log(subtract(10, 4));  // 6
console.log(PI);               // 3.14159
console.log(div(15, 3));       // 5
console.log(MathUtils.power(2, 3)); // 8
```

---

## DOM Manipülasyonu

### Element Seçme

**Element Seçim Metodları:**

```javascript
// ID ile seç
let element = document.getElementById('myId');

// Class ile seç
let elements = document.getElementsByClassName('myClass');
let firstElement = elements[0];

// Tag ile seç
let paragraphs = document.getElementsByTagName('p');

// CSS selector ile seç (ilk eşleşen)
let firstDiv = document.querySelector('.myClass');
let firstInput = document.querySelector('input[type="text"]');

// CSS selector ile seç (tüm eşleşenler)
let allDivs = document.querySelectorAll('.myClass');
let allInputs = document.querySelectorAll('input');

// NodeList'i Array'e çevir
let divsArray = Array.from(allDivs);
```

### Element Manipülasyonu

**İçerik Değiştirme:**

```javascript
let element = document.getElementById('myElement');

// Text içeriği
element.textContent = 'Yeni metin';
element.innerText = 'Görünen metin';

// HTML içeriği
element.innerHTML = '<strong>Kalın metin</strong>';

// Attribute'ler
element.setAttribute('class', 'newClass');
element.setAttribute('data-id', '123');
let className = element.getAttribute('class');

// Class manipülasyonu
element.classList.add('newClass');
element.classList.remove('oldClass');
element.classList.toggle('active');
let hasClass = element.classList.contains('myClass');

// Style değiştirme
element.style.color = 'red';
element.style.backgroundColor = 'yellow';
element.style.fontSize = '20px';
```

**Element Oluşturma ve Ekleme:**

```javascript
// Yeni element oluştur
let newDiv = document.createElement('div');
newDiv.textContent = 'Yeni div';
newDiv.className = 'created-element';

// Element ekle
let container = document.getElementById('container');
container.appendChild(newDiv);

// Belirli pozisyona ekle
container.insertBefore(newDiv, container.firstChild);

// innerHTML ile ekle
container.innerHTML += '<p>Yeni paragraf</p>';

// Element sil
let elementToRemove = document.getElementById('removeMe');
elementToRemove.remove(); // Modern yöntem
// elementToRemove.parentNode.removeChild(elementToRemove); // Eski yöntem
```

### Olay Yönetimi

**Event Listener Ekleme:**

```javascript
let button = document.getElementById('myButton');

// Click event
button.addEventListener('click', function() {
  console.log('Butona tıklandı!');
});

// Arrow function ile
button.addEventListener('click', () => {
  console.log('Arrow function ile click!');
});

// Event object kullanma
button.addEventListener('click', function(event) {
  event.preventDefault(); // Default davranışı engelle
  console.log('Event target:', event.target);
  console.log('Mouse position:', event.clientX, event.clientY);
});

// Multiple events
function handleInput(event) {
  console.log('Input değeri:', event.target.value);
}

let input = document.getElementById('myInput');
input.addEventListener('input', handleInput);
input.addEventListener('focus', () => console.log('Input focused'));
input.addEventListener('blur', () => console.log('Input blurred'));
```

**Event Delegation:**

```javascript
// Container'a tek listener ekle, child elementler için de çalışır
let container = document.getElementById('container');

container.addEventListener('click', function(event) {
  if (event.target.classList.contains('button')) {
    console.log('Button clicked:', event.target.textContent);
  }
  
  if (event.target.tagName === 'LI') {
    console.log('List item clicked:', event.target.textContent);
  }
});
```

---

## Sık Kullanılan Dahili Nesneler

### String Metodları

**Temel String İşlemleri:**

```javascript
let text = "  JavaScript Programming  ";

// Uzunluk
console.log(text.length); // 25

// Boşlukları temizle
console.log(text.trim());     // "JavaScript Programming"
console.log(text.trimStart()); // "JavaScript Programming  "
console.log(text.trimEnd());   // "  JavaScript Programming"

// Büyük/küçük harf
console.log(text.toLowerCase());  // "  javascript programming  "
console.log(text.toUpperCase());  // "  JAVASCRIPT PROGRAMMING  "

// Arama
console.log(text.indexOf('Script'));     // 6
console.log(text.lastIndexOf('a'));      // 18
console.log(text.includes('Java'));      // true
console.log(text.startsWith('  Java'));  // true
console.log(text.endsWith('ing  '));     // true

// Kesme ve ayırma
console.log(text.slice(2, 12));          // "JavaScript"
console.log(text.substring(2, 12));      // "JavaScript"
console.log(text.substr(2, 10));         // "JavaScript" (deprecated)

let words = text.trim().split(' ');
console.log(words); // ["JavaScript", "Programming"]

// Değiştirme
console.log(text.replace('JavaScript', 'JS'));     // Ilk eşleşeni değiştir
console.log(text.replaceAll('a', '@'));           // Tüm eşleşenleri değiştir

// Tekrar etme
console.log('Ha'.repeat(3)); // "HaHaHa"

// Padding
console.log('5'.padStart(3, '0'));  // "005"
console.log('5'.padEnd(3, '0'));    // "500"
```

### Number Metodları

**Number İşlemleri:**

```javascript
let num = 3.14159;
let str = "123.45px";

// Parsing
console.log(parseInt(str));       // 123
console.log(parseFloat(str));     // 123.45
console.log(Number(str));         // NaN (çünkü px var)
console.log(Number("123.45"));    // 123.45

// Formatting
console.log(num.toFixed(2));      // "3.14"
console.log(num.toPrecision(4));  // "3.142"
console.log(num.toExponential(2)); // "3.14e+0"

// Checking
console.log(Number.isInteger(5));     // true
console.log(Number.isInteger(5.0));   // true
console.log(Number.isInteger(5.1));   // false
console.log(Number.isNaN(NaN));       // true
console.log(Number.isFinite(100));    // true
console.log(Number.isFinite(Infinity)); // false

// Constants
console.log(Number.MAX_VALUE);        // En büyük sayı
console.log(Number.MIN_VALUE);        // En küçük pozitif sayı
console.log(Number.MAX_SAFE_INTEGER); // 9007199254740991
console.log(Number.POSITIVE_INFINITY); // Infinity
```

### Math Nesnesi

**Math Metodları:**

```javascript
// Temel işlemler
console.log(Math.abs(-5));        // 5
console.log(Math.ceil(4.2));      // 5
console.log(Math.floor(4.8));     // 4
console.log(Math.round(4.6));     // 5
console.log(Math.trunc(4.9));     // 4

// Min/Max
console.log(Math.min(1, 2, 3));   // 1
console.log(Math.max(1, 2, 3));   // 3

// Power ve kök
console.log(Math.pow(2, 3));      // 8
console.log(Math.sqrt(16));       // 4
console.log(Math.cbrt(27));       // 3

// Rastgele sayı
console.log(Math.random());       // 0-1 arası
console.log(Math.floor(Math.random() * 10)); // 0-9 arası

// Trigonometrik
console.log(Math.sin(Math.PI / 2)); // 1
console.log(Math.cos(0));           // 1
console.log(Math.tan(Math.PI / 4)); // 1

// Logaritma
console.log(Math.log(Math.E));      // 1
console.log(Math.log10(100));       // 2

// Constants
console.log(Math.PI);    // 3.141592653589793
console.log(Math.E);     // 2.718281828459045
```

### Date Nesnesi

**Date İşlemleri:**

```javascript
// Date oluşturma
let now = new Date();
let specificDate = new Date('2024-01-15');
let dateWithTime = new Date(2024, 0, 15, 10, 30, 0); // Ay 0-11 arası

console.log(now);          // Current date and time
console.log(specificDate); // Mon Jan 15 2024...

// Get metodları
console.log(now.getFullYear());  // 2024
console.log(now.getMonth());     // 0-11 (Ocak = 0)
console.log(now.getDate());      // 1-31
console.log(now.getDay());       // 0-6 (Pazar = 0)
console.log(now.getHours());     // 0-23
console.log(now.getMinutes());   // 0-59
console.log(now.getSeconds());   // 0-59
console.log(now.getTime());      // Timestamp (milisaniye)

// Set metodları
let date = new Date();
date.setFullYear(2025);
date.setMonth(11); // Aralık
date.setDate(25);  // 25. gün
console.log(date); // Dec 25, 2025

// Formatting
console.log(date.toString());       // Tam format
console.log(date.toDateString());   // Sadece tarih
console.log(date.toTimeString());   // Sadece saat
console.log(date.toISOString());    // ISO format
console.log(date.toLocaleDateString('tr-TR')); // Türkçe format

// Date aritmetiği
let tomorrow = new Date();
tomorrow.setDate(tomorrow.getDate() + 1);

let oneWeekAgo = new Date();
oneWeekAgo.setDate(oneWeekAgo.getDate() - 7);

// İki tarih arasındaki fark (milisaniye)
let diff = tomorrow.getTime() - now.getTime();
let daysDifference = diff / (1000 * 60 * 60 * 24);
console.log(`Fark: ${daysDifference} gün`);
```

---

Bu cheatsheet, JavaScript'in temel ve ileri seviye özelliklerini kapsamlı bir şekilde içerir. Hızlı başvuru için tasarlanmış ve her konuda pratik örnekler sunmaktadır. Modern JavaScript geliştirme için gerekli tüm bilgileri içerir ve sürekli güncellenen dil özelliklerini takip eder.