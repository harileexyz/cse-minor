# Module 3: Node.js and Express.js

**Course:** Web Application Development (MNCST509)
**Programme:** B.Tech CSE Minor, Semester 5 (KTU, Kerala)
**Module duration:** 11 contact hours
**Prior knowledge:** HTML, CSS, JavaScript, jQuery (Modules 1 and 2)

---

## Table of Contents

1. Learning outcomes
2. Suggested lesson plan (11 hours)
3. Two diagrams to draw first (request/response cycle and event loop)
4. Topic 1: Introduction to Node.js
5. Topic 2: Working with Node.js core modules (fs, http, path)
6. Topic 3: Building a simple web server (routing and static files)
7. Topic 4: Introduction to Express.js
8. Mini-project: College Notice Board
9. Question bank (KTU exam style) with model answers
10. Classroom activities
11. Quick revision sheet

---

## 1. Learning outcomes

After this module, a student will be able to:

- **LO1:** Explain what Node.js is, and list its main features and advantages.
- **LO2:** Compare Node.js with traditional server-side technologies such as PHP with Apache and Java thread-per-request servers.
- **LO3:** Install Node.js and npm, create a `package.json`, install packages and run a script.
- **LO4:** Use the core modules `fs`, `http` and `path` to read and write files, build a server and handle file paths.
- **LO5:** Build a web server with only the `http` module, with basic routing and static file serving using correct `Content-Type` headers.
- **LO6:** Build the same server in Express.js, handle GET and POST requests, read route parameters, query strings and request bodies, and serve static files.
- **LO7:** Explain what middleware is and write a simple custom middleware.

---

## 2. Suggested lesson plan (11 contact hours)

Assume one contact hour = 50 to 60 minutes. Plan below uses 11 hours, split into 8 sessions.

| Session | Time | Topic | Method |
|---|---|---|---|
| 1 | 1 hr | Why Node.js? Features, single thread, event loop, non-blocking I/O. Compare with PHP/Apache and Java | Talk + board diagram + restaurant analogy |
| 2 | 2 hr | Install Node and npm, `node -v`, `npm init`, `package.json`, installing packages, first script | Live demo + lab (every student installs) |
| 3 | 2 hr | `fs` module: readFile, writeFile, appendFile; sync vs callback vs promises | Code-along + 3 exercises |
| 4 | 1 hr | `path` module, `__dirname`, `path.join`, `path.extname` | Code-along + quick quiz |
| 5 | 1.5 hr | `http` module: first server, `req` and `res`, status codes, headers | Live coding |
| 6 | 1.5 hr | Routing with `req.url` and `req.method`; serving static files with Content-Type | Lab |
| 7 | 1.5 hr | Express: install, GET, POST, params, query, `express.json()`, `express.urlencoded()`, `express.static`, middleware | Code-along |
| 8 | 0.5 hr + homework | Mini-project hand-out, revision, doubt clearing | Group work |

Total = 1 + 2 + 2 + 1 + 1 + 1.5 + 1.5 + 1.5 + 0.5 = 11.0 hours of contact time (the last 0.5 hour is the project briefing; the project itself is finished as homework or in a lab slot).

**Suggested 10-minute rhythm inside each session:** 10 min idea, 10 min analogy and diagram, 20 min live code, 10 min students try, 5 min check-your-understanding questions.

**Before Session 2, ask students to:**
- Have a laptop with internet.
- Install VS Code (a free code editor).
- Be ready to open a terminal (Command Prompt or PowerShell on Windows, Terminal on Mac and Linux).

---

## 3. Two diagrams to draw first

### 3.1 The request/response cycle

Every web page you open follows this path. Draw this on the board in Session 1 and keep coming back to it.

```
   BROWSER (client)                                   SERVER (Node.js)
 +------------------+                              +----------------------+
 | User types       |   1. HTTP REQUEST            |                      |
 | http://site.com  | ---------------------------> | 4. Server receives   |
 | /notices         |   GET /notices HTTP/1.1      |    request (req)     |
 |                  |   Host: site.com             |                      |
 |                  |                              | 5. Server decides:   |
 |                  |                              |    - which route?    |
 |                  |                              |    - read a file?    |
 |                  |                              |    - ask database?   |
 |                  |                              |                      |
 |                  |   2. HTTP RESPONSE           | 6. Server builds     |
 | 3. Browser shows | <--------------------------- |    response (res)    |
 |    the page      |   HTTP/1.1 200 OK            |                      |
 |                  |   Content-Type: text/html    |                      |
 |                  |   <html>...</html>           |                      |
 +------------------+                              +----------------------+

 A request has:  method (GET/POST), URL, headers, optional body
 A response has: status code (200/404/500), headers, body
```

**Plain meaning:** the browser asks, the server answers. Node.js gives us the `req` object (the question) and the `res` object (the answer we are writing).

### 3.2 The event loop (how one thread serves many people)

```
                      YOUR JAVASCRIPT CODE (ONE THREAD)
                      +-------------------------------+
   new request  ----> |      CALL STACK               |
   arrives            |  runs one function at a time  |
                      +---------------+---------------+
                                      |
                  slow work? (file, network, database)
                                      |
                                      v
                      +-------------------------------+
                      |  HELPERS (OS / libuv threads) |
                      |  do the slow work in the      |
                      |  background                   |
                      +---------------+---------------+
                                      |
                              work finished
                                      |
                                      v
                      +-------------------------------+
                      |  CALLBACK QUEUE               |
                      |  [cb1] [cb2] [cb3] ...        |
                      +---------------+---------------+
                                      |
                      +---------------v---------------+
                      |         EVENT LOOP            |
                      |  "Is the call stack empty?    |
                      |   Yes -> push next callback." |
                      +-------------------------------+
                                      |
                                      v
                          back to the CALL STACK
```

**Plain meaning:** Node has only one worker for JavaScript. When it gets slow work, it hands it to a helper and moves on to the next customer. When the helper is done, the event loop calls your callback function.

---

# 4. Topic 1: Introduction to Node.js

## 4.1 What is Node.js?

**Simple explanation.** Until about 2009, JavaScript ran only inside a web browser (Chrome, Firefox). Node.js lets us run JavaScript **outside** the browser, on our own computer or on a server. It is built on Chrome's V8 engine (the part of Chrome that understands and runs JavaScript quickly).

Important points:
- Node.js is **not** a language. The language is JavaScript.
- Node.js is **not** a framework. It is a **runtime** (a program that can run JavaScript).
- With Node.js you can write command-line tools, web servers, APIs, and more.

**Analogy.** Think of JavaScript as a person who can only work inside one shop (the browser). Node.js is a licence that lets the same person work anywhere: in the godown, in the office, in the kitchen. The skills are the same; only the place changes.

### Features and advantages of Node.js

| Feature | What it means in simple words | Advantage |
|---|---|---|
| **Single thread** | JavaScript code runs in one main line of work | Simple to write; no worry about two threads changing the same data at once |
| **Event loop** | A loop that picks up finished jobs and runs their callbacks | One thread can serve thousands of users |
| **Non-blocking I/O** | While waiting for a file or database, Node does other work | Fast under heavy load; does not waste time waiting |
| **npm ecosystem** | npm is the world's largest library store for code (over two million packages) | Do not write everything from zero; install and use |
| **JavaScript everywhere** | Same language in browser and server | One language to learn; same team can do front end and back end; JSON works naturally |
| **Fast (V8 engine)** | V8 turns JavaScript into machine code | Good speed |
| **Cross-platform** | Runs on Windows, Mac and Linux | Same code everywhere |
| **Good for real-time apps** | Chat, live tracking, notifications | Many open connections cost little memory |
| **Open source and large community** | Free, with lots of tutorials and help | Easy to find answers |

**Analogy for single thread plus non-blocking.** Picture a small Kerala tea shop with **one** master. A customer orders tea. The master puts milk on the stove (slow work). He does **not** stand and stare at the milk. He takes the next order, wraps a parcel, and returns when the milk boils. One master serves many customers, because he never waits idle.

## 4.2 Single thread, event loop and non-blocking I/O in detail

**What is I/O?** Input/Output: reading a file, writing a file, talking to a database, calling another website. These are **slow** compared to the CPU. A CPU can do millions of steps while a disk reads one file.

**Blocking code:** the program stops and waits until the slow work is done.
**Non-blocking code:** the program starts the slow work, carries on, and gets told when it finishes (through a callback, a promise, or `async/await`).

**Analogy: restaurant.**

- **Blocking (bad waiter):** takes your order, walks to the kitchen, stands there until the biryani is ready, brings it to you, and only then goes to the next table. Ten tables means a very long wait for the tenth.
- **Non-blocking (Node waiter):** takes your order, hands the slip to the kitchen, goes to the next table. When the kitchen rings the bell, he serves that dish. One waiter handles ten tables.

The **kitchen** is the operating system and helper threads. The **bell** is the event loop. The **order slip with "call me when ready"** is the callback.

### Code example: blocking and non-blocking side by side

Create `blocking-demo.js`:

```js
// blocking-demo.js
// Shows the difference between blocking and non-blocking code.

console.log('1. Start');

// Non-blocking: timer runs in the background
setTimeout(() => {
  console.log('3. This came after 2 seconds (non-blocking)');
}, 2000);

console.log('2. End of main code');

// Blocking: this loop holds the one thread for about 3 seconds
const start = Date.now();
while (Date.now() - start < 3000) {
  // doing nothing, but nobody else can run now
}
console.log('4. Blocking loop finished after 3 seconds');
```

Run:

```bash
node blocking-demo.js
```

Expected output (the first two lines appear at once, the last two after about 3 seconds):

```
1. Start
2. End of main code
4. Blocking loop finished after 3 seconds
3. This came after 2 seconds (non-blocking)
```

**Why is line 3 printed after line 4?** The timer was set for 2 seconds, but the one thread was busy in the `while` loop for 3 seconds. The timer callback had to wait in the queue until the thread was free. This shows the danger of blocking code: **one blocked thread blocks all users**.

**Real-world example.** Netflix moved parts of its web layer to Node.js to cut start-up time. PayPal rebuilt some web apps in Node.js and reported faster response with fewer files and fewer lines. LinkedIn moved its mobile backend to Node.js to handle many connections with fewer servers. Uber uses Node.js for services that handle huge numbers of small, quick requests (such as matching riders and drivers). All of them have one thing in common: **many users, lots of waiting for data, small amount of calculation**. That is exactly what Node.js is good at.

**Common mistakes**
- Thinking Node.js is a new language. It is JavaScript.
- Thinking "single thread" means "can serve only one user". It serves many, because it does not wait.
- Writing heavy calculations (for example, finding primes up to a billion) in the main thread. This blocks everyone. Node is for I/O-heavy work, not for heavy CPU work.
- Using `Sync` functions inside a running server.

**Check your understanding**
1. What does "non-blocking I/O" mean? Give a restaurant example.
2. Why is line 3 printed last in the code above even though its timer is only 2 seconds?
3. Name three companies that use Node.js and say why it suits them.
4. Is Node.js a language, a framework or a runtime?

## 4.3 How Node.js differs from traditional server-side technologies

### Traditional model 1: PHP with Apache

Apache is a web server program. For a PHP site, Apache usually creates (or reuses) a **separate process or thread for each request**. Each one runs the PHP script from top to bottom, sends the result and finishes. If the script waits for a database, **that process or thread waits too**, and it holds memory while waiting.

### Traditional model 2: Java thread-per-request

In a classic Java servlet container (such as Tomcat), each incoming request is given **one thread** from a pool. That thread does all the work for the request, including waiting for the database. If 1,000 users come at once, you need about 1,000 threads. Each thread uses memory (often around 1 MB for its stack). When the pool is full, new users **wait in a line**.

### Node.js model

One main thread plus the event loop. A waiting request does **not** hold a thread. Node simply remembers "when the database answers, run this callback".

```
THREAD-PER-REQUEST (PHP/Apache, classic Java)
  User 1 --> Thread 1 [work][....waiting for DB....][work]
  User 2 --> Thread 2 [work][....waiting for DB....][work]
  User 3 --> Thread 3 [work][....waiting for DB....][work]
  (many users = many threads = more memory)

NODE.JS (one thread + event loop)
  Thread: [U1 work][U2 work][U3 work][U1 cb][U2 cb][U3 cb]
          (waiting is done by OS in background; thread never idles)
```

### Comparison table

| Point | PHP + Apache | Java (thread-per-request) | Node.js |
|---|---|---|---|
| Language | PHP | Java | JavaScript |
| Request handling | Process/thread per request | Thread per request | Single thread + event loop |
| While waiting for DB/file | That thread/process waits (blocked) | That thread waits (blocked) | Thread is free; callback runs later |
| Memory under many users | High | High | Low |
| Best for | Content sites, CMS (WordPress) | Large enterprise systems, heavy computing | Real-time apps, APIs, many connections |
| Front end and back end language | Different | Different | Same (JavaScript) |
| Weak point | Slower under huge load | Heavy and more code | Heavy CPU work blocks the thread |
| Server software | Needs Apache or Nginx separately | Needs Tomcat or similar | Server is written in your own code (`http` module) |

**Analogy: three types of office counters.**
- **PHP/Apache and Java:** a college office where each student gets **one clerk** who stays with them from start to finish, even while the student goes off to find a missing certificate. The clerk sits idle. For 500 students you need 500 clerks.
- **Node.js:** one clerk who takes your form, tells you "come back after ten minutes", takes the next form, and calls you when the stamp is ready.

**Real-world example.** IRCTC-like systems face bursts of users at 10:00 AM for Tatkal booking. A thread-per-request design needs very many threads at that moment. An event-driven Node.js layer in front can hold many waiting connections cheaply. (This is an illustration; real systems use many technologies together.) Many companies use Node.js as a thin "front" layer that talks to older systems behind it.

