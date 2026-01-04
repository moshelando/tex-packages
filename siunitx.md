> **siunitx overview**

The **siunitx** package mainly consists of:

- `\num`
- `\unit`
- `\qty` (essentially `<num><unit>`)

> **Scope**

`siunitx` can be used in **any environment**:

- math mode
- regular text
- headings
- captions, etc.

> **\num**

`\num[<options>]{<number>}`

**Formatting behavior**

Adds a leading zero before decimals:

`\num{.25} → 0.25`

Converts scientific notation:

`\num{5e6}  → 5 × 10^{6}`
`\num{5e-6} → 5 × 10^{-6}`

> **\unit**

`\unit[<options>]{<unit>}`


`\unit` accepts both **literals** and **macros**.

Examples:

`\unit{cm^2}`
`\unit{\centi\meter\squared}`


**Unit literals**

- `.` and `~` indicate an **inter-unit product**, rendered as a space
- `_` places the next character or `{<group>}` as a subscript
- `^` places the next character or `{<group>}` as a superscript

**Unit macros**

Includes:

- **prefixes**, e.g. `\kilo`
- **units**, e.g. `\gram`

Rules:

- A prefix followed by a unit is parsed as a single unit
- Adjacent units imply an inter-unit product and are space-separated

`**\per**`

`\per` expresses division between units and has **three modes**:

- **reciprocal** (default): renders the following unit with exponent −1
- **symbol**: renders a `/`
- **fraction**: renders a stacked fraction

To locally change per-mode:

`\unit[per-mode=symbol]{\meter\per\second}`

To globally change per-mode, place the following in the preamble:

`\sisetup{`
  `per-mode = <symbol / fraction>`
`}`

**Powers**

- `\squared`, `\cubed` apply to the **previous unit**
- `\square`, `\cubic` apply to the **next unit**

To assign explicit powers, use either:

`<unit>\tothe{n}`

or

`\raiseto{n}<unit>`

**Subscripts**

`<main>\of{<sub>}`


**Cancellation**

If the `cancel` package is loaded, `\cancel` may be used and applies to the **next unit token**.

> **Accepted Units**

The following are common accepted units. For each, use either the symbol literal or the macro command:

**SI base units**

| Unit | Command | Symbol |
| --- | --- | --- |
| ampere | `\ampere` | A |
| candela | `\candela` | cd |
| kelvin | `\kelvin` | K |
| kilogram | `\kilogram` | kg |
| meter | `\meter` | m |
| mole | `\mole` | mol |
| second | `\second` | s |

**Additional units**

| Unit | Command | Symbol |
| --- | --- | --- |
| coulomb | `\coulomb` | C |
| decibel | `\decibel` | dB |
| degree | `\degree` | ° |
| degree Celsius | `\degreeCelsius` | °C |
| electronvolt | `\electronvolt` | eV |
| farad | `\farad` | F |
| hertz | `\hertz` | Hz |
| hour | `\hour` | h |
| joule | `\joule` | J |
| liter | `\liter` | L |
| newton | `\newton` | N |
| ohm | `\ohm` | Ω |
| pascal | `\pascal` | Pa |
| radian | `\radian` | rad |
| tesla | `\tesla` | T |
| volt | `\volt` | V |
| watt | `\watt` | W |

**Prefixes**

| Prefix | Command | Symbol | Power |
| --- | --- | --- | --- |
| pico | `\pico` | p | −12 |
| nano | `\nano` | n | −9 |
| micro | `\micro` | μ | −6 |
| milli | `\milli` | m | −3 |
| centi | `\centi` | c | −2 |
| deci | `\deci` | d | −1 |
| deca | `\deca` | da | 1 |
| kilo | `\kilo` | k | 3 |
| mega | `\mega` | M | 6 |
| giga | `\giga` | G | 9 |

**Common prefix–unit combinations**

Common prefix-unit combinations have dedicated macros:

| Unit | Command | Symbol |
| --- | --- | --- |
| nanogram | `\ng` | ng |
| microgram | `\ug` | μg |
| milligram | `\mg` | mg |
| gram | `\g` | g |
| kilogram | `\kg` | kg |
| picometre | `\pm` | pm |
| nanometre | `\nm` | nm |
| micrometre | `\um` | μm |
| millimetre | `\mm` | mm |
| centimetre | `\cm` | cm |
| decimetre | `\dm` | dm |
| metre | `\m` | m |
| kilometre | `\km` | km |
| nanosecond | `\ns` | ns |
| microsecond | `\us` | μs |
| millisecond | `\ms` | ms |
| second | `\s` | s |
| femtomole | `\fmol` | fmol |
| picomole | `\pmol` | pmol |
| nanomole | `\nmol` | nmol |
| micromole | `\umol` | μmol |
| millimole | `\mmol` | mmol |
| mole | `\mol` | mol |
| kilomole | `\kmol` | kmol |
| milliliter | `\mL` | mL |
| liter | `\L` | L |

> **\qty**

`\qty[<options>]{<number>}{<unit>}`


`\qty` formats a quantity by:

- formatting `<number>` using `\num`
- formatting `<unit>` using `\unit`
- inserting a space between `<number>` and `\unit`

`<options>` may include both **number** and **unit** options.
