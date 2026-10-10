# Module 3: Server-Side Development with Node.js

**Course:** Web Application Development (MNCST509)
**Programme:** B.Tech CSE Minor, KTU, Semester 5
**Module:** 3 of the syllabus (11 contact hours)

This module is written for students who have **never built a server before**. Keep every class small: explain one idea, run one example, let students change it.

---

## Contents

1. Introduction to Node.js
   - 1.1 What is Node.js?
   - 1.2 Features and advantages
   - 1.3 Installing Node.js and npm
   - 1.4 Running a simple Node.js script
2. Working with Node.js Core Modules
   - 2.1 What is a module?
   - 2.2 File System: reading and writing files
   - 2.3 HTTP: creating a basic web server
   - 2.4 Working with file and directory paths
3. Building a Simple Web Server
   - 3.1 Using the http module to create a web server
   - 3.2 Handling basic routing
   - 3.3 Serving static files (HTML, CSS, JS)
4. Introduction to Express.js
   - 4.1 Installing Express.js
   - 4.2 Setting up a basic Express server
   - 4.3 Handling GET and POST requests
5. Exam questions (short answers)

## Suggested lesson plan

| Class | Topic |
|---|---|
| 1 | What is Node.js, features, advantages |
| 2 | Installing Node.js and npm, first script |
| 3 | Modules, reading and writing files |
| 4 | Paths (`path`, `__dirname`) |
| 5 | First web server with `http` |
| 6 | Routing |
| 7 | Serving HTML, CSS and JS files |
| 8 | Installing Express, first Express server |
| 9 | GET requests in Express |
| 10 | POST requests in Express (form data) |
| 11 | Revision and exam questions |

---

# 1. Introduction to Node.js

## 1.1 What is Node.js?

Until now, our JavaScript ran **only inside the browser** (Chrome, Edge). **Node.js** lets JavaScript run **directly on your computer**, outside the browser.

This means we can use JavaScript to build the **server**: the program on the other side of the internet that sends web pages and data to the browser.

**Analogy:** think of a restaurant.

```
  Customer (browser)  --->  Waiter  --->  Kitchen (server)
  "One masala dosa"                       makes the dosa
  Customer gets dosa  <---  Waiter  <---  sends it out
```

- The **browser** is the customer. It asks for things.
- The **server** is the kitchen. It prepares what was asked and sends it back.
- Before Node.js, JavaScript could only sit at the customer's table. Node.js lets JavaScript work in the kitchen too.

**Real world:** Netflix, PayPal, LinkedIn and Uber use Node.js for parts of their servers.

### Check your understanding
1. Where did JavaScript run before Node.js?
2. In the restaurant example, who is the browser and who is the server?

## 1.2 Features and advantages

| Feature | In simple words |
|---|---|
| **JavaScript everywhere** | Same language for the web page and the server. Learn one, use it for both. |
| **Fast** | Uses Google Chrome's V8 engine, which runs JavaScript very quickly. |
| **Non-blocking** | Does not sit and wait for slow work (like reading a file). It moves on and comes back when the work is done. |
| **Single thread, many users** | One worker handles many users by never standing idle. |
| **npm** | A huge free store of ready-made code packages. |
| **Free and open source** | Anyone can use it. |

**Analogy for "non-blocking": the smart waiter.**

- A **slow waiter** takes your order, goes to the kitchen and **stands there** until your dosa is ready. Other customers wait.
- A **smart waiter (Node.js)** gives your order to the kitchen, then takes the **next table's** order. When your dosa is ready, the kitchen rings a bell and the waiter brings it.

One smart waiter can serve many tables. That is why Node.js handles many users well.

**How Node.js is different from older servers (like PHP or Java):**

| Older servers | Node.js |
|---|---|
| Often give each user their own worker (thread) | One worker handles many users |
| Workers often wait while files or databases are read | Does not wait; picks up the result later |
| Server language is different from browser language | JavaScript on both sides |

**Note:** Node.js is not good for very heavy calculation (like video editing), because that keeps the one worker busy.

### Check your understanding
1. Explain "non-blocking" using the waiter example.
2. Give three advantages of Node.js.

## 1.3 Installing Node.js and npm

**npm** (Node Package Manager) comes with Node.js. It downloads ready-made code packages for you.

