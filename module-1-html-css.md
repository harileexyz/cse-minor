# Module 1: Introduction to HTML and CSS

**Course:** Web Application Development (MNCST509)
**Programme:** B.Tech CSE Minor, KTU, Semester 5
**Module:** 1 of the syllabus (11 contact hours)

This module is written for students who have **never made a web page**. Teach one idea at a time, run the example in the browser, then let students change it.

**How to run every example:** open a text editor (VS Code or Notepad), save the code as `something.html`, and double-click the file to open it in Chrome. After changing the code, save and press `F5` to refresh.

---

## Contents

**Part A: HTML5**
1. Structuring and editing an HTML5 document
2. Headings
3. Hyperlinks
4. Images
5. Special characters and horizontal rules
6. Lists
7. Tables
8. Forms
9. Internal linking
10. Meta elements
11. HTML5 form input types
12. Input and datalist elements, and the autocomplete attribute
13. Page structure elements

**Part B: CSS**
14. Introduction to CSS and basic syntax
15. Inline styles, embedded style sheets, linking external style sheets
16. Conflict resolution
17. Selectors
18. Properties and values
19. Backgrounds
20. List styles
21. Element dimensions
22. Box model and text flow
23. `div` and `span`
24. Positioning: relative and absolute
25. Table layouts
26. Basics of responsive CSS: viewport and media queries

**Part C:** Mini-project and exam questions

## Suggested lesson plan

| Class | Topics |
|---|---|
| 1 | Document structure, headings, hyperlinks, images, special characters, horizontal rules |
| 2 | Lists, tables |
| 3 | Forms and input types |
| 4 | Datalist, autocomplete, internal linking, meta elements, page structure elements |
| 5 | Introduction to CSS, three ways to add CSS, conflict resolution |
| 6 | Selectors, properties and values, backgrounds |
| 7 | List styles, dimensions, box model, text flow |
| 8 | `div` and `span`, positioning, table layouts |
| 9 | Responsive CSS, viewport, media queries |
| 10 | Mini-project |
| 11 | Revision and exam questions |

**The big idea for students:**

```
HTML  = the skeleton and the content   (what is on the page)
CSS   = the clothes and the make-up    (how it looks)
```

**Analogy:** a house. HTML is the walls, doors and windows. CSS is the paint, curtains and furniture.

---

# PART A: HTML5

## 1. Structuring and Editing an HTML5 Document

**HTML** (HyperText Markup Language) describes the content of a web page using **tags**. Most tags come in pairs: an opening tag and a closing tag.

```
<p>Hello</p>
 ^    ^    ^
open content close
```

The tag name plus its content is called an **element**. Some tags have **attributes** that give extra information, written as `name="value"`:

```html
<a href="https://www.google.com">Go to Google</a>
```

**Every HTML5 page has this skeleton:**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>My First Page</title>
</head>
<body>
  <h1>Hello, world!</h1>
  <p>This is my first web page.</p>
</body>
</html>
```

| Part | Meaning |
|---|---|
| `<!DOCTYPE html>` | Tells the browser "this is an HTML5 page" |
| `<html>` | The root. Everything is inside it |
| `<head>` | Information **about** the page (title, settings). Not shown on the page |
| `<title>` | Text shown on the browser tab |
| `<body>` | Everything the visitor **sees** |

**Analogy:** a student's file. The cover (head) has the name and subject. The pages inside (body) have the actual content.

**Comments** (ignored by the browser, notes for you): `<!-- this is a comment -->`

**Real world:** every website you open, such as the college website or IRCTC, is HTML underneath. Right-click any page and choose *View page source* to see it.

**Common mistakes:**
- Forgetting the closing tag.
- Saving the file as `page.html.txt` (turn on file extensions to check).
- Forgetting to save before refreshing.

### Check your understanding
1. What is the difference between `<head>` and `<body>`?
2. What is an attribute? Give one example.

## 2. Headings

HTML has six heading sizes, `<h1>` (biggest, most important) to `<h6>` (smallest).

```html
<h1>College Fest 2026</h1>
<h2>Events</h2>
<h3>Technical events</h3>
<p>A paragraph is written with the p tag.</p>
<br>   <!-- a line break -->
```

Use one `<h1>` per page, as the main title. Use headings for meaning, not just to make text big.

**Analogy:** a newspaper. Big headline (h1), section titles (h2), smaller sub-titles (h3).

## 3. Hyperlinks

The `<a>` (anchor) tag makes a link. The `href` attribute holds the address.

```html
<a href="https://www.ktu.edu.in">KTU website</a>              <!-- another website -->
<a href="about.html">About us</a>                              <!-- another page of ours -->
<a href="https://www.google.com" target="_blank">Open in a new tab</a>
<a href="mailto:principal@college.edu">Email the principal</a>
```

**Analogy:** a link is a **door** from one room to another. `href` is the address on the door.

**Real world:** every "Click here", menu item and "Buy now" button on Flipkart is a link.

## 4. Images

```html
<img src="logo.png" alt="College logo" width="200">
```

| Attribute | Meaning |
|---|---|
| `src` | Where the image file is |
| `alt` | Text shown if the picture fails to load. Also read aloud for blind users |
| `width`, `height` | Size in pixels |

`<img>` has no closing tag. Keep the image in the same folder as the HTML file, or write the folder: `src="images/logo.png"`.

An image can also be a link:

```html
<a href="https://www.ktu.edu.in"><img src="logo.png" alt="KTU"></a>
```

**Common mistake:** wrong file name or wrong folder in `src`, so the picture does not show. Check capital and small letters.

## 5. Special Characters and Horizontal Rules

Some symbols have a special meaning in HTML, or are not on the keyboard. We write them as **character entities**, starting with `&` and ending with `;`.

| Write | Shows | Meaning |
|---|---|---|
| `&lt;` | `<` | less than |
| `&gt;` | `>` | greater than |
| `&amp;` | `&` | ampersand |
| `&copy;` | © | copyright |
| `&nbsp;` | (space) | a space that doesn't collapse |
| `&#8377;` | ₹ | rupee sign |

