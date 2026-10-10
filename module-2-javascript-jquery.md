# Module 2: JavaScript and jQuery

**Course:** Web Application Development (MNCST509)
**Programme:** B.Tech CSE Minor, KTU, Semester 5
**Module:** 2 of the syllabus (11 contact hours)

---

## Table of Contents

**Part A: JavaScript**
1. Introduction to Scripting
2. Programming Fundamentals: Variables, Data Types, Operators
3. Obtaining User Input: prompt, alert, confirm
4. Arithmetic
5. Decision Making
6. Control Statements (if/else, switch, loops, break/continue)
7. Functions
8. Arrays
9. Objects
10. Document Object Model (DOM)
11. Form Processing (Validation)

**Part B: jQuery (short version)**
12. What is jQuery? A Basic Example
13. Selecting Elements
14. Getting and Changing Content, Attributes and CSS
15. Inserting New Elements
16. Looping with .each()
17. Events and the Event Object
18. Effects and Animation
19. Traversing the DOM
20. Working with Forms
21. JavaScript Libraries

**Part C: Plain JavaScript vs jQuery**
**Part D: Mini-Projects (Tea Shop Bill in JavaScript, To-do List in jQuery)**
**Part E: Question Bank (KTU style)**

---

## Learning Outcomes

After this module, a student will be able to:

1. Explain what a scripting language is and why web pages need JavaScript.
2. Use variables (`var`, `let`, `const`), data types and operators correctly.
3. Take input from the user with `prompt`, `confirm` and show output with `alert`.
4. Write programs using `if/else`, `switch`, `for`, `while`, `do-while`, `break` and `continue`.
5. Write and call functions; store data in arrays and objects.
6. Use the DOM to read and change a web page from JavaScript.
7. Validate a form before it is submitted.
8. Use jQuery to select elements, change content, attributes and CSS, handle events, and add effects and animations.
9. Traverse the DOM and work with forms using jQuery.
10. Explain what a JavaScript library is and why we use one.

## Suggested Lesson Plan (11 contact hours)

| Session | Time | Topics | Style |
|---|---|---|---|
| 1 | 1 hr | Introduction to scripting, where to put JS, console, variables, data types | Talk + live demo |
| 2 | 1 hr | Operators, arithmetic, prompt/alert/confirm | Demo + 10 min activity |
| 3 | 1 hr | Decision making: if/else, switch | Examples + pair work |
| 4 | 1 hr | Loops, break/continue | Examples + pattern printing |
| 5 | 1 hr | Functions, arrays, objects | Demo + quiz |
| 6 | 1 hr | DOM + events in plain JS | Live coding |
| 7 | 1 hr | Form processing and validation | Lab style |
| 8 | 1 hr | jQuery basics, selectors, content, attributes, CSS | Demo + comparisons |
| 9 | 1 hr | Insert elements, each(), events, event object | Demo + activity |
| 10 | 1 hr | Effects, animation, traversing, forms, libraries | Demo |
| 11 | 1 hr | Mini-project (tea shop bill) + question bank revision | Lab + discussion |

Each one-hour session suggestion: 10 min recap and warm-up, 30 min teaching with live code, 15 min student activity, 5 min check-your-understanding questions.

**How to run the code:** Save any example as `something.html`, then double-click to open in Chrome. Press `F12` to open the Developer Tools, then the Console tab to see `console.log` messages and errors.

---

# PART A: JAVASCRIPT

---

## 1. Introduction to Scripting

### Simple explanation

HTML builds the structure of a page. CSS makes it look good. **JavaScript makes it do things.**

A **script** is a small set of instructions that the browser reads and runs, line by line. A language used for such scripts is a **scripting language**. JavaScript is the scripting language of the web. It runs inside the browser on the user's own computer or phone (this is called **client-side** scripting). No extra software is needed. Every browser already has a JavaScript engine (Chrome has one called V8).

What can JavaScript do on a page?
- Check a form before sending it.
- Show or hide things (menus, popups).
- Change text, images and colours without reloading the page.
- React when the user clicks, types or scrolls.
- Talk to a server in the background (for example, to refresh a score).

Note: Java and JavaScript are two different languages. Their names are similar only because of marketing history.

### Three ways to add JavaScript

1. **Inline** (inside an HTML tag): quick, but messy.
2. **Internal** (inside a `<script>` tag in the same file).
3. **External** (a separate `.js` file linked with `src`). This is the best method for real projects.

### Analogy

Think of a **tea shop**. HTML is the shop's building: counter, shelves, stove. CSS is the paint and the signboard. JavaScript is the **tea master** who actually does things: takes your order, makes the tea, gives the bill. Without him the shop looks good but nothing happens.

### Code example

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>My First Script</title>
</head>
<body>
  <h1>Welcome to Chai Point</h1>
  <p id="msg">This text will change.</p>

  <!-- 1. Inline JavaScript -->
  <button onclick="alert('Inline: Hello!')">Inline click</button>

  <!-- 2. Internal JavaScript -->
  <script>
    console.log("Page loaded");                    // shows in the Console
    document.write("<p>Written by JavaScript</p>"); // writes into the page
    document.getElementById("msg").innerHTML = "Text changed by JavaScript!";
  </script>

  <!-- 3. External JavaScript (needs a file named app.js in the same folder) -->
  <!-- <script src="app.js"></script> -->
</body>
</html>
```

Note: the script is placed at the **end of body** so the elements already exist when the script looks for them.

Comments in JavaScript:

```javascript
// single line comment
/* multi
   line comment */
```

### Real-world example

When you type the wrong OTP on a bank or UPI page and a red message appears instantly without the page reloading, that is JavaScript. Google Maps moving as you drag is JavaScript. The "Add to cart" count going up on Flipkart is JavaScript.

### Common mistakes

- Putting the script in `<head>` and then looking for elements that are not loaded yet.
- Forgetting the closing `</script>`.
- Mixing up Java and JavaScript.
- Not opening the Console, so errors stay hidden.

### Check your understanding

1. What is a scripting language? Name where JavaScript runs.
2. List the three ways of adding JavaScript to an HTML page.
3. Why do we usually keep the `<script>` tag at the end of `<body>`?

---

## 2. Programming Fundamentals: Variables, Data Types, Operators

### 2.1 Variables

A **variable** is a named box that holds a value. You can use the name later to get the value back.

JavaScript gives three keywords to make a variable:

| Keyword | Can change value? | Scope (where it works) | Notes |
|---|---|---|---|
| `var` | Yes | Whole function | Old style. Can be re-declared. Avoid in new code. |
| `let` | Yes | Only inside its `{ }` block | Modern. Use for values that change. |
| `const` | No (cannot be reassigned) | Only inside its `{ }` block | Use for values that never change. |

Rules for names: start with a letter, `_` or `$`; no spaces; case matters (`Total` and `total` are different); cannot use reserved words like `if` or `class`. Style: `camelCase`, for example `totalAmount`.

**Analogy:** A variable is a **steel tiffin box with a label**. `let` is a box where you can change the food. `const` is a **sealed box**: label and food are fixed. `var` is an old box that sometimes leaks outside its shelf (scope problems).

```html
<!DOCTYPE html>
<html>
<body>
<script>
  var oldWay = "I am var";
  let age = 20;              // can change
  const college = "CET";     // cannot change

  age = 21;                  // fine
  // college = "MEC";        // ERROR: Assignment to constant variable

  console.log(oldWay, age, college);

  // Scope difference
  if (true) {
    var a = 1;   // visible outside the block
    let b = 2;   // visible only inside the block
  }
  console.log(a);            // 1
  // console.log(b);         // ERROR: b is not defined
</script>
</body>
</html>
```

### 2.2 Data types

| Type | Example | Meaning |
|---|---|---|
| Number | `42`, `3.14` | Whole and decimal numbers (one type for both) |
| String | `"Kerala"`, `'tea'` | Text |
| Boolean | `true`, `false` | Yes or no |
| Undefined | `let x;` | Variable made but no value given |
| Null | `null` | Value deliberately empty |
| Object | `{name:"Anu"}`, arrays | Collection of values |
| Symbol, BigInt | rare | Not needed for this course |

JavaScript is **dynamically typed**: you do not write the type. The same variable can hold a number now and a string later. Use `typeof` to check the type.

**Analogy:** Think of a **WhatsApp message**. It can be text, a number in the text, a yes/no reaction (thumbs up), or empty (a deleted message: `null`). Messages that are not yet written are `undefined`.

```html
<!DOCTYPE html>
<html>
<body>
<script>
  let price = 15;             // number
  let item = "Chai";          // string
  let isHot = true;           // boolean
  let sugar;                  // undefined
  let discount = null;        // null
  let student = { name: "Anu", roll: 12 };   // object
  let marks = [80, 90, 75];   // array (also an object)

  console.log(typeof price);     // number
  console.log(typeof item);      // string
  console.log(typeof isHot);     // boolean
  console.log(typeof sugar);     // undefined
  console.log(typeof discount);  // object  (a famous old quirk)
  console.log(typeof student);   // object
  console.log(typeof marks);     // object

  // Strings: joining and template literals
  let msg1 = "Order: " + item + " Rs." + price;
  let msg2 = `Order: ${item} Rs.${price}`;    // backticks, easier
  console.log(msg1);
  console.log(msg2);
  console.log(item.length);          // 4
  console.log(item.toUpperCase());   // CHAI
