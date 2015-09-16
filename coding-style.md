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

# Test Code (Debugging through messages)

While all program code should be nicely indented following it's block structure, test messages etc. are supposed to be aligned to the very left of the source code.

Example:

```
            DatasetHelper:ThrowDatasetErrors (DATASET dsAuftragsart:HANDLE) . 

            FIND FIRST eAuftragsart .
            
BufferHelper:ShowBuffer (BUFFER eAuftragsart:HANDLE) .
            
            /* Mandant/Unternehmen should be assigned by HaufeDataAccess:CommitChanges */
            FIND Auftragsart WHERE Auftragsart.MandantNr     = oAppSession:Tenant:Mandant 
                               AND Auftragsart.Unternehmen   = oAppSession:Tenant:Unternehmen
                               AND Auftragsart.AuftragsartNr = iAuftragsArtNr
                NO-LOCK NO-ERROR . 
```

This makes it more obvious that the code should be removed before finalizing the work.
