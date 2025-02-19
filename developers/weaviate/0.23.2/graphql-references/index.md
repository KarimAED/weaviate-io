---
layout: layout-documentation
solution: weaviate
sub-menu: GraphQL references
title: GraphQL references
intro: GraphQL references overview
description: GraphQL references overview
tags: ['GraphQL references']
menu-order: 0
open-graph-type: article
og-img: documentation.jpg
toc: true
redirect_from:
    - /documentation/weaviate/current/graphql-references/index.html
    - /documentation/weaviate/current/graphql-references/
---

# All references

All references have their individual subpages, click on one of the references below for more information.

- [Get{}](get.html)
- [Aggregate{}](aggregate.html)
- [Explore{}](explore.html)
- [filters](filters.html)
- [underscore properties](underscore-properties.html)

# GraphQL 

Weaviate's basic query language is [GraphQL](https://graphql.org/). GraphQL is a query language built on using graph data structures. It is an efficient method of data retrieval and mutation, since it mitigates the common over-fetching and under-fetching problems of other query languages. You can query a Weaviate after you've created a [schema](../how-tos/how-to-create-a-schema.html) and [populated it](../how-tos/how-to-import-data.html) with data.

## Query structure

You can query Weaviate for semantic kinds based on standard GraphQL queries. The examples below only contain the GraphQL query. You can POST a GraphQL query to Weaviate as follows:

```bash
$ curl http://localhost/v1/graphql -X POST -H 'Content-type: application/json' -d '{GraphQL query}'
```

A GraphQL JSON object is defined as:

```json
{
    "query": "{ # GRAPHQL QUERY }"
}
```

GraphQL queries follows a defined structure, defined to interact with your data in Weaviate as good as possible. Queries are structured as follows:


```graphql
{
  <Function> {
    <SemanticKind> {
      <Class> {
        <property>
        _<underscore-property>
      }
    }
  }
}
```

- There are three **functions** currently defined in Weaviate's GraphQL: `Get{}`, `Aggregate{}` and `Explore{}`. [`Get{}`](get.html) functions are used to easily retrieve data from your Weaviate instance, while [`Aggregate{}`](aggregate.html) is used to obtain meta information about data objects and its properties. With [`Explore{}`](explore.html) you can browse through the data to with semantic search, and a slightly different query structure than above is used (there is no `<SemanticKind>` and `<className>` defined, since you are searching in a fuzzy way):

```graphql
{
  Explore (<search arguments>) {
      beacon
      certainty
      className
  }
}
```

- [**SemanticKind**](../more-resources/glossary.html) in a GraphQL query should always be `Things` or `Actions`, it is the semantic kind you want to retrieve from Weaviate.
- [**Class**](../more-resources/glossary.html) is the name of the class you want to fetch, defined in the [schema](../restful-api-references/schema.html).
- With including a [**property**](../more-resources/glossary.html) (lowercase) list in the query, you specify exactly which property values you want to return. If the property is a reference to another object (beacon), then use the following structure:

```graphql
{
  <Function> {
    <SematicKind> {
      <Class> {
        <property>
        _<underscore-property>
        <PropertyWithReference>
          ... on <ClassOfBeacon> {
            <property>
            _<underscore-property>
          }
      }
    }
  }
}
```

- To obtain meta information about a data object (for example for interpretation or visualization purposes), use the [**_underscore-property**](underscore-properties.html). 


## More Resources

{% include docs-support-links.html %}