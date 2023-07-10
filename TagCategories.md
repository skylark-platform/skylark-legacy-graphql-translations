# Tag Categories


Contents:

- [Get Tag Category](#get-tag-category)
  - [By Name](#get-tag-category-by-name)
- [List Tag Categories](#list-tag-categories)

---

## Get Tag Category

### Legacy

`/api/tag-categories/{id}`

### GraphQL

```graphql
query MyQuery {
  getTagCategory(uid: "01H502W745ZEPK1X3GMS6G3DMM") {
    uid
    name
  }
}
```

```graphql
query MyQuery {
  getTagCategory(external_id: "cate_c597361120044e13b16eef623d4f0a4c") {
    uid
    name
  }
}
```

### Get Tag Category by name

#### Legacy

`/api/tag-categories/?name={name}`


#### GraphQL

Currently Skylark does not support look up by field value, only `uid` and `external_id`.

You can achieve this functionality using the `search` query:

```graphql
# You can replace the $name variable with a hardcoded string
query MyQuery($name: String!) {
  search(query: $name, limit_search_fields: "name") {
    objects {
      ... on TagCategory {
        name
        uid
        slug
      }
    }
  }
}
```

*Note: `name` must be configured as a [searchable field](https://docs.skylarkplatform.com/docs/editing-searchable-attributes)*

More information on Search and the `limit_search_fields` argument: https://docs.skylarkplatform.com/docs/editing-searchable-attributes

If this doesn't work for you, contact our customer success team.

---

## List Tag Categories

### Legacy

`/api/tag-categories/`

### GraphQL

```graphql
query MyQuery {
  listTagCategory(language: "en", next_token: "", limit: 10) {
    next_token
    objects {
      slug
      name
      uid
    }
  }
}
```
