# ![This is an image](https://www.vectorlogo.zone/logos/nodejs/nodejs-horizontal.svg) Node.js - Лабораторна робота 3

### _Тема: Express.js та EJS_

#### Відпові на контрольні питання:

<u>_1. Опишіть механізм наслідування в JavaScript._</u>

Механізм наслідування в JavaScript дозволяє створювати нові об'єкти на основі вже існуючих об'єктів, де новий об'єкт зберігає в собі властивості та методи батьківського об'єкта та може бути розширеним новими властивостями та методами. Це дозволяє створювати більш складні об'єкти, які можуть мати спільний функціонал, але водночас можуть бути різними в деяких аспектах.

Є кілька способів реалізації наслідування в JavaScript. Один з найпоширеніших способів - це використання прототипів. Кожен об'єкт в JavaScript має прототип, який можна використовувати для створення нових об'єктів зі спільними властивостями та методами.

Для створення нового об'єкта на основі існуючого об'єкта, спочатку потрібно створити новий об'єкт, який буде використовувати прототип батьківського об'єкта. Для цього можна використовувати функцію-конструктор, яка буде створювати новий об'єкт та наслідувати властивості та методи батьківського об'єкта. Наприклад:

```JavaScript
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.sayHello = function() {
  console.log(`Hello, my name is ${this.name}`);
}

function Student(name, age, grade) {
  Person.call(this, name, age);
  this.grade = grade;
}

Student.prototype = Object.create(Person.prototype);
Student.prototype.constructor = Student;

Student.prototype.sayGrade = function() {
  console.log(`My grade is ${this.grade}`);
}

const john = new Student('Max', 20, 'A');
john.sayHello(); // Output: Hello, my name is Max
john.sayGrade(); // Output: My grade is A
```

У цьому прикладі, функція-конструктор `Person` створює об'єкт з властивостями `name` та `age`, а також методом `sayHello`. Функція-конструктор `Student` створює новий об'єкт на основі батьківського об 'єкта `Person`, використовуючи метод `call` для належного встановлення значень `name` та `age`. Далі, за допомогою `Object.create`, створюється новий об'єкт, який має прототипом об'єкт `Person.prototype`. Це дозволяє новому об'єкту отримати доступ до методів та властивостей батьківського об'єкта.

Зверніть увагу на рядок `Student.prototype.constructor = Student`. Цей рядок встановлює правильний конструктор для нового об'єкта `Student`. Це необхідно, оскільки при створенні нового об'єкта на основі прототипа `Person`.prototype, конструктор за замовчуванням буде вказувати на `Person`, а не на `Student`.

Після того, як був створений новий об'єкт `Student`, можна додати до нього нові методи та властивості. У прикладі використовується метод `sayGrade`, який був доданий до прототипу `Student.prototype`.
В результаті, коли ми створюємо новий об'єкт `max` за допомогою функції-конструктора `Student`, він успадковує властивості та методи з об'єкта `Person`, а також має свій власний метод `sayGrade`. Це дозволяє нам з легкістю створювати нові об'єкти на основі існуючих, що робить код більш ефективним та зрозумілим.

Загалом, механізм наслідування в JavaScript дозволяє зменшити дублювання коду та створювати більш складні об'єкти зі спільним функціоналом. Це є важливим інструментом для розробки програмного забезпечення, яке має багато спільних елементів.

---

<u>_2. Яку функцію виконує Express.js?_</u>

**Express.js** - це фреймворк для розробки веб-додатків на мові JavaScript, який дозволяє легко створювати серверну частину застосунку та взаємодіяти з клієнтами за допомогою HTTP запитів. Основна функція Express - це маршрутизація запитів HTTP, тобто визначення, які дії повинні виконуватись при отриманні певного запиту на сервер.

Express дозволяє створювати маршрути для різних методів HTTP, таких як **GET**, **POST**, **PUT** та **DELETE**, та пов'язувати їх з функціями обробки, які виконують певні дії при отриманні запиту на цей маршрут. Крім того, Express надає можливість використовувати **middleware**, що дозволяє здійснювати обробку запитів перед тим, як вони будуть оброблені функцією маршруту.

Express також підтримує роботу з різними шаблонізаторами, такими як **Pug**, **EJS** та **Handlebars**, що дозволяє легко генерувати HTML-сторінки для відображення на клієнтському боці.

