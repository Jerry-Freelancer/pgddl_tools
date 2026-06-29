# pgddl_tools

`pgddl_tools` is a PostgreSQL extension that adds SQL helpers for inspecting
and reconstructing DDL for common database objects.

## Features

- `pgddl_tools.get_relation_ddl(relation regclass, include_indexes boolean)`
  returns DDL for tables, partitioned tables, foreign tables, views, and
  materialized views.
- `pgddl_tools.get_schema_ddl(schema_name name, include_indexes boolean)`
  returns DDL for all supported relations in a schema.
- Helper functions expose quoted names, relation kinds, column definitions,
  table constraints, and non-constraint indexes.

The generated DDL is intended for inspection, review, and documentation. It is
not a byte-for-byte replacement for `pg_dump`.

## Build and install

```sh
make
sudo make install
```

Then enable it in a database:

```sql
CREATE EXTENSION pgddl_tools;
```

## Examples

```sql
SELECT pgddl_tools.get_relation_ddl('public.accounts'::regclass);
SELECT pgddl_tools.get_relation_ddl('public.accounts'::regclass, false);
SELECT pgddl_tools.get_schema_ddl('public');
```