**Analogy:** npm is like the **Play Store** for code. You need a feature, you install it with one command.

**Steps:**

1. Go to https://nodejs.org and download the **LTS** version (LTS means "Long Term Support", the stable one).
2. Install it like any normal program (click Next, Next, Finish).
3. Open a terminal (Command Prompt on Windows, Terminal on Mac) and check:

```
node -v
npm -v
```

If both show a version number (for example `v22.11.0` and `10.9.0`), it worked.

**Starting a project with npm:**

```
mkdir myapp
cd myapp
npm init -y
```

`npm init -y` creates a file called `package.json`. It is the **ID card** of your project: its name, version, and the list of packages it needs.

To install a package (for example Express, used in Section 4):

```
npm install express
```

This downloads the package into a folder called `node_modules` and writes its name into `package.json`.

### Check your understanding
1. What is npm? Give one command that uses it.
2. What is `package.json` for?

## 1.4 Running a simple Node.js script

Create a file `hello.js`:

```javascript
console.log("Hello from Node.js!");

let a = 10;
let b = 20;
console.log("Sum is", a + b);
```

Run it in the terminal, from the same folder:

```
node hello.js
```

Output:

```
Hello from Node.js!
Sum is 30
```

There is no browser and no HTML. Node.js runs the file and prints to the terminal.

**Common mistakes:**
- Running `node hello.js` from the wrong folder. Use `cd` to go to the folder first.
- Using `alert()` or `document`. These exist only in the browser, not in Node.js.

### Try it
Change the script to print your name and the multiplication table of 5.

---

# 2. Working with Node.js Core Modules

## 2.1 What is a module?

A **module** is a file of ready-made code. Node.js comes with some built in, called **core modules**. You don't need to install them.

| Module | Used for |
|---|---|
| `fs` | reading and writing files ("file system") |
| `http` | making a web server |
| `path` | working with file and folder paths |

You load a module with `require`:

```javascript
const fs = require("fs");
```

**Analogy:** modules are like tools in a toolbox. `require` means "take the screwdriver out of the box".

## 2.2 File System: reading and writing files

**Write a file:**

```javascript
// write.js
const fs = require("fs");

fs.writeFile("notes.txt", "Hello students!", function (err) {
  if (err) {
    console.log("Error:", err);
    return;
  }
  console.log("File saved");
});
```

Run `node write.js`. A file `notes.txt` appears in the folder.

**Read a file:**

```javascript
// read.js
const fs = require("fs");

fs.readFile("notes.txt", "utf8", function (err, data) {
  if (err) {
    console.log("Error:", err);
    return;
  }
  console.log("File content:", data);
});
```

Output:

```
File content: Hello students!
```

**Add to a file (without deleting old content):**

```javascript
fs.appendFile("notes.txt", "\nNew line added", function (err) {
  if (err) console.log(err);
});
```

**What is the `function (err, data)` part?** It is a **callback**: a function Node.js calls **after** the work is finished. This is the "kitchen rings the bell" from the waiter example.

**Sync version (simpler, but blocks):**

```javascript
const data = fs.readFileSync("notes.txt", "utf8");
console.log(data);
```

`readFileSync` waits until the file is read. It is fine for small scripts, but servers should use `readFile` so they don't block other users.

**Common mistakes:**
- Forgetting `"utf8"`. Then you get strange output like `<Buffer 48 65 6c ...>` instead of text.
- Reading a file that does not exist. The `err` tells you `ENOENT` (meaning "file not found").

### Check your understanding
1. Write a Node.js script to read `data.txt` and print it.
2. What is the difference between `writeFile` and `appendFile`?
3. What is the difference between `readFile` and `readFileSync`?

## 2.3 HTTP: creating a basic web server

The `http` module lets Node.js answer requests from a browser.

```javascript
// server.js
const http = require("http");

const server = http.createServer(function (req, res) {
  res.writeHead(200, { "Content-Type": "text/plain" });
  res.end("Hello, World!");
});

server.listen(3000, function () {
  console.log("Server running at http://localhost:3000");
});
```

Run `node server.js`, then open http://localhost:3000 in the browser. You see **Hello, World!**

What each part means:

