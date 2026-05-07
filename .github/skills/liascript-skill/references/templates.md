# LiaScript Course Templates

Ready-to-use templates for common course types. Copy and customize for your needs.

## Basic Course Template

```markdown
<!--
author:   Your Name
email:    your@email.com
version:  1.0.0
language: en
narrator: US English Female

comment:  A brief course description that appears on preview cards.

logo:     https://your-logo-url.png
-->

# Course Title

Welcome to this course! 

--{{0}}--
Hello and welcome! In this course, you will learn about [topic]. 
Let's get started with the basics.

## Learning Objectives

By the end of this course, you will be able to:

     {{1}}
- Understand the fundamentals of [topic]

     {{2}}
- Apply [skill] in practical scenarios

     {{3}}
- Evaluate and analyze [concept]

## Section 1: Introduction

Content for the first section...

### Key Concept

--{{0}}--
This is an important concept that forms the foundation of everything else.

Explanation of the key concept with examples.

### Quick Check

What is the main idea of [concept]?

[( )] Incorrect option A
[(X)] Correct answer
[( )] Incorrect option B
[[?]] Think about what we just discussed
***
Explanation of why this is the correct answer.
***

## Section 2: Deep Dive

More detailed content...

## Summary

Key takeaways from this course:

1. First main point
2. Second main point  
3. Third main point

## Final Quiz

<!-- data-randomize -->
Question 1: ...

[(X)] Correct
[( )] Wrong
[( )] Wrong

Question 2: ...

[[correct answer]]
[[?]] Hint for this question
```

---

## Programming Tutorial Template

````markdown
<!--
author:   Your Name
version:  1.0.0
language: en
narrator: US English Male

import: https://raw.githubusercontent.com/LiaTemplates/Pyodide/master/README.md

comment:  Learn [programming language] through hands-on exercises.
-->

# Learn [Language] Programming

## Getting Started

### Your First Program

--{{0}}--
Let's write your first program! The classic "Hello, World!" example.

```python
print("Hello, World!")
```
@Pyodide.eval

     {{1}}
Try modifying the message above and running it again!

### Variables

```python
# Try changing these values
name = "Alice"
age = 25
print(f"My name is {name} and I am {age} years old.")
```
@Pyodide.eval

### Exercise: Variables

Create variables for your own name and age, then print them.

```python
# Your code here
name = 
age = 
print(f"My name is {name} and I am {age} years old.")
```
@Pyodide.eval

### Check Your Understanding

What will this code print?

```python
x = 5
y = 3
print(x + y)
```

[( )] 53
[(X)] 8
[( )] "x + y"
***
Variables x and y contain numbers, so + performs addition: 5 + 3 = 8
***

## Functions

### Defining Functions

```python
def greet(name):
    return f"Hello, {name}!"

# Call the function
message = greet("World")
print(message)
```
@Pyodide.eval

### Practice: Write a Function

Write a function that calculates the area of a rectangle.

```python
def rectangle_area(width, height):
    # Your code here
    pass

# Test it
print(rectangle_area(5, 3))  # Should print 15
```
@Pyodide.eval
````

---

## Language Learning Template

```markdown
<!--
author:   Your Name
version:  1.0.0
language: en
narrator: US English Female

comment:  Learn basic [language] vocabulary and phrases.
-->

# Basic [Language] Course

## Greetings

### Common Phrases

--{{0 [Target Language] Female}}--
[Phrase in target language]

| [Language] | English | Audio |
|------------|---------|-------|
| Hola | Hello | {!> Spanish Female}{Hola} |
| Buenos días | Good morning | {!> Spanish Female}{Buenos días} |
| Buenas noches | Good night | {!> Spanish Female}{Buenas noches} |

### Practice

Match the greeting with its meaning:

[ [Hello] [Good morning] [Goodbye] ]
[   (X)       ( )          ( )     ] Hola
[   ( )       (X)          ( )     ] Buenos días  
[   ( )       ( )          (X)     ] Adiós

### Conversation Practice

--{{0}}--
Listen to the conversation and answer the questions.

??[Dialogue](https://example.com/audio/dialogue1.mp3)

What was the first greeting used?

[[Hola]]

## Vocabulary

### Numbers 1-10

| Number | [Language] | 
|--------|-----------|
| 1 | uno |
| 2 | dos |
| 3 | tres |
| 4 | cuatro |
| 5 | cinco |

### Quiz: Numbers

How do you say "3" in [language]?

[( )] uno
[( )] dos
[(X)] tres
[( )] cuatro
```