```html
<p>Price: &#8377;250</p>
<p>&copy; 2026 My College</p>
<p>To make a paragraph, write &lt;p&gt;.</p>
```

**Horizontal rule:** `<hr>` draws a line across the page to separate sections.

```html
<h2>Section one</h2>
<hr>
<h2>Section two</h2>
```

### Check your understanding
1. How do you show the text `<h1>` on a page without it becoming a heading?
2. What does `<hr>` do?

## 6. Lists

**Unordered list** (bullets) and **ordered list** (numbers). Each item is an `<li>`.

```html
<h3>Shopping</h3>
<ul>
  <li>Tea</li>
  <li>Sugar</li>
  <li>Milk</li>
</ul>

<h3>Steps to make tea</h3>
<ol>
  <li>Boil water</li>
  <li>Add tea leaves</li>
  <li>Add milk and sugar</li>
</ol>
```

**Nested list** (a list inside a list item):

```html
<ul>
  <li>Fruits
    <ul>
      <li>Mango</li>
      <li>Banana</li>
    </ul>
  </li>
  <li>Vegetables</li>
</ul>
```

**Definition list** (terms and meanings):

```html
<dl>
  <dt>HTML</dt><dd>Language for page content</dd>
  <dt>CSS</dt><dd>Language for page style</dd>
</dl>
```

**Real world:** menus on websites are almost always `<ul>` lists, styled with CSS.

## 7. Tables

A table is made of rows (`<tr>`), header cells (`<th>`) and data cells (`<td>`).

```html
<table border="1">
  <caption>Exam Timetable</caption>
  <tr>
    <th>Date</th>
    <th>Subject</th>
    <th>Time</th>
  </tr>
  <tr>
    <td>10 Nov</td>
    <td>Web Development</td>
    <td>10 AM</td>
  </tr>
  <tr>
    <td>12 Nov</td>
    <td>Databases</td>
    <td>10 AM</td>
  </tr>
</table>
```

Joining cells: `colspan="2"` makes a cell stretch over two columns, `rowspan="2"` over two rows.

```html
<tr><td colspan="3">Lunch break</td></tr>
```

**Analogy:** a class timetable on the notice board.

**Real world:** results pages, bus timetables, price lists.

**Common mistake:** using a table to arrange the whole page layout. Tables are for **data** only. Use CSS for layout.

### Check your understanding
1. Write a table with 2 columns (Name, Marks) and 2 students.
2. What is the difference between `<th>` and `<td>`?
3. What does `colspan` do?

## 8. Forms

A **form** collects information from the user: login, registration, search, feedback.

```html
<form action="/register" method="post">
  <label for="name">Name:</label>
  <input type="text" id="name" name="name">
  <br><br>
  <label for="pw">Password:</label>
  <input type="password" id="pw" name="password">
  <br><br>
  <input type="submit" value="Register">
</form>
```

| Part | Meaning |
|---|---|
| `<form>` | The box around all fields |
| `action` | Where the data is sent (a server address) |
| `method` | `get` (shown in the address bar, for searches) or `post` (hidden, for passwords and saving) |
| `<label>` | The text next to a field. `for` matches the field's `id`, so clicking the label selects the field |
| `<input>` | A field. `type` decides which kind |
| `name` | The name under which the data is sent |

More form items:

```html
<!-- radio buttons: pick one (same name) -->
<input type="radio" name="gender" value="male"> Male
<input type="radio" name="gender" value="female"> Female

<!-- checkboxes: pick many -->
<input type="checkbox" name="hobby" value="music"> Music
<input type="checkbox" name="hobby" value="sports"> Sports

<!-- dropdown -->
<select name="dept">
  <option value="cse">CSE</option>
  <option value="ece">ECE</option>
</select>

<!-- big text box -->
<textarea name="comments" rows="4" cols="30"></textarea>

<!-- buttons -->
<button type="submit">Send</button>
```

