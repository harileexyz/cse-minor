# Module 4: React, Full-Stack Connection, Deployment and Git

**Course:** Web Application Development (MNCST509) | **Programme:** B.Tech CSE Minor, KTU, Semester 5
**Module 4 contact hours:** 11

---

## Table of Contents

1. Learning outcomes
2. Suggested lesson plan (11 hours)
3. The big picture: full-stack flow
4. Topic 1: Component-based architecture and React (components, JSX, props, Vite)
5. Topic 2: Forms and state with `useState` and `useEffect`
6. Topic 3: MongoDB and Mongoose (brief)
7. Topic 4: REST, JSON, HTTP methods, status codes, CORS
8. Topic 5: Form components and submitting data with `fetch()` / Axios
9. Topic 6: Receiving and displaying data (GET and POST)
10. Topic 7: Conditional rendering, loading and error handling
11. Topic 8: Hosting the React frontend (build, Vercel, Netlify)
12. Topic 9: Deploying the backend (Render, environment variables, Atlas)
13. Topic 10: Connecting the frontend to the deployed backend
14. Topic 11: Git and GitHub
15. Capstone mini-project: Event Registration and Feedback (MERN)
16. Question bank (KTU style)
17. Quick revision sheet

---

## 1. Learning outcomes

After this module, a student can:

- **LO1:** Explain component-based architecture and build a React app using components, JSX and props.
- **LO2:** Create a React project with Vite and run it.
- **LO3:** Build forms with controlled inputs using `useState`, and run side effects with `useEffect`.
- **LO4:** Explain MongoDB documents, collections, schemas and models, and use Mongoose with MongoDB Atlas.
- **LO5:** Build a REST API in Express and call it from React using `fetch()` or Axios (GET and POST).
- **LO6:** Show loading, error and success states using conditional rendering.
- **LO7:** Build a React app for production and host it on Vercel or Netlify.
- **LO8:** Deploy an Express + MongoDB backend on Render using environment variables and an Atlas connection string.
- **LO9:** Connect the deployed frontend and backend using `VITE_API_URL` and CORS.
- **LO10:** Use Git and GitHub for version control: init, add, commit, push, pull, clone, branch, merge, `.gitignore`.

---

## 2. Suggested lesson plan (11 contact hours)

| Session | Time | Topics | Activity |
|---|---|---|---|
| 1 | 1 h | Why React; component-based architecture; Vite setup; first component | Everyone creates a Vite project and edits `App.jsx` |
| 2 | 1 h | JSX rules, props, lists with `map`, keys | Build a "Swiggy restaurant card" list |
| 3 | 1 h | `useState`, events, controlled inputs, forms | Build a feedback form that shows input on submit |
| 4 | 1 h | `useEffect`: dependency array, cleanup | Live clock with cleanup; fetch data from a public API |
| 5 | 1 h | MongoDB, Mongoose, Atlas; REST, JSON, HTTP methods, status codes, CORS | Create Atlas cluster; test API in browser / Postman |
| 6 | 1 h | Express API (GET and POST) + submit form with `fetch` / Axios | Connect form to the backend |
| 7 | 1 h | Display data from API; conditional rendering; loading and error states | Add spinner and error message to the list |
| 8 | 1 h | `npm run build`; Vercel / Netlify; Render; env variables; Atlas string; `VITE_API_URL` | Deploy backend, then frontend |
| 9 | 1 h | Git basics: init, add, commit, push, pull, clone, `.gitignore` | Push project to GitHub |
| 10 | 1 h | Branching, merge, merge conflicts, GitHub workflow | Group exercise: create a conflict and fix it |
| 11 | 1 h | Capstone demo, doubt clearing, question bank practice | Pair demo + mock exam questions |

Tip for the teacher: keep Sessions 1 to 4 hands-on. Ask students to type the code, not copy it.

---

## 3. The big picture: full-stack flow

A **full-stack app** has three layers: what the user sees (frontend), the middle worker (backend), and the storage (database).

```text
 USER'S BROWSER                          YOUR SERVER (Render)               DATABASE (MongoDB Atlas)
+-------------------+   1. fetch()      +--------------------+  3. query   +----------------------+
|  React app        | ----------------> |  Express + Node.js | ----------> |  Collection:         |
|  (Vercel/Netlify) |   HTTP request    |  routes, cors,     |  Mongoose   |  registrations       |
|                   |   GET / POST      |  mongoose          |             |  { name, email ... } |
|  - components     |   JSON body       +--------------------+             +----------------------+
|  - useState       |                           |                                    |
|  - useEffect      |   2. server checks        |  4. data comes back                |
|                   |      the request          | <----------------------------------+
|                   |                           |
|                   | <-------------------------+
|                   |   5. HTTP response (status code + JSON)
|  6. setState()    |
|     React redraws |
|     the screen    |
+-------------------+
```

Reading the diagram in simple words:

1. The user clicks "Submit". React calls `fetch()` and sends a request.
2. Express receives it, checks it.
3. Express asks MongoDB (through Mongoose) to save or read data.
4. MongoDB returns the result.
5. Express sends back JSON with a status code (200, 201, 400, 500).
6. React saves the result in state, and the screen updates.

**Analogy:** A restaurant. The customer (React) tells the waiter (fetch) the order. The waiter goes to the kitchen manager (Express). The manager checks the store room (MongoDB) and the food comes back the same way.

---

## 4. Topic 1: Component-based architecture and React

Syllabus: *Introduction to component-based architecture using React (what React is, components, JSX, props, setting up with Vite).*

### 4.1 What is React?

- React is a **JavaScript library** for building user interfaces (UI). It was created by Facebook (now Meta) and released in 2013.
- You describe **what the screen should look like** for the current data. React updates the page when the data changes.
- It builds **Single Page Applications (SPA)**: the page loads once, then only the changed parts are redrawn. No full page reload.
- React uses a **Virtual DOM**: a light copy of the page in memory. React compares old and new copies and changes only the different parts in the real DOM. This is fast.

**Jargon note:** DOM (Document Object Model) means the tree of HTML elements the browser keeps in memory.

**Plain JS / jQuery vs React**

| jQuery style (imperative) | React style (declarative) |
|---|---|
| "Find this div, change its text, add this class" | "When count is 5, the screen looks like this" |
| You manage DOM changes by hand | React manages DOM changes |
| Becomes messy in big apps | Stays organised with components |

```js
// jQuery way: you tell the browser each step
$("#count").text(count);
$("#btn").addClass("active");
```

```jsx
// React way: you describe the result
<p className={active ? "active" : ""}>{count}</p>
```

### 4.2 Component-based architecture

A **component** is a small, reusable piece of UI that has its own look and logic. A full page is built by joining many components, like a tree.

```text
                 <App>
                   |
     +-------------+--------------+
     |             |              |
 <Navbar>     <EventList>     <Footer>
                   |
             +-----+------+
             |            |
        <EventCard>  <EventCard>
```

**Analogy:** LEGO blocks. A LEGO car is made from wheels, windows and a body. Each block is small, can be reused, and can be swapped. A React page is made from components in the same way. If one wheel is broken, you change only that wheel, not the whole car.

**Why it helps build scalable and maintainable apps**

1. **Reusability:** write `<Button />` once, use it 50 times.
2. **Separation of concerns:** each component does one job (the Navbar only handles the navigation).
3. **Easy maintenance:** a bug in the login form is fixed in `LoginForm.jsx` only.
4. **Team work:** different developers work on different components without clashing.
5. **Testability:** small parts can be tested alone.
6. **Scalability:** adding a feature means adding components, not rewriting the app.

**Real-world example:** On Instagram, a post is one `Post` component. It contains `Avatar`, `Image`, `LikeButton`, `CommentList`. The feed shows the same `Post` component hundreds of times with different data.

### 4.3 Setting up with Vite

**Vite** (French word for "fast", say "veet") is a tool that creates and runs a React project quickly. Older tool: Create React App (now outdated).

Requirements: Node.js installed (check with `node -v`).

```bash
# 1. Create a project
npm create vite@latest my-first-react -- --template react

# (or run "npm create vite@latest" and answer the questions:
#   Project name: my-first-react
#   Framework: React
#   Variant: JavaScript)

# 2. Go inside, install packages
cd my-first-react
npm install

# 3. Start the development server
npm run dev
# Open the URL shown, usually http://localhost:5173
```

Project folder (important parts):

```text
my-first-react/
  index.html          <- the only HTML page; has <div id="root"></div>
  package.json        <- list of packages and scripts
  vite.config.js      <- Vite settings
  public/             <- files served as they are (favicon, images)
  src/
    main.jsx          <- starting point: puts <App /> into #root
    App.jsx           <- main component
    App.css, index.css
    assets/
```

`src/main.jsx`:

```jsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import App from "./App.jsx";
import "./index.css";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

Scripts in `package.json`:

| Command | Meaning |
|---|---|
| `npm run dev` | Start the development server with hot reload |
| `npm run build` | Make the optimised production files in `dist/` |
| `npm run preview` | Test the production build locally |

### 4.4 JSX

**JSX** (JavaScript XML) is a way to write HTML-like code inside JavaScript. The browser does not understand it; Vite converts it to normal JavaScript calls.

```jsx
const name = "Anjali";
const element = <h1>Hello, {name}!</h1>;
```

JSX rules (students often forget these):

1. A component must return **one parent element**. Use a wrapper `<div>` or a fragment `<> ... </>`.
2. Use `className` instead of `class`, and `htmlFor` instead of `for`.
3. Close all tags: `<img />`, `<input />`, `<br />`.
4. Write JavaScript inside **curly braces** `{ }`.
5. Attributes are camelCase: `onClick`, `onChange`, `tabIndex`.
6. Styles are objects: `style={{ color: "red", fontSize: "20px" }}`.
7. Comments inside JSX: `{/* comment */}`.
8. Component names start with a **capital letter**: `<Card />`, not `<card />`.

```jsx
function Demo() {
  const price = 249;
  const isVeg = true;
  return (
    <>
      <h2 className="title">Paneer Butter Masala</h2>
      <p style={{ color: isVeg ? "green" : "red" }}>
        {isVeg ? "Veg" : "Non-veg"}
      </p>
      <p>Price: Rs. {price}</p>
      <p>With GST: Rs. {(price * 1.05).toFixed(2)}</p>
    </>
  );
}
```

**Analogy:** JSX is like a form template at the college office: fixed text, with blanks `{ }` that get filled with each student's real data.

### 4.5 Components (function components)

A component is a JavaScript function that returns JSX. We use only **function components** (modern React). Class components are old.

```jsx
// src/components/Welcome.jsx
function Welcome() {
  return <h2>Welcome to MNCST509</h2>;
}
export default Welcome;
```

```jsx
// src/App.jsx
import Welcome from "./components/Welcome.jsx";

function App() {
  return (
    <div>
      <Welcome />
      <Welcome />
    </div>
  );
}
export default App;
```

### 4.6 Props

**Props** (short for properties) are the inputs to a component. A parent passes data to a child through props. Props are **read-only**: the child must not change them.

**Analogy:** Props are like the order slip given to a cook. The cook (component) makes the dish using the slip (props). The cook does not rewrite the slip. Same cook, different slip, different dish.

### Complete example: Swiggy-style restaurant cards

```jsx
// src/components/RestaurantCard.jsx
function RestaurantCard({ name, cuisine, rating, deliveryTime, isOpen = true }) {
  return (
    <div style={{ border: "1px solid #ddd", borderRadius: 8, padding: 12, margin: 8, width: 240 }}>
      <h3>{name}</h3>
      <p>{cuisine}</p>
      <p>Rating: {rating} / 5</p>
      <p>{deliveryTime} min</p>
      <p style={{ color: isOpen ? "green" : "red" }}>{isOpen ? "Open" : "Closed"}</p>
    </div>
  );
}
export default RestaurantCard;
```

```jsx
// src/App.jsx
import RestaurantCard from "./components/RestaurantCard.jsx";

