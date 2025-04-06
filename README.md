# 📦 `solomd2html`: Standalone Markdown to HTML Converter

This lightweight JavaScript module offers a dependency-free Markdown-to-HTML parser that works seamlessly in both **browsers** and **Node.js**.

# ✅ Key Features:
- Converts standard Markdown into native DOM elements.
- Handles all common block-level elements:
  - Headings, paragraphs, and horizontal rules.
  - Blockquotes, including nested ones.
  - Lists that are ordered, unordered, and nested.
  - Code blocks, both indented and fenced, with optional language labels.
  - Tables in pipe-style and grid-style formats.
  - Embedded raw HTML, which is preserved and rendered as source.

- Supports inline formatting:
  - Bold, italic, strikethrough, and inline code.
- Outputs real DOM elements, making it ideal for browser display or server-side rendering.

# Usage

> [!WARNING]
> `parseAdnRender` does not sanitize HTML. Exercise caution with user-supplied data and apply necessary sanitization.

## Browser

Include the JavaScript file in your HTML file:

```html
<script src="solomd2html.js"></script>
```

Refer to the provided index.html for guidance. A minified version is also available:

```html
<script src="solomd2html.min.js"></script>
```
Once the script is included, use it by passing a Markdown snippet and the target element for the output. Optionally, provide a [third parameter](#options) as an object to override default settings. Current options include:

```json
 {
  "codeCopy": true,
  "streamReply": true,
  "abortSignal": null,
  "onAbort": null,
  "onRenderStarted": null,
  "onRendering": null,
  "onRenderComplete": null
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

The script can be used as a module in Node.js as well.

## Parameters

- `txt` - The markdown text that will be transformed.
- `elm_container` - The root element to which the output will be appended.

## Options

The third parameter is an object that accepts additional settings for managing the output:

- `codeCopy` (`boolean`) - If `true`, a Copy button is added to each code block. Default value is `true`.
- `streamReply` (`boolean`) - If `true`, the output will be streamed; otherwise, the entire block will be appended to the given root.  Default value is `true`.

### Events and Callback Options

- `abortSignal`: default `null`: Allows interrupt the streaming midway. [More about AbortController](https://developer.mozilla.org/en-US/docs/Web/API/AbortController)

**Example**:

```
const controller = new AbortController();
parseAndRender({  abortSignal: controller.signal  });
```

Once the signal is available if could be used from outside script. Let's asume we have an abort button:

```
  const abortBtn = document.getElementById('myAbortButton');
  const abortHandler = createAbortHandler(controller, abortBtn);
  abortBtn.addEventListener('click', abortHandler);

  function createAbortHandler(controller, abortBtn) {
      return function abortHandler() {
          controller.abort(); // we need a closure here of the previously created controller
          // abortBtn?.removeEventListener('click', abortHandler); // if we don't need it anymore
          console.log("Stream Aborted...');
      };
  }
```

Callbacks can also be attached to these events:

- `onAbort`
- `onRenderStarted`
- `onRendering`: fired at the begining of rendering of each block
- `onRenderComplete`

**Callback Example**:

```
const res = parseAdnRender(txt, rootEl {onRenderComplete: renderCompleteFired});
```

Listeners can be added to these events as well:

- `abort`
- `renderStarted`
- `rendering`
- `renderComplete`

**Listener Example**:
```
rootEl.addEventListener('renderComplete', renderCompleteFired);

function renderCompleteFired(e){
    console.log("Render completed...');
}

const res = parseAdnRender(txt, rootEl );
```

>![Note]
> All event and listeners are attached to the root element passed as a second parameter to the `parseAdnRender`


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