| Code | Meaning |
|---|---|
| `createServer(function (req, res) {...})` | Make a server. The function runs every time someone visits. |
| `req` | the **request**: what the browser asked for |
| `res` | the **response**: what we send back |
| `writeHead(200, ...)` | `200` means "OK". `Content-Type` says what kind of data we are sending. |
| `res.end("...")` | send the reply and finish |
| `listen(3000)` | wait for visitors on port 3000 |
| `localhost` | your own computer |

**Analogy:** a **port** is like a counter number in a bank. The building (your computer) has many counters; our server sits at counter 3000.

To stop the server, press `Ctrl + C` in the terminal.

**Common mistakes:**
- Forgetting `res.end()`. The browser keeps loading forever.
- Changing the code and not restarting the server. Stop it with `Ctrl + C` and run `node server.js` again.

## 2.4 Working with file and directory paths

Different computers write paths differently (Windows uses `\`, Mac and Linux use `/`). The `path` module builds paths correctly on any computer.

```javascript
// paths.js
const path = require("path");

console.log(__dirname);   // the folder this file is in
console.log(__filename);  // full path of this file

const filePath = path.join(__dirname, "public", "index.html");
console.log(filePath);    // e.g. /home/anu/myapp/public/index.html

console.log(path.basename(filePath));  // index.html
console.log(path.extname(filePath));   // .html
console.log(path.dirname(filePath));   // /home/anu/myapp/public
```

| Code | Gives |
|---|---|
| `__dirname` | folder of the current file |
| `path.join(a, b, c)` | joins pieces into one correct path |
| `path.basename(p)` | just the file name |
| `path.extname(p)` | just the extension (`.html`, `.css`) |
| `path.dirname(p)` | just the folder part |

**Analogy:** `path.join` is like writing a full postal address in the right order. You give the parts (house, street, town) and it puts them together properly.

**Why it matters:** in Section 3 we use `path.join(__dirname, ...)` to find our HTML files, and `path.extname` to know if a file is HTML, CSS or JS.

### Check your understanding
1. What does `__dirname` give you?
2. What does `path.extname("style.css")` return?

---

# 3. Building a Simple Web Server

## 3.1 Using the http module to create a web server

We already made one in 2.3. Here is the full journey of one request:

```
 1. You type  http://localhost:3000/about  in the browser
                     |
                     v
 2. Browser sends a REQUEST:   GET /about
                     |
                     v
 3. Node.js server runs our function(req, res)
    - looks at req.url  ->  "/about"
    - decides what to send
                     |
                     v
 4. Server sends a RESPONSE:   200 OK + the page
                     |
                     v
 5. Browser shows the page
```

Two useful parts of `req`:
- `req.url`: the path asked for, like `/` or `/about`
- `req.method`: the type of request, like `GET` (asking for something) or `POST` (sending something)

## 3.2 Handling basic routing

**Routing** means sending a different reply for each URL.

**Analogy:** a college office. "Fees" goes to counter 1, "Certificates" to counter 2. Anything else: "Sorry, wrong counter."

```javascript
// routes.js
const http = require("http");

const server = http.createServer(function (req, res) {
  res.setHeader("Content-Type", "text/html");

  if (req.url === "/") {
    res.writeHead(200);
    res.end("<h1>Home Page</h1><p>Welcome to our college</p>");
  } else if (req.url === "/about") {
    res.writeHead(200);
    res.end("<h1>About Us</h1><p>Started in 1995</p>");
  } else if (req.url === "/contact") {
    res.writeHead(200);
    res.end("<h1>Contact</h1><p>Phone: 0471 123456</p>");
  } else {
    res.writeHead(404);
    res.end("<h1>404 - Page Not Found</h1>");
  }
});

server.listen(3000, function () {
  console.log("Open http://localhost:3000");
});
```

Try `/`, `/about`, `/contact`, and `/xyz` in the browser.

**Status codes to remember:**

| Code | Meaning |
|---|---|
| 200 | OK, here it is |
| 404 | Not found |
| 500 | Server error (something broke on our side) |

### Check your understanding
1. What is routing?
2. Which property of `req` tells us the URL asked for?
3. Add a `/courses` route that shows a list of three courses.

## 3.3 Serving static files (HTML, CSS, JS)

Writing HTML inside JavaScript strings gets messy. Instead, keep real files in a folder and let the server send them. These are called **static files** because the server sends them as they are, without changing them.

**Folder structure:**

```
myapp/
  server.js
  public/
    index.html
    style.css
    script.js
```

**public/index.html**

```html
<!DOCTYPE html>
<html>
<head>
  <title>My Node Site</title>
  <link rel="stylesheet" href="/style.css">
</head>
<body>
  <h1>Hello from a real HTML file!</h1>
  <button id="btn">Click me</button>
  <script src="/script.js"></script>
</body>
</html>
```

**public/style.css**

```css
body { font-family: Arial; background: #f0f8ff; text-align: center; }
h1 { color: darkblue; }
```

**public/script.js**

```javascript
document.getElementById("btn").onclick = function () {
  alert("JavaScript file loaded from the server!");
};
```

**server.js**

```javascript
const http = require("http");
const fs = require("fs");
const path = require("path");

// which Content-Type to send for each file extension
const types = {
  ".html": "text/html",
  ".css": "text/css",
  ".js": "text/javascript"
};

const server = http.createServer(function (req, res) {
  // "/" means the home page
  let fileName = req.url === "/" ? "index.html" : req.url;
  let filePath = path.join(__dirname, "public", fileName);
  let ext = path.extname(filePath);

  fs.readFile(filePath, function (err, data) {
    if (err) {
      res.writeHead(404, { "Content-Type": "text/html" });
      res.end("<h1>404 - File Not Found</h1>");
      return;
    }
    res.writeHead(200, { "Content-Type": types[ext] || "text/plain" });
    res.end(data);
  });
});

server.listen(3000, function () {
  console.log("Open http://localhost:3000");
});
```

**What happens:** the browser asks for `/`, gets `index.html`, sees the `<link>` and `<script>` tags, and then asks the server for `/style.css` and `/script.js`. Our server finds each file in `public` and sends it with the right `Content-Type`.

**Analogy:** the server is a librarian. You ask for a book by name, the librarian finds it on the shelf (`public` folder) and hands it over. If the book is not there: "404, not found."

**Common mistakes:**
- Wrong `Content-Type`. If CSS is sent as `text/plain`, the browser ignores the styles.
- Putting files outside the `public` folder.

### Check your understanding
1. What are static files?
2. Why do we need different `Content-Type` values?
3. Which two modules, besides `http`, did we use here, and why?

---

# 4. Introduction to Express.js

Section 3 worked, but we wrote a lot of `if/else` and file code by hand. **Express.js** is a package that does this work for us in fewer lines.

**Analogy:** building a server with only `http` is like cooking everything from raw rice and spices. Express is like a kitchen with ready-made masala: same food, much faster.

## 4.1 Installing Express.js

```
mkdir express-app
cd express-app
npm init -y
npm install express
```

Express is not a core module, so we install it with npm. You will now see `node_modules` and `"express"` listed in `package.json`.

## 4.2 Setting up a basic Express server

```javascript
// app.js
const express = require("express");
const app = express();

app.get("/", function (req, res) {
  res.send("Hello from Express!");
});

app.listen(3000, function () {
  console.log("Server running at http://localhost:3000");
});
```

Run `node app.js` and open http://localhost:3000.

Compare with the `http` version:

| With http | With Express |
|---|---|
| `if (req.url === "/about")` | `app.get("/about", ...)` |
| `res.writeHead(200, {...}); res.end(...)` | `res.send(...)` |
| Read files and set Content-Type by hand | `app.use(express.static("public"))` |
| Send 404 yourself | Express sends 404 for unknown routes |

**Serving static files is one line in Express:**

```javascript
app.use(express.static("public"));
```

Now every file inside `public` (HTML, CSS, JS, images) is served automatically.

## 4.3 Handling GET and POST requests

| Request | Used when | Example |
|---|---|---|
| **GET** | the browser **asks** for something | open a page, search |
| **POST** | the browser **sends** data to save | submit a form, sign up |

**Analogy:** GET is asking the shopkeeper "what is the price of tea?". POST is handing over a filled admission form.

### GET routes

```javascript
// get.js
const express = require("express");
const app = express();

// simple GET
app.get("/welcome", function (req, res) {
  res.send("Welcome to Express");
});

// route parameter: /student/25  ->  req.params.id is "25"
app.get("/student/:id", function (req, res) {
  res.send("Student roll number: " + req.params.id);
});

// query string: /search?name=anu  ->  req.query.name is "anu"
app.get("/search", function (req, res) {
  res.send("You searched for: " + req.query.name);
});

app.listen(3000, function () {
  console.log("Open http://localhost:3000/welcome");
});
```

Try:
- http://localhost:3000/welcome
- http://localhost:3000/student/25
- http://localhost:3000/search?name=anu

### POST route with a form

```javascript
// post.js
const express = require("express");
const app = express();

// lets Express read form data sent by POST
app.use(express.urlencoded({ extended: true }));

// GET: show the form
app.get("/", function (req, res) {
  res.send(`
    <h2>Fest Registration</h2>
    <form action="/register" method="POST">
      Name: <input name="name"><br><br>
      Department: <input name="dept"><br><br>
      <button type="submit">Register</button>
    </form>
  `);
});

// POST: receive the form data
app.post("/register", function (req, res) {
  const name = req.body.name;
  const dept = req.body.dept;
  console.log("New registration:", name, dept);
  res.send("<h2>Thank you " + name + " from " + dept + "! You are registered.</h2>");
});

app.listen(3000, function () {
  console.log("Open http://localhost:3000");
});
```

**What happens:**
1. You open `/`. A GET request shows the form.
2. You fill it and click Register. The browser sends a **POST** request to `/register` with the data.
3. Express puts the data in `req.body`, and we send a thank-you message.

**Note:** if data is sent as JSON (for example from React in Module 4), add `app.use(express.json());` too.

**Common mistakes:**
- Forgetting `app.use(express.urlencoded(...))`. Then `req.body` is `undefined`.
- Form `method="GET"` when the route is `app.post`. Express then says "Cannot GET /register".
- Not restarting the server after changing code.

### Check your understanding
1. What is the difference between GET and POST?
2. Write an Express route that answers `/hello` with "Hello students".
3. What is `req.body` used for?
4. What is the difference between `req.params` and `req.query`?

### Class activity (15 min)
Students add a `/menu` GET route that shows a canteen menu, and a form that POSTs a food order to `/order`. The server replies "Your order for (item) is placed."

---

# 5. Exam Questions (short answers)

**Q1. What is the purpose of npm? How is it used in Node.js projects? (3 marks)**
npm (Node Package Manager) installs and manages ready-made code packages. `npm init -y` creates `package.json`, which lists the project's details and packages. `npm install express` downloads a package into `node_modules` and records it in `package.json`. Anyone can then run `npm install` to get all the packages the project needs.

**Q2. Write a Node.js http server that responds with "Hello, World!" (3 marks)**
See the code in section 2.3.

**Q3. Key features and advantages of Node.js. How is it different from traditional server-side technologies? (5 marks)**
Write the features table from 1.2 (JavaScript everywhere, fast V8 engine, non-blocking, single thread handling many users, npm, open source). Then write the "older servers versus Node.js" table, and explain non-blocking with the waiter example.

**Q4. Node.js script using fs to read a file and display its content (4 marks)**
See `read.js` in section 2.2.

**Q5. Explain how a basic web server is created using the http module. How is routing handled? (5 marks)**
1. `require("http")`
2. `http.createServer(function (req, res) {...})`. The function runs for every request.
3. Use `res.writeHead` to set the status and type, and `res.end` to send the reply.
4. `server.listen(3000)` starts it.
Routing: check `req.url` (and `req.method`) with `if/else`, send a different reply for each path, and return 404 for unknown paths. Give the code from 3.2.

**Q6. Express.js program to handle GET at /welcome and send "Welcome to Express" (4 marks)**

```javascript
const express = require("express");
const app = express();

app.get("/welcome", function (req, res) {
  res.send("Welcome to Express");
});

app.listen(3000);
```

**More practice:**
1. What is a core module? Name three. (3 marks)
2. Explain `path.join` and `__dirname` with an example. (3 marks)
3. Write a Node.js server that serves `index.html` and `style.css` from a `public` folder. (5 marks)
4. Explain GET and POST in Express with an example of a form. (6 marks)
