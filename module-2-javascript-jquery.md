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

**Part B: jQuery**
12. A Basic jQuery Example
13. Finding Elements and jQuery Selection
14. Getting Element Content
15. Updating Elements and Changing Content
16. Inserting Elements and Adding New Content
17. Getting and Setting Attributes
18. Getting and Setting CSS Properties
19. Using .each()
20. Events
21. The Event Object
22. Effects
23. Animating CSS Properties and Using Animation
24. Traversing the DOM
25. Working with Forms
26. JavaScript Libraries

**Part C: Plain JavaScript vs jQuery**
**Part D: Mini-Project (Tea Shop Bill Calculator)**
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

# PART B: jQUERY

---

## 12. A Basic jQuery Example

### Simple explanation

**jQuery** is a JavaScript library (a ready-made set of functions) that makes common page tasks short and easy. Its motto: "write less, do more".

To use it, include it with a `<script>` tag (from a CDN, a fast public server):

```html
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
```

The main shape of every jQuery line:

```
$(selector).action(parameters);
```

- `$` (dollar sign) is the jQuery function (same as writing `jQuery`).
- `selector` says **which** element(s).
- `action` says **what to do**.

**Document ready:** wrap code so it runs only after the page is loaded:

```javascript
$(document).ready(function () {
  // your code
});
// short form:
$(function () {
  // your code
});
```

**Analogy:** jQuery is like **UPI/GPay**. Earlier, paying someone needed many steps (bank details, IFSC, account number, transfer). GPay wraps all that into "scan and pay". jQuery wraps long JavaScript steps into short one-liners.

### Code example

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>First jQuery</title>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
</head>
<body>
  <h2 id="head">Hello</h2>
  <p>This paragraph will disappear.</p>
  <button id="hideBtn">Hide paragraph</button>
  <button id="showBtn">Show paragraph</button>

  <script>
    $(document).ready(function () {
      $("#hideBtn").click(function () {
        $("p").hide();
      });
      $("#showBtn").click(function () {
        $("p").show();
      });
      $("#head").text("Hello from jQuery!");
    });
  </script>
</body>
</html>
```

Because the jQuery file is loaded in `<head>` and our code waits for ready, this order is safe. The jQuery `<script src>` must come **before** your own code.

### Real-world example

Many older and current sites (Bootstrap 3 sites, WordPress themes, government and college portals) use jQuery for menus, sliders, popups and form checks. Around the world a very large share of websites still load jQuery.

### Common mistakes

- Loading your script before the jQuery file (`$ is not defined` error).
- Forgetting `#` for id or `.` for class in the selector.
- Not using document ready when the script is in `<head>`.
- Being offline when using the CDN link (page cannot get jQuery).

### Check your understanding

1. What does `$` mean in jQuery?
2. Why do we write `$(document).ready(...)`?
3. Write the jQuery line to hide all `<h2>` elements.

---

## 13. Finding Elements and jQuery Selection

### Simple explanation

jQuery selectors use **CSS syntax** (you already know it from Module 1), plus a few extras.

| Selector | Meaning |
|---|---|
| `$("p")` | all paragraphs |
| `$("#box")` | element with id `box` |
| `$(".note")` | all with class `note` |
| `$("p.note")` | `<p>` elements with class `note` |
| `$("ul li")` | all `li` inside `ul` |
| `$("ul > li")` | direct children `li` of `ul` |
| `$("h1, h2, p")` | several selectors |
| `$("*")` | everything |
| `$("[href]")` | has `href` attribute |
| `$("a[target='_blank']")` | attribute equals |
| `$("li:first")` / `:last` | first / last match |
| `$("li:even")` / `:odd` | even / odd (counting from 0) |
| `$("li:eq(2)")` | the third item |
| `$(":input")` | all form inputs |
| `$(":checked")` | checked boxes and radios |
| `$("p:contains('tea')")` | paragraphs with the word tea |
| `$(this)` | the element that triggered the event |

Every selection returns a **jQuery object** (a list that can hold zero, one or many elements). Actions run on all of them at once. Check how many were found with `.length`.

**Analogy:** A selector is a **WhatsApp group broadcast**. `$("p")` means "send to everyone in the paragraph group". `$("#box")` is a personal message to one person with a unique ID.

### Code example

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Selectors</title>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <style>
    .mark { background: yellow; }
    li { padding: 3px; }
  </style>
</head>
<body>
  <h3 id="menuTitle">Menu</h3>
  <ul id="menu">
    <li class="veg">Idli</li>
    <li class="veg">Dosa</li>
    <li class="nonveg">Chicken Fry</li>
    <li class="veg">Upma</li>
    <li class="nonveg">Fish Curry</li>
  </ul>
  <p>Select by:</p>
  <button id="b1">class .veg</button>
  <button id="b2">first</button>
  <button id="b3">even</button>
  <button id="b4">contains "Fish"</button>
  <button id="b5">clear</button>
  <p id="info"></p>

  <script>
    $(function () {
      $("#b1").click(function () {
        let found = $(".veg");
        found.addClass("mark");
        $("#info").text(found.length + " veg items selected");
      });
      $("#b2").click(function () { $("#menu li:first").addClass("mark"); });
      $("#b3").click(function () { $("#menu li:even").addClass("mark"); });
      $("#b4").click(function () { $("li:contains('Fish')").addClass("mark"); });
      $("#b5").click(function () { $("li").removeClass("mark"); $("#info").text(""); });
    });
  </script>
</body>
</html>
```

### Real-world example

"Highlight all unread messages", "tick all checkboxes" (Select All in Gmail), and "show only veg dishes" on a food app are one selector plus one action.

### Common mistakes

- Using the same `id` on many elements (only the first is found).
- Confusing `:eq(2)` (third item) with 2nd item.
- Expecting a selector to throw an error when nothing matches (it silently matches nothing; check `.length`).
- Quote problems inside selector strings.

### Check your understanding

1. Write selectors for: every `<li>` inside `#menu`; every element with class `error`; the first `<p>`.
2. What does `$(this)` refer to?
3. How can you find out how many elements a selector matched?

---

## 14. Getting Element Content

### Simple explanation

Three methods read (and write) content:

| Method | Reads | Notes |
|---|---|---|
| `.text()` | Plain text only (tags removed) | Safe |
| `.html()` | HTML inside, including tags | Be careful with user text |
| `.val()` | Value of form fields (`input`, `textarea`, `select`) | Used in forms |

