# Regular Expressions (Regex) Cheat Sheet

Powerful pattern matching for searching, validating, extracting, and transforming text. Examples use a widely supported flavor (PCRE-style). Notes are included where engines differ across common regex engines.

## Table of Contents

- [Basics](#basics)
- [Flags / Modifiers](#flags--modifiers)
- [Character Classes](#character-classes)
- [Anchors and Boundaries](#anchors-and-boundaries)
- [Quantifiers](#quantifiers)
- [Grouping, Alternation, and References](#grouping-alternation-and-references)
- [Lookaround](#lookaround)
- [Escapes and Special Characters](#escapes-and-special-characters)
- [Common Patterns](#common-patterns)
- [Practical Tasks](#practical-tasks)
  - [Validation](#validation)
  - [Extraction](#extraction)
  - [Replacement](#replacement)
- [Engine differences and portability](#engine-differences-and-portability)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)
- [Tools & References](#tools--references)

## Basics

- Literal match: `cat` matches the substring "cat".
- Concatenation: `foo\sbar` matches "foo bar" (with whitespace between).
- Alternation: `cat|dog` matches either "cat" or "dog".
- Case sensitivity: defaults to case-sensitive unless the ignore-case flag is enabled.

Test drive a pattern against sample text using online tools listed below.

## Flags / Modifiers

- i — ignore case
- m — multiline: `^` and `$` match start/end of line
- s — dotall: `.` matches newlines as well
- x — free-spacing/comments: ignore unescaped whitespace and allow inline comments
- u — Unicode mode: enable Unicode-aware classes/escapes
- global — find all matches (engine/tool dependent; not a pattern flag in some engines)

Note: How to enable flags differs by engine (inline like `(?imx)`, literal suffixes, or constructor options). Consult your engine’s documentation.

## Character Classes

- `.` — any character except newline (unless s/dotall flag)
- `\w` — word char: `[A-Za-z0-9_]` (Unicode-aware under some engines with `u`)
- `\W` — not word char
- `\d` — digit: `[0-9]` (Unicode digits vary by engine)
- `\D` — not digit
- `\s` — whitespace: space, tab, newline, etc.
- `\S` — not whitespace
- Custom set: `[abc]` any of a, b, or c
- Ranges: `[A-Z]`, `[a-z]`, `[0-9]`
- Negated set: `[^abc]` any char except a, b, or c

Common sets:

- Hex: `[0-9A-Fa-f]`
- Word-ish (ASCII): `[A-Za-z0-9_]`

## Anchors and Boundaries

- `^` — start of string (or line in multiline mode)
- `$` — end of string (or line in multiline mode)
- `\b` — word boundary (between `\w` and `\W`)
- `\B` — not a word boundary

Examples:

- `^Hello` matches "Hello" at line start
- `world$` matches "world" at line end
- `\bcat\b` matches "cat" as a whole word

## Quantifiers

- `?` — 0 or 1 (optional)
- `*` — 0 or more
- `+` — 1 or more
- `{n}` — exactly n
- `{n,}` — at least n
- `{n,m}` — between n and m inclusive

Greedy vs lazy:

- Greedy (default) grabs as much as possible: `.+`
- Lazy (non-greedy) adds `?`: `.+?`

Possessive quantifiers (where supported): `++`, `*+`, `?+`, `{n,m}+` prevent backtracking.

## Grouping, Alternation, and References

- Capturing group: `( ... )` assigned an index starting at 1
- Non-capturing group: `(?: ... )` groups without creating a capture
- Named group: variants like `(?<name> ... )` or `(?P<name> ... )`
- Alternation: `(foo|bar|baz)`
- Backreference: `\1`, `\2` or named forms like `\k<name>` / `(?P=name)`

Examples:

- Duplicate word: `\b(\w+)\s+\1\b` matches "the the"
- HTML-like tag pair: `<(\w+)[^>]*>.*?<\/\1>` (simplified)

## Lookaround

Zero-width assertions that don't consume characters.

- Positive lookahead: `X(?=Y)` — X followed by Y
- Negative lookahead: `X(?!Y)` — X not followed by Y
- Positive lookbehind: `(?<=Y)X` — X preceded by Y
- Negative lookbehind: `(?<!Y)X` — X not preceded by Y

Notes:

- Lookbehind and advanced assertions have varying support; see [Engine differences and portability](#engine-differences-and-portability).
- Variable-length lookbehind is often unsupported.

Examples:

- Number with commas: `(?<=\d)(?=(\d{3})+(?!\d))` used in replacement to insert commas
- Extract value after key: `(?<=\buser=)[^&\s]+`

## Escapes and Special Characters

- Escape metacharacters to match literally: `\.^$|?*+()[]{}\\`
- Newline `\n`, carriage return `\r`, tab `\t`
- Unicode code points: some engines support forms like `\u{1F600}` or named characters; hex escapes like `\xhh`/`\uhhhh` are common.

## Common Patterns

- Email (simple, practical):
  - `\b[\w.%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}\b`
- URL (simplified):
  - `\bhttps?:\/\/[\w.-]+(?:\:[0-9]+)?(?:\/[\w.~!#$&'()*+,;=:@%-]*)*\b`
- ISO date `YYYY-MM-DD`:
  - `\b\d{4}-\d{2}-\d{2}\b`
- Time `HH:MM` 24h:
  - `\b(?:[01]\d|2[0-3]):[0-5]\d\b`
- IPv4:
  - `\b(?:(?:25[0-5]|2[0-4]\d|[01]?\d?\d)\.){3}(?:25[0-5]|2[0-4]\d|[01]?\d?\d)\b`
- Hex color:
  - `#(?:[0-9A-Fa-f]{3}){1,2}\b`
- Slug:
  - `^[a-z0-9]+(?:-[a-z0-9]+)*$`
- US phone (common formats):
  - `\b(?:\+1[ -]?)?(?:\(\d{3}\)|\d{3})[ -]?\d{3}[ -]?\d{4}\b`

## Engine differences and portability

Regex engines mostly follow similar concepts, but details vary across flavors like PCRE/ECMAScript (JavaScript), .NET, Python `re`, Java, Ruby, and RE2 (Go). Use the notes below to write patterns that travel well and to spot portability pitfalls.

What varies across engines:

- Lookaround support

  - Most modern engines support lookahead; lookbehind is widely supported in .NET, Java, PCRE, Python 3.8+, and modern JS; older JS runtimes may lack it.
  - Variable-length lookbehind is often unsupported even where lookbehind exists.

- Backreferences and backtracking

  - Backreferences are unsupported in RE2 (used by Go and some tools), which also disallows lookaround to avoid catastrophic backtracking.
  - Backtracking engines (PCRE, .NET, Java, Python, JS) can hit performance cliffs on ambiguous patterns; prefer linear/safer constructions.

- Named group syntax and references

  - Group declaration variants: `(?<name>...)` or `(?P<name>...)`.
  - Backreference variants: `\k<name>`, `(?P=name)`, numeric like `\1`.
  - Replacement syntax varies: `$1`, `\1`, `${name}`, `\g<name>`.

- Flags and option names

  - Common flags exist but naming differs: ignore-case (i), multiline (m), dotall/singleline (s), verbose (x), Unicode (u), global (g).
  - “Multiline” typically changes `^`/`$` to match per line. “Singleline/dotall” makes `.` match newlines.

- Unicode semantics

  - Meaning of `\w`, `\b`, and case-insensitivity can change under Unicode vs ASCII modes. Enable Unicode mode where appropriate.

- Atomic/possessive behavior

  - Possessive quantifiers (`*+`, `++`) and atomic groups `(?>(...))` exist in PCRE/Java/.NET, but not in JS/Python.

- Anchors

  - `^`/`$` are affected by multiline; absolute anchors `\A`/`\z` are safer for whole-string matches where available.

- Global matching vs iteration

  - Some engines require explicit global iteration (e.g., a “global” flag or loop) to get all matches with captures.

- Safety and limits

  - Some environments support timeouts/limits; others (like RE2) avoid backtracking features entirely.

- String literal escaping
  - Language string syntax can require escaping backslashes. Prefer raw/verbatim strings when available to keep patterns readable.

Portability checklist:

- Prefer simple, explicit character classes over `.` when newlines or Unicode matter.
- Anchor validations with `^...$` or absolute `\A...\z` where available.
- Use non-capturing groups `(?:...)` unless you need captures; reduces accidental numbering mismatches.
- Avoid nested greedy constructs like `(.*)+`; tighten with classes or use lazy quantifiers `*?` where safe.
- Don’t rely on features missing in some engines (e.g., backreferences/lookbehind) if you must run on RE2.
- Document required flags and the engines you tested against.
- For performance-critical paths, prefer precompilation/caching and, where supported, timeouts or non-backtracking/linear-time options.

Mapping cheat sheet (concepts, not syntax):

- Ignore case: i / option flag
- Multiline line-anchors: m / option flag
- Dot matches newline: s / “singleline” option
- Free-spacing/comments: x / “verbose” option
- Unicode mode/classes: u / engine-specific Unicode switches
- Named groups/backrefs: one of `(?<name>...)`, `(?P<name>...)`, with backrefs `\k<name>`, `(?P=name)`
- Absolute anchors: `\A` start, `\z` end (where available)

Tip: When sharing a regex across tools, include a short note like “PCRE-compatible, requires dotall and Unicode flags” and provide a small set of test strings + expected matches.

## Practical Tasks

### Validation

- Strictly validate vs "good enough": prefer simpler patterns unless you must enforce exact spec.
- Use anchors `^...$` for full-string validation.

Example: username 3–16 chars, letters, digits, underscore:

```
^[A-Za-z0-9_]{3,16}$
```

### Extraction

Extract domain from email:

```
^[^@]+@(?<domain>[^@]+)$
```

Extract text between quotes (double):

```
"([^"]*)"
```

Extract key-value pairs like `key=value`:

```
\b(?<key>[A-Za-z_][A-Za-z0-9_]*)=(?<val>[^\s;]+)
```

### Replacement

Swap first and last name: "Doe, John" -> "John Doe"

Find: `^(?<last>[^,]+),\s*(?<first>.+)$`

Replace: first last (use your engine’s named‑group replacement syntax)

Insert commas in numbers: `1234567` -> `1,234,567`

Find: `\B(?=(\d{3})+(?!\d))` Replace with: `,`

Normalize whitespace: collapse multiple spaces/tabs to single space

Find: `\s+` Replace: single space

## Best Practices

- Start simple; only increase complexity when necessary.
- Anchor your pattern (`^...$`) for validations to prevent partial matches.
- Prefer readable, maintainable patterns. Use free-spacing/comments mode when available (`re.VERBOSE`, `(?x)`).
- Use non-capturing groups `(?:...)` when you don't need the capture.
- Be mindful of catastrophic backtracking; avoid nested greedy quantifiers like `(.*)+`.
- Benchmark on representative inputs if performance matters.
- Consider parser-based solutions for complex formats (e.g., full RFC-compliant emails/URLs).

## Troubleshooting

- Pattern matches too much: make quantifiers lazy (e.g., `.*?`) or constrain with character classes.
- No matches found: check escaping and anchors; test without anchors to isolate.
- Different results across languages: review engine differences (lookbehind, Unicode, flags).
- Slow regex: eliminate backtracking hotspots by tightening patterns or using atomic/possessive where supported.

## Tools & References

- regex101.com — PCRE/ECMAScript tester with explanations
- regexr.com — interactive builder and community patterns
- Debuggex.com — visual regex diagrams
- MDN Web Docs: Regular Expressions (JavaScript)
- Python `re` module documentation

---

Quick tip: When in doubt, add tests with sample inputs and expected matches to lock down behavior before refactoring a regex.
