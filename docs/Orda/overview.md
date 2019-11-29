---
id: overview
title: Overview
---

## What is ORDA?  
ORDA stands for **Object Relational Data Access**. It is an enhanced technology using a database as an object – by the language or with user interface widgets.

Relations are transparently included in the concept, in combination with lazy loading, to remove all the typical hassles of data selection or transfer from the developer.

With ORDA, data is accessed through an abstraction layer, the **datastore**. A datastore is an object that provides an interface to the database model and data through objects. For example, a table is mapped to a dataclass object, a field is an attribute of a dataclass, and records are entities. 


## Why use ORDA?  
Instead of representing information as tables, records, and fields, ORDA uses an alternate approach that more accurately maps data to real-world concepts.

Imagine the ability to denormalize a relational structure, yet not affect efficiency. Imagine describing everything about the business objects in your application in such a way that using the data becomes simple and straightforward and removes the need for a complete understanding of the relational structure.

In a datastore, a single dataclass can incorporate all of the elements that make up a traditional relational database table, but can also include values from related parent entities, and direct references to related entities and entity selections.

A query returns a list of entities called an entity selection, which fulfills the role of a SQL query’s row set. The difference is that each entity "knows" where it belongs in the data model and "understands" its relationship to all other entities. This means that a developer does not need to explain in a query how to relate the various pieces of information, nor in an update how to write modified values back to the relational structure.

In addition, ORDA objects such as entity selections or entities can be easily bound to form objects such as list boxes or variables. Combined with powerful features such as the `This` and `Form` commands, they allow the building modern and modular interfaces based upon objects and collections.

## How to use ORDA?  
Basically, ORDA handles objects. In ORDA, all main concepts, including the datastore itself, are available through objects. ORDA objects are created and instanciated when necessary by 4D methods (you do not need to create them).

Note, however, that you will usually need to store them in 4D object variables, like any other object (declared with the `C_OBJECT` command). Objects in ORDA can be handled like 4D standard objects, but they automatically benefit from specific properties and methods.

ORDA available objects are:

- **Datastore**: the datastore is the interface object to the database. It builds a representation of the whole database as object. The main (default) datastore is always available through the `ds` command, but the `Open datastore` command allows referencing any remote datastore. 
- **Dataclass**: a dataclass is the equivalent of a table. It is used as an object model and references all fields as attributes, including relational attributes (attributes built upon relations between dataclasses). Relational attributes can be used in queries like any other attribute.
- **Attribute**: dataclass properties are attribute objects describing the underlying fields or relations.
- **Entity selection**: an entity selection references one or more entities from a dataclass. It is usually created as a result of a query.
- **Entity**: an entity is the equivalent of a record. It is actually an object that references a record in the database.


## ORDA prerequisites
Since ORDA objects rely on the 4D database structure, you need to make sure all tables and fields are ORDA compliant:

- Tables without a primary key or with a composite primary key are not exposed in the datastore.
- BLOB type fields are not managed.
- Table, field, and relation names must be compliant with standard [object naming conventions](Concepts/identifier.md).
- Any modifications applied at the level of the database structure require that you restart the 4D database so that the ORDA model layer is reloaded and updated accordingly. These modifications include:
	- adding or removing a table, a field, or a relation
renaming of a table, a field, or a relation
	- retyping a field

> ORDA does not take into account the "Invisible" option for tables or fields, nor the virtual structure defined through `SET TABLE TITLES` or `SET FIELD TITLES`.