</script>
</body>
</html>
```

### 2.3 Operators

| Group | Operators | Example |
|---|---|---|
| Arithmetic | `+ - * / % **` | `7 % 3` gives 1 |
| Assignment | `= += -= *= /= %=` | `x += 5` means `x = x + 5` |
| Increment/Decrement | `++ --` | `count++` |
| Comparison | `== === != !== > < >= <=` | `5 === "5"` is false |
| Logical | `&&` (and), `\|\|` (or), `!` (not) | `age>=18 && hasId` |
| String | `+` (join) | `"Hi " + "Anu"` |
| Ternary | `cond ? a : b` | `marks>=40 ? "Pass":"Fail"` |

Very important: `==` compares values after changing types (loose). `===` compares value **and** type (strict). Always prefer `===`.

```html
<!DOCTYPE html>
<html>
<body>
<script>
  console.log(5 == "5");    // true  (loose, type ignored)
  console.log(5 === "5");   // false (strict, types differ)
  console.log(5 !== "5");   // true

  let age = 20, hasId = true;
  console.log(age >= 18 && hasId);   // true
  console.log(age < 18 || hasId);    // true
  console.log(!hasId);               // false

  let marks = 52;
  let result = marks >= 40 ? "Pass" : "Fail";
  console.log(result);               // Pass

  let n = 5;
  n++;            // 6
  n += 10;        // 16
  console.log(n);

  console.log("5" + 3);   // "53"  (string joining)
  console.log("5" - 3);   // 2     (converted to number)
</script>
</body>
</html>
```

### Real-world example

On Swiggy, `const deliveryFee = 40;` stays fixed for an order, while `let cartTotal` keeps changing as you add dishes. The check "is the cart total above Rs. 199?" uses a comparison operator, and "is the user logged in AND is the address saved?" uses `&&`.

### Common mistakes

- Using `=` (assign) instead of `===` (compare) inside `if`.
- Expecting `"5" + 3` to be 8.
- Trying to change a `const` value.
- Writing `Let` or `CONST` (keywords are case sensitive).
- Believing `typeof null` is `"null"`.

### Check your understanding

1. Difference between `let`, `const` and `var`?
2. What will `console.log("10" + 5)` and `console.log("10" - 5)` print? Why?
3. Difference between `==` and `===`? Give an example.
4. What is the output of `typeof undefined`?

### Classroom activity: "Predict the output" (5 min)

Show on the board, ask students to guess before running:
`console.log(2 + "2")`, `console.log(2 * "3")`, `console.log(10 % 4)`, `console.log(true + 1)`, `console.log(0 == false)`.
(Answers: `"22"`, `6`, `2`, `2`, `true`.)

---

## 3. Obtaining User Input: prompt, alert, confirm

### Simple explanation

JavaScript has three small built-in popup boxes (called **dialogs**).

| Function | Purpose | Buttons | Returns |
|---|---|---|---|
| `alert(msg)` | Show a message | OK | nothing (`undefined`) |
| `confirm(msg)` | Ask a yes/no question | OK, Cancel | `true` or `false` |
| `prompt(msg, default)` | Ask the user to type something | OK, Cancel, text box | the typed **string**, or `null` if Cancel |

Important: `prompt()` **always returns a string**, even if the user types a number. Convert it using `Number()`, `parseInt()` or `parseFloat()`.

**Analogy:** At a **railway counter**: `alert` is the announcement "Train is 20 minutes late" (you can only listen and say OK). `confirm` is the clerk asking "Cancel the ticket? Yes or No". `prompt` is the clerk asking "What is your name?" and writing down your answer on a form.

### Code example

```html
<!DOCTYPE html>
<html>
<head><meta charset="UTF-8"><title>Dialogs</title></head>
<body>
<h2>Dialog boxes demo</h2>
<script>
  // prompt returns a string (or null on Cancel)
  let name = prompt("Enter your name:", "Student");

  if (name === null || name.trim() === "") {
    alert("You did not enter a name.");
  } else {
    // second input, converted to number
    let ageText = prompt("Enter your age:");
    let age = Number(ageText);

    if (isNaN(age)) {
      alert("Age must be a number!");
    } else {
      let ok = confirm("Hello " + name + ", you are " + age + ". Is this correct?");
      if (ok) {
        alert("Thank you, details saved.");
        document.write("<p>Name: " + name + ", Age: " + age + "</p>");
      } else {
        alert("Okay, please refresh and try again.");
      }
    }
  }
</script>
</body>
</html>
```

### prompt() versus alert()

| Point | `alert()` | `prompt()` |
|---|---|---|
| Purpose | Only shows information | Takes input from user |
| Text box | No | Yes |
| Buttons | OK only | OK and Cancel |
| Return value | `undefined` | String typed by user, or `null` if Cancel |
| Example | `alert("Saved!");` | `let n = prompt("Name?");` |

### Real-world example

Many old sites use `confirm("Are you sure you want to delete?")` before deleting. Modern sites use fancy popups, but they follow the same idea: ask, then act on true or false. `alert` is often used for quick messages like "Form submitted". Real sites rarely use `prompt`, because it looks plain and blocks the page, but it is excellent for learning.

### Common mistakes

- Adding two prompt values directly: `"5" + "3"` gives `"53"`, not 8.
- Not handling `null` when the user presses Cancel (then `null.trim()` crashes).
- Using many alerts, which annoys users.
- Forgetting that these dialogs **stop** the page until closed.

### Check your understanding

1. What does `confirm()` return?
2. User types `25` in a prompt. What is the type of the value you get back?
3. Write code that asks for the user's name and greets them with an alert.
4. What does `prompt()` return when the user clicks Cancel?

---

## 4. Arithmetic

### Simple explanation

JavaScript can do all normal maths. Remember **operator precedence** (order): brackets first, then `**`, then `* / %`, then `+ -`. Use brackets when unsure.

Useful `Math` helpers:

| Code | Result |
|---|---|
| `Math.round(4.6)` | 5 |
| `Math.floor(4.9)` | 4 (round down) |
| `Math.ceil(4.1)` | 5 (round up) |
| `Math.sqrt(25)` | 5 |
| `Math.pow(2,3)` | 8 |
| `Math.max(3,9,5)` | 9 |
| `Math.min(3,9,5)` | 3 |
| `Math.abs(-7)` | 7 |
| `Math.random()` | random number from 0 up to (not including) 1 |
| `(3.14159).toFixed(2)` | `"3.14"` (a string) |

Division by zero gives `Infinity`, not an error. Wrong maths such as `"abc" * 2` gives `NaN` (Not a Number). Test with `isNaN(x)`.

Float surprise: `0.1 + 0.2` gives `0.30000000000000004`. Use `toFixed(2)` for money.

**Analogy:** The JavaScript calculator is like the **UPI/GPay split bill** feature: you give amounts and the number of friends, it does the maths, and you round the result to rupees and paise.

### Code example: simple calculator with prompts

```html
<!DOCTYPE html>
<html>
<head><meta charset="UTF-8"><title>Arithmetic</title></head>
<body>
<script>
  let a = parseFloat(prompt("Enter first number:"));
  let b = parseFloat(prompt("Enter second number:"));

  if (isNaN(a) || isNaN(b)) {
    document.write("Please enter valid numbers.");
  } else {
    document.write("<h3>Results</h3>");
    document.write("Sum: " + (a + b) + "<br>");
    document.write("Difference: " + (a - b) + "<br>");
    document.write("Product: " + (a * b) + "<br>");
    document.write("Quotient: " + (b !== 0 ? (a / b).toFixed(2) : "Cannot divide by zero") + "<br>");
    document.write("Remainder: " + (a % b) + "<br>");
    document.write("a power b: " + Math.pow(a, b) + "<br>");
    document.write("Bigger: " + Math.max(a, b) + "<br>");
  }

  // Split-bill example (GPay style)
  const bill = 1250;
  const friends = 4;
  console.log("Each pays Rs. " + (bill / friends).toFixed(2));  // 312.50

  // Random number between 1 and 6 (dice)
  let dice = Math.floor(Math.random() * 6) + 1;
  console.log("Dice: " + dice);