**Common mistakes**
- Saying "Node.js is always faster". It is better for I/O-heavy work, not for heavy calculation.
- Saying "Node.js has no threads at all". Node uses background threads for some jobs (like file operations). Only **your JavaScript code** runs on one thread.
- Mixing up Apache (a web server program) with PHP (a language).

**Check your understanding**
1. What happens to a Java servlet thread while it waits for a database?
2. Give two differences between PHP/Apache and Node.js.
3. When is Node.js a poor choice?

## 4.4 Installing Node.js and npm

**What is npm?** npm stands for **Node Package Manager**. It comes with Node.js. It does two jobs:
1. It is an **online store** (registry) of free code packages.
2. It is a **command-line tool** to download those packages into your project and to run project scripts.

**Analogy.** npm is like a **supermarket plus a delivery boy**. The registry is the supermarket shelf (packages like `express`, `lodash`). The `npm install` command is the delivery boy who brings the item to your kitchen (the `node_modules` folder) and writes it into your shopping list (`package.json`).

### Installation steps

Always download the **LTS** (Long Term Support) version from **https://nodejs.org**. LTS is the stable version for normal use.

**Windows**
1. Go to nodejs.org and click the LTS button to download the `.msi` installer.
2. Double-click it. Click Next, accept the licence, keep the default options (make sure "Add to PATH" stays ticked).
3. Finish. Close any open terminal and open a **new** one.

**macOS**
- Download the `.pkg` installer from nodejs.org and run it, **or** use Homebrew:

```bash
brew install node
```

**Linux (Ubuntu or Debian)**

```bash
sudo apt update
sudo apt install nodejs npm
```

(The version from `apt` may be old. For the newest LTS, use the official instructions on nodejs.org or a tool called `nvm`, Node Version Manager.)

### Checking that it worked

```bash
node -v
npm -v
```

Expected output (your numbers will be different):

```
v20.11.1
10.2.4
```

If you see "command not found" or "not recognized", close the terminal, open a new one, and try again. If it still fails, the PATH was not set; reinstall.

**Try the REPL.** Typing just `node` opens an interactive prompt (REPL = Read, Evaluate, Print, Loop). It is like the browser console.

```bash
node
> 2 + 3
5
> "Kerala".toUpperCase()
'KERALA'
> .exit
```

### npm init and package.json

**package.json** is the identity card and shopping list of a project. It stores the project name, version, start command and the list of packages it needs.

Create a project:

```bash
mkdir my-first-app
cd my-first-app
npm init -y
```

`-y` means "say yes to all the questions". Without `-y`, npm asks you name, version, description and so on one by one.

Generated `package.json`:

```json
{
  "name": "my-first-app",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

Meaning of key fields:

| Field | Meaning |
|---|---|
| `name`, `version` | Project name and version number |
| `main` | The first file to run |
| `scripts` | Short commands you can run with `npm run <name>` |
| `dependencies` | Packages needed when the app runs |
| `devDependencies` | Packages needed only while developing (for example, testing tools) |

### Installing packages

```bash
npm install express
```

What happens:
1. npm downloads `express` and the packages it needs into a new folder `node_modules/`.
2. It adds a line in `package.json` under `"dependencies"`.
3. It creates `package-lock.json`, which locks exact versions so everyone on the team gets the same code.

After this, `package.json` has:

```json
"dependencies": {
  "express": "^4.19.2"
}
```

(`^` means "this version or a newer compatible one".)

More commands:

| Command | What it does |
|---|---|
| `npm install` | Installs everything listed in `package.json` (use after cloning a project) |
| `npm install <pkg>` | Installs a package and saves it in dependencies |
| `npm install <pkg> --save-dev` or `-D` | Saves in devDependencies |
| `npm install -g <pkg>` | Installs globally, usable from anywhere (for tools such as `nodemon`) |
| `npm uninstall <pkg>` | Removes a package |
| `npm list` | Shows installed packages |
| `npm run <script>` | Runs a script from the `scripts` section |
| `npm start` | Shortcut for `npm run start` |

**Adding your own script.** Edit `package.json`:

```json
"scripts": {
  "start": "node index.js",
  "dev": "nodemon index.js"
}
```

Now `npm start` runs `node index.js`.

**Important rules**
- Never upload `node_modules` to Git or share it by pen drive. It is big and can be rebuilt with `npm install`. Add it to `.gitignore`.
- Share `package.json` and `package-lock.json`.

### Purpose of npm (exam-ready summary)

1. Download and install third-party packages.
2. Record the project's dependencies in `package.json`.
3. Manage versions (`package-lock.json`).
4. Run scripts (`npm start`, `npm run dev`).
5. Publish your own packages for others.

**Real-world example.** A typical company Node.js project has hundreds of packages (Express for the server, `jsonwebtoken` for login tokens, `mongoose` for the database, and so on). A new developer joining just runs `git clone` then `npm install`, and the whole project is ready in a minute.

**Common mistakes**
- Running `npm install` in the wrong folder (always check that `package.json` is in the folder you are in).
- Naming a project folder or file `express` (it clashes with the package of the same name).
- Deleting `package.json` and then wondering why the packages vanish from the list.
- Committing `node_modules`.
- Forgetting to open a new terminal after installing Node on Windows.

**Check your understanding**
1. What do `node -v` and `npm -v` show?
2. What is the difference between `dependencies` and `devDependencies`?
3. What does `npm init -y` do?
4. A friend sends you a project without `node_modules`. What one command makes it work?

## 4.5 Running a simple Node.js script

**Simple explanation.** A Node.js script is a normal `.js` file. We run it using the command `node filename.js`. There is no browser, no HTML. The output appears in the terminal.

**Analogy.** The browser is a stage with a screen (the page). Running a Node script is like a **radio**: no screen, only a voice (text in the terminal).

### Code example: `hello.js`

```js
// hello.js
// Our first Node.js program.

const name = 'Anjali';
const year = new Date().getFullYear();

function greet(person) {
  return 'Hello, ' + person + '! Welcome to Node.js.';
}

console.log(greet(name));
console.log('This year is', year);

// Node-only things (not available in browsers)
console.log('Running file:', __filename);
console.log('Node version:', process.version);

// Command-line arguments: node hello.js Ravi
const arg = process.argv[2];
if (arg) {
  console.log(greet(arg));
}
```

Run:

```bash
node hello.js
node hello.js Ravi
```

Expected output of the first command (year, path and version will differ):

```
Hello, Anjali! Welcome to Node.js.
This year is 2026
Running file: /Users/anjali/my-first-app/hello.js
Node version: v20.11.1
```

Second command adds one more line at the end:

```
Hello, Ravi! Welcome to Node.js.
```

**Things to notice**
- `console.log` prints to the terminal, not to a web page.
- `process` is a global Node object. `process.argv` is an array: index 0 is the node program path, index 1 is the script path, index 2 onward are your own arguments.
- There is no `document` or `window` in Node. Writing `document.getElementById(...)` in Node gives `ReferenceError: document is not defined`.
- `__filename` and `__dirname` work in CommonJS files (the `require` style used in this module).

### CommonJS modules: `require` and `module.exports`

Node lets you split code into files. This module uses the **CommonJS** style.

`mathTools.js`:

```js
// mathTools.js
function add(a, b) {
  return a + b;
}
function square(n) {
  return n * n;
}
module.exports = { add, square };
```

`app.js`:

```js
// app.js
const { add, square } = require('./mathTools'); // './' means "in this folder"
console.log(add(2, 3));    // 5
console.log(square(4));    // 16
```

Run:

```bash
node app.js
```

Expected output:

```
5
16
```

Three kinds of things you can `require`:
1. **Core modules** that come with Node: `require('fs')`, `require('http')`, `require('path')`.
2. **Your own files:** `require('./mathTools')`.
3. **npm packages:** `require('express')`.

**Real-world example.** Build tools such as the ones used to bundle React apps, code formatters and test runners are all simple Node scripts run from the terminal. Developers at companies like Uber and LinkedIn write many small Node scripts to automate boring tasks (renaming files, converting data, running checks).

**Common mistakes**
- Running `node hello` from the wrong folder: you get `Cannot find module`. Use `cd` to go to the file's folder, or give the full path.
- Using browser things (`document`, `alert`) in Node.
- Forgetting `./` in `require('./mathTools')`. Without it, Node looks for a package named `mathTools`.
- Forgetting `module.exports`, so the other file gets an empty object.

**Check your understanding**
1. What command runs `app.js`?
2. What will `process.argv[2]` hold when you run `node hello.js Ravi`?
3. Why does `alert('hi')` fail in Node?
4. What is the difference between `require('fs')` and `require('./fs')`?

### Classroom activity 1: "First script" (10 minutes)
Each student writes `about.js` that prints their name, roll number and college, then takes a favourite subject as a command-line argument and prints it. Pair up and run each other's files.

---

# 5. Topic 2: Working with Node.js core modules

Core modules come built in with Node. No `npm install` needed. We will study three: **fs**, **http** and **path**.

## 5.1 File System module (`fs`): reading and writing files

**Simple explanation.** The `fs` module lets your program read, create, change and delete files and folders on the computer. A browser is not allowed to do this (for safety). Node on a server can.

**Analogy.** `fs` is the **college office clerk who handles the record room**. You ask: "bring me file 24", "write this new entry", "add this to the end of the register". The clerk goes to the shelves (the disk) and does it.

### Three styles: synchronous, callback (asynchronous), promises

Almost every `fs` function exists in three forms.

| Style | Example | How it behaves |
|---|---|---|
| **Synchronous** | `fs.readFileSync(path, 'utf8')` | Blocks. Program waits. Returns the data directly. Throws an error if it fails |
| **Asynchronous with callback** | `fs.readFile(path, 'utf8', (err, data) => {...})` | Does not block. Callback runs later. Error is the **first** argument |
| **Promises** | `require('fs').promises` or `require('fs/promises')`, use with `await` | Does not block. Returns a promise. Works well with `async/await` |

**Analogy: three ways to get a certificate from the college office.**
- **Synchronous:** you stand at the counter and wait until the clerk brings it. Nobody behind you can be served.
- **Callback:** you leave your phone number. The clerk calls when it is ready. You do other things.
- **Promise with await:** the clerk gives you a token. You say "I will wait for this token" (`await`), but the **office** (the thread) keeps serving others meanwhile.

### Reading files

Create a text file `notes.txt` in the same folder:

```
Node.js is fun.
Second line of the file.
```

#### (a) Synchronous read

```js
// read-sync.js
const fs = require('fs');

try {
  const data = fs.readFileSync('notes.txt', 'utf8');
  console.log('File content:');
  console.log(data);
} catch (err) {
  console.error('Could not read file:', err.message);
}
console.log('Done (this prints after the file is read)');
```

Run: `node read-sync.js`

Expected output:

```
File content:
Node.js is fun.
Second line of the file.

Done (this prints after the file is read)
```

(There is an empty line if the file ends with a newline.)

#### (b) Asynchronous with callback

```js
// read-async.js
const fs = require('fs');

fs.readFile('notes.txt', 'utf8', (err, data) => {
  if (err) {
    console.error('Could not read file:', err.message);
    return;
  }
  console.log('File content:');
  console.log(data);
});

console.log('Request sent. Doing other work...');
```

Run: `node read-async.js`

Expected output:

```
Request sent. Doing other work...
File content:
Node.js is fun.
Second line of the file.
```

Notice that "Request sent" comes **first**. The file read finished later.

#### (c) Promises with async/await

```js
// read-promise.js
const fs = require('fs').promises;

async function showFile() {
  try {
    const data = await fs.readFile('notes.txt', 'utf8');
    console.log('File content:');
    console.log(data);
  } catch (err) {
    console.error('Could not read file:', err.message);
  }
}

showFile();
console.log('showFile() called, program continues...');
```

Run: `node read-promise.js`

Expected output:

```
showFile() called, program continues...
File content:
Node.js is fun.
Second line of the file.
```

**Why `'utf8'`?** Without an encoding, you get a **Buffer** (raw bytes) such as `<Buffer 4e 6f 64 65 ...>`. Giving `'utf8'` turns the bytes into readable text.

**What if the file is missing?** The error looks like:

```
Could not read file: ENOENT: no such file or directory, open 'notes.txt'
```

`ENOENT` means "Error NO ENTry", the file or folder does not exist.

### Writing files: `writeFile`

`writeFile` **creates** the file if it does not exist, and **replaces everything** if it does.

```js
// write-demo.js
const fs = require('fs');

fs.writeFile('output.txt', 'Hello from Node.js!\n', (err) => {
  if (err) {
    console.error('Write failed:', err.message);
    return;
  }
  console.log('output.txt written successfully');
});
```

Run: `node write-demo.js`

Expected output:

```
output.txt written successfully
```

`output.txt` now contains: `Hello from Node.js!`

### Adding to a file: `appendFile`

`appendFile` adds text at the **end** and keeps the old content. Creates the file if missing.

```js
// append-demo.js
const fs = require('fs');

const line = 'Visit at ' + new Date().toLocaleTimeString() + '\n';

fs.appendFile('visits.log', line, (err) => {
  if (err) {
    console.error('Append failed:', err.message);
    return;
  }
  console.log('Line added to visits.log');
});
```

Run it three times: `node append-demo.js`. Each run prints `Line added to visits.log`, and `visits.log` grows by one line each time, for example:

```
Visit at 10:15:02 AM
Visit at 10:15:09 AM
Visit at 10:15:14 AM
```

**Analogy.** `writeFile` is **tearing out the page and writing a fresh one** (old content gone). `appendFile` is **adding a new entry at the bottom of the register**.

### A complete example using promises: read, change, write

```js
// copy-upper.js
// Reads notes.txt, makes it UPPERCASE, and saves as notes-upper.txt
const fs = require('fs').promises;

async function main() {
  try {
    const text = await fs.readFile('notes.txt', 'utf8');
    const upper = text.toUpperCase();
    await fs.writeFile('notes-upper.txt', upper);
    await fs.appendFile('notes-upper.txt', '--- end of file ---\n');
    const result = await fs.readFile('notes-upper.txt', 'utf8');
    console.log(result);
  } catch (err) {
    console.error('Something went wrong:', err.message);
  }
}