const restaurants = [
  { id: 1, name: "Kayees Biriyani", cuisine: "Biriyani", rating: 4.5, deliveryTime: 35 },
  { id: 2, name: "Sagar Restaurant", cuisine: "South Indian", rating: 4.2, deliveryTime: 25 },
  { id: 3, name: "Kerala Cafe", cuisine: "Kerala meals", rating: 4.0, deliveryTime: 40, isOpen: false },
];

function App() {
  return (
    <div>
      <h1>Restaurants near you</h1>
      <div style={{ display: "flex", flexWrap: "wrap" }}>
        {restaurants.map((r) => (
          <RestaurantCard
            key={r.id}
            name={r.name}
            cuisine={r.cuisine}
            rating={r.rating}
            deliveryTime={r.deliveryTime}
            isOpen={r.isOpen}
          />
        ))}
      </div>
    </div>
  );
}
export default App;
```

Points to explain:

- `{ name, cuisine, ... }` in the function parameter is **destructuring** of the props object.
- `isOpen = true` is a default value.
- `restaurants.map(...)` turns a list of data into a list of components.
- `key` helps React identify each item. Use a unique id, not the array index when the list can change.
- `children` prop: whatever you write between the tags.

```jsx
function Card({ title, children }) {
  return (
    <section>
      <h3>{title}</h3>
      {children}
    </section>
  );
}
// <Card title="Notice"><p>Exam on Monday</p></Card>
```

**Real-world example:** Facebook created React for its news feed. Instagram, Netflix (parts of its UI), Airbnb, Uber, WhatsApp Web and Flipkart-style shops use React. Netflix shows rows of movie cards: one `MovieCard` component, many data items.

**Common mistakes**

- Lowercase component name (`<card />` is treated as an HTML tag).
- Returning two sibling elements without a wrapper or fragment.
- Using `class` instead of `className`.
- Changing props inside the child (`props.name = "x"` does not work and is wrong).
- Forgetting `key` in a `.map()` list (React warning).
- Forgetting `export default` or the wrong import path.

**Check your understanding**

1. What is a component? Why is it compared to a LEGO block?
2. Write the JSX for a heading that shows your name using a variable.
3. What are props? Can a child change the props it receives?
4. Why does React need a `key` when we render a list?

**Classroom activity (10 min):** Make a `StudentCard` component with props `name`, `roll`, `branch`. Show 4 cards from an array of your friends' details.

---

## 5. Topic 2: Forms and state with `useState` and `useEffect`

Syllabus: *Creating forms and managing state using useState and useEffect (controlled inputs, dependency array, cleanup).*

### 5.1 State and `useState`

**State** is data that a component remembers, and when it changes, the screen updates. A normal variable is forgotten on each render and does not update the screen. State does.

**Hook:** a special React function (name starts with `use`) that lets function components use React features. `useState` and `useEffect` are hooks.

Syntax:

```jsx
const [value, setValue] = useState(initialValue);
```

- `value`: the current data.
- `setValue`: the function to change it. Calling it makes React redraw the component.
- `initialValue`: the starting value.

**Analogy:** The scoreboard at a cricket ground. The score is state. When a run is scored (`setScore`), the board updates and everyone sees the new number. If the operator only wrote the score on a paper in his pocket (a normal variable), the board would not change.

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Likes: {count}</p>
      <button onClick={() => setCount(count + 1)}>Like</button>
      <button onClick={() => setCount(0)}>Reset</button>
    </div>
  );
}
export default Counter;
```

Rules:

1. Never change state directly (`count = 5` is wrong). Always use the setter.
2. For objects and arrays, make a **new copy**: `setUser({ ...user, name: "Ravi" })`, `setItems([...items, newItem])`.
3. When the new value depends on the old value, use the function form: `setCount(prev => prev + 1)`.
4. Hooks must be called at the top level of a component, not inside `if` or loops.
5. State updates are not instant: the new value is seen in the next render.

### 5.2 Controlled inputs and forms

In a **controlled input**, React state is the single source of truth for the input's value. The input shows `value={state}` and updates the state in `onChange`.

**Analogy:** A college library register. Every entry is written in the register (state) first, and what you see is always read from the register. The register and the screen can never disagree.

### Complete example: form that accepts input and displays it on submission

```jsx
// src/components/FeedbackForm.jsx
import { useState } from "react";

function FeedbackForm() {
  const [form, setForm] = useState({ name: "", email: "", message: "" });
  const [submitted, setSubmitted] = useState(null);

  const handleChange = (e) => {
    const { name, value } = e.target;
    setForm({ ...form, [name]: value });   // update only the field that changed
  };

  const handleSubmit = (e) => {
    e.preventDefault();                    // stop the page from reloading
    setSubmitted(form);                    // save a copy to display
    setForm({ name: "", email: "", message: "" }); // clear the form
  };

  return (
    <div style={{ maxWidth: 360, margin: "20px auto" }}>
      <h2>Feedback</h2>
      <form onSubmit={handleSubmit}>
        <div>
          <label htmlFor="name">Name</label><br />
          <input id="name" name="name" value={form.name} onChange={handleChange} required />
        </div>
        <div>
          <label htmlFor="email">Email</label><br />
          <input id="email" name="email" type="email" value={form.email} onChange={handleChange} required />
        </div>
        <div>
          <label htmlFor="message">Message</label><br />
          <textarea id="message" name="message" rows="3" value={form.message} onChange={handleChange} />
        </div>
        <button type="submit">Submit</button>
      </form>

      {submitted && (
        <div style={{ marginTop: 16, background: "#eef", padding: 10 }}>
          <h3>You submitted:</h3>
          <p>Name: {submitted.name}</p>
          <p>Email: {submitted.email}</p>
          <p>Message: {submitted.message}</p>
        </div>
      )}
    </div>
  );
}
export default FeedbackForm;
```

Key points:

- `name` attribute on each input matches the key in the state object, so one `handleChange` serves all inputs.
- `[name]: value` is a **computed property name** in JavaScript.
- `e.preventDefault()` stops the browser's default reload on form submit.
- Checkbox uses `checked={state}` and `e.target.checked`. Select uses `value` like input.

```jsx
// Checkbox and select quick example
const [agree, setAgree] = useState(false);
const [dept, setDept] = useState("CSE");

<input type="checkbox" checked={agree} onChange={(e) => setAgree(e.target.checked)} />
<select value={dept} onChange={(e) => setDept(e.target.value)}>
  <option>CSE</option>
  <option>ECE</option>
  <option>EEE</option>
</select>
```

### 5.3 `useEffect`

A **side effect** is any work that happens outside the normal "calculate and return JSX" job of a component: fetching data, setting a timer, changing the page title, listening to events.

`useEffect` runs your code **after** React has drawn the screen.

```jsx
useEffect(() => {
  // effect code: runs after render
  return () => {
    // cleanup code (optional): runs before the next effect and when the component is removed
  };
}, [dependencies]);
```

**The dependency array** decides when the effect runs:

| Dependency array | When the effect runs |
|---|---|
| Not given: `useEffect(fn)` | After every render |
| Empty: `useEffect(fn, [])` | Only once, after the first render (on mount) |
| `[a, b]` | After first render, and whenever `a` or `b` changes |

**Cleanup function:** the function returned from the effect. It undoes the effect: clears timers, removes event listeners, cancels requests. It runs when the component is removed (unmount) and before the effect runs again. Without cleanup you get memory leaks and duplicate timers.

**Analogy:** A Zomato notification. When you open an order screen, you "subscribe" to delivery updates (effect). When you leave the screen, you "unsubscribe" (cleanup). If you never unsubscribe, the phone keeps getting updates for orders you no longer care about.

### Difference between `useState` and `useEffect`

| | `useState` | `useEffect` |
|---|---|---|
| Purpose | Store data that changes and affects the screen | Run side effects (fetch, timers, subscriptions) |
| Returns | `[value, setter]` | Nothing (optionally a cleanup function) |
| When it works | When you call the setter | After render, based on the dependency array |
| Triggers re-render? | Yes, when the setter is called | No by itself; it can call a setter which re-renders |
| Example | `const [count, setCount] = useState(0)` | `useEffect(() => { document.title = count }, [count])` |

They are often used together: `useEffect` fetches data, then `setData` (from `useState`) stores it, then the screen updates.

### Complete example 1: live clock with cleanup

```jsx
import { useState, useEffect } from "react";

function Clock() {
  const [time, setTime] = useState(new Date());

  useEffect(() => {
    const id = setInterval(() => setTime(new Date()), 1000);
    return () => clearInterval(id);   // cleanup: stop the timer when component goes away
  }, []);                              // [] = start once

  return <h3>{time.toLocaleTimeString()}</h3>;
}
export default Clock;
```

### Complete example 2: dependency array in action

```jsx
import { useState, useEffect } from "react";

function TitleUpdater() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState("");

  // runs only when count changes (not when name changes)
  useEffect(() => {
    document.title = `Clicked ${count} times`;
  }, [count]);

  return (
    <div>
      <button onClick={() => setCount(count + 1)}>Click ({count})</button>
      <input value={name} onChange={(e) => setName(e.target.value)} placeholder="type here" />
    </div>
  );
}
export default TitleUpdater;
```

### Complete example 3: useEffect fetching data from an API (exam question)

Uses the free public API `https://jsonplaceholder.typicode.com/users`.

```jsx
import { useState, useEffect } from "react";

function UserList() {
  const [users, setUsers] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    const controller = new AbortController();   // lets us cancel the request in cleanup

    async function loadUsers() {
      try {
        const res = await fetch("https://jsonplaceholder.typicode.com/users", {
          signal: controller.signal,
        });
        if (!res.ok) throw new Error(`Server error: ${res.status}`);
        const data = await res.json();
        setUsers(data);
      } catch (err) {
        if (err.name !== "AbortError") setError(err.message);
      } finally {
        if (!controller.signal.aborted) setLoading(false);
      }
    }

    loadUsers();
    return () => controller.abort();   // cleanup
  }, []);                              // run once on mount

  if (loading) return <p>Loading...</p>;
  if (error) return <p style={{ color: "red" }}>Error: {error}</p>;

  return (
    <ul>
      {users.map((u) => (
        <li key={u.id}>{u.name} ({u.email})</li>
      ))}
    </ul>
  );
}
export default UserList;
```

Why we write `async function` inside the effect: the effect callback itself must not be `async` (it must return nothing or a cleanup function, not a Promise).

**Note about StrictMode:** In development, React deliberately runs effects twice (mount, cleanup, mount) to help you find missing cleanups. You may see two network calls in `npm run dev`. This does not happen in production.

**Real-world example:** On Netflix, when the home page opens, an effect fetches the list of rows. When you search, an effect with `[searchText]` as dependency fetches new results each time the text changes. On Instagram, a chat screen subscribes to new messages and unsubscribes when you close it (cleanup).

**Common mistakes**

- Missing dependency array: the effect runs after every render, and with `setState` inside it causes an **infinite loop**.
- Forgetting a variable the effect uses in the dependency array: stale (old) values.
- Writing `useEffect(async () => ...)` directly.
- Forgetting cleanup for `setInterval` or event listeners.
- Mutating state directly: `form.name = "x"` (the screen will not update).
- Using `value` on an input without `onChange` (the field becomes read-only).
- Forgetting `e.preventDefault()` in a form submit.

**Check your understanding**

1. What is a controlled input? Why is `onChange` needed?
2. What is the difference between `useEffect(fn)`, `useEffect(fn, [])` and `useEffect(fn, [x])`?
3. What is a cleanup function? Give one example where it is required.
4. Differentiate `useState` and `useEffect` in four points.