</script>
</body>
</html>
```

### Real-world example

GST calculation on a bill, EMI calculators on bank sites, "You save Rs. 300 (30% off)" on Flipkart, and the run rate on a cricket scoreboard (`runs / overs`) are all arithmetic in JavaScript.

### Common mistakes

- Forgetting to convert prompt strings to numbers.
- Using `^` for power (it is a different operator). Use `**` or `Math.pow`.
- Showing money without `toFixed(2)`.
- Forgetting that `/` gives decimals (`7/2` is 3.5, not 3).

### Check your understanding

1. What is the result of `2 + 3 * 4`? And `(2 + 3) * 4`?
2. What do `NaN` and `Infinity` mean? When do they appear?
3. Write one line to get a random whole number from 1 to 10.

---

## 5. Decision Making

### Simple explanation

A program must choose between actions. We use **conditions** (things that are true or false). In JavaScript these keywords are `if`, `else if`, `else` and `switch`.

Forms:

```javascript
if (condition) { ... }

if (condition) { ... } else { ... }

if (c1) { ... } else if (c2) { ... } else { ... }

switch (value) {
  case x: ...; break;
  case y: ...; break;
  default: ...;
}
```

Use `switch` when you compare **one value** against many fixed options. Without `break`, execution "falls through" to the next case.

**Falsy values** (treated as false in a condition): `false`, `0`, `""`, `null`, `undefined`, `NaN`. Everything else is truthy.

**Analogy:** **Traffic signal:** red then stop, else if yellow then get ready, else go. And a **tea shop menu board** is like `switch`: you say "2" and the shop picks the 2nd item.

### Code example: grade and menu

```html
<!DOCTYPE html>
<html>
<head><meta charset="UTF-8"><title>Decisions</title></head>
<body>
<script>
  // if / else if / else  (KTU style grade)
  let marks = Number(prompt("Enter marks out of 100:"));
  let grade;

  if (isNaN(marks) || marks < 0 || marks > 100) {
    grade = "Invalid marks";
  } else if (marks >= 90) {
    grade = "S";
  } else if (marks >= 80) {
    grade = "A";
  } else if (marks >= 70) {
    grade = "B";
  } else if (marks >= 50) {
    grade = "C";
  } else if (marks >= 40) {
    grade = "P (Pass)";
  } else {
    grade = "F (Fail)";
  }
  document.write("<p>Grade: " + grade + "</p>");

  // switch: tea shop menu
  let choice = prompt("1 Tea, 2 Coffee, 3 Lemon Tea, 4 Snack");
  let item, cost;

  switch (choice) {
    case "1":
      item = "Tea"; cost = 10;
      break;
    case "2":
      item = "Coffee"; cost = 15;
      break;
    case "3":
      item = "Lemon Tea"; cost = 12;
      break;
    case "4":
      item = "Snack"; cost = 20;
      break;
    default:
      item = "Unknown"; cost = 0;
  }
  document.write("<p>" + item + " costs Rs. " + cost + "</p>");

  // Leap year with logical operators
  let year = 2024;
  if ((year % 4 === 0 && year % 100 !== 0) || year % 400 === 0) {
    console.log(year + " is a leap year");
  }
</script>
</body>
</html>
```

### Real-world example

IRCTC: "if the seat is available, show Book Now; else if RAC, show RAC; else show Waitlist". Swiggy: "if the cart is above Rs. 199 then free delivery else charge Rs. 40". A college result page decides Pass or Fail the same way as the grade code above.

### Common mistakes

- `if (x = 5)` instead of `if (x === 5)`.
- Forgetting `break` in `switch`.
- Putting a semicolon right after `if (...)`; that ends the `if` early.
- In `switch`, comparing a string `"1"` with a number `1` (switch uses strict comparison).

### Check your understanding

1. When would you use `switch` instead of `if-else if`?
2. What happens if you forget `break` in a case?
3. Write a condition that is true only if a number is between 10 and 20 (both included).
4. Name four falsy values.

---

## 6. Control Statements (Loops, break, continue)

### Simple explanation

A **loop** repeats a block of code. Use loops when you must do the same job many times.

| Loop | Use when | Syntax |
|---|---|---|
| `for` | You know how many times | `for (init; condition; update) { }` |
| `while` | You repeat while a condition is true; condition checked **first** | `while (cond) { }` |
| `do-while` | Run at least once; condition checked **after** | `do { } while (cond);` |

- `break` stops the loop immediately.
- `continue` skips the rest of this round and goes to the next round.

**Analogy:** A **tea master pouring cups**: `for` is "pour exactly 10 cups". `while` is "keep pouring while customers are waiting". `do-while` is "pour one cup first, then check whether anyone else wants one". `break` is "shop closed, stop now". `continue` is "this customer wants no sugar, skip the sugar step and move on".

### Code example

```html
<!DOCTYPE html>
<html>
<head><meta charset="UTF-8"><title>Loops</title></head>
<body>
<script>
  // for: table of 5
  document.write("<h3>Table of 5</h3>");
  for (let i = 1; i <= 10; i++) {
    document.write("5 x " + i + " = " + (5 * i) + "<br>");
  }

  // while: sum of digits
  let n = 4821, sum = 0;
  while (n > 0) {
    sum += n % 10;          // last digit
    n = Math.floor(n / 10); // remove last digit
  }
  document.write("<p>Sum of digits of 4821 = " + sum + "</p>");

  // do-while: runs at least once (password retry)
  let pass;
  do {
    pass = prompt("Enter the secret word (hint: kerala):");
  } while (pass !== "kerala" && pass !== null);
  document.write("<p>Loop finished.</p>");

  // break: stop at first number divisible by 7
  for (let i = 1; i <= 100; i++) {
    if (i % 7 === 0) {
      document.write("<p>First multiple of 7 is " + i + "</p>");
      break;
    }
  }

  // continue: print odd numbers only
  document.write("Odd numbers: ");
  for (let i = 1; i <= 10; i++) {
    if (i % 2 === 0) continue;   // skip even
    document.write(i + " ");
  }

  // Nested loop: star triangle
  document.write("<pre>");
  for (let r = 1; r <= 4; r++) {
    let line = "";
    for (let c = 1; c <= r; c++) line += "* ";
    document.write(line + "\n");
  }
  document.write("</pre>");
</script>
</body>
</html>
```

### Real-world example

Zomato listing 20 restaurants uses a loop to make one card per restaurant. A cricket scoreboard loops over 11 batsmen to print each row. WhatsApp loops over messages to show them on screen.

### Common mistakes

- **Infinite loop**: forgetting `i++` in `while`, so the condition never becomes false (the browser tab hangs).
- Off by one: using `<` when you meant `<=`.
- Using `let` outside the loop and expecting the counter to stay unchanged.
- Using `continue` before the update step in a `while` loop (skips `i++` and loops forever).

### Check your understanding

1. Difference between `while` and `do-while`?
2. What is the output of: `for (let i=1;i<=5;i++){ if(i===3) continue; console.log(i); }`?
3. Same loop but with `break` instead of `continue`?
4. Write a loop to print numbers 10 down to 1.

### Classroom activity: "Fizz Buzz" (10 min)

Print 1 to 30. For multiples of 3 print `Fizz`, multiples of 5 print `Buzz`, multiples of both print `FizzBuzz`. Sample answer:

```javascript
for (let i = 1; i <= 30; i++) {
  if (i % 15 === 0) console.log("FizzBuzz");
  else if (i % 3 === 0) console.log("Fizz");
  else if (i % 5 === 0) console.log("Buzz");
  else console.log(i);
}
```

---

## 7. Functions

### Simple explanation

A **function** is a named block of code you write once and use many times. It can take **parameters** (inputs) and give back a result with `return`.

Ways to write a function:

```javascript
// 1. Function declaration
function add(a, b) { return a + b; }

// 2. Function expression
const sub = function (a, b) { return a - b; };

// 3. Arrow function (short, modern)
const mul = (a, b) => a * b;
```

Points to know:
- If there is no `return`, the function gives back `undefined`.
- Variables made inside a function are **local** (not visible outside).
- Functions can have **default values**: `function greet(name = "Guest")`.
- Functions can be passed to other functions (as in event handlers and `setTimeout`). This is called a **callback**.

**Analogy:** A function is a **recipe card for masala chai**. You write the recipe once. Each time a customer comes, you follow the same card with different input (ginger or no ginger) and get a cup as output.

### Code example

```html
<!DOCTYPE html>
<html>
<head><meta charset="UTF-8"><title>Functions</title></head>
<body>
<p id="out"></p>
<script>
  // function with parameters and return
  function calculateBill(price, qty) {
    return price * qty;
  }

  // default parameter
  function greet(name = "Guest") {
    return "Welcome, " + name + "!";
  }

  // arrow function
  const gst = (amount) => amount * 0.05;

  // function that calls another function
  function finalAmount(price, qty) {
    let subtotal = calculateBill(price, qty);
    return subtotal + gst(subtotal);
  }

  // function with no return (just does something)
  function showMessage(text) {
    document.getElementById("out").innerHTML = text;
  }

  console.log(greet());              // Welcome, Guest!
  console.log(greet("Anu"));         // Welcome, Anu!
  console.log(calculateBill(10, 3)); // 30
  showMessage("Total with GST: Rs. " + finalAmount(10, 3).toFixed(2)); // 31.50

  // callback: function passed to another function
  setTimeout(function () {
    console.log("This ran after 2 seconds");
  }, 2000);

  // local vs global scope
  let shopName = "Chai Point";        // global
  function test() {
    let secret = 123;                 // local
    console.log(shopName, secret);
  }
  test();
  // console.log(secret);  // ERROR: secret is not defined
