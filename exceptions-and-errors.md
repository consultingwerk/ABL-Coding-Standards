# Exceptions / Errors

In all new code, we use structured error handling. So all new classes and procedure files use

```
ROUTINE-LEVEL ON ERROR UNDO, THROW. 
```
or
```
BLOCK-LEVEL ON ERROR UNDO, THROW. 
```

BLOCK-LEVEL should be used when we know that code is only executed on OpenEdge 11.3 and above. It is not allowed to use conditional compilation to determine the use of ROUTINE-LEVEL or BLOCK-LEVEL as error handling is a critical property of code execution. 

When ROUTINE-LEVEL error handling is used, all loops with default error handling, should use the ON ERROR UNDO, THROW option:

```
FOR EACH Customer ON ERROR UNDO, THROW:
```

As typically the mix of standard (old style) error handling options like ON ERROR UNDO, NEXT from within loops and ON ERROR UNDO, THROW for routine blocks has unexpected side effects.

Block with no default error handling should use the ON ERROR UNDO, THROW option when they need a CATCH or FINALLY block.

```
IF <condition> THEN DO ON ERROR UNDO, THROW:


   CATCH err AS Progress.Lang.Error:
   END CATCH. 
END.
```

## Event handler

All UI Event handler should have a CATCH for Progress.Lang.Error at the end.
If error are not catched here, errors would be thrown to the WAIT-FOR statement which would only display the default error message dialog, which does not look pretty and does not provide further debugging output (other than the stack trace).

```
METHOD PRIVATE VOID button1_Click (sender AS System.Object, e AS System.EventArgs):

    /* Event handler code */

    CATCH err AS Progress.Lang.Error:
        Consultingwerk.Util.ErrorHelper:ShowErrorMessage (err) . 
    END CATCH . 
END METHOD.
```

### Error classes

Especially in framework code – but typically also in application code – the usage of specialized error classes is recommended when throwing errors, so statements like this

```
UNDO, THROW NEW Progress.Lang.AppError (“This is an error”, 0). 
```

should be avoided.

For Consultingwerk all custom error classes should inherit from Consultingwerk.Exceptions.Exception as this carries further debugging information. 

All error classes should be defined SERIALIZABLE on OpenEdge 11.4. The SERIALIZABLE flag might by defined with conditional compilation so that in OpenEdge 11.3 and before the SERIALIZABLE is not used (the Service Interface will ensure the proper transportation of the error message in that case). 

```
{Consultingwerk/products.i}
USING Consultingwerk.Exceptions.* FROM PROPATH .
USING Progress.Lang.*             FROM PROPATH .

CLASS Consultingwerk.Exceptions.InvalidValueException 
    INHERITS Exception
    {&SERIALIZABLE}:  
```

{&SERIALIZABLE} is defined in Consultingwerk/products.i

Errors should always be thrown with error messages. As such the constructor of the Progress.Lang.AppError should be invoked with a CHARACTER and a number (zero is o.k.). Because otherwise the error would be initialized with a RETURN-VALUE property and the default AVM error handling would not show the error message. 

Errors should be thrown like this (or preferably a derived type resulting in the same constructor):

```
UNDO, THROW NEW Progress.Lang.AppError  (“Error message”, 0). 
```

These errors should NOT be used:

```
UNDO, THROW NEW Progress.Lang.AppError  (“Return value”). 
```

