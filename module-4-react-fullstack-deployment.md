# Module 4: Full Stack Integration using React and Deployment

**Course:** Web Application Development (MNCST509)
**Programme:** B.Tech CSE Minor, KTU, Semester 5
**Module:** 4 of the syllabus (11 contact hours)

This module is written for students with **no experience** in React or Git. Teach one idea at a time, run the example, then let students change it.

Through the module we build **one small app**: a **Student Feedback app**. A student types a name and a message, the message is saved in a database, and the page shows all messages.

---

## Contents

1. Component-based architecture using React
2. Forms and state using `useState` and `useEffect`
3. MongoDB in brief
4. Building the backend (Node.js, Express, MongoDB)
5. Connecting React to the backend
   - 5.1 Form component and handling input
   - 5.2 Submitting data with `fetch()` or Axios
   - 5.3 Receiving and displaying data (GET and POST)
   - 5.4 Conditional rendering, loading and error handling
6. Hosting the frontend
7. Deploying the backend (Express + MongoDB)
8. Connecting the frontend to the deployed backend
9. Introduction to Git: commit, push, pull, branching
10. Exam questions (short answers)

## Suggested lesson plan

| Class | Topic |
|---|---|
| 1 | Components, JSX, props. Setting up React |
| 2 | `useState`: a counter and a form |
| 3 | `useEffect` |
| 4 | MongoDB basics |
| 5 | Express API: GET and POST |
| 6 | React form and sending data |
| 7 | Showing data, loading and error messages |
| 8 | Git: commit, push, pull |
| 9 | Git: branching. Hosting the frontend |
| 10 | Deploying backend. Connecting both |
| 11 | Revision and exam questions |

## The big picture

```
  BROWSER (React app)              SERVER (Express)            DATABASE (MongoDB)
 +-------------------+  fetch   +------------------+        +----------------+
 | Form + list       | -------> | POST /api/feedback| -----> | save message   |
 |                   | <------- | (sends JSON back) | <----- |                |
 +-------------------+          +------------------+        +----------------+
```

**Analogy:** a restaurant again. React is the **menu and the order slip** the customer sees. Express is the **waiter and kitchen manager**. MongoDB is the **store room** where everything is kept.

---

# 1. Component-based Architecture using React

## 1.1 What is React?

**React** is a JavaScript library (made by Facebook) for building web pages out of small, reusable pieces called **components**.

**Analogy:** LEGO blocks. A big castle is built from small blocks. You make a block once and use it many times. A web page is the same: a `Header` block, a `Card` block, a `Button` block.

Think of the Swiggy app: the restaurant card is **one component**, used again and again for every restaurant in the list.

**Why it helps (exam point):**
- **Reusable:** write once, use many times.
- **Easy to maintain:** a bug in the button is fixed in one place.
- **Easy to grow:** a big app is just many small components.
- **Fast updates:** React changes only the part of the page that changed.

**Real world:** Facebook, Instagram, Netflix and Airbnb use React.

## 1.2 Setting up a React app

Install Node.js first (Module 3). Then in the terminal:

```
npm create vite@latest feedback-app
```

Choose **React**, then **JavaScript**. Then:

```
cd feedback-app
npm install
npm run dev
```

