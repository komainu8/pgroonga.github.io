---
title: "%% operator"
upper_level: ../
---

# `%%` operator

## Summary

This operator is deprecated since 1.2.0. Use [`&@` operator][match-v2] instead.

`%%` operator performs full text search by one keyword.

## Syntax

```sql
column %% keyword
```

`column` is a column to be searched. It's `text` type, `text[]` type or `varchar` type.

`keyword` is a keyword for full text search. It's `text` type for `text` type or `text[]` type `column`. It's `varchar` type for `varchar` type `column`.

## Operator classes

You need to specify one of the following operator classes to use this operator:

  * `pgroonga_text_full_text_search_ops_v2`: Default for `text`

  * `pgroonga_text_array_full_text_search_ops_v2`: Default for `text[]`

  * `pgroonga_varchar_full_text_search_ops_v2`: For `varchar`

  * `pgroonga_text_full_text_search_ops`: For `text`

  * `pgroonga_text_array_full_text_search_ops`: For `text[]`

  * `pgroonga_varchar_full_text_search_ops`: For `varchar`

## Usage

Here are sample schema and data for examples:

```sql
CREATE TABLE memos (
  id integer,
  content text
);

CREATE INDEX pgroonga_content_index ON memos USING pgroonga (content);
```

```sql
INSERT INTO memos VALUES (1, 'PostgreSQL is a relational database management system.');
INSERT INTO memos VALUES (2, 'Groonga is a fast full text search engine that supports all languages.');
INSERT INTO memos VALUES (3, 'PGroonga is a PostgreSQL extension that uses Groonga as index.');
INSERT INTO memos VALUES (4, 'There is groonga command.');
```

You can perform full text search with one keyword by `%%` operator:

```sql
SELECT * FROM memos WHERE content %% 'engine';
--  id |                                content                                 
-- ----+------------------------------------------------------------------------
--   2 | Groonga is a fast full text search engine that supports all languages.
-- (1 row)
```

If you want to perform full text search with multiple keywords or AND/OR search, use [`&@~` operator][query-v2].

If you want to perform full text search with multiple keywords OR search, use [`&@|` operator][match-in-v2].

## See also

  * [`&@~` operator][query-v2]: Full text search by easy to use query language

  * [`&@|` operator][match-in-v2]: Full text search by an array of keywords

[match-v2]:match-v2.html
[query-v2]:query-v2.html
[match-in-v2]:match-in-v2.html
