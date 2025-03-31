# 📦 `solomd2html`: Standalone Markdown to HTML Converter

This lightweight JavaScript module provides a dependency-free Markdown-to-HTML parser that works in both **browsers** and **Node.js**.

# ✅ Features:
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

# Demo

1. Clone the repo:

Open terminal in any forder of your choice and run:

```
git clone https://github.com/ivostoykov/solomd2html.git
```

2. Run any server of your choice on this folder:

### Nodejs

```Nodejs
http-server .
```

If needed install it with:
```Nodejs
npm install -g http-server
```

### Python 3

```Python3
python3 -m http.server
```

### Python 2

```Python2
python -m SimpleHTTPServer
```

then run in browser:

```
http://localhost:8000/index.html
```

This simple base will use the provided `example.md` and will parse it on load.

# Usage

> [!WARNING]
> `parse` does not sanitize the HTML

## Browser

Open the provided index.html file.

Attach the script with:

```html
<script src="solomd2html.js"></script>
```

or provided minified version:

```html
<script src="solomd2html.min.js"></script>
```


An valid existing element is needed where the result HTML will be appended to:

```js
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

Please use [Issues section](https://github.com/ivostoykov/solomd2html/issues) for bug reports and suggestions.