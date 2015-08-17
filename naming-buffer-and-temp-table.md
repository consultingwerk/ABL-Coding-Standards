# Naming of Buffers and Temp-Tables

```
DEFINE BUFFER {Buffer-Name} FOR Customer.
DEFINE TEMP-TABLE ttCustomer NO-UNDO LIKE Customer.
```

When defining a buffer or a temp-table the name should be build out of the role of the buffer or temp-table in the current context and the table name of the related database or temp-table as a prefix.

{Buffer-Name} -> SourceCustomer
 
If we now add a column name as shown below this provides an effective advantage when searching for all occurrences of a column name of a table.

Source**Customer.CustNum**

This is a nice to have rule. So exceptions are o.k.

Before-Tables defined for ProDataset temp-tables do not follow this form. As before-tables and after-tables (the normal temp-table name) are typically used in the same context it is considered that this makes code easier readable.
