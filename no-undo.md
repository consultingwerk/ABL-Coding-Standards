# The usage of “NO-UNDO” when defining variables or temp-tables

Always use the NO-UNDO option while defining variables or temp-tables. It increases the runtime efficiency of the generated R-Code cause no “before values” will be processed and stored in the local .lbi-file or memory. It is especially recommended to use this option with temp-tables because the overhead is larger here than it is for a single variable.

```
DEFINE VARIABLE i            AS INTEGER NO-UNDO .
DEFINE PARAMETER piParameter AS INTEGER NO-UNDO .
```

**Must-use rule: Always use “NO-UNDO“ option**

In those really rare circumstances where the default undo behavior is needed, the developer has to provide a short description like the following so that other developers don’t get the impression that the NO-UNDO option was just forgotten and may break the code during refactoring.

```
DEFINE VARIABLE i AS INTEGER. /* UNDO, as the loop counter 
                                 needs to be reset in case of 
                                 error. */
```
