> ORBITAL BOX DIAGRAMS

Orbital box diagrams are a common chemical notation used to depict the occupancy and spin of electrons in atomic orbitals. Each orbital is represented as a box, and each electron as an arrow within the box.

This macro provides a simple way to typeset such diagrams using TikZ.

The macro draws **notation only**; it does not model orbital energies or electron filling rules.

The macro does not infer subshell size or apply filling rules; the diagram is drawn exactly as specified.

Hund’s rule, pairing, and exceptions are handled explicitly by the input.

> MAIN COMMAND

Orbital box diagrams are drawn using:

```
\orbox{<groups>}
```

This command draws **one horizontal line** of orbital boxes, grouped by subshell.

> GROUP SYNTAX

Each group has the form:

```
{<subshell label>}{<electron list>}
```

where:

- `<subshell label>` is the subshell label (`1s`, `2p`, `3d`, etc.)
- `<electron list>` is a comma-separated list specifying the number of electrons in each orbital

Groups are separated by semicolons.

> ELECTRON LIST

Each entry in `<electron list>` corresponds to **one orbital box**.

Allowed values are:

- `0` — empty orbital
- `1` — singly occupied orbital (spin up)
- `2` — doubly occupied orbital (spin up and spin down)

The number of entries in the list determines the number of boxes drawn.

Example:

```
{3d}{1,1,0,0,0}
```

draws five boxes (a `d` subshell), with two singly occupied orbitals and three empty orbitals.

> EXAMPLE

```
\orbox{
    {1s}{2};
    {2s}{2};
    {2p}{2,2,2};
    {3s}{2};
    {3p}{2,2,2};
    {4s}{2};
    {3d}{1,1,0,0,0}
}
```

This produces a single horizontal orbital box diagram showing filled `s` and `p` subshells and a partially filled `3d` subshell.