Called **with no argument**, they **get**. Called **with an argument**, they **set** (change). When you select many elements, `.text()` and `.html()` as getters give a joined result for text, but `.html()` returns only from the first element.

**Analogy:** Reading a **parcel**. `.html()` opens the box and shows the item with its packing material (tags). `.text()` tells you only what the item is. `.val()` reads what the customer wrote on the delivery slip (form field).

### Code example

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Get content</title>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
</head>
<body>
  <p id="para">Special: <b>Masala</b> Dosa</p>
  <input type="text" id="who" value="Anu">
  <br><br>
  <button id="t">Get text</button>
  <button id="h">Get html</button>
  <button id="v">Get value</button>
  <p id="show"></p>

  <script>
    $(function () {
      $("#t").click(function () {
        $("#show").text("text(): " + $("#para").text());
        // Special: Masala Dosa
      });
      $("#h").click(function () {
        $("#show").text("html(): " + $("#para").html());
        // Special: <b>Masala</b> Dosa
      });
      $("#v").click(function () {
        $("#show").text("val(): " + $("#who").val());
        // Anu
      });
    });
  </script>
</body>
</html>
```

### Real-world example

When you press "Search" on Flipkart, the site reads the search box using `.val()`. A "copy coupon" button reads the coupon text with `.text()`.

### Common mistakes

- Using `.text()` on an input (use `.val()`).
- Reading `.val()` from a `<p>` (gives empty string).
- Expecting `.html()` to give the HTML of all selected elements (only the first).

### Check your understanding

1. Difference between `.text()` and `.html()`?
2. Which method reads what the user typed in a text box?
3. What does `$("#a").html()` return if `#a` contains `<i>Hi</i>`?

---

## 15. Updating Elements and Changing Content

### Simple explanation

The same methods **set** content when you pass a value:

```javascript
$("#msg").text("Order placed");
$("#msg").html("<b>Order placed</b>");
$("#name").val("Anu");
```

You can also pass a **function** to compute the new content for each element:

```javascript
$("li").text(function (index, oldText) {
  return (index + 1) + ". " + oldText;
});
```

Other helpful ones: `.empty()` (remove all children, keep the element) and `.remove()` (remove the element itself). `.replaceWith()` swaps an element with new content.

**Analogy:** Think of the **railway station display board**. The board stays fixed, but the train name and platform number change. `.text()` is the person changing the message on the board.

### Code example

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Update content</title>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
</head>
<body>
  <h3 id="status">Order: Preparing</h3>
  <ul id="items">
    <li>Tea</li>
    <li>Vada</li>
    <li>Samosa</li>
  </ul>
  <input type="text" id="nameBox" placeholder="Your name">
  <br><br>
  <button id="b1">Mark delivered</button>
  <button id="b2">Number the items</button>
  <button id="b3">Fill name</button>
  <button id="b4">Empty list</button>

  <script>
    $(function () {
      $("#b1").click(function () {
        $("#status").html("Order: <span style='color:green'>Delivered</span>");
      });
      $("#b2").click(function () {
        $("#items li").text(function (i, old) {
          return (i + 1) + ". " + old;
        });
      });
      $("#b3").click(function () { $("#nameBox").val("Anu"); });
      $("#b4").click(function () { $("#items").empty(); });
    });
  </script>
</body>
</html>
```

### Real-world example

Swiggy's order tracking text ("Preparing", "Out for delivery", "Delivered"), live cricket score numbers, and "3 items in cart" badges update this way.

### Common mistakes

- Calling `.text("...")` expecting HTML tags to work (they show as plain text).
- Pressing the button twice and applying "1. 1. Tea" (the function runs again on the new text).
- Using `.empty()` when you meant `.remove()`.

### Check your understanding

1. What happens when `.text()` is given an argument?
2. Difference between `.empty()` and `.remove()`?
3. Write a line to set the value of `#city` to "Kochi".

---

## 16. Inserting Elements and Adding New Content

### Simple explanation

| Method | Where the new content goes |
|---|---|
| `.append(x)` | **inside** the element, at the **end** |
| `.prepend(x)` | **inside**, at the **start** |
| `.after(x)` | **outside**, right **after** the element |
| `.before(x)` | **outside**, right **before** the element |
| `.appendTo(target)` | reverse form: `$(x).appendTo(target)` |

`x` can be an HTML string (`"<li>New</li>"`), a DOM element or a jQuery object. You can also build elements: `$("<li>", { text: "New", class: "item" })`.

Remove with `.remove()`. For elements added **later**, use event delegation: `$("#list").on("click", "li", fn)` (see Events).

**Analogy:** A **train**. `.append` attaches a coach at the end, `.prepend` attaches one right behind the engine, `.before` and `.after` put something on the platform before or after the whole train.

### Code example: dynamic list

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Insert elements</title>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <style>
    #box { border: 1px solid #999; padding: 8px; width: 260px; }
  </style>
</head>
<body>
  <div id="box">
    <p>Middle paragraph</p>
  </div>
  <br>
  <button id="a">append</button>
  <button id="p">prepend</button>
  <button id="af">after</button>
  <button id="bf">before</button>

  <hr>
  <input type="text" id="task" placeholder="New task">
  <button id="add">Add to list</button>
  <ul id="tasks"></ul>

  <script>
    $(function () {
      $("#a").click(function ()  { $("#box").append("<p>Appended (end, inside)</p>"); });
      $("#p").click(function ()  { $("#box").prepend("<p>Prepended (start, inside)</p>"); });
      $("#af").click(function () { $("#box").after("<p>After the box (outside)</p>"); });
      $("#bf").click(function () { $("#box").before("<p>Before the box (outside)</p>"); });

      $("#add").click(function () {
        let t = $("#task").val().trim();
        if (t === "") { alert("Type a task"); return; }
        let li = $("<li></li>").text(t);       // .text() keeps it safe
        $("#tasks").append(li);
        $("#task").val("").focus();
      });

      // delegation: works for items added later
      $("#tasks").on("click", "li", function () {
        $(this).remove();
      });
    });
  </script>
