# Markdown Cheat Sheet

## Table of Contents
- [Headers](#headers)
- [Text Formatting](#text-formatting)
- [Lists](#lists)
- [Links](#links)
- [Images](#images)
- [Code](#code)
- [Tables](#tables)
- [Blockquotes](#blockquotes)
- [Horizontal Rules](#horizontal-rules)
- [Line Breaks](#line-breaks)
- [Escape Characters](#escape-characters)
- [GitHub Flavored Markdown](#github-flavored-markdown)
- [Extended Syntax](#extended-syntax)
- [Tips & Best Practices](#tips--best-practices)

## Headers

```markdown
# H1 Header
## H2 Header
### H3 Header
#### H4 Header
##### H5 Header
###### H6 Header

Alternative H1
==============

Alternative H2
--------------
```

**Rendered:**
# H1 Header
## H2 Header
### H3 Header
#### H4 Header
##### H5 Header
###### H6 Header

## Text Formatting

### Basic Formatting
```markdown
**Bold text** or __Bold text__
*Italic text* or _Italic text_
***Bold and italic*** or ___Bold and italic___
~~Strikethrough~~
```

**Rendered:**
**Bold text** or __Bold text__  
*Italic text* or _Italic text_  
***Bold and italic*** or ___Bold and italic___  
~~Strikethrough~~

### Advanced Formatting
```markdown
This is <sub>subscript</sub> and <sup>superscript</sup>
<mark>Highlighted text</mark>
<kbd>Ctrl</kbd> + <kbd>C</kbd>
```

**Rendered:**
This is <sub>subscript</sub> and <sup>superscript</sup>  
<mark>Highlighted text</mark>  
<kbd>Ctrl</kbd> + <kbd>C</kbd>

## Lists

### Unordered Lists
```markdown
- Item 1
- Item 2
  - Nested item 1
  - Nested item 2
    - Double nested item
- Item 3

* Alternative syntax
* Works the same
  * Nested with asterisk

+ Plus signs work too
+ Same result
```

**Rendered:**
- Item 1
- Item 2
  - Nested item 1
  - Nested item 2
    - Double nested item
- Item 3

### Ordered Lists
```markdown
1. First item
2. Second item
   1. Nested numbered item
   2. Another nested item
3. Third item

1. Numbers don't have to be sequential
1. They will auto-increment
1. Like this
```

**Rendered:**
1. First item
2. Second item
   1. Nested numbered item
   2. Another nested item
3. Third item

### Task Lists (GitHub Flavored)
```markdown
- [x] Completed task
- [ ] Uncompleted task
- [ ] Another task
  - [x] Nested completed task
  - [ ] Nested uncompleted task
```

**Rendered:**
- [x] Completed task
- [ ] Uncompleted task
- [ ] Another task
  - [x] Nested completed task
  - [ ] Nested uncompleted task

## Links

### Basic Links
```markdown
[Link text](https://example.com)
[Link with title](https://example.com "Optional title")
<https://example.com>
<email@example.com>
```

### Reference Links
```markdown
[Link text][reference]
[Another link][another-ref]

[reference]: https://example.com
[another-ref]: https://example.com "Optional title"
```

### Internal Links (Anchors)
```markdown
[Link to section](#headers)
[Link to custom anchor](#custom-anchor)

<a name="custom-anchor"></a>
```

## Images

### Basic Images
```markdown
![Alt text](image-url.jpg)
![Alt text](image-url.jpg "Optional title")
```

### Reference Images
```markdown
![Alt text][image-ref]

[image-ref]: image-url.jpg "Optional title"
```

### Images with Links
```markdown
[![Alt text](image-url.jpg)](https://example.com)
```

### HTML Image Control
```markdown
<img src="image-url.jpg" alt="Alt text" width="300" height="200">
```

## Code

### Inline Code
```markdown
Use `backticks` for inline code.
Use `git status` to check repository status.
```

**Rendered:**
Use `backticks` for inline code.  
Use `git status` to check repository status.

### Code Blocks
````markdown
```
Basic code block
No syntax highlighting
```

```javascript
// JavaScript code block
function hello() {
    console.log("Hello, World!");
}
```

```python
# Python code block
def hello():
    print("Hello, World!")
```

```bash
# Bash code block
echo "Hello, World!"
ls -la
```
````

### Indented Code Blocks
```markdown
    Indent with 4 spaces
    for code blocks
    No syntax highlighting
```

## Tables

### Basic Tables
```markdown
| Header 1 | Header 2 | Header 3 |
|----------|----------|----------|
| Row 1    | Data     | Data     |
| Row 2    | Data     | Data     |
```

**Rendered:**
| Header 1 | Header 2 | Header 3 |
|----------|----------|----------|
| Row 1    | Data     | Data     |
| Row 2    | Data     | Data     |

### Table Alignment
```markdown
| Left | Center | Right |
|:-----|:------:|------:|
| Left | Center | Right |
| align| align  | align |
```

**Rendered:**
| Left | Center | Right |
|:-----|:------:|------:|
| Left | Center | Right |
| align| align  | align |

### Complex Table Content
```markdown
| Feature | Supported | Notes |
|---------|:---------:|-------|
| **Bold** | ✅ | Works in tables |
| `Code` | ✅ | Inline code works |
| [Links](/) | ✅ | Links work too |
| Line<br>breaks | ✅ | Use `<br>` tag |
```

## Blockquotes

### Basic Blockquotes
```markdown
> This is a blockquote.
> It can span multiple lines.

> You can also use blockquotes
> to highlight important information.
```

**Rendered:**
> This is a blockquote.
> It can span multiple lines.

### Nested Blockquotes
```markdown
> This is a blockquote.
> 
> > This is a nested blockquote.
> > It's indented further.
> 
> Back to the original level.
```

### Blockquotes with Other Elements
```markdown
> ## Header in blockquote
> 
> - List item 1
> - List item 2
> 
> `Code` and **bold** work too.
```

## Horizontal Rules

```markdown
---

***

___

<!-- HTML version -->
<hr>
```

**Rendered:**
---

## Line Breaks

```markdown
Two spaces at the end of line  
create a line break.

Alternatively, use a blank line

to create a paragraph break.

<br>
HTML break tag works too.
```

## Escape Characters

```markdown
\* Escaped asterisk
\_ Escaped underscore
\` Escaped backtick
\# Escaped hash
\[ Escaped bracket
\\ Escaped backslash
```

**Characters that can be escaped:**
```
\ ` * _ { } [ ] ( ) # + - . !
```

## GitHub Flavored Markdown

### Syntax Highlighting
````markdown
```diff
+ Added line
- Removed line
  Unchanged line
```

```json
{
  "name": "example",
  "version": "1.0.0"
}
```
````

### Mentions and References
```markdown
@username mentions a user
#123 references issue #123
GH-123 also references issue #123
username/repository#123 references issue in another repo
```

### Emoji
```markdown
:smile: :heart: :thumbsup:
:rocket: :sparkles: :tada:

GitHub also supports Unicode emoji: 😄 ❤️ 👍
```

### Collapsible Sections
```markdown
<details>
<summary>Click to expand</summary>

Hidden content goes here.

- Can contain lists
- **Formatted text**
- `Code blocks`

</details>
```

### Math (GitHub)
```markdown
Inline math: $x^2 + y^2 = z^2$

Block math:
$$
\sum_{i=1}^{n} x_i = x_1 + x_2 + \cdots + x_n
$$
```

## Extended Syntax

### Footnotes
```markdown
Here's a sentence with a footnote[^1].

[^1]: This is the footnote content.
```

### Definition Lists
```markdown
Term 1
: Definition 1

Term 2
: Definition 2
: Another definition for term 2
```

### Abbreviations
```markdown
The HTML specification is maintained by the W3C.

*[HTML]: Hyper Text Markup Language
*[W3C]: World Wide Web Consortium
```

## Tips & Best Practices

### File Naming
- Use `.md` or `.markdown` extension
- Use lowercase with hyphens: `my-document.md`
- Avoid spaces in filenames

### Writing Tips
- Use consistent heading hierarchy
- Add blank lines around headers
- Use meaningful link text (avoid "click here")
- Add alt text to images for accessibility
- Use tables sparingly; consider lists for simple data

### Organization
```markdown
# Document Title

Brief description of the document.

## Table of Contents
- [Section 1](#section-1)
- [Section 2](#section-2)

## Section 1

Content here...

## Section 2

Content here...
```

### Common Pitfalls
- Forgetting blank lines around code blocks
- Inconsistent list indentation
- Missing alt text for images
- Overusing formatting (less is more)
- Not testing how it renders

### Tools and Editors
- **VS Code**: Great Markdown support with preview
- **Typora**: WYSIWYG Markdown editor
- **Mark Text**: Real-time preview editor
- **Online**: Dillinger.io, StackEdit
- **CLI**: Pandoc for conversion

### Markdown Linting
Use tools like:
- `markdownlint` for VS Code
- `remark-lint` for Node.js
- `mdl` (Markdown Lint Tool)

### Preview and Testing
- Always preview your Markdown
- Test on target platform (GitHub, GitLab, etc.)
- Check on mobile devices
- Validate links regularly

### Performance Tips
- Optimize images (compress, use appropriate formats)
- Use relative links when possible
- Keep documents focused and not too long
- Use proper heading structure for navigation

---

*Remember: Different Markdown parsers may have slight variations. Always test your content on the target platform.*