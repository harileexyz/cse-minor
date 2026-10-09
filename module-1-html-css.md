# Module 1: HTML5 and CSS3 (Web Application Development, MNCST509)

**Programme:** B.Tech CSE Minor, KTU, Semester 5
**Course:** Web Application Development (MNCST509)
**Module:** 1 - Introduction to HTML5 and Style Sheets
**Contact hours:** 11
**Audience:** Beginners. No earlier web development knowledge is assumed.

---

## Table of Contents

1. Learning outcomes
2. Suggested lesson plan (11 hours)
3. Setting up (tools you need)
4. Part A: HTML5
   1. Structuring and editing an HTML5 document
   2. Fundamentals of HTML
   3. Headings
   4. Hyperlinks
   5. Images
   6. Special characters and horizontal rules
   7. Lists
   8. Tables
   9. Forms
   10. Internal linking
   11. Meta elements
   12. HTML5 form input types
   13. Input and datalist elements, and the autocomplete attribute
   14. Page structure elements
5. Part B: CSS
   15. Introduction to CSS
   16. Basic syntax and structure
   17. Inline styles, embedded style sheets, external style sheets
   18. Conflict resolution (cascade, specificity, importance, source order)
   19. CSS selectors
   20. Properties and values
   21. Positioning: absolute and relative
   22. Backgrounds
   23. List styles
   24. Element dimensions
   25. Table layouts
   26. Box model and text flow
   27. div and span
   28. Responsive CSS, viewport and media queries
6. Mini project: College fest registration page
7. Question bank (KTU exam style)
8. Quick revision sheet

---

## 1. Learning outcomes

After this module, a student will be able to:

- **LO1.** Write a complete, valid HTML5 page with correct structure.
- **LO2.** Use headings, links, images, lists, tables and forms to present content.
- **LO3.** Build forms using HTML5 input types, `datalist` and `autocomplete`.
- **LO4.** Use meta elements and page structure elements (`header`, `nav`, `main`, `section`, `article`, `aside`, `footer`).
- **LO5.** Apply CSS in three ways (inline, embedded, external) and explain which one wins when styles clash.
- **LO6.** Use CSS selectors, properties, backgrounds, list styles and table styles.
- **LO7.** Explain and use the box model, element dimensions, positioning, `div` and `span`.
- **LO8.** Make a simple page that adjusts to phone, tablet and laptop screens using the viewport meta tag and media queries.

---

## 2. Suggested lesson plan (11 contact hours)

Each session mixes a short talk (explain + analogy), a live coding demo, and a short student activity. Rule of thumb: **20 minutes talk, 25 minutes code, 15 minutes student try-out** per hour.

| Session | Duration | Topics | Activity |
|---|---|---|---|
| 1 | 1 hr | What is the web, how a page reaches your phone, HTML5 document structure, fundamentals, headings | "Build your visiting card" page |
| 2 | 1 hr | Hyperlinks, images, special characters, horizontal rules | Link your page to 3 real sites, add a photo |
| 3 | 1 hr | Lists, tables | Make a class timetable table |
| 4 | 1 hr | Forms basics, internal linking, meta elements | Student feedback form |
| 5 | 1 hr | HTML5 input types, datalist, autocomplete, page structure elements | "IRCTC style" booking form |
| 6 | 1 hr | Introduction to CSS, syntax, inline/embedded/external | Style yesterday's visiting card |
| 7 | 1 hr | Conflict resolution (cascade, specificity, importance, order), selectors | "Who wins?" quiz game |
| 8 | 1 hr | Properties/values, backgrounds, list styles, element dimensions | Make a Swiggy-style menu list |
| 9 | 1 hr | Box model, text flow, `div` and `span`, table layouts | Draw the box model on paper, then in browser |
| 10 | 1 hr | Positioning (relative, absolute), simple layouts | Header + two columns layout |
| 11 | 1 hr | Responsive CSS, viewport, media queries, revision, start mini project | Mini project (finish at home) |

Tip for the teacher: keep a browser and a code editor side by side on the projector. Change one line, save, refresh. Students learn web development fastest when they *see* each change.

---

## 3. Setting up (tools you need)

You only need three things. All are free.

1. **A browser:** Chrome, Edge or Firefox.
2. **A code editor:** Visual Studio Code (VS Code). Install the "Live Server" extension so the page refreshes by itself when you save.
3. **A folder:** Make a folder called `module1`. Keep every practice file inside it.

**How to run a page:** Save the file with the extension `.html` (for example `index.html`). Double-click it. It opens in the browser. Or right-click in VS Code and choose "Open with Live Server".

**Developer tools:** Press `F12` in the browser. Click the small arrow icon and then click any part of a web page. You can see its HTML and CSS. This works on Flipkart, IRCTC, any site. Great for learning (you can only change it on your own screen, not on the real site).

### How a web page reaches you (30-second story)

```text
 Your phone/laptop               Internet                 Server (Flipkart's computer)
 (Browser)         --- request: "give me flipkart.com" --->
                   <--- reply: HTML + CSS + images ---------
 Browser reads the HTML and CSS and draws the page.
```

- **HTML** = the content and structure (the *skeleton*).
- **CSS** = the look (the *clothes and makeup*).
- **JavaScript** = the behaviour (the *muscles*). This comes in later modules.

---

# PART A: HTML5

---

## Topic 1. Structuring and editing an HTML5 document

### Simple explanation

HTML stands for **HyperText Markup Language**. It is not a programming language. It is a *markup* language: you wrap text in **tags** to tell the browser what each piece of text is (a heading, a paragraph, a link, and so on).

Every HTML5 page follows the same basic skeleton:

- `<!DOCTYPE html>` tells the browser "this is an HTML5 page".
- `<html>` is the outer box that holds everything.
- `<head>` holds information *about* the page (title, character set, links to CSS). It is not shown on the page itself.
- `<body>` holds everything the visitor *sees*.

### Analogy

Think of a **college admission form**. The top part has the form number, the academic year and office-use boxes (that is the `head`: details about the form). The bottom part is where the student writes name, address and marks (that is the `body`: the actual content). The `DOCTYPE` is like the heading "Government of Kerala, Application Form" which tells you what kind of paper it is.

### Code example

Save as `index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My First Page</title>
</head>
<body>
  <h1>Hello, Kerala!</h1>
  <p>This is my first web page. I am learning HTML5.</p>
</body>
</html>
```

**Line by line:**

| Line | Meaning |
|---|---|
| `<!DOCTYPE html>` | Use modern HTML5 rules. Always the first line. |
| `<html lang="en">` | Root element. `lang="en"` says the page is in English (helps screen readers and search engines). |
| `<meta charset="UTF-8">` | Letters and symbols (even Malayalam) show correctly. |
| `<meta name="viewport" ...>` | Makes the page fit phone screens (more in Topic 28). |
| `<title>` | The text on the browser tab. Also used in Google results and bookmarks. |
| `<body>` | Everything the visitor sees. |

### Editing tips

- **Indent** (push inside lines to the right) child tags by 2 spaces. It makes mistakes easy to find.
- **Close every tag.** If you open `<p>`, close with `</p>`.
- **Nest properly.** Close the *inner* tag first. `<b><i>text</i></b>` is right; `<b><i>text</b></i>` is wrong.
- **Comments** are notes for humans. The browser ignores them: `<!-- this is a comment -->`.
- Tag names are not case sensitive, but write them in **lowercase** by convention.
- The browser ignores extra spaces and line breaks. 10 spaces look the same as 1 space.

### Real-world example

Right-click on the IRCTC or your college website and choose "View page source". You will see this same skeleton: `DOCTYPE`, `html`, `head` with title and links, then `body`. Every website in the world starts like this.

### Common mistakes

- Forgetting `<!DOCTYPE html>` (browser switches to "quirks mode" and may display things oddly).
- Putting visible content in `<head>`.
- Saving the file as `index.html.txt` (Windows hides extensions). Turn on "show file extensions".
- Not closing tags.

### Check your understanding

1. What is the difference between `<head>` and `<body>`?
2. Why do we write `<meta charset="UTF-8">`?
3. What text shows on the browser tab, and which tag controls it?
4. Is HTML a programming language? Why or why not?

### Classroom activity (5 min): "Spot the 4 errors"

Show this on the board and ask students to find the errors.

```html
<html>
<head>
  <h1>My Page</h1>
</head>
<body>
  <p>Hello <b><i>world</b></i>
</body>
```

Answers: no DOCTYPE; heading placed in `head`; wrong nesting of `b` and `i`; `<p>` not closed (and `</html>` missing).

---

## Topic 2. Fundamentals of HTML (tags, elements, attributes, text)

### Simple explanation

- **Tag:** the word in angle brackets, like `<p>`. Most come in pairs: an opening tag `<p>` and a closing tag `</p>`.
- **Element:** the opening tag + content + closing tag. `<p>Hello</p>` is one paragraph element.
- **Attribute:** extra information inside the opening tag, written as `name="value"`. Example: `<a href="https://www.google.com">`.
- **Empty (void) elements:** have no content and no closing tag. Examples: `<br>`, `<hr>`, `<img>`, `<input>`, `<meta>`.
- **Block vs inline:**
  - *Block* elements take a full row and start on a new line (`p`, `h1`, `div`, `ul`).
  - *Inline* elements stay inside the line (`a`, `b`, `span`, `img`).

Common text tags:

| Tag | Use |
|---|---|
| `<p>` | Paragraph |
| `<br>` | Line break |
| `<b>` / `<strong>` | Bold / important text |
| `<i>` / `<em>` | Italic / emphasised text |
| `<u>` | Underline |
| `<mark>` | Highlighted text |
| `<small>` | Small print |
| `<sub>` / `<sup>` | Subscript / superscript (H<sub>2</sub>O, x<sup>2</sup>) |
| `<del>` / `<ins>` | Deleted / inserted text |
| `<blockquote>` | Long quote |
| `<code>` / `<pre>` | Code text / keep spaces and line breaks as typed |

`<strong>` and `<em>` carry *meaning* ("this is important"); `<b>` and `<i>` only change the look. Prefer `strong` and `em`.

Global attributes that work on almost every tag: `id`, `class`, `style`, `title` (tooltip), `lang`, `hidden`.

### Analogy

A tag is like a **label on a tiffin box**: "Rice", "Curry", "Pickle". The label tells you what is inside without opening it. An attribute is the *extra note* on the label, like "extra spicy".

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Text Basics</title>
</head>
<body>
  <p>This is a normal paragraph. The browser <strong>wraps</strong> long lines by itself.</p>

  <p>Roses are red,<br>Violets are blue,<br>HTML is easy,<br>And so are you.</p>

  <p>Water is H<sub>2</sub>O and area of a square is a<sup>2</sup>.</p>

  <p>Old price: <del>Rs. 999</del> New price: <ins>Rs. 499</ins></p>

  <p>This is <mark>highlighted</mark> and this is <em>emphasised</em>.</p>

  <pre>
 Line one
    Line two (spaces are kept)
  </pre>

  <p title="I am a tooltip">Hover over me.</p>
</body>
</html>
```

### Real-world example

Flipkart shows the old price struck out and the new price next to it. That is exactly the `<del>` and `<ins>` idea (they use CSS for style, but the meaning is the same). News sites use `<blockquote>` for quoted statements.

### Common mistakes

- Using many `<br>` tags to make space. Use CSS margins instead.
- Using `<b>` where `<strong>` is meant.
- Writing `<p>` inside another `<p>`. Not allowed.
- Using quotes wrongly in attributes: `href=https://x.com` without quotes can break.

### Check your understanding

1. Define tag, element and attribute with one example each.
2. Name four empty elements.
3. What is the difference between block and inline elements? Give two examples each.
4. Why is `<strong>` preferred over `<b>`?

---

## Topic 3. Headings

### Simple explanation

HTML has six heading levels: `<h1>` (biggest, most important) down to `<h6>` (smallest). Headings give a page its **outline**. Rules of good practice:

- Use only **one `<h1>`** per page (the main title).
- Do not skip levels (do not jump from `h1` to `h4`).
- Do not use headings just to make text big. Use CSS for size.

Screen readers and Google use headings to understand your page.

### Analogy

A **newspaper**: the big front-page headline is `h1`, section titles like "Sports" and "Business" are `h2`, and the title of each news item under Sports is `h3`.

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Headings Demo</title>
</head>
<body>
  <h1>Kerala Daily News</h1>

  <h2>Sports</h2>
  <h3>Kerala Blasters win at Kochi</h3>
  <p>Match report goes here.</p>

  <h2>Business</h2>
  <h3>Gold rate drops in Kerala</h3>
  <h4>Details for jewellers</h4>
  <p>Business report goes here.</p>

  <h5>Small heading (h5)</h5>
  <h6>Smallest heading (h6)</h6>
</body>
</html>
```

### Real-world example

A Wikipedia page has one `h1` (the article name), then `h2` for each section ("History", "Geography"), and `h3` for sub-sections. The "contents" box at the top is built from these headings.

### Common mistakes

- Using `<h1>` many times on one page.
- Picking heading level by size, not by importance.
- Using `<b>` instead of a heading for section titles.

### Check your understanding

1. How many heading levels does HTML have?
2. Why should a page normally have only one `h1`?
3. Which heading is right for a sub-section inside an `h2` section?

---

## Topic 4. Hyperlinks

### Simple explanation

A hyperlink takes the visitor from one page to another. It uses the **anchor** tag `<a>` with the `href` (hypertext reference) attribute, which holds the destination.

```html
<a href="destination">Clickable text</a>
```

Types of destination:

| Type | Example |
|---|---|
| Absolute URL (full address on another site) | `https://www.ktu.edu.in` |
| Relative URL (file in your own site) | `about.html`, `pages/contact.html`, `../index.html` |
| Email link | `mailto:hod@college.edu` |
| Phone link | `tel:+914712345678` |
| Section in same page | `#contact` (see Topic 10) |
| File download | `<a href="notes.pdf" download>` |

Useful attributes:

- `target="_blank"` opens the link in a new tab.
- `rel="noopener noreferrer"` goes with `target="_blank"` for safety.
- `title="..."` shows a tooltip.

A link can also wrap an image (see Topic 5).

### Analogy

A hyperlink is a **KSRTC route board** on a bus: "Ernakulam - Thrissur". It says where you will land if you step in. An absolute URL is the full address with state and pin code. A relative URL is "the shop next door" (only makes sense from where you stand).

### Code example

Create `index.html` and `about.html` in the same folder.

`index.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Links Demo</title>
</head>
<body>
  <h1>Useful links</h1>
  <ul>
    <li><a href="https://www.ktu.edu.in" target="_blank" rel="noopener noreferrer">KTU website (new tab)</a></li>
    <li><a href="about.html">About page (my own file)</a></li>
    <li><a href="mailto:hod@example.edu">Email the HOD</a></li>
    <li><a href="tel:+914712345678">Call the college office</a></li>
    <li><a href="syllabus.pdf" download>Download syllabus</a></li>
  </ul>
</body>
</html>
```

`about.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>About</title>
</head>
<body>
  <h1>About us</h1>
  <p><a href="index.html">Back to home</a></p>
</body>
</html>
```

### Real-world example

- The "Call us" button on a Zomato restaurant page uses a `tel:` link; tapping it opens your phone dialer.
- The WhatsApp "Chat with us" button on small business sites is a link: `https://wa.me/919876543210`.
- The IRCTC menu bar is a set of links.

### Common mistakes

- Forgetting `https://` on outside links. Then the browser looks for a file in your own folder.
- Wrong file name or capital letters (`About.html` vs `about.html` may fail on servers).
- Link text like "click here". Better: "Download the syllabus".
- `target="_blank"` without `rel="noopener noreferrer"`.

### Check your understanding

1. Which attribute holds the destination of a link?
2. Difference between absolute and relative URL, with an example each?
3. How do you make a link that opens the mail app?
4. What does `target="_blank"` do?

---

## Topic 5. Images

### Simple explanation

The `<img>` tag shows a picture. It is an empty element.

```html
<img src="photo.jpg" alt="Description of the photo" width="300" height="200">
```

- `src` (source): file path or URL of the image. Required.
- `alt` (alternative text): text shown if the image fails to load, and read aloud by screen readers. Required for good practice.
- `width`, `height`: size in pixels. Set both so the page does not "jump" while loading.
- `loading="lazy"`: load the image only when the user scrolls near it. Saves data.

