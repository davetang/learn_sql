# SQL

Use the [Ensembl public MySQL Servers](https://www.ensembl.org/info/data/mysql.html?redirect=no) to demonstrate; see the [database schema](https://www.ensembl.org/info/docs/api/core/core_schema.html).

```console
mysql --user=anonymous --host=ensembldb.ensembl.org -A
use ensembl_compara_113;
```

## Subqueries

Create a subquery that finds rows where the `species_set_id` column is repeated over 20 times.

```sql
SELECT species_set_id, count(*)
FROM species_set
WHERE species_set_id IN (
    SELECT species_set_id
    FROM species_set
    GROUP BY species_set_id
    HAVING COUNT(*) > 20
)
GROUP BY species_set_id;
```
```
+----------------+----------+
| species_set_id | count(*) |
+----------------+----------+
|          83217 |       21 |
|          85063 |       27 |
|          85643 |       24 |
|          86261 |       43 |
|          86262 |       91 |
|          86264 |       63 |
|          86951 |      200 |
|          86963 |       32 |
|          86964 |       65 |
|          89506 |      282 |
|          89507 |       23 |
|          89648 |       31 |
|          89649 |       27 |
+----------------+----------+
13 rows in set (0.267 sec)
```
