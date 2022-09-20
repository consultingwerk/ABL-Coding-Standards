# Variable and Parameter Definitions

## Variables

Type     	| Prefix	| Possible alternative name
------------|-----------|--------------------------
INTEGER	    | i	        | i j n m
INT64	    | i	
DECIMAL	    | de	
DATE	    | da	
DATETIME    |	dt	
DATETIME_TZ	| dtz	
CHARACTER	| c	
LONGCHAR	| lc	
HANDLE	    | h	
COM-HANDLE	| ch	
LOGICAL	    | l	
RECID	    | re	
ROWID	    | ro	    | row_id, rowId
MEMPTR	    | m	
Progress.Lang.Object (and derived) | o	

*Nomen nest Omen* – names should specify what they are used for. It is considered a better practice to define two explicitly named variables rather than reusing a variable with an unclear name “just because it’s no longer needed in the original context”.

The variable names [i, j, n, m] are allowed as loop counters (INTEGER).

**Must-have rule:** If the variable names are short then only those four names should be used.

**Should Rule:** If there are nested loops then the pairs of i + j and n + m should be used.

## Parameters

While passing a variable to a procedure or defining a parameter the direction (INPUT / OUTPUT / INPUT-OUTPUT) it is preferred not to specify the INPUT option. It’s common to most development systems that the default parameter direction is INPUT.

Inside a procedure / function / method parameter names will be prefixed (before the data type prefix) with a **lower case p**.

In property SET methods, the parameter name may remain *“arg”* as suggested by the OpenEdge Architect wizard.

Usage:      | Sample                | Description
------------|-----------------------|----------------
Variable:	| daAppointmentDate	    | Datatype as prefix
Parameter:	| pdaAppointmentDate	| p{arameter} plus datatype as prefix

In the default CATCH block template provided by Progress Developer Studio it is o.k. to use the name *“err”* for the error being caught. In cases where multiple CATCH blocks for different error types are needed in a routine-level block it is recommended to use the normal naming rules for error objects (oException, oNotSupportedException, ...).

The name of variables used for Object references should allow to guess the type name of the referenced objects. 

oForm, oParentForm
oBusinessEntity

If the context makes it clear which “type” on object is from, it is o.k. to name reference variables based on the context only:

Sample           | Description
-----------------|---------------
oCustomerDataset | o.k. for CustomerDatasetModel
oCustomer        | o.k. for CustomerTableModel

## Grouping of variable declarations

Group variable declarations into logical blocks. Separate those blocks using blank lines. 

The AS and NO-UNDO phrases should be formatted in tabular fashion.

All variables have to be declared at the beginning of a routine level block.

```
DEFINE VARIABLE cEntity               AS CHARACTER                             NO-UNDO.
DEFINE VARIABLE cTables               AS CHARACTER                             NO-UNDO.
DEFINE VARIABLE cQueries              AS CHARACTER                             NO-UNDO.
DEFINE VARIABLE cJoins                AS CHARACTER                             NO-UNDO.
DEFINE VARIABLE iNumRecords           AS INTEGER                               NO-UNDO.
DEFINE VARIABLE hFindDataset          AS HANDLE                                NO-UNDO.
        
DEFINE VARIABLE cInitialContext       AS CHARACTER                             NO-UNDO.
DEFINE VARIABLE iPos                  AS INTEGER                               NO-UNDO.
        
DEFINE VARIABLE lWaitStateActive      AS LOGICAL                               NO-UNDO.
DEFINE VARIABLE cQueryString          AS CHARACTER                             NO-UNDO.
DEFINE VARIABLE lPositionWasZero      AS LOGICAL                               NO-UNDO INIT FALSE .
```

## Parameter definitions

All Parameters should be defined at the beginning of a PROCEDURE or FUNCTION.
