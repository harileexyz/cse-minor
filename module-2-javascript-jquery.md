# Module 2: JavaScript and jQuery

**Course:** Web Application Development (MNCST509)
**Programme:** B.Tech CSE Minor, KTU, Semester 5
**Module:** 2 of the syllabus (11 contact hours)

This module is written for students who know basic HTML and CSS (Module 1) but are **new to JavaScript**. Teach one idea at a time, run the example, then let students change it.

**How to run every example:** save the code as `something.html`, double-click to open it in Chrome. Press `F12` and open the **Console** tab to see `console.log` messages and errors.

---

## Contents

**Part A: JavaScript**
1. Introduction to scripting
2. Programming fundamentals: variables, data types, operators
3. Obtaining user input with prompt dialogues
4. Arithmetic
5. Decision making
6. Control statements (loops)
7. Functions
8. Arrays
9. Objects
10. Document Object Model (DOM)
11. Form processing

**Part B: jQuery**
12. What is jQuery? A basic example
13. Selecting elements
14. Getting and changing content, attributes and CSS
15. Inserting new elements
16. Looping with `.each()`
17. Events and the event object
18. Effects and animation
19. Traversing the DOM
20. Working with forms
21. JavaScript libraries

**Part C:** Mini-project and exam questions

## Suggested lesson plan

| Class | Topics |
|---|---|
| 1 | Scripting, variables, data types |
| 2 | Operators, arithmetic, prompt dialogues |
| 3 | Decision making |
| 4 | Loops |
| 5 | Functions, arrays |
| 6 | Objects, DOM |
| 7 | Form processing |
| 8 | jQuery basics, selecting, content, attributes, CSS |
| 9 | Inserting, `.each()`, events |
| 10 | Effects, traversing, forms, libraries |
| 11 | Mini-project and exam questions |

---

# PART A: JAVASCRIPT

## 1. Introduction to Scripting

**HTML** gives a page its content. **CSS** gives it style. **JavaScript** makes it **do things**: react to clicks, check forms, change content without reloading.

**Analogy:** a TV. HTML is the screen and cabinet, CSS is the colours and picture settings, JavaScript is the remote control that makes things happen.

A **script** is a small program that runs inside the browser. **Scripting** means writing such programs.

**Three ways to add JavaScript:**

```html
<!-- 1. Inside the page -->
<script>
  console.log("Hello from the page");
</script>

<!-- 2. In an external file (best for real sites) -->
<script src="script.js"></script>

<!-- 3. Inside a tag (for tiny jobs) -->
<button onclick="alert('Clicked!')">Click me</button>
```

**First program:**

```html
<!DOCTYPE html>
<html>
<head><title>First JS</title></head>
<body>
  <h2 id="msg">Hello</h2>
  <script>
    console.log("Page loaded");
    document.getElementById("msg").innerHTML = "Hello from JavaScript!";
  </script>
</body>
</html>
```

**Real world:** the "Add to cart" button, the live seat count on IRCTC, and the "like" heart on Instagram are all JavaScript.

**Common mistakes:**
- Putting `<script>` before the element it uses. Put scripts at the **end of the body**.
- Mixing up `"` and `'` quotes.
- Not opening the Console, so errors stay hidden.

### Check your understanding
1. What is the role of JavaScript on a web page?
2. Name two ways to add JavaScript to a page.

## 2. Programming Fundamentals

### 2.1 Variables

A **variable** is a named box that holds a value.

```javascript
let name = "Anu";        // can change later
const pi = 3.14;         // cannot change
var old = 10;            // old style, avoid
name = "Rahul";          // fine
console.log(name, pi);
```

Rules for names: start with a letter, `_` or `$`; no spaces; case matters (`age` and `Age` are different). Use meaningful names like `totalMarks`.

**Analogy:** a labelled steel container in the kitchen. The label is the name; what is inside can change (`let`) or is sealed (`const`).

### 2.2 Data types

| Type | Example | Meaning |
|---|---|---|
| Number | `25`, `3.5` | whole and decimal numbers |
| String | `"hello"` | text |
| Boolean | `true`, `false` | yes or no |
| Undefined | `let x;` | variable with no value yet |
| Null | `null` | deliberately empty |