**Classroom activity (15 min):** Build a "Search students" box: a list of 10 names in an array, an input, and show only names that contain the typed text (use `filter`). Then extend: use `useEffect` to change `document.title` to "Searching: <text>".

---

## 6. Topic 3: MongoDB and Mongoose (brief)

Syllabus: *brief MongoDB + Mongoose intro (documents, collections, schema, model, MongoDB Atlas).*

### 6.1 MongoDB basics

**MongoDB** is a **NoSQL database**. It stores data as flexible, JSON-like records instead of rows in tables.

| SQL (MySQL) | MongoDB |
|---|---|
| Database | Database |
| Table | **Collection** |
| Row | **Document** |
| Column | Field |
| Fixed structure | Flexible structure |

- **Document:** one record, stored in BSON (Binary JSON, a compact form of JSON). Every document has a unique `_id`.
- **Collection:** a group of documents, like a folder of forms.

**Analogy:** A college library. The whole library is the **database**. One shelf of "Computer Science books" is a **collection**. One single book is a **document**. In SQL, every book would have to fit the same strict card format. In MongoDB, one book can have extra details (like "CD included") without changing the rest.

A document:

```json
{
  "_id": "665f1c2e9a1b2c3d4e5f6a7b",
  "name": "Anjali Nair",
  "email": "anjali@example.com",
  "event": "Tech Fest 2026",
  "rating": 5,
  "skills": ["React", "Node"],
  "createdAt": "2026-10-01T10:30:00.000Z"
}
```

### 6.2 MongoDB Atlas

**MongoDB Atlas** is the free cloud service that hosts MongoDB for you. No installation needed, and your deployed server can reach it from anywhere.

Steps to set up (free "M0" tier):

1. Sign up at mongodb.com/atlas.
2. Create a **cluster** (choose free M0, region near India such as Mumbai).
3. **Database Access** > Add a database user (username + password). Remember them.
4. **Network Access** > Add IP address. For learning, "Allow access from anywhere" (`0.0.0.0/0`). Needed so Render can connect.
5. **Connect** > **Drivers** > copy the connection string:

```text
mongodb+srv://<username>:<password>@cluster0.abcde.mongodb.net/eventsdb?retryWrites=true&w=majority
```

Replace `<username>` and `<password>`. Put the **database name** (`eventsdb`) after the `/`. If the password has special characters like `@` or `#`, URL-encode them (`@` becomes `%40`).

### 6.3 Mongoose

**Mongoose** is a Node.js library (ODM: Object Data Modeling) that connects Express to MongoDB. MongoDB itself does not force any structure, so Mongoose adds structure and checks.

- **Schema:** the blueprint. It says which fields exist, their types, and rules (required, min, max, default).
- **Model:** a tool made from the schema. It gives you functions to create, read, update and delete documents (`find`, `create`, `findById`, `deleteOne` ...).

**Analogy:** A schema is the printed admission form (fields, which are compulsory). The model is the admission office clerk who accepts filled forms, files them, and finds them later.

Setup:

```bash
mkdir mongo-demo && cd mongo-demo
npm init -y
npm install mongoose dotenv
```

In `package.json` add `"type": "module"` to use `import` syntax.

`.env`

```text
MONGO_URI=mongodb+srv://myuser:mypassword@cluster0.abcde.mongodb.net/demo?retryWrites=true&w=majority
```

`demo.js`

```js
import "dotenv/config";
import mongoose from "mongoose";

// 1. Schema
const studentSchema = new mongoose.Schema(
  {
    name: { type: String, required: true, trim: true },
    email: { type: String, required: true, lowercase: true },
    age: { type: Number, min: 16, max: 60 },
    branch: { type: String, default: "CSE" },
  },
  { timestamps: true } // adds createdAt and updatedAt automatically
);

// 2. Model (collection name becomes "students")
const Student = mongoose.model("Student", studentSchema);

async function main() {
  await mongoose.connect(process.env.MONGO_URI);
  console.log("Connected to MongoDB");

  // Create
  const s = await Student.create({ name: "Ravi Kumar", email: "RAVI@mail.com", age: 20 });
  console.log("Saved:", s);

  // Read
  const all = await Student.find();
  console.log("All students:", all.length);

  const one = await Student.findOne({ name: "Ravi Kumar" });
  console.log("Found:", one.email);

  // Update
  await Student.updateOne({ _id: s._id }, { age: 21 });

  // Delete
  await Student.deleteOne({ _id: s._id });

  await mongoose.disconnect();
}

main().catch((err) => {
  console.error(err.message);
  process.exit(1);
});
```

Run with `node demo.js`.

Useful Mongoose methods:

| Method | Does |
|---|---|
| `Model.create(obj)` | Insert a document |
| `Model.find(filter)` | Get many; `find()` gets all |
| `Model.findById(id)` | Get one by id |
| `Model.findByIdAndUpdate(id, data, { new: true })` | Update and return new version |
| `Model.findByIdAndDelete(id)` | Delete |
| `.sort({ createdAt: -1 })` | Newest first |

**Real-world example:** Many startups, and companies like Uber, eBay and Forbes, use MongoDB. A food-delivery app stores each order as a document with a list of items inside it. A relational DB would need several tables for this.

**Common mistakes**

- Wrong password or special characters in the URI not encoded.
- Not adding IP `0.0.0.0/0` in Atlas Network Access (connection times out).
- Forgetting `await` on database calls.
- Forgetting the database name in the URI (data goes into a database called `test`).
- Committing the `.env` file with the real password to GitHub.

**Check your understanding**

1. Define document and collection. How do they compare to row and table?
2. What is the difference between a schema and a model?
3. What is MongoDB Atlas? Why do we need Network Access settings?

**Classroom activity (15 min):** Each student creates an Atlas free cluster, makes a user, and runs `demo.js` successfully. Check the data in Atlas "Browse Collections".

---

## 7. Topic 4: REST, JSON, HTTP methods, status codes, CORS

Syllabus: *Receiving and displaying data from REST API (GET and POST; explain REST, JSON, HTTP methods, status codes, CORS).*

### 7.1 API and REST

- **API** (Application Programming Interface): a set of rules for one program to talk to another. Our Express server exposes an API to the React app.
- **REST** (Representational State Transfer): a style for designing web APIs. Rules in simple words:
  1. Everything is a **resource** (students, events, orders) with a URL, like `/api/events`.
  2. Use **HTTP methods** to say what to do with it.
  3. The server is **stateless**: each request carries everything needed; the server does not remember you between requests.
  4. Data is exchanged usually as **JSON**.

**Analogy:** IRCTC. The menu of things you can ask the server is the API. `GET /trains` is "show me trains". `POST /bookings` is "book this ticket". Each request stands alone: you must show your login each time.

### 7.2 JSON

**JSON** (JavaScript Object Notation) is a light text format for data. Keys in double quotes, values can be string, number, boolean, null, array, object.

```json
{ "id": 1, "name": "Anjali", "passed": true, "marks": [78, 85, 90], "address": { "city": "Kochi" } }
```

- `JSON.stringify(obj)`: object to JSON text (for sending).
- `JSON.parse(text)`: JSON text to object (after receiving).
- Express: `res.json(obj)` sends JSON; `express.json()` middleware reads JSON from the request into `req.body`.
- In the browser: `res.json()` of `fetch` reads the response body as JSON.

### 7.3 HTTP methods

| Method | Meaning | CRUD | Example |
|---|---|---|---|
| **GET** | Read data | Read | `GET /api/events` (list events) |
| **POST** | Create new data (data in body) | Create | `POST /api/registrations` |
| **PUT** | Replace / update fully | Update | `PUT /api/registrations/12` |
| **PATCH** | Update part | Update | `PATCH /api/registrations/12` |
| **DELETE** | Remove | Delete | `DELETE /api/registrations/12` |

Parts of a request: **URL**, **method**, **headers** (e.g. `Content-Type: application/json`), **body** (for POST/PUT).
Parts of a response: **status code**, **headers**, **body**.

### 7.4 Status codes

| Range | Meaning | Common codes |
|---|---|---|
| 1xx | Information | rarely seen |
| 2xx | Success | **200 OK**, **201 Created** |
| 3xx | Redirect | 301, 304 |
| 4xx | Client mistake | **400 Bad Request**, **401 Unauthorized**, **403 Forbidden**, **404 Not Found** |
| 5xx | Server mistake | **500 Internal Server Error**, 503 |

Easy memory: 2xx = "all good", 4xx = "you made a mistake", 5xx = "we made a mistake".

**Analogy:** Swiggy order: 200/201 = "order placed"; 400 = "you forgot your address"; 404 = "restaurant not found"; 500 = "our kitchen's system crashed".

### 7.5 CORS

**Same-origin policy:** a browser rule that stops a web page from one **origin** reading data from a different origin. An origin = protocol + domain + port. `http://localhost:5173` (React) and `http://localhost:5000` (Express) are different origins because the ports differ.

**CORS** (Cross-Origin Resource Sharing): a way for the **server** to tell the browser "I allow requests from this other origin". The server sends the header `Access-Control-Allow-Origin`. In Express we use the `cors` package.

**Analogy:** A hostel gate. Normally the guard (browser) does not let visitors from outside the college in. If the warden (server) has put your name on the approved visitors list (CORS allow list), you can enter.

```js
import cors from "cors";

app.use(cors());                                        // allow all origins (OK for learning only)

app.use(cors({ origin: "http://localhost:5173" }));     // allow only the React dev server

app.use(cors({ origin: process.env.CLIENT_URL }));      // production: from env variable
```

The famous error:

```text
Access to fetch at 'http://localhost:5000/api/x' from origin 'http://localhost:5173'
has been blocked by CORS policy: No 'Access-Control-Allow-Origin' header is present.
```

Fix: add/configure `cors` **on the server**. CORS is a browser rule, so Postman and curl never show this error.

For POST requests with JSON, the browser first sends an automatic **preflight** request (method `OPTIONS`) asking "may I send this?". The `cors` package answers it for you.

### 7.6 A minimal REST API (Express)

```bash
mkdir api-demo && cd api-demo
npm init -y
npm install express cors
```

Add `"type": "module"` in `package.json`.

```js
// server.js
import express from "express";
import cors from "cors";

const app = express();
app.use(cors());
app.use(express.json());

let students = [
  { id: 1, name: "Anjali" },
  { id: 2, name: "Ravi" },
];

// GET all
app.get("/api/students", (req, res) => {
  res.status(200).json(students);
});

// GET one
app.get("/api/students/:id", (req, res) => {
  const s = students.find((x) => x.id === Number(req.params.id));
  if (!s) return res.status(404).json({ message: "Student not found" });
  res.json(s);
});

// POST create
app.post("/api/students", (req, res) => {
  const { name } = req.body;
  if (!name) return res.status(400).json({ message: "Name is required" });
  const student = { id: students.length + 1, name };
  students.push(student);
  res.status(201).json(student);
});

app.listen(5000, () => console.log("API on http://localhost:5000"));
```

Test: open `http://localhost:5000/api/students` in the browser.

**Real-world example:** When you open the Instagram app, it calls GET endpoints for the feed and POST endpoints when you like or comment. Weather widgets, UPI apps, and IRCTC's partner apps all talk to servers using REST and JSON.

**Common mistakes**

- Forgetting `app.use(express.json())`, so `req.body` is `undefined`.
- Using the wrong status code (sending 200 for an error).
- Trying to fix CORS in React. It must be fixed on the server.
- Not sending `Content-Type: application/json` header from the client.

**Check your understanding**