Приклад коду, який демонструє декілька функцій, які виконує Express:

```JavaScript
const express = require('express');
const app = express();

// Обробка GET-запитів до кореневого шляху "/"
app.get('/', (req, res) => {
  res.send('Hello World!');
});

// Обробка POST-запитів до шляху "/users"
app.post('/users', (req, res) => {
  // Логіка для створення нового користувача
});

// Використання middleware для логування запитів
app.use((req, res, next) => {
  console.log(`${req.method} ${req.url}`);
  next();
});

// Обробка помилок 404 (ресурс не знайдено)
app.use((req, res, next) => {
  res.status(404).send("Sorry, can't find that!");
});

// Приклад використання шаблонування EJS
app.set('view engine', 'ejs');
app.get('/users/:id', (req, res) => {
  const user = { name: 'John', age: 30, id: req.params.id };
  res.render('user', { user });
});

app.listen(3000, () => {
  console.log('Server started on port 3000');
});
```

В цьому прикладі:

- Обробка GET-запитів до кореневого шляху "/" відправляє відповідь з текстом "Hello World!".
- Обробка POST-запитів до шляху "/users" містить логіку для створення нового користувача.
- Middleware для логування запитів логує метод та URL запиту до консолі.
- Middleware для обробки помилок 404 відправляє клієнту відповідь з текстом "Sorry, can't find that!" у випадку, якщо запитаний ресурс не знайдено.
- Шаблонування EJS використовується для генерації відповіді на GET-запити до шляху "/users/:id". Шаблон `user.ejs` приймає об'єкт `user`, який містить інформацію про користувача, і відображає цю інформацію на сторінці.

---

<u>_3. Що таке middleware? Наведіть приклади_</u>

**Middleware** - це програмний код, який діє як посередник між додатком та його сервером або іншими додатками. Він може виконувати певні функції, такі як аутентифікація, авторизація, обробка запитів, реєстрація та логування.
Наприклад, у веб-розробці, middleware може використовуватися для авторизації користувачів, перевірки даних форм, обробки файлів, кешування даних і багатьох інших функцій. Також, middleware може використовуватися в інших галузях програмування, таких як розробка мобільних додатків та програмного забезпечення для серверів.

Ось декілька прикладів middleware:

- **Express.js** - фреймворк для створення веб-додатків на Node.js, що містить вбудований middleware для обробки запитів, маршрутизації, аутентифікації, статичних файлів тощо.
- **Redux** - бібліотека управління станом для JavaScript додатків, що використовує middleware для зберігання і обробки даних.
- **Django** - веб-фреймворк для розробки веб-додатків на мові Python, що містить middleware для обробки запитів, сесій, аутентифікації тощо.
- **Apache** - веб-сервер, що містить вбудований middleware для обробки запитів, журналювання, аутентифікації тощо.

Middleware у Express - це функція, яка зазвичай додається до ланцюжка обробки запитів і відповідей на сервері. Middleware дозволяє виконувати певні операції над запитом або відповіддю, такі як перевірка автентифікації, обробка даних, логування, кешування, тощо.

Кожна функція middleware приймає три параметри:

- об'єкт запиту (req) - містить інформацію про HTTP запит
- об'єкт відповіді (res) - містить методи, що дозволяють налаштувати відповідь на запит
- функцію next - функція, яка потрібна для передачі контролю до наступного middleware

Приклади middleware для Express:

1.  Middleware для логування запитів

```JavaScript
const express = require('express');
const app = express();

app.use((req, res, next) => {
  console.log(`[${new Date().toISOString()}] ${req.method} ${req.url}`);
  next();
});
```

2. Middleware для перевірки наявності авторизації

```JavaScript
const express = require('express');
const app = express();

app.use((req, res, next) => {
  if (!req.headers.authorization) {
    return res.status(401).send('Authorization header is missing');
  }
  // інші перевірки авторизації
  next();
});
```

3. Middleware для обробки помилок

```JavaScript
const express = require('express');
const app = express();

app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).send('Something broke!');
});
```

4. Middleware для визначення IP-адреси клієнта

```JavaScript
const express = require('express');
const app = express();

app.use((req, res, next) => {
  const ipAddress = req.headers['x-forwarded-for'] || req.connection.remoteAddress;
  req.ipAddress = ipAddress;
  next();
});
```