</script>
</body>
</html>
```

### Real-world example

A "calculate delivery charge" function on Swiggy is used on every cart page. A `validateEmail()` function is reused on login, signup and contact forms. Libraries like jQuery are just a big collection of ready-made functions.

### Common mistakes

- Defining a function but never calling it (forgetting the `()`).
- Writing `return` and then putting code after it (never runs).
- Forgetting `return` and getting `undefined`.
- Writing `onclick="myFunc"` instead of `onclick="myFunc()"`.
- Using a variable defined inside a function from outside.

### Check your understanding

1. What is the difference between a parameter and an argument?
2. What does a function return if there is no `return` statement?
3. Write an arrow function that returns the square of a number.
4. What is a callback function? Give one example.

---

## 8. Arrays

### Simple explanation

An **array** is an ordered list of values stored in one variable. Each item has a numbered position called an **index**, starting from **0**.

```javascript
let fruits = ["apple", "mango", "banana"];
fruits[0]      // "apple"
fruits.length  // 3
```

Common array methods:

| Method | What it does |
|---|---|
| `push(x)` | Add at end |
| `pop()` | Remove from end |
| `unshift(x)` | Add at start |
| `shift()` | Remove from start |
| `indexOf(x)` | Position of x, or -1 if not found |
| `includes(x)` | true/false |
| `slice(a,b)` | Copy a part (does not change original) |
| `splice(i,n)` | Remove n items from position i (changes original) |
| `join(",")` | Make a string |
| `sort()` | Sort (text order by default) |
| `reverse()` | Reverse order |
| `forEach(fn)` | Run fn on each item |
| `map(fn)` | Make a new array by changing each item |
| `filter(fn)` | Make a new array with items that pass a test |
| `reduce(fn, start)` | Combine all items into one value |

**Analogy:** An array is a **railway train**. Coaches are numbered from 0 (engine side). Each coach holds one thing. You can attach a coach at the end (`push`), detach one (`pop`), or ask "which coach has the pantry?" (`indexOf`).

### Code example

```html
<!DOCTYPE html>
<html>
<head><meta charset="UTF-8"><title>Arrays</title></head>
<body>
<ul id="list"></ul>
<p id="result"></p>
<script>
  let menu = ["Tea", "Coffee", "Samosa"];
  menu.push("Vada");            // add at end
  menu.unshift("Lemon Tea");    // add at start
  menu.pop();                   // remove "Vada"
  console.log(menu);            // ["Lemon Tea","Tea","Coffee","Samosa"]
  console.log(menu.length);     // 4
  console.log(menu.indexOf("Coffee")); // 2
  console.log(menu.includes("Pizza")); // false

  // loop over array: classic for
  for (let i = 0; i < menu.length; i++) {
    console.log(i + ": " + menu[i]);
  }

  // forEach: show on page
  let list = document.getElementById("list");
  menu.forEach(function (item) {
    list.innerHTML += "<li>" + item + "</li>";
  });

  // numbers: map, filter, reduce
  let prices = [10, 15, 20, 12];
  let withGst = prices.map(p => p * 1.05);          // new array
  let costly = prices.filter(p => p >= 15);         // [15, 20]
  let total = prices.reduce((sum, p) => sum + p, 0); // 57
  document.getElementById("result").innerHTML =
    "Total: Rs. " + total + " | Costly items: " + costly.join(", ");

  // sort numbers correctly
  let scores = [45, 9, 100, 23];
  scores.sort((a, b) => a - b);
  console.log(scores);   // [9, 23, 45, 100]

  // 2D array (rows and columns)
  let marks = [[80, 70], [60, 90]];
  console.log(marks[1][1]);   // 90
</script>
</body>
</html>
```

### Real-world example

The list of restaurants on Zomato, products on a Flipkart search page, your WhatsApp chats, and the 11 players in a team are all arrays. "Sort by price: low to high" is `sort()`. "Show only veg" is `filter()`. "Cart total" is `reduce()`.

### Common mistakes

- Thinking the first index is 1 (it is 0).
- Reading `arr[arr.length]` (this is beyond the end; the last is `arr[arr.length - 1]`).
- Using `sort()` on numbers without a compare function (`[100, 9]` sorts as `[100, 9]` because it sorts as text).
- Confusing `slice` (copy) with `splice` (changes original).

### Check your understanding

1. What is the index of the last item in an array of 8 items?
2. What does `push()` do, and what does `pop()` do?
3. Write code to find the sum of numbers in `[4, 8, 15]` using a loop.
4. What is the difference between `map()` and `filter()`?

---

## 9. Objects

### Simple explanation

An **object** stores related data as **key: value pairs** (called properties). A function stored inside an object is called a **method**. Arrays use number positions; objects use names.

```javascript
let student = {
  name: "Anu",
  roll: 12,
  marks: [80, 90],
  greet: function () { return "Hi, I am " + this.name; }
};
student.name        // dot notation
student["roll"]     // bracket notation
```

`this` inside a method means "the object that owns this method".

Useful things: add a property (`student.city = "Kochi"`), delete (`delete student.roll`), check (`"name" in student`), loop over keys (`for (let key in student)`), and **JSON** (`JSON.stringify(obj)` to make text, `JSON.parse(text)` to get the object back). JSON is the standard format to send data between browser and server.

An array of objects is the most common structure on real websites.

**Analogy:** An object is a **college ID card**. Fields: name, roll number, branch, blood group. You ask for a field by its label. A method is something the card holder can do, such as "introduce yourself".

### Code example

```html
<!DOCTYPE html>
<html>
<head><meta charset="UTF-8"><title>Objects</title></head>
<body>
<div id="board"></div>
<script>
  // object with properties and a method
  let batsman = {
    name: "Virat",
    runs: 82,
    balls: 53,
    strikeRate: function () {
      return ((this.runs / this.balls) * 100).toFixed(1);
    }
  };

  console.log(batsman.name);           // Virat
  console.log(batsman["runs"]);        // 82
  console.log(batsman.strikeRate());   // 154.7
  batsman.fours = 7;                   // add property
  batsman.runs = 90;                   // change property

  // loop over keys
  for (let key in batsman) {
    if (typeof batsman[key] !== "function") {
      console.log(key + " = " + batsman[key]);
    }
  }

  // array of objects: scoreboard
  let team = [
    { name: "Rohit", runs: 45, balls: 30 },
    { name: "Gill",  runs: 63, balls: 41 },
    { name: "Kohli", runs: 82, balls: 53 }
  ];

  let html = "<table border='1' cellpadding='6'><tr><th>Player</th><th>Runs</th><th>Balls</th></tr>";
  let totalRuns = 0;
  team.forEach(function (p) {
    html += "<tr><td>" + p.name + "</td><td>" + p.runs + "</td><td>" + p.balls + "</td></tr>";
    totalRuns += p.runs;
  });
  html += "</table><p>Team total: " + totalRuns + "</p>";
  document.getElementById("board").innerHTML = html;

  // JSON
  let text = JSON.stringify(team[0]);
  console.log(text);                   // {"name":"Rohit","runs":45,"balls":30}
  let back = JSON.parse(text);
  console.log(back.runs);              // 45
