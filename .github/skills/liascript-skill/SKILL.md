---
name: liascript-course
description: Create fully interactive, offline-capable online courses using LiaScript Markdown. Use this skill whenever users want to create educational content, online courses, e-learning materials, interactive tutorials, quizzes, presentations with animations, or any learning materials. Triggers include mentions of "course", "lesson", "tutorial", "quiz", "learning module", "educational content", "LiaScript", "OER" (Open Educational Resources), "SCORM", "interactive slides", "e-learning", or requests for teaching materials with animations, text-to-speech, or self-assessment. Also use when converting existing documents into interactive learning formats or when users want to add quizzes, surveys, or executable code blocks to educational content.
---

# LiaScript Course Creator

LiaScript is an extended Markdown dialect that transforms plain text into fully interactive, offline-capable online courses rendered directly in the browser. This skill enables creation of professional educational content with quizzes, animations, text-to-speech, executable code, and more.

## Quick Start

Every LiaScript course is a single Markdown file with a header comment containing metadata:

```markdown
<!--
author: Your Name
email: your@email.com
version: 1.0.0
language: en
narrator: US English Female

comment: A brief description of your course.
-->

# Course Title

First section content...

## Subsection

More content with interactive elements...
```

## Core Concepts

### Document Structure

- **Sections**: Created with `#` headings (each becomes a "slide")
- **Subsections**: Use `##`, `###`, etc. for nested content
- **Blocks**: Paragraphs, lists, tables, code, etc. separated by blank lines

### Local Sub-Titles (No TOC Entry)

Use underline syntax for headings that appear visually but are **not added to the table of contents**:

```markdown
## Section Title

Local Subsection
================

Local Sub-SubSection
--------------------
```

`=` creates a heading one level below the current section; `-` creates one two levels below.

### Three Display Modes

LiaScript supports three presentation modes users can switch between:
1. **Textbook**: All content visible, no animations
2. **Presentation**: Animations with text-to-speech narration
3. **Slides**: Animations without spoken text (captions shown)

---

## Semantic HTML Tags

### Multiple Headings on One Slide

Each `#` heading starts a new slide. To place multiple subheadings on the **same slide** without splitting it, wrap them in `<section>` or `<article>`:

```markdown
# Slide Title

<section>
## Part One

Content here...
</section>

<article>
## Part Two

More content here...
</article>
```

Use `<section>` for grouping related content, `<article>` for self-contained blocks. Both produce the same visual result — the difference is semantic.

### Preventing Markdown Parsing (`<lia-keep>`)

Wrap raw HTML in `<lia-keep>` to prevent LiaScript from parsing it as Markdown. Useful for complex HTML tables, custom styles, or any HTML where indentation and formatting must be preserved exactly:

```markdown
<lia-keep>
  <style>
    table, td { border: 1px solid black; padding: 8px; }
  </style>
  <table>
    <tr><td>Cell 1</td><td rowspan="2">Cell 2</td></tr>
    <tr><td>Cell 3</td></tr>
  </table>
</lia-keep>
```

---

## Quizzes

LiaScript provides powerful quiz types. Always place quiz elements on their own line with blank lines before/after.

### Text Input Quiz

```markdown
What is the capital of France?

[[Paris]]
```

### Single Choice Quiz

```markdown
What is 2 + 2?

[( )] 3
[(X)] 4
[( )] 5
```

### Multiple Choice Quiz

```markdown
Which are programming languages?

[[X]] Python
[[X]] JavaScript
[[ ]] HTML
[[ ]] CSS
```

### Selection Quiz (Dropdown)

Inline dropdown — wrap the correct option in `(...)`, options separated by `|`:

```markdown
The sky is usually [[ (blue) | red | green ]].
```

### Matrix Quiz

The header row defines the column labels (use `[[ ]]` double brackets to wrap the whole header). Each body row is a quiz vector:

- `( )` / `(X)` → **single-choice** (radio button) — only one answer per row
- `[ ]` / `[X]` → **multi-choice** (checkbox) — multiple answers per row

```markdown
[[Berlin] [Paris] [Rome]]
[  (X)      ( )    ( )  ] Germany
[  ( )      (X)    ( )  ] France
[  ( )      ( )    (X)  ] Italy
```

### Gap Text Quiz