main();
```

Run: `node copy-upper.js`

Expected output (with the notes.txt shown earlier):

```
NODE.JS IS FUN.
SECOND LINE OF THE FILE.
--- end of file ---
```

### Other handy `fs` functions

| Function | Use |
|---|---|
| `fs.existsSync(path)` | Does it exist? Returns true/false |
| `fs.unlink(path, cb)` | Delete a file |
| `fs.mkdir(path, cb)` | Create a folder |
| `fs.readdir(path, cb)` | List files in a folder |
| `fs.rename(old, new, cb)` | Rename or move |
| `fs.stat(path, cb)` | Size, dates, is it a file or folder |

### Exam-style program: read a file and display content in the console

```js
// readfile-exam.js
const fs = require('fs');

fs.readFile('data.txt', 'utf8', function (err, data) {
  if (err) {
    console.log('Error reading file: ' + err.message);
    return;
  }
  console.log(data);
});
```

(See the Question Bank for the full answer with explanation.)

### When to use which style?

| Situation | Use |
|---|---|
| Small script run once, such as reading a config file at start-up | Sync is fine |
| A running web server | **Never** use sync in a request handler. Use callback or promises |
| Modern code | Promises with `async/await` (cleanest) |

**Real-world example.** Log files: servers append a line to a log for every request (`appendFile` or streams). Image upload services at companies such as Uber (driver documents) or LinkedIn (profile photos) read and write files on the server before sending them to cloud storage. Build tools read thousands of source files using `fs`.

**Common mistakes**
- Using `readFileSync` inside a server request handler, which blocks all users.
- Forgetting the `'utf8'` argument, then printing a Buffer.
- Ignoring `err` in the callback.
- Using `writeFile` when you wanted to add to a file (old data is lost!).
- Wrong relative path. `'notes.txt'` is relative to where you **ran the command** (the current working directory), not to where the script file sits. Fix with `path.join(__dirname, 'notes.txt')` (see 5.3).
- Forgetting `await` before `fs.promises.readFile`, then printing `Promise { <pending> }`.

**Check your understanding**
1. Write the difference between `writeFile` and `appendFile`.
2. In `fs.readFile(path, 'utf8', (err, data) => {})`, what is the first argument of the callback and why is it checked first?
3. Why is `readFileSync` a bad idea inside a web server?
4. What does `ENOENT` mean?

### Classroom activity 2: "Visitor register" (15 minutes)
Students write a script that takes a name from `process.argv[2]` and appends `name - time` to `register.txt`, then reads the file and prints all entries. Do it first with callbacks, then convert to `async/await`.

---

## 5.2 HTTP module: creating a basic web server

**Simple explanation.** The `http` module lets Node **listen** for requests from browsers and **send back** responses. With about five lines, you have a web server.

**Analogy.** An `http` server is the **reception counter** of a post office. Letters (requests) arrive. The clerk (your callback function) reads the address and writes a reply (response). The counter has a number (the **port**) so people know which window to go to.

### The smallest server: respond "Hello, World!"

```js
// server-hello.js
const http = require('http');

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Hello, World!');
});

server.listen(3000, () => {
  console.log('Server running at http://localhost:3000/');
});
```

Run:

```bash
node server-hello.js
```

Expected output in terminal:

```
Server running at http://localhost:3000/
```

Now open a browser and visit `http://localhost:3000`. The page shows:

```
Hello, World!
```

The terminal stays "busy". That is normal, because the server keeps running and waiting. To stop it, press **Ctrl + C**.

**You can also test with the terminal** (open a second terminal):

```bash
curl http://localhost:3000
```

Output:

```
Hello, World!
```

### Line by line

| Code | Meaning |
|---|---|
| `require('http')` | Load the built-in http module |
| `http.createServer(callback)` | Make a server. The callback runs **for every request** |
| `req` | The request object: what the browser asked (URL, method, headers) |
| `res` | The response object: what we send back |
| `res.writeHead(200, {...})` | Send the status code and headers. `200` = OK |
| `res.end('Hello, World!')` | Send the body and finish the response. **Must call**, or the browser waits forever |
| `server.listen(3000, cb)` | Start listening on port 3000. `cb` runs once when ready |

**What is localhost and port?** `localhost` means "this same computer" (address `127.0.0.1`). A port is a numbered door on the computer. Port 80 is the usual door for websites, but we use 3000 for development so we need no special rights.

**Common status codes**

| Code | Meaning | Everyday example |
|---|---|---|
| 200 | OK | Counter gives what you asked |
| 201 | Created | New record saved |
| 301/302 | Redirect | "This counter has moved to window 5" |
| 400 | Bad request | Form filled wrongly |
| 404 | Not found | "No such file in record room" |
| 405 | Method not allowed | Using a window for the wrong purpose |
| 500 | Server error | Clerk's computer crashed |

### Sending HTML

```js
// server-html.js
const http = require('http');

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/html' });
  res.write('<h1>Welcome to KSRTC Info Desk</h1>');
  res.write('<p>Next bus to Kochi: 10:30 AM</p>');
  res.end();
});

server.listen(3000, () => console.log('Listening on port 3000'));
```

Run: `node server-html.js`, then open `http://localhost:3000`.

Terminal shows:

```
Listening on port 3000
```

Browser shows a heading and a paragraph. `res.write()` can be called many times; `res.end()` is the last call.

**Content-Type matters.** If you send HTML but set `text/plain`, the browser shows the raw tags as text. The `Content-Type` header tells the browser **what kind of thing** it received.

### Looking inside the request

```js
// server-info.js
const http = require('http');

const server = http.createServer((req, res) => {
  console.log('Method :', req.method);
  console.log('URL    :', req.url);
  console.log('Browser:', req.headers['user-agent']);
  console.log('---');

  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('You asked for ' + req.method + ' ' + req.url);
});

server.listen(3000, () => console.log('Open http://localhost:3000/hello'));
```

Run: `node server-info.js` and visit `http://localhost:3000/hello`.

Terminal shows (the browser may also request `/favicon.ico`, which is why you often see two blocks):

```
Open http://localhost:3000/hello
Method : GET
URL    : /hello
Browser: Mozilla/5.0 (...)
---
Method : GET
URL    : /favicon.ico
Browser: Mozilla/5.0 (...)
---
```

Browser shows: `You asked for GET /hello`.

**Real-world example.** Under the hood, Express (used by PayPal, Uber and many others), Next.js and many API frameworks all sit on top of this very `http` module. Learning it shows you what the frameworks hide.

**Common mistakes**
- Forgetting `res.end()`. The browser spins forever.
- Sending the response twice (`res.end()` called two times) gives an error.
- Port already in use: `Error: listen EADDRINUSE: address already in use :::3000`. Stop the old server (Ctrl + C) or use another port.
- Editing the code and expecting the browser to change without restarting the server. Stop and run again (or use `nodemon`).
- Wrong `Content-Type`.
- Writing `http://localhost` without `:3000`.

**Check your understanding**
1. What is the job of the callback given to `createServer`?
2. What happens if we never call `res.end()`?
3. What does status code 404 mean?
4. Why do we see two requests in the terminal when we open one page?

### Classroom activity 3: "Bus timing server" (15 minutes)
Students change `server-html.js` to show a table of three bus timings. They share the link `http://<their-ip>:3000` with a neighbour on the same Wi-Fi to see each other's page. (Find your IP with `ipconfig` on Windows or `ifconfig` on Mac/Linux.)

---

## 5.3 Working with file and directory paths: the `path` module

**Simple explanation.** Different systems write paths differently: Windows uses backslash `C:\Users\anu\file.txt`, Mac and Linux use forward slash `/Users/anu/file.txt`. If you join paths by hand (`'folder' + '/' + 'file.txt'`), the code may break on another system. The `path` module builds and reads paths correctly for **whichever system you are on**.

**Analogy.** The `path` module is like a **postal PIN-code and address formatter**. You give pieces (house, street, city), it writes the full address in the correct format, and it can also pull pieces out of an address (the PIN, the street).

### Special variables: `__dirname` and `__filename`

| Variable | Meaning |
|---|---|
| `__dirname` | Full path of the **folder** that contains the current script file |
| `__filename` | Full path of the **current script file** |

They are available in CommonJS modules. They do not change if you run the command from another folder, so they are safer than relative paths like `'notes.txt'`.

### Main functions

| Function | What it does | Example result |
|---|---|---|
| `path.join(a, b, ...)` | Joins parts with the correct separator and cleans `..` | `path.join('a','b','c.txt')` gives `a/b/c.txt` |
| `path.resolve(a, b)` | Makes an **absolute** path | `/home/user/a/b` |
| `path.basename(p)` | Last part (file name) | `/x/y/photo.jpg` gives `photo.jpg` |
| `path.dirname(p)` | Folder part | `/x/y/photo.jpg` gives `/x/y` |
| `path.extname(p)` | Extension, with dot | `.jpg` |
| `path.parse(p)` | Breaks into an object | `{ root, dir, base, ext, name }` |
| `path.isAbsolute(p)` | Starts from the root? | true/false |
| `path.sep` | Separator for this system | `/` or `\` |

### Code example

```js
// path-demo.js
const path = require('path');

console.log('__dirname :', __dirname);
console.log('__filename:', __filename);

const file = path.join(__dirname, 'uploads', 'photos', 'anu.jpg');
console.log('Joined    :', file);

console.log('basename  :', path.basename(file));
console.log('dirname   :', path.dirname(file));
console.log('extname   :', path.extname(file));
console.log('name only :', path.basename(file, '.jpg'));
console.log('parse     :', path.parse('/home/anu/report.pdf'));

// join also cleans up '..'
console.log('Cleaned   :', path.join('/a/b', '../c', 'd.txt'));

console.log('Is absolute?', path.isAbsolute(file));
```

Run: `node path-demo.js`

Expected output on Mac/Linux, if the script is in `/Users/anu/demo` (on Windows you will see backslashes and `C:\...`):

```
__dirname : /Users/anu/demo
__filename: /Users/anu/demo/path-demo.js
Joined    : /Users/anu/demo/uploads/photos/anu.jpg
basename  : anu.jpg
dirname   : /Users/anu/demo/uploads/photos
extname   : .jpg
name only : anu
parse     : {
  root: '/',
  dir: '/home/anu',
  base: 'report.pdf',
  ext: '.pdf',
  name: 'report'
}
Cleaned   : /a/c/d.txt
Is absolute? true
```

### Using `__dirname` with `fs` (the safe way)

```js
// safe-read.js
const fs = require('fs');
const path = require('path');

const filePath = path.join(__dirname, 'notes.txt');

fs.readFile(filePath, 'utf8', (err, data) => {
  if (err) {
    console.error('Error:', err.message);
    return;
  }
  console.log(data);
});
```

Now `node safe-read.js` works even when run from another folder, for example `node demo/safe-read.js` from the parent folder.

**Real-world example.** Every web framework uses `path` to find views, static folders and uploaded files. The static file server in Express (`express.static`) uses `path.join(__dirname, 'public')`. A file upload feature (for example, LinkedIn resume upload) uses `path.extname` to check that the file is `.pdf` or `.docx` and to reject others.

**Common mistakes**
- Building paths with `+ '/' +`. Use `path.join`.
- Confusing `__dirname` (folder of the script) with `process.cwd()` (folder where you ran the command).
- Writing `path.join(__dirname, '/public')` and expecting an absolute path. `join` simply combines. Use `resolve` for absolute.
- Forgetting that `extname` includes the dot (`.jpg`, not `jpg`).
- Using `__dirname` in ES module files (`import` style). It does not exist there. This module uses CommonJS, so it is fine.

**Check your understanding**
1. What is the difference between `__dirname` and `__filename`?
2. What does `path.extname('/docs/notice.pdf')` return?
3. Why is `path.join` better than string `+`?
4. What does `path.join('/a/b', '../c')` give?

### Classroom activity 4: "File type checker" (10 minutes)
Write a function `kind(filename)` using `path.extname` that returns `'image'` for `.jpg/.png`, `'document'` for `.pdf/.docx`, otherwise `'unknown'`. Test with five names.

---

# 6. Topic 3: Building a simple web server

In Topic 2 we made a server that gives the same answer to everyone. A real website gives **different answers for different URLs**: `/` is the home page, `/about` is the about page, `/style.css` is a stylesheet. This is **routing** and **static file serving**.

## 6.1 Using the `http` module to create a web server (step by step)

**Steps to create a web server (exam answer):**
1. Import the module: `const http = require('http');`
2. Create the server with `http.createServer(callback)`. The callback receives `req` and `res`.
3. Inside the callback, read the request (`req.url`, `req.method`) and decide what to send.
4. Set status code and headers with `res.writeHead()` (or `res.statusCode` and `res.setHeader()`).
5. Send the body and finish with `res.end()`.
6. Start listening: `server.listen(port, callback)`.

**Analogy: KSRTC enquiry counter.** The clerk (callback) hears the question (request). "Which bus to Thrissur?" The clerk looks at the board, answers (response) and says "next, please". The counter is open all day (listen).

### Another way to write the same thing

```js
// server-style2.js
const http = require('http');

const server = http.createServer();

// 'request' is an event. Node fires it for each incoming request.
server.on('request', (req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain; charset=utf-8');
  res.end('Namaskaram from the server!');
});