```javascript
let age = 20;
let city = "Kochi";
let passed = true;
console.log(typeof age);     // number
console.log(typeof city);    // string
```

Join strings with `+`: `"Hello " + city` gives `Hello Kochi`.

### 2.3 Operators

| Kind | Operators | Example |
|---|---|---|
| Arithmetic | `+ - * / % ` | `7 % 3` is `1` |
| Assignment | `= += -=` | `x += 5` means `x = x + 5` |
| Comparison | `== === != !== > < >= <=` | `5 > 3` is `true` |
| Logical | `&& \|\| !` | and, or, not |
| Increase / decrease | `++ --` | `count++` |

**`==` versus `===`:** `"5" == 5` is `true` (compares value only). `"5" === 5` is `false` (compares value and type). **Always use `===`.**

**Common mistakes:**
- Using `=` (store) when you mean `===` (compare).
- Forgetting that `"5" + 3` gives `"53"` (text joining), not `8`.

### Check your understanding
1. What is the difference between `let` and `const`?
2. What does `"10" + 5` give? What does `"10" - 5` give?
3. What is the difference between `==` and `===`?

## 3. Obtaining User Input with Prompt Dialogues

JavaScript has three **dialog boxes**:

| Dialog | Use | Returns |
|---|---|---|
| `alert("text")` | Show a message with OK | nothing |
| `prompt("question", "default")` | Ask the user to **type** something | the text typed (or `null` if Cancel) |
| `confirm("question")` | Ask OK or Cancel | `true` or `false` |

```html
<script>
  let name = prompt("What is your name?");
  alert("Hello, " + name + "!");

  let sure = confirm("Do you want to continue?");
  if (sure) {
    alert("Great, let us continue");
  } else {
    alert("Stopped");
  }
</script>
```

**Important:** `prompt` always gives back **text**. To use it as a number, convert it:

```javascript
let age = Number(prompt("Enter your age"));
alert("Next year you will be " + (age + 1));
```

**`prompt()` versus `alert()` (exam point):** `alert` only **shows** a message and returns nothing. `prompt` **asks for input** and returns what the user typed.

**Analogy:** `alert` is a loudspeaker announcement (one way). `prompt` is a counter clerk asking "Name, please?" (two way).

**Common mistakes:** adding two prompted numbers without `Number(...)`, so `"5" + "3"` gives `"53"`.

## 4. Arithmetic

```javascript
let a = 17, b = 5;
console.log(a + b);   // 22
console.log(a - b);   // 12
console.log(a * b);   // 85
console.log(a / b);   // 3.4
console.log(a % b);   // 2   (remainder)
console.log(a ** 2);  // 289 (power)
```

Order of work: brackets, then `* / %`, then `+ -`. Use brackets to be clear.

Useful `Math` tools:

```javascript
Math.round(4.6);     // 5
Math.floor(4.9);     // 4
Math.ceil(4.1);      // 5
Math.max(3, 9, 5);   // 9
Math.sqrt(16);       // 4
Math.random();       // random number between 0 and 1
(3.14159).toFixed(2) // "3.14"  (2 decimal places)
```

**Simple calculator:**

```html
<script>
  let x = Number(prompt("First number"));
  let y = Number(prompt("Second number"));
  alert("Sum = " + (x + y) + "\nProduct = " + (x * y));
</script>
```

**Real world:** bill totals, GST, EMI and discount calculations on shopping sites.

## 5. Decision Making

Programs choose what to do using conditions.

```javascript
let marks = Number(prompt("Enter marks"));

if (marks >= 90) {
  alert("Grade A");
} else if (marks >= 60) {
  alert("Grade B");
} else if (marks >= 40) {
  alert("Pass");
} else {
  alert("Fail");
}
```

**`switch`** is neat when checking one value against many choices:

```javascript
let day = Number(prompt("Day number (1-3)"));
switch (day) {
  case 1: alert("Monday"); break;
  case 2: alert("Tuesday"); break;
  case 3: alert("Wednesday"); break;
  default: alert("Not in this demo");
}
```

