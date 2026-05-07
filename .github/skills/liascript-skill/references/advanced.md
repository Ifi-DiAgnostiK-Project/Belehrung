# LiaScript Advanced Reference

This document covers advanced LiaScript features including macros, scripting, imports, and complex quiz configurations.

## Table of Contents

1. [Macros](#macros)
2. [Scripting](#scripting)
3. [Importing Courses](#importing-courses)
4. [Quiz Configuration](#quiz-configuration)
5. [Code Execution Templates](#code-execution-templates)
6. [Styling & Attributes](#styling--attributes)
7. [HTML Integration](#html-integration)

---

## Full Metadata Reference

All available header fields:

```markdown
<!--
author:   Name
email:    email@example.com
version:  1.0.0
language: en
narrator: US English Female

comment:  Course description (shown in preview cards)
logo:     URL to course logo/image
icon:     URL to custom favicon

mode:     Presentation  (default mode: Textbook | Presentation | Slides)
dark:     true          (default to dark theme)

classroom: disable      (hide real-time classroom button; use "enable" in SCORM exports)
sharing:   false        (hide the share button)

persistent: true        (keep slide DOM alive when navigating away)

translateWithGoogle: false
translation: Deutsch translations/German.md

font:       Noto Sans, Roboto   (Google Fonts names, comma-separated)
repository: https://github.com/user/repo
edit:       true                (show edit button linking to live editor)

import:   URL to macro template
import:   URL to second template (multiple allowed)
link:     URL to external CSS
link:     URL to second stylesheet (multiple allowed)
script:   URL to external JavaScript
script:   URL to second script (multiple allowed)

@onload
// JS executed once when the course initializes
@end
-->
```

---

## Macros

Macros are reusable text substitutions defined in the header.

### Simple Macros

```markdown
<!--
@author: Dr. Jane Smith

@greeting: Hello and welcome to this course!

@important: **⚠️ Important:** 
-->

# My Course

@greeting

@important This concept is crucial for the exam.
```

### Parameterized Macros

```markdown
<!--
@highlight: <span style="background: @0; padding: 2px 5px;">@1</span>

@youtube: !?[Video](@0)
-->

# Examples

This is @highlight(yellow,highlighted text) in the paragraph.

Watch this explanation:
@youtube(https://www.youtube.com/watch?v=dQw4w9WgXcQ)
```

### Multi-line Macros

```markdown
<!--
@note
<div class="note">

**📝 Note:** @0

</div>
@end
-->

@note(This is an important note that spans multiple lines and can contain **formatting**.)
```

---

## Reactive Scripts (`<script>` Inline Elements)

Inline `<script>` tags are interactive elements — they render their return value directly in the page and re-execute whenever their inputs change.

### Interactive Inputs

Attach an `input` attribute to turn the script into a UI control. The current value is available as `@input`:

```markdown
Slider: <script input="range" min="0" max="100" value="50" output="myVal">@input</script>

Text:   <script input="text" value="hello">
"You typed: @input"
</script>

Number: <script input="number" min="0" max="1000" value="1">
let i = @input
"Square: " + i * i
</script>
```

Common `input` types: `range`, `text`, `number`, `button`, `submit`, `select`.

### Linking Scripts Together

Use `output="name"` on one script and `@input(\`name\`)` in another. The second script re-runs whenever the first changes:

```markdown
$a =$ <script input="range" min="1" max="10" value="2" output="a">@input</script>
$b =$ <script input="range" min="1" max="10" value="3" output="b">@input</script>

<script run-once>
"Result: " + (@input(`a`) * @input(`b`))
</script>
```

`run-once` means the script only re-executes when its referenced `@input(...)` values change, not on every page render.

### Return Types

The last expression determines what is rendered:

```markdown
<script>"Hello World"</script>

<script>"HTML: <b>bold text</b>"</script>

<script>"LIASCRIPT: ## Dynamic Heading"</script>
```

### Async Results (`send.lia`)

For async operations (fetch, setTimeout), return `"LIA: wait"` immediately and send the result later:

```markdown
<script>
fetch("https://api.example.com/data")
  .then(r => r.json())
  .then(d => send.lia("LIASCRIPT: **" + d.value + "**"))
  .catch(() => send.lia("error loading data"))

"LIA: wait"
</script>
```

### Script Attributes

| Attribute | Description |
|-----------|-------------|
| `input` | Input type: `range`, `text`, `number`, `button`, `submit`, `select` |
| `value` | Default input value |
| `output` | ID for referencing this script's value from another script |
| `run-once` | Re-execute only when referenced `@input(...)` values change |
| `modify` | Allow users to edit the script source |

---

## Importing Courses

Import macros and styles from other LiaScript courses:

```markdown
<!--
import: https://raw.githubusercontent.com/LiaTemplates/Pyodide/main/README.md

import: https://raw.githubusercontent.com/LiaPlayground/LiaScript_Tutorial_Kigali/main/README.md
-->
```

### Popular Template Imports

| Template | URL | Description |
|----------|-----|-------------|
| Pyodide | `LiaTemplates/Pyodide` | Run Python in browser |
| Processing | `LiaTemplates/processing` | Processing.js graphics |
| Algebrite | `LiaTemplates/Algebrite` | Computer algebra |
| mermaid | `LiaTemplates/mermaid` | Mermaid diagrams |
| vtk | `LiaTemplates/vtk` | 3D visualization |

Usage after import:
```markdown
```python
print("Hello from Python!")
for i in range(5):
    print(f"Count: {i}")
```
@Pyodide.eval
```

---

## Quiz Configuration

### Quiz Attributes

Control quiz behavior with HTML comment attributes:

```markdown
<!-- data-randomize data-max-trials="3" -->
What is 2+2?

[( )] 3
[(X)] 4
[( )] 5
```

Available attributes:

| Attribute | Values | Description |
|-----------|--------|-------------|
| `data-randomize` | (flag) | Shuffle options |
| `data-max-trials` | number | Auto-solve after N wrong attempts |
| `data-solution-button` | on/off/number | Control solution button visibility |
| `data-hint-button` | on/off/number | Control hint button visibility |
| `data-show-partial-solution` | true/false | Highlight correct/incorrect in matrix quizzes |
| `data-score` | number | SCORM scoring weight |

### Custom Quiz Validation (JavaScript)

```markdown
What is the answer to life, the universe, and everything?

[[42]]
<script>
  // @input is the user's answer
  let answer = @input.trim().toLowerCase();
  
  if (answer === "42" || answer === "forty-two" || answer === "forty two") {
    true  // Correct
  } else if (answer.includes("4") && answer.includes("2")) {
    "Getting warmer! It's just the number."
  } else {
    false  // Incorrect
  }
</script>
```

---

## Code Execution Templates

### JavaScript (Built-in)

````markdown
```javascript
console.log("Hello!");
```
<script>@input</script>
````

### HTML Preview

````markdown
```html
<button onclick="alert('Clicked!')">Click me</button>
```
@Eval.runHTML
````

### Custom Execution with Output

````markdown
```python  main.py
x = 10
y = 20
print(f"Sum: {x + y}")
```
```text  -output
```
<script>
  // Send to external API, process, etc.
  send.handle("output").exec();
</script>
````

---

## Styling & Attributes

### Block-level Styling

Apply CSS to entire blocks:

```markdown
<!-- style="color: red; font-size: 1.5em;" -->
This entire paragraph is red and larger.

<!-- style="background: #f0f0f0; padding: 1em; border-radius: 8px;" -->
This is a styled box with padding and rounded corners.
```

### Inline Styling

```markdown
This word is <!-- style="color: blue;" -->blue<!-- style -->  normal again.
```

### Custom Classes

Define in header, use in content:

```markdown
<!--
link: https://your-styles.css

style: 
  .warning { 
    background: #fff3cd; 
    border-left: 4px solid #ffc107; 
    padding: 1em; 
  }
-->

<!-- class="warning" -->
This is a warning message!
```

---

## Text Shortcuts

### Arrow Shortcuts

```markdown
-> ->> >-> <- <-< <<- <-> => <= <=>
--> <-- <--> ==> <== <==>
~> <~
```

### Smiley Shortcuts

```markdown
:-) ;-) :-D :-O :-( :-| :-/ :-P :-* :') :'(
```

---

## HTML Integration

### Inline HTML

```markdown
This is <b>bold</b> and <span style="color:red">red</span>.
```

### Block HTML

```markdown
<div style="display: flex; gap: 1em;">

![Image 1](url1)

![Image 2](url2)

</div>
```

### Preserving Raw HTML

Use `<lia-keep>` to prevent LiaScript parsing:

```markdown
<lia-keep>
<table border="1">
  <tr><td>Raw HTML table</td></tr>
</table>
</lia-keep>
```

---

## Special Elements

### Footnotes

```markdown
This has a footnote[^1] and another[^note].

[^1]: First footnote content.
[^note]: Named footnote content.
```

### Abbreviations

```markdown
The HTML specification is maintained by the W3C.

*[HTML]: Hyper Text Markup Language
*[W3C]: World Wide Web Consortium
```

### Details/Summary (Collapsible)

```markdown
<details>
<summary>Click to expand</summary>

Hidden content that appears when expanded.

- Can include
- Any markdown

</details>
```

---

## Exporting Courses

LiaScript courses can be exported using the CLI exporter:

```bash
npx @liascript/exporter -i course.md -o output/ --format scorm
```

Export formats:
- `scorm` - SCORM 1.2 package for LMS
- `scorm2004` - SCORM 2004 package
- `ims` - IMS Content Package
- `pdf` - PDF document
- `web` - Standalone web folder

---

## SVG Graphics

### Inline SVG

Write raw `<svg>` tags directly in the Markdown — LiaScript renders them as vector graphics:

```markdown
<svg viewBox="0 0 200 100">
  <circle cx="50" cy="50" r="40" fill="lightblue" stroke="blue" stroke-width="2"/>
  <text x="50" y="55" font-size="10" text-anchor="middle">Circle</text>

  <rect x="110" y="10" width="80" height="80" fill="lightgreen" stroke="green" stroke-width="2"/>
  <text x="150" y="55" font-size="10" text-anchor="middle">Rectangle</text>
</svg>
```

SVG scales to full available width automatically.

### Embedding LiaScript Inside SVG (`<foreignObject>`)

Use `<foreignObject>` to place rendered Markdown or math at specific coordinates inside an SVG. Always define `x`, `y`, `width`, and `height`:

```markdown
<svg viewBox="0 0 280 200">

<foreignObject x="130" y="0" width="150" height="80">
Circumference:

$$C = 2 \pi r$$
</foreignObject>

<circle cx="100" cy="100" r="80" fill="lightblue" stroke="blue" stroke-width="2"/>
<line x1="100" y1="100" x2="180" y2="100" stroke="red" stroke-width="2"/>

<foreignObject x="55" y="110" width="100" height="80">
Area:

$$A = \pi r^2$$
</foreignObject>

</svg>
```

Any LiaScript content works inside `<foreignObject>`: math, animations, quizzes, or even other SVGs.

---

## JSON Model (For AI Generation)

LiaScript provides a JSON schema for generating courses programmatically. Use the `@liascript/markdownify` npm package:

```javascript
import liascriptify from '@liascript/markdownify'

const course = {
  meta: {
    author: "AI Assistant",
    language: "en"
  },
  sections: [
    {
      title: "Introduction",
      indent: 1,
      body: [
        "Welcome to this course!",
        {
          type: "Quiz",
          quizType: "single-choice",
          body: ["Option A", "Option B", "Option C"],
          solution: 1
        }
      ]
    }
  ]
}

const markdown = await liascriptify(course)
```

This is useful for programmatic course generation or AI pipelines.