1. What is REST? List the HTTP methods and what each does.
2. What do 200, 201, 400, 404 and 500 mean?
3. What is CORS? Why does the error appear when React (5173) calls Express (5000)?
4. What is the difference between `JSON.stringify` and `JSON.parse`?

**Classroom activity (10 min):** Match game. Teacher shows 8 situations ("password wrong", "page not found", "new student saved", ...). Students shout the right status code.

---

## 8. Topic 5: Form components and submitting data with `fetch()` / Axios

Syllabus: *Creating form components and handling input; Submitting form data using fetch() or Axios.*

### 8.1 `fetch()`

`fetch(url, options)` is built into browsers. It returns a **Promise** (a value that will arrive later). Use `async/await` to wait for it.

Important: `fetch` does **not** throw an error for 400 or 500 responses. It only throws when the network fails. So always check `res.ok`.

```js
// GET
const res = await fetch("http://localhost:5000/api/students");
if (!res.ok) throw new Error("Request failed: " + res.status);
const data = await res.json();

// POST
const res2 = await fetch("http://localhost:5000/api/students", {
  method: "POST",
  headers: { "Content-Type": "application/json" },
  body: JSON.stringify({ name: "Meera" }),   // must be a string
});
const created = await res2.json();
```

### 8.2 Axios

**Axios** is a popular library that makes HTTP calls simpler.

```bash
npm install axios
```

Differences from fetch:

| | `fetch` | `axios` |
|---|---|---|
| Install | Built in | `npm install axios` |
| JSON body | `JSON.stringify` + header by hand | Pass an object; it is done for you |
| Read response | `await res.json()` | Already in `response.data` |
| HTTP errors (4xx, 5xx) | Does not throw; check `res.ok` | Throws automatically |
| Base URL | Write each time | `axios.create({ baseURL })` |

```js
import axios from "axios";

// GET
const { data } = await axios.get("http://localhost:5000/api/students");

// POST
const response = await axios.post("http://localhost:5000/api/students", { name: "Meera" });
console.log(response.status); // 201
console.log(response.data);   // created student
```

### Axios POST snippet that shows a success message (exam question)

```jsx
import { useState } from "react";
import axios from "axios";

function AddStudent() {
  const [name, setName] = useState("");
  const [message, setMessage] = useState("");

  const handleSubmit = async (e) => {
    e.preventDefault();
    setMessage("");
    try {
      const response = await axios.post("http://localhost:5000/api/students", { name });
      if (response.status === 201) {
        setMessage(`Success: ${response.data.name} was added!`);
        setName("");
      }
    } catch (error) {
      // Axios puts server replies for 4xx/5xx in error.response
      setMessage(error.response?.data?.message || "Something went wrong");
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <input value={name} onChange={(e) => setName(e.target.value)} placeholder="Student name" />
      <button type="submit">Add</button>
      {message && <p>{message}</p>}
    </form>
  );
}
export default AddStudent;
```

### Complete example: form submitting to the API with fetch

```jsx
import { useState } from "react";

const API = "http://localhost:5000";

function AddStudentFetch() {
  const [name, setName] = useState("");
  const [status, setStatus] = useState({ type: "", text: "" });
  const [submitting, setSubmitting] = useState(false);

  const handleSubmit = async (e) => {
    e.preventDefault();
    setSubmitting(true);
    setStatus({ type: "", text: "" });
    try {
      const res = await fetch(`${API}/api/students`, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ name }),
      });
      const data = await res.json();
      if (!res.ok) throw new Error(data.message || "Failed to save");
      setStatus({ type: "success", text: `Added ${data.name}` });
      setName("");
    } catch (err) {
      setStatus({ type: "error", text: err.message });
    } finally {
      setSubmitting(false);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <input value={name} onChange={(e) => setName(e.target.value)} />
      <button disabled={submitting}>{submitting ? "Saving..." : "Add"}</button>
      {status.text && (
        <p style={{ color: status.type === "success" ? "green" : "red" }}>{status.text}</p>
      )}
    </form>
  );
}
export default AddStudentFetch;
```

**Analogy:** Posting a letter. `fetch`/Axios is the postman. The URL is the address, the method is "speed post" or "ordinary", the body is the letter inside the envelope, and the response is the acknowledgement card that comes back.

**Real-world example:** When you tap "Place order" on Swiggy, the app sends a POST with your cart as JSON. Instagram's "Post comment" button does the same. Sign-up forms on every site do this.

**Common mistakes**

- Forgetting `JSON.stringify(body)` with fetch.
- Forgetting the `Content-Type` header (server receives an empty body).
- Not checking `res.ok` with fetch.
- Sending the request on every keystroke instead of on submit.
- Not disabling the button while submitting (double click makes two entries).

**Check your understanding**

1. Why must we call `JSON.stringify` when sending with `fetch` but not with Axios?
2. Does `fetch` throw for a 404 response? How do we detect it?
3. Write an Axios POST that sends `{ email }` and shows "Subscribed!" on success.

---

## 9. Topic 6: Receiving and displaying data (GET and POST)

### 9.1 The pattern

1. Create state for `items`.
2. In `useEffect` with `[]`, call `GET` and `setItems`.
3. Render with `items.map`.
4. After a POST, either refetch the list or add the new item into state.

**Analogy:** A notice board in college. When you arrive (page opens), you read all notices (GET). When a teacher pins a new notice (POST), the board must be refreshed so everyone sees it.

### Complete example: Student manager (React side) for the API from section 7.6

```jsx
// src/App.jsx
import { useState, useEffect } from "react";

const API = "http://localhost:5000";

function App() {
  const [students, setStudents] = useState([]);
  const [name, setName] = useState("");

  // GET on first load
  useEffect(() => {
    fetch(`${API}/api/students`)
      .then((res) => res.json())
      .then((data) => setStudents(data))
      .catch((err) => console.error(err));
  }, []);

  // POST on submit
  const addStudent = async (e) => {
    e.preventDefault();
    const res = await fetch(`${API}/api/students`, {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ name }),
    });
    if (res.ok) {
      const created = await res.json();
      setStudents([...students, created]);   // update screen without refetch
      setName("");
    }
  };

  return (
    <div style={{ maxWidth: 400, margin: "20px auto" }}>
      <h1>Students</h1>
      <form onSubmit={addStudent}>
        <input value={name} onChange={(e) => setName(e.target.value)} placeholder="Name" />
        <button type="submit">Add</button>
      </form>
      <ul>
        {students.map((s) => (
          <li key={s.id}>{s.name}</li>
        ))}
      </ul>
    </div>
  );
}
export default App;
```

Run: start the server (`node server.js`) in one terminal and React (`npm run dev`) in another. This is why you need **two terminals**.

Two ways to run `fetch` in `useEffect`: `.then()` chain (above) or `async` function inside (section 5.3). Both are fine.

**Real-world example:** Netflix's home screen is GET data rendered as rows of cards. Airbnb's search page calls GET `/listings?city=Goa&guests=2` and renders each result as a card.

**Common mistakes**

- Calling `fetch` directly in the component body (runs on every render, causes loops).
- Using the data before it arrives (`students.map` on `undefined`). Start state as `[]`.
- Forgetting to update the state after POST, so the screen looks unchanged.
- Hard-coding `localhost` in code that will be deployed (fix in Topic 10).

**Check your understanding**

1. Why do we put the GET call inside `useEffect` with `[]`?
2. After a successful POST, what are two ways to show the new item?
3. Why should the initial state of a list be `[]` and not `null`?

---

## 10. Topic 7: Conditional rendering and basic loading / error handling

Syllabus: *Conditional rendering and basic loading/error handling.*

**Conditional rendering** means showing different UI depending on a condition, using plain JavaScript.

**Analogy:** IRCTC seat availability. The same box shows "Available 45", "WL 12" or "Regret" depending on the data. Or the Swiggy order screen: "Finding delivery partner...", "Preparing", "On the way", "Delivered".

Ways to do it:

```jsx
// 1. if with early return
if (loading) return <p>Loading...</p>;

// 2. Ternary: either/or
{isLoggedIn ? <Dashboard /> : <Login />}

// 3. && : show or nothing
{error && <p className="error">{error}</p>}

// 4. A variable
let content;
if (items.length === 0) content = <p>No items</p>;
else content = <List items={items} />;
```

Warning: `{count && <p>..</p>}` shows `0` on screen when `count` is 0. Use `{count > 0 && ...}`.

### The three states of any data request

| State | Variable | Screen shows |
|---|---|---|
| Loading | `loading === true` | spinner / "Loading..." |
| Error | `error !== null` | friendly error message, maybe a Retry button |
| Success | data available | the data (or "No data yet" if empty) |

### Complete example: component that renders content based on fetch success (exam question)

```jsx
import { useState, useEffect } from "react";

function PostList() {
  const [posts, setPosts] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState("");

  const loadPosts = async () => {
    setLoading(true);
    setError("");
    try {
      const res = await fetch("https://jsonplaceholder.typicode.com/posts?_limit=5");
      if (!res.ok) {
        throw new Error(`Request failed with status ${res.status}`);
      }
      const data = await res.json();
      setPosts(data);
    } catch (err) {
      setError(err.message || "Could not load posts");
    } finally {
      setLoading(false);
    }
  };

  useEffect(() => {
    loadPosts();
  }, []);

  if (loading) {
    return <p>Loading posts...</p>;
  }

  if (error) {
    return (
      <div>
        <p style={{ color: "red" }}>Error: {error}</p>
        <button onClick={loadPosts}>Try again</button>
      </div>
    );
  }

  if (posts.length === 0) {
    return <p>No posts found.</p>;
  }

  return (
    <div>
      <h2>Latest posts</h2>
      <ul>
        {posts.map((p) => (
          <li key={p.id}>
            <strong>{p.title}</strong>
          </li>
        ))}
      </ul>
    </div>
  );
}
export default PostList;
```

How to test the error state: change the URL to a wrong one (`.../postz`) or switch off Wi-Fi in browser dev tools (Network tab > Offline).

**Real-world example:** YouTube shows grey skeleton boxes while videos load, an error "Something went wrong. Retry" if the network fails, and "No results" for an empty search. All three are conditional rendering.

**Common mistakes**

- Not setting `loading` back to `false` (use `finally`).
- Not clearing the old error before a retry.
- Showing raw technical errors to users (like "TypeError: undefined").
- Not handling the empty list case.
- `{count && ...}` printing `0`.

**Check your understanding**

1. Name three ways to do conditional rendering in JSX.
2. Why is the `finally` block useful in a data-loading function?
3. List the three states a data request can be in, and what UI each should show.

**Classroom activity (10 min):** Take the `PostList` code. Each group breaks it in a different way (wrong URL, offline, empty array) and shows the matching UI.

---

## 11. Topic 8: Hosting the React frontend (build, Vercel, Netlify)

Syllabus: *Hosting frontend React app (npm run build, Vercel/Netlify).*

### 11.1 What `npm run build` does

During development, Vite runs a dev server, and your code is not optimised. For the real world you create a **production build**: it combines all files, **minifies** (removes spaces, shortens names), and removes unused code.

```bash
npm run build
```

Output goes to the `dist/` folder:

```text
dist/
  index.html
  assets/
    index-a1b2c3d4.js     <- all your JS in one small file
    index-e5f6g7h8.css
```

A React app (SPA) after build is just **static files**: HTML, CSS, JS. Any static host can serve it. No Node server needed for the frontend.

Test locally: `npm run preview`.

**Analogy:** Cooking at home vs. packing a tiffin. The dev server is you cooking in your kitchen, with all the tools lying around. The build is the neatly packed tiffin box (small, ready to carry and serve anywhere).

### 11.2 Deploying on Vercel