Without `break`, execution falls into the next case.

Combine conditions: `if (age >= 18 && hasId)` (both), `if (a || b)` (either).

**Analogy:** a fork in the road with signboards. You take the road whose sign matches your destination.

**Real world:** IRCTC checks "is the seat free?" and "is the age above 60 for the senior discount?".

**Common mistake:** `if (x = 5)` (stores 5) instead of `if (x === 5)` (compares).

### Check your understanding
1. Write code to check whether a number is even or odd.
2. When would you use `switch` instead of `if/else`?

## 6. Control Statements (Loops)

A **loop** repeats code.

```javascript
// for: when you know how many times
for (let i = 1; i <= 5; i++) {
  console.log("Number " + i);
}

// while: repeat while a condition is true
let n = 1;
while (n <= 3) {
  console.log("Round " + n);
  n++;
}

// do...while: runs at least once
let k = 10;
do {
  console.log("k is " + k);
  k++;
} while (k < 5);
```

| Loop | Checks the condition |
|---|---|
| `for` | first, then repeats |
| `while` | first, then repeats |
| `do...while` | **after** running once |

**`break` and `continue`:**

```javascript
for (let i = 1; i <= 10; i++) {
  if (i === 3) continue;   // skip 3
  if (i === 6) break;      // stop the loop at 6
  console.log(i);          // prints 1 2 4 5
}
```

**Multiplication table:**

```javascript
let num = Number(prompt("Table of which number?"));
for (let i = 1; i <= 10; i++) {
  console.log(num + " x " + i + " = " + num * i);
}
```

**Analogy:** a loop is a **temple circumambulation**: keep going round until the count is complete. `break` means leave early, `continue` means skip this round.

**Common mistake:** forgetting `n++` in a `while` loop, so it never ends (the page freezes).

### Check your understanding
1. Print the numbers 1 to 10 using a `for` loop.
2. What is the difference between `while` and `do...while`?
3. What do `break` and `continue` do?

## 7. Functions

A **function** is a named block of code you can use again and again.

```javascript
function greet(name) {
  return "Hello, " + name + "!";
}

console.log(greet("Anu"));     // Hello, Anu!
console.log(greet("Rahul"));   // Hello, Rahul!

function add(a, b) {
  return a + b;
}
let total = add(5, 7);         // 12
```

| Part | Meaning |
|---|---|
| `name` in brackets | **parameter**: the input |
| `return` | sends the answer back |
| `greet("Anu")` | **calling** the function |

**Analogy:** a recipe card. Write it once, cook it many times with different ingredients (parameters).

**Why functions help organise code:** write once and reuse, easy to fix in one place, and big programs become small named pieces.

**Common mistakes:** forgetting `return`, or writing the function but never calling it.

## 8. Arrays

An **array** stores **many values** in one variable. Positions (indexes) start at **0**.

```javascript
let fruits = ["Mango", "Banana", "Apple"];

console.log(fruits[0]);        // Mango
console.log(fruits.length);    // 3

fruits.push("Orange");         // add at end
fruits.pop();                  // remove from end
fruits.unshift("Grapes");      // add at start
fruits.shift();                // remove from start

for (let i = 0; i < fruits.length; i++) {
  console.log(i + ": " + fruits[i]);
}
```

| Tool | Does |
|---|---|
| `push(x)` / `pop()` | add / remove at the end |
| `unshift(x)` / `shift()` | add / remove at the start |
| `length` | number of items |
| `indexOf(x)` | position of x (or -1) |
| `sort()` | sort the items |

**Analogy:** a row of numbered lockers. `fruits[0]` is locker number 0.

**Real world:** a shopping cart is an array of items.

**Common mistake:** counting from 1. The last item is at `length - 1`.

### Check your understanding
1. How do you get the last item of an array?
2. Write code to add up all numbers in `[4, 8, 15]` using a loop.

## 9. Objects

An **object** stores related information using **name: value** pairs.

