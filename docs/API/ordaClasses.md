---
id: ordaClasses
title: ORDA User Classes
---

ORDA allows you to create a high-level class functions above the data model, so that you can write business-oriented code and "publish" it just like an API. Datastores, dataclasses, entity selections, and entities are all available as class objects that can contain functions. 

For example, you could create a `getAge()` function in the `EmployeeEntity` class that would be as simple to call as:

```4d
$age:=ds.Employee(1).getAge()
```

Thanks to this feature, the whole business logic of your 4D application can be stored as a independent layed, so that it can be easily maintained, or reused. 

![](assets/en/API/api.png)


## ORDA Classes Overview

All ORDA classes are exposed as properties of the **`cs`** object, which is the class store of the 4D database.

The following ORDA class objects are available:

|ORDA object|Class|Instanciated by|
|---|---|---|
|datastore|cs.dbNameDataStore|`ds` command|
|remoteDatastore|cs.localIdDataStore|`Open datastore` command|
|dataClassX|cs.DataClassX|dataStore.DataClassX, dataStore[DataClassX]|
|entity from dataClassX|cs.DataClassXEntity|dataClass.get(), dataClass.new(), entitySelection.first(), entitySelection.last(), entity.previous(), entity.next(), entity.first(), entity.last(), entity.clone()|
|entitySelection from dataClassX|cs.DataClassXSelection|dataClass.query(),entitySelection.query(), dataClass.all(), dataClass.fromCollection(), dataClass.newSelection(), entitySelection.drop(), entity.getSelection(), entitySelection.and(), entitySelection.minus(), entitySelection.or(), entitySelection.orderBy(), entitySelection.orderByFormula(), entitySelection.slice(), Create entity selection|


## DataStore Class


### Local datastore

A 4D database exposes its own DataStore class in the `cs` class store. Exposed name is *dbName*DataStore (where *dbName* is the .4DProject file name). 

Example:

Database file name|DataStore class name|
|---|---|
|Employee.4DProject|cs.EmployeeDataStore|
 
You can create functions in the *dbName*DataStore class, that will be available through the `ds` object. 

Example:

```4d  
// cs.EmployeeDataStore class

Class extends _DataStore

Function getDesc
  $0:="Database exposing employees and their companies"
```

This function can then be called:

```4d
$desc:=ds.getDesc() //"Database exposing..."
```


### Remote datastore

A session opened on a remote datastore is referenced through a `localId`. The `localId` is referenced in the `cs` class store. Exposed name is *localId*dDataStore (where *localId* is the ID of the remote datastore, as defined by the `Open datastore` command). 

Example:

LocalID|DataStore class name|
|---|---|
|remoteDB|cs.remoteDBDataStore|
 
The *localId*DataStore class can be referenced in the code editor, but you cannot add functions to it. 

> *localId*DataStore classes are not available through the Class tab of the 4D Explorer. 



## DataClass

Each table of the database already exposed with ORDA offers a DataClass class in the `cs` class store.

Exposed class name is DataClass*X* (where *X* is the table name). 

Example:

Database table name|DataStore class name|
|---|---|
|Employee|cs.DataClassEmployee|

Example:

```4D
// cs.Company class


Class extends DataClass

// Returns companies which revenue is over the average
// Returns an entity selection related to the DataClass Company 
Function GetBestOnes()
$sel:=This.query("revenues >= :1";This.all().average("revenues"));
$0:=$sel
```


Then on a form, you can display the best companies by getting this entity selection: ds.Company.GetBestOnes()