1. Push your project to GitHub (see Topic 11).
2. Go to vercel.com and sign in with GitHub.
3. **Add New > Project**, pick your repository.
4. Settings (Vercel detects Vite):
   - Framework Preset: **Vite**
   - Build Command: `npm run build`
   - Output Directory: `dist`
   - Root Directory: the folder with the frontend (for example `frontend` if in a monorepo)
5. Add **Environment Variables** (for example `VITE_API_URL`), see Topic 10.
6. Click **Deploy**. You get a link like `https://my-app.vercel.app`.
7. Every `git push` to `main` redeploys automatically (continuous deployment).

### 11.3 Deploying on Netlify

Option A, from GitHub: **Add new site > Import from Git**, build command `npm run build`, publish directory `dist`.

Option B, drag and drop: run `npm run build`, then drag the `dist` folder to app.netlify.com/drop.

### 11.4 Fix for page refresh 404 on routes

If you use React Router and refresh on `/about`, the server looks for a file called `about` and gives 404. Tell the host to always serve `index.html`.

Netlify: file `public/_redirects` with:

```text
/*    /index.html   200
```

Vercel: file `vercel.json` in the project root:

```json
{
  "rewrites": [{ "source": "/(.*)", "destination": "/index.html" }]
}
```

(Our capstone has one page, so this is only for future apps.)

**Real-world example:** Static hosting with a CDN (Content Delivery Network, servers in many cities) is how big sites deliver the JS bundle fast to users anywhere. Many company landing pages and dashboards use Vercel or Netlify.

**Common mistakes**

- Deploying the `src` folder instead of `dist`.
- Wrong root directory (the build fails with "package.json not found").
- Using `localhost` URLs in the code (works on your laptop, fails for everyone else).
- Forgetting that env variables are baked into the code **during build**: after changing them, redeploy.
- Committing `node_modules`.

**Check your understanding**

1. What happens when we run `npm run build`? What is in `dist`?
2. Why can a React app be hosted without a Node server?
3. Name the build command and output directory for a Vite app on Vercel.

---

## 12. Topic 9: Deploying the backend (Express + MongoDB) on Render

Syllabus: *Deploying backend (Express + MongoDB) (Render, environment variables, MongoDB Atlas connection string).*

### 12.1 Environment variables

An **environment variable** is a setting kept **outside the code**: passwords, database URLs, ports, API keys. The code reads it with `process.env.NAME`.

Why:

1. **Security:** secrets are never pushed to GitHub.
2. **Flexibility:** the same code uses a local database on your laptop and Atlas on the server.

**Analogy:** The code is a house plan. The environment variables are the house keys. You share the plan freely, but never hand out keys.

Using dotenv:

```bash
npm install dotenv
```

`.env` (local file, **never** committed):

```text
PORT=5000
MONGO_URI=mongodb+srv://myuser:mypassword@cluster0.abcde.mongodb.net/eventsdb?retryWrites=true&w=majority
CLIENT_URL=http://localhost:5173
```

```js
import "dotenv/config";           // loads .env into process.env
const port = process.env.PORT || 5000;
```

Add `.env` to `.gitignore`. Provide a `.env.example` with fake values, so others know which variables are needed.

### 12.2 Getting the server ready for Render

Checklist:

1. `package.json` has `"type": "module"` and a start script:

```json
{
  "name": "event-api",
  "version": "1.0.0",
  "type": "module",
  "main": "server.js",
  "scripts": {
    "start": "node server.js",
    "dev": "node --watch server.js"
  }
}
```

2. Use `process.env.PORT` (Render gives its own port):

```js
const PORT = process.env.PORT || 5000;
```

3. Atlas Network Access allows `0.0.0.0/0`.
4. Code is on GitHub, `.env` and `node_modules` are not.

### 12.3 Deploy steps on Render

1. Sign up at render.com with GitHub.
2. **New > Web Service**, select your repository.
3. Fill:
   - Name: `event-api`
   - Root Directory: `backend` (if the repo has both folders)
   - Runtime: **Node**
   - Build Command: `npm install`
   - Start Command: `npm start`
   - Instance type: Free
4. Under **Environment Variables**, add `MONGO_URI` (the Atlas string) and `CLIENT_URL` (your frontend URL; you may put a temporary value first and update later).
5. Click **Create Web Service**. Watch the logs. When it says "Live", you get `https://event-api.onrender.com`.
6. Test by opening `https://event-api.onrender.com/api/registrations` in a browser.

Notes about the free plan: the service **sleeps** after about 15 minutes with no traffic. The next request can take 30 to 60 seconds to wake it. Tell students to open the backend link once before a demo.

**Real-world example:** Real companies keep database passwords in secret managers and environment variables. Several famous data leaks happened because someone pushed passwords or keys to a public GitHub repository.

**Common mistakes**