Common formats: **JPG** (photos), **PNG** (logos, transparency), **GIF** (small animations), **SVG** (sharp icons that never blur), **WebP** (modern, small size).

`<figure>` and `<figcaption>` wrap an image with its caption.

### Analogy

`<img>` is like a **photo stuck on a notice board with a name label below**. The `src` is where the photo is kept in the cupboard; the `alt` is the name label, so even if the photo falls off, people still know what it was.

### Code example

Put a picture called `campus.jpg` in the same folder (or use any image file name you have).

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Images Demo</title>
</head>
<body>
  <h1>Our Campus</h1>

  <!-- Local image -->
  <img src="campus.jpg" alt="Main block of our college" width="400">

  <!-- Image from internet -->
  <img src="https://via.placeholder.com/200x100" alt="Grey placeholder box" width="200" height="100">

  <!-- Image with a caption -->
  <figure>
    <img src="campus.jpg" alt="Main block of our college" width="300">
    <figcaption>Figure 1: The main block.</figcaption>
  </figure>

  <!-- Image as a link -->
  <a href="https://www.ktu.edu.in">
    <img src="logo.png" alt="KTU logo - click to visit KTU" width="80">
  </a>
</body>
</html>
```

(If the images are missing, you will see the `alt` text. That itself is a good demo of why `alt` matters.)

### Real-world example

Every product card on Flipkart or Amazon is an `<img>` with `alt` text of the product name. Product images on Swiggy use `loading="lazy"` so the page does not download 200 food pictures at once.

### Common mistakes

- Wrong path in `src`. Image shows a broken icon.
- Missing `alt` attribute.
- Using a huge 8 MB photo at 100 px size. The page becomes slow. Compress images.
- Stretching only one of width or height so the picture looks squashed.

### Check your understanding

1. What is the purpose of `alt`?
2. Name two image formats and where each fits best.
3. How do you make an image clickable?
4. What does `loading="lazy"` do?

---

## Topic 6. Special characters (entities) and horizontal rules

### Simple explanation

**Special characters.** Some characters have a special job in HTML (like `<` which starts a tag). Some are not on the keyboard (like the copyright sign). For these we use **character entities**: they start with `&` and end with `;`.

| You want | Write | Name |
|---|---|---|
| `<` | `&lt;` | less than |
| `>` | `&gt;` | greater than |
| `&` | `&amp;` | ampersand |
| `"` | `&quot;` | quote |
| copyright sign | `&copy;` | copyright |
| registered sign | `&reg;` | registered |
| trademark sign | `&trade;` | trademark |
| Indian rupee sign | `&#8377;` | rupee (number code) |
| non-breaking space | `&nbsp;` | extra visible space |
| right arrow | `&rarr;` | arrow |
| degree sign | `&deg;` | degree |
| heart | `&hearts;` | heart |

`&nbsp;` is a space that does not wrap and is not collapsed. Do not use many of them to push text around; use CSS.

**Horizontal rule.** `<hr>` draws a line across the page. It marks a change of topic. It is an empty element.

### Analogy

Entities are like **writing "Rs." instead of the rupee symbol when your keyboard does not have it**: a code that stands for a character. `<hr>` is like the **line you draw on paper** to separate one answer from another.

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Entities and Rules</title>
</head>
<body>
  <h1>Special Characters</h1>

  <p>To start a paragraph, write &lt;p&gt; and to end it write &lt;/p&gt;.</p>
  <p>Tom &amp; Jerry, Rs.&nbsp;500 or &#8377;500</p>
  <p>Temperature: 32&deg;C in Kochi &rarr; 24&deg;C in Munnar</p>

  <hr>

  <h2>Second topic</h2>
  <p>The line above separates the two topics.</p>

  <hr width="50%" align="left">

  <footer>
    <p>&copy; 2026 My College. All rights reserved.</p>
  </footer>
</body>
</html>
```

(Note: `width` and `align` on `<hr>` are old style and work only for demo. In real work, size and position the line using CSS.)

### Real-world example

Every website footer has "&copy; 2026 Company Name". Price tags use the rupee entity. Tutorial sites show code like `<div>` on the page by writing `&lt;div&gt;`.

### Common mistakes

- Typing `<` directly in text (the browser thinks a tag has started).
- Forgetting the `;` at the end of an entity.
- Using `&nbsp;` many times for layout.
- Using `<hr>` just as decoration. It should mean a topic break.

### Check your understanding

1. Why do we need character entities? Write the entity for `<`, `&` and the copyright sign.
2. What does `&nbsp;` do?
3. Which tag draws a horizontal line? Is it an empty element?

---

## Topic 7. Lists

### Simple explanation

HTML has three kinds of lists:

1. **Unordered list** `<ul>`: bullets. For items where order does not matter.
2. **Ordered list** `<ol>`: numbers (or letters). For steps or rankings.
3. **Description list** `<dl>`: term + description pairs. Uses `<dt>` (term) and `<dd>` (description).

Items of `ul` and `ol` go in `<li>` (list item). Lists can be **nested** (a list inside an `<li>`).

Useful attributes on `<ol>`: `type="a"` (letters), `type="I"` (roman), `start="5"`, `reversed`.

### Analogy

- `<ul>` is a **shopping list** for the tea shop: tea leaves, sugar, milk. Order does not matter.
- `<ol>` is a **recipe**: Step 1 boil water, Step 2 add tea. Order matters.
- `<dl>` is a **dictionary**: word and its meaning.

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Lists Demo</title>
</head>
<body>
  <h2>Tea Shop Stock (unordered)</h2>
  <ul>
    <li>Tea leaves</li>
    <li>Sugar</li>
    <li>Milk</li>
  </ul>

  <h2>How to make chai (ordered)</h2>
  <ol>
    <li>Boil water.</li>
    <li>Add tea leaves and ginger.</li>
    <li>Add milk and sugar.</li>
    <li>Strain and serve hot.</li>
  </ol>

  <h2>Top 3 (letters, starting at C)</h2>
  <ol type="A" start="3">
    <li>Third item, shown as C</li>
    <li>Fourth item, shown as D</li>
  </ol>

  <h2>Nested list: Semester 5 subjects</h2>
  <ul>
    <li>Web Application Development
      <ul>
        <li>Module 1: HTML and CSS</li>
        <li>Module 2: JavaScript</li>
      </ul>
    </li>
    <li>Computer Networks</li>
  </ul>

  <h2>Description list</h2>
  <dl>
    <dt>HTML</dt>
    <dd>Language used to build the structure of a web page.</dd>
    <dt>CSS</dt>
    <dd>Language used to style a web page.</dd>
  </dl>
</body>
</html>
```

### Real-world example

- The menu on every website is usually a `<ul>` of links.
- A "Order summary" with steps on Swiggy (placed, preparing, out for delivery) is an ordered flow.
- FAQ pages use description lists (question and answer).

### Common mistakes

- Putting text directly inside `<ul>` without `<li>`.
- Closing the outer `<li>` before the nested list.
- Using `<br>` and symbols to fake a list.

### Check your understanding

1. Which list type would you choose for "Steps to book a train ticket"? Why?
2. Write the code of a nested list with two main items and two sub items under the first.
3. What are `dt` and `dd`?

---

## Topic 8. Tables

### Simple explanation

A table shows data in rows and columns. Tags:

| Tag | Meaning |
|---|---|
| `<table>` | The whole table |
| `<caption>` | Title of the table |
| `<thead>`, `<tbody>`, `<tfoot>` | Header, body, footer groups |
| `<tr>` | Table row |
| `<th>` | Header cell (bold, centred by default) |
| `<td>` | Data cell |
| `colspan="n"` | Cell stretches across n columns |
| `rowspan="n"` | Cell stretches across n rows |

Use tables **only for data**, not to design page layouts (that is old-fashioned; use CSS).

### Analogy

A table is the **KTU timetable on the classroom wall** or an **IRCTC train schedule chart**: rows for each train or period, columns for details. A merged cell (`colspan`) is like the "Lunch break" cell stretching across all columns.

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Table Demo</title>
</head>
<body>
  <table border="1" cellpadding="6">
    <caption>Class Timetable - S5 CSE Minor</caption>
    <thead>
      <tr>
        <th>Day</th>
        <th>Period 1</th>
        <th>Period 2</th>
        <th>Period 3</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Monday</td>
        <td>Web Dev</td>
        <td>Networks</td>
        <td>Lab</td>
      </tr>
      <tr>
        <td>Tuesday</td>
        <td>Networks</td>
        <td colspan="2">Seminar (two periods)</td>
      </tr>
      <tr>
        <td>Wednesday</td>
        <td rowspan="2">Library (two days)</td>
        <td>Web Dev</td>
        <td>Maths</td>
      </tr>
      <tr>
        <td>Thursday</td>
        <td>Maths</td>
        <td>Web Dev</td>
      </tr>
    </tbody>
    <tfoot>
      <tr>
        <td colspan="4">Timetable may change. Check notice board.</td>
      </tr>
    </tfoot>
  </table>
</body>
</html>
```

(The `border` and `cellpadding` attributes are old HTML; we use them only to see the grid quickly. In Topic 25 we do it properly with CSS.)

### Real-world example

- IRCTC "Train between stations" result list.
- Marks list on the KTU result page.
- Price comparison grids on Flipkart (phone specifications).

### Common mistakes

- Cells not matching in count per row (columns look broken).
- Using a table to place images and text in columns (layout tables).
- Forgetting `<th>` for header cells (bad for screen readers).
- Wrong `colspan` numbers.

### Check your understanding

1. Differences between `th` and `td`?
2. Write a table with 2 rows and 3 columns, with a header row.
3. What does `rowspan="2"` do?
4. Why should we not use tables for page layout?

---

## Topic 9. Forms

### Simple explanation

A form collects information from the visitor and sends it to a server (login, sign-up, search, payment). Basic structure:

```html
<form action="/submit" method="post">
  <label for="name">Name</label>
  <input type="text" id="name" name="name">
  <button type="submit">Send</button>
</form>
```

Parts of a form:

| Part | Role |
|---|---|
| `<form>` | Container. `action` = where to send the data (a server address). `method` = how: `get` (data goes in the URL, for searches) or `post` (data hidden in the request body, for passwords and big data). |
| `<label>` | Text beside a field. `for="id"` links it to the field, so clicking the label focuses the field. |
| `<input>` | One-line field of many types. |
| `<textarea>` | Multi-line text box. |
| `<select>` + `<option>` | Drop-down list. |
| `<button>` | Click button. `type="submit"` sends, `type="reset"` clears. |
| `<fieldset>` + `<legend>` | Group related fields with a title. |

Important attributes: `name` (the key the server receives; without it, the field's data is **not sent**), `id` (unique tag for label and CSS), `value`, `placeholder` (grey hint), `required`, `disabled`, `readonly`, `maxlength`, `min`, `max`.

Radio buttons that share the same `name` form one group (only one can be picked). Checkboxes allow many.

### Analogy

A form is a **paper application form at a bank counter**. The `<form>` is the whole sheet. `action` is the counter where you submit it. Each `<input>` is a box to fill. `label` is the printed text "Name:". Pressing "submit" is handing it over to the clerk (the server).

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Student Feedback Form</title>
</head>
<body>
  <h1>Student Feedback</h1>

  <form action="https://example.com/feedback" method="post">

    <fieldset>
      <legend>Your details</legend>

      <p>
        <label for="sname">Full name:</label>
        <input type="text" id="sname" name="sname" placeholder="Anu Mathew" required>
      </p>

      <p>
        <label for="mail">Email:</label>
        <input type="email" id="mail" name="mail" required>
      </p>

      <p>Year:
        <input type="radio" id="y3" name="year" value="3"> <label for="y3">3rd</label>
        <input type="radio" id="y4" name="year" value="4"> <label for="y4">4th</label>
      </p>

      <p>
        <label for="dept">Department:</label>
        <select id="dept" name="dept">
          <option value="">-- choose --</option>
          <option value="cse">CSE</option>
          <option value="ece">ECE</option>
          <option value="me">Mechanical</option>
        </select>
      </p>
    </fieldset>

    <fieldset>
      <legend>Your opinion</legend>

      <p>Liked:
        <input type="checkbox" id="c1" name="liked" value="teaching"> <label for="c1">Teaching</label>
        <input type="checkbox" id="c2" name="liked" value="labs"> <label for="c2">Labs</label>
        <input type="checkbox" id="c3" name="liked" value="canteen"> <label for="c3">Canteen</label>
      </p>

      <p>
        <label for="msg">Comments:</label><br>
        <textarea id="msg" name="msg" rows="4" cols="40" maxlength="300"></textarea>
      </p>
    </fieldset>

    <button type="submit">Submit</button>
    <button type="reset">Clear</button>
  </form>
</body>
</html>
```

Because `action` points to a sample address, submitting will not work. In Module on server side you will connect a real server. For now, click Submit to see the browser check `required` fields.

### Real-world example

- The login box of any site, the search bar of Flipkart (a tiny GET form: the search word goes into the URL as `?q=...`).
- The passenger details form in IRCTC.
- The address form in Swiggy or Zomato.

### Common mistakes

- Missing `name` attribute: data is not sent.
- `label for` not matching the input `id`.
- Radio buttons with different `name`s (all can be selected).
- Using `get` for passwords (they appear in the address bar).

### Check your understanding

1. What is the job of `action` and `method`?
2. Difference between `get` and `post`?
3. Why do radio buttons in a group share the same `name`?
4. What happens when you click a `<label>` that is linked correctly?

---

## Topic 10. Internal linking

### Simple explanation

Internal linking means linking to a **spot inside the same page** (or a spot in another page). Two steps:

1. Give the target element an `id`: `<h2 id="contact">Contact</h2>`
2. Link to it with `#` and the id: `<a href="#contact">Go to contact</a>`

To link to a spot in another page: `<a href="about.html#team">Our team</a>`.
A link with just `#` (or `#top`) jumps to the top of the page.

(People also call links between your own pages "internal links", like `about.html`; the same idea with files.)

### Analogy

