---
title: "CREATE TABLE Statement (Microsoft Access SQL)"
  
  
manager: soliver
ms.date: 3/9/2015
ms.audience: Developer
 
f1_keywords:
- jetsql40.chm5277563
  
localization_priority: Normal
ms.assetid: fc45d36e-6e43-c030-5016-cca8bb1379fe
description: "Creates a new table."
---

# CREATE TABLE Statement (Microsoft Access SQL)

Creates a new table.
  
> [!NOTE]
> The Microsoft Access database engine does not support the use of CREATE TABLE, or any of the DDL statements, with non-Microsoft Access database engine databases. Use the DAO Create methods instead. 
  
## Syntax

CREATE [TEMPORARY] TABLE  *table*  (  *field1 type*  [(  *size*  )] [NOT NULL] [WITH COMPRESSION | WITH COMP] [  *index1*  ] [,  *field2*  *type*  [(  *size*  )] [NOT NULL] [  *index2*  ] [, …]] [, CONSTRAINT  *multifieldindex*  [, …]]) 
  
The CREATE TABLE statement has these parts:
  
|**Part**|**Description**|
|:-----|:-----|
| *table*  <br/> |The name of the table to be created.  <br/> |
| *field1*  ,  *field2*  <br/> |The name of field or fields to be created in the new table. You must create at least one field.  <br/> |
| *type*  <br/> |The data type of  *field*  in the new table.  <br/> |
| *size*  <br/> |The field size in characters (Text and Binary fields only).  <br/> |
| *index1*  ,  *index2*  <br/> |A CONSTRAINT clause defining a single-field index. For more information on how to create this index, see [CONSTRAINT Clause](constraint-clause-microsoft-access-sql.md).  <br/> |
| *multifieldindex*  <br/> |A CONSTRAINT clause defining a multiple-field index. For more information on how to create this index, see [CONSTRAINT Clause](constraint-clause-microsoft-access-sql.md).  <br/> |
   
## Remarks

Use the CREATE TABLE statement to define a new table and its fields and field constraints. If NOT NULL is specified for a field, then new records are required to have valid data in that field.
  
A CONSTRAINT clause establishes various restrictions on a field, and can be used to establish the primary key. You can also use the [CREATE INDEX](create-index-statement-microsoft-access-sql.md) statement to create a primary key or additional indexes on existing tables. 
  
You can use NOT NULL on a single field or within a named CONSTRAINT clause that applies to either a single field or to a multiple-field named CONSTRAINT. However, you can apply the NOT NULL restriction only once to a field. Attempting to apply this restriction more than once results in a run-time error.
  
When a TEMPORARY table is created it is visible only within the session in which it was created. It is automatically deleted when the session is terminated. Temporary tables can be accessed by more than one user.
  
The WITH COMPRESSION attribute can be used only with the CHARACTER and MEMO (also known as TEXT) data types and their synonyms.
  
The WITH COMPRESSION attribute was added for CHARACTER columns because of the change to the Unicode character representation format. Unicode characters uniformly require two bytes for each character. For existing Microsoft® Jet databases that contain predominately character data, this could mean that the database file would nearly double in size when converted to the Microsoft Access database engine format. However, Unicode representation of many character sets, those formerly denoted as Single-Byte Character Sets (SBCS) can easily be compressed to a single byte. If you define a CHARACTER column with this attribute, data will automatically be compressed as it is stored and uncompressed when retrieved from the column.
  
MEMO columns can also be defined to store data in a compressed format. However, there is a limitation. Only instances of MEMO columns that, when compressed, will fit within 4096 bytes or less, will be compressed. All other instances of MEMO columns will remain uncompressed. This means that within a given table, for a given MEMO column, some data may be compressed and some data may not be compressed.
  
## Example

This example creates a new table called ThisTable with two text fields.
  
```
Sub CreateTableX1() 
 
    Dim dbs As Database 
 
    ' Modify this line to include the path to Northwind 
    ' on your computer. 
    Set dbs = OpenDatabase("Northwind.mdb") 
 
    ' Create a table with two text fields. 
    dbs.Execute "CREATE TABLE ThisTable " _ 
        &amp; "(FirstName CHAR, LastName CHAR);" 
 
    dbs.Close 
 
End Sub 

```

This example creates a new table called MyTable with two text fields, a Date/Time field, and a unique index made up of all three fields.
  
```
Sub CreateTableX2() 
 
    Dim dbs As Database 
 
    ' Modify this line to include the path to Northwind 
    ' on your computer. 
 
    Set dbs = OpenDatabase("Northwind.mdb") 
 
    ' Create a table with three fields and a unique 
    ' index made up of all three fields. 
    dbs.Execute "CREATE TABLE MyTable " _ 
        &amp; "(FirstName CHAR, LastName CHAR, " _ 
        &amp; "DateOfBirth DATETIME, " _ 
        &amp; "CONSTRAINT MyTableConstraint UNIQUE " _ 
        &amp; "(FirstName, LastName, DateOfBirth));" 
 
    dbs.Close 
 
End Sub
```

This example creates a new table with two text fields and an **Integer** field. The SSN field is the primary key. 
  
```
Sub CreateTableX3() 
 
     Dim dbs As Database 
 
    ' Modify this line to include the path to Northwind 
    ' on your computer. 
    Set dbs = OpenDatabase("Northwind.mdb") 
 
    ' Create a table with three fields and a primary 
    ' key. 
    dbs.Execute "CREATE TABLE NewTable " _ 
        &amp; "(FirstName CHAR, LastName CHAR, " _ 
        &amp; "SSN INTEGER CONSTRAINT MyFieldConstraint " _ 
        &amp; "PRIMARY KEY);" 
 
    dbs.Close 
 
End Sub 

```