- Pushing `.env` to GitHub (rotate the password at once if this happens).
- Hard-coding the port 5000 (Render's port is different).
- Not allowing Render's IP in Atlas (error: "MongooseServerSelectionError").
- Adding the variables in `.env` only and not on Render's dashboard.
- Using `nodemon` as the start command (it is a dev tool).

**Check your understanding**

1. What is an environment variable? Why not write the DB password in the code?
2. Which values do we put on Render's dashboard for our backend?
3. Why does the first request to a free Render service take long?

---

## 13. Topic 10: Connecting the frontend to the deployed backend

Syllabus: *Connecting frontend to deployed backend (VITE_API_URL env var, CORS).*

### 13.1 `VITE_API_URL`

On your laptop, the backend is `http://localhost:5000`. After deployment, it is `https://event-api.onrender.com`. We should not change code each time. Use an environment variable.

Vite rules:

- Only variables that start with `VITE_` are available in the browser code.
- Read with `import.meta.env.VITE_API_URL` (not `process.env`).
- Variables are replaced at **build time**.
- Never put real secrets in `VITE_` variables: everyone can see them in the browser.

Files in the frontend folder:

`.env` (for local development)

```text
VITE_API_URL=http://localhost:5000
```

`.env.production` (optional, used by `npm run build`)

```text
VITE_API_URL=https://event-api.onrender.com
```

In code:

```js
// src/api.js
export const API_URL = import.meta.env.VITE_API_URL || "http://localhost:5000";
```

```jsx
import { API_URL } from "./api.js";

fetch(`${API_URL}/api/registrations`);
```

On Vercel or Netlify, set the variable in **Project Settings > Environment Variables**: `VITE_API_URL = https://event-api.onrender.com` (no slash at the end). Then **redeploy**.

### 13.2 Final CORS setup

After the frontend is live (say `https://event-app.vercel.app`):

1. On Render, set `CLIENT_URL=https://event-app.vercel.app` (no trailing slash).
2. Restart the service.
3. Server code uses it:

```js
app.use(cors({ origin: process.env.CLIENT_URL }));
```

To allow both local and live:

```js
const allowed = [process.env.CLIENT_URL, "http://localhost:5173"];
app.use(cors({ origin: allowed }));
```

### 13.3 Debug checklist when it does not work

1. Open browser **DevTools > Network** tab: what URL is called? What status?
2. Is the URL still `localhost`? Then the env variable was not set or you did not redeploy.
3. CORS error? Check `CLIENT_URL` (exact match, `https`, no trailing slash).
4. 500 error? Open Render **Logs**: usually Atlas connection problem.
5. Very slow first load? Render free plan is waking up.
6. `Mixed content` error? An `https` site cannot call an `http` backend. Use the `https` Render URL.

**Real-world example:** Companies keep separate "environments": development, staging, production, each with its own API URL set through variables. The same React code runs everywhere.

**Common mistakes**

- Naming it `API_URL` instead of `VITE_API_URL` (it will be `undefined`).
- Trailing slash in URL producing `//api/...`.
- Setting the variable after build, but not redeploying.
- CORS origin has a path or trailing slash.

**Check your understanding**

1. Why must the variable begin with `VITE_`?
2. Which side (frontend or backend) fixes a CORS error?
3. Why do we need to redeploy the frontend after changing `VITE_API_URL`?

---

## 14. Topic 11: Version control and Git

Syllabus: *Introduction to Git: what version control is, git init, add, commit, push, pull, clone, branching, merge, .gitignore, GitHub.*

### 14.1 What is version control?

A **version control system (VCS)** records every change made to your files over time. You can go back to an old version, see who changed what, and work with a team without overwriting each other.

**Analogy:** Think of the file names `report_final.docx`, `report_final_v2.docx`, `report_final_FINAL_really.docx`. Version control does this properly: one project, with a saved history of every change. Or like WhatsApp chat backup: you can restore older messages.

Benefits: history, backup, teamwork, experiments without risk (branches), and tracking bugs.

- **Git:** the version control tool on your own computer (free, by Linus Torvalds, 2005). It works offline.
- **GitHub:** a website that stores Git repositories online, with sharing, collaboration and pull requests. (Similar: GitLab, Bitbucket.) Git is the tool; GitHub is the cloud storage and social site.

### 14.2 Three areas of Git

```text
 Working folder        Staging area           Local repository          GitHub (remote)
 (your files)    --->  (ready to save)  --->  (saved history)    --->   (online copy)
        git add             git commit              git push
 <-------------------------------------------------------------------   git pull / git clone
```

**Analogy:** Sending a parcel. You put items on the table (working folder), choose what goes in the box (`git add` = staging), seal the box and write a label (`git commit` = message), and send it to the courier office (`git push`).

### 14.3 Setup (one time)

```bash
git --version
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

### 14.4 Core commands

| Command | Meaning |
|---|---|
| `git init` | Start tracking this folder (creates hidden `.git`) |
| `git status` | See which files are changed / staged |
| `git add file.js` | Stage one file |
| `git add .` | Stage all changes |
| `git commit -m "message"` | Save a snapshot with a message |
| `git log --oneline` | See the history |
| `git remote add origin <url>` | Link to the GitHub repository |
| `git push -u origin main` | Upload commits (first time with `-u`) |
| `git pull` | Download and merge new changes from GitHub |
| `git clone <url>` | Copy a whole GitHub repo to your computer |
| `git branch` | List branches |
| `git branch name` | Create a branch |
| `git switch name` | Move to a branch (`git switch -c name` creates and moves) |
| `git merge name` | Bring the branch's changes into the current branch |
| `git diff` | See exact changes |

### 14.5 Complete walkthrough

```bash
# --- A. Start a new project ---
mkdir event-app && cd event-app
git init
git branch -M main                     # name the main branch "main"

echo "# Event App" > README.md
git status                             # README.md is "untracked"
git add README.md                      # stage
git commit -m "Add README"             # save

# --- B. Put it on GitHub ---
# 1. On github.com click New repository (name: event-app). Do not add a README there.
# 2. Copy the repo URL, then:
git remote add origin https://github.com/YOUR-USERNAME/event-app.git
git push -u origin main

# --- C. Daily work ---
git add .
git commit -m "Add registration form"
git push

# --- D. Get a project from GitHub ---
git clone https://github.com/YOUR-USERNAME/event-app.git

# --- E. Get new changes made by a friend ---
git pull
```

Pushing to GitHub asks you to log in. Use a **Personal Access Token** instead of the password (GitHub > Settings > Developer settings > Tokens), or use GitHub Desktop / SSH keys.

Good commit messages: short and clear. "Add loading state to list" is good. "changes" or "asdf" is bad.

### 14.6 Branching and merging

A **branch** is a separate line of work. You can build a new feature on a branch without disturbing the stable `main` branch. When done, you **merge** it back.

**Analogy:** You are writing a project report. You make a copy of the file to try a new chapter. If the chapter is good, you paste it into the real report (merge). If not, you delete the copy and the report is untouched.

```text
main:      A---B---C-----------F   (F = merge commit)
                    \         /
feature:             D---E---+
```

```bash
git switch -c feature/feedback-form    # create and move to new branch
# ...edit files...
git add .
git commit -m "Add feedback form"

git switch main                         # go back to main
git merge feature/feedback-form         # bring the feature in
git branch -d feature/feedback-form     # delete the finished branch
git push
```

**Merge conflict:** happens when two branches change the **same line** of a file. Git cannot choose, so it marks the file:

```text
<<<<<<< HEAD
<h1>Event Registration</h1>
=======
<h1>Register for Tech Fest</h1>
>>>>>>> feature/title
```

Fix: open the file, keep the correct text, delete the three marker lines, then:

```bash
git add file.jsx
git commit -m "Resolve merge conflict in title"
```

### 14.7 `.gitignore`

A text file named `.gitignore` in the project root lists files and folders Git must **not** track. Reasons: huge folders (`node_modules`), generated files (`dist`), secrets (`.env`).

```text
# dependencies
node_modules/

# environment files with secrets
.env
.env.local
.env.production

# build output
dist/
build/

# logs and system files
*.log
.DS_Store
```

Important: `.gitignore` only works for files not yet tracked. If you already committed `.env`, run `git rm --cached .env`, commit, and change the password.

### 14.8 GitHub workflow (teams)

1. **Fork** or clone the repository.
2. Create a branch for your task.
3. Commit and push the branch.
4. Open a **Pull Request (PR)**: asks the team to review and merge your branch into `main`.
5. After approval, merge. Platforms like Vercel and Render redeploy automatically.

**Real-world example:** The Linux kernel (where Git started), React itself, VS Code and almost every company use Git. React is open source on GitHub, and thousands of people send pull requests. A developer's GitHub profile is also used as a portfolio in job hunting.

**Common mistakes**

- Running `git init` inside another repo, or in the wrong folder (such as the home folder).
- Forgetting `git add` before `git commit` (nothing to commit).
- Committing `node_modules` and `.env`.
- Pushing without pulling first (rejected push; run `git pull` first).
- Writing meaningless commit messages.
- Working directly on `main` in a team.

**Check your understanding**

1. What is version control? Difference between Git and GitHub?
2. Explain the sequence `git add`, `git commit`, `git push` with an analogy.
3. What is a merge conflict and how do you resolve it?
4. What is the use of `.gitignore`? Which three entries are a must in a MERN project?

**Classroom activity (20 min, pairs):**
1. Student A creates a repo, adds `index.html`, pushes.
2. Student B clones, creates a branch, edits the same line as A, pushes.
3. A edits the same line on `main` and merges B's branch. They face a conflict and solve it together.

---

## 15. Capstone mini-project: Event Registration and Feedback (MERN)

**Goal:** Students register for a college event with a rating and feedback comment. The page shows a list of all registrations.

**Features:** form (name, email, event, rating, feedback) > POST to API > saved in MongoDB > list refreshes > loading, error and empty states > deploy online.

### 15.1 Folder structure

```text
event-registration/
  .gitignore
  README.md
  backend/
    package.json
    server.js
    .env                 (not committed)
    .env.example
    models/
      Registration.js
    routes/
      registrations.js
  frontend/
    package.json         (created by Vite)
    index.html
    vite.config.js
    .env                 (not committed)
    .env.example
    src/
      main.jsx
      App.jsx
      api.js
      components/
        RegistrationForm.jsx
        RegistrationList.jsx
```

Root `.gitignore`:

```text
node_modules/
.env
.env.*
!.env.example
dist/
*.log
.DS_Store
```

### 15.2 Backend

Create it:

```bash
mkdir event-registration && cd event-registration
mkdir backend && cd backend
npm init -y
npm install express mongoose cors dotenv
```

`backend/package.json`

```json
{
  "name": "event-api",
  "version": "1.0.0",
  "type": "module",
  "main": "server.js",
  "scripts": {
    "start": "node server.js",
    "dev": "node --watch server.js"
  },
  "dependencies": {
    "cors": "^2.8.5",
    "dotenv": "^16.4.5",
    "express": "^4.19.2",
    "mongoose": "^8.4.0"
  }
}
```

(The version numbers can differ; `npm install` will pick the latest.)

`backend/.env`

```text
PORT=5000
MONGO_URI=mongodb+srv://myuser:mypassword@cluster0.abcde.mongodb.net/eventsdb?retryWrites=true&w=majority
CLIENT_URL=http://localhost:5173
```

`backend/.env.example` (safe to commit)

```text
PORT=5000
MONGO_URI=your-atlas-connection-string-here
CLIENT_URL=http://localhost:5173
```

`backend/models/Registration.js`

```js
import mongoose from "mongoose";

const registrationSchema = new mongoose.Schema(
  {
    name: {
      type: String,
      required: [true, "Name is required"],
      trim: true,
      minlength: [2, "Name must have at least 2 characters"],
    },
    email: {
      type: String,
      required: [true, "Email is required"],
      trim: true,
      lowercase: true,
      match: [/^\S+@\S+\.\S+$/, "Please enter a valid email"],
    },
    event: {
      type: String,
      required: [true, "Please choose an event"],
      enum: {
        values: ["Tech Fest", "Hackathon", "Cultural Night", "Workshop"],
        message: "{VALUE} is not a valid event",
      },
    },
    rating: {
      type: Number,
      min: [1, "Rating must be at least 1"],
      max: [5, "Rating must be at most 5"],
      default: 5,
    },
    feedback: {
      type: String,
      trim: true,
      maxlength: [300, "Feedback can be at most 300 characters"],
      default: "",
    },
  },
  { timestamps: true }
);

const Registration = mongoose.model("Registration", registrationSchema);
export default Registration;
```

`backend/routes/registrations.js`

```js
import express from "express";
import Registration from "../models/Registration.js";

const router = express.Router();

// GET /api/registrations  -> list all, newest first
router.get("/", async (req, res) => {
  try {
    const items = await Registration.find().sort({ createdAt: -1 });
    res.status(200).json(items);
  } catch (err) {
    console.error(err);
    res.status(500).json({ message: "Server error while fetching registrations" });
  }
});

// POST /api/registrations  -> create one
router.post("/", async (req, res) => {
  try {
    const { name, email, event, rating, feedback } = req.body;
    const created = await Registration.create({ name, email, event, rating, feedback });
    res.status(201).json(created);
  } catch (err) {
    // Mongoose validation errors -> 400
    if (err.name === "ValidationError") {
      const messages = Object.values(err.errors).map((e) => e.message);
      return res.status(400).json({ message: messages.join(", ") });
    }
    console.error(err);
    res.status(500).json({ message: "Server error while saving registration" });
  }
});

// DELETE /api/registrations/:id  -> optional extra
router.delete("/:id", async (req, res) => {
  try {
    const removed = await Registration.findByIdAndDelete(req.params.id);
    if (!removed) return res.status(404).json({ message: "Registration not found" });
    res.status(200).json({ message: "Deleted" });
  } catch (err) {
    // invalid ObjectId format -> CastError
    if (err.name === "CastError") return res.status(400).json({ message: "Invalid id" });
    res.status(500).json({ message: "Server error while deleting" });
  }
});

export default router;
```

`backend/server.js`

```js
import "dotenv/config";
import express from "express";
import cors from "cors";
import mongoose from "mongoose";
import registrationRoutes from "./routes/registrations.js";

const app = express();
const PORT = process.env.PORT || 5000;

// Allow the React app (local and deployed) to call this API
const allowedOrigins = [process.env.CLIENT_URL, "http://localhost:5173"].filter(Boolean);
app.use(cors({ origin: allowedOrigins }));

// Read JSON bodies
app.use(express.json());

// Health check (handy to test the deployment and wake up Render)
app.get("/", (req, res) => {
  res.json({ status: "ok", message: "Event Registration API is running" });
});

app.use("/api/registrations", registrationRoutes);

// Unknown route
app.use((req, res) => {
  res.status(404).json({ message: "Route not found" });
});

// Connect to the database first, then start listening
async function start() {
  try {
    if (!process.env.MONGO_URI) throw new Error("MONGO_URI is not set");
    await mongoose.connect(process.env.MONGO_URI);
    console.log("MongoDB connected");
    app.listen(PORT, () => console.log(`Server running on port ${PORT}`));
  } catch (err) {
    console.error("Failed to start server:", err.message);
    process.exit(1);
  }
}

start();
```

Test locally:

```bash
cd backend
npm run dev
# Browser: http://localhost:5000/            -> {"status":"ok",...}
# Browser: http://localhost:5000/api/registrations  -> []
```

Test the POST with curl (or Postman):

```bash
curl -X POST http://localhost:5000/api/registrations \
  -H "Content-Type: application/json" \
  -d '{"name":"Anjali","email":"anjali@mail.com","event":"Hackathon","rating":5,"feedback":"Great!"}'
```

### 15.3 Frontend

```bash
cd ..            # back to event-registration/
npm create vite@latest frontend -- --template react
cd frontend
npm install
```

`frontend/.env`

```text
VITE_API_URL=http://localhost:5000
```

`frontend/.env.example`

```text
VITE_API_URL=http://localhost:5000
```

`frontend/src/api.js`

```js
// Base URL of the backend. Comes from .env locally and from Vercel settings online.
export const API_URL = (import.meta.env.VITE_API_URL || "http://localhost:5000").replace(/\/$/, "");

// Small helper so every call checks errors the same way
async function request(path, options) {
  const res = await fetch(`${API_URL}${path}`, options);
  let data = null;
  try {
    data = await res.json();
  } catch {
    // response had no JSON body
  }
  if (!res.ok) {
    throw new Error((data && data.message) || `Request failed (${res.status})`);
  }
  return data;
}

export function getRegistrations() {
  return request("/api/registrations");
}

export function createRegistration(payload) {
  return request("/api/registrations", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(payload),
  });
}
```

`frontend/src/main.jsx` (the Vite default, with `index.css` import; keep as it is)

```jsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import "./index.css";
import App from "./App.jsx";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

`frontend/src/App.jsx`

```jsx
import { useState, useEffect, useCallback } from "react";
import RegistrationForm from "./components/RegistrationForm.jsx";
import RegistrationList from "./components/RegistrationList.jsx";
import { getRegistrations } from "./api.js";

function App() {
  const [registrations, setRegistrations] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState("");

  const loadRegistrations = useCallback(async () => {
    setLoading(true);
    setError("");
    try {
      const data = await getRegistrations();
      setRegistrations(data);
    } catch (err) {
      setError(err.message || "Could not load registrations");
    } finally {
      setLoading(false);
    }
  }, []);

  // Load the list once, when the page opens
  useEffect(() => {
    loadRegistrations();
  }, [loadRegistrations]);

  // Called by the form after a successful save: put the new item at the top
  const handleCreated = (newItem) => {
    setRegistrations((prev) => [newItem, ...prev]);
  };

  return (
    <div className="container">
      <h1>College Event Registration</h1>
      <p className="subtitle">Register for an event and tell us how it went.</p>

      <RegistrationForm onCreated={handleCreated} />

      <h2>Registered students ({registrations.length})</h2>
      <RegistrationList
        registrations={registrations}
        loading={loading}
        error={error}
        onRetry={loadRegistrations}
      />
    </div>
  );
}

export default App;
```

`frontend/src/components/RegistrationForm.jsx`

