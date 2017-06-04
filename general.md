# General conventions

## WIDGETS

If WIDGETs are created in the code, always create a WIDGET POOL using the “CREATE WIDGET POOL” statement or the USE-WIDGET-POOL option of the CLASS statement.

And then use the "DELETE OBJECT" statement with "IF VALID-HANDLE" or "IF VALID-OBJECT" in the FINALLY block (alternatively use the Consultingwerk.Util.GarbageCollectorHelper).

Exception are those widget references that are returned to the outside from factory methods.

## IF and CASE

If nested formatting of a single IF statement increases readability, this is considered good practice. But it should not be overdone.

```
IF THIS-OBJECT:DesignTime THEN 
    RETURN FALSE . 
```

```
IF VALID-HANDLE(hDataset) AND 
   NOT THIS-OBJECT:FindString > "":U THEN
    hDataset:EMPTY-DATASET ()   .
```

```
IF VALID-OBJECT (THIS-OBJECT:SmartDataSource) AND THIS-OBJECT:ForeignFields > "":U THEN 

    THIS-OBJECT:FetchQueryString = SUBSTITUTE("&1 &2":U, 
                                              THIS-OBJECT:EvaluateParentQuery (), 
                                              THIS-OBJECT:QuerySort).
ELSE DO:
    IF THIS-OBJECT:QueryString = "":U AND THIS-OBJECT:QuerySort > "":U THEN
        THIS-OBJECT:FetchQueryString = SUBSTITUTE ("FOR EACH &1 &2":U,
                                                   THIS-OBJECT:EntityTable,
                                                   THIS-OBJECT:QuerySort) .
    ELSE
        THIS-OBJECT:FetchQueryString = SUBSTITUTE("&1 &2":U,
                                                  THIS-OBJECT:QueryString,
                                                  THIS-OBJECT:QuerySort).
END.
```

A THEN DO or ELSE DO block is recommended when a THEN contains an IF statement and one of the two IF statements uses an ELSE option. 

In case of a sequence of IF statements on related conditions it is recommended to use a CASE block.

When coding an IF statement with only one command following no DO block is required and the statement should be broken with indentation into the following line.

```
IF ... THEN
    Statement
```

```
IF ... THEN DO:
    Statement.
    Statement.
END.
```

When inserting more than one statements between the if statement the DO is kept in the line with the IF. 

Inline statements are indented with 4 leading spaces and the END is on the same indentation level as the IF.

```
IF ... THEN
    IF ... THEN
        Statement.
    ELSE
        Statement.
```
```
IF ... THEN DO:
    IF ... THEN
        Statement.
    ELSE
        Statement.
END.
ELSE
    Statement.
```

When there is more than one comparison for a single IF statement then the operator AND / OR is at the end of the first line and the next parameter (variable or else) is at the same level of the first comparison.

```
IF a = b AND
   c = d THEN
    Statement.
```
```
IF (a = b AND
    c = d) OR
   x = y THEN
    Statement.
```
When the DO Block following the IF requires additional options, the following formatting should be considered:

```
IF ... THEN
DO TRANSACTION:

END.
```

```
IF ... THEN
DO ON ERROR UNDO, THROW:

END.
```

```
IF ... THEN
FOR EACH|REPEAT

END.
```

## END statements

End statements should use the option to specify the block type they are closing, like 

```
END CASE.
END METHOD.
END CONSTRUCTOR.
END FUNCTION.
END PROCEDURE. 
```

## File Header information’s

Always give an Author Name and the Company.
Author Name / Consultingwerk Ltd.


## FOR EACH statements

```
FOR EACH ...:
    IF ... THEN NEXT.
```

Coding an “IF ... THEN NEXT.” is only allowed if the condition cannot be added to the query. (e.g.: UDF UserDefinedFunction). A reason should be added as a comment why the condition is not expressed in the query.

```
FOR EACH ...:
	FIND [FIRST] {WEHERE|OF} ... .
	IF AVAILABLE THEN DO:
```

The “FIND ...” should be included into the “FOR EACH” and if needed coded with an OUTER-JOIN.

## Formatting of FOR EACH blocks

```
FOR EACH Table1 WHERE Table1.Field
FOR EACH Table1 WHERE Table1.Field1  = xyz
                  AND Table1.Field  >= xyz
                  AND Table1.Field  <= xyz {NO-LOCK(,I:)}
                BY xxx
    EACH|FIRST|LAST Table2 WHERE (Table2.Field  = xyz
                             AND  Table2.Field >= xyz)
                              OR (Table2.Field  = xyz)
```


## Other formatting

```
ASSIGN i = 42.

ASSIGN
    i = 42
    j = 84
    .
```
### FRAME

```
ASSIGN [FRAME{FrameName}]
    Field1
    Field2
    Field3
    .
```

```
UPDATE {[place here if only one field].}
    Field1
    Field2
    Field3
    .
```

```
DISPLAY
    Field1
    Filed2
    Field3
    [WITH FRAME {FrameName}]
    .
```

### Comments

## Style

A normal comment uses the "old" style of coding.

/* here is the comment */

A typical comment including the name of the editor and the date would look like this:

/* Marko Rueterbories / Consultingwerk Ltd. 04.06.2017:
   Changed something here */

## Restriction

As a matter of fact, as long as we are supporting older versions of OpenEdge prior to 11.6 it is not allowed to use double slashes "//" style comments. Doing this would break the build in all older versions of OpenEdge. 