</body>
</html>
```

### Real-world example

New chat messages in WhatsApp Web, "load more" restaurants on Zomato, and new comments under a post are added with `append`.

### Common mistakes

- Mixing up inside (`append/prepend`) with outside (`after/before`).
- Building HTML from user text with string joining and `.html()` (script injection risk). Use `.text()` for user content.
- Attaching click handlers directly to items that do not exist yet (use delegation).

### Check your understanding

1. Difference between `append()` and `after()`?
2. Write jQuery to add `<li>Ice</li>` at the start of `#cold`.
3. Why does `$("#tasks").on("click","li",...)` work for new items but `$("li").click(...)` does not?

---

## 17. Getting and Setting Attributes

### Simple explanation

**Attributes** are things like `src`, `href`, `alt`, `id`, `title`, `disabled`.

| Task | Code |
|---|---|
| Get | `$("a").attr("href")` |
| Set one | `$("img").attr("src", "b.png")` |
| Set many | `$("img").attr({ src: "b.png", alt: "Tea" })` |
| Remove | `$("a").removeAttr("title")` |
| Properties (true/false things) | `$("#c").prop("checked")`, `.prop("disabled", true)` |
| Classes | `.addClass()`, `.removeClass()`, `.toggleClass()`, `.hasClass()` |
| Data attributes | `.data("price")` reads `data-price="12"` |

Use `.prop()` for `checked`, `disabled` and `selected`. Use `.attr()` for the rest.

**Analogy:** Attributes are like the **labels on a parcel** (address, phone, "fragile"). Changing the `src` of an image is like changing the sticker on the parcel; the box is the same.

### Code example

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Attributes</title>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
</head>
<body>
  <a id="link" href="https://www.ktu.edu.in" title="KTU site">KTU Website</a>
  <p id="info"></p>
  <button id="get">Get href</button>
  <button id="set">Change link</button>
  <button id="rm">Remove title</button>

  <hr>
  <input type="text" id="txt" placeholder="Type here">
  <button id="dis">Disable / Enable box</button>
  <br><br>
  <input type="checkbox" id="chk"> Accept
  <button id="chkBtn">Is it ticked?</button>

  <hr>
  <button id="tea" data-name="Tea" data-price="10">Tea</button>
  <span id="priceInfo"></span>

  <script>
    $(function () {
      $("#get").click(function () {
        $("#info").text("href = " + $("#link").attr("href"));
      });
      $("#set").click(function () {
        $("#link").attr({
          href: "https://www.google.com",
          title: "Google"
        }).text("Google");
      });
      $("#rm").click(function () { $("#link").removeAttr("title"); });

      $("#dis").click(function () {
        let isOff = $("#txt").prop("disabled");
        $("#txt").prop("disabled", !isOff);
      });
      $("#chkBtn").click(function () {
        alert($("#chk").prop("checked") ? "Yes, ticked" : "No, not ticked");
      });

      $("#tea").click(function () {
        $("#priceInfo").text($(this).data("name") + " costs Rs. " + $(this).data("price"));
      });
    });
  </script>
</body>
</html>
```

### Real-world example

Changing a product image when you click a colour swatch on Flipkart (`attr("src", ...)`), disabling the "Pay" button until all fields are filled (`prop("disabled", true)`), and reading `data-id` of the clicked dish to add it to the cart.

### Common mistakes

- Using `.attr("checked")` to read the current state (use `.prop("checked")`).
- Typing `$("img").attr("source", ...)` (wrong attribute name).
- Forgetting that `.data("price")` reads `data-price`.

### Check your understanding

1. Write jQuery to change the `alt` of all images to "Photo".
2. When do we use `.prop()` instead of `.attr()`?
3. How do you read `data-id` from a button?

---

## 18. Getting and Setting CSS Properties

### Simple explanation

Use `.css()`:

```javascript
$("p").css("color");                       // get
$("p").css("color", "blue");               // set one
$("p").css({ color: "white", "background-color": "navy", padding: "8px" }); // many
```

Property names can be written as `"background-color"` or `backgroundColor`. Related: `.width()`, `.height()`, `.offset()`, `.addClass()` / `.removeClass()` / `.toggleClass()` (best way for bigger style changes, because the CSS stays in the style sheet).

**Analogy:** `.css()` is a **sticky note of styling instructions** you stick on an element, such as "make this text blue". Using `addClass` is like handing the element a whole ready-made **uniform**.

### Code example

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>CSS with jQuery</title>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <style>
    .dark { background: #222; color: #fff; }
    #card { padding: 20px; width: 280px; border: 2px solid teal; }
  </style>
</head>
<body>
  <div id="card">
    <h3>Today's Offer</h3>
    <p>Free sweet on orders above Rs. 300.</p>
  </div>
  <br>
  <button id="b1">Blue text</button>
  <button id="b2">Many styles</button>
  <button id="b3">Read colour</button>
  <button id="b4">Toggle dark class</button>
  <button id="b5">Bigger width</button>
  <p id="out"></p>

  <script>
    $(function () {
      $("#b1").click(function () { $("#card p").css("color", "blue"); });
      $("#b2").click(function () {
        $("#card").css({
          "background-color": "lightyellow",
          "border-radius": "12px",
          "font-family": "Georgia"
        });
      });
      $("#b3").click(function () {
        $("#out").text("Colour of paragraph: " + $("#card p").css("color"));
        // browsers return it as rgb(...)
      });
      $("#b4").click(function () { $("#card").toggleClass("dark"); });
      $("#b5").click(function () { $("#card").width($("#card").width() + 40); });
    });
  </script>
</body>
</html>
```

### Real-world example

Turning a form field border red when it is invalid, switching dark mode on a site, highlighting the row of the table you hover over.

### Common mistakes

- Writing `background-color` without quotes inside an object (it needs quotes because of the dash).
- Setting numbers without units for properties that need them as text (`"10px"`). jQuery adds `px` for plain numbers in many cases, but be clear.
- Putting lots of styling in JavaScript instead of using classes.

### Check your understanding

1. How do you read the font size of a paragraph?
2. Write one statement to set both `color` and `font-size` for `#title`.
3. Why is `toggleClass` often better than many `.css()` calls?

---

## 19. Using .each()

### Simple explanation

`.each()` loops over every element in a selection and runs a function on each one.

```javascript
$("li").each(function (index, element) {
  // index = 0,1,2...
  // element = the DOM element; $(this) or $(element) gives a jQuery object
});
```

- Inside, `this` is the current element. Use `$(this)` to apply jQuery methods.
- `return false` inside `.each()` stops the loop (like `break`). `return true` skips to next (like `continue`).
- `$.each(array, function(index, value){})` works on plain arrays and objects.