```jsx
import { useState } from "react";
import { createRegistration } from "../api.js";

const EVENTS = ["Tech Fest", "Hackathon", "Cultural Night", "Workshop"];
const emptyForm = { name: "", email: "", event: "", rating: 5, feedback: "" };

function RegistrationForm({ onCreated }) {
  const [form, setForm] = useState(emptyForm);
  const [submitting, setSubmitting] = useState(false);
  const [message, setMessage] = useState({ type: "", text: "" });

  const handleChange = (e) => {
    const { name, value } = e.target;
    setForm((prev) => ({ ...prev, [name]: value }));
  };

  const handleSubmit = async (e) => {
    e.preventDefault();
    setMessage({ type: "", text: "" });

    // simple check before calling the server
    if (!form.name.trim() || !form.email.trim() || !form.event) {
      setMessage({ type: "error", text: "Please fill name, email and event." });
      return;
    }

    setSubmitting(true);
    try {
      const created = await createRegistration({
        ...form,
        rating: Number(form.rating),
      });
      onCreated(created);
      setForm(emptyForm);
      setMessage({ type: "success", text: "Thank you! Your registration was saved." });
    } catch (err) {
      setMessage({ type: "error", text: err.message });
    } finally {
      setSubmitting(false);
    }
  };

  return (
    <form className="card" onSubmit={handleSubmit}>
      <label htmlFor="name">Name</label>
      <input id="name" name="name" value={form.name} onChange={handleChange} placeholder="Your full name" />

      <label htmlFor="email">Email</label>
      <input id="email" name="email" type="email" value={form.email} onChange={handleChange} placeholder="you@college.edu" />

      <label htmlFor="event">Event</label>
      <select id="event" name="event" value={form.event} onChange={handleChange}>
        <option value="">-- choose an event --</option>
        {EVENTS.map((ev) => (
          <option key={ev} value={ev}>{ev}</option>
        ))}
      </select>

      <label htmlFor="rating">Rating (1 to 5)</label>
      <select id="rating" name="rating" value={form.rating} onChange={handleChange}>
        {[1, 2, 3, 4, 5].map((n) => (
          <option key={n} value={n}>{n}</option>
        ))}
      </select>

      <label htmlFor="feedback">Feedback</label>
      <textarea
        id="feedback"
        name="feedback"
        rows="3"
        maxLength={300}
        value={form.feedback}
        onChange={handleChange}
        placeholder="What did you like?"
      />

      <button type="submit" disabled={submitting}>
        {submitting ? "Submitting..." : "Register"}
      </button>

      {message.text && (
        <p className={message.type === "success" ? "msg success" : "msg error"}>{message.text}</p>
      )}
    </form>
  );
}

export default RegistrationForm;
```

`frontend/src/components/RegistrationList.jsx`

```jsx
function RegistrationList({ registrations, loading, error, onRetry }) {
  if (loading) {
    return <p>Loading registrations... (the free server may take up to a minute to wake up)</p>;
  }

  if (error) {
    return (
      <div className="msg error">
        <p>Error: {error}</p>
        <button onClick={onRetry}>Try again</button>
      </div>
    );
  }

  if (registrations.length === 0) {
    return <p>No registrations yet. Be the first!</p>;
  }

  return (
    <ul className="list">
      {registrations.map((r) => (
        <li key={r._id} className="card">
          <strong>{r.name}</strong> registered for <em>{r.event}</em>
          <div>Rating: {"★".repeat(r.rating)}{"☆".repeat(5 - r.rating)}</div>
          {r.feedback && <p>"{r.feedback}"</p>}
          <small>{new Date(r.createdAt).toLocaleString("en-IN")}</small>
        </li>
      ))}
    </ul>
  );
}

export default RegistrationList;
```

`frontend/src/index.css` (replace the default, simple styling)

```css
body {
  font-family: system-ui, Arial, sans-serif;
  background: #f4f6fb;
  margin: 0;
  color: #222;
}
.container { max-width: 560px; margin: 0 auto; padding: 20px; }
.subtitle { color: #555; margin-top: -8px; }
.card {
  background: #fff;
  border: 1px solid #dde;
  border-radius: 8px;
  padding: 14px;
  margin-bottom: 12px;
  display: flex;
  flex-direction: column;
  gap: 6px;
}
input, select, textarea { padding: 8px; border: 1px solid #bbb; border-radius: 6px; font: inherit; }
button { padding: 10px; background: #4f46e5; color: #fff; border: 0; border-radius: 6px; cursor: pointer; }
button:disabled { opacity: 0.6; cursor: not-allowed; }
.list { list-style: none; padding: 0; }
.msg { padding: 8px; border-radius: 6px; }
.msg.success { background: #e6f7ec; color: #176b3a; }
.msg.error { background: #fdecec; color: #a11; }
```

Run both locally (two terminals):

```bash
# Terminal 1
cd event-registration/backend && npm run dev

# Terminal 2
cd event-registration/frontend && npm run dev
# open http://localhost:5173
```

Things to test: submit an empty form (message shown), submit valid data (appears in list), stop the backend (list shows error and Retry works after you restart), check Atlas "Browse Collections".

### 15.4 Push to GitHub

From the `event-registration` root folder:

```bash
git init
git branch -M main
# create the root .gitignore (shown in 15.1) before the next line
git add .
git status                       # check: .env and node_modules must NOT be listed
git commit -m "Initial commit: MERN event registration app"

# create an empty repo on github.com named event-registration, then:
git remote add origin https://github.com/YOUR-USERNAME/event-registration.git
git push -u origin main
```

Add a feature on a branch (practice):

```bash
git switch -c feature/delete-button
# ...make changes...
git add .
git commit -m "Add delete button for registrations"
git push -u origin feature/delete-button
# open a Pull Request on GitHub, review, merge
git switch main
git pull
```

### 15.5 Deployment, step by step

**Step 1: MongoDB Atlas (database)**

1. Create a free M0 cluster.
2. Database Access: create user (for example `eventuser`) with a password without special characters.
3. Network Access: add `0.0.0.0/0`.
4. Copy the connection string, put your user, password and the database name `eventsdb`.
5. Test locally by running the backend: you should see "MongoDB connected".

**Step 2: Backend on Render**

1. Render > New > Web Service > connect GitHub repo `event-registration`.
2. Root Directory `backend`, Build `npm install`, Start `npm start`, Free instance.
3. Environment variables:
   - `MONGO_URI` = Atlas string
   - `CLIENT_URL` = `http://localhost:5173` for now
4. Deploy. Copy the URL, for example `https://event-api.onrender.com`.
5. Open `https://event-api.onrender.com/` (should show the status JSON) and `/api/registrations` (should show `[]`).

**Step 3: Frontend on Vercel**

1. Vercel > Add New > Project > import the same repo.
2. Root Directory `frontend`. Framework: Vite. Build `npm run build`, Output `dist`.
3. Environment variable: `VITE_API_URL` = `https://event-api.onrender.com`
4. Deploy. Copy the URL, for example `https://event-registration.vercel.app`.

**Step 4: Connect them (CORS)**

1. On Render, edit `CLIENT_URL` to `https://event-registration.vercel.app` (no trailing slash).
2. Save. Render restarts the service.
3. Open the Vercel URL. First load may take up to a minute (free server waking up). Submit a registration and refresh to see it is saved.

**Step 5: Update later**

Make code change, then:

```bash
git add .
git commit -m "Improve form validation message"
git push
```

Render and Vercel both redeploy automatically.

**Final checklist (students tick each):**

- [ ] `.env` files are not in GitHub
- [ ] Atlas user and network access set
- [ ] Backend URL opens and shows JSON
- [ ] `VITE_API_URL` set on Vercel, redeployed
- [ ] `CLIENT_URL` set on Render to the exact Vercel URL
- [ ] Form submits from the live site and the data appears in Atlas
- [ ] At least 5 commits and 1 merged branch in the GitHub history

**Extension ideas:** delete button, filter by event, average rating, edit, login with JWT, pagination.

---

## 16. Question bank (KTU style)

### Part A: 3 marks each (answer all, ten questions)

1. What is JSX? Write one rule of JSX.
2. Define a component in React. Give a small example.
3. What are props? How are they different from state?
4. What is a controlled input in React?
5. What is the use of the dependency array in `useEffect`?
6. What is a document and a collection in MongoDB?
7. What is CORS? Why is it needed?
8. Write the use of `npm run build` in a Vite project.
9. What is an environment variable? Give an example used in a Node app.
10. What is the use of `.gitignore`? Give two entries.

**Model answers (Part A, key points for 3 marks)**

1. JSX (JavaScript XML) is a syntax that allows writing HTML-like markup inside JavaScript. Vite/Babel converts it into `React.createElement` calls. Rule: a component must return a single parent element (or fragment `<>...</>`); also `class` is written `className`. (1 + 1 + 1)
2. A component is a reusable, independent piece of UI written as a JavaScript function that returns JSX. Example:
```jsx
function Hello({ name }) { return <h1>Hello {name}</h1>; }
```
3. Props are inputs passed from parent to child; they are read-only. State is data owned and changed inside a component using `useState`; changing it re-renders. Props come from outside, state lives inside.
4. An input whose value is controlled by React state: `value={x}` and `onChange={e => setX(e.target.value)}`. React state is the single source of truth.
5. It tells React when to run the effect: `[]` runs once after mount; `[a]` runs when `a` changes; no array runs after every render.
6. A document is a single record in JSON/BSON form with an `_id`. A collection is a group of documents, similar to a table. 
7. CORS (Cross-Origin Resource Sharing) lets a server permit browser requests from a different origin through the header `Access-Control-Allow-Origin`. It is needed because browsers block cross-origin reads by default (same-origin policy), e.g. React on port 5173 calling Express on port 5000.
8. It creates an optimised production build (minified, bundled HTML/CSS/JS) in the `dist` folder, which can be hosted on static hosts such as Vercel or Netlify.
9. A value kept outside the code (secret or setting) and read through `process.env`. Example: `MONGO_URI`, stored in a `.env` file.
10. It lists files Git must not track. Examples: `node_modules/`, `.env`.

### Part B: 9 marks each (answer any 6 out of 8; here six main questions with sub-parts)

**Q11.** (a) What is `useEffect`? How is it different from `useState`? (4 marks)
(b) Write a React component that uses `useEffect` to fetch data from an API and display it. (5 marks)

**Q12.** (a) Write a simple React component that conditionally renders content depending on whether data was fetched successfully, with basic error handling. (6 marks)
(b) Explain the three states of a data request in a UI. (3 marks)

**Q13.** (a) Explain component-based architecture in React. (4 marks)
(b) How does it help in building scalable and maintainable applications? Illustrate with an example. (5 marks)

**Q14.** (a) Write a React component that manages a form using `useState`, accepts user input and displays it on submission. (6 marks)
(b) What is a controlled component? What is the role of `e.preventDefault()`? (3 marks)

**Q15.** (a) Describe how React communicates with a backend using REST APIs. (4 marks)
(b) Explain how form submission and data fetching are handled, with code. (5 marks)

**Q16.** (a) Write an Axios POST request snippet that sends form data and shows a success message using the response. (5 marks)
(b) Compare `fetch()` and Axios. (4 marks)

**Additional Part B questions for practice**

**Q17.** (a) Explain the steps to deploy a MERN app: MongoDB Atlas, Render and Vercel. (6 marks)
(b) What is `VITE_API_URL` and why is it needed? (3 marks)

**Q18.** (a) Explain Git workflow with the commands init, add, commit, push, pull and clone. (5 marks)
(b) What is a branch? Explain how branches are merged and how a conflict is solved. (4 marks)

### Model answers for the key exam questions

#### Answer to Q11: `useEffect`, `useState`, and fetching data

**(a)** `useEffect` is a React hook used to perform **side effects** in function components, that is, work done outside rendering such as fetching data, timers, subscriptions and changing the document title. It runs after the component renders. Syntax: `useEffect(callback, dependencyArray)`. The callback may return a **cleanup** function that runs before the next effect and on unmount. (2 marks)

Difference (2 marks):

| `useState` | `useEffect` |
|---|---|
| Creates and stores state data | Runs side-effect code |
| Returns `[value, setValue]` | Returns nothing / cleanup function |
| Updating with the setter causes re-render | Runs after render depending on the dependency array |
| Example: `const [n, setN] = useState(0)` | Example: `useEffect(() => {...}, [])` |

