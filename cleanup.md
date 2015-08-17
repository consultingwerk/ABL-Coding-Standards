# Cleanup Code

All Cleanup code needs to be put into a FINALLY block to ensure that it is processed even if an error occurred.

Note, that each nested undoable block may have it’s own FINALLY block.

```
FINALLY:
	IF VALID-OBJECT hQuery THEN
		DELETE OBJECT hQuery .
END FINALLY.

FINALLY:
	SESSION:SET-WAIT-STATE (“”) .
END FINALLY.
```
 