```javascript
let student = {
  name: "Anu",
  age: 20,
  dept: "CSE",
  marks: [80, 90, 85]
};

console.log(student.name);          // Anu
console.log(student["dept"]);       // CSE
student.age = 21;                   // change
student.city = "Kochi";             // add new

// an object can hold a function too
let car = {
  brand: "Maruti",
  start: function () {
    console.log(this.brand + " started");
  }
};
car.start();                        // Maruti started
```

Array of objects (very common):

```javascript
let students = [
  { name: "Anu", marks: 85 },
  { name: "Rahul", marks: 72 }
];
for (let i = 0; i < students.length; i++) {
  console.log(students[i].name + " scored " + students[i].marks);
}
```

**Analogy:** a student ID card. Fields like name, roll number and department, all about one person.

**Array versus object:** use an array for a **list of similar things**, an object for the **details of one thing**.

### Check your understanding
1. Create an object for a book with title, author and price.
2. How do you read and change one property?

## 10. Document Object Model (DOM)

The browser turns the HTML page into a **tree of objects** called the **DOM**. JavaScript uses it to read and change the page.

```
document
  └── html
       ├── head
       └── body
            ├── h1
            └── p
```

**Analogy:** a family tree of the page. JavaScript can find any member and change them.

**Finding elements:**

```javascript
document.getElementById("title");          // by id
document.querySelector(".note");           // first match of a CSS selector
document.querySelectorAll("p");            // all matches
```

**Changing them:**

```javascript
let el = document.getElementById("title");
el.innerHTML = "New heading";              // change content
el.style.color = "red";                    // change style
el.style.fontSize = "30px";
el.setAttribute("title", "Tooltip");       // change attribute
```

**Reacting to events:**

```html
<h2 id="title">Hello</h2>
<button id="btn">Change</button>

<script>
  document.getElementById("btn").onclick = function () {
    let t = document.getElementById("title");
    t.innerHTML = "You clicked the button!";
    t.style.color = "green";
  };
</script>
```

Common events: `onclick`, `onmouseover`, `onmouseout`, `onkeyup`, `onchange`, `onsubmit`.

**Real world:** a "Show password" tick box, dark mode switches, and the live character counter on a tweet box all change the DOM.

**Common mistakes:**
- Running the script before the element exists (put script at the end of the body).
- Wrong id spelling (the result is `null` and an error in the Console).

### Check your understanding
1. What is the DOM?
2. Write code to change the text of a paragraph with id `intro` when a button is clicked.

## 11. Form Processing

Before sending a form to a server, JavaScript can **check the input** (**validation**). This saves time and gives instant feedback.

**Reading form values:**

```javascript
let name = document.getElementById("name").value;
```

**Validation example: check that a field is not empty, and the mobile number is 10 digits.**

```html
<!DOCTYPE html>
<html>
<head><title>Validation</title></head>
<body>
  <h3>Register</h3>
  <form id="regForm">
    Name: <input type="text" id="name"><br><br>
    Mobile: <input type="text" id="mobile"><br><br>
    <button type="submit">Register</button>
  </form>
  <p id="msg" style="color:red"></p>

  <script>
    document.getElementById("regForm").onsubmit = function (e) {
      let name = document.getElementById("name").value.trim();
      let mobile = document.getElementById("mobile").value.trim();
      let msg = document.getElementById("msg");

      if (name === "") {
        msg.innerHTML = "Please enter your name";
        e.preventDefault();               // stop the form from being sent
        return;
      }
      if (mobile.length !== 10 || isNaN(mobile)) {
        msg.innerHTML = "Mobile must be 10 digits";
        e.preventDefault();
        return;
      }
      msg.innerHTML = "";
      alert("Form is valid. Thank you " + name + "!");
      e.preventDefault();                  // (only for this demo, so the page stays)
    };
  </script>
</body>
</html>
```

How it works:
1. `onsubmit` runs when the user clicks Register.
2. We read each value, with `.trim()` removing spaces.
3. If something is wrong, we show a message and call `e.preventDefault()` to **stop the submission**.

**Analogy:** the security guard at a gate checking your ID card **before** you go in.

**Real world:** every sign-up form that says "Email is invalid" or "Password too short".

