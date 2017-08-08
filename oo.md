# OO Object Oriented

## USING

By default we will be USING full packages (namespaces) like this:

```
USING {Package}.{Subpackage}.*
USING Consultingwerk.SmartComponents.Implementation.*
```

If only one subclass is needed or there are conflicts with other classes we will specify individual class references in the USING statement:

```
USING {Package}.{Subpackage}.Classname
USING Consultingwerk.Dynamics.SpecialClass
```

However, it should be attempted to avoid naming conflicts between class names at all by using clear and individual class names!

To improve compile time performance, add a USING statement with the FROM ASSEMBLY or FROM PROPATH option for every Class or Namespace reference used in the code.

This will have big impact on compile time performance when the source code (or parts of it) are located on a network share.

So a USING statement looks like in example

```
USING Consultingwerk.SmartComponents.Base.* FROM PROPATH.
USING Progress.Lang.*                       FROM ASSEMBLY.
```

For better readability USING statements should be formatted in tabular order and sorted by alphabet (unless this would have an impact on the class name resolution in case of naming conflict, which should be documented using a comment anyway).

## Class Variables

Variables should be defined without the package name to enhance readability of source code.

```
DEFINE VARIABLE ... AS {unqualified class of ...} 
```

## Class Names

Class names should use the name of the most relevant base class as a suffix in their name to increase descriptiveness:

Samples:

Customer**BusinessEntity**
Customer**DataAccess**
Customer**DatasetModel**
Customer**TableModel**
Customer**Form**		(from SmartWindow**Form** which is a Form)
Weekday**Enum**

Classes that are used as parameter objects only to specific method of another class should be named as ...Parameter, samples:

ShipOrder**Parameter**
YearEndReport**Parameter**

When these parameter objects actually inherit from Consultingwerk.JsonSerializable, it is considered better practice to qualify those class names as “Parameter” objects than as “Serializable” (as serializable objects are typically used as parameters for AppServer calls).

## Interface Names
Interface type names will be prefixed with a capital I.

## Method Names 

Method and Class names begin with a capitalized letter.
Variable names begin with a lower case letter.

## CLASS Statement

At the beginning of a CLASS or INTERFACE block, the IMPLEMENTS and INHERITS options should be broken into the next line in the source code.

```
CLASS Demo.Customer.CustomerBusinessEntity 
    INHERITS BusinessEntity
    USE-WIDGET-POOL: 
```

### Usabe of THIS-OBJECT references

When accessing an object instance's own members (methods, properties, events), we should always use THIS-OBJECT as this makes the scope clearer:

```
THIS-OBJECT:RetrieveData () .
```

When accessing static members (methods, properites, events) of the same class, we'll always be referenceing the member with the (short) class name:

```
BufferHelper:UniqueIndexFields () .
```

Exception from those rules are class wide (static or instance scoped) variables (variables defined outside any method). Those may be referenced by the short variable name only. 
