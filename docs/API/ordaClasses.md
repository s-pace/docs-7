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
|datastore|cs.*dbName*DataStore|`ds` command|
|remoteDatastore|cs.*localId*DataStore|`Open datastore` command|
|dataClassX|cs.*DataClassX*|dataStore.DataClassX, dataStore[DataClassX]|
|entity from dataClassX|cs.*DataClassX*Entity|dataClass.get(), dataClass.new(), entitySelection.first(), entitySelection.last(), entity.previous(), entity.next(), entity.first(), entity.last(), entity.clone()|
|entitySelection from dataClassX|cs.*DataClassX*Selection|dataClass.query(),entitySelection.query(), dataClass.all(), dataClass.fromCollection(), dataClass.newSelection(), entitySelection.drop(), entity.getSelection(), entitySelection.and(), entitySelection.minus(), entitySelection.or(), entitySelection.orderBy(), entitySelection.orderByFormula(), entitySelection.slice(), Create entity selection|

>*dbName* is the .4DProject file name

## DataStore Class


### Local datastore

A 4D database exposes its own DataStore class in the `cs` class store. 

- **Inherit from**: _DataStore 
- **Exposed name**: *dbName*DataStore (where *dbName* is the .4DProject file name)

|Database file name|DataStore class name|
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

A session opened on a remote datastore is referenced through a `localId`. The `localId` is referenced in the `cs` class store. 

- **Exposed name**: *localId*DataStore (where *localId* is the ID of the remote datastore, as defined by the `Open datastore` command). 

LocalID|DataStore class name|
|---|---|
|remoteDB|cs.remoteDBDataStore|
 
The *localId*DataStore class can be referenced in the code editor, but you cannot add functions to it. 

> *localId*DataStore classes are not available through the Class tab of the 4D Explorer. 



## DataClass Class

Each table exposed with ORDA of the database offers a DataClass class in the `cs` class store.

- **Inherit from**: DataClass 
- **Exposed name**: *DataClassX* (where *DataClassX* is the table name). 

|Table name|DataClass class name|
|---|---|
|Employee|cs.Employee|

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

Then, you can get an entity selection of the "best" companies by executing: 

```4d
var $best : cs.Company 
$best:=ds.Company.GetBestOnes()
```

## EntitySelection Class

Each table exposed with ORDA of the database offers an EntitySelection class in the `cs` class store.

- **Inherit from**: EntitySelection 
- **Exposed name**: *DataClassX*Selection (where *DataClassX* is the table name). 

|Table name|EntitySelection class name|
|---|---|
|Employee|cs.EmployeeSelection|


Example:

```4d
// cs.EmployeeSelection class


Class extends EntitySelection

// Returns the average value of an attribute
// in an entity selection

Function getAverage()
    var $attribute,$1 : text
    $attribute:=$1
    $0:=This.average($attribute)

```

Then, you can get any average value of the selection by executing: 

```4d
$avgSalary:=ds.Company.all().employees.getAverage("salary")
$avgSalary:=ds.Company.all().employees.getAverage("age")
```

## Entity Class

Each table exposed with ORDA of the database offers an Entity class in the `cs` class store.

- **Inherit from**: Entity 
- **Exposed name**: *DataClassX*Entity (where *DataClassX* is the table name). 

|Table name|Entity class name|
|---|---|
|Employee|cs.EmployeeEntity|

Example:

```4d
// cs.EmployeeEntity class


Class extends Entity

// Returns the age using the birthdate

Function age()
	$0:=Year of(Current date)-Year of(This.birthdate)

```

Then, you can get the age of an employee: 

```4d
$age:=ds.Employee(1).age()
```