---

## Science/Math Template

```markdown
<!--
author:   Your Name
version:  1.0.0
language: en
narrator: US English Female

comment:  Understanding [scientific concept] through visual explanations.
-->

# Understanding [Topic]

## The Fundamentals

### Key Formula

--{{0}}--
The most important equation in this topic is shown below.

$$
E = mc^2
$$

Where:
- $E$ is energy
- $m$ is mass  
- $c$ is the speed of light

### Visualization

```ascii
    Energy
      ^
      |      /
      |     /
      |    /
      |   /
      |  /
      | /
      |/____________> Mass
```

### Interactive Calculator

Calculate the energy for a given mass:

Mass (kg): <script input="number" value="1" output="mass">@input</script>

Energy = <script>
let m = @input(`mass`);
let c = 299792458; // speed of light
let E = m * c * c;
E.toExponential(3) + " Joules"
</script>

### Check Your Understanding

If you double the mass, what happens to the energy?

[( )] It stays the same
[(X)] It doubles
[( )] It quadruples
[( )] It halves
[[?]] Look at the formula - energy is directly proportional to mass.
***
Since $E = mc^2$, energy is directly proportional to mass. 
Double the mass means double the energy.
***

## Worked Examples

### Example 1

Problem: Calculate the energy of 2 kg of matter.

     {{1}}
**Step 1:** Identify known values
- $m = 2$ kg
- $c = 3 \times 10^8$ m/s

     {{2}}
**Step 2:** Apply the formula
$$E = mc^2 = 2 \times (3 \times 10^8)^2$$

     {{3}}
**Step 3:** Calculate
$$E = 2 \times 9 \times 10^{16} = 1.8 \times 10^{17} \text{ J}$$
```

---

## Quiz-Heavy Assessment Template

```markdown
<!--
author:   Your Name
version:  1.0.0
language: en
narrator: US English Female

comment:  Self-assessment quiz on [topic].
-->

# [Topic] Assessment

## Instructions

--{{0}}--
This assessment contains 10 questions covering the key concepts from this unit.
Take your time and use the hints if you need them.

- Complete all questions
- You can retry questions
- Hints are available for each question

## Part 1: Multiple Choice

<!-- data-max-trials="2" -->
**Question 1:** [Question text]

[( )] Option A
[(X)] Option B (correct)
[( )] Option C
[( )] Option D
[[?]] Hint for question 1
***
Explanation of the correct answer.
***

<!-- data-max-trials="2" -->
**Question 2:** [Question text]

[[X]] Correct option 1
[[ ]] Wrong option
[[X]] Correct option 2
[[ ]] Wrong option
[[?]] Remember: multiple answers may be correct!

## Part 2: Fill in the Blank

**Question 3:** The capital of France is [[Paris]].

**Question 4:** Complete the sentence:

Water boils at [[100]] degrees [[ Celsius | (Fahrenheit) | Kelvin ]] at sea level.

## Part 3: Matching

**Question 5:** Match the terms with their definitions:

[ [Term A] [Term B] [Term C] ]
[   (X)      ( )      ( )   ] Definition of A
[   ( )      (X)      ( )   ] Definition of B
[   ( )      ( )      (X)   ] Definition of C

## Results

Congratulations on completing the assessment! 

Review any questions you found difficult and revisit the relevant course sections.
```

---

## Data Visualization Template

````markdown
<!--
author:   Your Name
version:  1.0.0
language: en
narrator: US English Female

comment:  Explore and understand [dataset topic] through interactive charts.
-->

# [Topic] Data Exploration

## Overview

--{{0}}--
In this course we explore [dataset topic] using interactive visualizations.
Switch between the table and chart views using the icon in the top-right of each table.

## Bar Chart: Comparing Categories

<!-- data-type="BarChart" data-title="[Title]" data-xlabel="Category" data-ylabel="Value" data-show -->
| Category   | Value |
|------------|------:|
| Group A    |    42 |
| Group B    |    78 |
| Group C    |    55 |
| Group D    |    91 |

## Line Plot: Trends Over Time

<!-- data-type="LinePlot" data-title="Trend Over Time" data-xlabel="Year" data-ylabel="Units" data-show -->
| Year | Series A | Series B |
|-----:|---------:|---------:|
| 2020 |       12 |        8 |
| 2021 |       18 |       14 |
| 2022 |       27 |       19 |
| 2023 |       35 |       28 |

