# 📦 `solomd2html`: Standalone Markdown to HTML Converter

This lightweight JavaScript module provides a dependency-free Markdown-to-HTML parser that works in both **browsers** and **Node.js**.

# ✅ Key Features:
- Converts standard Markdown into native DOM elements
- Handles all common block-level elements:
  - Headings, paragraphs, horizontal rules
  - Blockquotes (with nesting)
  - Lists (ordered, unordered, nested)
  - Code blocks: indented and fenced (with optional language labels)
  - Tables: pipe-style and grid-style
  - Embedded raw HTML (preserved and rendered as source)
- Supports inline formatting:
  - Bold, italic, strikethrough, inline code
- Outputs real DOM (not strings), ideal for browser display or server-side rendering

# Usage

> [!WARNING]
> `parse` does not sanitize the HTML. Be cautious when processing user-supplied data and apply necessary sanitization.

## Browser

Open the provided index.html file.

Include one of the JavaScript files in your HTML:

```html
<script src="solomd2html.js"></script>
```

or use the provided minified version:

```html
<script src="solomd2html.min.js"></script>
```

Once the script is available, use it by passing the Markdown snippet and the target element where the result is intended to appear.

### Usage in browser example

Ensure an element is available in the DOM for appending parsed HTML:

```javascript
document.addEventListener("DOMContentLoaded", async e => init(e) );
async function init(e){
  elm_container = document.querySelector(`#container`);
  const txt = await getText();
  const res = parse(txt, elm_container);
}

async function getText(){
  const response = await fetch(`example.md`);
  return await response.text();
}
```

Feel free to use the [Issues section](https://github.com/ivostoykov/solomd2html/issues) for bug reports and suggestions.


# Demo

## Clone the repo:

Open a terminal in any folder of your choice and execute:

```bash
git clone https://github.com/ivostoykov/solomd2html.git
```

## Set up a server of your choice to host files from this folder:

### Node.js

```bash
http-server .
```

Install with this command, if necessary:

```bash
npm install -g http-server
```

### Python 3

```bash
python3 -m http.server
```

### Python 2

```bash
python -m SimpleHTTPServer
```

Visit the following URL in your browser to see the result:

```
http://localhost:8000/index.html
```

This simple base will use the provided `example.md` and will parse it on load.