**Note:** this check helps users, but the **server must check again**, because a user can bypass browser checks.

### Check your understanding
1. What is form validation? Why do it?
2. What does `e.preventDefault()` do?
3. Write code to check that a text field is not empty when a form is submitted.

---

# PART B: jQUERY

---

## 12. What is jQuery? A Basic Example

**jQuery** is a JavaScript library: a ready-made file of functions that makes common page tasks short. Motto: "write less, do more".

**Analogy:** jQuery is like **GPay**. Paying with bank details, IFSC and account number takes many steps. GPay turns it into "scan and pay". jQuery turns long JavaScript into one-liners.

Every jQuery line has the same shape:

```
$(selector).action();
   which       what to do
```

Add jQuery **before** your own script, and put your code inside "document ready" so it runs after the page loads:

```html
<!DOCTYPE html>
<html>
<head>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
</head>
<body>
  <p>This paragraph will hide.</p>
  <button id="hideBtn">Hide</button>

  <script>
    $(function () {              // short form of $(document).ready(...)
      $("#hideBtn").click(function () {
        $("p").hide();
      });
    });
  </script>
</body>
</html>
```

**Real world:** WordPress themes, Bootstrap 3 sites and many college and government portals still use jQuery for menus, sliders and popups.

**Common mistake:** loading your script before jQuery gives the error `$ is not defined`.

---

## 13. Selecting Elements

jQuery uses the same selectors as CSS.

| Selector | Selects |
|---|---|
| `$("p")` | all `<p>` elements |
| `$("#menu")` | element with id `menu` |
| `$(".item")` | all elements with class `item` |
| `$("ul li")` | `<li>` inside a `<ul>` |
| `$("li:first")` | first `<li>` |
| `$("input[type='text']")` | text boxes |

**Analogy:** a selector is like a teacher calling "everyone in the last bench" or "roll number 12". It picks who should act.

---

## 14. Getting and Changing Content, Attributes and CSS

The same method **reads** when you give no value, and **writes** when you give a value.

| Task | Read | Write |
|---|---|---|
| Text | `$("#a").text()` | `$("#a").text("Hi")` |
| HTML | `$("#a").html()` | `$("#a").html("<b>Hi</b>")` |
| Form value | `$("#name").val()` | `$("#name").val("Anu")` |
| Attribute | `$("img").attr("src")` | `$("img").attr("src", "tea.jpg")` |
| CSS | `$("p").css("color")` | `$("p").css("color", "blue")` |
| Class | `$("p").hasClass("x")` | `addClass`, `removeClass`, `toggleClass` |

```javascript
$("#price").text("Rs. 20");
$("#logo").attr("alt", "Chai Corner logo");
$("p").css({ color: "blue", fontSize: "18px" });   // many CSS properties at once
```

**Analogy:** `text()` is like reading the menu board; `text("new")` is like wiping it and writing a new price.

---

## 15. Inserting New Elements

| Method | Where it adds |
|---|---|
| `append()` | at the end, inside |
| `prepend()` | at the start, inside |
| `after()` | just after, outside |
| `before()` | just before, outside |
| `remove()` | deletes the element |

```javascript
$("#menu").append("<li>Samosa</li>");    // added at the bottom of the list
$("#menu").prepend("<li>Tea</li>");      // added at the top
$("#oldItem").remove();
```

**Real world:** new WhatsApp Web messages, or "Load more" products on Flipkart, are added to the page this way.

---

## 16. Looping with .each()

`.each()` runs a function once for every selected element. `$(this)` is the current element.

```javascript
$("li").each(function (index) {
  $(this).text((index + 1) + ". " + $(this).text());   // numbers every list item
});
```

**Analogy:** a class teacher taking attendance, calling each student one by one.

---

## 17. Events and the Event Object

An **event** is something the user does: click, typing, mouse over, submit.

| Event | Fires when |
|---|---|
| `click` | element is clicked |
| `mouseenter` / `mouseleave` | mouse moves in / out |
| `keyup` | a key is released |
| `change` | a dropdown or box value changes |
| `submit` | a form is submitted |