Open the address shown (usually http://localhost:5173). **Vite** is a tool that sets up and runs the React project for us.

The important files:

```
feedback-app/
  index.html        the one HTML page
  package.json      list of packages
  src/
    main.jsx        starts React
    App.jsx         our main component  <-- we edit this
```

## 1.3 Components and JSX

A component is just a **JavaScript function that returns HTML-like code**. That HTML-like code is called **JSX**.

```jsx
// src/App.jsx
function Welcome() {
  return <h2>Welcome to the feedback app</h2>;
}

function App() {
  return (
    <div>
      <Welcome />
      <Welcome />
      <p>This is my first React page.</p>
    </div>
  );
}

export default App;
```

Rules of JSX:
- Component names start with a **capital letter** (`Welcome`, not `welcome`).
- A component returns **one** outer element (wrap in a `<div>`).
- Use `className` instead of `class`.
- Put JavaScript inside curly braces: `<p>2 + 3 = {2 + 3}</p>`.
- Every tag must be closed: `<br />`, `<input />`.

## 1.4 Props: giving data to a component

**Props** (short for properties) are the values we pass into a component, like arguments to a function.

```jsx
function FeedbackItem(props) {
  return (
    <div style={{ border: "1px solid gray", margin: "8px", padding: "8px" }}>
      <b>{props.name}</b>
      <p>{props.message}</p>
    </div>
  );
}

function App() {
  return (
    <div>
      <FeedbackItem name="Anu" message="Great class!" />
      <FeedbackItem name="Rahul" message="Please share the notes." />
    </div>
  );
}

export default App;
```

One `FeedbackItem` block, used twice with different data.

**Common mistakes:**
- Lower-case component name (React treats it as a normal HTML tag).
- Forgetting the curly braces: `{props.name}`.
- Returning two elements side by side with no outer wrapper.

### Check your understanding
1. What is a component? What is JSX?
2. What are props? Give an example.
3. Give two reasons component-based design helps in big apps.

---

# 2. Forms and State using `useState` and `useEffect`

## 2.1 `useState`: remembering values

A normal variable does not make React update the page. **State** is a value that React **remembers**, and the page **updates automatically** when it changes.

**Analogy:** state is the **scoreboard** at a cricket match. When the score changes, the board shows the new number. You don't rebuild the stadium.

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}

export default Counter;
```

- `useState(0)` starts with the value `0`.
- `count` is the current value.
- `setCount` is the **only** way to change it.

## 2.2 A form with state

A **controlled input** keeps its value in state. Each key press updates the state.

```jsx
import { useState } from "react";

function NameForm() {
  const [name, setName] = useState("");
  const [shown, setShown] = useState("");

  function handleSubmit(e) {
    e.preventDefault();      // stop the page from reloading
    setShown(name);
    setName("");             // clear the box
  }

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <input
          value={name}
          onChange={(e) => setName(e.target.value)}
          placeholder="Your name"
        />
        <button type="submit">Submit</button>
      </form>
      {shown && <p>Hello, {shown}!</p>}
    </div>
  );
}

export default NameForm;
```

What happens: you type, `onChange` updates `name`. You press Submit, `handleSubmit` runs, and the name is displayed. This is the "form with `useState`" exam question.

## 2.3 `useEffect`: doing something after the page shows

`useEffect` runs code **after** the component appears on screen. We use it for things like **loading data from a server** when the page opens.

**Analogy:** you enter a restaurant (page shows), and **then** the waiter brings water (effect). It happens after you sit down.

```jsx
import { useState, useEffect } from "react";

function Clock() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const timer = setInterval(() => setSeconds((s) => s + 1), 1000);
    return () => clearInterval(timer);   // clean up when the component goes away
  }, []);                                // [] means: run only once, at the start

  return <p>Page open for {seconds} seconds</p>;
}

