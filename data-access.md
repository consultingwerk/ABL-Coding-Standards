# Accessing Data with 4GL/ABL

```
FIND	(Table / Buffer)	[NO-LOCK | SHARE-LOCK | EXCLUSIVE-LOCK]
FOR EACH			        [NO-LOCK | SHARE-LOCK | EXCLUSIVE-LOCK]
PRESELECT EACH		        [NO-LOCK | SHARE-LOCK | EXCLUSIVE-LOCK]
GET				            [NO-LOCK | SHARE-LOCK | EXCLUSIVE-LOCK]
```

It is strongly recommended to read all data from a database in NO-LOCK mode.
 
The session-parameter (-NL NO-LOCK by default) was introduced to change the compiler default we do consider it as problematic when code from different sources is combined in a single project and changing the default lock mode can cause issues (SHARE-LOCK may be expected by legacy code or the Progress Dynamics source code as the default).

Therefore we will neither use the –NL startup parameter nor rely on any default lock mode.

The usage of SHARE-LOCK may be required in some (rather rare) circumstances. There should be a short explanation why it is used in source code.

**Must-use rule: Always specify the lock mode using the NO-LOCK / SHARE-LOCK / EXCLUSIVE-LOCK option with each record access. Do not rely on –NL or any default lock mode.**

Any data access from database tables without explicitly specifying the LOCK type is prohibited.

Temp-Tables data access does not require the specification of a LOCK type. However it is not considered a mistake when data access on temp-tables is coded with a LOCK type specification.
 
While refactoring code a buffer once defined against a database table might be used for a temp-table table later and vice versa. When it is expected that code written against temp-tables initially may be used against database tables later, it is considered good practice to specify the LOCK type when writing the code initially. 

```
FIND-FIRST ttCustomer NO-LOCK.
```