**Analogy:** a paper admission form. Each blank line is an input. Submitting is handing it to the office.

**Real world:** every login page, IRCTC ticket booking, and Google search box is a form.

## 9. Internal Linking

**Internal linking** means linking to a **place on the same page**. Useful for long pages ("Jump to Fees").

Step 1: give the target an `id`. Step 2: link to it with `#id`.

```html
<a href="#fees">Go to Fees</a>

<h2>Admissions</h2>
<p>...long text...</p>

<h2 id="fees">Fees</h2>
<p>Fee details here.</p>

<a href="#top">Back to top</a>
```

You can also link to a place on another page: `<a href="courses.html#cse">CSE course</a>`.

**Analogy:** the index of a book. "Chapter 5: page 40" takes you straight there.

**Real world:** Wikipedia's contents box, and "Back to top" arrows.

## 10. Meta Elements

`<meta>` tags go in `<head>` and give information **about** the page. They are not shown.

```html
<head>
  <meta charset="UTF-8">
  <meta name="description" content="Official page of the college tech fest">
  <meta name="keywords" content="college, fest, tech, events">
  <meta name="author" content="Anu">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tech Fest</title>
</head>
```

| Meta tag | Use |
|---|---|
| `charset` | Which letters and symbols the page may use (UTF-8 supports all languages) |
| `description` | The short text Google may show under your link |
| `keywords` | Words about the page |
| `author` | Who wrote it |
| `viewport` | Makes the page fit on mobile screens (used again in Section 26) |

**Analogy:** the label on a book's spine. You don't read it as content, but it tells people about the book.

### Check your understanding
1. How do you link to a heading lower on the same page?
2. Name three meta tags and say what they do.

## 11. HTML5 Form Input Types

HTML5 added new input types. The browser then gives **free checking** and the right keyboard on phones.

```html
<form>
  Name: <input type="text" name="name"><br><br>
  Email: <input type="email" name="email"><br><br>
  Password: <input type="password" name="pw"><br><br>
  Age: <input type="number" name="age" min="17" max="30"><br><br>
  Date of birth: <input type="date" name="dob"><br><br>
  Mobile: <input type="tel" name="mobile"><br><br>
  Website: <input type="url" name="site"><br><br>
  Favourite colour: <input type="color" name="colour"><br><br>
  Rating: <input type="range" name="rating" min="1" max="5"><br><br>
  Search: <input type="search" name="q"><br><br>
  <input type="submit">
</form>
```

| Type | What it gives |
|---|---|
| `email` | Checks for an `@` sign |
| `number` | Only numbers; `min` and `max` set limits |
| `date` | A calendar picker |
| `tel` | Phone number keypad on mobile |
| `url` | Checks that it looks like a web address |
| `color` | A colour picker |
| `range` | A slider |
| `search` | A search box |

**Useful attributes:**

| Attribute | Meaning |
|---|---|
| `required` | Must be filled before submitting |
| `placeholder="..."` | Grey hint text inside the box |
| `maxlength="10"` | Longest text allowed |
| `pattern="[0-9]{10}"` | Must match this pattern (here: 10 digits) |
| `disabled` | Cannot be used |

```html
<input type="text" name="mobile" required placeholder="10-digit mobile" pattern="[0-9]{10}">
```

Try pressing Submit with this box empty. The browser shows an error by itself.

## 12. Input and Datalist Elements, and the autocomplete Attribute

**`<datalist>`** gives a text box a list of **suggestions**. The user may pick one or type their own.

```html
<label for="course">Choose a course:</label>
<input list="courses" id="course" name="course">

<datalist id="courses">
  <option value="Computer Science">
  <option value="Electronics">
  <option value="Mechanical">
  <option value="Civil">
</datalist>
```

The `list="courses"` on the input matches the `id="courses"` on the datalist. Start typing "C" and the matching suggestions appear.

**`<select>` versus `<datalist>`:** with `select` the user **must** choose from the list. With `datalist` the user **may** type something else.

**`autocomplete` attribute:** tells the browser whether it may remember and fill in earlier answers.

```html
<input type="text" name="name" autocomplete="on">         <!-- browser may suggest -->
<input type="password" name="pw" autocomplete="off">      <!-- do not remember -->

<form autocomplete="off"> ... </form>                       <!-- applies to the whole form -->
```

| Value | Meaning |
|---|---|
| `on` | Browser may fill in from saved values (like your saved email) |
| `off` | Browser should not save or suggest |

**Real world:** when you click an address box on a shopping site and Chrome offers your saved address, that is autocomplete. The "Where to?" box on a travel site that suggests city names works like a datalist.

### Check your understanding
1. What is the difference between `<select>` and `<datalist>`?
2. When would you set `autocomplete="off"`?
3. Name four HTML5 input types.

## 13. Page Structure Elements

HTML5 has tags that say **what each part of the page is**. They look like the older `<div>` but have a meaning.