server.listen(3000, '127.0.0.1', () => {
  console.log('Listening on http://127.0.0.1:3000');
});
```

Run: `node server-style2.js`

Terminal:

```
Listening on http://127.0.0.1:3000
```

Browser: `Namaskaram from the server!`

(Connect it to the event loop idea: `server.on('request', ...)` is exactly "when this event happens, run my callback".)

## 6.2 Handling basic routing (`req.url` and `req.method`)

**Simple explanation.** **Routing** means deciding what to do based on **which URL** was asked and **which method** was used.

- `req.url` is the path (plus query string), such as `/about` or `/search?q=bus`.
- `req.method` is the type of request: `GET` (give me something), `POST` (here is some data to save), `PUT`, `DELETE`.

**Analogy: post office sorting room.** Each letter has an address (URL). The sorter reads it and puts it in the right bag (route). A parcel (POST) and a postcard (GET) may go to the same city but use different counters (method).

### Code example

```js
// router.js
const http = require('http');

const server = http.createServer((req, res) => {
  const { url, method } = req;

  if (url === '/' && method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'text/html; charset=utf-8' });
    res.end('<h1>Home</h1><a href="/about">About</a> | <a href="/contact">Contact</a>');

  } else if (url === '/about' && method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'text/html; charset=utf-8' });
    res.end('<h1>About</h1><p>This is a demo college site.</p><a href="/">Back</a>');

  } else if (url === '/contact' && method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'text/plain; charset=utf-8' });
    res.end('Email: office@college.example');

  } else if (url === '/api/time' && method === 'GET') {
    // Sending JSON
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ time: new Date().toISOString() }));

  } else {
    res.writeHead(404, { 'Content-Type': 'text/html; charset=utf-8' });
    res.end('<h1>404 - Page not found</h1>');
  }
});

server.listen(3000, () => console.log('Router running on http://localhost:3000'));
```

Run: `node router.js`

Terminal:

```
Router running on http://localhost:3000
```

Try these in the browser or with curl:

| URL | Result |
|---|---|
| `http://localhost:3000/` | Home page with links |
| `http://localhost:3000/about` | About page |
| `http://localhost:3000/contact` | `Email: office@college.example` |
| `http://localhost:3000/api/time` | `{"time":"2026-10-09T10:20:30.123Z"}` (your time will differ) |
| `http://localhost:3000/xyz` | `404 - Page not found` |

Test with curl and see the status line:

```bash
curl -i http://localhost:3000/xyz
```

Output (first lines):

```
HTTP/1.1 404 Not Found
Content-Type: text/html; charset=utf-8
...
<h1>404 - Page not found</h1>
```

### Query strings and the `URL` class

If the user visits `/search?q=bus&to=Kochi`, then `req.url` is the whole string `/search?q=bus&to=Kochi`. It will not equal `/search`. Use the built-in `URL` class to split it.

```js
// router-query.js
const http = require('http');

const server = http.createServer((req, res) => {
  // The second argument gives a base so URL can parse a relative path
  const parsed = new URL(req.url, 'http://' + req.headers.host);
  const pathname = parsed.pathname;               // '/search'
  const q = parsed.searchParams.get('q');          // 'bus'
  const to = parsed.searchParams.get('to');        // 'Kochi'

  if (pathname === '/search') {
    res.writeHead(200, { 'Content-Type': 'text/plain; charset=utf-8' });
    res.end('You searched for ' + q + ' going to ' + to);
  } else {
    res.writeHead(404, { 'Content-Type': 'text/plain' });
    res.end('Not found');
  }
});

server.listen(3000, () => console.log('Try http://localhost:3000/search?q=bus&to=Kochi'));
```

Run: `node router-query.js`. Visit the URL from the log line.

Browser shows: `You searched for bus going to Kochi`

### Handling a POST body in plain Node

Data in a POST request arrives in **pieces (chunks)**. We collect them and then use them.

```js
// post-plain.js
const http = require('http');

const server = http.createServer((req, res) => {
  if (req.method === 'POST' && req.url === '/greet') {
    let body = '';

    req.on('data', (chunk) => {
      body += chunk.toString();       // collect pieces
    });

    req.on('end', () => {             // all pieces arrived
      let data;
      try {
        data = JSON.parse(body);
      } catch (e) {
        res.writeHead(400, { 'Content-Type': 'application/json' });
        res.end(JSON.stringify({ error: 'Invalid JSON' }));
        return;
      }
      res.writeHead(200, { 'Content-Type': 'application/json' });
      res.end(JSON.stringify({ message: 'Hello, ' + data.name + '!' }));
    });

  } else {
    res.writeHead(404, { 'Content-Type': 'text/plain' });
    res.end('Not found');
  }
});

server.listen(3000, () => console.log('POST to http://localhost:3000/greet'));
```

Run: `node post-plain.js`, then in another terminal:

```bash
curl -X POST -H "Content-Type: application/json" -d '{"name":"Meera"}' http://localhost:3000/greet
```

Output:

```
{"message":"Hello, Meera!"}
```

(On Windows PowerShell, use `curl.exe` and escape quotes, or use a tool like Postman or Thunder Client in VS Code.)

**Analogy.** The body arrives like **water in buckets**: you keep pouring each bucket (`data`) into one tank (`body`) and only start using it when the last bucket arrives (`end`).

This is a lot of code for one simple job. Express (Topic 4) removes it with `express.json()`.

**How is routing handled? (exam answer)** In the request callback we read `req.url` and `req.method` and compare them using `if / else if` (or `switch`). For each match, we set the status code, headers and body and call `res.end()`. If nothing matches we send a 404. This works, but with many routes it becomes long, which is why frameworks like Express exist.

**Real-world example.** API gateways and microservices at companies like Uber start as small route tables (`GET /trip/:id`, `POST /trip`). A food-ordering app such as Swiggy has routes like `GET /restaurants`, `POST /orders`, `GET /orders/:id`. The idea is the same as our `if / else if`, just organised better.

**Common mistakes**
- Comparing `req.url === '/search'` when the URL has a query string.
- Not sending a 404 for unknown routes, so the browser hangs.
- Forgetting `return` after sending an error, then calling `res.end()` twice.
- Using `JSON.parse` without `try/catch`, so a bad request crashes the server.
- Forgetting `JSON.stringify` when sending an object (`res.end({a:1})` throws an error).
- Using `res.write` or `res.end` after the response already ended.

**Check your understanding**
1. What are `req.url` and `req.method`?
2. Why does `if (req.url === '/search')` fail for `/search?q=bus`?
3. How does Node receive the body of a POST request?
4. What status code should an unknown URL return?

## 6.3 Serving static files (HTML, CSS, JS) with correct Content-Type

**Simple explanation.** **Static files** are files that are sent as they are: `.html`, `.css`, `.js`, images, PDFs. The server finds the file on the disk, reads it and sends it. The browser needs the **right `Content-Type` header** to know whether it is HTML, CSS or JavaScript. Wrong type: CSS may not apply, scripts may not run.

**Analogy.** Static files are **printed forms kept in the college office cupboard**. The clerk does not write anything new. He finds the right form and hands it over with a label saying what it is ("Admission form: paper"). The label is the Content-Type.

### Common MIME types

MIME type is the standard name for the kind of a file.

| Extension | Content-Type |
|---|---|
| `.html` | `text/html` |
| `.css` | `text/css` |
| `.js` | `text/javascript` (older: `application/javascript`) |
| `.json` | `application/json` |
| `.png` | `image/png` |
| `.jpg`, `.jpeg` | `image/jpeg` |
| `.gif` | `image/gif` |
| `.svg` | `image/svg+xml` |
| `.ico` | `image/x-icon` |
| `.txt` | `text/plain` |
| `.pdf` | `application/pdf` |

### Folder structure

```
static-server/
  server.js
  public/
    index.html
    about.html
    css/
      style.css
    js/
      app.js
    images/
      logo.png      (optional)
```

### `public/index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>My Static Site</title>
  <link rel="stylesheet" href="/css/style.css">
</head>
<body>
  <h1>Welcome to our Department</h1>
  <p id="msg">Loading message...</p>
  <a href="/about.html">About</a>
  <script src="/js/app.js"></script>
</body>
</html>
```

### `public/about.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>About</title>
  <link rel="stylesheet" href="/css/style.css">
</head>
<body>
  <h1>About Us</h1>
  <p>We teach Web Application Development.</p>
  <a href="/">Home</a>
</body>
</html>
```

### `public/css/style.css`

```css
body {
  font-family: Arial, sans-serif;
  background: #f4f7fb;
  margin: 40px;
}
h1 {
  color: #1a4d8f;
}
a {
  color: #d9480f;
}
```

### `public/js/app.js`

```js
document.getElementById('msg').textContent =
  'This text was set by JavaScript served from Node.js!';
```

### `server.js` (the static server)

```js
// server.js
const http = require('http');
const fs = require('fs');
const path = require('path');

const PORT = 3000;
const PUBLIC_DIR = path.join(__dirname, 'public');

const MIME_TYPES = {
  '.html': 'text/html; charset=utf-8',
  '.css':  'text/css; charset=utf-8',
  '.js':   'text/javascript; charset=utf-8',
  '.json': 'application/json; charset=utf-8',
  '.png':  'image/png',
  '.jpg':  'image/jpeg',
  '.jpeg': 'image/jpeg',
  '.gif':  'image/gif',
  '.svg':  'image/svg+xml',
  '.ico':  'image/x-icon',
  '.txt':  'text/plain; charset=utf-8'
};

const server = http.createServer((req, res) => {
  // Only allow GET
  if (req.method !== 'GET') {
    res.writeHead(405, { 'Content-Type': 'text/plain' });
    res.end('Method Not Allowed');
    return;
  }

  // Remove query string, decode %20 etc.
  let urlPath;
  try {
    urlPath = decodeURIComponent(new URL(req.url, 'http://localhost').pathname);
  } catch (e) {
    res.writeHead(400, { 'Content-Type': 'text/plain' });
    res.end('Bad Request');
    return;
  }

  // '/' means the home page
  if (urlPath === '/') {
    urlPath = '/index.html';
  }

  // Build the full path on disk
  const filePath = path.join(PUBLIC_DIR, urlPath);

  // SECURITY: stop people using ../ to escape the public folder
  if (!filePath.startsWith(PUBLIC_DIR)) {
    res.writeHead(403, { 'Content-Type': 'text/plain' });
    res.end('Forbidden');
    return;
  }

  const ext = path.extname(filePath).toLowerCase();
  const contentType = MIME_TYPES[ext] || 'application/octet-stream';

  fs.readFile(filePath, (err, content) => {
    if (err) {
      if (err.code === 'ENOENT') {
        res.writeHead(404, { 'Content-Type': 'text/html; charset=utf-8' });
        res.end('<h1>404 - File not found</h1>');
      } else {
        res.writeHead(500, { 'Content-Type': 'text/plain' });
        res.end('Server error');
      }
      return;
    }
    res.writeHead(200, { 'Content-Type': contentType });
    res.end(content);   // content is a Buffer (raw bytes); works for images too
  });
});

server.listen(PORT, () => {
  console.log('Static server running at http://localhost:' + PORT);
});
```

Run (from inside `static-server/`):

```bash
node server.js
```

Terminal:

```
Static server running at http://localhost:3000
```

In the browser:

| URL | You see |
|---|---|
| `http://localhost:3000/` | Home page, styled blue heading, and the text changed by JavaScript |
| `http://localhost:3000/about.html` | About page |
| `http://localhost:3000/css/style.css` | The raw CSS text |
| `http://localhost:3000/nothing.html` | `404 - File not found` |

Check headers with curl:

```bash
curl -I http://localhost:3000/css/style.css
```

Expected (first lines):

```
HTTP/1.1 200 OK
Content-Type: text/css; charset=utf-8
```

**How the browser loads a whole page:** it first asks for `/`. The server sends `index.html`. The browser reads the HTML, sees `<link href="/css/style.css">` and `<script src="/js/app.js">`, and sends **new requests** for each. So one page can mean many requests, and our server handles each one the same way.

```
Browser                         Server
  | GET /                         |
  |------------------------------>|  reads public/index.html
  |<------------------------------|  200, text/html
  | GET /css/style.css            |
  |------------------------------>|  reads public/css/style.css
  |<------------------------------|  200, text/css
  | GET /js/app.js                |
  |------------------------------>|  reads public/js/app.js
  |<------------------------------|  200, text/javascript
```

**Why we check `startsWith(PUBLIC_DIR)`:** a bad user could request `/../server.js` to steal your source code. `path.join` cleans `..`, so the final path would point outside `public`. The check blocks it. This is called **path traversal protection**. Express does this for you in `express.static`.

**Real-world example.** Every website serves static assets: logos, CSS, bundles of JavaScript. Large sites (Netflix, LinkedIn) put these on a CDN (Content Delivery Network, many servers around the world close to users) rather than on the Node server, but the idea is identical. For small projects, a Node server serving a `public` folder is the standard.

**Common mistakes**
- Wrong or missing `Content-Type`. CSS served as `text/plain` is ignored by the browser. A `.js` served as `text/html` may be blocked.
- Using `readFileSync` and blocking the server.
- Using relative paths like `'public/index.html'` and then running the command from another folder. Use `path.join(__dirname, ...)`.
- Forgetting the leading `/` in HTML (`href="css/style.css"` can break on nested pages; `href="/css/style.css"` is safer).
- Not handling `/` so the home page gives 404.
- Not blocking `../` paths.
- Reading images as `'utf8'`. This damages binary files. Read as Buffer (no encoding).

**Check your understanding**
1. Which header tells the browser the type of a file?
2. Why do we call `fs.readFile` without `'utf8'` in the static server?
3. A page has one HTML file, one CSS file and one JS file. How many requests does the server receive?
4. What is path traversal and how do we stop it?

### Classroom activity 5: "Break it and fix it" (15 minutes)
1. In `server.js`, change `.css` to `'text/plain'`. Reload the browser. The page loses its style. Open DevTools, Network tab, and find the cause.
2. Change it back. Request `http://localhost:3000/../server.js` using `curl --path-as-is`. See the 403.
3. Ask: "What would happen if we remove the security check?"

---

# 7. Topic 4: Introduction to Express.js

## 7.1 What is Express.js and why do we use it?