## Geographic Map

<!-- data-type="map" data-src="https://code.highcharts.com/mapdata/custom/europe.geo.json" data-title="Values by Country" data-show -->
| Country | Value |
|---------|------:|
| Germany |    82 |
| France  |    67 |
| Spain   |    47 |

## Interactive Calculator

Adjust the slider to explore the relationship:

$x =$ <script input="range" min="1" max="100" value="10" output="x">@input</script>

Result: <script run-once>
let x = @input(`x`)
"$y = " + (x * x) + "$"
</script>

## Quiz: Reading Charts

Looking at the bar chart above, which category had the highest value?

[( )] Group A
[( )] Group B
[( )] Group C
[(X)] Group D
[[?]] Check the bar heights in the chart view.
***
Group D had the highest value at 91.
***
````

---

## Multilingual Course Template

````markdown
<!--
author:   Your Name
version:  1.0.0
language: en
narrator: US English Female

translateWithGoogle: false
translation: Deutsch translations/de.md

comment:  [Course topic] — available in multiple languages with native TTS narration.
-->

# [Course Title]

## Introduction

--{{0}}--
Welcome to this course. The content is available in English with text-to-speech narration.

--{{0 German Female}}--
Willkommen zu diesem Kurs. Der Inhalt ist auf Englisch verfügbar, aber dieser Kommentar wird auf Deutsch gesprochen.

Content of the introduction slide here.

## Vocabulary: Greetings

| English       | Deutsch         | Español          | Audio (EN) | Audio (DE) |
|---------------|-----------------|------------------|------------|------------|
| Hello         | Hallo           | Hola             | {!> US English Female}{Hello} | {!> German Female}{Hallo} |
| Good morning  | Guten Morgen    | Buenos días      | {!> US English Female}{Good morning} | {!> German Female}{Guten Morgen} |
| Thank you     | Danke           | Gracias          | {!> US English Female}{Thank you} | {!> German Female}{Danke} |
| Goodbye       | Auf Wiedersehen | Adiós            | {!> US English Female}{Goodbye} | {!> German Female}{Auf Wiedersehen} |

## Quiz: Match the Translation

How do you say "Thank you" in German?

[( )] Hallo
[( )] Guten Morgen
[(X)] Danke
[( )] Auf Wiedersehen

## Reading: Short Passage

--{{0 US English Female}}--
Read along as the passage is narrated in English.

The quick brown fox jumps over the lazy dog.
This sentence contains every letter of the English alphabet.

--{{1 German Female}}--
Jetzt hören Sie die deutsche Übersetzung.

     {{1}}
*Der schnelle braune Fuchs springt über den faulen Hund.*
````

---

## Classroom / Collaborative Template

````markdown
<!--
author:   Your Name
version:  1.0.0
language: en
narrator: US English Female

comment:  An interactive session designed for real-time classroom use with synchronized quizzes and surveys.

classroom: enable
-->

# [Session Title]

> **Before you begin:** Open the classroom by clicking the share button and entering the room name your instructor provides.
> All quiz and survey responses will be anonymously aggregated for the group.

## Warm-Up Survey

How familiar are you with today's topic?

- [(1 - Not at all)] I have never heard of it
- [(2 - A little)]   I have heard the term
- [(3 - Somewhat)]   I understand the basics
- [(4 - Very)]       I use it regularly

## Collaborative Code

Everyone in the classroom can edit this snippet together:

```javascript
// Edit this code — changes sync to all connected peers
function greet(name) {
  return "Hello, " + name + "!";
}

console.log(greet("class"));
```
<script>@input</script>

## Poll: Quick Check

Which option best describes [concept]?

<!-- data-randomize -->
- [(X)] Correct description
- [( )] Plausible but wrong
- [( )] Clearly wrong
- [( )] Clearly wrong

## Open Question

What is your biggest takeaway from today?

    [[___ ___ ___]]

## Wrap-Up

--{{0}}--
Thanks for participating. The aggregated results from your quizzes and surveys are visible to the instructor in real time.

Review the key points before we close:

     {{1}}
- Point 1

     {{2}}
- Point 2

     {{3}}
- Point 3
````

---

## Tips for Using Templates

1. **Customize the header** with your information
2. **Adjust the narrator voice** to match your language
3. **Add/remove sections** based on your content needs
4. **Include media** (images, videos, audio) where helpful
5. **Test all quizzes** to ensure correct answers work
6. **Preview your course** at https://liascript.github.io/course/