**Analogy:** A **teacher taking attendance**: she goes through each student on the list (`each`), reads the name (`this`), and marks present.

### Code example

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>each()</title>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
</head>
<body>
  <ul id="cart">
    <li data-price="10">Tea</li>
    <li data-price="15">Coffee</li>
    <li data-price="20">Samosa</li>
  </ul>
  <button id="total">Calculate total</button>
  <button id="num">Number the items</button>
  <p id="out"></p>

  <script>
    $(function () {
      $("#total").click(function () {
        let sum = 0;
        $("#cart li").each(function () {
          sum += Number($(this).data("price"));
        });
        $("#out").text("Total = Rs. " + sum);     // 45
      });

      $("#num").click(function () {
        $("#cart li").each(function (i) {
          $(this).prepend((i + 1) + ". ");
        });
      });

      // $.each on an array
      let colours = ["red", "green", "blue"];
      $.each(colours, function (i, c) {
        console.log(i + " => " + c);
      });

      // $.each on an object
      $.each({ name: "Anu", age: 20 }, function (key, value) {
        console.log(key + ": " + value);
      });
    });
  </script>
</body>
</html>
```

### Real-world example

Adding all item prices in a cart, checking every input in a form for emptiness, and numbering rows in a table.

### Common mistakes

- Using `this.text()` (this is a plain DOM element; write `$(this).text()`).
- Using `return false` thinking it only skips (it stops the whole loop).
- Using `.each()` when a single jQuery method already works on all elements (for example `$("p").hide()` needs no loop).

### Check your understanding

1. What are the two parameters of the `.each()` callback?
2. How do you stop an `.each()` loop early?
3. Why do we write `$(this)` inside `.each()`?

---

## 20. Events

### Simple explanation

An **event** is something that happens on the page: a click, a key press, a mouse movement, a form submit. jQuery lets you attach a function (called an **event handler**) that runs when the event happens.

| Group | Events |
|---|---|
| Mouse | `click`, `dblclick`, `mouseenter`, `mouseleave`, `mouseover`, `mouseout`, `hover` |
| Keyboard | `keydown`, `keyup`, `keypress` (old) |
| Form | `submit`, `change`, `focus`, `blur`, `input` |
| Window/document | `ready`, `load`, `resize`, `scroll` |

Two ways to attach:

```javascript
$("#btn").click(function () { ... });         // shortcut
$("#btn").on("click", function () { ... });   // general, preferred
$("#btn").off("click");                       // remove handler
$("#btn").one("click", fn);                   // run only once
$("#list").on("click", "li", fn);             // delegation (for later-added items)
$("#box").hover(inFn, outFn);                 // mouse in and mouse out
```

**Analogy:** An event is the **doorbell**. The handler is the **person who opens the door**. Nothing happens until someone rings.

### Code example

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>jQuery events</title>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <style>
    #box { width: 220px; height: 80px; background: lightblue; padding: 10px; }
  </style>
</head>
<body>
  <div id="box">Hover, click and double-click me</div>
  <br>
  <input type="text" id="tweet" maxlength="40" placeholder="Type (max 40)">
  <span id="count">40 left</span>
  <br><br>
  <select id="city">
    <option value="">Choose</option>
    <option>Kochi</option>
    <option>Trivandrum</option>
  </select>
  <p id="log"></p>

  <script>
    $(function () {
      // hover: mouse in / mouse out
      $("#box").hover(
        function () { $(this).css("background-color", "orange"); },
        function () { $(this).css("background-color", "lightblue"); }
      );

      $("#box").on("click", function () { $("#log").text("Clicked"); });
      $("#box").dblclick(function () { $("#log").text("Double-clicked"); });

      // keyup: live character counter
      $("#tweet").on("keyup", function () {
        let left = 40 - $(this).val().length;
        $("#count").text(left + " left");
      });

      // change: dropdown
      $("#city").change(function () {
        $("#log").text("You chose: " + $(this).val());
      });

      // one(): only first time
      $("#box").one("click", function () { console.log("First click only"); });
    });
  </script>
</body>
</html>
```

### Real-world example

Search suggestions that appear while you type (keyup), a menu that opens on hover or click, "Place order" on click, and the WhatsApp message box enabling the send button when you type.

### Common mistakes

- Calling the function instead of passing it: `.click(doIt())` instead of `.click(doIt)`.
- Adding the same handler many times, so it runs many times.
- Using arrow functions and then expecting `this` to be the element (use normal `function`).
- Using `.click()` for items created later (use delegation).

### Check your understanding

1. Name three mouse events and three keyboard/form events.
2. What is event delegation and why is it used?
3. Write jQuery to change the background colour of `#box` to red on mouseover and back to white on mouseout.

---

## 21. The Event Object

### Simple explanation

jQuery gives every handler an **event object** (often named `e` or `event`) with details about what happened.

| Property / method | Meaning |
|---|---|
| `e.type` | Name of event ("click") |
| `e.target` | The element that was actually clicked |
| `e.currentTarget` / `this` | The element the handler is attached to |
| `e.pageX`, `e.pageY` | Mouse position on page |
| `e.which` / `e.key` | Which key was pressed |
| `e.preventDefault()` | Stop the browser's default action (link opening, form submitting) |
| `e.stopPropagation()` | Stop the event moving up to parent elements ("bubbling") |
| `e.timeStamp` | When it happened |

**Bubbling:** an event on an inner element also goes up to its parents. A click on a button inside a div also triggers the div's click handler unless you stop it.

**Analogy:** The event object is the **delivery receipt** that comes with a parcel: it tells you who sent it, where it was delivered, and at what time.

### Code example

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Event object</title>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <style>
    #pad { width: 300px; height: 120px; border: 2px dashed gray; padding: 6px; }
    #outer { padding: 20px; background: #eef; width: 280px; }
  </style>
