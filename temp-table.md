# Temp-Table Definitions

See related: [Naming of Buffers and Temp-Tables](naming-buffer-and-temp-table.md "Naming of Buffers and Temp-Tables")

TEMP-TABLE definitions should to be stored in include file for allowing reuse.

It is considered very helpful to provide compile time parameters for the access mode to those temp-tables:

```
DEFINE {1} TEMP-TABLE ttXXX NO-UNDO
	...
```

When temp-tables are used within Business Entities further options may be needed as compile time parameters:

```
DEFINE {&ACCESS} TEMP-TABLE eCustomer{&SUFFIX} NO-UNDO 
	{&REFERENCE-ONLY} 
	&IF DEFINED (NO-BEFORE) EQ 0 &THEN BEFORE-TABLE eCustomerBefore{&SUFFIX} &ENDIF
```

Include File Parameter| Description
----------------------|-----------------
ACCESS                | Class Member Access (PRIVATE/PROTECTED/STATIC)
SUFFIX				  | A name suffix if a routine needs to define the same temp-table twice in a single compile-unit
REFERENCE-ONLY	      | Allows to pass the "REFERENCE-ONLY" option when a temp-table is only needed with BIND or BY-REFERENCE
NO-BEFORE             | When set, the temp-table definition ommits the definition of the before-table

This allows to provide the PRIVATE/PROTECTED/STATIC option as a parameter to those include files if needed.