**Simple explanation.** Express is a small, fast **web framework** for Node.js. A framework is a ready-made set of tools and rules that does the boring, repeated work. Express sits on top of the `http` module. It gives us a clean way to write routes, read request data, serve static files and plug in extra features (middleware).

**Analogy.** Using the plain `http` module is like **cooking a full meal from raw vegetables on a wood fire**. Using Express is like **cooking in a fully equipped kitchen with a gas stove, mixer, and labelled jars**. The food is still your cooking; the tools save time.

**Plain `http` vs Express**

| Task | Plain `http` | Express |
|---|---|---|
| Route | `if (req.url === '/a' && req.method === 'GET')` | `app.get('/a', ...)` |
| Send JSON | `res.writeHead(...)` and `JSON.stringify` | `res.json(obj)` |
| Read JSON body | Collect chunks, `JSON.parse` | `express.json()` |
| Static files | Our own 50-line code | `express.static('public')` |
| URL parameters | Cut the string by hand | `req.params.id` |
| Query string | `new URL(...)` | `req.query.q` |

**Real-world example.** Express is the most widely used Node.js framework. Companies such as Uber, PayPal (parts of it), IBM and many start-ups use it for their APIs. Many Indian food-delivery, ticketing and fintech start-ups write their REST APIs in Express.

## 7.2 Installing Express.js

```bash
mkdir express-demo
cd express-demo
npm init -y
npm install express
```

After install, `package.json` has `"express": "^4.x.x"` under `dependencies` and a `node_modules` folder appears.

Check:

```bash
npm list express
```

Expected output (version may differ):

```
express-demo@1.0.0 /Users/anu/express-demo
`-- express@4.19.2
```

**Note for teacher:** Express 5 is also available (`npm install express` may install version 5 depending on the date). All code in this module works in both Express 4 and Express 5. The one difference to watch: in Express 5, `req.body` is `undefined` when no body parser has run, instead of `{}`.

## 7.3 Setting up a basic Express server

```js
// app.js
const express = require('express');

const app = express();
const PORT = 3000;

app.get('/', (req, res) => {
  res.send('Hello from Express!');
});

app.listen(PORT, () => {
  console.log(`Express server running at http://localhost:${PORT}`);
});
```

Run:

```bash
node app.js
```

Terminal:

```
Express server running at http://localhost:3000
```

Browser at `http://localhost:3000`:

```
Hello from Express!
```

Compare to the plain version: no `writeHead`, no `Content-Type`, no `end`. `res.send()` works out the type for us (a string becomes `text/html`, an object becomes JSON).

**Parts**
- `express()` creates an application object, `app`.
- `app.get(path, handler)` says "when a GET request comes for this path, run this handler".
- `app.listen(port, cb)` starts the server (it calls `http.createServer` inside).

**Handy tool: nodemon.** It restarts your server every time you save a file.

```bash
npm install --save-dev nodemon
```

Then in `package.json`:

```json
"scripts": {
  "start": "node app.js",
  "dev": "nodemon app.js"
}
```

Run `npm run dev`. (Node 18.11 and later also has `node --watch app.js`.)

**Common mistakes**
- Calling the file `express.js` (conflicts with the package name).
- Forgetting `npm install express` and getting `Error: Cannot find module 'express'`.
- Forgetting `app.listen`, so the program starts and exits without serving.
- Using `res.send` twice for one request (error: "Cannot set headers after they are sent").

**Check your understanding**
1. What is Express and how is it related to the `http` module?
2. Which two commands install Express in a new folder?
3. What does `app.listen(3000)` do?

## 7.4 Handling GET requests

**Simple explanation.** A **GET** request asks the server for something and does not change anything on the server. Opening a web page is a GET. Express uses `app.get(path, handler)`.

**Analogy.** GET is like **asking the IRCTC enquiry window "Is train 12625 on time?"** You just ask. Nothing changes.

### Basic GET route: the `/welcome` exam example

```js
// welcome.js
const express = require('express');
const app = express();

app.get('/welcome', (req, res) => {
  res.send('Welcome to Express');
});

app.listen(3000, () => {
  console.log('Server started on port 3000');
});
```

Run: `node welcome.js`

Terminal:

```
Server started on port 3000
```

Visit `http://localhost:3000/welcome`, and the browser shows:

```
Welcome to Express
```

Any other URL (such as `/`) gives Express's default:

```
Cannot GET /
```

### The `req` and `res` objects in Express

| Object/method | Use |
|---|---|
| `req.params` | Values from the URL path (`/users/:id`) |
| `req.query` | Values after `?` in the URL |
| `req.body` | Data sent in a POST body (needs `express.json()` or `express.urlencoded()`) |
| `req.headers` | Request headers |
| `req.method`, `req.path` | Method and path |
| `res.send(x)` | Send text, HTML, object, or buffer |
| `res.json(obj)` | Send JSON |
| `res.status(code)` | Set status (chainable): `res.status(404).send('...')` |
| `res.sendFile(absPath)` | Send a file |
| `res.redirect(url)` | Redirect |

### Route parameters (`req.params`)

A route parameter is a **variable part of the path**, written with a colon.

**Analogy.** Think of the **roll number on a college ID**. The pattern is "student number ___". `/students/21` and `/students/45` follow the same pattern but with different numbers.

```js
// params.js
const express = require('express');
const app = express();

const students = {
  1: { name: 'Anjali', branch: 'CSE' },
  2: { name: 'Rahul', branch: 'ECE' },
  3: { name: 'Fathima', branch: 'CSE' }
};

// /students/2
app.get('/students/:id', (req, res) => {
  const student = students[req.params.id];
  if (!student) {
    return res.status(404).json({ error: 'Student not found' });
  }
  res.json(student);
});

// Two parameters: /trains/12625/seats/SL
app.get('/trains/:trainNo/seats/:classCode', (req, res) => {
  const { trainNo, classCode } = req.params;
  res.send(`Train ${trainNo}, class ${classCode}: seats available`);
});

app.listen(3000, () => console.log('Params demo on http://localhost:3000'));
```

Run: `node params.js`

| URL | Output |
|---|---|
| `/students/2` | `{"name":"Rahul","branch":"ECE"}` |
| `/students/9` | `{"error":"Student not found"}` with status 404 |
| `/trains/12625/seats/SL` | `Train 12625, class SL: seats available` |

Note: `req.params` values are always **strings**. Convert with `Number(req.params.id)` if you need a number.

### Query strings (`req.query`)

The part after `?` is the **query string**: `key=value` pairs joined by `&`. Used for search, filter, sort, page number.

**Analogy.** When you ask at a bus stand, "Buses **to Kochi, after 6 PM, AC only**." The place is the path; the conditions are the query.

```js
// query.js
const express = require('express');
const app = express();

const buses = [
  { id: 1, to: 'Kochi',   time: 6,  ac: true  },
  { id: 2, to: 'Kochi',   time: 9,  ac: false },
  { id: 3, to: 'Thrissur', time: 7, ac: true  },
  { id: 4, to: 'Kochi',   time: 18, ac: true  }
];

// /buses?to=Kochi&ac=true
app.get('/buses', (req, res) => {
  let result = buses;

  if (req.query.to) {
    result = result.filter(b => b.to.toLowerCase() === req.query.to.toLowerCase());
  }
  if (req.query.ac === 'true') {
    result = result.filter(b => b.ac);
  }
  res.json(result);
});

app.listen(3000, () => console.log('Query demo on http://localhost:3000'));
```

Run: `node query.js`

Visit `http://localhost:3000/buses?to=Kochi&ac=true`. Output:

```
[{"id":1,"to":"Kochi","time":6,"ac":true},{"id":4,"to":"Kochi","time":18,"ac":true}]
```

Visit `http://localhost:3000/buses` (no query): all four buses.

**Params vs query: when to use which?**

| | Route params | Query string |
|---|---|---|
| Looks like | `/students/21` | `/students?branch=CSE` |
| Meaning | Identifies **one specific thing** | **Filters, sorts, searches** a list |
| Required? | Yes (part of the path) | Optional |
| Read with | `req.params` | `req.query` |

**Real-world example.** Amazon-like URLs: `/product/12345` (param) and `/search?q=phone&sort=price` (query). Swiggy: `/restaurants/543` and `/restaurants?cuisine=south-indian&rating=4`. LinkedIn: `/in/username` (param).

**Common mistakes**
- Reading `req.query.id` when the route is `/students/:id` (should be `req.params.id`).
- Forgetting that all values are strings (`'true'`, not `true`; `'5'`, not `5`).
- Putting a general route (`/students/:id`) above a specific one (`/students/new`). Express matches in order, so `new` is taken as an id. Put specific routes first.
- Sending two responses in one handler (missing `return`).

**Check your understanding**
1. What is the value of `req.params.id` for `/students/7`?
2. What is `req.query` for `/search?q=bus&page=2`?
3. When should we use a route parameter and when a query string?
4. Why is order of routes important in Express?

## 7.5 Handling POST requests: `express.json()` and `express.urlencoded()`

**Simple explanation.** A **POST** request **sends data to the server**, usually to create or save something: a login form, a new notice, a booking. The data is in the **request body**, not in the URL. In Express: `app.post(path, handler)`.

**Analogy.** GET is **asking at the counter**. POST is **submitting a filled form at the counter**; the clerk keeps it.

### Why do we need body parsers?

The body arrives as raw bytes in chunks (remember the "buckets" analogy). Express has built-in **middleware** to collect and convert it, and then put the result in `req.body`.

| Middleware | Handles | Content-Type of request | Typical source |
|---|---|---|---|
| `express.json()` | JSON text | `application/json` | `fetch(...)` from JavaScript, Postman, mobile apps |
| `express.urlencoded({ extended: true })` | Form data like `name=Anu&age=20` | `application/x-www-form-urlencoded` | A normal HTML `<form method="POST">` |

Without them, `req.body` is `undefined` (or `{}` in older versions).

### Code example: JSON POST and HTML form POST

```js
// post.js
const express = require('express');
const app = express();

// Body parsers: must come BEFORE the routes that use req.body
app.use(express.json());                         // for JSON bodies
app.use(express.urlencoded({ extended: true })); // for HTML form bodies

const feedback = [];   // temporary storage in memory

// Show a simple form on GET /
app.get('/', (req, res) => {
  res.send(`
    <h2>Feedback</h2>
    <form method="POST" action="/feedback">
      <input name="name" placeholder="Your name" required><br><br>
      <textarea name="message" placeholder="Message" required></textarea><br><br>
      <button type="submit">Send</button>
    </form>
    <p><a href="/feedback">See all feedback</a></p>
  `);
});

// Receive data (works for BOTH form and JSON)
app.post('/feedback', (req, res) => {
  const { name, message } = req.body;

  if (!name || !message) {
    return res.status(400).json({ error: 'name and message are required' });
  }

  const item = { id: feedback.length + 1, name, message };
  feedback.push(item);

  console.log('New feedback:', item);
  res.status(201).json({ saved: true, item });
});

// List all
app.get('/feedback', (req, res) => {
  res.json(feedback);
});

app.listen(3000, () => console.log('POST demo on http://localhost:3000'));
```

Run: `node post.js`

**Test 1: with the HTML form.** Open `http://localhost:3000`, fill in and press Send. The browser shows:

```
{"saved":true,"item":{"id":1,"name":"Anu","message":"Great class"}}
```

Terminal shows:

```
New feedback: { id: 1, name: 'Anu', message: 'Great class' }
```

**Test 2: with curl sending JSON.**

```bash
curl -X POST -H "Content-Type: application/json" -d '{"name":"Ravi","message":"Nice"}' http://localhost:3000/feedback
```

Output:

```
{"saved":true,"item":{"id":2,"name":"Ravi","message":"Nice"}}
```

**Test 3: missing data.**

```bash
curl -X POST -H "Content-Type: application/json" -d '{"name":"Ravi"}' http://localhost:3000/feedback
```

Output (status 400):

```
{"error":"name and message are required"}
```

**Test 4:** visit `http://localhost:3000/feedback` and see the list as JSON.

**Note:** Because `feedback` is only a JavaScript array in memory, **everything is lost when the server restarts**. In the mini-project we will save to a file.

### Sending JSON from the browser with `fetch`

```html
<!-- Could be placed in public/index.html -->
<script>
  fetch('/feedback', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ name: 'Sneha', message: 'Hello from fetch' })
  })
    .then(r => r.json())
    .then(data => console.log(data));
</script>
```

The header `Content-Type: application/json` is **required**. Without it `express.json()` ignores the body.

### What does `extended: true` mean?

For `urlencoded`: `true` uses the `qs` library, which supports nested objects (`user[name]=Anu`). `false` uses the simpler built-in `querystring`. For a beginner, either works for flat forms. Using `{ extended: true }` is the common choice.

### GET vs POST summary

| | GET | POST |
|---|---|---|
| Purpose | Read data | Send data to save/create |
| Data location | URL (query string) | Request body |
| Visible in URL? | Yes | No |
| Size limit | Small | Large |
| Safe to repeat? | Yes | No (may create duplicates) |
| Browser bookmark | Possible | Not meaningful |
| Express | `app.get`, `req.query`, `req.params` | `app.post`, `req.body` |

**Real-world example.** Every login form, signup, payment (PayPal checkout), order placement (Swiggy "Place order"), and tweet/post (LinkedIn "Post") is a POST request. The server reads `req.body`, checks it, saves to a database and replies with a status such as 201 (created).

**Common mistakes**
- Not adding `express.json()` or `express.urlencoded()`, so `req.body` is `undefined` and the app crashes with "Cannot destructure property of undefined".
- Adding the body parser **after** the routes. Order matters.
- Sending JSON from `fetch` without `Content-Type: application/json`.
- HTML form fields without a `name` attribute. Only fields with `name` are sent.
- Testing a POST route by typing the URL in the browser. The address bar always sends GET; you get `Cannot GET /feedback` (or a different handler runs).
- Not validating input.