</head>
<body>
  <div id="pad">Move the mouse here</div>
  <p id="pos"></p>

  <a id="ktu" href="https://www.ktu.edu.in">KTU (click will be blocked)</a>

  <br><br>
  <input type="text" id="key" placeholder="Press keys here">
  <p id="keyInfo"></p>

  <div id="outer">Outer div
    <button id="inner">Inner button</button>
  </div>
  <p id="bub"></p>

  <script>
    $(function () {
      $("#pad").on("mousemove", function (e) {
        $("#pos").text("X: " + e.pageX + ", Y: " + e.pageY);
      });

      $("#ktu").on("click", function (e) {
        e.preventDefault();                       // link will not open
        alert("Event type: " + e.type + ", target tag: " + e.target.tagName);
      });

      $("#key").on("keyup", function (e) {
        $("#keyInfo").text("You pressed: " + e.key);
        if (e.key === "Enter") {
          $("#keyInfo").text("Enter pressed. Value = " + $(this).val());
        }
      });

      // bubbling
      $("#outer").on("click", function () { $("#bub").append("outer clicked. "); });
      $("#inner").on("click", function (e) {
        e.stopPropagation();       // remove this line to see both messages
        $("#bub").append("inner clicked. ");
      });
    });
  </script>
</body>
</html>
```

### Real-world example

Drawing apps and image croppers use `pageX/pageY`. Pressing **Enter** to send a message in WhatsApp Web uses the key info from the event. Custom links that open a popup instead of a new page use `preventDefault()`.

### Common mistakes

- Forgetting to put `e` as a parameter and then using `e`.
- Using `return false` in jQuery (it does both `preventDefault` and `stopPropagation`) when you only needed one.
- Confusing `e.target` (what was clicked) with `this` (what has the handler).

### Check your understanding

1. What is the event object?
2. What does `e.preventDefault()` do? Give one use.
3. What is event bubbling?

---

## 22. Effects

### Simple explanation

jQuery has ready-made visual effects. Most accept a speed (`"slow"`, `"fast"`, or milliseconds) and an optional callback function that runs when the effect finishes.

| Group | Methods |
|---|---|
| Show/hide | `.show()`, `.hide()`, `.toggle()` |
| Slide | `.slideDown()`, `.slideUp()`, `.slideToggle()` |
| Fade | `.fadeIn()`, `.fadeOut()`, `.fadeToggle()`, `.fadeTo(speed, opacity)` |
| Control | `.stop()`, `.delay(ms)` |

**Analogy:** Effects are the **cinema theatre curtain** and lights. The screen is always there. `fade` is the lights dimming, `slide` is the curtain going up or down, `hide` is a sudden blackout.

### Code example

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Effects</title>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <style>
    #panel { background: #ffe8a3; padding: 15px; width: 300px; margin: 10px 0; }
    #title { cursor: pointer; background: teal; color: white; padding: 8px; width: 300px; }
  </style>
</head>
<body>
  <button id="hide">Hide</button>
  <button id="show">Show</button>
  <button id="toggle">Toggle</button>
  <button id="fin">Fade in</button>
  <button id="fout">Fade out</button>
  <button id="fto">Fade to 30%</button>

  <div id="panel">Today's offer: Buy 2 Tea, get 1 Vada free!</div>

  <div id="title">Click for FAQ (slide effect)</div>
  <div id="faq" style="display:none; background:#eee; padding:10px; width:300px;">
    Delivery takes 30 minutes. Pay by UPI or cash.
  </div>

  <p id="done"></p>

  <script>
    $(function () {
      $("#hide").click(function () { $("#panel").hide(500); });
      $("#show").click(function () { $("#panel").show("slow"); });
      $("#toggle").click(function () { $("#panel").toggle(); });
      $("#fin").click(function () { $("#panel").fadeIn(1000); });
      $("#fout").click(function () {
        $("#panel").fadeOut(1000, function () {
          $("#done").text("Fade finished (callback ran)");
        });
      });
      $("#fto").click(function () { $("#panel").fadeTo(800, 0.3); });

      $("#title").click(function () { $("#faq").slideToggle("fast"); });
    });
  </script>
</body>
</html>
```

### Real-world example

FAQ accordions, "back to top" buttons that fade in when you scroll down, notification banners that fade away after some seconds, dropdown menus that slide down.

### Common mistakes

- Starting a new effect while the old one is running, causing a queue (use `.stop()` first).
- Forgetting `display:none` in CSS for something that should start hidden (or using `.hide()` at ready).
- Treating the code after an effect as if it runs after the effect ends (it does not; use the callback).

### Check your understanding

1. Difference between `hide()` and `fadeOut()`?
2. What does `slideToggle()` do?
3. What is a callback in an effect? Why is it needed?
4. Write jQuery to hide a paragraph when a button with id `btn` is clicked.

---

## 23. Animating CSS Properties and Using Animation

### Simple explanation

`.animate()` changes **numeric** CSS properties smoothly over time.

```javascript
$(selector).animate({ properties }, duration, easing, callback);
```

- Properties must be **numbers** (`width`, `height`, `opacity`, `left`, `top`, `fontSize`, `marginLeft`). Colours need an extra plugin (jQuery UI).
- Relative values are allowed: `left: "+=50px"`.
- To move an element with `left/top` it needs `position: relative` or `absolute`.
- Several `.animate()` calls on the same element run one after another (a **queue**).
- `.stop()` stops the current animation; `.delay(ms)` waits.
- For many effects, CSS animations are lighter, but `.animate()` is in the syllabus and is useful for learning.

**Analogy:** A **cricket ball** going to the boundary. The start and end are fixed. The animation draws the path between them smoothly instead of teleporting the ball.

### Code example

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>animate()</title>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <style>
    #stage { width: 500px; height: 80px; border: 1px solid #999; position: relative; margin: 15px 0; }
    #ball  { width: 50px; height: 50px; background: crimson; border-radius: 50%;
             position: absolute; left: 0; top: 15px; }
    #msg { font-size: 16px; }
  </style>
</head>
<body>
  <button id="go">Move right</button>
  <button id="back">Back</button>
  <button id="grow">Grow</button>
  <button id="chain">Chain</button>
  <button id="stop">Stop</button>

  <div id="stage"><div id="ball"></div></div>
  <p id="msg">Animate my font size</p>

  <script>
    $(function () {
      $("#go").click(function () {
        $("#ball").animate({ left: "450px" }, 1500, function () {
          $("#msg").text("Reached the boundary!");
        });
      });
      $("#back").click(function () { $("#ball").animate({ left: "0px" }, 1000); });
      $("#grow").click(function () {
        $("#ball").animate({ width: "+=20px", height: "+=20px" }, "fast");
        $("#msg").animate({ fontSize: "30px" }, 600);
      });
      $("#chain").click(function () {
        $("#ball")
          .animate({ left: "200px" }, 600)
          .animate({ top: "0px" }, 400)
          .delay(300)
          .animate({ opacity: 0.3 }, 500)
          .animate({ left: "0px", top: "15px", opacity: 1 }, 800);
      });
      $("#stop").click(function () { $("#ball").stop(true); });
    });
  </script>
