## 1  Essentials: What HTML _is_

|Concept|Key Points|
|---|---|
|**Definition**|HyperText Markup Language – a declarative language that describes document structure and semantic meaning, interpreted by user agents (browsers, screen readers, crawlers).|
|**Specification**|Maintained as a _Living Standard_ by WHATWG. W3C publishes a snapshot (HTML 5.3).|
|**Syntax**|SGML‑inspired; case‑insensitive element names, start/end tags (`<p>`, `</p>`), attributes in the start tag.|
|**Rendering model**|Browser parses into a DOM tree ➜ rendering, accessibility trees, JS interaction.|

---

## 2  Document Skeleton
```html
<!DOCTYPE html>          <!-- Quirks‑mode guard -->
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>Document title shown in the tab</title>
    <!-- other metadata -->
  </head>
  <body>
    <!-- visible content -->
    <script src="..."></script>
  </body>
</html>

```


- **`<!DOCTYPE html>`** triggers _standards mode_.
    
- **`<html>` attributes**: `lang`, `dir`, `translate`, and any [global attributes](#globalAttrs).
    
- **`<head>`** → metadata nodes only (scripts, styles, meta, base, link, title, noscript).
    
- **`<body>`** → all renderable content & interactive scripts.
    

---

## 3  Global Attributes <a name="globalAttrs"></a>

These are valid on _every_ element unless explicitly forbidden:

|Attribute|Purpose / Notes|
|---|---|
|`accesskey`|Keyboard shortcut.|
|`autocapitalize`|Capitalization hint for virtual keyboards.|
|`class`|Space‑separated tokens for CSS/JS hooks.|
|`contenteditable` (`true`/`false`)|Makes element editable.|
|`data-*`|Custom data attributes (dataset API).|
|`dir`|Text direction: `ltr`, `rtl`, `auto`.|
|`draggable`|Drag‑and‑drop hint.|
|`hidden`|Boolean; participates in the _hidden_ styling/interaction heuristic.|
|`id`|Unique document‑wide identifier.|
|`inert`|(Experimental) removes from accessibility & focusing order.|
|`is`|For customized built‑in elements (Web Components).|
|`itemid`, `itemprop`, `itemref`, `itemscope`, `itemtype`|Microdata vocabulary hooks.|
|`lang`|BCP 47 language tag for locale.|
|`part`|Shadow DOM styling hook.|
|`slot`|Assign nodes to a `<slot>` in Shadow DOM.|
|`spellcheck`|`true`/`false`.|
|`style`|Inline CSS.|
|`tabindex`|Focus order.|
|`title`|Tooltip & accessibility label.|
|`translate`|`yes`/`no` content translation hint.|

---

## 4  Event‑Handler Content Attributes (JS hooks)

`onclick`, `onchange`, `oninput`, `onload`, `onsubmit`, _etc._ – every DOM event type has a matching `on…` attribute whose value is inline JavaScript.

---

## 5  Element Reference by Category

Below, every **bold tag** is followed by ⚙️ for notable _element‑specific_ attributes (excluding global/event). Obsolete/deprecated tags are in ~~strikethrough~~.

### 5.1  Metadata (_allowed only inside `<head>`_)

|Tag|Description|⚙️ Specific Attributes|
|---|---|---|
|**`<base>`**|Sets base URL for relative links.|`href`, `target`|
|**`<link>`**|External resource hint _(CSS, icons, preload, etc.)_.|`rel`, `href`, `as`, `crossorigin`, `type`, `media`, `sizes`, `imagesrcset`, `integrity`, `hreflang`, `referrerpolicy`|
|**`<meta>`**|Generic metadata / HTTP‑equiv.|`name`, `content`, `http-equiv`, `charset`|
|**`<style>`**|Embedded CSS.|`media`, `type`|
|**`<title>`**|Document title.|_(none)_|

### 5.2  Sectioning & Document Outline

|Tag|Purpose|⚙️|
|---|---|---|
|**`<body>`**|Document body root|`onafterprint` … `onunload`, `background` (obsolete)|
|**`<article>`**|Independent, self‑contained composition|—|
|**`<section>`**|Thematic grouping with optional heading|—|
|**`<nav>`**|Major navigation links|—|
|**`<aside>`**|Tangential content (sidebars, pull quotes)|—|
|**`<header>`**, **`<footer>`**|Intro/ outro for nearest sectioning ancestor|—|
|**`<h1>` … `<h6>`**|Headings|`align` (obsolete)|
|**`<address>`**|Contact information|—|
|~~`<hgroup>`~~|(Dropped; use heading levels)||

### 5.3  Text Content

|Tag|Purpose|⚙️|
|---|---|---|
|**`<p>`**|Paragraph|—|
|**`<hr>`**|Thematic break|—|
|**`<pre>`**|Preformatted text|`width` (obsolete)|
|**`<blockquote>`**|Extended quotation|`cite`|
|**`<ol>`**, **`<ul>`**, **`<li>`**|Ordered/unordered list|`type`, `start`, `reversed` (`ol`)|
|**`<dl>`**, **`<dt>`**, **`<dd>`**|Description list|—|
|**`<figure>`**, **`<figcaption>`**|Self‑contained illustration & caption|—|
|**`<div>`**|Generic flow container|—|

### 5.4  Inline Text Semantics

|Tag|Meaning|⚙️|
|---|---|---|
|**`<a>`**|Hyperlink|`href`, `target`, `rel`, `download`, `referrerpolicy`, `type`, `hreflang`, `ping`|
|**`<em>`**, **`<strong>`**|Emphasis / importance|—|
|**`<small>`**, **`<sub>`**, **`<sup>`**|Side comments, subscripts, superscripts|—|
|**`<br>`**|Line break|`clear` (obsolete)|
|**`<span>`**|Generic inline container|—|
|**`<code>`**, **`<kbd>`**, **`<var>`**, **`<samp>`**|Computer code, keyboard input, variables, sample output|—|
|**`<mark>`**|Highlight|—|
|**`<time>`**|Machine‑readable date/time|`datetime`|
|**`<b>`**, **`<i>`**, **`<u>`**, **`<s>`**|No semantic emphasis, stylistic|`align` (obsolete)|
|**`<abbr>`**|Abbreviation|`title` for expansion|
|**`<cite>`**|Citation of a creative work|—|
|**`<q>`**|Short inline quote|`cite`|
|**`<data>`**|Machine‑readable equivalent|`value`|
|**`<ruby>`**, **`<rt>`**, **`<rp>`**|East‑Asian pronunciation guides|—|
|**`<bdi>`**, **`<bdo>`**|Bi‑directional text isolator/override|`dir`|
|**`<wbr>`**|Word‑break opportunity|—|

### 5.5  Images & Multimedia

|Tag|Role|⚙️|
|---|---|---|
|**`<img>`**|Raster/ vector inline|`src`, `alt`, `srcset`, `sizes`, `crossorigin`, `usemap`, `referrerpolicy`, `loading`, `decoding`, `width`, `height`|
|**`<picture>`**|Responsive art‑direction container|—|
|**`<source>`**|Media source for `<picture>`, `<audio>`, `<video>`|`src`, `srcset`, `sizes`, `type`, `media`|
|**`<audio>`**, **`<video>`**|Media playback|`src`, `controls`, `autoplay`, `loop`, `muted`, `preload`, `poster` (video), `width`, `height`|
|**`<track>`**|Timed text (captions, subtitles)|`kind`, `src`, `srclang`, `label`, `default`|
|**`<map>`**, **`<area>`**|Image map hotspots|`name` (`map`); `shape`, `coords`, `href`, `alt`, `target`, `download`, `rel`, `referrerpolicy` (`area`)|
|~~`<embed>`~~ (use `<iframe>`/ `<img>`/ `<object>`), **`<object>`**, **`<param>`**|Generic embedded resource; legacy plug‑in support.||

### 5.6  Embedded & Interactive Content

|Tag|Description|⚙️|
|---|---|---|
|**`<iframe>`**|Nested browsing context|`src`, `srcdoc`, `name`, `sandbox`, `allow`, `allowfullscreen`, `referrerpolicy`, `loading`|
|**`<canvas>`**|Bitmap drawing surface (JS API)|`width`, `height`|
|**`<svg>`**|Inlined Scalable Vector Graphics|(SVG attribute set)|
|**`<math>`**|Inlined MathML|(MathML attributes)|
|**`<details>`**, **`<summary>`**|Disclosure widget|`open` (`details`)|
|**`<dialog>`**|Modal / non‑modal dialog|`open`|
|**`<menu>`**, **`<menuitem>`** (obsolete)|Context menus|—|
|**`<slot>`**, **`<template>`**|Web Component shadow DOM slots & inert templates|`name` (`slot`)|

### 5.7  Forms & Input Controls

|Tag|Role|⚙️ Key Attributes (beyond global)|
|---|---|---|
|**`<form>`**|Form container|`action`, `method`, `enctype`, `autocomplete`, `novalidate`, `target`, `rel`|
|**`<fieldset>`**, **`<legend>`**|Group controls|`disabled`, `form`, `name`|
|**`<label>`**|Caption for a control|`for`|
|**`<input>`**|Versatile single‑line control|`type` (`text` default + _155+_ others), `name`, `value`, `placeholder`, `required`, `pattern`, `min`, `max`, `step`, `list`, `size`, `autocomplete`, `multiple`, `accept`, `checked`, `readonly`, `disabled`, `form`, `height`, `width`|
|**`<textarea>`**|Multiline text|`rows`, `cols`, `wrap`|
|**`<select>`**, **`<optgroup>`**, **`<option>`**|Drop‑down / listbox|`multiple`, `size`, `disabled`, `selected`, `label`, `value`|
|**`<datalist>`**|Autocomplete suggestions|`id` linked to `list` attr on `<input>`|
|**`<button>`**|Pushbutton|`type` (`submit`, `reset`, `button`), `disabled`, `name`, `value`, `form`|
|**`<output>`**|Calculation result|`for`, `name`|
|**`<progress>`**|Task completion bar|`max`, `value`|
|**`<meter>`**|Scalar measurement within a known range|`min`, `max`, `low`, `high`, `optimum`, `value`|
|**`<selectlist>`** (experimental)|Native select‑menu fallback for custom UI||

### 5.8  Table Content

|Tag|Purpose|⚙️|
|---|---|---|
|**`<table>`**|Tabular data root|`border`, `summary` (obsolete), `width`|
|**`<caption>`**|Title for the table|—|
|**`<colgroup>`**, **`<col>`**|Column metadata|`span`, `width`|
|**`<thead>`**, **`<tbody>`**, **`<tfoot>`**|Row groupings|—|
|**`<tr>`**|Table row|—|
|**`<th>`**, **`<td>`**|Header / data cell|`colspan`, `rowspan`, `headers`, `scope`, `abbr`|

### 5.9  Edits & Annotations

|Tag|Function|⚙️|
|---|---|---|
|**`<ins>`**, **`<del>`**|Inserted / removed content|`cite`, `datetime`|
|**`<mark>`**|Highlight|—|

### 5.10  Scripting

|Tag|Role|⚙️|
|---|---|---|
|**`<script>`**|Inline or external JS/JSON/GraphQL/...|`src`, `type`, `async`, `defer`, `nomodule`, `crossorigin`, `integrity`, `referrerpolicy`, `nonce`|
|**`<noscript>`**|Fallback when JS disabled.|—|

### 5.11  Web Components / Custom Elements

- **`<template>`** inert DOM fragment.
    
- **`<slot>`** named insertion point.
    
- `is="x-button"` attribute for _customized built‑in_ elements.
    
- `customElements.define('x-widget', class extends HTMLElement { … })` via JavaScript.
    

---

## 6  Deprecated & Obsolete Elements/Attributes

|Category|Examples / Modern Replacement|
|---|---|
|_Presentation_|~~`<font>`~~ (`CSS font-family`), ~~`<center>`~~ (`text-align:center`), ~~`<big>`~~ (`font-size`), `align`, `border`, `bgcolor` ⇒ CSS.|
|_Framesets_|~~`<frameset>`, `<frame>`, `<noframes>`~~ – use `<iframe>` or CSS layout.|
|_Plug‑in_|~~`<applet>`~~ (use `<iframe>` or `<object>` for legacy), ~~`<bgsound>`~~.|
|_Interactions_|~~`<keygen>`~~ replaced by WebCrypto API.|
|_Scripting_|`language` attr on `<script>` (use `type`).|

Browsers still parse many of these for backward compatibility but they are **invalid in modern HTML** and should be avoided.

---

## 7  ARIA & Accessibility Checklist

- **ARIA roles (`role="navigation"`, `role="dialog"` …)** expand semantics when native element doesn’t convey meaning.
    
- **ARIA properties & states** like `aria‑label`, `aria‑expanded`, `aria‑pressed` mirror widget state.
    
- _Rule of thumb_: **Prefer native elements** because they carry built‑in semantics & keyboard behavior.
    

---

## 8  Microdata, RDFa & JSON‑LD

- **Microdata** attributes (`itemscope itemtype itemprop`) embed structured data directly.
    
- **RDFa** uses `typeof`, `property` etc.
    
- **JSON‑LD** `<script type="application/ld+json">` is the recommended way for search‑engine schema.
    

---

## 9  Authoring Best Practices

1. **Semantic first** – choose the element that conveys meaning, not appearance.
    
2. **Separation of concerns** – presentation in CSS, behavior in JS.
    
3. **Progressive enhancement** – functional without JS; then layer interactivity.
    
4. **Accessibility** – proper headings outline, alt text, form labels, ARIA where necessary.
    
5. **Performance** – use `async`/`defer` on scripts, `loading="lazy"` on images/iframes, `preload`/`prefetch` as hints.
    
6. **Validation** – use the W3C/WHATWG validator to catch structural errors.
    

---

## 10  Common Character References

`&lt;` `<`, `&gt;` `>`, `&amp;` `&`, `&quot;` `"`, `&apos;` `'` plus 2 000+ named entities (e.g., `&copy;`, `&nbsp;`, `&euro;`).  
_Numeric forms_ `&#169;` (decimal) or `&#xA9;` (hex) work universally.

---

## 11  HTML APIs You’ll Meet in JS

|API|Quick Note|
|---|---|
|**DOM**|`document.querySelector`, `createElement`, `appendChild`.|
|**Custom Elements**|`window.customElements.define`.|
|**Shadow DOM**|`attachShadow({mode:'open'})`.|
|**Canvas 2D / WebGL / WebGPU**|Graphics.|
|**Media**|`HTMLMediaElement`, `MediaStream`, `WebAudio`.|
|**Drag & Drop**|`dragstart`, `drop` events.|
|**Fullscreen / Screen Orientation**|Immersive experiences.|
|**IntersectionObserver**|Lazy‑loading, in‑view tracking.|

---

## 12  HTML vs. XHTML

- XHTML = HTML syntax expressed as _XML_; served as `application/xhtml+xml`.
    
- Requires self‑closing syntax `<br/>`, well‑formedness, lower‑case tags.
    
- Modern best practice: **use regular HTML or _polyglot_ syntax** unless you need strict XML tooling.
    

---

## 13  Cheat‑Sheet: Key Attribute Groups

- **Fetch‑related**: `crossorigin`, `integrity`, `referrerpolicy`.
    
- **Lazy loading**: `loading="lazy"`, `decoding="async"`.
    
- **Form association**: `form`, `formaction`, `formenctype` on outside‑form elements.
    
- **Security / sandbox**: `<iframe sandbox="allow-scripts">`, `rel="noopener noreferrer"` on links.
    

---

## 14  Further Study Checklist

1. **MDN element reference** – canonical descriptions & live examples.
    
2. **HTML Living Standard** – for edge‑case details & algorithmic parsing rules.
    
3. **ARIA Authoring Practices Guide (APG)** – building accessible custom widgets.
    
4. **Lighthouse / Web Vitals** – measure performance & accessibility.
    

---

### 🗝️ Key Takeaways

- **Choose semantics** → better SEO, accessibility, maintainability.
    
- **All elements can carry global attributes**, then optionally their own specials.
    
- **Obsolete presentational markup** survived for legacy pages but should be replaced by CSS.
    
- **HTML is living** – new attributes like `fetchpriority`, `popover`, `enterkeyhint` appear over time; stay updated via WHATWG change logs.
    



Below is a _developer‑oriented mini handbook_ for the 15 HTML elements you’ll touch **every single day**.  
For each tag you get:

1. **Primary role / semantics** – what it _means_.
    
2. **Content model** – what you’re allowed to nest inside.
    
3. **Essential attributes** – the handful that matter 99 % of the time.
    
4. **Browser defaults** (display + margins).
    
5. **Accessibility / SEO tips** – how it’s announced to assistive tech & crawlers.
    
6. **Gotchas & best‑practice snippet**.
    

---

## 1. `<!DOCTYPE html>`

|||
|---|---|
|**Role**|Signals the HTML Living Standard to the parser; forces _standards mode_.|
|**Attributes**|_None_|
|**Gotcha**|Must be the **first** line, no spaces before it. Older doctypes (`<!DOCTYPE HTML PUBLIC…>`) are obsolete.|

---

## 2. `<html>`

|||
|---|---|
|**Semantics**|Root element of the document.|
|**Content model**|Exactly one `<head>` + one `<body>`.|
|**Key attrs**|`lang="en"`, `dir="ltr"` or `rtl`, `[translate]`|
|**Accessibility**|Screen readers use `lang` to pick TTS voice.|
|**Snippet**|`<html lang="en" dir="ltr">…</html>`|

---

## 3. `<head>`

Holds metadata—not rendered.

| **Common children** | `<meta>`, `<title>`, `<link>`, `<script>`, `<style>`, `<base>` |  
| **Tip** | Put `<meta charset="utf-8">` first for fastest encoding detection. |

---

## 4. `<body>`

|||
|---|---|
|**Semantics**|All visible/interactive content.|
|**Default display**|Block, margin = 0.|
|**Event attrs**|`onload`, `onunload`, `onafterprint` (rarely used today).|
|**Best practice**|Keep `<script>` tags at the _end_ or add `defer`/`async`.|

---

## 5. `<div>`

|||
|---|---|
|**Semantics**|_None_ – generic block‑level wrapper.|
|**Attrs**|Only global (`class`, `id`, `data-*`, …).|
|**Display**|`block` with full‑width stretch.|
|**Gotcha**|Overuse ⇒ “div‑itis.” Prefer semantic tags (`<section>`, `<header>`, …) when meaning exists.|
|**Snippet**|`<div class="card">…</div>`|

---

## 6. `<span>`

Inline counterpart to `div`.

| **Display** | `inline`; no width/height margins respected. |  
| **Use when** | You need a hook _inside_ a line of text. |  
| **Example** | `Welcome, <span class="username">Shashank</span>!` |

---

## 7. `<p>`

|||
|---|---|
|**Semantics**|Paragraph of prose.|
|**Content model**|_Phrasing_ content only (no another `<p>` by spec). Browsers auto‑close preceding `<p>` when you open a new block element.|
|**Default CSS**|`display:block; margin:1em 0;`|
|**SEO**|Search engines treat each `<p>` as a textual unit—good for readability.|

---

## 8. `<a>`

|||
|---|---|
|**Semantics**|Hyperlink / interactive anchor.|
|**Inline vs. block**|`a` is _inline by default_ but can be block‑level in HTML 5.|
|**Essential attrs**|`href`, `target="_blank"`, `rel="noopener noreferrer"`, `download`, `aria-label`.|
|**Accessibility**|Content between tags becomes link text—keep it descriptive (not “click here”).|
|**Snippet**|`<a href="https://example.com" rel="noopener" target="_blank">Docs ↗︎</a>`|

---

## 9. `<img>`

|||
|---|---|
|**Semantics**|Embeds a raster/vector image that is _part of the content_ (not decoration).|
|**Required attrs**|`src`, `alt`.|
|**Responsive attrs**|`srcset`, `sizes`, `loading="lazy"`|
|**Display**|`inline-block`, baseline‑aligned.|
|**Accessibility**|`alt=""` (empty) marks a _purely decorative_ image.|
|**Pitfall**|Missing `alt` causes screen readers to read the file name.|

---

##10. Heading elements `<h1>` … `<h6>`

|||
|---|---|
|**Semantics**|Section titles; they create the _outline_.|
|**Default CSS**|Large bold block with margins.|
|**Accessibility**|Screen readers expose heading hierarchy; don’t skip from `h1` to `h4`.|
|**Best practice**|One `<h1>` per page (not enforced but recommended).|

---

##11. `<section>`, `<article>`

||`<section>`|`<article>`|
|---|---|---|
|**Meaning**|Thematic grouping of content, usually with own heading.|Self‑contained piece intended for reuse (syndication, RSS, etc.).|
|**ARIA role**|`region` if it has an accessible name.|`article`|
|**SEO**|`<article>` is favored for blog posts, forum entries.||

---

##12. `<nav>`

|||
|---|---|
|**Semantics**|Major site navigation block.|
|**Best practice**|Put a heading `<h2 class="sr-only">Site Navigation</h2>` inside for screen readers if the link list has no visible title.|

---

##13. `<form>` & core controls (`input`, `label`, `button`)

### `<form>`

_Attributes_: `action`, `method="post|get"`, `autocomplete`, `novalidate`, `target`, `enctype`.

### `<input type="…">` cheat sheet

|Type|Purpose|Bonus attrs|
|---|---|---|
|`text`|single‑line text|`maxlength`, `placeholder`|
|`email`|validated email list|`multiple`|
|`number`|numeric spinner|`min`, `max`, `step`|
|`checkbox`/`radio`|binary / exclusive pick|`checked`, `value`|
|`date`, `time`, `datetime-local`, `month`, `week`|calendar pickers|`min`, `max`, `step`|
|`file`|file chooser|`accept="image/*"`, `multiple`|

`<label for="id">` wires caption ↔ control, enlarging click target and improving accessibility.

### `<button>`

Default `type` is **submit** inside a form—declare `type="button"` if you only need JS handler.

---

##14. `<script>` & `<link>`

|`<script>`|`<link>` (CSS, preload, icon)|
|---|---|
|`src`, `type`, `defer`, `async`, `nomodule`, `crossorigin`, `integrity`|`rel="stylesheet"`, `"preload"`, `"icon"`, `"manifest"`; `href`, `as`, `media`, `integrity`|
|`defer` waits until HTML parsed; `async` executes as soon as fetched.|Place CSS early so it blocks render less (HTTP/2 push or preload).|

---

##15. `<table>`, `<tr>`, `<th>`, `<td>`

|||
|---|---|
|**Semantics**|_Tabular data_ (not layout!).|
|**Minimal structure**|`<table><thead><tr><th>…` then `<tbody><tr><td>`|
|**Accessibility**|Use `<caption>` for title; `<th scope="row|
|**CSS tip**|`border-collapse:collapse` for cleaner borders.|

---

### Quick “When should I use X vs. Y?”

|Task|Use this element|
|---|---|
|Group unrelated widgets just for CSS grid/flex|`div`|
|Stand‑alone article, blog post, comment|`article`|
|Top nav bar or side menu|`nav`|
|Highlight inline code|`code`|
|Emphasize a _word_|`em` (stress) or `strong` (importance)|
|Visually hidden but screen‑reader visible text|`<span class="sr-only">…</span>` (CSS clip technique)|

---

## Closing Tips

1. **Add semantic heading hierarchy before styling** – you can change fonts later.
    
2. **Every form control must have an associated `<label>`** (except buttons).
    
3. **Images: think “Could I replace it with text?”** If yes, that text is your `alt`.
    
4. **Avoid presentational attributes** (`align`, `bgcolor`) – do it in CSS.
    
5. **Validate** via [https://validator.w3.org/nu/](https://validator.w3.org/nu/) to catch accidental unclosed tags.
    

Master these core tags and attributes, and 80 % of everyday HTML authoring will feel effortless.