**Check your understanding**
1. Where is the data in a POST request?
2. What happens to `req.body` if we forget `express.json()`?
3. Which middleware handles a normal HTML form? Which handles `fetch` with JSON?
4. Why can't we test a POST route by typing the URL into the browser?

## 7.6 Serving static files: `express.static`

**Simple explanation.** `express.static('public')` is a **built-in middleware** that serves every file inside the `public` folder, with the right `Content-Type`, with security checks and caching headers. All our 60 lines of static server code become **one line**.

**Analogy.** It is the **self-service shelf** in the college library. Anything on that shelf (the `public` folder) can be taken by anyone. Things in the staff room (the rest of your project) are not reachable.

### Folder structure

```
express-static/
  app.js
  package.json
  public/
    index.html
    css/style.css
    js/app.js
```

(Use the same `index.html`, `style.css`, `app.js` files from Topic 3.)

### `app.js`

```js
// app.js
const express = require('express');
const path = require('path');

const app = express();

// Serve everything in /public. Use an absolute path for safety.
app.use(express.static(path.join(__dirname, 'public')));

// Optional: serve under a prefix, so /assets/css/style.css works
// app.use('/assets', express.static(path.join(__dirname, 'public')));

// A normal route still works alongside
app.get('/api/hello', (req, res) => {
  res.json({ message: 'Hello from the API' });
});

// Fallback for unknown URLs (put LAST)
app.use((req, res) => {
  res.status(404).send('<h1>404 - Page not found</h1>');
});

app.listen(3000, () => console.log('Static + API at http://localhost:3000'));
```

Run: `node app.js`

| URL | Result |
|---|---|
| `http://localhost:3000/` | Serves `public/index.html` automatically |
| `http://localhost:3000/css/style.css` | CSS with `Content-Type: text/css` |
| `http://localhost:3000/js/app.js` | The JavaScript file |
| `http://localhost:3000/api/hello` | `{"message":"Hello from the API"}` |
| `http://localhost:3000/xyz` | `404 - Page not found` |

Note: the folder name `public` is **not** part of the URL. The file `public/css/style.css` is reached at `/css/style.css`.

**Real-world example.** A single-page application (React or Angular front end) is usually built into a `dist` or `build` folder of static files. A small Express server often serves that folder with `express.static`, and also provides `/api/...` routes for data. This pattern is very common in company projects.

**Common mistakes**
- Using a relative path `express.static('public')` and running the server from another folder. `path.join(__dirname, 'public')` is safer.
- Putting `public` in the URL: `/public/css/style.css` (wrong; use `/css/style.css`).
- Putting secret files (like `.env` or the JSON data file) inside `public`. Everything inside is downloadable by anyone.
- Placing the 404 fallback **before** `express.static`, so files are never found.

**Check your understanding**
1. What does `express.static('public')` do?
2. If a file is at `public/images/logo.png`, what URL shows it?
3. Why should secrets never be placed in the `public` folder?

## 7.7 A short introduction to middleware

**Simple explanation.** **Middleware** is a function that runs **in the middle**: after the request arrives, **before** the final handler sends the response. It can look at or change `req` and `res`, then either **end the response** or call `next()` to pass control to the next function in line.

A middleware function looks like this:

```js
function myMiddleware(req, res, next) {
  // do something with req / res
  next();   // pass on to the next one
}
```

**Analogy: passport control and security at an airport** (or the **KSRTC bus depot gate**). Before you reach the bus, you pass gates: ticket check, bag scan, ID check. Each gate can **let you through** (`next()`) or **stop you** (send a response). The bus (route handler) is the last step.

```
Request
   |
   v
[ Logger ] --next()--> [ express.json() ] --next()--> [ Auth check ] --next()--> [ Route handler ]
   |                         |                             |                          |
   |                         |                      (no token? STOP,                  v
   |                         |                       send 401)                    Response
```

**Express's main idea:** an Express app is **a chain of middleware functions**, run in the order they were added with `app.use()` or `app.get()` etc.

### Types of middleware

| Type | Example |
|---|---|
| **Built-in** | `express.json()`, `express.urlencoded()`, `express.static()` |
| **Third-party** (from npm) | `morgan` (logging), `cors`, `helmet` (security), `cookie-parser` |
| **Custom** (your own) | A logger, a login check |
| **Error-handling** | Has four parameters `(err, req, res, next)` |

### Code example

```js
// middleware.js
const express = require('express');
const app = express();

// 1. Custom logger: runs for EVERY request
app.use((req, res, next) => {
  const time = new Date().toLocaleTimeString();
  console.log(`[${time}] ${req.method} ${req.url}`);
  next();   // do not forget this!
});

// 2. Built-in body parser
app.use(express.json());

// 3. Middleware only for one route: simple "API key" check
function checkKey(req, res, next) {
  if (req.query.key === 'secret123') {
    next();                       // allowed
  } else {
    res.status(401).json({ error: 'Invalid key' });   // stop here
  }
}

app.get('/', (req, res) => {
  res.send('Public home page');
});

app.get('/admin', checkKey, (req, res) => {
  res.send('Welcome, admin!');
});

// 4. Error-handling middleware (4 parameters, goes LAST)
app.get('/crash', (req, res) => {
  throw new Error('Something broke!');
});

app.use((err, req, res, next) => {
  console.error('Error caught:', err.message);
  res.status(500).json({ error: 'Internal Server Error' });
});

app.listen(3000, () => console.log('Middleware demo on http://localhost:3000'));
```

Run: `node middleware.js`

Visit these in order:

| URL | Browser shows | Terminal log |
|---|---|---|
| `/` | `Public home page` | `[10:30:01 AM] GET /` |
| `/admin` | `{"error":"Invalid key"}` (401) | `[10:30:05 AM] GET /admin` |
| `/admin?key=secret123` | `Welcome, admin!` | `[10:30:10 AM] GET /admin?key=secret123` |
| `/crash` | `{"error":"Internal Server Error"}` (500) | `[...] GET /crash` then `Error caught: Something broke!` |

**Rules to remember**
1. Order matters: middleware runs top to bottom.
2. Always call `next()` **or** send a response. If you do neither, the request hangs.
3. Never do both (send a response **and** call `next()` to a handler that sends another).
4. `app.use(fn)` runs for all methods and paths. `app.use('/api', fn)` runs only for paths that start with `/api`.
5. Error handlers have **four** parameters and are placed **last**.

**Real-world example.** In real companies, middleware handles: logging every request (Uber's services), checking login tokens (LinkedIn), limiting too many requests from one user (rate limiting for PayPal APIs), compressing responses, and adding security headers. Almost every Express app begins with a stack of middleware.

**Common mistakes**
- Forgetting `next()`. The page loads forever.
- Putting `express.json()` after the routes.
- Putting the error handler before the routes.
- Calling `next()` after already sending a response.
- Thinking middleware is only for third-party packages. Any function with `(req, res, next)` is middleware.

**Check your understanding**
1. What is middleware? Where does it sit in the request flow?
2. What happens if middleware neither calls `next()` nor sends a response?
3. Is `express.static` a middleware? How do we know?
4. Write a middleware that prints the HTTP method and URL of every request.

### Classroom activity 6: "Gate keeper" (15 minutes)
Add a middleware to `middleware.js` that blocks any request between `/secret/...` unless the header `x-user: teacher` is present. Test with curl: `curl -H "x-user: teacher" http://localhost:3000/secret/marks`.

---

# 8. Mini-project: College Notice Board

**Goal:** A small website where students can see notices, and staff can add a notice. We build it twice:

- **Version 1:** plain `http` module. Static files plus routing. Read-only list (GET).
- **Version 2:** rewritten in Express. GET and POST routes. Notices saved to a JSON file using `fs`.

Doing both shows students how much work Express saves.

## 8.1 Folder structure

```
notice-board/
  package.json
  server-plain.js        (Version 1: http module)
  server-express.js      (Version 2: Express)
  data/
    notices.json         (our tiny "database")
  public/
    index.html
    css/
      style.css
    js/
      app.js
```

Setup:

```bash
mkdir notice-board
cd notice-board
npm init -y
npm install express
mkdir data public public/css public/js
```

Add scripts to `package.json`:

```json
"scripts": {
  "plain": "node server-plain.js",
  "start": "node server-express.js"
}
```

## 8.2 Shared files (used by both versions)

### `data/notices.json`

```json
[
  {
    "id": 1,
    "title": "Internal Exam Timetable",
    "body": "Series test 1 begins on Monday. Check the department board.",
    "date": "2026-10-05"
  },
  {
    "id": 2,
    "title": "Onam Celebration",
    "body": "College Onam celebration on Friday at 10 AM in the main auditorium.",
    "date": "2026-10-06"
  }
]
```

### `public/index.html`

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>College Notice Board</title>
  <link rel="stylesheet" href="/css/style.css">
</head>
<body>
  <header>
    <h1>College Notice Board</h1>
  </header>

  <main>
    <section id="add-section">
      <h2>Add a notice</h2>
      <form id="notice-form">
        <input type="text" id="title" placeholder="Title" required>
        <textarea id="body" placeholder="Notice text" rows="3" required></textarea>
        <button type="submit">Post notice</button>
      </form>
      <p id="status"></p>
    </section>

    <section>
      <h2>Latest notices</h2>
      <div id="notice-list">Loading...</div>
    </section>
  </main>

  <script src="/js/app.js"></script>
</body>
</html>
```

### `public/css/style.css`

```css
* { box-sizing: border-box; }

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f1f5f9;
  color: #1e293b;
}

header {
  background: #1e3a8a;
  color: white;
  padding: 16px 24px;
}

main {
  max-width: 700px;
  margin: 24px auto;
  padding: 0 16px;
}

form input, form textarea {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid #cbd5e1;
  border-radius: 6px;
  font-size: 15px;
}

button {
  background: #1e3a8a;
  color: white;
  border: none;
  padding: 10px 18px;
  border-radius: 6px;
  cursor: pointer;
}

.notice {
  background: white;
  border-left: 5px solid #f59e0b;
  padding: 12px 16px;
  margin-bottom: 12px;
  border-radius: 6px;
}

.notice h3 { margin: 0 0 6px; }
.notice small { color: #64748b; }
```

### `public/js/app.js` (browser code, uses `fetch`)

```js
const listDiv = document.getElementById('notice-list');
const form = document.getElementById('notice-form');
const statusP = document.getElementById('status');

async function loadNotices() {
  try {
    const res = await fetch('/api/notices');
    const notices = await res.json();

    if (notices.length === 0) {
      listDiv.textContent = 'No notices yet.';
      return;
    }

    listDiv.innerHTML = '';
    // newest first
    notices.slice().reverse().forEach((n) => {
      const div = document.createElement('div');
      div.className = 'notice';

      const h3 = document.createElement('h3');
      h3.textContent = n.title;          // textContent is safe from script injection

      const p = document.createElement('p');
      p.textContent = n.body;

      const small = document.createElement('small');
      small.textContent = 'Posted on ' + n.date;

      div.append(h3, p, small);
      listDiv.appendChild(div);
    });
  } catch (err) {
    listDiv.textContent = 'Could not load notices.';
  }
}

form.addEventListener('submit', async (e) => {
  e.preventDefault();
  const title = document.getElementById('title').value.trim();
  const body = document.getElementById('body').value.trim();

  try {
    const res = await fetch('/api/notices', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ title, body })
    });

    if (res.ok) {
      statusP.textContent = 'Notice posted!';
      form.reset();
      loadNotices();
    } else {
      const err = await res.json().catch(() => ({}));
      statusP.textContent = 'Error: ' + (err.error || res.status);
    }
  } catch (err) {
    statusP.textContent = 'Network error.';
  }
});

loadNotices();
```

## 8.3 Version 1: plain `http` module (static files and routing)

This version serves the files in `public/` and answers `GET /api/notices` by reading the JSON file. It cannot save new notices (we would need to parse the body by hand; see section 6.2). When a student presses "Post notice" here they get a 405 error. That is the **teaching point**: the plain version gets messy fast.

### `server-plain.js`

```js
// server-plain.js
const http = require('http');
const fs = require('fs');
const path = require('path');

const PORT = 3000;
const PUBLIC_DIR = path.join(__dirname, 'public');
const DATA_FILE = path.join(__dirname, 'data', 'notices.json');

const MIME_TYPES = {
  '.html': 'text/html; charset=utf-8',
  '.css':  'text/css; charset=utf-8',
  '.js':   'text/javascript; charset=utf-8',
  '.json': 'application/json; charset=utf-8',
  '.png':  'image/png',
  '.jpg':  'image/jpeg',
  '.ico':  'image/x-icon'
};

function sendJson(res, status, obj) {
  res.writeHead(status, { 'Content-Type': 'application/json; charset=utf-8' });
  res.end(JSON.stringify(obj));
}

function serveStatic(urlPath, res) {
  if (urlPath === '/') urlPath = '/index.html';

  const filePath = path.join(PUBLIC_DIR, urlPath);
  if (!filePath.startsWith(PUBLIC_DIR)) {
    res.writeHead(403, { 'Content-Type': 'text/plain' });
    return res.end('Forbidden');
  }

  const ext = path.extname(filePath).toLowerCase();
  const type = MIME_TYPES[ext] || 'application/octet-stream';

  fs.readFile(filePath, (err, content) => {
    if (err) {
      res.writeHead(err.code === 'ENOENT' ? 404 : 500, { 'Content-Type': 'text/html; charset=utf-8' });
      return res.end(err.code === 'ENOENT' ? '<h1>404 - Not found</h1>' : '<h1>500 - Server error</h1>');
    }
    res.writeHead(200, { 'Content-Type': type });
    res.end(content);
  });
}