Write them as `$("#btn").click(fn)` or `$("#btn").on("click", fn)`.

The function gets an **event object** (usually called `e`) with details about what happened:

```javascript
$("a").on("click", function (e) {
  e.preventDefault();               // stop the link from opening
  console.log(e.type, e.pageX, e.pageY);   // "click" and mouse position
});
```

**Analogy:** an event is the doorbell ringing; the event object is the doorbell camera telling you who pressed it and when.

**Exam favourite: change a div's colour on mouse over and back on mouse out**

```javascript
$("#box").mouseenter(function () {
  $(this).css("background-color", "yellow");
}).mouseleave(function () {
  $(this).css("background-color", "white");
});
```

---

## 18. Effects and Animation

| Effect | What it does |
|---|---|
| `hide()`, `show()`, `toggle()` | hide / show / switch |
| `fadeIn()`, `fadeOut()`, `fadeToggle()` | slowly appear / disappear |
| `slideUp()`, `slideDown()`, `slideToggle()` | roll up / roll down |
| `animate({...}, time)` | smoothly change number-based CSS |

Time is in milliseconds (1000 = 1 second), or `"slow"` / `"fast"`.

```javascript
$("#faq-answer").slideToggle("slow");                       // FAQ open/close
$("#box").animate({ width: "300px", opacity: 0.5 }, 1000);  // grow and fade in 1 s
```

**Note:** `animate()` works only on number values (width, height, opacity, left). It cannot animate colours without a plugin.

**Real world:** FAQ sections that slide open, and "Added to cart" messages that fade away.

---

## 19. Traversing the DOM (Moving Around the Page Tree)

| Method | Moves to |
|---|---|
| `parent()` | the element just above |
| `children()` | elements just below |
| `find("x")` | any matching element below |
| `siblings()` | elements at the same level |
| `next()` / `prev()` | the next / previous sibling |

```javascript
$(".delete").click(function () {
  $(this).parent().remove();    // remove the <li> that holds this button
});
```

**Analogy:** a family tree. From yourself you can go to your parent, your children or your brothers and sisters.

---

## 20. Working with Forms

```javascript
$("#regForm").submit(function (e) {
  if ($("#name").val().trim() === "") {
    e.preventDefault();                  // stop sending the form
    $("#err").text("Name is required");
  }
});
```

Useful: `val()` reads a value, `$("#agree").is(":checked")` checks a checkbox, `$("#city").change(fn)` reacts to a dropdown.

---

## 21. JavaScript Libraries

A **library** is code someone else wrote that you can reuse, so you don't write everything yourself.

| Library | Used for |
|---|---|
| jQuery | page changes, events, effects |
| Chart.js | charts and graphs |
| Lodash | helper functions for arrays and objects |
| Moment.js / Day.js | dates and times |
| React (Module 4) | building user interfaces from components |

**Analogy:** a library is like buying ready-made parotta from the shop instead of making the dough yourself.

**Why jQuery is used less today:** modern JavaScript now has short built-in ways (`document.querySelector`, `classList`, `fetch`) for most things jQuery made easy. It is still common in older sites, so it is worth knowing.

---

## One page to try everything

Save as `jquery-demo.html` and open it in Chrome.

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>jQuery Demo</title>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <style>
    #box { width: 120px; height: 60px; background: white; border: 1px solid #333; }
    .done { text-decoration: line-through; color: gray; }
  </style>