export default Clock;
```

The second part, `[]`, is the **dependency array**:

| Written as | Effect runs |
|---|---|
| `useEffect(fn, [])` | once, when the component first appears |
| `useEffect(fn, [name])` | first time, and again whenever `name` changes |
| `useEffect(fn)` | after every update (rarely wanted) |

**`useState` versus `useEffect` (exam point):**

| `useState` | `useEffect` |
|---|---|
| Stores a value that can change | Runs code after the page shows |
| Changing it updates the page | Used for fetching data and timers |

**Common mistakes:**
- Changing state directly (`count = count + 1`). Always use `setCount`.
- Forgetting `e.preventDefault()` in a form, so the page reloads.
- Forgetting `[]` in `useEffect`, which can cause an endless loop of fetches.

### Check your understanding
1. Why do we use `setCount` and not `count = count + 1`?
2. What does `[]` do in `useEffect`?
3. What is a controlled input?

---

# 3. MongoDB in Brief

**MongoDB** is a **database**: a place where an app keeps its data permanently.

Our earlier data was in variables and vanished when the page closed. A database keeps it.

**Analogy:** a **register book** in a college office. Each student has one page (a **document**). All pages together make the book (a **collection**).

| Excel / old style | MongoDB word |
|---|---|
| Table | Collection |
| Row | Document |
| Column | Field |

A document looks like a JavaScript object:

```json
{ "name": "Anu", "message": "Great class!" }
```

**Mongoose** is a Node.js package that lets us talk to MongoDB using JavaScript. We describe our data with a **schema** (the shape of one document) and make a **model** (the tool to save and read).

**MongoDB Atlas** is MongoDB running **free in the cloud**, so we do not need to install it. Setup:

1. Go to https://www.mongodb.com/atlas and sign up.
2. Create a free cluster.
3. Under *Database Access*, create a user (username and password).
4. Under *Network Access*, allow access from anywhere (`0.0.0.0/0`) for class use.
5. Click *Connect*, then *Drivers*, and copy the **connection string**. It looks like:

```
mongodb+srv://USER:PASSWORD@cluster0.xxxxx.mongodb.net/feedbackdb
```

Replace `USER` and `PASSWORD` with yours.

**Real world:** Many startups use MongoDB to store users, orders and posts.

### Check your understanding
1. What is a database? Why do we need one?
2. What are a collection and a document?
3. What is Mongoose for?

---

# 4. Building the Backend (Node.js, Express, MongoDB)

## 4.1 What is a REST API?

A **REST API** is a set of web addresses (URLs) our server offers so other programs (like React) can ask for or send data. The data travels as **JSON** (the object-like text format).

| Method | Meaning | Our address |
|---|---|---|
| GET | read data | `GET /api/feedback` |
| POST | send new data to save | `POST /api/feedback` |

**Status codes:** `200` OK, `201` created, `400` bad request (user's mistake), `500` server error.

**Analogy:** an API is the **menu** of a restaurant. It lists what you may ask for. You never go into the kitchen yourself.

## 4.2 Setting up the backend

```
mkdir feedback-server
cd feedback-server
npm init -y
npm install express mongoose cors dotenv
```

- `cors`: lets our React app (on another address) call this server. The browser blocks this by default, and `cors` allows it.
- `dotenv`: reads secret values from a `.env` file.

Create a file `.env` (never share this file):

```
MONGO_URI=mongodb+srv://USER:PASSWORD@cluster0.xxxxx.mongodb.net/feedbackdb
PORT=5000
```

## 4.3 The server code

```javascript
// server.js
require("dotenv").config();
const express = require("express");
const mongoose = require("mongoose");
const cors = require("cors");

const app = express();
app.use(cors());
app.use(express.json());      // lets Express read JSON sent by React

// connect to MongoDB
mongoose
  .connect(process.env.MONGO_URI)
  .then(() => console.log("MongoDB connected"))
  .catch((err) => console.log("MongoDB error:", err.message));

// schema and model
const Feedback = mongoose.model(
  "Feedback",
  new mongoose.Schema({
    name: { type: String, required: true },
    message: { type: String, required: true },
    createdAt: { type: Date, default: Date.now }
  })
);

// GET: send all feedback, newest first
app.get("/api/feedback", async (req, res) => {
  try {
    const list = await Feedback.find().sort({ createdAt: -1 });
    res.json(list);
  } catch (err) {
    res.status(500).json({ error: "Could not read feedback" });
  }
});

// POST: save one new feedback
app.post("/api/feedback", async (req, res) => {
  const { name, message } = req.body;
  if (!name || !message) {
    return res.status(400).json({ error: "Name and message are required" });
  }
  try {
    const saved = await Feedback.create({ name, message });
    res.status(201).json(saved);
  } catch (err) {
    res.status(500).json({ error: "Could not save feedback" });
  }
});