</script>
</body>
</html>
```

### Real-world example

A single Swiggy restaurant is an object: `{name, rating, cuisines, deliveryTime}`. The home page gets an array of such objects from the server (as JSON) and shows a card for each. Your logged-in profile, a Flipkart product and an IRCTC train entry are all objects.

### Common mistakes

- Using `student.name` when the key is stored in a variable (use `student[key]`).
- Forgetting commas between properties.
- Using an arrow function as a method and expecting `this` to work.
- Writing JSON with single quotes (JSON needs double quotes).

### Check your understanding

1. How are objects different from arrays?
2. How do you add a new property `city` to an existing object `student`?
3. What is a method? What does `this` mean inside it?
4. Create an object for a Flipkart product with name, price and a method that gives the price after 10 percent discount.

---

## 10. Document Object Model (DOM)

### Simple explanation

When the browser loads an HTML page, it builds a **tree of objects** in memory. This tree is the **DOM**. Every tag, every piece of text and every attribute becomes a **node** in the tree. JavaScript can read and change this tree, and the page changes on screen immediately.

The top is `document`, then `html`, with `head` and `body` as children, and so on.

Finding elements:

| Method | Returns |
|---|---|
| `document.getElementById("id")` | One element |
| `document.getElementsByClassName("c")` | List of elements |
| `document.getElementsByTagName("p")` | List of elements |
| `document.querySelector("css")` | First match (any CSS selector) |
| `document.querySelectorAll("css")` | All matches |

Changing things:

| Task | Code |
|---|---|
| Change HTML inside | `el.innerHTML = "<b>Hi</b>"` |
| Change plain text | `el.textContent = "Hi"` |
| Change attribute | `el.setAttribute("src","a.png")` or `el.src = "a.png"` |
| Change style | `el.style.color = "red"` |
| Add/remove class | `el.classList.add("x")`, `.remove("x")`, `.toggle("x")` |
| Create element | `document.createElement("li")` |
| Add into page | `parent.appendChild(child)` |
| Remove | `el.remove()` |

**Events** tell us when something happens. Attach with `addEventListener("click", function)`. Common events: `click`, `dblclick`, `mouseover`, `mouseout`, `keyup`, `change`, `submit`, `load`.

**Analogy:** The DOM is the **family tree of a joint family** on a wedding invitation. You can point to any person (element) by name or relation, change their details, add a new baby, or remove someone from the chart. The printed invitation (page) updates as you edit.

### Code example

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>DOM demo</title>
  <style>
    .highlight { background: yellow; }
    li { margin: 4px 0; }
  </style>
</head>
<body>
  <h2 id="title">Today's Specials</h2>
  <ul id="menu">
    <li class="item">Masala Dosa</li>
    <li class="item">Idli</li>
  </ul>

  <input type="text" id="newItem" placeholder="New dish">
  <button id="addBtn">Add</button>
  <button id="colorBtn">Toggle highlight</button>
  <button id="removeBtn">Remove last</button>

  <script>
    const title = document.getElementById("title");
    const menu = document.getElementById("menu");
    const input = document.getElementById("newItem");

    // change text and style
    title.textContent = "Today's Specials (Kochi Branch)";
    title.style.color = "darkgreen";

    // create and add an element
    document.getElementById("addBtn").addEventListener("click", function () {
      let text = input.value.trim();
      if (text === "") {
        alert("Please type a dish name");
        return;
      }
      let li = document.createElement("li");
      li.className = "item";
      li.textContent = text;
      menu.appendChild(li);
      input.value = "";
      input.focus();
    });

    // class toggle on all items
    document.getElementById("colorBtn").addEventListener("click", function () {
      let items = document.querySelectorAll(".item");
      items.forEach(function (li) {
        li.classList.toggle("highlight");
      });
    });

    // remove last item
    document.getElementById("removeBtn").addEventListener("click", function () {
      let last = menu.lastElementChild;
      if (last) last.remove();
    });

    // hover event on the title
    title.addEventListener("mouseover", function () { title.style.color = "red"; });
    title.addEventListener("mouseout", function () { title.style.color = "darkgreen"; });
  </script>
</body>
</html>
```

### Real-world example

Every time Flipkart updates the cart count without reloading, Zomato adds a dish into your cart panel, or WhatsApp Web shows a new message bubble, JavaScript is creating or changing DOM nodes.

### Common mistakes

- Running the script before the element exists (script in head without waiting).
- Using `getElementsByClassName(...)` and treating it as one element (it is a list).
- Using `innerHTML` with text typed by users (security risk: script injection). Prefer `textContent` for user text.
- Wrong id spelling or using `#` in `getElementById("#title")`.

### Check your understanding

1. What is the DOM? Why is it described as a tree?
2. Difference between `innerHTML` and `textContent`?
3. Write code to change the text of a paragraph with id `info` to "Hello".
4. Name any four events.

### Classroom activity: "Live colour changer" (10 min)

Ask students to make three buttons (Red, Green, Blue) that change the page background using `document.body.style.backgroundColor`.

---

## 11. Form Processing (Validation)

### Simple explanation

**Form validation** means checking what the user typed **before** it goes to the server. It saves time and gives instant feedback, for example "Email is not valid".

How JavaScript handles it:
1. Listen for the form's `submit` event (or button click).
2. Read each field's value (`input.value`).
3. Test the value (empty? right length? matches a pattern?).
4. If wrong: show an error message and stop the submission with `event.preventDefault()` (or `return false` in `onsubmit`).
5. If right: allow the form to go.

Common checks: required field, minimum length, only digits (phone), email format, password match, age range, checkbox ticked.

**Regular expression (regex)** is a pattern to match text. Example: a 10-digit Indian mobile number starting with 6-9: `/^[6-9]\d{9}$/`. Use `pattern.test(value)`.

HTML5 also has built-in validation (`required`, `minlength`, `type="email"`), but JavaScript gives full control and custom messages. Important: **client-side validation is only for user comfort. A server must always validate again** because anyone can bypass the browser checks.

**Analogy:** Validation is the **security guard at a college gate** checking the ID card. He checks quickly at the gate (JavaScript, fast, saves trouble). But the office inside also checks again (server), because a fake ID could get past a sleepy guard.

### Code example: registration form

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Form Validation</title>
  <style>
    body { font-family: Arial; margin: 30px; }
    .row { margin-bottom: 12px; }
    label { display: inline-block; width: 140px; }
    .error { color: red; font-size: 13px; margin-left: 140px; }
    .ok { color: green; font-weight: bold; }
  </style>
</head>
<body>
  <h2>Student Registration</h2>
  <form id="regForm" novalidate>
    <div class="row">
      <label for="fullname">Full name</label>
      <input type="text" id="fullname">
      <div class="error" id="nameErr"></div>
    </div>
    <div class="row">
      <label for="email">Email</label>
      <input type="text" id="email">
      <div class="error" id="emailErr"></div>
    </div>
    <div class="row">
      <label for="phone">Mobile</label>
      <input type="text" id="phone" maxlength="10">
      <div class="error" id="phoneErr"></div>
    </div>
    <div class="row">
      <label for="pass">Password</label>
      <input type="password" id="pass">
      <div class="error" id="passErr"></div>
    </div>
    <div class="row">
      <label for="pass2">Confirm password</label>
      <input type="password" id="pass2">
      <div class="error" id="pass2Err"></div>
    </div>
    <div class="row">
      <input type="checkbox" id="agree"> <label for="agree" style="width:auto">I agree to the rules</label>
      <div class="error" id="agreeErr"></div>
    </div>
    <button type="submit">Register</button>
    <p id="status"></p>
  </form>

  <script>
    document.getElementById("regForm").addEventListener("submit", function (event) {
      let valid = true;

      // helper: show or clear message
      function setError(id, message) {
        document.getElementById(id).textContent = message;
        if (message !== "") valid = false;
      }

      let name = document.getElementById("fullname").value.trim();
      let email = document.getElementById("email").value.trim();
      let phone = document.getElementById("phone").value.trim();
      let pass = document.getElementById("pass").value;
      let pass2 = document.getElementById("pass2").value;
      let agree = document.getElementById("agree").checked;

      // 1. empty check
      setError("nameErr", name === "" ? "Name cannot be empty" : "");

      // 2. email pattern
      let emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      setError("emailErr", emailPattern.test(email) ? "" : "Enter a valid email");

      // 3. Indian mobile: 10 digits, starts with 6-9
      setError("phoneErr", /^[6-9]\d{9}$/.test(phone) ? "" : "Enter a valid 10-digit mobile number");

      // 4. password length
      setError("passErr", pass.length >= 6 ? "" : "Password must be at least 6 characters");

      // 5. confirm password
      setError("pass2Err", pass === pass2 ? "" : "Passwords do not match");

      // 6. checkbox
      setError("agreeErr", agree ? "" : "You must accept the rules");

      if (!valid) {
        event.preventDefault();     // stop the form from being submitted
        document.getElementById("status").textContent = "";
      } else {
        event.preventDefault();     // for this demo we also stay on the page
        document.getElementById("status").innerHTML = "<span class='ok'>Form is valid. Ready to send!</span>";
      }
    });
  </script>
</body>
</html>
```

### Short answer: check an empty text field on submit

```html
<!DOCTYPE html>
<html>
<body>
  <form onsubmit="return checkEmpty()">
    Name: <input type="text" id="uname">
    <input type="submit" value="Submit">
  </form>
  <script>
    function checkEmpty() {
      let v = document.getElementById("uname").value.trim();
      if (v === "") {
        alert("Name field cannot be empty");
        return false;     // blocks submission
      }
      return true;        // allows submission
    }
  </script>