**(b)** (5 marks: states 1, effect with fetch 2, loading/error 1, rendering list 1)

```jsx
import { useState, useEffect } from "react";

function UserList() {
  const [users, setUsers] = useState([]);       // state to hold data
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function loadUsers() {
      try {
        const res = await fetch("https://jsonplaceholder.typicode.com/users");
        if (!res.ok) throw new Error("HTTP error " + res.status);
        setUsers(await res.json());
      } catch (err) {
        setError(err.message);
      } finally {
        setLoading(false);
      }
    }
    loadUsers();
  }, []);   // empty array: run only once after first render

  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error: {error}</p>;
  return (
    <ul>
      {users.map((u) => <li key={u.id}>{u.name}</li>)}
    </ul>
  );
}
export default UserList;
```

Explanation: on first render `users` is empty and `loading` is true. After render, the effect fetches data; `setUsers` stores it, `setLoading(false)` hides the loader, React re-renders and shows the list.

#### Answer to Q12: conditional rendering with error handling

**(a)** (6 marks)

```jsx
import { useState, useEffect } from "react";

function Products() {
  const [products, setProducts] = useState([]);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState("");

  useEffect(() => {
    fetch("https://fakestoreapi.com/products?limit=5")
      .then((res) => {
        if (!res.ok) throw new Error("Failed with status " + res.status);
        return res.json();
      })
      .then((data) => setProducts(data))
      .catch((err) => setError(err.message))
      .finally(() => setLoading(false));
  }, []);

  if (loading) return <p>Loading products...</p>;           // case 1
  if (error) return <p style={{ color: "red" }}>{error}</p>; // case 2
  if (products.length === 0) return <p>No products found.</p>; // case 3

  return (                                                    // case 4: success
    <ul>
      {products.map((p) => (
        <li key={p.id}>{p.title} - Rs. {p.price}</li>
      ))}
    </ul>
  );
}
export default Products;
```

**(b)** Loading: request is in progress, show a spinner/text. Error: request failed (network or non-2xx status), show a friendly message and optionally a Retry button. Success: show the data, or an "empty" message if the list has no items. Handling all three prevents a blank screen or a crash.

#### Answer to Q13: component-based architecture

**(a)** In React, the UI is divided into small, independent, reusable pieces called **components**. Each component is a function that takes input (props), may keep its own data (state), and returns JSX describing its part of the screen. Components are put together like a tree: the `App` component contains `Header`, `Content` and `Footer`, and these contain smaller components. Data flows **one way, from parent to child through props**. (4 marks)

```text
        App
       /   \
  Navbar   Feed
             |
           Post (reused many times)
           /  \
     LikeButton  CommentBox
```

**(b)** (5 marks) Advantages:

1. **Reusability:** one `Button` or `Card` used in many places; less code.
2. **Maintainability:** a change or bug fix is made in one file and applies everywhere.
3. **Separation of concerns:** each component has one job, so code is easy to read.
4. **Scalability:** new features are added as new components without rewriting old ones.
5. **Parallel teamwork:** developers work on separate components.
6. **Easy testing:** small units are tested independently.
7. **Performance:** React re-renders only components whose data changed.

Example: On Instagram, `Post` is written once and used for every post in the feed. If Instagram wants to add a "Share" button, it changes only the `Post` component and every post gets it.

#### Answer to Q14: form with `useState` showing input on submission

**(a)** (6 marks)

```jsx
import { useState } from "react";

function SimpleForm() {
  const [name, setName] = useState("");
  const [city, setCity] = useState("");
  const [submittedData, setSubmittedData] = useState(null);

  const handleSubmit = (e) => {
    e.preventDefault();                       // prevent page reload
    setSubmittedData({ name, city });         // keep the submitted values
    setName("");
    setCity("");
  };

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <input
          type="text"
          placeholder="Name"
          value={name}
          onChange={(e) => setName(e.target.value)}
        />
        <input
          type="text"
          placeholder="City"
          value={city}
          onChange={(e) => setCity(e.target.value)}
        />
        <button type="submit">Submit</button>
      </form>

      {submittedData && (
        <p>
          Hello {submittedData.name} from {submittedData.city}!
        </p>
      )}
    </div>
  );
}
export default SimpleForm;
```

**(b)** A controlled component is a form element whose value is held in React state and updated through `onChange`, so React controls what the input shows. `e.preventDefault()` stops the browser's default form behaviour (reloading the page), so React can handle the data in JavaScript.

#### Answer to Q15: how React talks to the backend using REST

**(a)** (4 marks) React runs in the browser and cannot access the database directly. It sends **HTTP requests** to a backend (for example Node/Express) that exposes **REST API** endpoints such as `GET /api/items` and `POST /api/items`. The backend validates the request, reads or writes the database (MongoDB through Mongoose), and sends back a **response** with a status code (200, 201, 400, 404, 500) and JSON data. React reads the JSON, stores it in state, and re-renders the UI. The browser requires the server to allow the React app's origin using **CORS**. Calls are made with `fetch()` or Axios, usually inside `useEffect` (for GET) or an event handler (for POST).

Flow:

```text
React component -> fetch/axios -> HTTP request (JSON) -> Express route -> Mongoose -> MongoDB
React state <- JSON response (status code) <- Express <- result <- MongoDB
```

**(b)** (5 marks)

```jsx
import { useState, useEffect } from "react";

function Notes() {
  const [notes, setNotes] = useState([]);
  const [text, setText] = useState("");
  const [error, setError] = useState("");

  // Data fetching: GET on page load
  useEffect(() => {
    fetch("http://localhost:5000/api/notes")
      .then((res) => {
        if (!res.ok) throw new Error("Could not load notes");
        return res.json();
      })
      .then(setNotes)
      .catch((err) => setError(err.message));
  }, []);

  // Form submission: POST
  const handleSubmit = async (e) => {
    e.preventDefault();
    try {
      const res = await fetch("http://localhost:5000/api/notes", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ text }),
      });
      if (!res.ok) throw new Error("Could not save note");
      const saved = await res.json();
      setNotes((prev) => [...prev, saved]);   // update UI
      setText("");
    } catch (err) {
      setError(err.message);
    }
  };

  return (
    <div>
      <form onSubmit={handleSubmit}>
        <input value={text} onChange={(e) => setText(e.target.value)} />
        <button type="submit">Add</button>
      </form>
      {error && <p style={{ color: "red" }}>{error}</p>}
      <ul>{notes.map((n) => <li key={n._id}>{n.text}</li>)}</ul>
    </div>
  );
}
export default Notes;
```

Matching Express handlers (for completeness):

```js
app.get("/api/notes", async (req, res) => res.json(await Note.find()));
app.post("/api/notes", async (req, res) => {
  const note = await Note.create({ text: req.body.text });
  res.status(201).json(note);
});
```

#### Answer to Q16: Axios POST with success message

**(a)** (5 marks)

```jsx
import { useState } from "react";
import axios from "axios";

function Subscribe() {
  const [email, setEmail] = useState("");
  const [successMsg, setSuccessMsg] = useState("");
  const [errorMsg, setErrorMsg] = useState("");

  const handleSubmit = async (e) => {
    e.preventDefault();
    setSuccessMsg("");
    setErrorMsg("");
    try {
      const response = await axios.post("http://localhost:5000/api/subscribe", { email });
      // response.status is 200/201, response.data is the JSON body
      setSuccessMsg(response.data.message || "Subscribed successfully!");
      setEmail("");
    } catch (error) {
      setErrorMsg(error.response?.data?.message || "Network or server error");
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <input type="email" value={email} onChange={(e) => setEmail(e.target.value)} required />
      <button type="submit">Subscribe</button>
      {successMsg && <p style={{ color: "green" }}>{successMsg}</p>}
      {errorMsg && <p style={{ color: "red" }}>{errorMsg}</p>}
    </form>
  );
}
export default Subscribe;
```

**(b)** Comparison (4 marks): use the table in Topic 5 (install, JSON body handling, `response.data`, automatic error throwing for 4xx/5xx, base URL and interceptors in Axios; `fetch` is built in and needs `res.ok` and `res.json()`).

#### Answer hints for Q17 and Q18

**Q17 (a)** Steps: (1) Create Atlas free cluster, add DB user, allow network access, copy connection string. (2) Push code to GitHub with `.env` ignored. (3) On Render create a Web Service from the repo, set build `npm install`, start `npm start`, add `MONGO_URI` and `CLIENT_URL`; deploy and get the backend URL. (4) On Vercel import the repo, root `frontend`, build `npm run build`, output `dist`, add `VITE_API_URL` with the Render URL; deploy. (5) Update `CLIENT_URL` on Render with the Vercel URL so CORS allows it. (6) Test and check logs. 
**(b)** `VITE_API_URL` is the environment variable holding the backend address. Read in code as `import.meta.env.VITE_API_URL`. It lets the same code use `http://localhost:5000` in development and the Render URL in production, without editing code. Only variables starting with `VITE_` are exposed to the browser.

**Q18 (a)** `git init` creates a repo; `git add` stages changes; `git commit -m` saves a snapshot to local history; `git push` uploads commits to GitHub; `git pull` downloads and merges remote changes; `git clone` copies a remote repo to the local machine. Draw the four-area diagram from section 14.2.
**(b)** A branch is an independent line of development (`git switch -c feature`). `git switch main` then `git merge feature` brings changes in. If both branches changed the same lines, a conflict occurs; Git inserts markers (`<<<<<<<`, `=======`, `>>>>>>>`); edit the file to keep the right content, remove the markers, `git add` the file and `git commit`.

### More short practice questions (for self-study)

1. What is the Virtual DOM? How does it make React fast?
2. Why is `key` needed in lists?
3. What happens if `useEffect` has no dependency array and calls `setState`?
4. Differentiate between SQL and MongoDB terms.
5. Write the Mongoose schema for a `Book` (title, author, price, inStock).
6. List four HTTP status codes and their meanings.
7. Why does a free Render backend respond slowly the first time?
8. What is the difference between `git pull` and `git clone`?
9. Why should `.env` never be pushed to GitHub?
10. What is the difference between `npm run dev` and `npm run build`?

---

## 17. Quick revision sheet

```text
REACT
  Component     = function returning JSX, name starts with capital letter
  Props         = input from parent, read-only
  useState      = [value, setValue], setter triggers re-render
  useEffect     = side effects; [] once, [x] on change of x, return cleanup
  Controlled    = value={state} + onChange
  Conditional   = if / ternary / &&  ->  loading, error, empty, success

BACKEND
  express.json()  -> read JSON body       cors() -> allow other origin
  mongoose: Schema -> Model -> create / find / findByIdAndDelete
  Status: 200 OK, 201 Created, 400 Bad request, 404 Not found, 500 Server error

CONNECT
  fetch(url, { method, headers: {"Content-Type":"application/json"}, body: JSON.stringify(x) })
  fetch needs res.ok check; axios throws on 4xx/5xx; data is in response.data

DEPLOY
  npm run build -> dist/ -> Vercel / Netlify
  Render: build "npm install", start "npm start", env: MONGO_URI, CLIENT_URL
  Vercel: env VITE_API_URL=https://your-api.onrender.com  (redeploy after change)
  Atlas: DB user + Network Access 0.0.0.0/0 + connection string

GIT
  init -> add -> commit -> remote add origin -> push
  clone, pull, switch -c, merge, .gitignore (node_modules, .env, dist)
```

**Teacher's closing note:** Ask each student to submit two links for the capstone: the GitHub repository and the live Vercel URL. Ask them to also explain, in their own words, one request going from the form to the database and back, using the diagram in Section 3.
