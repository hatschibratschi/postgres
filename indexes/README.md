# Operator Classes of Indexes

## text_pattern_ops, varchar_pattern_ops, and bpchar_pattern_ops

B-tree indexes on the types text, varchar, and char

`CREATE INDEX ON tls224_appln_cpc (cpc_class_symbol varchar_pattern_ops);`

show all defined operator classes:

```
SELECT am.amname AS index_method,
       opc.opcname AS opclass_name,
       opc.opcintype::regtype AS indexed_type,
       opc.opcdefault AS is_default
FROM pg_am am, pg_opclass opc
WHERE opc.opcmethod = am.oid
ORDER BY index_method, opclass_name;
```

## Operators

`LIKE, ILIKE` or `NOT LIKE, NOT ILIKE`

https://www.postgresql.org/docs/9.4/indexes-opclass.html

# GIN indexes

Generalized Inverted iNdex,

`CREATE EXTENSION pg_trgm;`

## pg_trgm trigram matching functions

`CREATE INDEX trgm_idx ON test.test_table USING gin (col gin_trgm_ops);`

- https://www.postgresql.org/docs/current/pgtrgm.html#id-1.11.7.42.6

`SELECT word_similarity('word', 'two words');`

## tsvector

`CREATE INDEX idx_test_col ON test.test_table USING GIN (to_tsvector('simple', col));`

`SELECT * FROM test.test_table WHERE to_tsvector('simple', col) @@ to_tsquery('simple', 'nano');`

`SELECT to_tsvector('english','car cars');`
`SELECT to_tsvector('english','cloud compute computing computer');`
`SELECT to_tsvector('german','Das Auto, die Autos');`

`SELECT to_tsvector('english','cloud computing') @@ to_tsquery('english', 'computer');` returns TRUE

Boolean operators
- & (AND)
- | (OR) 
- ! (NOT)

### position

`INSERT INTO test.test_table2 VALUES(1,'2010-06-29', '2010-06-29', 'nano test abcd nano');`

get `nano` at position 4 (also when it is on position 1)
`SELECT * FROM test.test_table2 CROSS JOIN unnest(to_tsvector('simple', col)) WHERE lexeme = 'nano' and positions @> '{4}';`

## links

GIN
- https://www.postgresql.org/docs/current/pgtrgm.html
- https://www.postgresql.org/docs/current/gin.html
- https://pganalyze.com/blog/gin-index


(cluster*, cloud*, grid?) [within 3 words of] (based; comput*; server?; process*; software; application) 
