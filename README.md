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
> `parseAdnRender` does not sanitize the HTML. Be cautious when processing user-supplied data and apply necessary sanitization.

## Browser

Include one of the JavaScript files in your HTML file:

```html
<script src="solomd2html.js"></script>
```

Take a look in the provided index.html file if needed.

A minified version is also provided:

```html
<script src="solomd2html.min.js"></script>
```

Once the script is available, you can use it by passing the Markdown snippet and the target element where the output should appear. Optionally, you can provide a [third parameter](#options) as an object to override default settings. Currently, the available option is:

```json
{
  "codeCopy": true
}
```

To call the parser, use:

```javascript
const res = parseAdnRender(txt, elm_container);
```

To disable the copy button for source code output, use:

```javascript
const res = parseAdnRender(txt, elm_container, { codeCopy: false } );
```

## Parameters

- `txt` - The markdown text that will be transformed.
- `elm_container` - The root element to which the output will be appended.

## Options

The third parameter is an object that accepts additional settings for managing the output:

- `codeCopy` (`boolean`) - If `true`, a Copy button is added to each code block. Default value is `true`.
- `streamReply` (`boolean`) - If `true`, the output will be streamed; otherwise, the entire block will be appended to the given root.  Default value is `true`.

### Script usage example

Ensure an element is available in the DOM for appending parsed HTML:

```javascript
document.addEventListener("DOMContentLoaded", async e => init(e) );
async function init(e){
  elm_container = document.querySelector(`#container`);
  const txt = await getText();
  const res = parseAdnRender(txt, elm_container);
}

async function getText(){
  const response = await fetch(`example.md`);
  return await response.text();
}
```

The script exports itself as a module, allowing it to be used in Node.js.

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
