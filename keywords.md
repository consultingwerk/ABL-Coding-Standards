# ABL Keywords

As long as the official 4GL/ABL Documentation uses upper case keywords we use upper case keywords. Developers need to pay attention on casing, "the editor did not provide the proper case" is not an excuse.

All .NET Keywords (class names, class member names) should be exactly cased like in the .NET framework (typically camel cased with an initial capital letter). 

The Progress Compiler relies on the first reference of a .NET Class name in exact writing anyway. Further this makes it clearer what kind of keyword is used, Sample:

```
USING System.Windows.Forms.* FROM ASSEMBLY . 

DEFINE BUTTON btnOk             NO-UNDO . /* defines an ABL Button Widget */
DEFINE VARIABLE btnOk AS Button NO-UNDO . /* defines a .NET Button */
```