const PORT = process.env.PORT || 5000;
app.listen(PORT, () => console.log("Server running on port " + PORT));
```

Run it with `node server.js`. Open http://localhost:5000/api/feedback in the browser. You should see `[]` (an empty list).

**What is `async` / `await`?** Talking to a database takes time. `await` means "wait here for the answer". A function that uses `await` is marked `async`. The `try/catch` handles errors.

**Common mistakes:**
- Wrong password in the connection string.
- Forgetting to allow your address in Atlas *Network Access*.
- Forgetting `app.use(express.json())`, so `req.body` is empty.

### Check your understanding
1. What do GET and POST do in our API?
2. Why do we need `cors`?
3. What does status code `400` mean?

---

# 5. Connecting React to the Backend

Create the React app as in 1.2. Keep the backend running on port 5000.

## 5.1 Form component and handling input

We keep the form's input in state (as in 2.2):

```jsx
const [name, setName] = useState("");
const [message, setMessage] = useState("");
```

and connect each input with `value` and `onChange`.

## 5.2 Submitting data with `fetch()` or Axios

**`fetch()`** is built into the browser. **Axios** is a package that does the same job with less code.

**POST with fetch:**

```javascript
const response = await fetch("http://localhost:5000/api/feedback", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ name, message })
});
const data = await response.json();
```

**POST with Axios** (first run `npm install axios`):

```javascript
import axios from "axios";

const response = await axios.post("http://localhost:5000/api/feedback", { name, message });
console.log(response.data);
```

| | fetch | Axios |
|---|---|---|
| Install | built in | `npm install axios` |
| Send JSON | `JSON.stringify` + header needed | automatic |
| Read reply | `await response.json()` | `response.data` |
| HTTP errors (like 400) | does **not** throw an error | throws an error |

**Analogy:** `fetch` and Axios are the **postman**. The URL is the address, the method (GET or POST) is the type of delivery.

## 5.3 Receiving and displaying data (GET and POST)

**GET with fetch**, inside `useEffect` so it loads when the page opens:

```javascript
useEffect(() => {
  fetch("http://localhost:5000/api/feedback")
    .then((res) => res.json())
    .then((data) => setList(data));
}, []);
```

Then show the list with `.map()`, which makes one component for every item:

```jsx
{list.map((item) => (
  <FeedbackItem key={item._id} name={item.name} message={item.message} />
))}
```

`key` helps React tell items apart. MongoDB gives every document a unique `_id`, which we use as the key.

## 5.4 Conditional rendering, loading and error handling

**Conditional rendering** means showing different things depending on a condition.

**Analogy:** a bus board that shows "Loading...", "Bus arrived" or "Bus cancelled" depending on the situation.

We keep three states: `loading`, `error` and the data.

```jsx
if (loading) return <p>Loading...</p>;
if (error)   return <p style={{ color: "red" }}>{error}</p>;
return <ul>...show the data...</ul>;
```

Other ways to show things conditionally:

```jsx
{list.length === 0 && <p>No feedback yet.</p>}
{success ? <p>Thank you!</p> : null}
```

## 5.5 The complete React app

Replace `src/App.jsx` with this:

```jsx
import { useState, useEffect } from "react";

const API_URL = "http://localhost:5000";

function FeedbackItem({ name, message }) {
  return (
    <div style={{ border: "1px solid #ccc", borderRadius: "6px", margin: "8px 0", padding: "8px" }}>
      <b>{name}</b>
      <p style={{ margin: "4px 0 0" }}>{message}</p>
    </div>
  );
}