const server = http.createServer((req, res) => {
  let pathname;
  try {
    pathname = decodeURIComponent(new URL(req.url, 'http://localhost').pathname);
  } catch (e) {
    res.writeHead(400, { 'Content-Type': 'text/plain' });
    return res.end('Bad Request');
  }

  // ---- Routing ----
  if (pathname === '/api/notices') {
    if (req.method === 'GET') {
      fs.readFile(DATA_FILE, 'utf8', (err, text) => {
        if (err) return sendJson(res, 500, { error: 'Could not read notices' });
        try {
          sendJson(res, 200, JSON.parse(text));
        } catch (e) {
          sendJson(res, 500, { error: 'Notice file is damaged' });
        }
      });
    } else {
      sendJson(res, 405, { error: 'Only GET is supported in the plain version' });
    }
    return;
  }

  // Everything else: try static files (GET only)
  if (req.method === 'GET') {
    serveStatic(pathname, res);
  } else {
    res.writeHead(405, { 'Content-Type': 'text/plain' });
    res.end('Method Not Allowed');
  }
});

server.listen(PORT, () => {
  console.log(`Plain server (Version 1) running at http://localhost:${PORT}`);
});
```

Run:

```bash
npm run plain
```

Expected terminal output:

```
> notice-board@1.0.0 plain
> node server-plain.js

Plain server (Version 1) running at http://localhost:3000
```

Check:
- `http://localhost:3000/` shows the page with the two notices from the JSON file.
- `http://localhost:3000/api/notices` shows the raw JSON.
- Posting a notice shows "Error: Only GET is supported in the plain version".
- `http://localhost:3000/nothing` shows `404 - Not found`.

Stop the server with Ctrl + C before running Version 2 (same port).

## 8.4 Version 2: Express (GET and POST, saving to the JSON file)

### `server-express.js`

```js
// server-express.js
const express = require('express');
const fs = require('fs').promises;
const path = require('path');

const app = express();
const PORT = 3000;
const DATA_FILE = path.join(__dirname, 'data', 'notices.json');

// ---------- Helper functions to read and write the JSON file ----------
async function readNotices() {
  try {
    const text = await fs.readFile(DATA_FILE, 'utf8');
    return JSON.parse(text);
  } catch (err) {
    if (err.code === 'ENOENT') return [];   // file missing means no notices yet
    throw err;
  }
}

async function writeNotices(notices) {
  await fs.writeFile(DATA_FILE, JSON.stringify(notices, null, 2));
}

// ---------- Middleware ----------
app.use((req, res, next) => {                     // simple logger
  console.log(`${req.method} ${req.url}`);
  next();
});
app.use(express.json());                          // JSON bodies (from fetch)
app.use(express.urlencoded({ extended: true }));  // HTML form bodies
app.use(express.static(path.join(__dirname, 'public')));

// ---------- Routes ----------

// GET all notices (optional search: /api/notices?q=onam)
app.get('/api/notices', async (req, res) => {
  try {
    let notices = await readNotices();
    const q = req.query.q;
    if (q) {
      const term = q.toLowerCase();
      notices = notices.filter(n =>
        n.title.toLowerCase().includes(term) || n.body.toLowerCase().includes(term)
      );
    }
    res.json(notices);
  } catch (err) {
    console.error(err);
    res.status(500).json({ error: 'Could not read notices' });
  }
});

// GET one notice by id (route parameter)
app.get('/api/notices/:id', async (req, res) => {
  try {
    const id = Number(req.params.id);
    const notices = await readNotices();
    const notice = notices.find(n => n.id === id);
    if (!notice) {
      return res.status(404).json({ error: 'Notice not found' });
    }
    res.json(notice);
  } catch (err) {
    console.error(err);
    res.status(500).json({ error: 'Server error' });
  }
});

// POST a new notice
app.post('/api/notices', async (req, res) => {
  try {
    const { title, body } = req.body || {};

    if (!title || !body || !title.trim() || !body.trim()) {
      return res.status(400).json({ error: 'title and body are required' });
    }

    const notices = await readNotices();
    const nextId = notices.length ? Math.max(...notices.map(n => n.id)) + 1 : 1;

    const notice = {
      id: nextId,
      title: title.trim(),
      body: body.trim(),
      date: new Date().toISOString().slice(0, 10)   // like 2026-10-09
    };

    notices.push(notice);
    await writeNotices(notices);

    res.status(201).json(notice);
  } catch (err) {
    console.error(err);
    res.status(500).json({ error: 'Could not save notice' });
  }
});

// 404 for anything else (must be LAST)
app.use((req, res) => {
  res.status(404).send('<h1>404 - Not found</h1>');
});

app.listen(PORT, () => {
  console.log(`Express server (Version 2) running at http://localhost:${PORT}`);
});
```

Run:

```bash
npm start
```

Expected terminal output:

```
> notice-board@1.0.0 start
> node server-express.js

Express server (Version 2) running at http://localhost:3000
GET /
GET /css/style.css
GET /js/app.js
GET /api/notices
```

(The log lines appear after you open the page.)

Test with curl:

```bash
# list
curl http://localhost:3000/api/notices

# one notice
curl http://localhost:3000/api/notices/2

# search
curl "http://localhost:3000/api/notices?q=onam"

# add a notice
curl -X POST -H "Content-Type: application/json" \
  -d '{"title":"Lab Holiday","body":"Computer lab closed on Saturday."}' \
  http://localhost:3000/api/notices
```

The last command returns (status 201; the date will be today's):

```
{"id":3,"title":"Lab Holiday","body":"Computer lab closed on Saturday.","date":"2026-10-09"}
```

Open `data/notices.json`. You will see the new notice saved. **Stop the server and start it again; the notice is still there.** This is the difference from the in-memory array we used before.

### Comparing Version 1 and Version 2

| Point | Version 1 (http) | Version 2 (Express) |
|---|---|---|
| Static files | About 25 lines, our own MIME table | One line: `express.static` |
| Routing | `if` / `else if` on `req.url` | `app.get`, `app.post` |
| Route parameter `/api/notices/2` | Cut the string by hand | `req.params.id` |
| Query `?q=onam` | `new URL(...).searchParams` | `req.query.q` |
| POST body | Collect chunks, `JSON.parse` | `express.json()` |
| JSON reply | `writeHead`, `JSON.stringify`, `end` | `res.status(201).json(obj)` |

### Extension ideas for fast students
1. Add `DELETE /api/notices/:id` with `app.delete`, and a delete button on each notice.
2. Add a simple password check middleware for POST (header `x-admin-key`).
3. Add a `category` field and filter with `?category=exam`.
4. Replace the JSON file with a database in the next module.

### Notes for the teacher about the JSON file approach
- Two users saving at the same instant can overwrite each other (a "race condition"). For a small college project this is acceptable; real systems use a database, which handles this.
- The `data` folder is **outside** `public`, so nobody can download the raw file directly; they must use our API.

**Real-world example.** The pattern (browser page, JSON API, storage) is exactly the same shape as LinkedIn's feed, IRCTC's train list or Swiggy's restaurant list. Only the storage (a big database instead of one file) and the size are different.

**Common mistakes in the project**
- `npm start` or `node` run from the wrong folder, so `package.json` or the data file is not found (our code uses `__dirname`, so the data path is safe, but `npm` needs the right folder).
- Forgetting to stop Version 1 before running Version 2: `EADDRINUSE`.
- Putting `notices.json` inside `public`.
- Writing invalid JSON by hand in `notices.json` (a trailing comma breaks `JSON.parse`).
- Posting JSON from `fetch` without the `Content-Type` header.
- Using `res.send` after `res.json` in the same handler.

**Check your understanding**
1. Why does Version 1 reply with 405 for a POST?
2. Which line in Version 2 saves the notice to disk?
3. How does the browser JavaScript get the list of notices?
4. Why do we find the next id with `Math.max`?

---

# 9. Question bank (KTU exam style)

Marks follow the KTU pattern: **Part A** has short questions of 3 marks each; **Part B** has 9-mark questions with parts (a) and (b).

## Part A: 3 marks each (answer all)

1. State the purpose of npm.
2. List any three features of Node.js.
3. Differentiate between synchronous and asynchronous file reading in Node.js.
4. What is the use of `package.json`?
5. Write a Node.js statement to display the full path of the current folder and the extension of the file `report.pdf`.
6. What is the difference between `fs.writeFile()` and `fs.appendFile()`?
7. What is the purpose of `req.url` and `req.method` in a Node.js server?
8. What is the use of the `Content-Type` header? Give the values used for HTML, CSS and JavaScript files.
9. Distinguish between route parameters and query strings in Express with one example each.
10. What is middleware in Express.js? Name any two built-in middleware.

### Model answers for Part A (key points; marking scheme in brackets)

**Q1. Purpose of npm (3 marks)**
npm (Node Package Manager) is the default package manager of Node.js. It is used to:
- install and remove third-party packages from the online npm registry (`npm install express`) [1];
- record the project's name, version, scripts and dependencies in `package.json`, and lock exact versions in `package-lock.json` [1];
- run project scripts (`npm start`) and share one's own packages [1].

**Q2. Three features (3 marks)**
Single-threaded with event loop; non-blocking asynchronous I/O; large package ecosystem (npm); same language (JavaScript) on client and server; very fast V8 engine; cross-platform. Any three, one line of explanation each.

**Q3. Sync vs async (3 marks)**
`fs.readFileSync` blocks the program until reading finishes and returns the data directly (errors are thrown, so use try/catch) [1.5]. `fs.readFile` does not block; it starts the read, the program continues, and a callback `(err, data)` runs later when ready [1.5]. In servers, async is preferred because sync freezes all users.

**Q4. package.json (3 marks)**
It is the metadata file of a Node project. It stores the name, version, entry file (`main`), scripts, and lists of `dependencies` and `devDependencies`. It is created by `npm init`. With it, anyone can rebuild the project's packages by running `npm install`.

**Q5.** 

```js
const path = require('path');
console.log(__dirname);                  // full path of the current folder
console.log(path.extname('report.pdf')); // .pdf
```

**Q6.** `writeFile` creates a file or **replaces** the old content completely. `appendFile` creates a file if missing or **adds** to the end, keeping old content.

**Q7.** `req.url` is the path (with query string) requested by the client, such as `/about`. `req.method` is the HTTP method (GET, POST, ...). The server uses both to decide which route/response to run.

**Q8.** `Content-Type` tells the browser the kind of data in the response so that it can show or run it correctly. HTML: `text/html`; CSS: `text/css`; JavaScript: `text/javascript` (or `application/javascript`).

**Q9.** Route parameter: part of the path, identifies one resource, read with `req.params`. Example: route `/students/:id`, URL `/students/5`, `req.params.id` is `'5'`. Query string: after `?`, used to filter or search, read with `req.query`. Example: `/students?branch=CSE`, `req.query.branch` is `'CSE'`.

**Q10.** Middleware is a function `(req, res, next)` that runs between receiving the request and sending the response; it can change `req`/`res`, end the response, or call `next()`. Built-in: `express.json()`, `express.urlencoded()`, `express.static()`.

## Part B: 9 marks each

**Q11.**
(a) Explain the purpose of npm and how it is used in Node.js projects. (5 marks)
(b) Describe the steps to create a project, install Express and record it in `package.json`. (4 marks)

**Q12.**
(a) Write an `http` module snippet that responds with "Hello, World!". (4 marks)
(b) Explain each line of your program. (5 marks)

**Q13.**
(a) Explain the key features and advantages of Node.js. (5 marks)
(b) How does Node.js differ from traditional server-side technologies such as PHP/Apache and Java? (4 marks)

**Q14.**
(a) Write a Node.js script using the `fs` module to read a file and display its content in the console. (4 marks)
(b) Explain the difference between `readFile`, `readFileSync` and the promise version with short code. (5 marks)

**Q15.**
(a) Explain how a basic web server is created using the `http` module. (5 marks)
(b) Explain how routing is handled, with an example that serves `/`, `/about` and a 404 page. (4 marks)

**Q16.**
(a) Write an Express.js program that handles a GET request at `/welcome` and sends "Welcome to Express". (4 marks)
(b) Explain route parameters, query strings, `express.json()` and `express.urlencoded()` with examples. (5 marks)

**Extra Part B questions for practice**

**Q17.**
(a) Explain the event loop in Node.js with a neat diagram. (5 marks)
(b) Explain the role of the `path` module with any four functions and `__dirname`. (4 marks)

**Q18.**
(a) Write a Node.js program using the `http` module to serve static HTML, CSS and JS files with the correct `Content-Type`. (6 marks)
(b) What is middleware? Write a custom logger middleware for Express. (3 marks)

---

## Model answers for Part B

### Q11 (a). Purpose of npm and how it is used (5 marks)

**What is npm?** npm stands for Node Package Manager. It is installed along with Node.js. It has two parts: (1) an online **registry** that stores more than two million free packages (libraries), and (2) a **command-line tool** to download and manage them. [1]

**Purposes** [2]
1. Install third-party packages: `npm install express`.
2. Manage dependencies: names and versions are saved in `package.json`; exact versions in `package-lock.json`.
3. Run scripts: `npm start`, `npm run dev`, `npm test`.
4. Share code: developers publish their packages with `npm publish`.
5. Update and remove packages: `npm update`, `npm uninstall`.

**How it is used in a project** [2]

```bash
npm init -y                  # creates package.json
npm install express          # downloads Express into node_modules, adds to dependencies
npm install --save-dev nodemon   # tool needed only during development
npm install                  # on another computer: installs everything in package.json
npm start                    # runs the "start" script
```

In code: `const express = require('express');`

The `node_modules` folder is not shared (it is big); only `package.json` and `package-lock.json` are shared.

### Q11 (b). Steps (4 marks)

1. `mkdir myapp` and `cd myapp` [0.5]
2. `npm init -y` creates `package.json` [1]
3. `npm install express` downloads Express and adds `"express": "^x.y.z"` to `dependencies`; creates `node_modules` and `package-lock.json` [1.5]
4. Create `app.js` with `require('express')` and run `node app.js` [1]

### Q12. `http` module snippet and explanation (9 marks)

(a)

```js
const http = require('http');

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Hello, World!');
});

server.listen(3000, () => {
  console.log('Server running at http://localhost:3000/');
});
```

Output in the browser at `http://localhost:3000`: `Hello, World!`