</body>
</html>
```

### Real-world example

IRCTC signup (username availability, password rules), UPI apps checking that the amount is not zero and the UPI ID has the `@` format, and every college admission form with "required" fields.

### Common mistakes

- Forgetting `preventDefault()` or `return false`, so the bad form still goes.
- Using `.value` without `.trim()` (a field with only spaces looks non-empty).
- Writing `onsubmit="checkEmpty()"` instead of `onsubmit="return checkEmpty()"`.
- Trusting only client-side validation.
- Reading a checkbox with `.value` instead of `.checked`.

### Check your understanding

1. Why is validation done on the client side? Why is it not enough on its own?
2. How do you stop a form from submitting using JavaScript?
3. Write a regex-based check for a 6-digit PIN code.
4. How do you check that two password fields match?

---

# PART B: jQUERY (SHORT VERSION)

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

# PART C: PLAIN JAVASCRIPT vs jQUERY (SIDE BY SIDE)

Both do the same job. jQuery is shorter; plain JavaScript needs no extra file and is now quite good too.

| Task | Plain JavaScript | jQuery |
|---|---|---|
| Wait for page | `document.addEventListener("DOMContentLoaded", fn)` | `$(fn)` |
| Select by id | `document.getElementById("a")` | `$("#a")` |
| Select all by class | `document.querySelectorAll(".c")` | `$(".c")` |
| Change text | `el.textContent = "Hi"` | `$("#a").text("Hi")` |
| Change HTML | `el.innerHTML = "<b>Hi</b>"` | `$("#a").html("<b>Hi</b>")` |
| Read input | `el.value` | `$("#a").val()` |
| Hide | `el.style.display = "none"` | `$("#a").hide()` |
| Set style | `el.style.color = "red"` | `$("#a").css("color","red")` |
| Add class | `el.classList.add("x")` | `$("#a").addClass("x")` |
| Get attribute | `el.getAttribute("href")` | `$("a").attr("href")` |
| Click event | `el.addEventListener("click", fn)` | `$("#a").click(fn)` |
| Add child | `el.appendChild(child)` | `$("#a").append(child)` |
| Loop over elements | `list.forEach(fn)` | `$(".c").each(fn)` |
| Fade out | needs CSS or timers | `$("#a").fadeOut()` |

### Example 1: hide a paragraph on button click

Plain JavaScript:

```html
<!DOCTYPE html>
<html>
<body>
  <p id="para">Hide me!</p>
  <button id="btn">Hide</button>
  <script>
    document.getElementById("btn").addEventListener("click", function () {
      document.getElementById("para").style.display = "none";
    });
  </script>
</body>
</html>
```

jQuery:

```html
<!DOCTYPE html>
<html>
<head><script src="https://code.jquery.com/jquery-3.7.1.min.js"></script></head>
<body>
  <p id="para">Hide me!</p>
  <button id="btn">Hide</button>
  <script>
    $(function () {
      $("#btn").click(function () { $("#para").hide(); });
    });
  </script>
</body>
</html>
```

### Example 2: change colour of all paragraphs

Plain JavaScript (needs a loop):

```javascript
document.querySelectorAll("p").forEach(function (p) {
  p.style.color = "blue";
});
```

jQuery (no loop needed, it acts on all):

```javascript
$("p").css("color", "blue");
```

### Example 3: add a new list item

Plain JavaScript:

```javascript
let li = document.createElement("li");
li.textContent = "Vada";
document.getElementById("menu").appendChild(li);
```

jQuery:

```javascript
$("#menu").append($("<li></li>").text("Vada"));
```

### Example 4: toggle with fade, using classes

Plain JavaScript:

```javascript
document.getElementById("btn").addEventListener("click", function () {
  document.getElementById("box").classList.toggle("hidden");   // CSS handles the fade
});
```

jQuery:

```javascript
$("#btn").click(function () { $("#box").fadeToggle(); });
```

### Discussion for the class

- jQuery is shorter and hides browser differences (a big help in the old days).
- Modern plain JavaScript (`querySelector`, `classList`, `fetch`) does much of what jQuery was needed for.
- jQuery is still common in old projects, WordPress, and many portals, so you must be able to read and write it.

---

# PART D: MINI-PROJECT: TEA SHOP BILL CALCULATOR

**Goal:** a page where the user enters the customer name, picks items and quantities, and gets a bill with GST. It has form validation. We build it in **plain JavaScript**. Version 2 is a short **jQuery** to-do list for practising selectors, events and effects.

**Features:**
1. Customer name and mobile number (validated).
2. Choose items from a dropdown with price and enter quantity.
3. Add items to a bill table (array of objects).
4. Show subtotal, 5 percent GST and grand total.
5. Remove an item. Clear bill.
6. Messages for wrong input.

**Concepts used:** variables, arrays, objects, functions, loops, DOM, events, validation, `toFixed`.

## Version 1: Plain JavaScript

Save as `teashop-js.html`.

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Chai Corner Bill (JavaScript)</title>
  <style>
    body { font-family: Arial, sans-serif; background: #fff8ec; margin: 0; padding: 20px; }
    .wrap { max-width: 640px; margin: auto; background: white; padding: 20px;
            border-radius: 10px; box-shadow: 0 2px 8px #ccc; }
    h1 { color: #8a4b08; text-align: center; margin-top: 0; }
    .row { margin: 10px 0; }
    label { display: inline-block; width: 120px; }
    input, select { padding: 6px; }
    button { padding: 7px 14px; cursor: pointer; background: #8a4b08; color: white; border: none; border-radius: 4px; }
    button.small { padding: 3px 8px; background: #b22; }
    .error { color: red; font-size: 13px; margin-left: 120px; min-height: 16px; }
    table { width: 100%; border-collapse: collapse; margin-top: 15px; }
    th, td { border: 1px solid #ddd; padding: 6px; text-align: center; }
    th { background: #f3e0c2; }
    .total td { font-weight: bold; }
  </style>
</head>
<body>
  <div class="wrap">
    <h1>Chai Corner</h1>

    <div class="row">
      <label for="cname">Customer</label>
      <input type="text" id="cname" placeholder="Name">
    </div>
    <div class="error" id="errName"></div>

    <div class="row">
      <label for="mobile">Mobile</label>
      <input type="text" id="mobile" maxlength="10" placeholder="10 digits">
    </div>
    <div class="error" id="errMobile"></div>

    <div class="row">
      <label for="item">Item</label>
      <select id="item">
        <option value="">-- choose --</option>
        <option value="Tea|10">Tea - Rs. 10</option>
        <option value="Coffee|15">Coffee - Rs. 15</option>
        <option value="Lemon Tea|12">Lemon Tea - Rs. 12</option>
        <option value="Samosa|20">Samosa - Rs. 20</option>
        <option value="Vada|12">Vada - Rs. 12</option>
      </select>
    </div>
    <div class="error" id="errItem"></div>

    <div class="row">
      <label for="qty">Quantity</label>
      <input type="number" id="qty" value="1" min="1" style="width:70px">
      <button id="addBtn">Add to bill</button>
      <button id="clearBtn" style="background:#555">Clear</button>
    </div>
    <div class="error" id="errQty"></div>

    <table id="billTable">
      <thead>
        <tr><th>Item</th><th>Price</th><th>Qty</th><th>Amount</th><th></th></tr>
      </thead>
      <tbody id="billBody"></tbody>
      <tfoot id="billFoot"></tfoot>
    </table>
    <p id="msg"></p>
  </div>

  <script>
    // ---------- Data ----------
    const GST_RATE = 0.05;
    let bill = [];     // array of objects: {name, price, qty}

    // ---------- Helper functions ----------
    function setError(id, text) {
      document.getElementById(id).textContent = text;
      return text === "";           // true if no error
    }

    function validateCustomer() {
      let name = document.getElementById("cname").value.trim();
      let mobile = document.getElementById("mobile").value.trim();
      let ok1 = setError("errName", name === "" ? "Please enter customer name" : "");
      let ok2 = setError("errMobile", /^[6-9]\d{9}$/.test(mobile) ? "" : "Enter a valid 10-digit mobile number");
      return ok1 && ok2;
    }

    function validateItem() {
      let item = document.getElementById("item").value;
      let qty = Number(document.getElementById("qty").value);
      let ok1 = setError("errItem", item === "" ? "Please choose an item" : "");
      let ok2 = setError("errQty",
        (Number.isInteger(qty) && qty >= 1 && qty <= 50) ? "" : "Quantity must be a whole number from 1 to 50");
      return ok1 && ok2;
    }

    function calculateTotals() {
      let subtotal = 0;
      for (let i = 0; i < bill.length; i++) {
        subtotal += bill[i].price * bill[i].qty;
      }
      let gst = subtotal * GST_RATE;
      return { subtotal: subtotal, gst: gst, grand: subtotal + gst };
    }

    function render() {
      let body = document.getElementById("billBody");
      let foot = document.getElementById("billFoot");
      body.innerHTML = "";
      foot.innerHTML = "";

      bill.forEach(function (line, index) {
        let tr = document.createElement("tr");
        tr.innerHTML =
          "<td>" + line.name + "</td>" +
          "<td>" + line.price + "</td>" +
          "<td>" + line.qty + "</td>" +
          "<td>" + (line.price * line.qty).toFixed(2) + "</td>" +
          "<td><button class='small' data-index='" + index + "'>X</button></td>";
        body.appendChild(tr);
      });

      if (bill.length > 0) {
        let t = calculateTotals();
        foot.innerHTML =
          "<tr class='total'><td colspan='3'>Subtotal</td><td colspan='2'>Rs. " + t.subtotal.toFixed(2) + "</td></tr>" +
          "<tr class='total'><td colspan='3'>GST (5%)</td><td colspan='2'>Rs. " + t.gst.toFixed(2) + "</td></tr>" +
          "<tr class='total'><td colspan='3'>Grand Total</td><td colspan='2'>Rs. " + t.grand.toFixed(2) + "</td></tr>";
      }
    }

    // ---------- Events ----------
    document.getElementById("addBtn").addEventListener("click", function () {
      let customerOk = validateCustomer();
      let itemOk = validateItem();
      if (!(customerOk && itemOk)) {
        document.getElementById("msg").textContent = "Please fix the errors above.";
        return;
      }
      document.getElementById("msg").textContent = "";

      let parts = document.getElementById("item").value.split("|");  // ["Tea","10"]
      let name = parts[0];
      let price = Number(parts[1]);
      let qty = Number(document.getElementById("qty").value);

      // if item already in bill, increase qty
      let existing = bill.find(function (l) { return l.name === name; });
      if (existing) {
        existing.qty += qty;
      } else {
        bill.push({ name: name, price: price, qty: qty });
      }
      document.getElementById("qty").value = 1;
      document.getElementById("item").value = "";
      render();
    });

    // delegation: one listener for all remove buttons
    document.getElementById("billBody").addEventListener("click", function (event) {
      if (event.target.tagName === "BUTTON") {
        let index = Number(event.target.getAttribute("data-index"));
        bill.splice(index, 1);
        render();
      }
    });

    document.getElementById("clearBtn").addEventListener("click", function () {
      if (bill.length === 0) { alert("The bill is already empty."); return; }
      if (confirm("Clear the whole bill?")) {
        bill = [];
        render();
      }
    });

    render();
  </script>
</body>
</html>
```

