# Asset Types

*Assets are a built-in Skylark Object Type that have a `type` field which replaces the `AssetType` object. You can modify the `AssetType` enum using the [editEnumConfiguration](https://docs.skylarkplatform.com/docs/edit-enums) mutation*

Asset Types in Skylark are different to how they were in Skylark Legacy.

In Skylark, instead of having an `AssetType` object, we use an [enum](https://docs.skylarkplatform.com/docs/edit-enums) which is essentially a list of options for an Asset's `type` field.

Contents:

- [List Asset Types](#list-asset-types)
- [List Assets by Asset Type](#list-assets-by-asset-type)

## List Asset Types

### Legacy

`/api/asset-types/`

### GraphQL

As hinted at before, there isn't a query to get the Asset Types in Skylark.

Instead, you can use [Introspection](https://graphql.org/learn/introspection/) to read the values:

```graphql
query GET_ASSET_TYPES {
  __type(name: "AssetType") {
    enumValues {
      name
    }
  }
}
```

which returns:

```json
{
  "data": {
    "__type": {
      "enumValues": [
        {
          "name": "EPISODE"
        },
        {
          "name": "APP"
        },
        {
          "name": "AUDIOBOOK"
        }
      ]
    }
  }
}
```

---

## List Assets by Asset Type

In case you want to retrieve Assets using the Asset Type, you can use the `search` query:

```graphql
query MyQuery {
  search(query: "", types: ["EPISODE"]) {
    objects {
      ... on SkylarkAsset {
        uid
        title
      }
    }
  }
}
```
