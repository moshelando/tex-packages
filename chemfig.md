> PREAMBLE

```javascript
\usepackage{chemfig}
```

> INSTANTIATION

The code is placed within:

```javascript
\chemfig{<code>}
```

> PRIMITIVE ELEMENTS

Primitive elements include vertices, or *atoms*, and edges, or *bonds*.

*Atoms* do not need to be actual atoms or molecules; any math-mode text works.

*Bonds* include:

```javascript
-   single
=   double
~   triple
>   right cram
<   left cram
>:  right cram dashed
<:  left cram dashed
```

> DRAWING STRUCTURE

The overall structure follows *turtle*-type instructions, where the drawer has directionality and procedurally draws each element, only changing direction when instructed.

The turtle begins facing east.

To draw a linear molecule:

```javascript
\chemfig{A-B}
```

This draws, from left to right, an `A` atom, a single bond, and a `B` atom.

Atoms are not required at vertices:

```javascript
\chemfig{-O}
```

If atoms are not provided, two bonds will directly attach:

```javascript
\chemfig{-=}
```

> CHANGING DIRECTION

To change the angle of a bond, place the angle command in brackets after the bond.

Default angle commands are integer multiples of 45°.

```javascript
\chemfig{A-[2]B}
```

This draws an `A` atom, a bond at 90° above it, and a `B` atom above that. Once the turtle direction is changed through an angled bond, it assumes the new direction until explicitly changed.

The default 45° increment can be changed in brackets after `\chemfig`, prior to `{<code>}`:

```javascript
\chemfig[angle increment = 30]{A-[1]B}
```

Additionally, specific angles—both absolute and relative to the current turtle direction—can be assigned directly:

- absolute: `[:n]`
- relative: `[::n]`

> BRANCHES

Branches are placed in parentheses. When the parentheses end, the turtle reverts to the pre-parentheses state:

```javascript
\chemfig{A(-[2]B)-C}
```

Branches may be nested.

> HOOKS

So far, an atom is attached to a bond by placing the atom immediately after the bond. To instead attach a bond to an already existing atom, use *hooks*, denoted `?`.

Immediately after the first atom, place `?`. After the second atom, place another `?`. This draws a single bond between the two atoms.

Hooks can be customized with specific names and non-single bonds using:

```javascript
?[<name>,{<bond>}]
```

Both arguments are placed in brackets after the first hook. Place the bond specification in curly braces. To later invoke the named hook, use:

```javascript
?[<name>]
```

> MODIFIERS

Modifiers, or *charges*, can be placed on atoms by preceding the atom with:

```javascript
\charge{<position in degrees>=<charge element>}{<atom>}

```

For example, to place a `2−` charge northeast of `O`:

```javascript
\charge{45=2-}{O}
```

`<charge element>` may be any text or specified `$<math>$`.

Common math symbols include `$\oplus$` and `$\ominus$`.

Chemfig provides specific references for Lewis dots: `\.` and `\:`.

Multiple charges may be placed on a single atom:

```javascript
\chemfig{\charge{0=\.,90=\.,180=\.,270=\.}{C}}
```

> BOND CUSTOMIZATION ARGUMENTS

We previously mentioned `<angle>` as the first indexed argument for `<bond>`.

Here we cover indices 2–4. If an argument for a lower index is omitted, include a comma to advance the index.

**Index 2** sets bond length (default = 1):

```javascript
\chemfig{A[,0.5]-B}
```

**Indices 3 and 4** control bond attachment points in multi-letter atoms. By default:

- bonds in quadrants I and IV attach to the rightmost letter
- bonds in quadrants II and III attach to the leftmost letter

To override this, specify the integer index of the desired letter.
The third index is the *departure* letter, and the fourth is the *arrival* letter.
Departure and arrival follow the turtle drawing sequence.

> RINGS

For rings, instead of specifying each bond angle, declare that `n` bonds form a ring. Bond angles are then assigned automatically.

Syntax:

```javascript
*n(<code>)
```

`*` initiates the ring statement. `n` is the number of sides. The bonds in `<code>` are placed sequentially at `360/n` angles.

```javascript
\chemfig{A*5(----O-)}
```

This creates a five-bond ring starting and ending at `A`, with mostly blank vertices and one `O`.

The ring statement does not itself place bonds; it only iterates angles for the bonds inside the parentheses. If fewer bonds than `n` are given, only those bonds are placed.

A ring does not need to follow a letter:

```javascript
\chemfig{*5(-----)}
```

This places a five-sided ring with no atoms.

> RING ORIENTATION

By default, the origin of a ring is the southwest corner.

This can be changed by placing a direction before the ring or the atom from which it extends:

```javascript
\chemfig{[:30]A*5(-----)}
```

If a ring is placed after a bond, it proceeds in the direction of that bond, with the leading bond bisecting the angle between the first and last bonds in the ring.

> RING BRANCHES

Atoms or plain vertices within rings may be branched:

```javascript
\chemfig{*5(--(-O)---)}
```

A molecule may begin with a ring and immediately branch from the first vertex:

```javascript
\chemfig{*5((-O)-----)}
```

To attach two rings, draw the second ring from a vertex of the first. Typically, the final bond of the second ring overlaps a bond of the first, so it is omitted.

> POTENTIAL RING ISSUES

**Issue 1**

When two rings are attached, a bond from one ring may intrude into an atom of the other. Example:

```javascript
\chemfig{A-B*5(-C-D*5(-X-Y-Z-)-E-F-)}
```

Here, the last bond of the second ring is omitted to avoid overlap, but the preceding bond extends to a vertex instead of attaching to `E`.

Two solutions:

**(a) Use hooks** to attach `E`:

```javascript
\chemfig{A-B*5(-C-D*5(-X-Y-Z?)-E?-F-)}
```

**(b) Insert a phantom atom** at the vertex:

```javascript
\chemfig{A-B*5(-C-D*5(-X-Y-Z-\phantom{E})-E-F-)}
```

**Issue 2**

If ring vertices contain multi-letter atoms, the automatic ring layout may appear lopsided, since spacing is based on first and last letters.

Solution: manually specify departure and arrival indices, choosing the letter on the side of the atom facing the ring.

> CUSTOM SCRIPTS

Custom macros may be defined as:

```javascript
\definesubmol{<name>}{<code>}
```

and invoked with:

```javascript
!{<name>}
```

Alternatively, define them as commands:

```javascript
\definesubmol\<command>{<code>}
```

and invoke with:

```javascript
!\command
```

Both forms simply paste the defined code.

The `{name}` form cannot take arguments. The `\command` form can:

```javascript
\definesubmol\<command><n>{<code>}
```

where `<n>` is the number of arguments. Refer to them inside `<code>` as `#1`, `#2`, etc., where the number corresponds to the argument index.