</head>
<body>
  <h2 id="title">Chai Corner Menu</h2>
  <ul id="menu">
    <li>Tea <button class="del">x</button></li>
    <li>Coffee <button class="del">x</button></li>
  </ul>

  <input id="newItem" placeholder="New item">
  <button id="addBtn">Add</button>
  <span id="err" style="color:red"></span>

  <p>
    <button id="blueBtn">Make paragraphs blue</button>
    <button id="toggleBtn">Show / hide menu</button>
  </p>
  <p>Hover over the box:</p>
  <div id="box"></div>

  <script>
    $(function () {
      // content
      $("#title").text("Chai Corner Menu (jQuery)");

      // insert + form value
      $("#addBtn").click(function () {
        var name = $("#newItem").val().trim();
        if (name === "") {
          $("#err").text("Type an item first");
          return;
        }
        $("#err").text("");
        $("#menu").append("<li>" + name + ' <button class="del">x</button></li>');
        $("#newItem").val("");
      });

      // traversing + remove (on document so new buttons also work)
      $(document).on("click", ".del", function () {
        $(this).parent().fadeOut(300, function () { $(this).remove(); });
      });

      // CSS on all paragraphs
      $("#blueBtn").click(function () {
        $("p").css("color", "blue");
      });

      // effect
      $("#toggleBtn").click(function () {
        $("#menu").slideToggle();
      });

      // mouse events
      $("#box").mouseenter(function () {
        $(this).css("background-color", "yellow");
      }).mouseleave(function () {
        $(this).css("background-color", "white");
      });
    });
  </script>
</body>
</html>
```

---

## Check your understanding (jQuery)

1. What does `$` mean, and why do we wrap code in `$(function () { ... })`?
2. What is the difference between `text()` and `text("Hi")`?
3. Write one line to add `<li>Vada</li>` at the end of `#menu`.
4. What does `e.preventDefault()` do in a form submit handler?
5. Name two effects and say what each does.
6. In `$(this).parent().remove()`, what gets removed?

**Classroom activity (10 min):** give each pair one row of the tables above. They must write a one-line example and show it working in the demo page.

---

# PART C: Mini-Project and Exam Questions

## Mini-project: Tea Shop Bill

A page where the user picks an item and quantity, adds it to a bill, and sees the total with 5 percent GST. It uses variables, arrays, objects, functions, loops, DOM, events and validation.