Like the **index page of a textbook**: "Chapter 4 on page 52". You jump straight to that place. Or like the **"Skip to platform 3" board** at a railway station: you do not walk through every platform.

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Internal Links</title>
  <style>
    section { height: 400px; border-bottom: 1px solid #ccc; padding: 10px; }
  </style>
</head>
<body id="top">
  <h1>Kerala Tourism Guide</h1>
  <nav>
    <a href="#munnar">Munnar</a> |
    <a href="#alleppey">Alleppey</a> |
    <a href="#kovalam">Kovalam</a>
  </nav>

  <section id="munnar">
    <h2>Munnar</h2>
    <p>Tea gardens and cool weather.</p>
    <a href="#top">Back to top</a>
  </section>

  <section id="alleppey">
    <h2>Alleppey</h2>
    <p>Backwaters and houseboats.</p>
    <a href="#top">Back to top</a>
  </section>

  <section id="kovalam">
    <h2>Kovalam</h2>
    <p>Beaches and lighthouse.</p>
    <a href="#top">Back to top</a>
  </section>
</body>
</html>
```

### Real-world example

- The "Table of contents" in Wikipedia.
- "Jump to FAQ" or "Back to top" buttons.
- Single-page websites where the top menu scrolls to "About", "Services" and "Contact" parts.

### Common mistakes

- Using the same `id` twice on a page. An id must be **unique**.
- Typing `href="contact"` instead of `href="#contact"`.
- Spaces or capital letter mismatch (`#Contact` is not `#contact`).

### Check your understanding

1. Write the two pieces of code needed to jump to a section called "fees".
2. Why must an `id` be unique?
3. How would you link to the `#team` section of `about.html`?

---

## Topic 11. Meta elements

### Simple explanation

`<meta>` tags go inside `<head>`. They give **information about the page** to the browser and search engines. They are not displayed. They are empty elements.

| Meta tag | Purpose |
|---|---|
| `<meta charset="UTF-8">` | Character encoding so all letters display properly |
| `<meta name="viewport" content="width=device-width, initial-scale=1.0">` | Mobile screen fit |
| `<meta name="description" content="...">` | Short summary shown in Google results |
| `<meta name="keywords" content="...">` | Keywords (old; search engines now mostly ignore it) |
| `<meta name="author" content="...">` | Page author |
| `<meta name="robots" content="noindex">` | Tell search engines not to list the page |
| `<meta http-equiv="refresh" content="5;url=home.html">` | Redirect after 5 seconds (use sparingly) |
| `<meta name="theme-color" content="#0a58ca">` | Colour of the browser bar on phones |

Other `head` children: `<title>`, `<link>` (CSS, icons), `<style>`, `<script>`, `<base>`.

### Analogy

Meta tags are like the **cover page of a file in a government office**: file number, subject, author, date. The clerk (search engine) reads the cover without opening the file.

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Official page of the CSE Minor programme, S5 batch.">
  <meta name="keywords" content="KTU, CSE minor, web development, HTML">
  <meta name="author" content="Dept of CSE">
  <meta name="theme-color" content="#0a58ca">
  <title>CSE Minor - Home</title>
  <link rel="icon" href="favicon.ico">
</head>
<body>
  <h1>Welcome to CSE Minor</h1>
  <p>View page source to see the meta tags. They are invisible here.</p>
</body>
</html>
```

### Real-world example

When you search "IRCTC" on Google, the grey sentence under the blue link comes from the `description` meta tag. When you share a link on WhatsApp and a small picture and title appear, it came from meta tags (Open Graph: `<meta property="og:title" ...>`).

### Common mistakes

- Putting `<meta>` inside `<body>`.
- Missing the viewport tag (page looks tiny on phones).
- Writing a very long or copied description.

### Check your understanding

1. Name three meta tags and what each does.
2. Where does the `description` text appear?
3. Which meta tag helps a page fit a phone screen?

---

## Topic 12. HTML5 form input types

### Simple explanation

The `<input>` tag changes its behaviour with the `type` attribute. HTML5 added many new types. They give you **free checking** and a **better keyboard on phones**.

| Type | What it gives you |
|---|---|
| `text` | Plain one-line text |
| `password` | Dots instead of letters |
| `email` | Checks for `@` and a dot; email keyboard on phone |
| `url` | Checks for a web address |
| `tel` | Phone keypad on mobile (no automatic check) |
| `number` | Only numbers; `min`, `max`, `step` |
| `range` | Slider |
| `date` | Calendar picker |
| `time` | Time picker |
| `datetime-local` | Date + time picker |
| `month`, `week` | Month / week picker |
| `color` | Colour chooser |
| `search` | Search box (often with a clear "x") |
| `file` | Choose a file to upload |
| `checkbox`, `radio` | Tick boxes / one-of-many |
| `hidden` | Invisible value sent with the form |
| `submit`, `reset`, `button` | Buttons |

Useful validation attributes: `required`, `min`, `max`, `minlength`, `maxlength`, `pattern` (a rule written as a regular expression), `placeholder`, `autofocus`.

### Analogy

Think of the **different boxes on a paper form**: a box with 10 small squares for a phone number, a tick box for gender, a calendar column for date of birth. Each box type guides you to fill the right kind of answer. HTML5 input types are the same: the type is the shape of the box.

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Input Types</title>
</head>
<body>
  <h1>Train Ticket Booking (practice)</h1>
  <form action="#" method="get">

    <p><label>Passenger name:
      <input type="text" name="pname" required minlength="3" placeholder="As on ID card"></label></p>

    <p><label>Email for ticket:
      <input type="email" name="email" required></label></p>

    <p><label>Mobile (10 digits):
      <input type="tel" name="mobile" pattern="[0-9]{10}" title="Enter exactly 10 digits" required></label></p>

    <p><label>Age:
      <input type="number" name="age" min="1" max="120" value="20"></label></p>

    <p><label>Journey date:
      <input type="date" name="jdate" required></label></p>

    <p><label>Preferred departure time:
      <input type="time" name="dtime"></label></p>

    <p><label>Seat comfort (1-10):
      <input type="range" name="comfort" min="1" max="10" value="5"></label></p>

    <p><label>Favourite colour of seat cover:
      <input type="color" name="clr" value="#0a58ca"></label></p>

    <p><label>Upload ID proof:
      <input type="file" name="idproof" accept=".jpg,.png,.pdf"></label></p>

    <p><label>Password:
      <input type="password" name="pw" minlength="8"></label></p>

    <p><label>Website (optional):
      <input type="url" name="site" placeholder="https://"></label></p>

    <input type="hidden" name="source" value="classroom-demo">

    <button type="submit">Book</button>
  </form>
</body>
</html>
```

Try it on a phone or in the browser's phone mode: the keyboard changes for `email`, `tel` and `number`. Click Book with a bad email to see the browser's own error message.

### Real-world example

- IRCTC and RedBus use a `date` picker for the journey date.
- Banking sites use `password` and `tel`.
- Flipkart's price filter slider is similar to `range`.
- Job portals use `file` for CV upload.

### Common mistakes

- Thinking browser validation is enough. Browser checks can be bypassed. The **server must check again**.
- Using `type="number"` for phone numbers or PIN codes (leading zeros disappear and the spinner arrows look odd). Use `tel` or `text` with `pattern`.
- Forgetting `name`.
- Assuming `date` looks the same in every browser (the style changes, the idea is the same).

### Check your understanding

1. Name six HTML5 input types and one use for each.
2. What does `pattern="[0-9]{10}"` mean?
3. Why should the server check the data again even when HTML does validation?
4. Which type is best for a PIN code and why?

---

## Topic 13. Input and datalist elements, and the autocomplete attribute

### Simple explanation

**`<datalist>`** gives an input box a **list of suggestions** as the user types. The user can still type something that is not in the list (unlike `<select>`). How to connect:

1. Make an input with `list="listName"`.
2. Make a `<datalist id="listName">` with `<option value="...">` items.

**`autocomplete` attribute** tells the browser whether it may **remember and auto-fill** the field using the user's saved details.

| Value | Meaning |
|---|---|
| `on` | Browser may suggest saved values |
| `off` | Do not suggest or remember (useful for one-time codes, sensitive data) |
| Specific tokens | Tell the browser what the field is: `name`, `email`, `tel`, `street-address`, `postal-code`, `username`, `current-password`, `new-password`, `one-time-code`, `cc-number` |

It can be put on the `<form>` (applies to all fields) or on one input.

Difference at a glance:

| | `datalist` | `autocomplete` |
|---|---|---|
| Who gives suggestions? | **You** (the developer) | The **browser** (from user's past entries) |
| Purpose | Help to choose a common value | Save typing for known personal details |

### Analogy

- **datalist** is the **tea shop owner** who, when you say "chaaya", shows you a board: "Plain, Ginger, Masala, Lemon?". You can pick one or ask for something else.
- **autocomplete** is the **shopkeeper who remembers you**: "Same as usual, Anu?" The browser remembers your name, address, phone.

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Datalist and Autocomplete</title>
</head>
<body>
  <h1>Bus Ticket (KSRTC style)</h1>

  <form action="#" method="post" autocomplete="on">

    <p>
      <label for="from">From:</label>
      <input list="stations" id="from" name="from" placeholder="Start typing..." autocomplete="off">
    </p>

    <p>
      <label for="to">To:</label>
      <input list="stations" id="to" name="to" placeholder="Start typing..." autocomplete="off">
    </p>

    <datalist id="stations">
      <option value="Thiruvananthapuram"></option>
      <option value="Kollam"></option>
      <option value="Kottayam"></option>
      <option value="Ernakulam"></option>
      <option value="Thrissur"></option>
      <option value="Palakkad"></option>
      <option value="Kozhikode"></option>
      <option value="Kannur"></option>
    </datalist>

    <hr>
    <h2>Passenger details (browser can auto-fill)</h2>

    <p>
      <label for="n">Name:</label>
      <input type="text" id="n" name="name" autocomplete="name">
    </p>
    <p>
      <label for="e">Email:</label>
      <input type="email" id="e" name="email" autocomplete="email">
    </p>
    <p>
      <label for="t">Mobile:</label>
      <input type="tel" id="t" name="phone" autocomplete="tel">
    </p>
    <p>
      <label for="pin">PIN code:</label>
      <input type="text" id="pin" name="pin" autocomplete="postal-code">
    </p>
    <p>
      <label for="otp">OTP:</label>
      <input type="text" id="otp" name="otp" autocomplete="one-time-code" inputmode="numeric">
    </p>
    <p>
      <label for="pw">New password:</label>
      <input type="password" id="pw" name="pw" autocomplete="new-password">
    </p>

    <button type="submit">Search buses</button>
  </form>
</body>
</html>
```

### Real-world example

- Station/city boxes on RedBus, IRCTC and MakeMyTrip suggest names as you type (they use JavaScript for richer behaviour, but `datalist` is the built-in simple version).
- Checkout pages on Flipkart and Swiggy auto-fill your name, phone and address using `autocomplete`.
- Banking sites set `autocomplete="off"` on OTP and card fields.

### Common mistakes

- `list="x"` not matching `<datalist id="x">`.
- Expecting `datalist` to *force* a choice (it does not; add `required` and check on the server if you need a strict value).
- Using `autocomplete="off"` on login password fields (it irritates users and password managers ignore it anyway).

### Check your understanding

1. How do you link an input to a datalist?
2. Difference between `<select>` and `<input list>`?
3. Give two cases where `autocomplete="off"` is sensible.
4. What do `autocomplete="email"` and `autocomplete="postal-code"` tell the browser?

---

## Topic 14. Page structure elements

### Simple explanation

Old pages used `<div>` for everything, so the browser could not tell the menu from the footer. HTML5 added **semantic** (meaningful) elements that name each part of a page.

| Element | Meaning |
|---|---|
| `<header>` | Top area: logo, site title, intro. Can also be the header of a section. |
| `<nav>` | Main navigation links (menu) |
| `<main>` | Main content of the page. Only **one** per page. |
| `<section>` | A themed group of content, usually with a heading |
| `<article>` | A self-contained piece that makes sense on its own (news story, blog post, product card) |
| `<aside>` | Side content (ads, related links, side notes) |
| `<footer>` | Bottom area: copyright, contacts, links |
| `<figure>`, `<figcaption>` | Image or diagram with a caption |
| `<address>` | Contact information |
| `<time datetime="2026-10-09">` | A date/time that machines can read |

Benefits: easier to read, better for **screen readers**, better for **search engines**, easier to style.

A typical page:

```text
+---------------------------------------+
| header (logo, title)                  |
+---------------------------------------+
| nav (Home | About | Contact)          |
+---------------------------+-----------+
| main                      | aside     |
|  section / article        | (side     |
|  section / article        |  links)   |
+---------------------------+-----------+
| footer (copyright)                    |
+---------------------------------------+
```

### Analogy

Think of a **newspaper or a college building**. The main gate with the name board is the `header`. The directory board is `nav`. The classrooms are `main`. A notice board on the side is `aside`. The office with address and phone is `footer`. Using `div` for all is like having a building with no signs on any door.

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Semantic Page</title>
</head>
<body>

  <header>
    <h1>Kerala Today</h1>
    <p>News from every district</p>
  </header>

  <nav>
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#">Sports</a></li>
      <li><a href="#">Business</a></li>
      <li><a href="#">Contact</a></li>
    </ul>
  </nav>

  <main>
    <section>
      <h2>Top Stories</h2>

      <article>
        <h3>Monsoon arrives early</h3>
        <p>Posted on <time datetime="2026-06-01">1 June 2026</time></p>
        <p>The southwest monsoon has reached Kerala coast three days early.</p>
      </article>

      <article>
        <h3>New metro line opens</h3>
        <p>Posted on <time datetime="2026-06-03">3 June 2026</time></p>
        <p>Commuters in Kochi get a new route from today.</p>
      </article>
    </section>

    <aside>
      <h2>Related links</h2>
      <ul>
        <li><a href="#">Weather report</a></li>
        <li><a href="#">Traffic update</a></li>
      </ul>
    </aside>
  </main>

  <footer>
    <p>&copy; 2026 Kerala Today</p>
    <address>Contact: <a href="mailto:news@example.com">news@example.com</a></address>
  </footer>

</body>
</html>
```

### Real-world example

News sites like The Hindu or Mathrubhumi: each story is an `article`, the "Trending" box on the side is an `aside`. Any college website has a `header` with the logo, a `nav` bar and a `footer` with address.

### Common mistakes

- Using `<section>` as a replacement for `<div>` everywhere. If there is no heading or theme, use `div`.
- More than one `<main>`.
- Putting `<nav>` around every group of links (use it for main menus only).
- Thinking these tags change the look. By default they do not; CSS makes them look different.

### Check your understanding

1. Why use `<header>` instead of `<div id="header">`?
2. Difference between `section` and `article`?
3. Draw a layout and label the semantic tag for each part.
4. How many `<main>` elements may a page have?

### Classroom activity (10 min): "Tag the college homepage"

Print or show a screenshot of your college's website. Students draw boxes and label each area with the correct HTML5 tag.

---

# PART B: CSS (Cascading Style Sheets)

---

## Topic 15. Introduction to CSS

### Simple explanation

CSS = **Cascading Style Sheets**. HTML says *what* things are. CSS says *how they look*: colour, font, size, spacing, position, layout.

Why a separate language?

- **Separation of concerns:** content in HTML, design in CSS.
- **One change, whole site:** change one line in one file and all 500 pages update.
- **Smaller pages, faster loading** (CSS file is saved once by the browser).
- **Different looks** for phone, laptop and print.

"Cascading" means that when many rules apply to the same element, there is a clear order of who wins (Topic 18).

### Analogy

HTML is the **bare building** (walls, doors, windows). CSS is **paint, curtains, tiles and furniture**. Without CSS the building works but looks plain. A person can repaint the whole building without rebuilding walls.

### Code example

The same HTML, before and after CSS.

Without CSS:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Before CSS</title>
</head>
<body>
  <h1>Chai Point</h1>
  <p>Fresh tea, every hour.</p>
</body>
</html>
```

With CSS (only a `<style>` block added):

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>After CSS</title>
  <style>
    body { font-family: Arial, sans-serif; background-color: #fff8e1; text-align: center; }
    h1   { color: #8d4004; font-size: 48px; }
    p    { color: #555; font-size: 20px; }
  </style>
</head>
<body>
  <h1>Chai Point</h1>
  <p>Fresh tea, every hour.</p>
</body>
</html>
```

### Real-world example

A site like Zomato changes the entire look (dark mode) by switching a few CSS rules. Festival themes (Onam special banners on Flipkart) are done mostly by changing CSS and images, not rewriting HTML.

### Common mistakes

- Using HTML tags only for looks (`<font>`, `<center>` are old and removed).
- Thinking CSS can create content. It only styles it (with rare exceptions).

### Check your understanding

1. What does CSS stand for? What is its job?
2. Give three advantages of keeping CSS separate from HTML.
3. What does "cascading" mean?

---

## Topic 16. Basic syntax and structure

### Simple explanation

A CSS rule has two parts: a **selector** (who to style) and a **declaration block** (what to do) in curly braces. Each declaration is `property: value;`.

```text
selector {
    property: value;
    property: value;
}
```

Example:

```css
h1 {
  color: blue;
  font-size: 32px;
}
```

- `h1` = selector (all level-1 headings).
- `color` = property; `blue` = value.
- The semicolon ends each declaration. The braces hold the block.

Comments: `/* this is a comment */`.

Common value types:

| Type | Examples |
|---|---|
| Colour | `red`, `#ff0000`, `rgb(255,0,0)`, `rgba(255,0,0,0.5)`, `hsl(0,100%,50%)` |
| Length | `px`, `em`, `rem`, `%`, `vw`, `vh` |
| Keywords | `bold`, `center`, `none`, `solid` |
| URL | `url("image.jpg")` |

**Units quick guide:** `px` = fixed pixels. `%` = percent of parent. `em` = relative to the element's font size. `rem` = relative to the root (page) font size. `vw`/`vh` = 1% of window width/height.

Grouping selectors: `h1, h2, h3 { color: navy; }`.

### Analogy

A CSS rule is like a **sentence in an instruction**: "For all *tea cups* (selector): make *colour* (property) *white* (value)". Each rule is a small order to the painter.

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>CSS Syntax</title>
  <style>
    /* one selector, many declarations */
    h1 {
      color: #0a58ca;           /* hex colour */
      font-size: 2rem;
      text-align: center;
    }

    /* grouped selectors */
    h2, h3 {
      color: rgb(180, 0, 90);   /* rgb colour */
      font-family: Georgia, serif;
    }

    p {
      color: #333;
      line-height: 1.6;         /* space between lines */
      font-size: 18px;
    }
  </style>
</head>
<body>
  <h1>CSS Syntax</h1>
  <h2>A subheading</h2>
  <h3>Another subheading</h3>
  <p>The same rule styles every paragraph on this page.</p>
  <p>This is a second paragraph, styled by the same rule.</p>
</body>
</html>
```

### Real-world example

Open any website, press F12 and select an element. The right-hand "Styles" panel lists CSS rules in exactly this selector-and-declarations shape.

### Common mistakes

- Missing semicolon (the next line stops working).
- Using `=` instead of `:`.
- Missing closing brace `}` (all rules below break).
- Spelling: `colour` is wrong, CSS uses American `color`.
- Missing unit: `font-size: 20;` is invalid. Write `20px`. (Only `0` can be unitless.)

### Check your understanding

1. Name the parts of a CSS rule.
2. What is the difference between `em`, `rem` and `px`?
3. Find the error: `p { color red; font-size: 20 }`.

---

## Topic 17. Inline styles, embedded style sheets and linking external style sheets

### Simple explanation

There are **three ways** to add CSS to HTML.

**1. Inline style.** Use the `style` attribute on one element. Affects only that element.

```html
<p style="color: red; font-size: 20px;">Red text</p>
```

**2. Embedded (internal) style sheet.** Put a `<style>` block inside `<head>`. Affects the whole page, but only that page.

```html
<head>
  <style>
    p { color: green; }
  </style>
</head>
```

**3. External style sheet.** Write CSS in a separate `.css` file, then link it with `<link>` in `<head>`. One file can style the whole website.

```html
<head>
  <link rel="stylesheet" href="style.css">
</head>
```

(Old method `@import url("style.css");` inside `<style>` also exists but `<link>` is faster and preferred.)

#### Difference between internal (embedded) and external style sheets

| Point | Internal / embedded | External |
|---|---|---|
| Where written | In `<style>` inside `<head>` of the same page | In a separate `.css` file |
| How attached | Directly in the HTML file | `<link rel="stylesheet" href="file.css">` |
| Scope | Only that one page | Any number of pages |
| Change effect | Must edit each page | Edit once, all pages change |
| Loading | CSS downloaded again with every page | File is downloaded once and **cached** (remembered) |
| Best for | Single page, quick test, email templates | Real websites |

Where does inline fit? Inline is the most local and hardest to maintain. Use it rarely (for example for a one-off value set by JavaScript).

### Analogy

- **Inline:** telling the barber about **one haircut for one person**: "this one, short sides".
- **Embedded:** a **notice on one classroom wall**: "all students wear ID in this room".
- **External:** a **college rule book** that every department follows. Change the rule book once and the whole college follows.

### Code example

Folder:

```text
module1/
  index.html
  contact.html
  style.css
```

`style.css`:

```css
/* style.css - shared by all pages */
body {
  font-family: Arial, sans-serif;
  background-color: #f4f6f8;
  margin: 0;
  padding: 20px;
}
h1 {
  color: #0a58ca;
}
.note {
  background-color: #fff3cd;
  padding: 10px;
}
```

`index.html` (uses all three ways):

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Three Ways of CSS</title>

  <!-- 1. External: shared by every page -->
  <link rel="stylesheet" href="style.css">

  <!-- 2. Embedded: only this page -->
  <style>
    p { color: #333; }
    .special { color: green; }
  </style>
</head>
<body>
  <h1>Three Ways of Adding CSS</h1>

  <p>This paragraph gets colour from the embedded sheet.</p>
  <p class="note">This paragraph gets a yellow box from the external file.</p>

  <!-- 3. Inline: only this element -->
  <p style="color: crimson; font-weight: bold;">This one uses an inline style.</p>

  <p><a href="contact.html">Go to contact page (same external CSS applies)</a></p>
</body>
</html>
```

`contact.html`:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Contact</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Contact</h1>
  <p class="note">The heading colour and yellow note come from style.css. No style written here.</p>
  <p><a href="index.html">Back</a></p>
</body>
</html>
```

Student task: change `h1` colour in `style.css` to red. Reload both pages. Both change. That is the power of external CSS.

### Real-world example

Large sites (IRCTC, Amazon, college portals) have one or a few `.css` files linked on every page, so the look stays the same on all pages. Inline styles are common in HTML emails (Gmail ignores `<style>` in some cases).

### Common mistakes

- Wrong `href` path to the CSS (page shows no styling).
- Forgetting `rel="stylesheet"`.
- Putting `<link>` in `<body>`.
- Writing `<style>` tags inside the `.css` file. The `.css` file has only CSS, no HTML tags.
- Writing inline styles with braces: `style="{color:red}"` is wrong.

### Check your understanding

1. Explain the difference between internal and external style sheets with examples. (Model answer in the Question bank.)
2. Which method is best for a 50-page website and why?
3. Write the tag that links `site.css` to a page.
4. What is the syntax difference between an inline style and an embedded rule?

---

## Topic 18. Conflict resolution: cascade, specificity, importance and source order

### Simple explanation

Often two or more rules try to style the same element in different ways. Example: one rule says `p` is red, another says green. The browser must choose. The choice follows the **cascade**, using these steps in order:

**Step 1. Importance (and origin).**
A declaration marked `!important` beats normal ones. For this course: normal declaration < `!important`. (Browser default styles are weaker than your styles.)

**Step 2. Specificity.** How *specific* is the selector? More specific wins.

| Selector kind | Score (think of it as a 4-digit number) |
|---|---|
| Inline style (`style="..."`) | 1,0,0,0 |
| ID selector (`#menu`) | 0,1,0,0 |
| Class `.card`, attribute `[type="text"]`, pseudo-class `:hover` | 0,0,1,0 |
| Element `p`, pseudo-element `::before` | 0,0,0,1 |
| Universal `*`, combinators (`>`, `+`, space) | 0,0,0,0 |

Compare from left to right. One ID beats any number of classes. One class beats any number of element names.

Examples:

| Selector | Score |
|---|---|
| `p` | 0,0,0,1 |
| `.note` | 0,0,1,0 |
| `p.note` | 0,0,1,1 |
| `#intro` | 0,1,0,0 |
| `div #intro p` | 0,1,0,2 |
| `ul li a:hover` | 0,0,1,3 |

**Step 3. Source order.** If importance and specificity are equal, the rule that comes **last** wins. (For several style sheets, the later one linked wins; embedded `<style>` after `<link>` beats the link.)

**Inheritance (related idea).** Some properties (like `color`, `font-family`) pass from parent to children. A rule written directly on the child always beats an inherited value, even if the inherited one came from a very specific rule.

**Summary order:**

```text
!important  >  inline style  >  ID  >  class/attribute/pseudo-class  >  element  >  inherited
(when scores tie, the LAST written rule wins)
```

**How to resolve a conflict in a real page (answer to the exam scenario):**

1. Open developer tools (F12) and look at the Styles panel. Struck-through lines are the losers.
2. Find which rules are competing for the same property.
3. Compare importance, then specificity, then source order.
4. Fix by: making the selector more specific (add a class or parent), moving the rule later in the file, or removing duplicate rules. Use `!important` only as the last option.
5. Keep CSS tidy: prefer classes, avoid IDs for styling, avoid inline styles, do not nest selectors too deep.

### Analogy

A **tug of war between three officers giving orders** to a clerk:

1. A **court order** (`!important`) beats everyone.
2. Otherwise, whoever has the **higher rank** wins (inline > ID > class > element). Specificity is rank.
3. If two officers have the **same rank**, the **latest order** is followed (source order).

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Who Wins?</title>
  <style>
    /* Rule A: element selector, score 0,0,0,1 */
    p { color: red; }

    /* Rule B: same score as A but written later, so B beats A */
    p { color: green; }

    /* Rule C: class, score 0,0,1,0 beats element rules */
    .info { color: blue; }

    /* Rule D: ID, score 0,1,0,0 beats class */
    #special { color: orange; }

    /* Rule E: !important beats even an inline style */
    .force { color: purple !important; }
  </style>
</head>
<body>
  <p>1. Plain paragraph. Result: GREEN (later rule beats earlier rule).</p>

  <p class="info">2. Class paragraph. Result: BLUE (class beats element).</p>

  <p class="info" id="special">3. Class and ID. Result: ORANGE (ID beats class).</p>

  <p class="info" id="special" style="color: black;">4. Plus inline style. Result: BLACK (inline beats ID).</p>

  <p class="force" id="special" style="color: black;">5. With !important. Result: PURPLE (!important beats inline).</p>

  <div style="color: teal;">
    <p>6. Child paragraph. Result: GREEN. The rule written on the p itself beats the colour inherited from the div.</p>
    <span>7. A span has no rule of its own, so it inherits TEAL from the div.</span>
  </div>
</body>
</html>
```

Ask students to predict each colour *before* opening the page. Then check.

### Real-world example

When you add Bootstrap (a ready-made style library) to a site and your own button colour does not apply, it is a specificity problem. Developers solve it by writing a more specific selector or loading their CSS after Bootstrap. Many bug-fixing hours in real projects go into this.

### Common mistakes

- Overusing `!important`. Then the next developer needs another `!important` to beat it, and so on.
- Thinking the **order of classes in the HTML** (`class="a b"`) matters. It does not. Order in the CSS file matters.
- Editing a rule and not seeing a change because a more specific rule is winning.
- Believing that "later always wins". It wins only when specificity is equal.

### Check your understanding

1. State the order in which the browser resolves conflicting rules.
2. Calculate the specificity of `#nav ul li.active a`.
3. Rule 1: `.box p { color: red; }`, Rule 2: `p.big { color: blue; }`. Which wins for `<div class="box"><p class="big">`? (Hint: work out both scores. They are equal, so source order decides: Rule 2 wins because it is written later.)
4. When is `!important` acceptable?

### Classroom activity (10 min): "Who wins?" card game

Give each group cards with selectors (`p`, `.a`, `#b`, `p.a`, inline, `!important`). Two cards are flipped. Groups shout which one wins and why. Score a point for each correct reason.

---

## Topic 19. Exploring CSS selectors

### Simple explanation

A selector picks **which elements** a rule applies to.

| Selector | Example | Picks |
|---|---|---|
| Universal | `*` | every element |
| Element (type) | `p` | all `<p>` |
| Class | `.note` | all elements with `class="note"` (many allowed) |
| ID | `#logo` | the one element with `id="logo"` |
| Group | `h1, h2` | all h1 and all h2 |
| Descendant | `nav a` | `a` anywhere inside `nav` |
| Child | `ul > li` | `li` that is a **direct** child of `ul` |
| Adjacent sibling | `h2 + p` | the `p` right after an `h2` |
| General sibling | `h2 ~ p` | all `p` after an `h2` (same parent) |
| Attribute | `input[type="email"]` | inputs of type email |
| Attribute begins with | `a[href^="https"]` | links starting with https |
| Attribute ends with | `a[href$=".pdf"]` | links ending with .pdf |
| Pseudo-class | `a:hover`, `li:first-child`, `li:nth-child(odd)`, `input:focus`, `input:required` | elements in a certain state/position |
| Pseudo-element | `p::first-line`, `p::first-letter`, `li::before` | a part of an element |

An element can have several classes: `class="btn btn-big"`.

### Analogy

Selectors are like **ways of calling out in a classroom**: "Everyone" (`*`), "All girls" (element), "Everyone wearing a red band" (class), "Roll number 21" (ID), "Anyone sitting inside the second row" (descendant), "The student sitting right after Anu" (sibling).

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Selectors</title>
  <style>
    * { font-family: Arial, sans-serif; }

    /* element */
    h1 { color: #0a58ca; }

    /* class */
    .highlight { background-color: yellow; }

    /* ID */
    #brand { font-size: 28px; font-weight: bold; }

    /* group */
    h2, h3 { color: #6a1b9a; }

    /* descendant: only links inside nav */
    nav a { color: #222; text-decoration: none; margin-right: 12px; }

    /* child: only direct li of .menu */
    .menu > li { list-style: square; }

    /* adjacent sibling: paragraph straight after an h2 */
    h2 + p { font-style: italic; }

    /* attribute */
    input[type="text"] { border: 2px solid #0a58ca; }
    a[href$=".pdf"] { color: crimson; }

    /* pseudo-classes */
    a:hover { text-decoration: underline; color: orangered; }
    li:nth-child(odd) { background-color: #eef; }
    input:focus { outline: 3px solid orange; }

    /* pseudo-elements */
    p::first-letter { font-size: 150%; color: darkgreen; }
    .price::before { content: "Rs. "; }
  </style>
</head>
<body>
  <h1 id="brand">College Portal</h1>

  <nav>
    <a href="#">Home</a>
    <a href="#">Notes</a>
    <a href="syllabus.pdf">Syllabus (PDF)</a>
  </nav>

  <h2>Notices</h2>
  <p>This paragraph follows an h2, so it is italic.</p>
  <p class="highlight">This paragraph is highlighted by a class.</p>

  <ul class="menu">
    <li>First</li>
    <li>Second</li>
    <li>Third</li>
  </ul>

  <p>Fee: <span class="price">500</span></p>

  <form>
    <input type="text" placeholder="Click me (focus style)">
  </form>
</body>
</html>
```

### Real-world example

- The "hover" effect when you move your mouse on a Flipkart product card is `:hover`.
- Zebra-striped (alternate coloured) rows in a results table are `tr:nth-child(even)`.
- Marking invalid form fields in red uses `input:invalid`.

### Common mistakes

- Using `.` for an ID or `#` for a class.
- Space matters: `.a .b` (b inside a) is not the same as `.a.b` (one element with both classes).
- Using the same `id` on many elements.
- Making selectors too long (hard to override).

### Check your understanding

1. Difference between class and ID selectors?
2. What is the difference between `div p` and `div > p`?
3. Write a selector for every link that ends with `.pdf`.
4. What does `li:nth-child(even)` select?

---

## Topic 20. Properties and values

### Simple explanation

A **property** is the thing you want to change (colour, size, font). A **value** is what you want to set it to. Here are the groups you will use most.

**Text and font**

| Property | Example values |
|---|---|
| `color` | `red`, `#333` |
| `font-family` | `Arial, sans-serif` |
| `font-size` | `16px`, `1.2rem` |
| `font-weight` | `normal`, `bold`, `700` |
| `font-style` | `italic` |
| `text-align` | `left`, `center`, `right`, `justify` |
| `text-decoration` | `none`, `underline`, `line-through` |
| `text-transform` | `uppercase`, `capitalize` |
| `line-height` | `1.5` |
| `letter-spacing` | `2px` |

**Box and look**

| Property | Example values |
|---|---|
| `width`, `height` | `200px`, `50%` |
| `margin`, `padding` | `10px`, `10px 20px` |
| `border` | `2px solid black` |
| `border-radius` | `8px`, `50%` (circle) |
| `background-color` | `#eee` |
| `box-shadow` | `2px 2px 6px gray` |
| `opacity` | `0` to `1` |
| `display` | `block`, `inline`, `inline-block`, `none`, `flex` |
| `cursor` | `pointer` |

**Shorthand.** Several properties in one line. Example: `border: 2px solid red;` = width + style + colour. `margin: 10px 20px 30px 40px;` goes top, right, bottom, left (clockwise, "TRouBLe"). `margin: 10px 20px;` = top/bottom 10, left/right 20.

**Other useful ideas:**

- **Inheritance.** `color`, `font-*`, `text-align`, `line-height` pass down to children. `margin`, `padding`, `border`, `background` do not.
- **Keyword values:** `inherit`, `initial`.
- **Colour formats:** name, hex, `rgb()`, `rgba()` (with transparency), `hsl()`.

### Analogy

Think of ordering a **custom T-shirt**. The property is the field on the order form ("Colour", "Size", "Text on front"). The value is what you write in the field ("Navy", "L", "Kerala Boy"). Shorthand is like ticking a combo pack.

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Properties and Values</title>
  <style>
    body {
      font-family: "Segoe UI", Arial, sans-serif;
      background-color: #f0f4f8;
      color: #222;
    }

    .card {
      width: 320px;
      margin: 30px auto;               /* centre the card horizontally */
      padding: 20px;
      background-color: white;
      border: 1px solid #ccc;
      border-radius: 12px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);
    }

    .card h2 {
      margin-top: 0;
      color: #d32f2f;
      text-transform: uppercase;
      letter-spacing: 1px;
    }

    .card p {
      line-height: 1.6;
      text-align: justify;
    }

    .price {
      font-size: 1.5rem;
      font-weight: bold;
      color: #2e7d32;
    }

    .btn {
      display: inline-block;
      padding: 10px 18px;
      background-color: #fc8019;       /* Swiggy-like orange */
      color: white;
      text-decoration: none;
      border-radius: 6px;
      cursor: pointer;
    }
    .btn:hover { background-color: #d96a0b; }
  </style>
</head>
<body>
  <div class="card">
    <h2>Masala Dosa</h2>
    <p>Crisp dosa filled with spiced potato, served with sambar and coconut chutney.</p>
    <p class="price">Rs. 80</p>
    <a class="btn" href="#">Add to cart</a>
  </div>
</body>
</html>
```

### Real-world example

A Swiggy or Zomato food card is exactly this: rounded corners, light shadow, price in bold colour, and a button that changes colour on hover.

### Common mistakes

- Writing `font-color` (no such property; use `color`).
- Writing `background: red` and expecting only the colour to change: `background` is a shorthand that also **resets** image, repeat, etc. Use `background-color` when you only mean the colour.
- Using `margin: 0 auto` on an inline element (it only centres block elements that have a width).
- Remembering the clockwise order wrongly.

### Check your understanding

1. What does `margin: 5px 10px 15px 20px;` mean?
2. Which properties are inherited and which are not? Give two of each.
3. Write CSS to make a paragraph bold, italic, red and centred.

---

## Topic 21. Positioning elements: relative and absolute

### Simple explanation

By default elements sit in **normal flow**: block elements go top to bottom, inline ones go left to right. The `position` property changes this.

| Value | Behaviour |
|---|---|
| `static` | Default. Normal flow. `top/left` do nothing. |
| `relative` | Stays in normal flow (keeps its space), but you can **nudge** it from where it would normally be using `top`, `left`, `right`, `bottom`. It also becomes the **reference box** for absolute children. |
| `absolute` | **Removed from normal flow** (others behave as if it is not there). Placed using `top/left/right/bottom` measured from the nearest ancestor that is **positioned** (not `static`). If none, from the page (the `html` area). |
| `fixed` | Like absolute but measured from the browser window; stays in place when scrolling (sticky menus). |
| `sticky` | Normal flow until you scroll to it, then sticks like fixed. |

Related: `z-index` decides which overlapping element is on top (higher number on top; works on positioned elements).

The golden pattern:

```css
.parent { position: relative; }          /* the reference */
.child  { position: absolute; top: 10px; right: 10px; }  /* placed inside the parent's corner */
```

### Analogy

- **Relative:** you are standing in a queue at the ticket counter and **take two steps right**. Your original place is still counted in the queue.
- **Absolute:** you **leave the queue** and go stand at "2 metres from the left wall of the room". The queue closes the gap as if you were never there. If the room (parent) has been marked as the reference ("relative"), the distance is measured from that room's wall.
- **Fixed:** the **CCTV camera on the wall**. It stays at the same spot even if the crowd moves.

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Positioning</title>
  <style>
    body { font-family: Arial, sans-serif; }

    .box { width: 120px; height: 60px; color: white; padding: 8px; }

    .a { background: steelblue; }
    .b { background: tomato; position: relative; top: 20px; left: 40px; } /* nudged, space kept */
    .c { background: seagreen; }

    /* Badge on a product card */
    .product {
      position: relative;            /* reference for the badge */
      width: 220px;
      height: 160px;
      margin-top: 40px;
      border: 2px solid #999;
      background: #fafafa;
      padding: 10px;
    }
    .badge {
      position: absolute;            /* placed inside the card */
      top: 8px;
      right: 8px;
      background: crimson;
      color: white;
      padding: 4px 8px;
      border-radius: 4px;
      font-size: 14px;
    }

    /* Fixed "Chat" button */
    .chat {
      position: fixed;
      bottom: 16px;
      right: 16px;
      background: #25d366;           /* WhatsApp green */
      color: white;
      padding: 12px 16px;
      border-radius: 30px;
    }
  </style>
</head>
<body>
  <h2>Relative</h2>
  <div class="box a">A: normal</div>
  <div class="box b">B: relative, moved</div>
  <div class="box c">C: normal (sits below B's ORIGINAL spot)</div>

  <h2>Absolute inside relative</h2>
  <div class="product">
    <span class="badge">30% OFF</span>
    <p>Wireless Earphones</p>
  </div>

  <div style="height: 800px;">Scroll down to see the fixed button stay. (Extra height for scrolling.)</div>

  <div class="chat">Chat with us</div>
</body>
</html>
```

### Real-world example

- The "20% OFF" badge on a Flipkart product image: `absolute` inside a `relative` card.
- The green WhatsApp chat button at the bottom-right of many business sites: `fixed`.
- A navigation bar that stays at the top while you scroll: `fixed` or `sticky`.
- The red notification count on top of an icon: `absolute`.

### Common mistakes

- Using `absolute` for the whole page layout (breaks on different screen sizes). Use it only for small overlays and badges.
- Forgetting `position: relative` on the parent, so the badge jumps to a corner of the whole page.
- Thinking `relative` removes the original space (it does not).
- Overlapping elements without `z-index`.

### Check your understanding

1. Difference between relative and absolute positioning?
2. In `position: absolute`, from what is `top` measured?
3. How do you place a badge in the top-right corner of a card?
4. Which position value keeps an element visible while scrolling?

---

## Topic 22. Backgrounds

### Simple explanation

| Property | Use |
|---|---|
| `background-color` | Solid colour |
| `background-image` | Picture: `url("pic.jpg")` or a gradient |
| `background-repeat` | `repeat` (default), `no-repeat`, `repeat-x`, `repeat-y` |
| `background-position` | `center`, `top right`, `50% 50%` |
| `background-size` | `auto`, `cover` (fill, may crop), `contain` (fit fully), `100px 50px` |
| `background-attachment` | `scroll` (default), `fixed` (parallax feel) |
| `background` | Shorthand for all of the above |

Gradient backgrounds need no image file:

```css
background: linear-gradient(to right, #ff7e5f, #feb47b);
```

Multiple backgrounds are allowed (comma separated). To keep text readable on a photo, put a dark transparent layer with `rgba()`.

### Analogy

The background is the **wall paint and poster behind a shop counter**. You can paint it a plain colour (`background-color`), stick one big poster (`no-repeat`, `cover`) or paste small stickers over and over like a wallpaper (`repeat`).

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Backgrounds</title>
  <style>
    body { margin: 0; font-family: Arial, sans-serif; }

    .hero {
      height: 260px;
      /* Use a real image file here. A gradient is the fallback layer under it. */
      background-color: #0a58ca;
      background-image: linear-gradient(135deg, #0a58ca, #6610f2);
      color: white;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 2rem;
    }

    .photo {
      height: 260px;
      background-image: url("campus.jpg");   /* put campus.jpg in the same folder */
      background-size: cover;
      background-position: center;
      background-repeat: no-repeat;
      background-color: #888;                /* shown if image is missing */
      color: white;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 2rem;
    }

    .photo span {
      background-color: rgba(0, 0, 0, 0.55); /* dark see-through layer for readable text */
      padding: 10px 20px;
      border-radius: 8px;
    }

    .stripes {
      height: 120px;
      background: repeating-linear-gradient(45deg, #ffe082, #ffe082 10px, #ffd54f 10px, #ffd54f 20px);
    }
  </style>
</head>
<body>
  <div class="hero">Gradient background</div>
  <div class="photo"><span>Photo background with cover</span></div>
  <div class="stripes"></div>
</body>
</html>
```

### Real-world example

- The big banner at the top of the Swiggy, BookMyShow or a college homepage is a CSS background image with text over it.
- Login pages with a full-screen photo behind the login card.
- Gradient buttons in modern apps.

### Common mistakes

- Wrong image path: the area stays plain.
- Using a background image and forgetting to set `height` (the element has no height, so no picture is seen).
- Text with poor contrast (white text on a light photo).
- Using background images for important content (screen readers cannot read it). Use `<img>` for that.

### Check your understanding

1. What is the difference between `cover` and `contain`?
2. How do you stop a background image from repeating?
3. Write CSS for a page background that is a left-to-right gradient from green to white.

---

## Topic 23. List styles

### Simple explanation

| Property | Use |
|---|---|
| `list-style-type` | Marker shape: `disc`, `circle`, `square`, `decimal`, `lower-alpha`, `upper-roman`, `none` |
| `list-style-image` | Your own small picture as marker: `url("tick.png")` |
| `list-style-position` | `outside` (default) or `inside` the text box |
| `list-style` | Shorthand |

Common trick: remove bullets with `list-style: none; padding: 0; margin: 0;` and turn a list into a **menu bar** with `display: inline-block` or `display: flex` on `li`.

### Analogy

List styles are like choosing the **bullet style in a Word document**: round dots, squares, numbers, or ticks. The `none` choice with horizontal layout is like a **line of tabs** on a file folder.

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>List Styles</title>
  <style>
    body { font-family: Arial, sans-serif; }

    ul.square  { list-style-type: square; }
    ul.circle  { list-style-type: circle; }
    ol.roman   { list-style-type: upper-roman; }
    ol.alpha   { list-style: lower-alpha inside; }
    ul.tick    { list-style-type: "\2713  "; }     /* a tick mark as marker */

    /* Menu bar from a list */
    nav ul {
      list-style: none;
      margin: 0;
      padding: 0;
      background-color: #0a58ca;
      display: flex;
    }
    nav li a {
      display: block;
      color: white;
      text-decoration: none;
      padding: 14px 20px;
    }
    nav li a:hover { background-color: #084298; }
  </style>
</head>
<body>
  <nav>
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#">Courses</a></li>
      <li><a href="#">Results</a></li>
      <li><a href="#">Contact</a></li>
    </ul>
  </nav>

  <h3>Square bullets</h3>
  <ul class="square"><li>Idli</li><li>Dosa</li><li>Puttu</li></ul>

  <h3>Circle bullets</h3>
  <ul class="circle"><li>Tea</li><li>Coffee</li></ul>

  <h3>Roman numbers</h3>
  <ol class="roman"><li>Module 1</li><li>Module 2</li><li>Module 3</li></ol>

  <h3>Letters inside</h3>
  <ol class="alpha"><li>Option one</li><li>Option two</li></ol>

  <h3>Tick marks</h3>
  <ul class="tick"><li>Clean code</li><li>Tested code</li></ul>
</body>
</html>
```

### Real-world example

Every website menu is a styled list. The "highlights" on a product page (with small ticks) are lists with a custom marker. Footer link columns on Amazon are lists with bullets removed.

### Common mistakes

- Removing bullets but leaving the left padding (menu looks pushed right).
- Using `<br>` and images instead of a real list.
- Putting `list-style` on `<li>` links that are `display: flex` (marker disappears in some cases; apply to `ul`).

### Check your understanding

1. Which property changes bullets to squares?
2. How do you remove bullets from a list?
3. Make a horizontal menu from a `ul`. Which property helps?

---

## Topic 24. Element dimensions

### Simple explanation

**Dimensions** = size of an element: `width`, `height`, and limits `min-width`, `max-width`, `min-height`, `max-height`.

- Block elements by default take the **full width** of the parent and **height of their content**.
- Inline elements (`span`, `a`) **ignore** `width` and `height`.
- Units: `px` (fixed), `%` (of parent), `vw/vh` (of window), `em/rem` (of font size), `auto` (browser decides).
- **`max-width`** is the secret of simple responsive design: `img { max-width: 100%; height: auto; }` shrinks big images to fit small screens.
- **`box-sizing`**: by default, `width` means *content only*; padding and border add on top. With `box-sizing: border-box`, `width` includes padding and border (easier maths). Many developers start with:

```css
* { box-sizing: border-box; }
```

- **`overflow`** controls content that is bigger than the box: `visible` (default), `hidden`, `scroll`, `auto`.

### Analogy

Think of **plastic boxes (dabbas)** in a kitchen. `width` and `height` are the size of the dabba. `max-width` is "this dabba will never be bigger than 20 cm even if you have more rice". `overflow: hidden` is "extra rice is cut off", `overflow: auto` is "give me a bigger lid with a scroll".

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Dimensions</title>
  <style>
    * { box-sizing: border-box; }
    body { font-family: Arial, sans-serif; }

    .fixed   { width: 300px; height: 80px;  background: #cfe8ff; margin-bottom: 10px; }
    .percent { width: 50%;   height: 80px;  background: #ffd6d6; margin-bottom: 10px; }
    .limit   { width: 100%; max-width: 400px; min-height: 80px; background: #d6ffd8; margin-bottom: 10px; }

    .scroller {
      width: 250px;
      height: 70px;
      overflow: auto;          /* try hidden, scroll, visible */
      border: 2px solid #333;
    }

    img.fluid { max-width: 100%; height: auto; }

    span.try { width: 200px; height: 100px; background: yellow; } /* ignored: inline */
    span.ok  { display: inline-block; width: 200px; height: 40px; background: orange; }
  </style>
</head>
<body>
  <div class="fixed">Fixed: 300px wide</div>
  <div class="percent">50% of the parent's width</div>
  <div class="limit">100% wide but never above 400px. Resize the window to see.</div>

  <div class="scroller">
    This box is small but the text is long. Because overflow is auto, a scrollbar appears so nothing is lost.
    Keep writing more text here so it overflows the small box and you can see the scrollbar clearly.
  </div>

  <p><span class="try">Inline span: width and height ignored</span></p>
  <p><span class="ok">inline-block: respects size</span></p>
</body>
</html>
```

### Real-world example

- Product images on Flipkart shrink on a phone because of `max-width: 100%`.
- A chat window in WhatsApp Web has a fixed height and `overflow: auto`, so messages scroll inside it.
- Article text is kept to `max-width: 700px` so lines are easy to read on a wide monitor.

### Common mistakes

- Setting a fixed `height` on a box with text. Text overflows when the screen gets narrow. Prefer `min-height`.
- Setting both `width` and `height` on an image with a different ratio (picture gets squashed).
- Forgetting `box-sizing: border-box`: `width: 100%` plus padding becomes wider than the screen and creates sideways scroll.
- Expecting `width` to work on `<span>`.

### Check your understanding

1. What is the effect of `max-width: 100%` on an image?
2. What does `box-sizing: border-box` change?
3. List the four values of `overflow` and what each does.
4. Why does `width` not work on `span`?

---

## Topic 25. Table layouts

### Simple explanation

Plain tables are ugly. CSS makes them neat.

| Property | Use |
|---|---|
| `border` on `table`, `th`, `td` | Lines |
| `border-collapse: collapse` | Merges double borders into one line (almost always wanted) |
| `border-spacing` | Gap between cells (when not collapsed) |
| `padding` on `th`, `td` | Space inside cells |
| `text-align`, `vertical-align` | Alignment inside cells |
| `width: 100%` | Full-width table |
| `table-layout: fixed` or `auto` | `auto` = column widths follow content (default). `fixed` = widths follow the first row and `width`, **faster and more predictable**. |
| `caption-side` | Caption top or bottom |
| `tr:nth-child(even)` | Zebra stripes |
| `tr:hover` | Highlight row on hover |
| `overflow-x: auto` on a wrapper `div` | Lets a wide table scroll sideways on phones |

### Analogy

Think of **ruled graph paper**. A plain table is a loose set of boxes. `border-collapse` draws one clean line between boxes instead of two. `table-layout: fixed` is like the printed paper with **fixed column widths**: no matter what you write, the columns stay as printed.

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Table Styling</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 16px; }

    .table-wrap { overflow-x: auto; }       /* sideways scroll on small screens */

    table {
      width: 100%;
      border-collapse: collapse;            /* one line between cells */
      table-layout: fixed;                  /* equal and predictable columns */
    }

    caption {
      caption-side: top;
      font-weight: bold;
      font-size: 1.2rem;
      padding: 8px;
    }

    th, td {
      border: 1px solid #bbb;
      padding: 10px;
      text-align: left;
    }

    th {
      background-color: #0a58ca;
      color: white;
    }

    tbody tr:nth-child(even) { background-color: #f2f6ff; }   /* zebra */
    tbody tr:hover           { background-color: #ffe9b3; }   /* hover highlight */

    td.num, th.num { text-align: right; }
    .pass { color: #2e7d32; font-weight: bold; }
    .fail { color: #c62828; font-weight: bold; }
  </style>
</head>
<body>
  <div class="table-wrap">
    <table>
      <caption>Internal Marks - S5 CSE Minor</caption>
      <thead>
        <tr><th>Roll No</th><th>Name</th><th class="num">Marks (50)</th><th>Result</th></tr>
      </thead>
      <tbody>
        <tr><td>21</td><td>Anu Mathew</td><td class="num">44</td><td class="pass">Pass</td></tr>
        <tr><td>22</td><td>Rahul Nair</td><td class="num">38</td><td class="pass">Pass</td></tr>
        <tr><td>23</td><td>Fathima S</td><td class="num">47</td><td class="pass">Pass</td></tr>
        <tr><td>24</td><td>Joseph K</td><td class="num">17</td><td class="fail">Fail</td></tr>
      </tbody>
    </table>
  </div>
</body>
</html>
```

### Real-world example

KTU results page, IRCTC PNR status table, a cricket scoreboard on Cricbuzz: all are tables with header colour, zebra stripes and right-aligned numbers.

### Common mistakes

- Forgetting `border-collapse` (thick double lines).
- Setting borders on `table` only (cells have no lines).
- Left-aligning numbers (hard to compare; right-align them).
- No scroll wrapper, so the table breaks the layout on phones.

### Check your understanding

1. What does `border-collapse: collapse` do?
2. Difference between `table-layout: auto` and `fixed`?
3. How do you give every second row a different colour?

---

## Topic 26. Box model and text flow

### Simple explanation

**Every element is a rectangular box.** The box model has four layers from inside to outside:

1. **Content:** the text or image itself (`width` and `height` apply here by default).
2. **Padding:** space **inside** the border, around the content. Takes the background colour.
3. **Border:** the line around the padding.
4. **Margin:** space **outside** the border, between this box and its neighbours. Always transparent.

ASCII diagram:

```text
+--------------------------------------------------+
|                     MARGIN                       |
|   +------------------------------------------+   |
|   |                 BORDER                   |   |
|   |   +----------------------------------+   |   |
|   |   |             PADDING              |   |   |
|   |   |   +--------------------------+   |   |   |
|   |   |   |                          |   |   |   |
|   |   |   |         CONTENT          |   |   |   |
|   |   |   |     (text / image)       |   |   |   |
|   |   |   |     width x height       |   |   |   |
|   |   |   +--------------------------+   |   |   |
|   |   |                                  |   |   |
|   |   +----------------------------------+   |   |
|   |                                          |   |
|   +------------------------------------------+   |
|                                                  |
+--------------------------------------------------+
```

**Total width** (default `content-box`):

```text
total width = margin-left + border-left + padding-left + width
            + padding-right + border-right + margin-right
```

Example: `width: 200px; padding: 20px; border: 5px solid; margin: 10px;`
Visible box = 200 + 20 + 20 + 5 + 5 = **250px**. Space taken including margins = 270px.
With `box-sizing: border-box`, the visible box is exactly **200px** (content shrinks to 150px).

**Margin collapsing.** The top and bottom margins of two stacked block elements merge into the larger one (not added). Example: 20px under one box and 30px above the next gives a gap of 30px, not 50px.

**`margin: 0 auto`** centres a block with a set width.

**Text flow.** How content is laid out in the page:

- **Block** elements stack **top to bottom**, each taking the full row.
- **Inline** elements flow **left to right**, wrap at the edge like words in a sentence, and ignore `width`, `height`, and top/bottom margin.
- **`inline-block`** flows like inline but accepts width, height and margins.
- **`float`** takes an element to the left or right and lets text wrap around it (like pictures in a newspaper). Use `clear: both` to stop wrapping. (Old way of layouts; modern pages use flexbox and grid, but floats are still right for text wrapping around images.)
- **`display: none`** hides and removes from layout; `visibility: hidden` hides but keeps the space.
- Text properties that affect flow: `white-space`, `overflow-wrap`, `text-overflow`, `line-height`, `text-indent`.

### Analogy

A box model is a **framed photo on a wall**. The photo itself is the content. The white card around the photo inside the frame is the padding. The wooden frame is the border. The empty wall space between this frame and the next one is the margin.

Text flow is like **people in a queue and a crowd**: block elements are people standing one behind the other in a straight line; inline elements are friends walking side by side who go to the next row when the road ends; a float is a **street vendor sitting at the left of the road** with people walking around him.

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Box Model and Text Flow</title>
  <style>
    body { font-family: Arial, sans-serif; background: #eee; }

    .box {
      width: 200px;
      padding: 20px;
      border: 5px solid #0a58ca;
      margin: 30px;
      background-color: #cfe8ff;      /* shows through padding, NOT through margin */
    }

    .border-box { box-sizing: border-box; }   /* compare widths with dev tools */

    /* Margin collapsing demo */
    .m1 { margin-bottom: 20px; background: #ffd6d6; }
    .m2 { margin-top: 30px;    background: #d6ffd8; }

    /* Float demo */
    .article { background: white; padding: 16px; overflow: auto; }
    .article img {
      float: left;
      width: 120px;
      height: 80px;
      margin: 0 12px 8px 0;
      background: #bbb;
    }

    /* inline vs inline-block */
    .tag {
      display: inline-block;
      padding: 6px 12px;
      margin: 4px;
      background: #fc8019;
      color: white;
      border-radius: 20px;
    }
  </style>
</head>
<body>
  <h2>1. Box model</h2>
  <div class="box">content-box: visible width = 200 + 40 + 10 = 250px</div>
  <div class="box border-box">border-box: visible width = 200px</div>

  <h2>2. Margin collapsing</h2>
  <div class="m1">Box 1 (margin-bottom 20px)</div>
  <div class="m2">Box 2 (margin-top 30px). Gap between boxes is 30px, not 50px.</div>

  <h2>3. Float (text wraps around)</h2>
  <div class="article">
    <img alt="Placeholder image box" src="data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///yH5BAEAAAAALAAAAAABAAEAAAIBRAA7">
    <p>The picture floats to the left and this paragraph flows around it. This is how magazines and news sites put a photo inside a story. Keep writing more words here so that the text goes below the picture after some lines and you can clearly see the wrap.</p>
  </div>

  <h2>4. Inline-block tags</h2>
  <span class="tag">HTML</span><span class="tag">CSS</span><span class="tag">JavaScript</span>
</body>
</html>
```

Open developer tools (F12), hover an element in the "Elements" panel and see the coloured box-model diagram: blue = content, green = padding, yellow = border, orange = margin.

### Real-world example

- Every card on Flipkart, Swiggy or Zomato is a box with padding inside and margin between cards.
- A news article with a photo on the left and text wrapping around is `float`.
- Tag chips ("Veg", "Bestseller") are `inline-block`.

### Common mistakes

- Thinking `width` includes padding and border (it does not unless `border-box`).
- Expecting margins of neighbouring blocks to add up.
- Giving background colour and wondering why margin is not coloured (margin is outside).
- Forgetting to clear floats: the parent collapses to zero height. Fix with `overflow: auto` on the parent (as in the demo) or `clear: both`.

### Check your understanding

1. Draw and label the box model.
2. A box has `width: 300px; padding: 10px; border: 2px; margin: 15px`. What is its visible width in `content-box`? (Answer: 300 + 20 + 4 = 324px.) In `border-box`? (300px.)
3. Difference between padding and margin?
4. What is the difference between `display: none` and `visibility: hidden`?

### Classroom activity (10 min): "Draw the box model"

Each student draws the box model of a **tiffin box** on paper: food = content, thick lid padding = padding, steel wall = border, gap to the next box in the bag = margin. Then they open dev tools on any site and match the diagram.

---

## Topic 27. div and span

### Simple explanation

`<div>` and `<span>` have **no meaning of their own**. They are plain containers used to group things so CSS (or JavaScript) can style or find them.

| | `<div>` | `<span>` |
|---|---|---|
| Type | Block | Inline |
| Takes | Full row, starts a new line | Only as much space as its content |
| Used for | Grouping sections, layout blocks, cards | Styling a few words in a line |
| Width/height | Works | Ignored (until `inline-block`) |
| Can contain | Other blocks and inline elements | Only inline content (text, `a`, `img`, other `span`) |

Always give them a `class` or `id` that explains their purpose: `<div class="product-card">`.

Prefer meaningful tags (`header`, `nav`, `section`) where they fit; use `div` and `span` when no meaningful tag exists.

### Analogy

- `<div>` is a **cardboard carton** that holds many items and sits on its own row in the godown.
- `<span>` is a **highlighter pen**: it marks a few words in a line without breaking the line.

### Code example

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>div and span</title>
  <style>
    body { font-family: Arial, sans-serif; background: #f4f6f8; }

    .order {                       /* div used as a card */
      width: 300px;
      background: white;
      border: 1px solid #ddd;
      border-radius: 10px;
      padding: 14px;
      margin: 16px;
    }

    .order .title { font-weight: bold; }
    .veg    { color: green; }       /* span used for a few words */
    .nonveg { color: #b71c1c; }
    .price  { float: right; font-weight: bold; }
    .status {
      background: #e8f5e9;
      color: #2e7d32;
      padding: 2px 8px;
      border-radius: 10px;
      font-size: 0.85rem;
    }
  </style>
</head>
<body>
  <div class="order">
    <div class="title">Meals Corner, Kochi</div>
    <div>
      <span class="veg">Veg thali</span> x 1
      <span class="price">Rs. 120</span>
    </div>
    <div>
      <span class="nonveg">Chicken biryani</span> x 2
      <span class="price">Rs. 360</span>
    </div>
    <div>Status: <span class="status">Out for delivery</span></div>
  </div>
</body>
</html>
```

### Real-world example

The order summary in a Swiggy-like app: each restaurant block is a `div`, and a coloured "veg"/"non-veg" label or the status chip is a `span`. Almost every real page has hundreds of `div`s.

### Common mistakes

- "Divitis": using nothing but `div` where `nav`, `header`, `ul` are better.
- Putting a `div` inside a `span` or `p` (invalid; block inside inline).
- Using `span` and `<br>` to build a layout.

### Check your understanding

1. Difference between `div` and `span`?
2. Which one will you use to colour just one word in a paragraph?
3. Why is `<div class="header">` less useful than `<header>`?

---

## Topic 28. Basics of responsive CSS: viewport and media queries

### Simple explanation

**Responsive web design** = one website that adapts to every screen size (phone, tablet, laptop) instead of making separate sites. In India most users open pages on **phones**, so this is very important.

The three tools:

1. **Viewport meta tag** (in HTML `<head>`):

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

Without it, a phone pretends to be about 980px wide and shrinks the whole page (tiny text). With it, the page width equals the real screen width.

2. **Flexible sizes:** use `%`, `max-width`, `rem`, `vw` rather than fixed `px` for big areas. `img { max-width: 100%; height: auto; }`.

3. **Media queries:** CSS rules that apply **only when a condition is true** (such as the screen width).

```css
@media (max-width: 600px) {
  /* rules only for screens 600px wide or narrower */
}
```

Common conditions: `min-width`, `max-width`, `orientation: landscape`, `prefers-color-scheme: dark`, `print`.

Typical breakpoints (guide only): up to 600px phone, 601-992px tablet, above 992px laptop/desktop.

**Mobile-first** approach: write the phone styles first, then add `@media (min-width: 768px) { ... }` for bigger screens. It keeps phone CSS light.

Small modern helpers (introduction only): **Flexbox** (`display: flex; flex-wrap: wrap;`) lines up items in a row that wraps on small screens.

### Analogy

Water takes the shape of any glass. A responsive page takes the shape of any screen. Or: a **tailor** who makes a shirt in S, M, L sizes from the same pattern. Media queries are the measuring tape that decides which size to use.

### Code example

A three-column layout on laptops, two on tablets and one column on phones.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Responsive Basics</title>
  <style>
    * { box-sizing: border-box; }
    body { margin: 0; font-family: Arial, sans-serif; background: #f4f6f8; }

    header { background: #0a58ca; color: white; padding: 16px; text-align: center; }

    .container {
      display: flex;
      flex-wrap: wrap;           /* items drop to the next row when no space */
      gap: 16px;
      padding: 16px;
    }

    /* Mobile-first: default is one column */
    .card {
      flex: 1 1 100%;
      background: white;
      padding: 16px;
      border-radius: 10px;
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.15);
    }

    /* Tablet: two columns */
    @media (min-width: 600px) {
      .card { flex: 1 1 calc(50% - 16px); }
    }

    /* Laptop: three columns */
    @media (min-width: 992px) {
      .card { flex: 1 1 calc(33.333% - 16px); }
    }

    /* Show a different message by screen size */
    .only-phone  { display: block; }
    .only-large  { display: none; }
    @media (min-width: 992px) {
      .only-phone { display: none; }
      .only-large { display: block; }
    }

    /* Dark mode if the user's phone is set to dark */
    @media (prefers-color-scheme: dark) {
      body { background: #121212; }
      .card { background: #1e1e1e; color: #eee; }
    }

    /* Hide decorations when printing */
    @media print {
      header { display: none; }
    }
  </style>
</head>
<body>
  <header>
    <h1>Responsive Cards</h1>
    <p class="only-phone">You are on a small screen.</p>
    <p class="only-large">You are on a large screen.</p>
  </header>

  <div class="container">
    <div class="card"><h2>Card 1</h2><p>Resize the browser window slowly.</p></div>
    <div class="card"><h2>Card 2</h2><p>Columns change at 600px and 992px.</p></div>
    <div class="card"><h2>Card 3</h2><p>This is how shopping sites arrange products.</p></div>
    <div class="card"><h2>Card 4</h2><p>Open F12, click the phone icon, test iPhone and iPad sizes.</p></div>
    <div class="card"><h2>Card 5</h2><p>Same HTML. Different CSS rules by width.</p></div>
    <div class="card"><h2>Card 6</h2><p>That is responsive design.</p></div>
  </div>
</body>
</html>
```

### Real-world example

Flipkart, Zomato and IRCTC show **two products per row on phone and five on laptop**; the top menu turns into a "hamburger" icon on small screens. All of it is media queries and flexible widths.

### Common mistakes

- Forgetting the viewport meta tag (media queries then seem not to work on a phone).
- Mixing up `min-width` (this wide **or wider**) and `max-width` (this wide **or narrower**).
- Using only fixed `px` widths, causing sideways scrolling on phones.
- Testing only on a laptop. Always test with dev tools device mode and on a real phone.
- Tiny tap targets: buttons and links should be at least about 44px tall on phones.

### Check your understanding

1. What does the viewport meta tag do?
2. Write a media query that turns the text colour red on screens narrower than 500px.
3. Difference between `min-width` and `max-width` media queries?
4. What is the "mobile-first" idea?

### Classroom activity (10 min): "Shrink the browser"

Open the mini project in the browser. Drag the window narrower and call out when the layout changes. Then open the device toolbar on the phone and check three phone models.

---

# MINI PROJECT: College Fest Registration Page

**Time:** 1 hour in class (finish at home). **Work:** in pairs.

### Goal

Build a responsive one-page website for a college fest called **"TechFest 2026"**. It must use almost everything taught in this module.

### Checklist (marking scheme, 20 marks)

| Item | Marks |
|---|---|
| Correct HTML5 skeleton, `lang`, `charset`, `viewport`, `title`, `description` meta | 3 |
| Semantic structure: `header`, `nav`, `main`, `section`, `article`, `aside`, `footer` | 3 |
| Navigation with internal links (`#events`, `#schedule`, `#register`) | 2 |
| Event list (`ul`/`ol`) and a schedule table with `thead`, `tbody`, `colspan` | 3 |
| Registration form with at least 6 input types, `label`, `datalist`, `autocomplete`, `required` | 4 |
| External CSS file with class, ID, descendant and `:hover` selectors | 2 |
| Responsive layout with at least one media query | 2 |
| Neatness, indentation, meaningful names | 1 |

### Folder

```text
techfest/
  index.html
  style.css
  banner.jpg      (optional; any image. The page works without it.)
```

### index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="TechFest 2026: register for coding, robotics and quiz events at our college.">
  <meta name="author" content="Student Council">
  <title>TechFest 2026 - Registration</title>
  <link rel="stylesheet" href="style.css">
</head>
<body id="top">

  <header class="site-header">
    <h1>TechFest 2026</h1>
    <p class="tagline">Code. Build. Compete. &#8226; 15-16 November 2026</p>
  </header>

  <nav class="main-nav">
    <ul>
      <li><a href="#events">Events</a></li>
      <li><a href="#schedule">Schedule</a></li>
      <li><a href="#register">Register</a></li>
      <li><a href="#contact">Contact</a></li>
    </ul>
  </nav>

  <main class="layout">

    <div class="content">

      <section id="about" class="hero">
        <h2>Welcome</h2>
        <p>
          TechFest is the yearly technical festival of our college. Two days of workshops,
          contests and fun. Students from all colleges in Kerala can join.
          Entry is <strong>free</strong> for KTU students.
        </p>
        <p><span class="chip">Free entry</span> <span class="chip">Certificates</span> <span class="chip">Cash prizes</span></p>
      </section>

      <section id="events">
        <h2>Events</h2>
        <div class="cards">
          <article class="card">
            <span class="badge">New</span>
            <h3>CodeSprint</h3>
            <p>A 2-hour coding contest. Solo entry.</p>
          </article>
          <article class="card">
            <h3>RoboRace</h3>
            <p>Build a line-follower robot. Teams of 3.</p>
          </article>
          <article class="card">
            <h3>Tech Quiz</h3>
            <p>Questions on gadgets, apps and the internet. Teams of 2.</p>
          </article>
        </div>

        <h3>Rules</h3>
        <ol>
          <li>Carry your college ID card.</li>
          <li>Reach the venue 15 minutes early.</li>
          <li>The judges' decision is final.</li>
        </ol>
      </section>

      <section id="schedule">
        <h2>Schedule</h2>
        <div class="table-wrap">
          <table>
            <caption>Two-day schedule</caption>
            <thead>
              <tr>
                <th>Time</th>
                <th>Day 1 (15 Nov)</th>
                <th>Day 2 (16 Nov)</th>
              </tr>
            </thead>
            <tbody>
              <tr>
                <td>9:30 AM</td>
                <td colspan="2" class="center">Inauguration (Main Auditorium)</td>
              </tr>
              <tr>
                <td>10:30 AM</td>
                <td>CodeSprint</td>
                <td>RoboRace</td>
              </tr>
              <tr>
                <td>1:00 PM</td>
                <td colspan="2" class="center">Lunch break</td>
              </tr>
              <tr>
                <td>2:00 PM</td>
                <td>Tech Quiz</td>
                <td>Prize distribution</td>
              </tr>
            </tbody>
          </table>
        </div>
      </section>

      <section id="register">
        <h2>Register now</h2>
        <form action="#" method="post">

          <fieldset>
            <legend>Your details</legend>

            <div class="field">
              <label for="fullname">Full name</label>
              <input type="text" id="fullname" name="fullname" required minlength="3"
                     autocomplete="name" placeholder="Anu Mathew">
            </div>

            <div class="field">
              <label for="email">Email</label>
              <input type="email" id="email" name="email" required autocomplete="email"
                     placeholder="you@example.com">
            </div>

            <div class="field">
              <label for="phone">Mobile number</label>
              <input type="tel" id="phone" name="phone" required pattern="[0-9]{10}"
                     title="Enter 10 digits" autocomplete="tel" placeholder="9876543210">
            </div>

            <div class="field">
              <label for="college">College</label>
              <input list="colleges" id="college" name="college" autocomplete="off"
                     placeholder="Start typing your college">
              <datalist id="colleges">
                <option value="College of Engineering Trivandrum"></option>
                <option value="Govt. Engineering College Thrissur"></option>
                <option value="Model Engineering College Thrikkakara"></option>
                <option value="Rajiv Gandhi Institute of Technology Kottayam"></option>
                <option value="Other"></option>
              </datalist>
            </div>

            <div class="field">
              <label for="dob">Date of birth</label>
              <input type="date" id="dob" name="dob" autocomplete="bday">
            </div>

            <div class="field">
              <label for="year">Year of study</label>
              <select id="year" name="year" required>
                <option value="">-- choose --</option>
                <option value="1">First year</option>
                <option value="2">Second year</option>
                <option value="3">Third year</option>
                <option value="4">Fourth year</option>
              </select>
            </div>
          </fieldset>

          <fieldset>
            <legend>Events you want to join</legend>
            <label class="inline"><input type="checkbox" name="event" value="codesprint"> CodeSprint</label>
            <label class="inline"><input type="checkbox" name="event" value="roborace"> RoboRace</label>
            <label class="inline"><input type="checkbox" name="event" value="quiz"> Tech Quiz</label>

            <div class="field">
              <span class="label-text">Food preference</span>
              <label class="inline"><input type="radio" name="food" value="veg" checked> Veg</label>
              <label class="inline"><input type="radio" name="food" value="nonveg"> Non-veg</label>
            </div>

            <div class="field">
              <label for="team">Team size (1 to 3)</label>
              <input type="number" id="team" name="team" min="1" max="3" value="1">
            </div>

            <div class="field">
              <label for="tshirt">T-shirt colour</label>
              <input type="color" id="tshirt" name="tshirt" value="#0a58ca">
            </div>

            <div class="field">
              <label for="idcard">Upload college ID</label>
              <input type="file" id="idcard" name="idcard" accept=".jpg,.png,.pdf">
            </div>

            <div class="field">
              <label for="note">Anything we should know?</label>
              <textarea id="note" name="note" rows="3" maxlength="200"></textarea>
            </div>
          </fieldset>

          <button type="submit" class="btn">Register</button>
          <button type="reset" class="btn btn-light">Clear</button>
        </form>
      </section>

    </div>

    <aside class="sidebar">
      <h2>Important dates</h2>
      <ul>
        <li>Last date to register: <time datetime="2026-11-10">10 Nov 2026</time></li>
        <li>Fest days: 15-16 Nov 2026</li>
      </ul>
      <h2>Quick links</h2>
      <ul>
        <li><a href="https://www.ktu.edu.in" target="_blank" rel="noopener noreferrer">KTU website</a></li>
        <li><a href="#top">Back to top</a></li>
      </ul>
    </aside>

  </main>

  <footer id="contact" class="site-footer">
    <p>&copy; 2026 TechFest, Student Council.</p>
    <address>
      Email: <a href="mailto:techfest@example.edu">techfest@example.edu</a> |
      Phone: <a href="tel:+914712345678">+91 471 234 5678</a>
    </address>
  </footer>

</body>
</html>
```

### style.css

```css
/* ---------- Basics ---------- */
* { box-sizing: border-box; }

body {
  margin: 0;
  font-family: "Segoe UI", Arial, sans-serif;
  line-height: 1.6;
  color: #222;
  background-color: #f4f6f8;
}

h1, h2, h3 { line-height: 1.2; }
a { color: #0a58ca; }
img { max-width: 100%; height: auto; }

/* ---------- Header ---------- */
.site-header {
  background: linear-gradient(135deg, #0a58ca, #6610f2);
  color: white;
  text-align: center;
  padding: 40px 16px;
}
.site-header h1 { margin: 0 0 8px; font-size: 2.2rem; }
.tagline { margin: 0; font-size: 1.1rem; }

/* ---------- Navigation ---------- */
.main-nav {
  background-color: #084298;
  position: sticky;            /* stays at top while scrolling */
  top: 0;
  z-index: 10;
}
.main-nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
.main-nav a {
  display: block;
  padding: 14px 20px;
  color: white;
  text-decoration: none;
}
.main-nav a:hover { background-color: #0a58ca; }

/* ---------- Layout: content + sidebar ---------- */
.layout {
  max-width: 1100px;
  margin: 20px auto;
  padding: 0 16px;
  display: flex;
  flex-direction: column;       /* phone: stacked */
  gap: 20px;
}
.content { flex: 1; }
.sidebar {
  background-color: white;
  border: 1px solid #ddd;
  border-radius: 10px;
  padding: 16px;
  align-self: flex-start;
}

section {
  background-color: white;
  border-radius: 10px;
  padding: 20px;
  margin-bottom: 20px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
}
section h2 { margin-top: 0; color: #084298; }

/* ---------- Hero chips ---------- */
.chip {
  display: inline-block;
  background-color: #e7f1ff;
  color: #084298;
  padding: 2px 12px;
  border-radius: 20px;
  font-size: 0.9rem;
  margin-right: 6px;
}

/* ---------- Cards with a badge ---------- */
.cards {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
}
.card {
  position: relative;            /* reference for the absolute badge */
  flex: 1 1 100%;
  border: 1px solid #ddd;
  border-radius: 10px;
  padding: 16px;
  background-color: #fafcff;
}
.card:hover { box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2); }
.card h3 { margin-top: 0; }
.badge {
  position: absolute;
  top: 10px;
  right: 10px;
  background-color: crimson;
  color: white;
  font-size: 0.75rem;
  padding: 2px 8px;
  border-radius: 4px;
}

/* ---------- Table ---------- */
.table-wrap { overflow-x: auto; }
table { width: 100%; border-collapse: collapse; }
caption { font-weight: bold; padding: 8px; text-align: left; }
th, td { border: 1px solid #bbb; padding: 10px; text-align: left; }
th { background-color: #0a58ca; color: white; }
tbody tr:nth-child(even) { background-color: #f2f6ff; }
tbody tr:hover { background-color: #fff3cd; }
td.center { text-align: center; font-weight: bold; }

/* ---------- Form ---------- */
fieldset {
  border: 1px solid #ccc;
  border-radius: 8px;
  margin: 0 0 16px;
  padding: 12px 16px;
}
legend { font-weight: bold; color: #084298; padding: 0 8px; }

.field { margin-bottom: 12px; }
.field label, .label-text { display: block; font-weight: 600; margin-bottom: 4px; }

input[type="text"],
input[type="email"],
input[type="tel"],
input[type="date"],
input[type="number"],
input[list],
select,
textarea {
  width: 100%;
  padding: 10px;
  border: 1px solid #aaa;
  border-radius: 6px;
  font-size: 1rem;
}
input:focus, select:focus, textarea:focus {
  outline: 3px solid #ffc107;
  border-color: #0a58ca;
}
input:invalid:not(:placeholder-shown) { border-color: crimson; }

label.inline { display: inline-block; font-weight: normal; margin-right: 16px; }
.field label.inline { display: inline-block; font-weight: normal; }

.btn {
  background-color: #fc8019;
  color: white;
  border: none;
  padding: 12px 24px;
  font-size: 1rem;
  border-radius: 6px;
  cursor: pointer;
}
.btn:hover { background-color: #d96a0b; }
.btn-light { background-color: #6c757d; }
.btn-light:hover { background-color: #565e64; }

/* ---------- Footer ---------- */
.site-footer {
  background-color: #212529;
  color: #ddd;
  text-align: center;
  padding: 20px 16px;
}
.site-footer a { color: #8bb9fe; }
.site-footer address { font-style: normal; }

/* ---------- Responsive ---------- */
@media (min-width: 600px) {
  .card { flex: 1 1 calc(50% - 16px); }
}

@media (min-width: 900px) {
  .layout { flex-direction: row; }      /* laptop: content left, sidebar right */
  .sidebar { width: 280px; flex-shrink: 0; }
  .card { flex: 1 1 calc(33.333% - 16px); }
}

@media print {
  .main-nav, .sidebar, .btn { display: none; }
}
```

### How to test

1. Open `index.html`. Click each menu item and check the page jumps to the right section.
2. Squeeze the window narrow. Cards should stack and the sidebar should drop below.
3. Try submitting with an empty name or a bad email. The browser should stop you.
4. Type "Mo" in the College box. See the suggestion. Pick one.
5. Press F12, switch on the phone view, and test two different phone sizes.

### Extension ideas for fast learners

- Add a banner `<img>` with `alt` text inside the header.
- Add a "Gallery" section with a `<figure>` for each picture.
- Add a dark mode with `@media (prefers-color-scheme: dark)`.
- Add a "Sponsors" description list (`dl`).

---

# QUESTION BANK (KTU exam style)

**Pattern used by KTU for this course (typical):**

- **Part A:** 10 questions x 3 marks (answer all).
- **Part B:** each module has 2 questions of 9 marks (answer one of the two), usually with subparts a and b.

Use the questions below as practice. Model answers or hints follow after the questions.

## Part A: Short answer (3 marks each)

1. What is the purpose of the `<!DOCTYPE html>` declaration? Write the minimum structure of an HTML5 document.
2. Differentiate between block-level and inline elements with two examples each.
3. Write HTML code to create an unordered list nested inside an ordered list.
4. What is the use of the `alt` attribute in the `<img>` tag? What happens if it is missing?
5. Explain `colspan` and `rowspan` with a small table example.
6. What are semantic elements in HTML5? Name any five.
7. What is the purpose of the `<meta>` tag? Give two examples.
8. Differentiate between `get` and `post` methods of a form.
9. What is the use of the `<datalist>` element?
10. Explain the three ways of adding CSS to an HTML page (one line each).
11. What is specificity in CSS? Arrange these in increasing order of specificity: ID selector, element selector, inline style, class selector.
12. What is the difference between `margin` and `padding`?
13. Distinguish between `position: relative` and `position: absolute`.
14. What is a media query? Write one example.
15. Write the CSS to remove bullets from a list and show list items in one row.

(15 questions are given for practice; the real paper has 10.)

## Part B: Long answer (9 marks each)

**Q1.**
(a) Explain the structure of an HTML5 form. Write a sample form using at least three different input types. (6 marks)
(b) Explain the `autocomplete` attribute and the `datalist` element with examples. (3 marks)

**Q2.**
(a) Explain the difference between internal and external style sheets in CSS with examples. (5 marks)
(b) Given a scenario where a webpage displays conflicting styles, how would you resolve the conflict using CSS principles? (4 marks)

**Q3.**
(a) Explain the CSS box model with a neat diagram. (5 marks)
(b) A box has `width: 250px; padding: 15px; border: 5px solid; margin: 20px;`. Calculate its total visible width and the total space it occupies (i) in the default model and (ii) with `box-sizing: border-box`. (4 marks)

**Q4.**
(a) Using CSS, create a basic layout with a header at the top and two sections side by side. Write the HTML and CSS. (6 marks)
(b) Explain how you would make this layout switch to a single column on mobile phones. (3 marks)

**Q5.**
(a) Write HTML and CSS to display an image in the centre of the page with a border and padding. (5 marks)
(b) Explain absolute and relative positioning with an example. (4 marks)

**Q6.**
(a) Create an HTML table with a caption, header row, three data rows and one merged cell. Style it using CSS (borders, header colour, striped rows). (6 marks)
(b) Explain the difference between `div` and `span` with examples. (3 marks)

**Q7 (extra practice).**
(a) Explain HTML5 page structure elements with a labelled layout and code. (5 marks)
(b) Explain internal linking in HTML with an example. (4 marks)

**Q8 (extra practice).**
(a) What are responsive web pages? Explain the role of the viewport meta tag and media queries with code. (6 marks)
(b) Explain the CSS selectors: class, ID, descendant, child and attribute selectors with examples. (3 marks)

---

## Model answers and hints

### Part A hints (short)

**A1.** `<!DOCTYPE html>` tells the browser to use HTML5 rules (standards mode). Minimum structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>
  Content
</body>
</html>
```

**A2.** Block: starts on a new line, takes full width (`div`, `p`, `h1`). Inline: stays in the line, takes only its content width (`span`, `a`, `img`, `strong`).

**A3.**

```html
<ol>
  <li>Item 1
    <ul>
      <li>Sub item A</li>
      <li>Sub item B</li>
    </ul>
  </li>
  <li>Item 2</li>
</ol>
```

**A4.** `alt` gives alternative text shown if the image cannot load and read aloud by screen readers; it also helps search engines. If missing, a broken image gives no hint, and the page is not accessible.

**A5.** `colspan="n"` makes a cell stretch over n columns; `rowspan="n"` over n rows.

```html
<table border="1">
  <tr><th colspan="2">Marks</th></tr>
  <tr><td rowspan="2">Anu</td><td>45</td></tr>
  <tr><td>48</td></tr>
</table>
```

**A6.** Semantic elements describe their meaning: `header`, `nav`, `main`, `section`, `article`, `aside`, `footer`, `figure`. They help accessibility, SEO and readability.

**A7.** `<meta>` gives information about the page and sits in `<head>`. Examples: `<meta charset="UTF-8">` (encoding), `<meta name="viewport" ...>` (mobile fit), `<meta name="description" content="...">` (search summary).

**A8.** GET sends data in the URL (visible, limited length, can be bookmarked; used for search). POST sends data in the request body (not visible in the URL, no small limit; used for login and sign-up).

**A9.** `<datalist>` supplies a list of suggested values for an `<input>` through its `list` attribute. The user can pick from the list or type something else.

**A10.** Inline: `style` attribute on one element. Embedded: `<style>` in `<head>` for one page. External: separate `.css` file linked with `<link rel="stylesheet" href="...">` for many pages.

**A11.** Specificity is the weight of a selector deciding which rule wins. Increasing order: element selector < class selector < ID selector < inline style.

**A12.** Padding is space inside the border between content and border (shows the background). Margin is space outside the border between boxes (transparent).

**A13.** Relative: positioned from its own normal position and keeps its space in the flow. Absolute: removed from flow and positioned from the nearest positioned ancestor (or the page).

**A14.** A media query applies CSS only when a condition holds:

```css
@media (max-width: 600px) {
  body { font-size: 14px; }
}
```

**A15.**

```css
ul { list-style: none; padding: 0; }
li { display: inline-block; margin-right: 10px; }
```

---

### Part B Q1: HTML5 form, autocomplete and datalist (model answer)

**(a) Structure of an HTML5 form**

A form collects user input and sends it to a server. Main parts:

1. `<form>`: container with `action` (URL that receives the data) and `method` (`get` or `post`).
2. `<label>`: caption for a field; `for` matches the field's `id`.
3. Form controls: `<input>` (with many `type`s), `<textarea>`, `<select>`/`<option>`, `<button>`.
4. `name` attribute on each control: the key under which the value is sent.
5. `<fieldset>` and `<legend>`: group related fields.
6. Submit button: sends the form.
7. HTML5 validation attributes: `required`, `min`, `max`, `pattern`, `minlength`, `maxlength`, `placeholder`.

Sample form (text, email, password, date, number, radio, checkbox):

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Registration Form</title>
</head>
<body>
  <h2>Student Registration</h2>
  <form action="/register" method="post">
    <fieldset>
      <legend>Personal details</legend>

      <p>
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required>
      </p>

      <p>
        <label for="email">Email:</label>
        <input type="email" id="email" name="email" required>
      </p>

      <p>
        <label for="pwd">Password:</label>
        <input type="password" id="pwd" name="pwd" minlength="8" required>
      </p>

      <p>
        <label for="dob">Date of birth:</label>
        <input type="date" id="dob" name="dob">
      </p>

      <p>
        <label for="age">Age:</label>
        <input type="number" id="age" name="age" min="16" max="60">
      </p>

      <p>Gender:
        <input type="radio" id="m" name="gender" value="male"><label for="m">Male</label>
        <input type="radio" id="f" name="gender" value="female"><label for="f">Female</label>
      </p>

      <p>Interests:
        <input type="checkbox" id="w" name="int" value="web"><label for="w">Web</label>
        <input type="checkbox" id="a" name="int" value="ai"><label for="a">AI</label>
      </p>
    </fieldset>

    <button type="submit">Register</button>
    <button type="reset">Reset</button>
  </form>
</body>
</html>
```

**(b) `autocomplete` and `datalist`**

- `autocomplete` is an attribute (on `<form>` or `<input>`) with values `on`, `off` or a token like `name`, `email`, `tel`. It tells the browser whether to remember and fill in values from the user's saved data. Use `off` for one-time passwords or sensitive data.
- `<datalist>` gives a list of **suggested options** for an input. The input's `list` attribute must match the datalist `id`. The user may still type a value that is not in the list.

```html
<label for="city">City:</label>
<input list="cities" id="city" name="city" autocomplete="off">
<datalist id="cities">
  <option value="Kochi"></option>
  <option value="Kozhikode"></option>
  <option value="Kollam"></option>
</datalist>

<input type="email" name="email" autocomplete="email">
```

---

### Part B Q2: Internal vs external style sheets, and conflict resolution (model answer)

**(a) Difference between internal and external style sheets**

- **Internal (embedded) style sheet:** CSS is written inside a `<style>` element within `<head>` of the HTML page. It affects only that page.
- **External style sheet:** CSS is written in a separate `.css` file and linked using `<link rel="stylesheet" href="style.css">` in `<head>`. One file can control many pages.

| Point | Internal | External |
|---|---|---|
| Location | `<style>` inside `<head>` | Separate `.css` file |
| Linking | Not needed | `<link>` tag |
| Scope | One page | Whole website |
| Maintenance | Edit every page | Edit one file |
| Page size and speed | Larger HTML, CSS repeated on every page | Smaller HTML, CSS file cached by browser |
| Use | Small, single page | Real websites |

Example, internal:

```html
<head>
  <style>
    h1 { color: blue; }
    p  { font-size: 18px; }
  </style>
</head>
```

Example, external:

`style.css`

```css
h1 { color: blue; }
p  { font-size: 18px; }
```

`index.html`

```html
<head>
  <link rel="stylesheet" href="style.css">
</head>
```

(For completeness: inline style is a third method, using the `style` attribute on one element, like `<p style="color:red;">`.)

**(b) Resolving conflicting styles**

When two or more rules style the same property of the same element, the browser applies the **cascade**:

1. **Importance:** a declaration with `!important` wins over normal ones.
2. **Specificity:** the more specific selector wins. Inline style (1,0,0,0) > ID (0,1,0,0) > class, attribute, pseudo-class (0,0,1,0) > element, pseudo-element (0,0,0,1).
3. **Source order:** if specificity is equal, the rule written **later** wins (also the later-linked style sheet).
4. **Inheritance:** an inherited value is the weakest; a rule that targets the element directly beats it.

Scenario: a paragraph with `class="note"` is expected to be green but shows red.

```css
p       { color: red; }        /* 0,0,0,1 */
.note   { color: green; }      /* 0,0,1,0 : wins, class beats element */
```

If the page still shows red, some other rule has higher specificity, for example `div p.note`. How to fix:

- Use the browser developer tools (F12) to find which rule wins (the losing declarations are struck through).
- Make your selector at least as specific, or move your rule below the other one.
- Remove duplicate or unnecessary rules.
- Use `!important` only as the last option.
- Good habits: use classes, avoid inline styles and IDs for styling, and keep one clear order of style sheets.

---

### Part B Q3: Box model (model answer)

**(a)** Every HTML element is a rectangular box made of four layers, from inside to outside: **content, padding, border, margin**.

```text
+--------------------------------------------------+
|                     MARGIN                       |
|   +------------------------------------------+   |
|   |                 BORDER                   |   |
|   |   +----------------------------------+   |   |
|   |   |             PADDING              |   |   |
|   |   |   +--------------------------+   |   |   |
|   |   |   |         CONTENT          |   |   |   |
|   |   |   |    (text, image: the     |   |   |   |
|   |   |   |    width x height area)  |   |   |   |
|   |   |   +--------------------------+   |   |   |
|   |   +----------------------------------+   |   |
|   +------------------------------------------+   |
+--------------------------------------------------+
```

- **Content:** the actual text or image. `width` and `height` set its size (in the default model).
- **Padding:** clear space between content and border. Shows the element's background.
- **Border:** line around padding and content.
- **Margin:** transparent space outside the border that separates the element from others. Vertical margins of adjacent blocks collapse into the larger one.

Total width = left margin + left border + left padding + width + right padding + right border + right margin. Setting `box-sizing: border-box` makes `width` include padding and border.

Example:

```css
.box {
  width: 250px;
  padding: 15px;
  border: 5px solid black;
  margin: 20px;
}
```

**(b)** Calculation.

(i) Default (`content-box`):
- Visible width = 250 + (15 x 2) + (5 x 2) = 250 + 30 + 10 = **290px**
- Space occupied = 290 + (20 x 2) = **330px**

(ii) `border-box`:
- Visible width = **250px** (content shrinks to 250 - 30 - 10 = 210px)
- Space occupied = 250 + 40 = **290px**

---

### Part B Q4: Header with two sections side by side (model answer)

**(a)**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Two Column Layout</title>
  <style>
    * { box-sizing: border-box; }
    body { margin: 0; font-family: Arial, sans-serif; }

    header {
      background-color: #0a58ca;
      color: white;
      text-align: center;
      padding: 20px;
    }

    .container {
      display: flex;          /* puts children side by side */
      gap: 16px;
      padding: 16px;
    }

    .left  { flex: 1; background-color: #e7f1ff; padding: 16px; }
    .right { flex: 2; background-color: #fff3cd; padding: 16px; }
  </style>
</head>
<body>
  <header>
    <h1>My Website</h1>
  </header>

  <div class="container">
    <section class="left">
      <h2>Section One</h2>
      <p>Left section takes one part of the width.</p>
    </section>
    <section class="right">
      <h2>Section Two</h2>
      <p>Right section takes two parts of the width.</p>
    </section>
  </div>
</body>
</html>
```

The `header` is a block element so it fills the top row. The `.container` uses `display: flex`, so its two child sections sit side by side. `flex: 1` and `flex: 2` give them a 1:2 width ratio.

Alternative using floats (older method):

```css
.left  { float: left;  width: 40%; }
.right { float: right; width: 60%; }
.container::after { content: ""; display: block; clear: both; }
```

**(b)** Add a media query that changes the direction of the flex container to a column:

```css
@media (max-width: 600px) {
  .container { flex-direction: column; }
}
```

With the viewport meta tag already in `<head>`, screens 600px or narrower will show Section One above Section Two.

---

### Part B Q5: Centre an image with border and padding; positioning (model answer)

**(a)**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Centered Image</title>
  <style>
    body { text-align: center; }          /* Method 1: centres inline content */

    .photo {
      border: 4px solid #0a58ca;
      padding: 12px;
      width: 300px;
      max-width: 100%;
      height: auto;
    }

    /* Method 2: block + auto margins (works for the image alone) */
    .photo2 {
      display: block;
      margin: 20px auto;
      border: 4px dashed crimson;
      padding: 10px;
      width: 300px;
      max-width: 100%;
      height: auto;
    }
  </style>
</head>
<body>
  <h1>My Photo</h1>
  <img class="photo" src="photo.jpg" alt="Portrait of a student">
  <img class="photo2" src="photo.jpg" alt="Portrait of a student">
</body>
</html>
```

Explanation: `text-align: center` on the parent centres inline elements such as `img`. To centre the image itself, make it `display: block` and give `margin: auto` on left and right. `border` draws the frame; `padding` adds space between the picture and the border. If vertical centring is also needed, use a flex container:

```css
body { display: flex; justify-content: center; align-items: center; min-height: 100vh; margin: 0; }
```

**(b) Positioning**

- **Relative:** `position: relative` keeps the element in normal flow, then shifts it by `top/left/right/bottom` from its own original spot. Its original space stays reserved.
- **Absolute:** `position: absolute` takes the element **out of the flow** and places it relative to the nearest ancestor with `position` other than `static` (or the page).

Example: a "SALE" label in the top-right corner of a card.

```html
<div class="card">
  <span class="tag">SALE</span>
  <p>Shoes</p>
</div>
```

```css
.card { position: relative; width: 200px; height: 120px; border: 1px solid #999; }
.tag  { position: absolute; top: 5px; right: 5px; background: red; color: white; padding: 2px 6px; }
```

---

### Part B Q6: Table and div/span (hints)

**(a)** Hint: use the table from Topic 25: `caption`, `thead` with `th`, `tbody` with 3 `tr`, one `td colspan="2"`; CSS: `border-collapse: collapse`, `th, td { border: 1px solid ...; padding: ... }`, `th { background-color }`, `tr:nth-child(even) { background-color }`.

**(b)** `div` is a block-level container used to group sections and for layout (a new line before and after, width and height work). `span` is an inline container used to style part of a text (no line break, width and height ignored). Both have no meaning of their own. Example: `<div class="card">Price: <span class="red">Rs. 99</span></div>`.

---

### Part B Q7 and Q8 (hints)

**Q7 (a)** Draw the layout from Topic 14 and list the elements with one line of meaning each (`header`, `nav`, `main`, `section`, `article`, `aside`, `footer`). Give the code from Topic 14. **(b)** Give `id` on the target, `<a href="#id">` on the link, plus `href="page.html#id"` for another page. Mention the unique `id` rule.

**Q8 (a)** Define responsive design. Viewport tag: `width=device-width, initial-scale=1.0` makes layout width equal device width. Media query code from Topic 28 with `min-width`/`max-width`, `flex-wrap`, and `max-width: 100%` for images. **(b)** Use the table in Topic 19 with one example each.

---

## Quick practice problems (for tutorials)

1. Write HTML for your own timetable using a table with a merged lunch cell.
2. Create a login form with email, password and a "remember me" checkbox, with label for each field.
3. Style a `<ul>` of five links into a horizontal menu; the link under the mouse must turn orange.
4. Create three boxes of 100px x 100px with 10px margin that sit next to each other. Then make them stack on phones.
5. Make a card (image on top, title, price, button) like a Flipkart product card and show an "OFFER" badge in the top-left using positioning.
6. Predict the colour: `#a .b p { color: red; }` vs `div.b p.c { color: blue; }` (the paragraph matches both). Which wins? (Answer: the first scores 0,1,1,1 and the second scores 0,0,2,2. The first wins because it has an ID.)
7. Fix this code: `<p style="{color: red}">Hello<p>`.

---

## Fun classroom activities (collected)

| Activity | Time | How it works |
|---|---|---|
| Spot the 4 errors | 5 min | Broken HTML on the board (Topic 1) |
| Tag the college homepage | 10 min | Label areas with semantic tags (Topic 14) |
| Who wins? card game | 10 min | CSS conflict cards (Topic 18) |
| Draw the tiffin-box model | 10 min | Box model on paper (Topic 26) |
| Shrink the browser | 10 min | Responsive demo (Topic 28) |
| "Zomato in 10 minutes" | 15 min | Teams build a restaurant card with only HTML and 5 CSS properties; best-looking wins |
| "Inspect and tell" | 10 min | Students open dev tools on IRCTC/Flipkart and name three HTML tags and three CSS properties they find |
| HTML Antakshari | 10 min | One team says a tag, the next team must say a tag that starts with the last letter of the previous one (`table` then `em`, then `meta`...) |
| Break and fix | 10 min | Each pair secretly breaks one line in a working page; the other pair finds and fixes it |

---

# QUICK REVISION SHEET

**HTML skeleton:** `DOCTYPE`, `html lang`, `head` (`meta charset`, `meta viewport`, `title`, `link`), `body`.

**Text:** `h1-h6`, `p`, `br`, `hr`, `strong`, `em`, `mark`, `sub`, `sup`, `pre`.

**Links:** `<a href="url" target="_blank">`, `mailto:`, `tel:`, `#id` for internal jump.

**Images:** `<img src alt width height>`, `figure`, `figcaption`.

**Entities:** `&lt; &gt; &amp; &quot; &copy; &nbsp; &#8377;`.

**Lists:** `ul`, `ol`, `li`, `dl`, `dt`, `dd`.

**Tables:** `table`, `caption`, `thead`, `tbody`, `tfoot`, `tr`, `th`, `td`, `colspan`, `rowspan`.

**Forms:** `form(action, method)`, `label for`, `input type`, `textarea`, `select/option`, `button`, `fieldset/legend`, `name`, `required`, `pattern`.

**HTML5 inputs:** `email url tel number range date time datetime-local month week color search file`.

**datalist and autocomplete:** `input list="id"` + `datalist id="id"`; `autocomplete="on|off|name|email|tel..."`.

**Structure:** `header nav main section article aside footer`.

**CSS ways:** inline (`style=""`), embedded (`<style>`), external (`<link rel="stylesheet">`).

**Cascade order:** `!important` > specificity (inline > ID > class > element) > source order (last wins) > inheritance.

**Selectors:** `*`, `p`, `.class`, `#id`, `a, b`, `a b`, `a > b`, `a + b`, `[attr]`, `:hover`, `:nth-child()`, `::before`.

**Box model:** content + padding + border + margin; `box-sizing: border-box`.

**Position:** `static`, `relative`, `absolute`, `fixed`, `sticky`; `z-index`.

**Backgrounds:** `background-color`, `image`, `repeat`, `position`, `size` (`cover/contain`), gradients.

**List styles:** `list-style-type`, `list-style-image`, `list-style-position`, `list-style`.

**Table CSS:** `border-collapse`, `table-layout`, `nth-child(even)`.

**Responsive:** viewport meta + `max-width: 100%` + `@media (min-width / max-width)` + flexible `%`, `rem` units.

---

*End of Module 1. Suggested next step: Module 2 (JavaScript basics) will make this registration page do real work, such as checking the form and showing messages without reloading.*