**Test cases to give students:**
1. Press Add with everything empty: errors appear.
2. Mobile `12345`: error. Mobile `9876543210`: accepted.
3. 2 Tea + 1 Samosa: subtotal 40, GST 2.00, total 42.00.
4. Add Tea again: quantity increases, no new row.
5. Quantity `0` or `2.5`: error.

## Version 2: jQuery To-do List (short)

Save as `todo-jquery.html`.

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>To-do list</title>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <style>
    body { font-family: Arial; margin: 30px; }
    li { cursor: pointer; margin: 5px 0; }
    li.done { text-decoration: line-through; color: gray; }
    .err { color: red; }
  </style>
</head>
<body>
  <h2>My Study To-do</h2>
  <input type="text" id="task" placeholder="e.g. Finish Module 2">
  <button id="add">Add</button>
  <span class="err" id="err"></span>
  <ul id="list"></ul>
  <p><span id="left">0</span> tasks left. <button id="clean">Remove done tasks</button></p>

  <script>
    $(function () {
      function updateCount() { $("#left").text($("#list li:not(.done)").length); }

      function addTask() {
        let text = $("#task").val().trim();
        if (text === "") { $("#err").text("Task cannot be empty"); return; }
        $("#err").text("");
        $("<li></li>").text(text).hide().appendTo("#list").slideDown(200);
        $("#task").val("").focus();
        updateCount();
      }

      $("#add").click(addTask);
      $("#task").on("keyup", function (e) { if (e.key === "Enter") addTask(); });

      $("#list").on("click", "li", function () {
        $(this).toggleClass("done");
        updateCount();
      });
      $("#clean").click(function () {
        $("#list li.done").slideUp(200, function () { $(this).remove(); });
        // count updates after removal; done items are already excluded
      });
    });
  </script>
</body>
</html>
```

---

# CLASSROOM ACTIVITIES (QUICK COLLECTION)

1. **Console detective (5 min):** Open any website, press F12, and in the Console type `document.title` and `document.querySelectorAll("a").length`. Ask: what did you learn about the page?
2. **Human DOM (10 min):** Students stand as a DOM tree (document, body, 2 divs, 3 paragraphs). The teacher says "change the colour of all paragraphs" and the paragraph students raise a hand. This explains selectors.
3. **Debug the bug (10 min):** Give broken code. Example: `$("#btn").click(hideIt())`, missing `$(function(){ })`, `if (x = 5)`, forgetting `return` in `onsubmit`. Students find and fix.
4. **Rock-paper-scissors (15 min):** Use `Math.random()`, an array, `if/else`, and `prompt`.
5. **Cricket scoreboard (15 min):** Array of player objects, loop to print a table, compute strike rate and team total.
6. **Hover gallery (10 min):** Four coloured divs; on hover change the background and show the name using jQuery.
7. **Plain JS vs jQuery race (10 min):** Half the class writes "hide a paragraph on click" in plain JS, the other half in jQuery. Compare lines of code.
8. **Quiz relay (10 min):** Two teams. The teacher asks "Which method?" questions (`prepend` or `append`? `attr` or `prop`?). One point each.

---

# PART E: QUESTION BANK (KTU STYLE)

Pattern: **Part A** has short questions (3 marks each). **Part B** has longer questions (9 marks each) with sub-parts. Marks below are suggestions.

## Part A (3 marks each)

1. What is a scripting language? Mention two uses of JavaScript in a web page.
2. Differentiate between `let`, `const` and `var`.
3. Differentiate between `prompt()` and `alert()` with an example of `prompt()`.
4. Write a JavaScript program fragment to find the largest of three numbers using if-else.
5. Differentiate between `while` and `do-while` loops with examples.
6. What is the DOM? Name any three methods used to select elements.
7. Write a jQuery snippet to hide a paragraph when a button is clicked.
8. What are the differences between `.text()`, `.html()` and `.val()` in jQuery?
9. Explain `.each()` in jQuery with a short example.
10. What is a JavaScript library? Mention two advantages of using jQuery.

## Part B (9 marks each)

11. (a) Explain how JavaScript handles form validation. (5 marks)
    (b) Write a JavaScript function that checks whether a text field is empty when the form is submitted. (4 marks)

12. (a) Explain functions and arrays in JavaScript with examples. (6 marks)
    (b) How do functions and arrays help to organise code? (3 marks)

13. (a) Explain the different control statements in JavaScript (`if`, `switch`, `for`, `while`, `do-while`, `break`, `continue`) with examples. (6 marks)
    (b) Write a program to print the sum of the first N natural numbers using a loop, where N is read with `prompt()`. (3 marks)

14. (a) Explain jQuery selectors with at least six examples. (5 marks)
    (b) Write a jQuery script to select all paragraphs and change their font colour to blue on a button click. (4 marks)

15. (a) Explain jQuery events and the event object with examples. (5 marks)
    (b) Write jQuery code to change the background colour of a `div` when the mouse is over it and change it back when the mouse moves out. (4 marks)

16. (a) Explain jQuery effects and the `animate()` method with examples. (5 marks)
    (b) Explain how to insert new elements into a page using jQuery (`append`, `prepend`, `after`, `before`). (4 marks)

**More practice (not for marks):**
- Explain DOM traversing methods in jQuery with examples.
- Write a program using an object that stores student details and prints them in a table.
- Compare plain JavaScript and jQuery for selecting elements and handling events.
- Write a form with name and email fields and validate it using jQuery.

---

## Model answers and answer hints

### Q3 (Part A). Difference between prompt() and alert(), with a prompt() example

| Point | `alert()` | `prompt()` |
|---|---|---|
| Purpose | Shows a message to the user | Asks the user to type a value |
| Input box | No | Yes |
| Buttons | OK | OK and Cancel |
| Returns | `undefined` (nothing useful) | Typed text as a string; `null` if Cancel |

```html
<!DOCTYPE html>
<html>
<body>
<script>
  let name = prompt("Enter your name:", "Guest");   // asks input
  if (name !== null && name.trim() !== "") {
    alert("Hello, " + name + "!");                  // shows output
  } else {
    alert("No name entered.");
  }
</script>
</body>
</html>
```

Note: the value returned by `prompt()` is always a string. Use `Number()` or `parseInt()` if a number is needed.

### Q7 (Part A). jQuery snippet to hide a paragraph when a button is clicked

```html
<!DOCTYPE html>
<html>
<head>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <script>
    $(document).ready(function () {
      $("#hideBtn").click(function () {
        $("p").hide();
      });
    });
  </script>
</head>
<body>
  <p>This paragraph will be hidden.</p>
  <button id="hideBtn">Hide</button>
