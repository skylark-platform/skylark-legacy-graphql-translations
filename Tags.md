# Tags

*Tags are a built-in Skylark Object Type*

Contents:

- [List Tags](#list-tags)

---

## List Tags

### Legacy

`/api/tags/`

### GraphQL

```graphql
query MyQuery {
  listSkylarkTag(language: "en", next_token: "", limit: 10) {
    next_token
    objects {
      slug
      name
      tag_categories {
        objects {
          name
          slug
        }
      }
    }
  }
}
```
