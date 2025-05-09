## 1  Essentials: What HTML _is_

|Concept|Key Points|
|---|---|
|**Definition**|HyperText Markup Language – a declarative language that describes document structure and semantic meaning, interpreted by user agents (browsers, screen readers, crawlers).|
|**Specification**|Maintained as a _Living Standard_ by WHATWG. W3C publishes a snapshot (HTML 5.3).|
|**Syntax**|SGML‑inspired; case‑insensitive element names, start/end tags (`<p>`, `</p>`), attributes in the start tag.|
|**Rendering model**|Browser parses into a DOM tree ➜ rendering, accessibility trees, JS interaction.|

---

## 2  Document Skeleton

`<!DOCTYPE html>          <!-- Quirks‑mode guard --> <html lang="en">   <head>     <meta charset="utf-8">     <meta name="viewport" content="width=device-width,initial-scale=1">     <title>Document title shown in the tab</title>     <!-- other metadata -->   </head>   <body>     <!-- visible content -->     <script src="..."></script>   </body> </html>`

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
    

These notes should cover virtually every element and its primary attributes while giving you contextual guidance on best usage. Keep them as your pocket reference whenever you code or review HTML documents. Happy markup!