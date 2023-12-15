H
===

The namespace H provides functions for quaternion multiplication in Dyalog APL.

Any array with four elements along its last axis with conformant elements can
be considered as a quaternion. Two quaternions can be multiplied together if
their elements conform.

For example, all these arrays are valid quaternions:

        a←?4⍴0            ⍝ simple quaternion with scalar elements
        b←?2 3 4⍴0        ⍝ array of quaternions with scalar elements
        c←?4⍴⊂2 3⍴0       ⍝ quaternion with array elements
        d←?2 3 4⍴⊂2 3⍴0   ⍝ array of quaternions with array elements

And all of these quaternions can be multiplied between them:

        (⍴¨∘.H.P⍨a b c d)((⍴∘⊃)¨∘.H.P⍨a b c d)
    ┌─────────────────────────┬─────────────────┐
    │┌─────┬─────┬─────┬─────┐│┌───┬───┬───┬───┐│
    ││4    │2 3 4│4    │2 3 4│││   │   │2 3│2 3││
    │├─────┼─────┼─────┼─────┤│├───┼───┼───┼───┤│
    ││2 3 4│2 3 4│2 3 4│2 3 4│││   │   │2 3│2 3││
    │├─────┼─────┼─────┼─────┤│├───┼───┼───┼───┤│
    ││4    │2 3 4│4    │2 3 4│││2 3│2 3│2 3│2 3││
    │├─────┼─────┼─────┼─────┤│├───┼───┼───┼───┤│
    ││2 3 4│2 3 4│2 3 4│2 3 4│││2 3│2 3│2 3│2 3││
    │└─────┴─────┴─────┴─────┘│└───┴───┴───┴───┘│
    └─────────────────────────┴─────────────────┘

It is also possible to combine scalar and array elements in a quaternion:

        e←0(?0)@0 2⊢c
        ⍴∘⊃¨(a c,3⍴⊂e)H.P¨(3⍴⊂e),a c 
    ┌─────┬─────┬─────┬─────┬─────┐
    │3 2 4│3 2 4│3 2 4│3 2 4│3 2 4│
    └─────┴─────┴─────┴─────┴─────┘

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
