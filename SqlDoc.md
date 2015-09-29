# DApps SQL API

Crypti DApps store blockchain data within a self-contained in-process [SQLite](https://sqlite.org/) database engine. Wherein all sidechain data is organized into relational tables. With each table being comprised of one to many table field/columns used to record the varying types of data of your DApp. So in essence, Crypti DApps behave like any other database where you can select/insert and remove information at will.

## Schemas

Before we can store any data on our sidechain. We need to initialize some tables. To initialize a table. We first need to describe the tables in our database schema.

Open the **blockchain.json** file in the root folder of your DApp, where you will find an array of objects.

The below example represents the schema of a **blocks** table:

```json
{
	"table": "blocks",
	"alias": "b",
	"type": "table",
	"tableFields": []
}
```

Let's quickly describe each property:

  * **table** - The table name.
  * **alias** - A shortened table name alias (example: **b**, the first letter(s) of your table name).
  * **type** - The object type. Can be "table" or "index". In our case "table".
  * **tableFields** - An array of table fields.

## Table Fields

Each field in the **tableFields** array is defined as follows:

```json
{
	"name": "id",
	"type": "String",
	"length": 21
},
{
	"name": "timestamp",
	"type": "BigInt"
},
{
	"name": "height",
	"type": "BigInt"
},
	{
	"name": "payloadLength",
	"type": "BigInt"
},
	{
	"name": "payloadHash",
	"type": "String",
	"length": 32
},
{
	"name": "prevBlockId",
	"type": "String",
	"length": 21
},
{
	"name": "pointId",
	"type": "String",
	"length": 21
},
{
	"name": "pointHeight",
	"type": "BigInt"
},
{
	"name": "delegate",
	"type": "String",
	"length": 64
},
{
	"name": "signature",
	"type": "String",
	"length": 128
},
{
	"name": "count",
	"type": "BigInt"
}
```

Each object represents a field in the table's schema, and can be described using the following three properties:

  * name - The field name.
  * type - The field type. Can be "String", "BigInt" or "Binary".
  * length - The field length. Required for "String" or "Binary" field types.

Please note, we don't recommend using "Binary" fields. As it will increase the amount of traffic passed back and forth between Crypti and your DApp. Instead we recommend converting Binary data to hexi-decimal format and saving it as "String". So, if you have a 32 byte binary buffer. Convert it to a hexi-decimal and then save to a "String" field with 64 chars length.

## Queries

Crypti provides a fully fledged SQL API, which allows you interact with the information stored in your DApp's database.

For further information, please read our [SQL API documentation](http://docs.crypti.me/Sql.html).

In summary, the following operations are supported:

  * batch  - Insert a group of records into a table.
  * insert - Insert one record into a table.
  * remove - Remove one or more records from a table.
  * select - Select one or more records from a table.

All of these operations are executed by first assembling them as JSON formatted query objects. Which are then passed to the `modules.api.sql.methodname` API function - replacing the `methodname` with your chosen operation e.g. `select`. Then converted to an actual SQL query and executed by the database.

Below we give a detailed overview of how this can be accomplished:

### Queries#select

Here is an example of how the base **select** query is constructed using the API:

```js
modules.api.sql.select({
	table: "tablename",
	condition: {
		field: value
	},
	sort: {},
	fields: [],
	map: []
})
```

As you can see we pass a query object to `modules.api.sql.select` comprised of the following properties:

* table - The table name to run the query against.
* condition - The query conditions e.g. equal to, greater than, less than.
* sort - The field to sort the query results by.
* fields - The fields to include within a select query result. Returns an array of fields.
* map - When fields returns an array of fields. Allows each field to be mapped to an object.

### Queries#select.condition

*Equal to condition:*

```js
{
	condition: {
		field: value
	}
}
```

*Greater than condition:*

```js
condition: {
	field: {
		$gt: value
	}
}
```

For a greater than or equal to condition use: *$gte*.

*Less then condition:*

```js
condition: {
	field: {
		$lt: value
	}
}
```

For a less than or equal to condition use: *$lte*.

*In condition:*

```js
condition: {
	field: {
		$in: [v1, v2, v3]
	}
}
```

*Not in condition:*

```js
condition: {
	field: {
		$nin: [v1, v2, v3]
	}
}
```

*Like condition:*

```js
condition: {
	field: {
		$like: value
	}
}
```

*Null condition:*

```js
condition: {
	field: $null
}
```

*Between condition:*

```js
condition: {
	field: {
		$between: [minvalue, maxvalue]
	}
}
```

*Equal to:*

```js
condition: {
	field: {
		$eq: value
	}
}
```

*Not equal to:*

```js
condition: {
	field: {
		$neq: value
	}
}
```

*OR:*

```js
condition: {
	field: {
		$or: [{
			field1: value1,
			field2: value2
		}]
	}
}
```

### Queries#select.sort

```js
sort: {
	field1: -1,
	field2: 1
}
```

Which translates to the following SQL fragment:

```sql
order by field1 asc, field2 desc
```

### Expression

```js
fields: [{
	expression: 'count(*)'
}]
```

## Further Documentation

This tutorial only gives a brief overview of what can be accomplished using the SQL API. So for more detailed information, please read our [json-sql](https://github.com/crypti/json-sql/tree/master/docs) documentation.