5. Middleware для обмеження кількості запитів

```JavaScript
const express = require('express');
const rateLimit = require('express-rate-limit');

const app = express();

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 хвилин
  max: 100 // максимальна кількість запитів за період
});
app.use(limiter);
```

Ці приклади допоможуть вам краще зрозуміти, як middleware використовується в Express.

---

<u>_4. Яка різниця між використанням шаблонізаторів для відображення і динамічними сторінками на основі JavaScript?_</u>

Шаблонізатори та динамічні сторінки на основі JavaScript - це дві різні технології для створення динамічного контенту на веб-сторінках.

Шаблонізатори використовуються для створення статичних HTML-сторінок з динамічним контентом. Вони працюють на серверній стороні і генерують HTML-код з даними, які отримують з бази даних або інших джерел даних. Шаблонізатори можуть бути корисними, коли сторінка має статичний вміст, але деякі частини, такі як дані користувачів або інформація про товари, можуть змінюватися в залежності від ситуації.

Динамічні сторінки на основі JavaScript дають можливість створювати динамічний контент, який змінюється без перезавантаження сторінки. Це досягається за допомогою JavaScript, який взаємодіє зі сторінкою і забезпечує відображення динамічного контенту. Динамічні сторінки на основі JavaScript дозволяють взаємодіяти з користувачем без перезавантаження сторінки і дають більшу можливість для створення складних веб-додатків.

Отже, різниця між шаблонізаторами та динамічними сторінками на основі JavaScript полягає в тому, що шаблонізатори генерують HTML-код на серверній стороні з даними, тоді як динамічні сторінки на основі JavaScript дозволяють взаємодіяти з користувачем без перезавантаження сторінки та забезпечують відображення динамічного контенту за допомогою JavaScript.

Розглянемо приклади, які демонструють різницю між ними:

1. Оновлення частини сторінки без перезавантаження

Якщо ви використовуєте шаблонізатор для відображення, ви можете оновлювати тільки ту частину сторінки, яку потрібно змінити, без перезавантаження всієї сторінки. Проте, це зазвичай потребує використання AJAX-запитів, що може бути трохи складним.

Якщо ви використовуєте динамічні сторінки на основі JavaScript, ви можете оновлювати сторінку динамічно, без використання AJAX-запитів. Це зазвичай більш простий спосіб, але він може бути менш гнучким.

2. Швидкість завантаження сторінки

Якщо ви використовуєте шаблонізатор для відображення, сторінка буде завантажуватися повністю при кожному запиті. Це може бути повільно, особливо якщо сторінка містить багато даних.

Якщо ви використовуєте динамічні сторінки на основі JavaScript, ви можете завантажувати тільки необхідні дані, що зменшує час завантаження сторінки. Це може бути швидше, особливо якщо ви завантажуєте лише необхідні дані.

Приклад коду для шаблонізатора Handlebars та динамічної сторінки на основі JavaScript з використанням бібліотеки jQuery для отримання даних з сервера.

- Шаблонізатор Handlebars:

```JavaScript
<!DOCTYPE html>
<html>
  <head>
    <title>Шаблонізатор Handlebars</title>
  </head>
<body>
    <ul>
      {{#each users}}
        <li>{{this.name}}</li>
      {{/each}}
     </ul>
</body>
</html>
```

- JavaScript для відображення даних з сервера на сторінці:

```JavaScript
$(document).ready(function() {
    $.ajax({
        url: "/api/users",
        type: "GET",
        success: function(data) {
            var users = data.users;
            var list = "";

            for (var i = 0; i < users.length; i++) {
                list += "<li>" + users[i].name + "</li>";
            }

            $("#user-list").html(list);
        }
    });
});
```

У цьому прикладі, шаблонізатор Handlebars використовується для відображення списку користувачів на сторінці. Код JavaScript звертається до сервера за допомогою асинхронного запиту, отримує дані у форматі JSON, та створює список користувачів, який відображається на сторінці.

Це демонструє різницю між шаблонізаторами та динамічними сторінками на основі JavaScript: шаблонізатор відображає дані, які вже є на сторінці, тоді як динамічні сторінки на основі JavaScript використовують асинхронні запити для отримання та відображення даних з сервера без перезавантаження сторінки.