</body>
</html>
```

Explanation: `$(document).ready` runs the code after the page loads. `$("#hideBtn").click(...)` attaches a click handler. `$("p").hide()` hides all paragraphs.

### Q2 (Part A). Differentiate let, const and var (hint)

- `var`: function scope, can be re-declared and changed, hoisted with value `undefined`.
- `let`: block scope, can be changed, cannot be re-declared in the same scope.
- `const`: block scope, must be given a value at declaration, cannot be reassigned (an object's inside can still change).
- Give a 3-line example for each.

### Q5 (Part A). while versus do-while (hint)

- `while` checks the condition first, so the body may run zero times.
- `do-while` runs the body first, then checks, so it runs at least once.
- Example: print 1 to 5 with each; show that with a false condition `while` prints nothing but `do-while` prints once.

### Q11. How JavaScript handles form validation, with an empty-field example

**(a) Explanation (model answer)**

Form validation is checking the data a user enters in a form before it is sent to the server. JavaScript does this on the client (browser) side.

Steps:
1. A handler is attached to the form's `onsubmit` event (or `submit` event with `addEventListener`).
2. The handler reads field values from the DOM using `document.getElementById("id").value` or `document.forms["name"]["field"].value`.
3. It tests the values using conditions: empty check, length check, number range, pattern (regular expression) for email or mobile, password match, checkbox checked.
4. If a test fails, it shows an error (with `alert` or by writing text into the page) and stops the submission by `return false` or `event.preventDefault()`.
5. If all tests pass, it allows the form to submit (`return true`).

Advantages: instant feedback, fewer useless requests to the server, better user experience.
Limitation: users can switch off or bypass JavaScript, so the **server must validate again**. HTML5 attributes (`required`, `type="email"`, `pattern`) give simple validation without script.

**(b) Example: empty text field on submit**

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Empty field check</title>
  <script>
    function validateForm() {
      let x = document.forms["myForm"]["fname"].value.trim();
      if (x === "") {
        alert("Name must be filled out");
        return false;          // stop submit
      }
      return true;             // allow submit
    }
  </script>
</head>
<body>
  <form name="myForm" action="submit.php" method="post" onsubmit="return validateForm()">
    Name: <input type="text" name="fname">
    <input type="submit" value="Submit">
  </form>
</body>
</html>
```

Marking hint: 2 marks for the idea and steps, 1 mark each for event, checks, stopping submission, and for the server-side remark. Code: 1 for function, 1 for reading the value, 1 for the empty condition and message, 1 for `return false/true` with `onsubmit="return ..."`.

### Q15(b). Change background of a div on mouse over, back on mouse out

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <style>
    #box { width: 200px; height: 100px; background-color: white; border: 1px solid black; }
  </style>
  <script>
    $(document).ready(function () {
      $("#box").mouseover(function () {
        $(this).css("background-color", "yellow");
      });
      $("#box").mouseout(function () {
        $(this).css("background-color", "white");
      });
    });
  </script>
</head>
<body>
  <div id="box">Move the mouse over me</div>
</body>
</html>
```

Shorter way using `hover`:

```javascript
$("#box").hover(
  function () { $(this).css("background-color", "yellow"); },
  function () { $(this).css("background-color", "white"); }
);
```

(`mouseenter` and `mouseleave` are slightly better than `mouseover` and `mouseout` when the div has children, because they do not fire again when the mouse moves over inner elements. `hover` uses them.)

### Q12. Functions and arrays in JavaScript, and how they organise code

**(a) Explanation**

*Function:* a named, reusable block of code that may take parameters and return a value. Defined with the `function` keyword (or arrow syntax) and called by name.

*Array:* an ordered collection of values stored in one variable, accessed by index starting at 0. It has a `length` and methods such as `push`, `pop`, `sort`, `map`, `filter`.

```html
<!DOCTYPE html>
<html>
<body>
<script>
  // Array: marks of 5 students
  let marks = [72, 45, 88, 30, 91];

  // Function: takes an array, returns the average
  function average(list) {
    let sum = 0;
    for (let i = 0; i < list.length; i++) {
      sum += list[i];
    }
    return sum / list.length;
  }

  // Function: takes an array, returns only passed marks (>= 40)
  function passed(list) {
    return list.filter(function (m) { return m >= 40; });
  }

  document.write("Average: " + average(marks).toFixed(2) + "<br>");   // 65.20
  document.write("Passed marks: " + passed(marks).join(", "));        // 72, 45, 88, 91

  marks.push(60);                       // add a new mark
  document.write("<br>Count now: " + marks.length);                  // 6
</script>
</body>
</html>
```

**(b) How they help organise code**

- **Functions** avoid repeating code (write once, call many times), break a big problem into small named steps, make testing and fixing easier (fix in one place), and allow reuse across pages.
- **Arrays** keep many related values under one name instead of many separate variables (`mark1, mark2, ...`), work well with loops, and allow built-in operations (sort, search, filter).
- Together: data goes in arrays, the logic that works on the data goes in functions. The program becomes shorter, readable and easier to change.

### Q14(b). Select all paragraphs, change font colour to blue on button click

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <script>
    $(document).ready(function () {
      $("#colorBtn").click(function () {
        $("p").css("color", "blue");
      });
    });
  </script>
</head>
<body>
  <p>First paragraph</p>
  <p>Second paragraph</p>
  <p>Third paragraph</p>
  <button id="colorBtn">Make text blue</button>
</body>
</html>
```

Explanation: `$("p")` selects every paragraph; `.css("color","blue")` sets the font colour on all of them at once, so no loop is needed.

### Q14(a). jQuery selectors (hint with six examples)

| Selector | Meaning |
|---|---|
| `$("p")` | element selector |
| `$("#id")` | id selector |
| `$(".class")` | class selector |
| `$("ul li")` | descendant selector |
| `$("p:first")` | first paragraph |
| `$("input[type='text']")` | attribute selector |
| `$("li:even")` | even-indexed items |
| `$(this)` | current element |

Write one line of explanation for each and show one live example.

### Q15(a). Events and event object (hint)

- Event: action on the page (click, hover, key, submit). Handler attached with `.click()`, `.on("click", fn)`; `.off()` removes it.
- Categories: mouse, keyboard, form, document/window.
- Event object: passed as the first parameter; has `type`, `target`, `pageX`, `pageY`, `key`, `preventDefault()`, `stopPropagation()`.
- Example: stop a link from opening using `e.preventDefault()`; show mouse coordinates with `mousemove`.

### Q16 (hint)

(a) Effects: `show/hide/toggle`, `fadeIn/fadeOut/fadeToggle/fadeTo`, `slideDown/slideUp/slideToggle`. `animate({props}, speed, callback)` changes numeric CSS properties. Give code like `$("#box").animate({left:"250px", opacity:0.5}, 1000)`.
(b) `append` (inside end), `prepend` (inside start), `after` (outside after), `before` (outside before). Show a small list example and say what each produces.

### Q13(b). Sum of first N natural numbers

```html
<!DOCTYPE html>
<html>
<body>
<script>
  let n = parseInt(prompt("Enter N:"));
  if (isNaN(n) || n < 1) {
    alert("Please enter a positive whole number");
  } else {
    let sum = 0;
    for (let i = 1; i <= n; i++) {
      sum += i;
    }
    alert("Sum of first " + n + " natural numbers = " + sum);
  }
</script>
</body>
</html>
```

### Q4 (Part A). Largest of three numbers

```javascript
let a = 12, b = 45, c = 30;
if (a >= b && a >= c) {
  console.log("Largest is " + a);
} else if (b >= a && b >= c) {
  console.log("Largest is " + b);
} else {
  console.log("Largest is " + c);
}
```

### Q8, Q9, Q10 (hints)

- Q8: `.text()` gets/sets plain text, `.html()` gets/sets HTML markup, `.val()` gets/sets form field values. Show one example of each.
- Q9: `.each()` runs a function for every element in the selection. Example: add up `data-price` of all list items. `$(this)` is the current element; `return false` stops the loop.
- Q10: A library is reusable code written by others. jQuery advantages: short syntax, handles browser differences, built-in effects and Ajax, big plugin community.

---

## Quick revision sheet (one page for students)

- Variables: `let` (change), `const` (fixed), avoid `var`.
- `prompt` returns string or `null`. `confirm` returns true/false. `alert` returns nothing.
- Use `===` not `==`.
- Loops: `for` (known count), `while` (condition first), `do-while` (at least once). `break` stops, `continue` skips.
- Array index starts at 0. Object uses `key: value`.
- DOM = tree of the page. Change it with `getElementById`, `querySelector`, `innerHTML`, `textContent`, `style`, `classList`, `createElement`, `appendChild`.
- Validation: read value, test, show error, `preventDefault()` / `return false`. Server must re-check.
- jQuery shape: `$(selector).action()`. Always wrap in `$(function(){ ... })`.
- Content: `.text() .html() .val()`. Insert: `.append .prepend .after .before`. Attributes: `.attr .prop .removeAttr`. CSS: `.css .addClass .toggleClass`.
- Events: `.click .on .hover .keyup .change .submit`. Event object: `e.preventDefault()`, `e.target`, `e.pageX`.
- Effects: `.hide .show .fadeIn .fadeOut .slideToggle .animate`.
- Traversing: `.parent .children .find .siblings .next .prev .closest`.
- Library = ready-made code. Load the library script before your own.

*End of Module 2.*