function App() {
  const [name, setName] = useState("");
  const [message, setMessage] = useState("");
  const [list, setList] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState("");
  const [success, setSuccess] = useState("");

  // load all feedback when the page opens
  useEffect(() => {
    fetch(API_URL + "/api/feedback")
      .then((res) => {
        if (!res.ok) throw new Error("Server error");
        return res.json();
      })
      .then((data) => {
        setList(data);
        setLoading(false);
      })
      .catch(() => {
        setError("Could not load feedback. Is the server running?");
        setLoading(false);
      });
  }, []);

  // send a new feedback
  async function handleSubmit(e) {
    e.preventDefault();
    setError("");
    setSuccess("");
    try {
      const res = await fetch(API_URL + "/api/feedback", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ name, message })
      });
      const data = await res.json();
      if (!res.ok) {
        setError(data.error || "Something went wrong");
        return;
      }
      setList([data, ...list]);      // add the new one at the top
      setName("");
      setMessage("");
      setSuccess("Thank you! Your feedback was saved.");
    } catch (err) {
      setError("Could not reach the server.");
    }
  }

  return (
    <div style={{ maxWidth: "480px", margin: "30px auto", fontFamily: "Arial" }}>
      <h2>Student Feedback</h2>

      <form onSubmit={handleSubmit}>
        <input
          value={name}
          onChange={(e) => setName(e.target.value)}
          placeholder="Your name"
          style={{ width: "100%", padding: "6px", marginBottom: "8px" }}
        />
        <textarea
          value={message}
          onChange={(e) => setMessage(e.target.value)}
          placeholder="Your message"
          style={{ width: "100%", padding: "6px", marginBottom: "8px" }}
        />
        <button type="submit">Send feedback</button>
      </form>

      {success && <p style={{ color: "green" }}>{success}</p>}
      {error && <p style={{ color: "red" }}>{error}</p>}

      <h3>All feedback</h3>
      {loading && <p>Loading...</p>}
      {!loading && list.length === 0 && !error && <p>No feedback yet.</p>}
      {list.map((item) => (
        <FeedbackItem key={item._id} name={item.name} message={item.message} />
      ))}
    </div>
  );
}

export default App;
```

Run both: backend with `node server.js` in one terminal, frontend with `npm run dev` in another. Add a feedback, refresh the page, and it is still there. That means it is saved in MongoDB.

**Test the error handling:** stop the backend and refresh. You should see the red error message.

**Common mistakes:**
- Backend not running (red error shown).
- Forgetting `cors` in the backend (browser console shows a "CORS" error).
- Forgetting `key` in a list (React warning in the console).
- Sending JSON with `fetch` but forgetting `JSON.stringify` and the `Content-Type` header.

### Check your understanding
1. Why is the GET request inside `useEffect` with `[]`?
2. How does the code show "Loading..." and an error?
3. What is the difference between `fetch` and Axios when the server replies with status `400`?
4. Why do we use `.map()` to show the list?

### Class activity (20 min)
Add a "Delete" button, or a character counter under the message box. Students pick one and try it.

---

# 6. Hosting the Frontend

Right now the app runs only on your laptop. **Hosting** puts it on the internet so anyone can open it.

**Steps:**

1. Build the production version:

```
npm run build
```

This creates a `dist` folder. It holds plain HTML, CSS and JS: the finished app.

2. Push the project to GitHub (see Section 9).
3. Go to https://vercel.com (or https://netlify.com) and sign in with GitHub.
4. Click **Add New Project** and pick your repository.
5. Vercel detects Vite automatically. Click **Deploy**.
6. After a minute you get a link like `https://feedback-app.vercel.app`.

Every time you push new code to GitHub, Vercel updates the site automatically.

**Analogy:** building the app is **packing it into a box**. Hosting is **placing the box in a shop** where customers can pick it up.

---

# 7. Deploying the Backend (Express + MongoDB)

The backend also needs to be online. We use **Render** (free for small apps). The database is already online in Atlas.

**Steps:**

1. Put the `feedback-server` folder on GitHub. Make sure `.env` and `node_modules` are in `.gitignore` (see Section 9) so secrets are **not** uploaded.
2. Check that `package.json` has a start script:

```json
"scripts": {
  "start": "node server.js"
}
```

3. Go to https://render.com and sign in with GitHub.
4. Click **New** > **Web Service** and pick the backend repository.
5. Fill in:
   - **Build command:** `npm install`
   - **Start command:** `npm start`
6. Under **Environment Variables**, add `MONGO_URI` with your Atlas connection string. (This is how the secret gets to the server without being in the code.)
7. Click **Create Web Service**. After a few minutes you get a link like `https://feedback-server.onrender.com`.
8. Test it: open `https://feedback-server.onrender.com/api/feedback`. You should see `[]` or your messages.

**Notes:**
- Free Render servers go to sleep when unused. The first request after a break can take about a minute.
- In Atlas *Network Access*, the address `0.0.0.0/0` must be allowed so Render can connect.

