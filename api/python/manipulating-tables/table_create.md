---
layout: api-command
language: Python
permalink: api/python/table_create/
command: table_create
related_commands:
    table_drop: table_drop/
    table_list: table_list/
---

# Command syntax #

{% apibody %}
db.table_create(table_name[, options]) &rarr; object
{% endapibody %}

# Description #

<img src="/assets/images/docs/api_illustrations/table_create_python.png" class="api_command_illustration" />

Create a table. A RethinkDB table is a collection of JSON documents.

If successful, the operation returns an object: `{created: 1}`. If a table with the same
name already exists, the operation throws `RqlRuntimeError`.

Note: that you can only use alphanumeric characters and underscores for the table name.

When creating a table you can specify the following options:

- `primary_key`: the name of the primary key. The default primary key is id;
- `durability`: if set to `'soft'`, this enables _soft durability_ on this table:
writes will be acknowledged by the server immediately and flushed to disk in the
background. Default is `'hard'` (acknowledgement of writes happens after data has been
written to disk);
- `datacenter`: the name of the datacenter this table should be assigned to.

The [data type](/docs/data-types/) of a primary key is usually a string (like a UUID) or a number, but it can also be a time, binary object, boolean or an array. It cannot be an object.

__Example:__ Create a table named 'dc_universe' with the default settings.

```py
r.db('test').table_create('dc_universe').run(conn)
```


__Example:__ Create a table named 'dc_universe' using the field 'name' as primary key.

```py
r.db('test').table_create('dc_universe', primary_key='name').run(conn)
```


__Example:__ Create a table to log the very fast actions of the heroes.

```py
r.db('test').table_create('hero_actions', durability='soft').run(conn)
```