```html
<body>
  <header>
    <h1>My College</h1>
    <nav>
      <a href="#">Home</a> |
      <a href="#">Courses</a> |
      <a href="#">Contact</a>
    </nav>
  </header>

  <main>
    <section>
      <h2>Latest news</h2>
      <article>
        <h3>Tech fest on 10 Nov</h3>
        <p>Register now.</p>
      </article>
    </section>

    <aside>
      <p>Advertisement or side links</p>
    </aside>
  </main>

  <footer>
    <p>&copy; 2026 My College</p>
  </footer>
</body>
```

| Tag | Meaning |
|---|---|
| `<header>` | Top part: logo, title |
| `<nav>` | Menu links |
| `<main>` | The main content (once per page) |
| `<section>` | A group of related content |
| `<article>` | A stand-alone piece (news item, blog post) |
| `<aside>` | Side content (ads, extra links) |
| `<footer>` | Bottom part: copyright, contact |

```
+---------------------------+
|          header           |
|            nav            |
+-------------------+-------+
|       main        | aside |
|  (section/article)|       |
+-------------------+-------+
|          footer           |
+---------------------------+
```

**Why use them (exam point):** they make the code easier to read, help search engines understand the page, and help screen readers used by blind people.

**Analogy:** a newspaper has a masthead, columns, a side box and a footer. These tags name each part.

### Check your understanding
1. Name five HTML5 page structure elements.
2. What is the difference between `<section>` and `<article>`?

---

# PART B: CSS

## 14. Introduction to CSS and Basic Syntax

**CSS** (Cascading Style Sheets) controls how HTML looks: colours, fonts, sizes, spaces, layout.

**Analogy:** HTML is a plain white wall. CSS is the paint.

**Basic syntax:**

```
selector {
  property: value;
  property: value;
}
```

```css
h1 {
  color: blue;
  font-size: 32px;
}
```

| Part | Meaning |
|---|---|
| `h1` | **Selector**: which elements to style |
| `color` | **Property**: what to change |
| `blue` | **Value**: how to change it |
| `{ }` | Holds the rules |
| `;` | Ends each rule |

**Comment in CSS:** `/* this is a comment */`

## 15. Inline, Embedded and External Style Sheets

There are **three ways** to add CSS.

**1. Inline style:** written inside one tag, with the `style` attribute. Affects only that tag.

```html
<p style="color: red; font-size: 20px;">This is red.</p>
```

**2. Embedded (internal) style sheet:** written in `<style>` inside `<head>`. Affects that one page.

```html
<head>
  <style>
    p { color: green; }
    h1 { text-align: center; }
  </style>
</head>
```

**3. External style sheet:** written in a separate `.css` file and linked. Affects every page that links to it.

`style.css`:

```css
body { background-color: #f0f8ff; font-family: Arial; }
h1 { color: darkblue; }
```

`index.html`:

```html
<head>
  <link rel="stylesheet" href="style.css">
</head>
```

| | Inline | Embedded | External |
|---|---|---|---|
| Where | In the tag | In `<head>` | Separate file |
| Affects | One element | One page | Whole website |
| Best for | Quick test | One-page site | Real websites |

**Analogy:**
- Inline = a sticky note on one student's desk.
- Embedded = a rule for one classroom.
- External = a rule for the whole college.

**Real world:** real websites use external style sheets, so changing one file changes the look of hundreds of pages.

### Check your understanding
1. Explain the difference between internal and external style sheets with examples. (exam question)
2. Why are external style sheets best for big websites?

## 16. Conflict Resolution

What if two rules say different things about the same element?

```html
<style>
  p { color: green; }
</style>
<p style="color: red;">Which colour am I?</p>
```

The answer is **red**. CSS has rules for deciding the winner.

**The rules, in order:**

1. **`!important`** wins over everything: `color: blue !important;` (use rarely).
2. **More specific wins.** Specificity (how targeted a selector is) from weakest to strongest:
   - element selector (`p`) is weakest
   - class selector (`.note`) is stronger
   - id selector (`#intro`) is stronger still
   - inline style is strongest (apart from `!important`)
3. **If equal, the one written last wins** (later rules override earlier ones).
4. Some properties are **inherited**: a child takes the parent's value if it has no rule of its own (for example, `color` and `font-family`).

**Example:**

```html
<style>
  p        { color: green; }      /* element:  weak */
  .note    { color: blue; }       /* class:    stronger */
  #special { color: orange; }     /* id:       stronger still */
</style>

<p>Green</p>
<p class="note">Blue</p>
<p class="note" id="special">Orange</p>
<p class="note" id="special" style="color: red;">Red (inline wins)</p>
```

**Analogy:** orders in a college. A general notice (element) can be overridden by the department's order (class), by the HOD's personal order (id), and by the principal's direct instruction (inline).

**Exam answer: how would you resolve a conflict?** Find which rules apply, then check `!important`, then specificity (inline > id > class > element), then source order (last one wins). Fix it by writing a more specific selector, reordering the rules, or removing the duplicate. Avoid `!important` unless needed.