</body>
</html>
```

### Real-world example

Image sliders and carousels on Flipkart or Amazon home pages, number counters that count up to "10,000 happy customers", progress bars filling up, and a cart icon that "jumps" when you add an item.

### Common mistakes

- Trying to animate non-numeric values like `color` or `display` (without a plugin).
- Not giving `position` to the element when using `left/top`.
- Clicking fast and filling the queue with many animations (use `.stop(true)` first).
- Forgetting units in strings (`"450px"`).

### Check your understanding

1. Which kind of CSS properties can `.animate()` change?
2. What does `.stop()` do? When is it useful?
3. Write jQuery to make `#box` 300 pixels wide in 2 seconds.

---

## 24. Traversing the DOM

### Simple explanation

**Traversing** means moving through the DOM tree from one element to its relatives: parent, children, siblings.

| Direction | Methods |
|---|---|
| Up | `.parent()`, `.parents()`, `.parentsUntil()`, `.closest(sel)` |
| Down | `.children()`, `.find(sel)` |
| Sideways | `.siblings()`, `.next()`, `.prev()`, `.nextAll()`, `.prevAll()` |
| Filtering | `.first()`, `.last()`, `.eq(n)`, `.filter(sel)`, `.not(sel)`, `.has(sel)` |

`.children()` looks only one level down; `.find()` searches all levels below. `.closest()` looks up from the element itself and returns the nearest ancestor that matches.

Methods can be **chained**: `$("li").first().next().addClass("hot")`.

**Analogy:** Think of **family relations**: parent (up), children (down), siblings (sideways). From your own position (the element) you can say "my father's brother's son" (`.parent().siblings().children()`).