Save as `teashop.html`:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Chai Corner Bill</title>
  <style>
    body { font-family: Arial; max-width: 420px; margin: 30px auto; }
    table { border-collapse: collapse; width: 100%; margin-top: 15px; }
    th, td { border: 1px solid #999; padding: 6px; text-align: left; }
    th { background: #333; color: white; }
    #error { color: red; }
  </style>
</head>
<body>
  <h2>Chai Corner</h2>

  Item:
  <select id="item">
    <option value="Tea">Tea - 10</option>
    <option value="Coffee">Coffee - 15</option>
    <option value="Samosa">Samosa - 20</option>
  </select>
  Quantity: <input type="number" id="qty" value="1" style="width:60px">
  <button id="addBtn">Add</button>
  <p id="error"></p>

  <table>
    <thead><tr><th>Item</th><th>Qty</th><th>Amount</th></tr></thead>
    <tbody id="billBody"></tbody>
  </table>
  <p id="totals"></p>

  <script>
    // prices stored in an object
    let prices = { Tea: 10, Coffee: 15, Samosa: 20 };
    // the bill is an array of objects
    let bill = [];

    function showBill() {
      let rows = "";
      let subtotal = 0;
      for (let i = 0; i < bill.length; i++) {
        let amount = bill[i].qty * prices[bill[i].item];
        subtotal = subtotal + amount;
        rows += "<tr><td>" + bill[i].item + "</td><td>" + bill[i].qty + "</td><td>" + amount + "</td></tr>";
      }
      document.getElementById("billBody").innerHTML = rows;

      let gst = subtotal * 0.05;
      document.getElementById("totals").innerHTML =
        "Subtotal: " + subtotal.toFixed(2) + "<br>" +
        "GST (5%): " + gst.toFixed(2) + "<br>" +
        "<b>Total: " + (subtotal + gst).toFixed(2) + "</b>";
    }

    document.getElementById("addBtn").onclick = function () {
      let item = document.getElementById("item").value;
      let qty = Number(document.getElementById("qty").value);
      let error = document.getElementById("error");

      // validation
      if (qty < 1 || !Number.isInteger(qty)) {
        error.innerHTML = "Quantity must be a whole number, 1 or more";
        return;
      }
      error.innerHTML = "";

      bill.push({ item: item, qty: qty });
      showBill();
    };
  </script>
</body>
</html>
```

Try: 2 Tea and 1 Samosa gives subtotal 40.00, GST 2.00, total 42.00. Quantity `0` shows the error.

**Extension (jQuery):** after Part B, rewrite the button click using `$("#addBtn").click(...)` and make new rows fade in with `.hide().fadeIn()`.

**Second small project: jQuery to-do list.** Save as `todo-jquery.html`:

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>To-do</title>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <style>
    .done { text-decoration: line-through; color: gray; }
    li { cursor: pointer; margin: 5px 0; }
  </style>
</head>
<body>
  <h2>My Tasks</h2>
  <input id="task" placeholder="New task">
  <button id="add">Add</button>
  <span id="err" style="color:red"></span>
  <ul id="list"></ul>
  <p>Click a task to mark it done.</p>

  <script>
    $(function () {
      $("#add").click(function () {
        let text = $("#task").val().trim();
        if (text === "") {
          $("#err").text("Type a task first");
          return;
        }
        $("#err").text("");
        $("<li>").text(text).hide().appendTo("#list").fadeIn();
        $("#task").val("");
      });

      $("#list").on("click", "li", function () {
        $(this).toggleClass("done");
      });
    });
  </script>
</body>
</html>
```

---

## Exam Questions (short answers)

**Q1. Difference between `prompt()` and `alert()`. Give an example of `prompt()` to get input. (3 marks)**

`alert()` only **shows** a message with an OK button and returns nothing. `prompt()` **asks the user to type** a value and returns it as text (or `null` if Cancel is pressed).

```javascript
let name = prompt("Enter your name");
alert("Hello, " + name);
```

**Q2. jQuery to hide a paragraph when a button is clicked. (3 marks)**

```html
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
<p>Hide me</p>
<button id="btn">Hide</button>
<script>
  $(function () {
    $("#btn").click(function () {
      $("p").hide();
    });
  });
</script>
```

**Q3. Explain how JavaScript handles form validation. Example to check if a text field is empty on submit. (6 marks)**

Explain: validation checks input before it is sent. JavaScript reads the values with `.value`, tests them with `if`, shows a message, and calls `e.preventDefault()` to stop the form being sent if there is a problem. Then give the code:

```html
<form id="f">
  <input type="text" id="name">
  <button type="submit">Submit</button>
</form>
<p id="msg" style="color:red"></p>

<script>
  document.getElementById("f").onsubmit = function (e) {
    let name = document.getElementById("name").value.trim();
    if (name === "") {
      document.getElementById("msg").innerHTML = "Name cannot be empty";
      e.preventDefault();
    }
  };
</script>
```

**Q4. jQuery to change a div's background when the mouse moves over it and back when it moves away. (3 marks)**

```javascript
$(function () {
  $("#box").mouseenter(function () {
    $(this).css("background-color", "yellow");
  }).mouseleave(function () {
    $(this).css("background-color", "white");
  });
});
```

**Q5. Explain functions and arrays in JavaScript with examples. How do they help organise code? (5 marks)**

A **function** is a named block of code that can be called many times. An **array** stores many values in one variable.

```javascript
let marks = [80, 65, 90];

function average(list) {
  let sum = 0;
  for (let i = 0; i < list.length; i++) {
    sum = sum + list[i];
  }
  return sum / list.length;
}

console.log(average(marks));   // 78.33...
```

How they help: functions avoid repeating code and can be fixed in one place; arrays keep related data together so a loop can process it. Together, large programs are split into small, named, reusable pieces.

**Q6. jQuery to select all paragraphs and change their font colour to blue on button click. (3 marks)**

```javascript
$(function () {
  $("#btn").click(function () {
    $("p").css("color", "blue");
  });
});
```

**More practice:**
1. Differentiate `let`, `const` and `var`. (3 marks)
2. Write a program to print the multiplication table of a number entered by the user. (4 marks)
3. Differentiate `while` and `do...while`. (3 marks)
4. What is the DOM? Explain with an example. (5 marks)
5. Explain any four jQuery effects with examples. (4 marks)
6. What is a JavaScript library? Why is jQuery used? (3 marks)
7. Differentiate between an array and an object. (3 marks)
