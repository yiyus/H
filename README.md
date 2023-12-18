H
===

The namespace H provides functions for quaternion multiplication in Dyalog APL.

Any array of rank 1 and length 4 with conformant elements can be considered a
quaternion. Two quaternions can be multiplied together if their elements, which
can be nested arrays, conform.

For example, all these arrays are valid quaternions:

        a←?4⍴0         ⍝ quaternion with scalar elements
        b←?4⍴⊂3⍴0      ⍝ quaternion with list elements
        c←?4⍴⊂2 3⍴0    ⍝ quaternion with matrix elements
        d←0 w@0 2⊢c    ⍝ quaternoin with mixed matrix and scalar elements

And all of these multiplications are valid:

        (⊂a)H.P¨a b c d
        (⊂b)H.P¨a b      ⍝ elements of b and c/d do not conform
        (⊂c)H.P¨a   c d
        (⊂d)H.P¨a   c d

In addition to the quaternion multiplication function `H.P`, an operator `H._P`
is provided, which can be used to apply different products. Eg:

        ⍴¨∘.×H._P⍨c
    ┌───────┬───────┬───────┬───────┐
    │2 3 2 3│2 3 2 3│2 3 2 3│2 3 2 3│
    └───────┴───────┴───────┴───────┘
        ⍴¨c+.×H._P⍉¨c
    ┌───┬───┬───┬───┐
    │2 2│2 2│2 2│2 2│
    └───┴───┴───┴───┘

The function `H.P` is equivalent to `H.(×P)`, but slightly faster.

Variables `uijk` refer to the base components of quaternions (see Hamilton 1843):

        H.(u i j k)
    ┌───────┬───────┬───────┬───────┐
    │1 0 0 0│0 1 0 0│0 0 1 0│0 0 0 1│
    └───────┴───────┴───────┴───────┘

Several auxiliary functions are provided:

    C     ⍝ quaternion conjugate (monadic)
    D     ⍝ quaternion dot product (dyadic)
    M     ⍝ quaternion magnitude (monadic)
    U     ⍝ quaternion of given magnitude (dyadic, monadic for unitary)
    A     ⍝ quaternion from axis and angle in radians (dyadic, monadic for z)
    AD    ⍝ quaternion from axis and angle in degrees (dyadic, monadic for z)
    E     ⍝ quaternion from Euler angles in radians (dyadic, monadic for xyz)
    ED    ⍝ quaternion from Euler angle in degrees (dyadic, monadic for xyz)
    RND   ⍝ generate random quaternions (dyadic, monadic for unitary)

The function `Test` (niladic) runs several tests.