Embed text-input and dropdown quizzes inline within any paragraph:

```markdown
The capital of France is [[Paris]] and the capital of Germany is [[Berlin]].

The fastest land animal is the [[ (cheetah) | lion | tiger ]].
```

### Gap Text in Any Block

Gap-text works inside any Markdown block — tables, blockquotes, styled paragraphs, even alongside ASCII art:

```markdown
| Verb   | Person | Präsens     | Partizip II    |
|--------|:------:|:-----------:|:--------------:|
| gehen  | Ich    | [[ werde ]] | [[ gegangen ]] |
| sagen  | Du     | [[ wirst ]] | [[ gesagt ]]   |
```

### Generic Quiz (Script-Driven)

Use `[[!]]` for fully custom quiz logic. There is **no input field** — the script itself decides whether the quiz is solved. The last expression must evaluate to `true` (correct) or `false` (incorrect):

```markdown
[[!]]
<script>
  Math.random() < 0.2
</script>
```

The script's last expression must evaluate to `true` (correct) or `false` (incorrect). Use for custom validation, external API checks, or developer-controlled state.

### Quiz Configuration

Add a comment **directly above the quiz options** (not above the question):

```markdown
<!-- data-randomize data-max-trials="3" data-solution-button="off" -->
[(X)] Correct
[( )] Wrong
```

- `data-randomize` — shuffle options on each load
- `data-max-trials="3"` — auto-solve after N wrong attempts
- `data-solution-button="off"` — hide the solve button (`"3"` = show after 3 fails)

### Quiz Hints & Explanations

Add hints with `[[?]]` and explanations with `***`:

```markdown
What year did WW2 end?

[[1945]]
[[?]] It was in the 1940s
[[?]] The war ended in Europe in May
***
World War 2 ended in 1945, with Victory in Europe 
Day on May 8th and Victory over Japan Day on September 2nd.
***
```

---

## Animations & Effects

### Basic Animations

Use `{{step}}` to show content at specific animation steps. Indent the tag with 4+ spaces so other Markdown renderers display it as code (readable fallback):

```markdown
     {{1}}
This appears on step 1.

     {{2}}
This appears on step 2.

     {{3-5}}
This appears on steps 3–5, then disappears.
```

### Grouped Animations

Wrap multiple blocks with a long line of asterisks (use 20+ asterisks as a horizontal rule). Place the animation tag on the line *above* the opening delimiter, with a blank line between the delimiter and content:

```markdown
            {{1-2}}
************************************

Everything in here appears together:

- Item 1
- Item 2
- A whole table or image

************************************
```

Alternatively, use `<section>` or `<article>` HTML tags as group delimiters:

```markdown
     {{2}}
<section>

Content block 1.

Content block 2.

</section>
```

### Inline Effects

Inline animations use single braces for both the step and the content — `{step}{content}`:

```markdown
This is {1}{visible on step 1} and {2}{this on step 2}.
```

A range hides the content after the end step:

```markdown
This {1-2}{appears at step 1, gone at step 3} continues.
```

### Combined Animation + TTS

Use `{{1 |>}}` to reveal a block AND auto-play TTS at that step. Or pair a block tag with a narrator comment for the same step:

```markdown
     {{1 |>}}
This appears at step 1 and is spoken automatically.

     {{2}}
This block appears at step 2.

--{{2}}--
And this is spoken aloud at step 2.
```

### CSS Transition Animations (animate.css)

Add a CSS class comment directly before the animated block (requires loading the stylesheet in the header):

```markdown
<!-- class="animate__animated animate__backInUp" -->
     {{1}}
This slides in from below at step 1.
```

Header setup:

```markdown
link: https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css
```

---

## Text-to-Speech & Comments

### Narrator Comments

Comments are spoken aloud in Presentation mode:

```markdown
--{{0}}--
This is spoken when the slide loads (step 0).

--{{1}}--
This is spoken when step 1 is triggered.
```

### Changing Voice

```markdown
--{{1 UK English Male}}--
This will be spoken in a British male voice.

--{{2 German Female}}--
Das wird auf Deutsch gesprochen.
```

### Playback Blocks

`{{|>}}` auto-plays the block when reached in Presentation mode. `{{!>}}` shows a click-to-play button instead:

```markdown
     {{|>}}
This entire paragraph will be read aloud automatically.

     {{!> Australian Female}}
This one only plays when the user clicks the speaker icon.
```

Group multiple blocks into one playback unit with `****`:

```markdown
     {{|>}}
************************************
This paragraph and the list below
are spoken together as one unit.

- Item one
- Item two

************************************
```

### Inline Playback

Use `{!>}{text}` for a play button inline — great for vocabulary or conjugation tables:

```markdown
{!>}{Hello} | {!> Deutsch Male}{Hallo} | {!> Russian Female}{Привет}
```

With a voice: `{!> UK English Male}{text}`. The `|>` variant auto-plays; `!>` requires a click.

### Hidden TTS Comments

Wrap a TTS comment inside an HTML comment to speak it aloud **without showing it** to the learner in any mode:

```markdown
<!-- --{{1}}--
This is spoken at step 1 but never displayed to the learner.
-->
```

Useful for adding narration that would be redundant or distracting as visible text.

### Available Voices

Common voices include:
- `US English Female`, `US English Male`
- `UK English Female`, `UK English Male`
- `German Female`, `German Male`  
- `French Female`, `French Male`
- `Spanish Female`, `Spanish Male`

See full list in `references/voices.md`.

---

## Multimedia

### Images

```markdown
![Alt text](url "Optional title/caption")
```

Control size with an inline style comment directly after the image tag (no blank line):

```markdown
![Alt text](url)<!-- style="width: 50%" -->
```

### Audio

```markdown
?[Audio description](url)
```

### Video

```markdown
!?[Video description](https://www.youtube.com/watch?v=VIDEO_ID)
```

Supports: YouTube, Vimeo, PeerTube, DailyMotion, TeacherTube, and direct video files.

### Embedded Content (iframes)

```markdown
??[Description](https://example.com/interactive-widget)
```

### QR Codes

Name a link `qr-code` to render it as a QR code:

```markdown
[qr-code](https://LiaScript.github.io)
```

Add an optional caption as the link title:

```markdown
[qr-code](https://LiaScript.github.io "Scan to visit the LiaScript website")
```

### Course Preview Cards

Name a link `preview-lia` to render a rich preview card for another LiaScript course (uses the raw GitHub URL):

```markdown
[preview-lia](https://raw.githubusercontent.com/LiaScript/docs/master/README.md)
```

### Galleries

Place multiple media items in a single paragraph (no blank lines between them):

```markdown
![Image 1](url1)
![Image 2](url2)
![Image 3](url3)
```

---

## Tables & Visualizations

### Basic Table

```markdown
| Header 1 | Header 2 | Header 3 |
|:---------|:--------:|---------:|
| Left     | Center   |    Right |
| Data     |   Data   |     Data |
```

### Data Visualization

Tables automatically become charts based on their data shape. Users can toggle between table and chart view.

**Auto-detected chart types:**

| Table shape | Chart type |
|---|---|
| First column is text, one numeric column | BarChart |
| First column is text, many numeric columns | Radar or Parallel |
| First column is numeric, no duplicates | LinePlot |
| First column is numeric, with duplicates | ScatterPlot |
| Two columns only | PieChart |
| Coordinate-like header + first column | HeatMap |

**Force a specific chart type** with a comment before the table:

```markdown
<!-- data-type="BarChart" -->
| Language | Users |
|----------|------:|
| Python   |   100 |
| JS       |    80 |
| Rust     |    40 |
```

Supported `data-type` values: `LinePlot`, `ScatterPlot`, `BoxPlot`, `BarChart`, `Radar`, `PieChart`, `Funnel`, `HeatMap`, `Parallel`, `Graph`, `Sankey`, `Map`.

**Customize labels and display:**

```markdown
<!--
data-type="LinePlot"
data-title="Revenue over Time"
data-xlabel="Year"
data-ylabel="USD (millions)"
data-show
-->
| Year | Revenue |
|-----:|--------:|
| 2020 |      12 |
| 2021 |      18 |
| 2022 |      27 |
```

- `data-title` — chart title
- `data-xlabel` / `data-ylabel` — axis labels
- `data-show` — open in chart view by default instead of table view
- `data-transpose` — swap rows and columns

**Map visualization** requires a GeoJSON source:

