# PostgreSQL Dump & Restore

## Dump Database

```bash
pg_dump -U postgres {database name} | gzip > {database name}.sql.gz
```

## Restore Database

Requires user to create an empty database prior to restore.

```bash
gunzip -c {database name}.sql.gz | psql -U postgres --set ON_ERROR_STOP=on {database name}
```


