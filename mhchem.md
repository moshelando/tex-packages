> PREAMBLE

```javascript
\usepackage[version=4]{mhchem
```

> MODES

```javascript
\ce{<formula>}
```

Works in all modes: text, math, and headings.

A `$<math>$` expression may be placed inside `\ce{<formula>}`, and vice versa, with multiple levels of nesting.

The font used follows the current mode (text or math). This can be changed in the preamble:

```javascript
\mhchemoptions{textfontcommand=\<font>}
\mhchemoptions{mathfontcommand=\<font>}
```

> INTERPRETING SUBSCRIPTS AND SUPERSCRIPTS

Numbers immediately following species are treated as subscripts:

```javascript
H2O   →   H₂O
```

Unnumbered charges immediately following species are treated as superscripts:

```javascript
H+    →   H⁺
H-    →   H⁻
```

Numbered charges must be explicitly superscripted, but do not require braces:

```javascript
O^2-  →   O²⁻
```

Numbers immediately preceding species are treated as stoichiometric coefficients, and a space is inserted, unless the number can be interpreted as a subscript:

```javascript
2H2O  →   2 H₂O
```

Nuclides and isotopes are designated using `^` and `_`:

```javascript
\ce{^227_90Th+}
```

> SYMBOLS

Arithmetic and relational symbols:

```javascript
+   
-   
=   
\pm
*   (renders as \cdot)
```

Bond symbols:

```javascript
-   single bond
=   double bond
#   triple bond

```

Note that `-` and `=` may also represent non-bond meanings. `mhchem` attempts to infer intent automatically.

To explicitly force a bond, use:

```javascript
\bond{<n>}
```

To suppress automatic bond interpretation, wrap the symbol in braces:

```javascript
{-}   
{=}
```

Reaction arrows:

```javascript
->     right
<-     left
<-->   stacked left–right
<=>    equilibrium (harpoons)

```

General arrow form:

```javascript
<arrowsymbol>[<text above>][<text below>]
```

Vertical arrows:

```javascript
v     down arrow
(^)   up arrow
```

If not automatically parsed, use `(v)`; to escape, use `{v}`.

For stacked fractions, use `\frac` in math mode:

```javascript
\ce{K = $\frac{\ce{Mg}}{\ce{Mg+}}$}
```

Parentheses and brackets may be used freely inside `\ce`.

To place underset text, use `\underset` in math mode:

```javascript
\ce{H+ $\underset{\text{water}}{\ce{H2O}}$}
```

> VARIABLES AND ITALICIZATION

Common variable symbols (e.g., `n`, `x`) are automatically parsed and italicized.

To prevent parsing, wrap the symbol in braces:

```javascript
{n}
```

To explicitly italicize, use math mode.

> STYLING

`\ce` works inside alignment environments:

```javascript
\begin{align*}
\ce{A & -> B \\ C & -> D}
\end{align*}
```

> CUSTOM COMMANDS

Custom commands may be defined in the preamble:

```javascript
\newcommand\<commandname>{<code>}
```

Commands may take arguments:

```javascript
\newcommand\<commandname>[<number of arguments>]{<code>}
```

Within `<code>`, reference arguments as `#1`, `#2`, etc., where the number corresponds to the argument index.