```markdown
<!-- data-type="map" data-src="https://code.highcharts.com/mapdata/custom/europe.geo.json" -->
| Country | Value |
|---------|------:|
| Germany |    82 |
| France  |    67 |
```

---

## Reactive Scripts

Inline `<script>` tags render their return value in the page and re-execute when inputs change. Use them for interactive sliders, linked calculations, and async data. See `references/advanced.md` for full syntax.

---

## Code Blocks

### Syntax Highlighted Code

````markdown
```python
def hello():
    print("Hello, World!")
```
````

### Executable Code

Attach a `<script>@input</script>` tag directly after the code block (no blank line) to make it runnable:

````markdown
```javascript
var x = 5 + 3;
console.log("5 + 3 =", x);
// the last expression is the return value shown below the output
x;
```
<script>@input</script>
````

The **last expression** in the block is used as the return value displayed beneath the console output. Since `console.log` returns `undefined`, always end with a meaningful value or omit it if you only care about `console.log` output.

For Python and other languages, import a template from LiaTemplates:

````markdown
<!--
import: https://raw.githubusercontent.com/LiaTemplates/Pyodide/master/README.md
-->

```python
print("Hello from Python!")
```
@Pyodide.eval
````

### Code Projects (Multiple Files)

Name each file by adding the filename after the language tag. Use `@input(0)`, `@input(1)` etc. to reference each file by index:

````markdown
```html  index.html
<!DOCTYPE html>
<html>
<head><script src="script.js"></script></head>
<body><h1 id="demo">Hello</h1></body>
</html>
```
```javascript  script.js
document.getElementById("demo").innerHTML = "Changed!";
```
<script>
  // files are available as @input(0) and @input(1)
  @input(0)
</script>
````

Hidden files (prefixed with `-`) are included in execution but not shown to the learner:

````markdown
```javascript  -helper.js
function greet(name) { return "Hello, " + name + "!"; }
```
```javascript  main.js
console.log(greet("World"));
```
<script>@input(0)\n@input(1)</script>
````

---

## SVG Graphics

Write raw `<svg>` tags directly in Markdown. Use `<foreignObject>` to embed rendered Markdown or math at specific coordinates inside an SVG. See `references/advanced.md` for full examples.

---

## ASCII Art Diagrams

LiaScript renders ASCII diagrams beautifully. Use ` ```ascii ` or open the block with 10+ backticks:

````markdown
```ascii
    +--------+     +--------+
    | Client |---->| Server |
    +--------+     +--------+
         |              |
         v              v
    +--------+     +--------+
    | Cache  |     |   DB   |
    +--------+     +--------+
```
````

### Styling

Add a `<!-- style="..." -->` comment before the block to control size, alignment, or SVG colors:

````markdown
<!-- style="max-width: 400px; stroke: green;" -->
```ascii
A ----> B ----> C
```
````

### Title / Caption

Add a title after the language tag — it renders as a caption below the diagram:

````markdown
```ascii  Fig.: System Architecture
+--------+     +--------+
| Client |---->| Server |
+--------+     +--------+
```
````

### Embedding LiaScript Elements

Place LiaScript content inside double quotes `"..."` within the ASCII art. Quoted content is rendered as a `foreignObject` overlaid on the diagram — use it for inline animations, math, or executable code:

````markdown
```ascii
 😀                                        😐
  |      "{1}{_How are you?_}"             |
  +---------------------------------------->|
  |      "{2}{**Need to do math**}"        |
  |<----------------------------------------+
  | "              {{3}}                 " |
  | "$$                                  " |
  | "  x = \sqrt[3]{y}                   " |
  | "$$                                  " |
  +---------------------------------------->|
```
````

- Single-line: `"content"` — one quoted string per line
- Multi-line block: multiple `"..."` lines starting at the **same horizontal position** form a block
- The longest line defines the block width

---

## Surveys

Surveys are quizzes without a correct answer. Use **4-space indentation** (or a list with `-`) for all survey options.

### Single-Choice Survey

Use a label inside `(...)` as the variable identifier. Numbers plot as distributions in classroom mode; text labels show as categorical values:

```markdown
How satisfied are you?