---

<u>_5. Як можна позбутися дублювання елементів сторінок використовуючи шаблонізатори, які повторюються - футер, хедер та інші?_</u>

Найкращим способом запобігти дублюванню елементів сторінок за допомогою шаблонізаторів є використання одного центрального міста для написання коду, а також використання змінних для отримання певних значень. Ця техніка дозволить вам перевірити текст, HTML-теги та інші дані перед використанням їх в вашій веб-сторінці.

Для уникнення дублювання елементів сторінок, які повторюються, можна використовувати шаблонізатори з підтримкою наслідування (`inheritance`) або включення (`include`).

Шаблонізатори з підтримкою наслідування дозволяють створювати базовий шаблон, який містить загальні елементи сторінок, такі як хедер, футер, меню тощо, а потім створювати дочірні шаблони, які наслідують ці елементи з базового шаблону та додають до них власний унікальний вміст. Таким чином, необхідні елементи сторінки дублюватися не будуть, оскільки вони будуть знаходитися в базовому шаблоні, який буде використовуватися для кожної сторінки.

Шаблонізатори з підтримкою включення дозволяють включати один шаблон в інший, щоб уникнути дублювання загальних елементів сторінок. Наприклад, футер можна створити в окремому шаблоні, а потім включити його в кожну сторінку, що забезпечить наявність футера на кожній сторінці без дублювання коду.

Конкретний спосіб уникнення дублювання елементів сторінок залежить від використовуваного шаблонізатора та його можливостей. Однак, в загальному випадку, використання наслідування та включення може значно полегшити створення та підтримку шаблонів.

Наприклад, використовуючи шаблонізатор `EJS`, можна створити базовий шаблон `base.ejs`, який містить загальні елементи сторінки:

```JavaScript
<!DOCTYPE html>
<html>
  <head>
    <title><%= title %></title>
  </head>
  <body>
    <header>
      <!-- Заголовок сайту, меню тощо -->
    </header>
    <main>
      <% include content %>
    </main>
    <footer>
      <!-- Підвал сайту -->
    </footer>
  </body>
</html>
```

Дочірні шаблони, які наслідуються від базового шаблону, можуть додавати свій унікальний вміст та перевизначати блоки базового шаблону за допомогою тегу `<%- include() %>`. Наприклад, дочірній шаблон `home.ejs`, який відображає головну сторінку сайту, може мати такий вміст:

```JavaScript
<% layout('base') %>
<% block title %>Головна сторінка<% endblock %>
<% block content %>
<!-- Вміст головної сторінки -->
<% endblock %>
```

При відображенні сторінки `home.ejs`, `EJS` автоматично включить базовий шаблон `base.ejs` та замінить блоки `<% block %>` у дочірньому шаблоні на їх вміст. Таким чином, на головній сторінці сайту будуть відображені загальні елементи сторінки з базового шаблону та унікальний вміст з дочірнього шаблону.

Інший спосіб уникнення дублювання елементів сторінки полягає використанні включення шаблонів. Наприклад, у шаблоні `base.ejs` можна використати тег `<%- include('header.ejs') %>` та `<%- include('footer.ejs') %>` для включення відповідних шаблонів для хедеру та футера, які містять відповідний HTML код.

Наприклад, файл `header.ejs` може містити наступний код:

```JavaScript
<header>
  <nav>
    <ul>
      <li><a href="/">Home</a></li>
      <li><a href="/about">About</a></li>
      <li><a href="/contact">Contact</a></li>
    </ul>
  </nav>
</header>
А файл footer.ejs може містити наступний код:
<footer>
  <p>&copy; 2023 My Website</p>
</footer>
```

Тоді у файлі `base.ejs` можна включити ці шаблони наступним чином:

```JavaScript
<!DOCTYPE html>
<html>
  <head>
    <title><%= title %></title>
  </head>
  <body>
    <% include('header.ejs') %>
    <main>
      <!-- Вміст сторінки -->
    </main>
    <% include('footer.ejs') %>
  </body>
</html>
```

При відображенні сторінки, `EJS` автоматично вставить HTML код з файлів `header.ejs` та `footer.ejs` у відповідні місця у шаблоні `base.ejs`. Ці два способи дозволяють уникнути дублювання елементів сторінки та полегшують підтримку веб-сайту.