---

# 8. Connecting the Frontend to the Deployed Backend

Our React code has `http://localhost:5000` written in it. The online backend has a different address. We should not hard-code it. Use an **environment variable**.

**Step 1: change one line in `App.jsx`:**

```javascript
const API_URL = import.meta.env.VITE_API_URL || "http://localhost:5000";
```

On your laptop, `VITE_API_URL` is not set, so it uses `localhost:5000`. Online, we set it.

**Step 2: on Vercel**, open the project, go to **Settings > Environment Variables**, and add:

```
Name:  VITE_API_URL
Value: https://feedback-server.onrender.com
```

**Step 3: redeploy** the frontend (Deployments > Redeploy).

**Step 4: test.** Open your Vercel link, add a feedback, and refresh. It should be saved.

**Checklist if it doesn't work:**

| Problem | Likely fix |
|---|---|
| Red "Could not reach server" | Wrong `VITE_API_URL`, or Render still waking up |
| CORS error in console | `app.use(cors())` missing in backend |
| Backend log says MongoDB error | Wrong `MONGO_URI`, or Atlas Network Access not open |
| Works locally, not online | Env variables not set on Vercel / Render |

**Analogy:** the environment variable is like the **address on a delivery slip**. The parcel (the app) stays the same; only the address changes between your home and the shop.

### Check your understanding
1. Why don't we put the database password in the code?
2. What does `npm run build` produce?
3. Name the three online parts of our app and where each one lives.

---

# 9. Introduction to Git

## 9.1 What is Git?

**Git** is a tool that **saves versions of your project**, so you can go back, see what changed, and work with others. **GitHub** is a website that stores Git projects online.

**Analogy:** think of a video game's **save points**. You save before a hard level. If you fail, you load the save. Each Git **commit** is a save point.

**Real world:** almost every software team uses Git. Without it, people end up with files like `final`, `final2`, `final_new_REAL`.

**One-time setup:**

```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

## 9.2 The basic steps

```
  your files  --git add-->  staging area  --git commit-->  saved version  --git push-->  GitHub
```

**Analogy:** packing a parcel. `add` puts things in the box. `commit` seals the box and writes a label. `push` posts the box to GitHub.

| Command | What it does |
|---|---|
| `git init` | start tracking this folder |
| `git status` | show what changed |
| `git add .` | put all changes in the box |
| `git commit -m "message"` | save a version with a short message |
| `git push` | send saved versions to GitHub |
| `git pull` | bring new versions from GitHub to your computer |
| `git log --oneline` | list the saved versions |

## 9.3 Put a project on GitHub

First, create a file named `.gitignore` so secrets and big folders are **not** uploaded:

```
node_modules
.env
dist
```

Then:

```
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/YOUR-NAME/feedback-app.git
git push -u origin main
```

(First create an empty repository on github.com and copy its address.)

**Everyday work:**

```
git add .
git commit -m "add delete button"
git push
```

**Getting changes a friend made:**

```
git pull
```

## 9.4 Branching

A **branch** is a **separate line of work**. You can try a new idea without breaking the working version.

**Analogy:** you are writing an assignment. You copy it, try a new introduction in the copy, and if you like it, you merge it back. If not, you throw the copy away. The original is safe.

```
main:     A --- B --------------- E        (merge brings the feature back)
                 \               /
