# General coding style

Bad Examples:

```
Def var i as i NO-UNDO.
Disp i .
```


4GL/ABL keywords must be written out unabbreviated. Always uppercase 4GL/ABL keywords.

1.	It’s more readable for human
2.	It’s more readable for tools (easier to search and replace)
3.	It’s more aligned with OpenEdge documentation and samples (except those published by Progress Software recently with the OERA samples)

```
DEFINE VARIABLE i AS INTEGER NO-UNDO .
DISPLAY i .
```

There are a few ABL keywords where the ABL documentation obviously provides an abbreviated form. One example is the RCODE-INFO system-handle. This appears to be an abbreviation for RCODE-INFORMATION.

It is considered good practice to use the documented form and not the undocumented form in cases like this.