**Order of the style sheet types:** if they conflict with equal specificity, the one **closest to the element** and **written last** wins. So inline beats embedded, and embedded beats a `<link>` that comes before it.

### Check your understanding
1. In which colour will this text appear? `p {color: green} .a {color: blue}` on `<p class="a">`.
2. Name the order in which CSS resolves conflicts.

## 17. Selectors

A **selector** chooses which HTML elements a rule applies to.

| Selector | Example | Chooses |
|---|---|---|
| Element | `p { }` | all `<p>` |
| Class | `.note { }` | everything with `class="note"` |
| Id | `#title { }` | the one element with `id="title"` |
| Universal | `* { }` | everything |
| Group | `h1, h2, p { }` | all of these |
| Descendant | `ul li { }` | `<li>` anywhere inside a `<ul>` |
| Child | `ul > li { }` | `<li>` directly inside `<ul>` |
| Attribute | `input[type="text"] { }` | text inputs |
| Pseudo-class | `a:hover { }` | a link while the mouse is over it |

```html
<style>
  p { font-family: Arial; }
  .highlight { background-color: yellow; }
  #main-title { color: purple; }
  a:hover { color: red; }
</style>

<h1 id="main-title">Selectors</h1>
<p>Normal paragraph.</p>
<p class="highlight">Highlighted paragraph.</p>
<a href="#">Hover over me</a>
```

**Class versus id:** a class can be used **many times** on a page. An id must be used **once only**.

**Analogy:** a class is like "all students wearing a blue shirt" (many people). An id is like a roll number (only one person).

## 18. Properties and Values

The most-used properties:

| Group | Properties | Example |
|---|---|---|
| Text | `color`, `font-family`, `font-size`, `font-weight`, `font-style` | `font-size: 18px;` |
| Text layout | `text-align`, `text-decoration`, `line-height`, `letter-spacing`, `text-transform` | `text-align: center;` |
| Box | `width`, `height`, `margin`, `padding`, `border` | `border: 1px solid black;` |
| Background | `background-color`, `background-image` | `background-color: yellow;` |

**Ways to write a colour:**

```css
color: red;               /* name */
color: #ff0000;           /* hex code */
color: rgb(255, 0, 0);    /* red, green, blue amounts */
```

**Units for size:**

| Unit | Meaning |
|---|---|
| `px` | pixels (fixed) |
| `%` | percent of the parent |
| `em`, `rem` | relative to the font size |
| `vw`, `vh` | percent of screen width, height |

```css
p {
  color: #333333;
  font-family: Arial, sans-serif;
  font-size: 18px;
  text-align: justify;
  line-height: 1.6;
}
```

## 19. Backgrounds

```css
body {
  background-color: #e8f4f8;
}

.banner {
  background-image: url("images/campus.jpg");
  background-repeat: no-repeat;     /* do not tile the picture */
  background-size: cover;           /* fill the whole area */
  background-position: center;
  height: 200px;
}
```

| Property | Meaning |
|---|---|
| `background-color` | solid colour |
| `background-image` | picture |
| `background-repeat` | `repeat` (default), `no-repeat`, `repeat-x`, `repeat-y` |
| `background-size` | `cover`, `contain`, or a size |
| `background-position` | where the picture sits |

**Real world:** the large photo behind the title on a college homepage is a CSS background image.

## 20. List Styles

```css
ul { list-style-type: square; }     /* disc, circle, square, none */
ol { list-style-type: upper-roman; } /* decimal, lower-alpha, upper-roman */
ul.menu { list-style-type: none; padding: 0; }   /* remove bullets */
ul.menu li { display: inline-block; margin-right: 15px; }   /* put items in a row */
```

Making a **menu bar** from a list is one of the most common tricks:

```html
<style>
  ul.menu { list-style-type: none; margin: 0; padding: 0; background: #333; }
  ul.menu li { display: inline-block; }
  ul.menu a { display: block; padding: 12px 18px; color: white; text-decoration: none; }
  ul.menu a:hover { background: #555; }
</style>

<ul class="menu">
  <li><a href="#">Home</a></li>
  <li><a href="#">Courses</a></li>
  <li><a href="#">Contact</a></li>
</ul>
```

### Check your understanding
1. Write CSS to remove the bullets from a list.
2. Write CSS to give a page a light blue background.

## 21. Element Dimensions

`width` and `height` set the size of an element.

```css
.card {
  width: 300px;
  height: 150px;
}
.photo { width: 100%; }            /* as wide as its parent */
.box { max-width: 600px; }         /* never wider than 600px */
.box { min-height: 100px; }        /* never shorter than 100px */
```

| Property | Meaning |
|---|---|
| `width`, `height` | exact size |
| `max-width`, `max-height` | upper limit |
| `min-width`, `min-height` | lower limit |

**Tip:** `max-width: 100%; height: auto;` on an image stops it from being wider than the screen.