### Code example

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Traversing</title>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <style>
    .hl { background: gold; }
    .card { border: 1px solid #aaa; padding: 8px; margin: 6px; width: 260px; }
  </style>
</head>
<body>
  <div class="card" id="c1">
    <h4>Biryani</h4>
    <p>Rs. 180</p>
    <button class="order">Order</button>
  </div>
  <div class="card" id="c2">
    <h4>Parotta</h4>
    <p>Rs. 40</p>
    <button class="order">Order</button>
  </div>

  <ul id="list">
    <li>One</li>
    <li id="two">Two</li>
    <li>Three</li>
    <li>Four</li>
  </ul>
  <button id="t1">parent / children</button>
  <button id="t2">siblings</button>
  <button id="t3">next / prev</button>
  <button id="t4">first / last / eq</button>
  <button id="clr">clear</button>
  <p id="out"></p>

  <script>
    $(function () {
      // From a button, climb to its own card, then read the sibling h4
      $(".order").click(function () {
        let card = $(this).closest(".card");          // up
        let dish = card.find("h4").text();            // down
        let price = $(this).prev("p").text();         // sideways (previous sibling)
        $("#out").text("Ordered " + dish + " (" + price + ")");
        card.siblings(".card").css("opacity", 0.4);   // sideways, other cards
        card.css("opacity", 1);
      });

      $("#t1").click(function () {
        $("#two").parent().addClass("hl");            // the ul
        $("#c1").children("h4").addClass("hl");
      });
      $("#t2").click(function () { $("#two").siblings().addClass("hl"); });
      $("#t3").click(function () {
        $("#two").next().addClass("hl");              // Three
        $("#two").prev().addClass("hl");              // One
      });
      $("#t4").click(function () {
        $("#list li").first().addClass("hl");
        $("#list li").last().addClass("hl");
        $("#list li").eq(2).addClass("hl");           // third item
      });
      $("#clr").click(function () { $(".hl").removeClass("hl"); $(".card").css("opacity", 1); });
    });
  </script>
</body>
</html>
```

### Real-world example

On a Zomato list, each dish card has its own "Add" button. Clicking it uses `.closest(".card")` to find the right dish, then `.find(".price")` to read its price. Without traversing you would need a separate id for every button.

### Common mistakes

- Using `.parent()` when you need `.closest()` (nesting level may change).
- Using `.children()` to search deep inside (it goes only one level; use `.find()`).
- Forgetting that `.siblings()` does not include the element itself.

### Check your understanding

1. Difference between `.children()` and `.find()`?
2. What does `.closest()` do?
3. In a table, how do you get the row of a clicked delete button?

---

## 25. Working with Forms

### Simple explanation

jQuery makes form work short:

| Task | Code |
|---|---|
| Read a text box or select | `$("#name").val()` |
| Set value | `$("#name").val("Anu")` |
| Check a checkbox is ticked | `$("#c").is(":checked")` or `.prop("checked")` |
| Selected radio value | `$("input[name='gender']:checked").val()` |
| Selected dropdown text | `$("#city option:selected").text()` |
| Submit event | `$("#form").on("submit", function(e){ ... })` |
| Collect all fields | `$("#form").serialize()` gives `name=Anu&age=20` |
| Disable/enable | `.prop("disabled", true/false)` |
| Reset form | `$("#form")[0].reset()` |
| Focus | `$("#name").focus()` |

Validation with jQuery is the same idea as plain JavaScript: read values, check, show messages, and call `e.preventDefault()` if invalid.

**Analogy:** The form is the **order slip at a restaurant**. jQuery is the waiter who quickly reads each box on the slip, checks that nothing is missing, and sends it to the kitchen only if complete.

### Code example: validation with jQuery

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>jQuery form</title>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <style>
    body { font-family: Arial; margin: 25px; }
    .row { margin: 10px 0; }
    .err { color: red; font-size: 13px; }
    input.bad, select.bad { border: 2px solid red; }
  </style>
</head>
<body>
  <h3>Food Order</h3>
  <form id="orderForm" novalidate>
    <div class="row">Name: <input type="text" id="name"> <span class="err" id="e1"></span></div>
    <div class="row">Email: <input type="text" id="email"> <span class="err" id="e2"></span></div>
    <div class="row">City:
      <select id="city">
        <option value="">-- choose --</option>
        <option value="KCH">Kochi</option>
        <option value="TVM">Trivandrum</option>
      </select>
      <span class="err" id="e3"></span>
    </div>
    <div class="row">Payment:
      <label><input type="radio" name="pay" value="UPI"> UPI</label>
      <label><input type="radio" name="pay" value="COD"> Cash</label>
      <span class="err" id="e4"></span>
    </div>
    <div class="row"><label><input type="checkbox" id="terms"> I accept the terms</label>
      <span class="err" id="e5"></span></div>
    <button type="submit">Place order</button>
  </form>
  <p id="result"></p>

  <script>
    $(function () {
      // live: remove red border when typing
      $("#name, #email").on("input", function () { $(this).removeClass("bad"); });

      $("#orderForm").on("submit", function (e) {
        e.preventDefault();
        $(".err").text("");
        $("input, select").removeClass("bad");
        let ok = true;

        let name = $("#name").val().trim();
        if (name === "") { $("#e1").text("Name required"); $("#name").addClass("bad"); ok = false; }

        let email = $("#email").val().trim();
        if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) {
          $("#e2").text("Valid email required"); $("#email").addClass("bad"); ok = false;
        }

        if ($("#city").val() === "") { $("#e3").text("Choose a city"); $("#city").addClass("bad"); ok = false; }

        let pay = $("input[name='pay']:checked").val();
        if (!pay) { $("#e4").text("Choose payment method"); ok = false; }

        if (!$("#terms").is(":checked")) { $("#e5").text("Please accept"); ok = false; }

        if (ok) {
          $("#result").html("Order placed for <b></b> in <i></i> via <u></u>.");
          $("#result b").text(name);
          $("#result i").text($("#city option:selected").text());
          $("#result u").text(pay);
          console.log($(this).serialize());   // name=...&email=...
        } else {
          $("#result").text("");
        }
      });
    });
  </script>
</body>
</html>
```

### Real-world example

Login and signup forms everywhere, checkout forms (Flipkart address form), IRCTC passenger details, and "Select All" checkboxes.

### Common mistakes

- Using `.val()` on a checkbox to know if it is ticked (use `.is(":checked")`).
- Forgetting `e.preventDefault()` in submit handler.
- Reading a radio group with `$("input[name='pay']").val()` (gives first radio value, not selected one; use `:checked`).
- `serialize()` skips fields without a `name` attribute.

### Check your understanding

1. How do you get the selected radio button's value?
2. What does `.serialize()` do?
3. Write jQuery to stop a form named `#f` from submitting if `#email` is empty.
4. Which method tells you if a checkbox is ticked?

---

## 26. JavaScript Libraries

### Simple explanation

A **library** is a collection of ready-made code that you can use in your project, so you do not write everything from scratch. You call the library's functions when you need them (you stay in control).

A **framework** (like Angular) is bigger and tells you how to structure your whole app (it calls your code).

Popular libraries:

| Library | Use |
|---|---|
| jQuery | Easy DOM, events, animation, Ajax |
| React | Build user interfaces from components |
| Lodash | Helpers for arrays/objects |
| Chart.js | Draw charts |
| Moment.js / Day.js | Dates |
| Axios | Make HTTP requests |
| Bootstrap JS, jQuery UI | Popups, date pickers, drag and drop |

Why use libraries?
- Saves time (less code).
- Tested by thousands of developers (fewer bugs).
- Works the same on different browsers.
- Large community and plugins.

Cost: extra file to download (slower load), you must learn it, and you may use only a small part of it.

How to add: via **CDN** (a link; fast, shared, cached) or by **downloading** the file and linking it locally (works offline). Always load the library **before** your own script. Put a fallback or use trusted sources.

**Analogy:** Cooking at home: you can grind your own masala from raw spices (plain JavaScript), or buy a **ready-made masala packet** (library). The packet saves time, but you pay for what you may not fully use.

### Code example: using two libraries

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Libraries</title>
  <!-- Library 1: jQuery from CDN -->
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
</head>
<body>
  <p id="p">Libraries save time.</p>
  <button id="b">Fade it</button>
  <p id="check"></p>

  <script>
    // Check whether the library loaded properly
    if (typeof jQuery === "undefined") {
      document.getElementById("check").textContent = "jQuery failed to load!";
    } else {
      document.getElementById("check").textContent = "jQuery version: " + $.fn.jquery;
      $("#b").click(function () { $("#p").fadeToggle(); });
    }
  </script>
</body>
</html>
```

### Real-world example

Most e-commerce sites use libraries for sliders, date pickers (IRCTC journey date), charts (stock apps) and maps (Google Maps API). Modern React sites like many startup apps are built entirely on a library.

### Common mistakes

- Loading the same library twice (or two jQuery versions) causing conflicts.
- Adding a heavy library for one small job.
- Using a CDN with no internet in the lab.
- Putting your script above the library script.

### Check your understanding

1. What is a JavaScript library? Name three.
2. Give two advantages and two disadvantages of using a library.
3. What is a CDN?
4. Difference between a library and a framework?

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

**Goal:** a page where the user enters the customer name, picks items and quantities, and gets a bill with GST. It has form validation. We build it first in **plain JavaScript**, then improve it with **jQuery** (adding effects, dynamic list, and cleaner code).

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

## Version 2: Enhanced with jQuery

Same idea. Changes made with jQuery:
- Shorter selection and event code.
- Rows **fade in** when added and **fade out** when removed.
- A live **"items in bill" counter** with a small animation.
- Red border on invalid fields using `addClass`.
- Mobile box accepts digits only while typing (live clean-up with `.on("input")`).
- Confirmation before clear.

Save as `teashop-jquery.html`.

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Chai Corner Bill (jQuery)</title>
  <script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>
  <style>
    body { font-family: Arial, sans-serif; background: #fff8ec; margin: 0; padding: 20px; }
    .wrap { max-width: 640px; margin: auto; background: white; padding: 20px;
            border-radius: 10px; box-shadow: 0 2px 8px #ccc; }
    h1 { color: #8a4b08; text-align: center; margin-top: 0; }
    .row { margin: 10px 0; }
    label { display: inline-block; width: 120px; }
    input, select { padding: 6px; }
    .bad { border: 2px solid red; }
    button { padding: 7px 14px; cursor: pointer; background: #8a4b08; color: white; border: none; border-radius: 4px; }
    button.small { padding: 3px 8px; background: #b22; }
    .error { color: red; font-size: 13px; margin-left: 120px; min-height: 16px; }
    table { width: 100%; border-collapse: collapse; margin-top: 15px; }
    th, td { border: 1px solid #ddd; padding: 6px; text-align: center; }
    th { background: #f3e0c2; }
    .total td { font-weight: bold; }
    #badge { display: inline-block; background: #2a7; color: white; border-radius: 12px;
             padding: 2px 10px; position: relative; }
    #banner { display: none; background: #dff5e1; padding: 8px; margin-top: 10px; border-radius: 4px; }
  </style>
</head>
<body>
  <div class="wrap">
    <h1>Chai Corner</h1>
    <div style="text-align:right">Items in bill: <span id="badge">0</span></div>

    <div class="row"><label for="cname">Customer</label>
      <input type="text" id="cname" placeholder="Name"></div>
    <div class="error" id="errName"></div>

    <div class="row"><label for="mobile">Mobile</label>
      <input type="text" id="mobile" maxlength="10" placeholder="10 digits"></div>
    <div class="error" id="errMobile"></div>

    <div class="row"><label for="item">Item</label>
      <select id="item">
        <option value="">-- choose --</option>
        <option value="Tea|10">Tea - Rs. 10</option>
        <option value="Coffee|15">Coffee - Rs. 15</option>
        <option value="Lemon Tea|12">Lemon Tea - Rs. 12</option>
        <option value="Samosa|20">Samosa - Rs. 20</option>
        <option value="Vada|12">Vada - Rs. 12</option>
      </select></div>
    <div class="error" id="errItem"></div>

    <div class="row"><label for="qty">Quantity</label>
      <input type="number" id="qty" value="1" min="1" style="width:70px">
      <button id="addBtn">Add to bill</button>
      <button id="clearBtn" style="background:#555">Clear</button></div>
    <div class="error" id="errQty"></div>

    <div id="banner"></div>

    <table>
      <thead><tr><th>Item</th><th>Price</th><th>Qty</th><th>Amount</th><th></th></tr></thead>
      <tbody id="billBody"></tbody>
      <tfoot id="billFoot"></tfoot>
    </table>
    <p id="msg"></p>
  </div>

  <script>
    $(function () {
      const GST_RATE = 0.05;
      let bill = [];

      // show/clear an error under a field; also mark the field
      function setError(errSel, fieldSel, text) {
        $(errSel).text(text);
        $(fieldSel).toggleClass("bad", text !== "");
        return text === "";
      }

      function validateCustomer() {
        let name = $("#cname").val().trim();
        let mobile = $("#mobile").val().trim();
        let a = setError("#errName", "#cname", name === "" ? "Please enter customer name" : "");
        let b = setError("#errMobile", "#mobile",
                         /^[6-9]\d{9}$/.test(mobile) ? "" : "Enter a valid 10-digit mobile number");
        return a && b;
      }

      function validateItem() {
        let qty = Number($("#qty").val());
        let a = setError("#errItem", "#item", $("#item").val() === "" ? "Please choose an item" : "");
        let b = setError("#errQty", "#qty",
                         (Number.isInteger(qty) && qty >= 1 && qty <= 50) ? "" : "Quantity must be a whole number 1 to 50");
        return a && b;
      }

      function render() {
        let $body = $("#billBody").empty();
        let $foot = $("#billFoot").empty();
        let subtotal = 0;
        let count = 0;

        $.each(bill, function (index, line) {
          let amount = line.price * line.qty;
          subtotal += amount;
          count += line.qty;
          $("<tr></tr>")
            .append($("<td></td>").text(line.name))
            .append($("<td></td>").text(line.price))
            .append($("<td></td>").text(line.qty))
            .append($("<td></td>").text(amount.toFixed(2)))
            .append($("<td></td>").append(
              $("<button class='small'>X</button>").attr("data-index", index)))
            .hide()
            .appendTo($body)
            .fadeIn(300);
        });

        if (bill.length > 0) {
          let gst = subtotal * GST_RATE;
          $foot.append(
            "<tr class='total'><td colspan='3'>Subtotal</td><td colspan='2'>Rs. " + subtotal.toFixed(2) + "</td></tr>" +
            "<tr class='total'><td colspan='3'>GST (5%)</td><td colspan='2'>Rs. " + gst.toFixed(2) + "</td></tr>" +
            "<tr class='total'><td colspan='3'>Grand Total</td><td colspan='2'>Rs. " + (subtotal + gst).toFixed(2) + "</td></tr>"
          );
        }
        $("#badge").text(count)
          .animate({ top: "-6px" }, 120)
          .animate({ top: "0px" }, 120);
      }

      function flash(text) {
        $("#banner").text(text).stop(true, true).fadeIn(200).delay(1500).fadeOut(400);
      }

      // digits only in the mobile box
      $("#mobile").on("input", function () {
        $(this).val($(this).val().replace(/\D/g, ""));
      });

      // clear red mark when the user changes the field
      $("#cname, #mobile, #item, #qty").on("input change", function () {
        $(this).removeClass("bad");
      });

      $("#addBtn").on("click", function () {
        // run both so that all errors show together
        let customerOk = validateCustomer();
        let itemOk = validateItem();
        if (!(customerOk && itemOk)) {
          $("#msg").text("Please fix the errors above.");
          return;
        }
        $("#msg").text("");

        let parts = $("#item").val().split("|");
        let name = parts[0], price = Number(parts[1]), qty = Number($("#qty").val());

        let existing = bill.find(function (l) { return l.name === name; });
        if (existing) { existing.qty += qty; }
        else { bill.push({ name: name, price: price, qty: qty }); }

        $("#qty").val(1);
        $("#item").val("");
        render();
        flash(qty + " x " + name + " added");
      });

      // delegation for remove buttons
      $("#billBody").on("click", "button", function () {
        let index = Number($(this).data("index"));
        $(this).closest("tr").fadeOut(250, function () {
          bill.splice(index, 1);
          render();
        });
      });

      $("#clearBtn").on("click", function () {
        if (bill.length === 0) { alert("The bill is already empty."); return; }
        if (confirm("Clear the whole bill?")) { bill = []; render(); flash("Bill cleared"); }
      });

      render();
    });
  </script>
</body>
</html>
```

**Extension tasks for students (homework):**
1. Add a discount coupon box (`TEA10` gives 10 percent off).
2. Save the bill in `localStorage` so it stays after refresh (`localStorage.setItem("bill", JSON.stringify(bill))`).
3. Add a "Print bill" button using `window.print()`.
4. Change the project into a **to-do list**: input, add, tick as done, delete, count remaining.

### Alternative small project: To-do list (quick version, jQuery)

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