feature:          C ---- D ------
```

| Command | What it does |
|---|---|
| `git branch` | list branches |
| `git branch delete-button` | create a branch |
| `git checkout delete-button` | switch to it |
| `git checkout -b delete-button` | create and switch in one step |
| `git merge delete-button` | bring that branch into the one you are on |

**Example:**

```
git checkout -b delete-button      # new branch
# ...edit files...
git add .
git commit -m "add delete button"
git checkout main                  # go back to main
git merge delete-button            # bring the work in
git push
```

**Common mistakes:**
- Committing `.env` or `node_modules`. Use `.gitignore`.
- Forgetting `git add` before `git commit` (nothing gets saved).
- Writing the message `fix` or `abc`. Write what you did.
- Forgetting `git pull` before starting work, which causes clashes later.

### Check your understanding
1. What is the difference between `git add`, `git commit` and `git push`?
2. Why do we use branches?
3. What goes in `.gitignore` and why?
4. What does `git pull` do?

### Class activity (15 min)
In pairs: one student creates a repository and pushes a file. The other clones it (`git clone <address>`), adds a line, commits and pushes. The first student runs `git pull` and sees the change.

---

# 10. Exam Questions (short answers)

**Q1. What is `useEffect` in React? How is it different from `useState`? Give an example of `useEffect` fetching data from an API. (3 marks)**

`useState` stores a value that can change, and the page updates when it changes. `useEffect` runs code after the component appears, and is used for work like fetching data.

```jsx
const [users, setUsers] = useState([]);

useEffect(() => {
  fetch("https://jsonplaceholder.typicode.com/users")
    .then((res) => res.json())
    .then((data) => setUsers(data));
}, []);
```

**Q2. A React component that conditionally renders based on whether data was fetched, with error handling. (3 marks)**

```jsx
import { useState, useEffect } from "react";

function Users() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState("");

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((res) => {
        if (!res.ok) throw new Error("Failed");
        return res.json();
      })
      .then((data) => {
        setUsers(data);
        setLoading(false);
      })
      .catch(() => {
        setError("Could not load data");
        setLoading(false);
      });
  }, []);

  if (loading) return <p>Loading...</p>;
  if (error) return <p style={{ color: "red" }}>{error}</p>;
  return (
    <ul>
      {users.map((u) => (
        <li key={u.id}>{u.name}</li>
      ))}
    </ul>
  );
}

export default Users;
```

**Q3. Explain component-based architecture in React. How does it help build scalable and maintainable applications? (5 marks)**

Write: (1) a component is a small reusable function that returns JSX; (2) a page is built by putting components inside components (a tree); (3) props pass data in. Then the benefits: reuse, a bug fixed in one place, easy for teams to work on different components, easy to grow, and React updates only what changed. Use the LEGO or Swiggy card example.

**Q4. A React component that manages a form using `useState`. It accepts input and displays it on submission. (4 marks)**

See `NameForm` in section 2.2.

**Q5. Describe how React communicates with a backend using REST APIs. How would you handle form submission and data fetching? (5 marks)**

1. The backend (Express) offers URLs such as `GET /api/feedback` and `POST /api/feedback` and sends JSON.
2. React calls these URLs with `fetch()` or Axios.
3. Fetching data: call GET inside `useEffect` with `[]`, save the result in state, and show it with `.map()`.
4. Form submission: keep inputs in state, and on submit call `e.preventDefault()`, then POST the data as JSON, and update the state with the reply.
5. Show loading and error messages with conditional rendering.

Use the code in section 5.5.

**Q6. An Axios POST request to a backend API that shows a success message in the UI. (4 marks)**

```jsx
import { useState } from "react";
import axios from "axios";

function SendFeedback() {
  const [name, setName] = useState("");
  const [message, setMessage] = useState("");
  const [status, setStatus] = useState("");

  async function handleSubmit(e) {
    e.preventDefault();
    try {
      const response = await axios.post("http://localhost:5000/api/feedback", { name, message });
      setStatus("Success: feedback saved for " + response.data.name);
    } catch (error) {
      setStatus("Error: could not send feedback");
    }
  }

  return (
    <form onSubmit={handleSubmit}>
      <input value={name} onChange={(e) => setName(e.target.value)} placeholder="Name" />
      <input value={message} onChange={(e) => setMessage(e.target.value)} placeholder="Message" />
      <button type="submit">Send</button>
      <p>{status}</p>
    </form>
  );
}

export default SendFeedback;
```

**More practice:**

1. What is the difference between `fetch` and Axios? (3 marks)
2. What is Git? Explain commit, push, pull and branch. (5 marks)
3. What is conditional rendering? Give an example. (3 marks)
4. Explain the steps to deploy a React frontend and an Express backend. (6 marks)
5. What is an environment variable? Why is the database password kept in one? (3 marks)