Overflow: if the content is bigger than the box, use `overflow: auto;` (scroll bars), `hidden` (cut off), or `visible` (spill out).

## 22. Box Model and Text Flow

**Every element is a box.** The box has four layers:

```
+----------------------------------------+
|                 MARGIN                 |   space outside the border
|   +--------------------------------+   |
|   |            BORDER              |   |   the edge line
|   |   +------------------------+   |   |
|   |   |        PADDING         |   |   |   space inside, around content
|   |   |   +----------------+   |   |   |
|   |   |   |    CONTENT     |   |   |   |   text or image
|   |   |   +----------------+   |   |   |
|   |   +------------------------+   |   |
|   +--------------------------------+   |
+----------------------------------------+
```

| Layer | Meaning |
|---|---|
| **Content** | the text or image itself |
| **Padding** | space between content and border (inside) |
| **Border** | the line around |
| **Margin** | space between this box and other boxes (outside) |

**Analogy:** a framed photo on a wall.
- The photo = content.
- The white mount board = padding.
- The wooden frame = border.
- The gap to the next frame on the wall = margin.

```css
.box {
  width: 200px;
  padding: 20px;
  border: 5px solid navy;
  margin: 30px;
  background-color: lightyellow;
}
```

**Writing shortcuts:**

```css
margin: 10px;                      /* all four sides */
margin: 10px 20px;                 /* top and bottom 10, left and right 20 */
margin: 10px 20px 30px 40px;       /* top, right, bottom, left (clockwise) */
margin-top: 10px;                  /* one side only */
```

**Total width = width + left and right padding + left and right border + left and right margin.** With the box above: 200 + 40 + 10 + 60 = 310px.

**`box-sizing: border-box;`** makes `width` include the padding and border, so the box is exactly the width you wrote. Many developers put this at the top of every style sheet:

```css
* { box-sizing: border-box; }
```

**Text flow** is how content is placed on the page. Elements are of two kinds:

| Kind | Behaviour | Examples |
|---|---|---|
| **Block** | Starts on a new line, takes the full width | `div`, `p`, `h1`, `ul` |
| **Inline** | Stays in the line of text, as wide as its content | `span`, `a`, `strong`, `img` |

The `display` property can change this: `display: block;`, `display: inline;`, `display: inline-block;`, `display: none;` (hides it).

Other text flow tools:

```css
img.left { float: left; margin-right: 10px; }   /* text wraps around the picture */
.clear { clear: both; }                          /* stop wrapping */
```

**Real world:** every item on a Flipkart page is a box with padding, border and margin.

**Exam question: centre an image with a border and padding.**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body { text-align: center; }
    img {
      border: 4px solid navy;
      padding: 10px;
    }
  </style>
</head>
<body>
  <img src="photo.jpg" alt="My photo" width="300">
</body>
</html>
```

Another way, for a block image: `img { display: block; margin: 0 auto; }`.

### Check your understanding
1. Draw the box model and name the four parts.
2. What is the difference between padding and margin?
3. What is the difference between block and inline elements?

## 23. `div` and `span`

These two tags have **no look and no meaning of their own**. They are containers we style with CSS.

| Tag | Type | Used for |
|---|---|---|
| `<div>` | block | grouping a **section** of the page |
| `<span>` | inline | styling **a few words** inside a line |

```html
<style>
  .card { border: 1px solid gray; padding: 10px; width: 250px; }
  .price { color: green; font-weight: bold; }
</style>

<div class="card">
  <h3>Masala Dosa</h3>
  <p>Crispy and hot. Price: <span class="price">&#8377;60</span></p>
</div>
```

**Analogy:** a `div` is a **cardboard box** to hold things together. A `span` is a **highlighter pen** used on a few words.

## 24. Positioning: Relative and Absolute

By default, elements sit in the normal flow, one after another. The `position` property lets us move them.

| Value | Meaning |
|---|---|
| `static` | Default. Normal flow |
| `relative` | Stays in flow, but can be **nudged from its own normal place** with `top`, `left`, etc. |
| `absolute` | Taken **out of the flow** and placed relative to the **nearest positioned parent** (or the page if none) |

**Relative:**

```css
.box { position: relative; top: 20px; left: 30px; }   /* moved 20px down, 30px right from where it would be */
```

**Absolute inside a relative parent** (the most useful pattern):

```html
<style>
  .parent {
    position: relative;           /* this becomes the reference */
    width: 300px; height: 150px;
    background: lightblue;
  }
  .badge {
    position: absolute;           /* placed relative to .parent */
    top: 10px; right: 10px;
    background: red; color: white; padding: 4px 8px;
  }
</style>

<div class="parent">
  <span class="badge">NEW</span>
  <p>Course card</p>