(b) Explanation
- `require('http')` loads the built-in HTTP module. [1]
- `http.createServer(callback)` creates a server object. The callback runs for every incoming request; it receives `req` (request) and `res` (response). [1.5]
- `res.writeHead(200, {...})` sends the status line `200 OK` and the header `Content-Type: text/plain`, which tells the browser that the body is plain text. [1]
- `res.end('Hello, World!')` writes the body and finishes the response. Without it the browser waits forever. [1]
- `server.listen(3000, cb)` makes the server wait for connections on port 3000; `cb` runs once when it starts. [1.5]

### Q13 (a). Key features and advantages of Node.js (5 marks)

Node.js is an open-source, cross-platform **JavaScript runtime** built on Chrome's V8 engine that allows JavaScript to run outside the browser.

| Feature | Advantage |
|---|---|
| Single-threaded | Simple model; low memory; no thread-locking problems |
| Event loop | One thread can serve thousands of users |
| Non-blocking (asynchronous) I/O | Does not wait for file/database; high throughput |
| npm ecosystem | Huge number of ready-made packages; faster development |
| JavaScript everywhere | Same language for front end and back end; JSON everywhere; one team |
| V8 engine | Fast execution |
| Cross-platform | Same code on Windows, Mac, Linux |
| Suited for real-time apps | Chat, live updates, streaming; used by Netflix, LinkedIn, Uber, PayPal |

(Any five rows with one-line explanation: 1 mark each.)

### Q13 (b). Differences from traditional technologies (4 marks)

| Point | PHP + Apache | Java (servlets) | Node.js |
|---|---|---|---|
| Model | Process/thread per request | Thread per request (thread pool) | Single thread + event loop |
| Waiting for I/O | Thread blocked | Thread blocked | Not blocked; callback later |
| Memory under load | High | High | Low |
| Language | PHP (back end only) | Java | JavaScript (front and back) |
| Best for | Content sites | Large enterprise apps, heavy computing | Real-time, API, many connections |
| Weakness | Slower with many users | Heavy, verbose | Heavy CPU tasks block the thread |

Explain: In traditional servers every user needs a thread that sits idle while waiting for the database. With 1000 users, 1000 threads use a lot of memory. In Node.js a single thread starts the slow work, moves to the next user and returns when the result is ready, so waiting costs almost nothing. [4 marks for table and explanation]

### Q14 (a). `fs` script to read a file and show it (4 marks)

```js
const fs = require('fs');

fs.readFile('data.txt', 'utf8', (err, data) => {
  if (err) {
    console.error('Error reading file:', err.message);
    return;
  }
  console.log('File content:');
  console.log(data);
});
```

Assume `data.txt` contains `Welcome to Node.js`. Output:

```
File content:
Welcome to Node.js
```

Explanation: `readFile` reads the file asynchronously; `'utf8'` converts bytes to text; the callback's first argument `err` is checked first (for example `ENOENT` if the file is missing); `data` holds the content which is printed with `console.log`. [Code 2, explanation 1, output 1]

### Q14 (b). Three styles (5 marks)

```js
const fs = require('fs');

// 1. Synchronous: blocks; returns data; use try/catch
try {
  const d = fs.readFileSync('data.txt', 'utf8');
  console.log(d);
} catch (e) { console.error(e.message); }

// 2. Callback: non-blocking
fs.readFile('data.txt', 'utf8', (err, d) => {
  if (err) return console.error(err.message);
  console.log(d);
});

// 3. Promise with async/await: non-blocking and clean
const fsp = require('fs').promises;
(async () => {
  try {
    console.log(await fsp.readFile('data.txt', 'utf8'));
  } catch (e) { console.error(e.message); }
})();
```

Points: sync blocks the thread, callback uses the error-first pattern, promises avoid "callback hell" and allow `await`. Do not use sync inside servers. [3 for code, 2 for points]

### Q15 (a). Creating a basic web server with `http` (5 marks)

Steps [3]:
1. Import `http`.
2. `http.createServer((req, res) => {...})` creates the server; the callback runs on each request.
3. Inside it, set status and headers with `res.writeHead(200, {'Content-Type': 'text/html'})`.
4. Send the body and end: `res.end('<h1>Hello</h1>')`.
5. `server.listen(port)` starts listening.

Code [2]:

```js
const http = require('http');
const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/html' });
  res.end('<h1>Hello from Node server</h1>');
});
server.listen(3000, () => console.log('Listening on 3000'));
```

When the browser sends a request to `localhost:3000`, Node calls the callback, we write the response, and the browser displays it (see request/response cycle diagram).

### Q15 (b). Routing (4 marks)

Routing means choosing the response based on `req.url` and `req.method`.

```js
const http = require('http');

const server = http.createServer((req, res) => {
  if (req.url === '/' && req.method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'text/html' });
    res.end('<h1>Home</h1>');
  } else if (req.url === '/about' && req.method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'text/html' });
    res.end('<h1>About us</h1>');
  } else {
    res.writeHead(404, { 'Content-Type': 'text/html' });
    res.end('<h1>404 - Page not found</h1>');
  }
});

server.listen(3000);
```

Outputs: `/` shows Home, `/about` shows About us, anything else shows the 404 page. For query strings, use `new URL(req.url, 'http://localhost')` and `pathname`/`searchParams`. In large apps, Express is used because the `if/else` chain becomes long. [Explanation 1.5, code 2, outputs 0.5]

### Q16 (a). Express GET `/welcome` (4 marks)

```js
const express = require('express');
const app = express();

app.get('/welcome', (req, res) => {
  res.send('Welcome to Express');
});

app.listen(3000, () => {
  console.log('Server started on port 3000');
});
```

Install with `npm install express`, run with `node app.js`, visit `http://localhost:3000/welcome`. Output: `Welcome to Express`. [Install and import 1, route 1.5, listen 1, output 0.5]

### Q16 (b). Params, query, body parsers (5 marks)

- **Route parameters** (`req.params`) [1]: `app.get('/students/:id', (req,res) => res.send(req.params.id));` URL `/students/5` gives `5`.
- **Query strings** (`req.query`) [1]: `app.get('/search', (req,res) => res.send(req.query.q));` URL `/search?q=bus` gives `bus`.
- **`express.json()`** [1.5]: built-in middleware that reads a request body of type `application/json` and puts the object in `req.body`. `app.use(express.json());` `app.post('/add', (req,res) => res.json(req.body));` A POST with `{"a":1}` returns `{"a":1}`.
- **`express.urlencoded({ extended: true })`** [1.5]: reads HTML form data (`application/x-www-form-urlencoded`), such as `name=Anu&age=20`, into `req.body`.

Both parsers must be registered with `app.use()` **before** the routes that use `req.body`.

### Q17 (a). Event loop (5 marks)

Draw the event loop diagram from section 3.2 [2 marks]. Explain [3 marks]: Node runs JavaScript in a single thread (call stack). When code asks for slow I/O (file, network, timer), Node gives the work to the operating system or to background threads (libuv). The main thread continues with the next code. When the background work ends, its callback is added to the **callback queue**. The **event loop** continuously checks whether the call stack is empty; if so, it takes the next callback from the queue and runs it. In this way one thread handles many requests without waiting. Example: the restaurant waiter who submits an order and serves other tables until the kitchen bell rings.

### Q17 (b). `path` module (4 marks)

- `path.join()`: joins segments using the right separator for the OS.
- `path.basename('/a/b/c.txt')` gives `c.txt`.
- `path.dirname('/a/b/c.txt')` gives `/a/b`.
- `path.extname('/a/b/c.txt')` gives `.txt`.
- `path.resolve()`: makes an absolute path. `path.parse()`: breaks a path into parts.
- `__dirname` gives the absolute path of the folder holding the current script; used as `path.join(__dirname, 'public')` so paths do not depend on where the command was run. [1 each for any four, with example]

### Q18 (a). Static file server (6 marks)

Give the `server.js` of section 6.3 (shortened):

```js
const http = require('http');
const fs = require('fs');
const path = require('path');

const MIME = {
  '.html': 'text/html',
  '.css': 'text/css',
  '.js': 'text/javascript'
};

http.createServer((req, res) => {
  const file = req.url === '/' ? '/index.html' : req.url;
  const filePath = path.join(__dirname, 'public', file);
  const type = MIME[path.extname(filePath)] || 'application/octet-stream';

  fs.readFile(filePath, (err, content) => {
    if (err) {
      res.writeHead(404, { 'Content-Type': 'text/plain' });
      return res.end('404 Not Found');
    }
    res.writeHead(200, { 'Content-Type': type });
    res.end(content);
  });
}).listen(3000, () => console.log('Static server on 3000'));
```

Marks: MIME table 1.5, building the path with `path.join` 1, reading the file and error handling 2, setting header and sending 1, listen 0.5. (Mention the `../` safety check for full marks.)

### Q18 (b). Middleware (3 marks)

Middleware is a function `(req, res, next)` that runs between request and response; it may modify them, end the response, or call `next()`. [1.5]

```js
app.use((req, res, next) => {
  console.log(req.method, req.url);
  next();
});
```

[1.5: code with `next()`]

---

# 10. Classroom activities (collected list)

Earlier sections have small activities. Here are bigger ones for revision sessions.

### Activity A: "Be the event loop" (role play, 15 minutes)
- Five students are customers at a restaurant. One student is the **single waiter**. One student is the **kitchen**. One student is the **event loop** who rings a bell.
- First round: the waiter must **wait** at the kitchen for each dish (blocking). Time how long the five customers wait.
- Second round: the waiter submits all orders and only serves when the bell rings (non-blocking). Time again.
- Discuss: where did the time go? Who was idle?

### Activity B: "Guess the output" (10 minutes)
Show on the projector, ask students to predict the order before running:

```js
console.log('A');
setTimeout(() => console.log('B'), 0);
Promise.resolve().then(() => console.log('C'));
console.log('D');
```

Answer:

```
A
D
C
B
```

Reason: `A` and `D` are normal (synchronous) code. The promise callback (`C`) runs before the timer callback (`B`), because promise callbacks have higher priority than timers. Even a timer of 0 milliseconds waits until the main code finishes. (Advanced; for curious students.)

### Activity C: "Route map" (group, 15 minutes)
Each group picks an app (Swiggy, IRCTC, KSRTC booking) and lists five routes with method and purpose, for example `GET /restaurants`, `GET /restaurants/:id`, `POST /orders`, `GET /orders/:id`, `GET /search?q=biryani`. Groups present and the class says whether each should be params, query or body.

### Activity D: "Fix the broken server" (pairs, 20 minutes)
Give this code with five bugs. Students find and fix them.

```js
const express = require('express');
const app = express();

app.get('/students/:id', (req, res) => {
  res.send('Student ' + req.query.id);          // Bug 1: should be req.params.id
});

app.post('/add', (req, res) => {
  res.json({ got: req.body });                  // Bug 2: body parser missing (add app.use(express.json()) above)
});

app.use(express.json());                        // Bug 3: this is after the route

app.get('/slow', (req, res, next) => {
  console.log('checking...');                   // Bug 4: neither next() nor a response
});

app.listen(3000);                               // Bug 5: no message; add console.log callback (minor)
```

### Activity E: "Build in 30 minutes" (individual lab)
Build a **Canteen Menu** app with Express: `GET /menu` (list from `menu.json`), `GET /menu/:id`, `POST /menu` (add item with name and price, validate that price is a number), and a static page showing the menu. This is the same as the notice board with new nouns; students who can do it have understood the module.

### Activity F: "Postman or Thunder Client practice" (15 minutes)
Install the free **Thunder Client** extension in VS Code (or Postman). Test the notice board API: send GET, POST with JSON, POST with missing field (see the 400), and GET with a wrong id (see the 404).

---

# 11. Quick revision sheet

**Node.js** = JavaScript runtime (V8) for outside the browser. Single thread, event loop, non-blocking I/O.

**npm** = package manager. `npm init -y`, `npm install pkg`, `npm install`, `npm start`. `package.json` lists dependencies. Do not share `node_modules`.

**CommonJS:** `const x = require('x')`, `module.exports = ...`.

**fs:** `readFile`, `writeFile` (replaces), `appendFile` (adds); `Sync` blocks; callbacks are error-first; promises with `await`.

**path:** `join`, `resolve`, `basename`, `dirname`, `extname`, `parse`; `__dirname` is the script's folder.

**http server skeleton:**

```js
const http = require('http');
http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Hello, World!');
}).listen(3000);
```

**Routing (plain):** compare `req.url` and `req.method`; send 404 for unknown.

**Static files:** map extension to Content-Type; read file; send; block `../`.

**Express skeleton:**

```js
const express = require('express');
const app = express();
app.use(express.json());
app.use(express.urlencoded({ extended: true }));
app.use(express.static('public'));
app.get('/welcome', (req, res) => res.send('Welcome to Express'));
app.post('/data', (req, res) => res.status(201).json(req.body));
app.listen(3000);
```

**Where is the data?**

| Data | Where | Read with |
|---|---|---|
| `/students/5` | Path | `req.params.id` |
| `/search?q=bus` | URL after `?` | `req.query.q` |
| Form or JSON | Body | `req.body` (needs a parser) |

**Middleware:** `(req, res, next)`; call `next()` or send a response; order matters; error handlers have four parameters and come last.

**Status codes to remember:** 200 OK, 201 Created, 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found, 405 Method Not Allowed, 500 Server Error.

**Top five beginner errors**
1. `Cannot find module 'express'`: run `npm install express` in the project folder.
2. `EADDRINUSE`: the port is busy; stop the old server.
3. Browser spins: forgot `res.end()` / `res.send()` / `next()`.
4. `req.body` is undefined: forgot `express.json()` or `express.urlencoded()` (or put it after the route).
5. CSS/JS not loading: wrong `Content-Type`, wrong path, or `express.static` not set.

*End of Module 3.*
