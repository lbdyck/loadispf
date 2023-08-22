# LOADISPF
Load ISPF elements that are inline in the REXX source code.

## Syntax
`load_info = loadispf()`
`rc = dropispf(load_info)`

The inline ISPF resources are limited to ISPF Messages, Panels, and
Skeletons, CLISTs and EXECs are also supported.

The inline resources must start in column 1 and use the following
syntax:

>START    used to indicate the start of the inline data

>END    - used to indicate the end of the inline data

Each resource begins with a type record:
>type name
   where type is CLIST, EXEC, MSG, PANEL, SKEL name is the name of the element

## Sample
```
-* rexx *-
load_info = loadispf()
... magic code happens here (your code) ...
rc = dropispf(load_info)
exit
>Start inline elements
>Panel panel1
...
>Msg msg1
...
>End of inline elements
```
## Return from LOADISPF Routine
The list of ddnames allocated for use along with the libdef's performed
or altlib

The format is ddname libdef ddname libdef ...

    libdef may be altlibc or altlibe

    for altlib clist or altlib exec

## Comments
The entire rexx program is processed from the
last record to the first to find the >START
record at which point all records from that
point on are processed until the >END
statement or the end of the program is found.

It is *strongly* suggested that the inline
elements be at the very end of your code so
that the search for them is faster.

Inline ISPTLIB or ISPLLIB were not supported
because the values for these would have to be
in hex.