</div>
```

The red "NEW" badge sits in the top-right corner of the blue card.

**Analogy:**
- **Relative:** you are in your seat, and you slide your chair 2 feet to the right. Others still treat your original seat as taken.
- **Absolute:** a notice pinned on the wall at an exact spot, measured from the corner of the notice board (the parent). It takes no space among the other items.

**Real world:** the "SALE" tag on a product photo, and the red notification number on an app icon.

### Check your understanding
1. What is the difference between relative and absolute positioning?
2. Why do we usually set the parent to `position: relative`?

## 25. Table Layouts

CSS makes plain tables look good.

```html
<style>
  table { border-collapse: collapse; width: 100%; }
  th, td { border: 1px solid #999; padding: 8px; text-align: left; }
  th { background-color: #333; color: white; }
  tr:nth-child(even) { background-color: #f2f2f2; }   /* zebra stripes */
  tr:hover { background-color: #ddd; }
</style>

<table>
  <tr><th>Name</th><th>Marks</th></tr>
  <tr><td>Anu</td><td>85</td></tr>
  <tr><td>Rahul</td><td>78</td></tr>
  <tr><td>Meera</td><td>92</td></tr>
</table>
```

| Property | Meaning |
|---|---|
| `border-collapse: collapse` | Joins the double borders into one line |
| `padding` on `td` | Space inside cells |
| `text-align` | Left, centre or right in cells |
| `width` | Width of the table |
| `table-layout: fixed` | Columns have equal fixed widths |

## 26. Basics of Responsive CSS: Viewport and Media Queries

**Responsive design** means the page **adjusts itself** to the screen: laptop, tablet or phone.

**Step 1: the viewport meta tag.** Without it, phones show the page as a tiny zoomed-out desktop page. Always put this in `<head>`:

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

It tells the phone: "use your real screen width".

**Step 2: flexible sizes.** Use `%` or `max-width` instead of fixed pixel widths:

```css
img { max-width: 100%; height: auto; }
.container { width: 90%; max-width: 1000px; margin: 0 auto; }
```

**Step 3: media queries.** These apply CSS **only when a condition is true**, such as a small screen.

```css
/* default: big screens, two columns side by side */
.column { float: left; width: 50%; }

/* screens 600px wide or narrower (phones): stack the columns */
@media (max-width: 600px) {
  .column { float: none; width: 100%; }
}
```

**Full example:** a header and two sections side by side that stack on a phone. This also answers the exam question *"basic layout with a header and two sections side by side"*.

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Responsive Layout</title>
  <style>
    * { box-sizing: border-box; }
    body { margin: 0; font-family: Arial; }

    header {
      background: #333; color: white;
      text-align: center; padding: 20px;
    }

    .row::after { content: ""; display: block; clear: both; }   /* clear the floats */

    .left  { float: left; width: 30%; background: #ddd;    padding: 15px; min-height: 150px; }
    .right { float: left; width: 70%; background: #f4f4f4; padding: 15px; min-height: 150px; }

    @media (max-width: 600px) {
      .left, .right { float: none; width: 100%; }
    }
  </style>
</head>
<body>
  <header><h1>My College</h1></header>
  <div class="row">
    <div class="left">Menu / Sidebar</div>
    <div class="right">Main content goes here.</div>
  </div>
</body>
</html>
```

How it works: `float: left` with widths 30% and 70% puts the two sections side by side under the header. The media query makes both full width on screens up to 600px, so they stack. Resize the browser window to see it change.

**Common breakpoints:** about 600px (phones), 768px (tablets), 1024px (laptops).

**Real world:** open the IRCTC or Flipkart site on a laptop and then on a phone. The layout changes using exactly this.

### Check your understanding
1. What does the viewport meta tag do?
2. What is a media query? Write one that makes the text red on screens narrower than 500px.
3. Why use `%` instead of `px` for widths?

---

# PART C: Mini-Project and Exam Questions

## Mini-project: College Fest Page

Create a folder `fest` with two files, `index.html` and `style.css`. Students must use: header, nav, section, table, form, lists, images, an external style sheet, box model, and one media query.

**index.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Tech Fest 2026 registration page">
  <title>Tech Fest 2026</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header>
    <h1>Tech Fest 2026</h1>
    <nav>
      <a href="#events">Events</a>
      <a href="#schedule">Schedule</a>
      <a href="#register">Register</a>
    </nav>
  </header>

  <main>
    <section id="events">
      <h2>Events</h2>
      <ul>
        <li>Web Design Contest</li>
        <li>Coding Challenge</li>
        <li>Quiz</li>
      </ul>
    </section>

    <section id="schedule">
      <h2>Schedule</h2>
      <table>
        <tr><th>Event</th><th>Date</th><th>Venue</th></tr>
        <tr><td>Web Design Contest</td><td>10 Nov</td><td>Lab 1</td></tr>
        <tr><td>Coding Challenge</td><td>11 Nov</td><td>Lab 2</td></tr>
        <tr><td>Quiz</td><td>12 Nov</td><td>Seminar Hall</td></tr>
      </table>
    </section>

    <section id="register">
      <h2>Register</h2>
      <form>
        <label for="name">Name</label>
        <input type="text" id="name" required>

        <label for="email">Email</label>
        <input type="email" id="email" required>

        <label for="dept">Department</label>
        <input list="depts" id="dept">
        <datalist id="depts">
          <option value="CSE">
          <option value="ECE">
          <option value="Mechanical">
        </datalist>

        <label for="dob">Date of birth</label>
        <input type="date" id="dob">

        <button type="submit">Register</button>
      </form>
    </section>
  </main>

  <footer>
    <p>&copy; 2026 My College</p>
  </footer>
</body>
</html>
```

**style.css**

```css
* { box-sizing: border-box; }

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background-color: #f4f8fb;
}

header {
  background-color: #1a3c6e;
  color: white;
  text-align: center;
  padding: 20px;
}

nav a {
  color: white;
  text-decoration: none;
  margin: 0 12px;
}
nav a:hover { text-decoration: underline; }

main {
  max-width: 800px;
  margin: 0 auto;
  padding: 15px;
}

section {
  background: white;
  border: 1px solid #ccc;
  border-radius: 6px;
  padding: 15px;
  margin-bottom: 20px;
}

table { border-collapse: collapse; width: 100%; }
th, td { border: 1px solid #999; padding: 8px; text-align: left; }
th { background-color: #1a3c6e; color: white; }
tr:nth-child(even) { background-color: #f2f2f2; }

form label { display: block; margin-top: 10px; }
form input { width: 100%; padding: 8px; margin-top: 4px; }
button { margin-top: 15px; padding: 10px 20px; background: #1a3c6e; color: white; border: none; border-radius: 4px; }

footer { background-color: #333; color: white; text-align: center; padding: 10px; }

@media (max-width: 600px) {
  header h1 { font-size: 22px; }
  nav a { display: block; margin: 8px 0; }
}
```

**Extension ideas:** add a banner image with a CSS background, a "NEW" badge using absolute positioning, a "Back to top" internal link.

---

## Exam Questions (short answers)

**Q1. Explain the difference between internal and external style sheets in CSS with examples. (3 marks)**

An **internal (embedded)** style sheet is written inside `<style>` in the `<head>` and affects only that page. An **external** style sheet is a separate `.css` file linked with `<link rel="stylesheet" href="style.css">`, and can style many pages.

```html
<!-- internal -->
<style> p { color: green; } </style>

<!-- external -->
<link rel="stylesheet" href="style.css">
```

External is better for big websites because one change updates every page.

**Q2. A web page shows conflicting styles. How do you resolve the conflict using CSS principles? (3 marks)**

See Section 16. Answer in order: `!important`, then specificity (inline > id > class > element), then source order (last wins). Fix by using a more specific selector, reordering rules, or removing duplicates.

**Q3. Explain the structure of an HTML5 form. Write a sample form with at least three different input types. Explain autocomplete and datalist. (6 marks)**

A form uses `<form>` with `action` and `method`. Inside are `<label>` and `<input>` elements, each with a `type` and `name`, and a submit button.

```html
<form action="/register" method="post" autocomplete="on">
  <label for="name">Name:</label>
  <input type="text" id="name" name="name" required><br><br>

  <label for="email">Email:</label>
  <input type="email" id="email" name="email" required><br><br>

  <label for="dob">Date of birth:</label>
  <input type="date" id="dob" name="dob"><br><br>

  <label for="course">Course:</label>
  <input list="courses" id="course" name="course">
  <datalist id="courses">
    <option value="CSE">
    <option value="ECE">
    <option value="Mechanical">
  </datalist><br><br>

  <input type="submit" value="Register">
</form>
```

`autocomplete="on"` lets the browser fill in saved answers, and `off` stops it. `<datalist>` gives a text box a list of suggestions that the user can pick or ignore, linked using the input's `list` attribute and the datalist's `id`.

**Q4. Create a basic layout with a header at the top and two sections side by side using CSS. Mention the technique. (3 marks)**

Use the example in Section 26. Technique: `float: left` with widths 30% and 70% (or `display: flex`), and a media query to stack them on small screens.

**Q5. Explain the box model with a diagram. Describe content, padding, border and margin. (5 marks)**

Draw the diagram from Section 22 and explain each layer. Add the example:

```css
.box { width: 200px; padding: 20px; border: 5px solid navy; margin: 30px; }
```

Total width = 200 + (2 x 20) + (2 x 5) + (2 x 30) = 310px.

**Q6. HTML and CSS to display an image in the centre of the page with a border and padding. (4 marks)**

Use the code in Section 22.

**More practice:**
1. Explain any four HTML5 form input types. (3 marks)
2. What is the difference between `id` and `class` selectors? (3 marks)
3. Explain relative and absolute positioning with an example. (5 marks)
4. What is a media query? How does it help in responsive design? (3 marks)
5. List the HTML5 page structure elements and their use. (4 marks)
6. Differentiate between block and inline elements. (3 marks)
7. Write HTML and CSS for a table with alternate row colours. (4 marks)
