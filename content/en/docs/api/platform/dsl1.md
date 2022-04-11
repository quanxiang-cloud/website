---
title: "query multiple parameters description"
description: "QuanXiang Cloud Low-Code Platform API Parameters Description"
keywords: "query multiple"
linkTitle: "query multiple parameters description"
weight: 7215
---

## Query Example

This subsection takes CURL as an example to illustrate the query parameters. The platform API supports multiple language calls, such as: CURL, JavaScript, Python.

![dsl1](/images/api/platform/dsl1.png)

## Query criteria

The QuanXiang Cloud Low-Code Platform API follows the [elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html?baymax=rec&rogue=rec-1&elektra=guide) query syntax.

### Single Field Query

If you need to inquire about a single field, you can use the keywords `match`, `term`, etc. for the query, with the following semantics:

#### match

The match condition is that the `desc` field contains the word "software".

```json
{
  "query" : { "match" : { "desc" : "software" }}
}
```



#### term

The match condition is that the `desc` field is equal to the word "software".

```json
{
  "query" : { "term" : { "desc" : "software" }}
}
```



#### terms

The match condition is that the inside of the `age` field is equal to any value in the array.

```json
{
  "query" : { "terms" : { "age" : [1,4,5,6,7,12] }}
}
```



#### range

`range` is used for range finding, the detailed parameters are described below.

- gte: more than or equal to.
- gt: larger.
- lt: less than or equal to.
- lte: less.

```json
{
  "query" : { "range": {
      "age": {
         "gte": 12,
         "gt": 11,
         "lt": 11,
         "lte": 12
      }
    }}
}
```





### Multi-field query

If you need to search for multiple keywords, for example, the query `name` equals Jack and `age` equals 1 or 2. First represent them with single-field queries `term` and `terms`, and then combine them with `bool` queries.

```json
{
  "query": {
    "bool": {
      "must": [
        { "term": { "name":  "Jack" }},
        { "terms": { "age":  [1,2]}} 
      ]
    }
  }
}
```

{{< alert tip >}}

**Instruction**

The query field relationships support joins using must, should, and must_not.

- must: means that all conditions must match.
- should: only one condition needs to be met.
- must_not: all conditions must not match.

{{</ alert >}}

## Sort

Sorting uses the `sort` field, which is received using an array. The sorting rules are: sort by `created_at` first, or `age` if `created_at` cannot be sorted.

{{< alert tip >}}

**Instruction**

The "-" sign indicates descending order, no need to use "+" for increasing order. For example:

- -created_at: means sorting by created_at in descending order.
- age: means sort by age in increasing order.

{{</ alert >}}

```json
{
    "sort":["-created_at" ,"age"]
}
```



## Paging

Supports paging using page and size.

page: starting from 1, the first page is represented by 1, and so on.

size: per page size.

```json
  {
    "page": 19,
    "size": 8
  }
```