- [(very good)]      I like it very much
- [(good)]           It is ok
- [(bad)]            I don't like it
- [(something else)] I am not sure
```

### Multiple-Choice Survey

```markdown
What topics interest you?

    [[AI]]
    [[Web Development]]
    [[Data Science]]
    [[Mobile Apps]]
```

### Text Survey (Single Line)

Use at least 3 underscores as the placeholder. Must be indented 4 spaces:

```markdown
What is your reaction?

    [[___]]
```

### Text Survey (Textarea / Multi-Line)

Repeat `___` groups (separated by spaces) to get a multi-line textarea — the number of groups sets the number of rows:

```markdown
Please describe your opinion in a few sentences:

    [[___ ___ ___ ___]]
```

---

## Tasks / Checklists

```markdown
- [X] Completed task
- [ ] Incomplete task  
- [ ] Another task
```

---

## Formulas (LaTeX)

### Inline Math

```markdown
The formula $E = mc^2$ changed physics.
```

### Block Math

```markdown
$$
\int_0^\infty e^{-x^2} dx = \frac{\sqrt{\pi}}{2}
$$
```

---

## Footnotes

```markdown
Something important[^1] to note[^🦶].

[^1]: Footnote content — supports full Markdown.
[^🦶]: Any marker works: numbers, words, or emoji.
```

Inline footnote (no definition block needed):

```markdown
See the W3C spec[^spec](The Web standard defining HTML5 semantics).
```

### Formula Macros

**Local** — define inside a formula, valid only within that expression:

```markdown
$ \def\foo{x^2} \foo + \foo $

$ \gdef\bar#1{#1^2} \bar{y} + \bar{y} $
```

**Global** — define in the course header with `formula:`, reusable in all formulas. The first word is the macro name (leading `\` optional), the rest is the body:

```markdown
<!--
author: Your Name

formula:  foo   {x^2}
formula:  \bar  {#1^2}
-->

$ \foo + \foo $

$ \bar{y} + \bar{y} $
```

### Chemical Formulas

Use `\ce{...}` inside standard math delimiters — no imports needed, mhchem is built in:

```markdown
Inline: $\ce{H2O}$

Block:
$$\ce{CO2 + C -> 2 CO}$$

$$\ce{Hg^2+ ->[I-] HgI2 ->[I-] [Hg^{II}I4]^2-}$$
```

---

## Text Formatting Extensions

Beyond standard Markdown, LiaScript adds:

### Extra Inline Styles

```markdown
~~underline~~
~~~strikethrough and underline~~~
^superscript^
```

All combinable with standard bold/italic: `**~~bold underline~~**`, `*^italic superscript^*`

### Typography Shortcuts

```markdown
-- en dash
--- em dash
... ellipsis (→ Unicode …)
```

Single and double quotes are auto-converted to typographic curly quotes based on the course `language:` setting. To override per-block use `<q lang="de">...</q>`.

LiaScript also converts arrow shortcuts (`->`, `=>`, `<->`, `-->`, etc.) and smileys (`:-)`). See `references/advanced.md` for the full list.

---

## Metadata Reference

```markdown
<!--
author:   Name
email:    email@example.com
version:  1.0.0
language: en
narrator: US English Female

comment:  Course description (shown in preview cards)
logo:     URL to course logo/image

import:   URL to macro template (multiple allowed)
-->
```

For additional fields (`mode`, `dark`, `classroom`, `font`, `persistent`, `link`, `script`, `@onload`, etc.) see `references/advanced.md`.

---

## Best Practices

- Each `#` heading = one slide; use `##`/`###` within slides
- Indent animation tags 4+ spaces: `     {{1}}`

- Include narrator comments for accessibility
- Provide alt text for all images
- Preview at https://liascript.github.io/LiveEditor/ and test all three display modes

---

## Output Guidelines

When generating LiaScript courses:

1. **Always include a complete header** with author, language, narrator, and comment
2. **Use proper blank line spacing** - LiaScript is whitespace-sensitive
3. **Test quiz syntax carefully** - brackets and parentheses must be exact
4. **Use animations sparingly** - they should enhance, not distract
5. **Save as `.md` file** - the course IS the Markdown file

For complex features (macros, custom scripts, imports), consult `references/advanced.md`.
For ready-to-use course templates, consult `references/templates.md`.
For available TTS voices, consult `references/voices.md`.
