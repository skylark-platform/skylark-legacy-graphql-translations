# Assets

Contents:

- [Get Asset](#get-asset)
- [List Assets](#list-assets)
- [Create Asset](#create-asset)
- [Update Asset](#update-asset)
- [Delete Asset](#delete-asset)

Related:

- [Asset Types](./AssetTypes.md)

---

## Get Asset

### Legacy

`/api/assets/${uid}?fields=`

### GraphQL

```graphql
query MyQuery {
  getSkylarkAsset(uid: "01H53N4EXWDDKWMW39YZJ44CET", language: "en") {
  # getSkylarkAsset(external_id: "asse_4e4a9d0e3c054790886684b924e1d13c", language: "en") {
    external_id
    internal_title
    title
    slug
    duration
    tags {
      objects {
        uid
      }
    }
    episodes {
      objects {
        uid
      }
    }
  }
}
```

#### Response

```json
{
  "data": {
    "getSkylarkAsset": {
      "external_id": "asse_4e4a9d0e3c054790886684b924e1d13c",
      "internal_title": "The Joy of Winning",
      "title": "The Joy of Winning",
      "slug": "the-joy-of-winning",
      "duration": 3189,
      "tags": {
        "objects": []
      },
      "episodes": {
        "objects": [
          {
            "uid": "01H53N53P6SR7EK5FWVRC7Z1P1"
          }
        ]
      }
    }
  }
}
```

---

## List Assets

### Legacy

`/api/assets/?fields=`


#### Output

```json
{
   "tags":[
      {
         "schedule_urls":[
            "/api/schedules/sche_aeba759af1f44c9ca75564c363c870b6/"
         ],
         "tag_url":"/api/tags/tag__7e83c349050b4369b960479039609dbe/"
      }
   ],
   "schedule_urls":[
      "/api/schedules/sche_fc5be8ad9bdd4bb889c35cdf51d369e9/"
   ],
   "slug":"current-both-d",
   "title":"current Season BOTH D",
   "parent_url":"/api/brands/bran_5cd1826f045449c5afc25798a247b7bd/",
   "language":"en",
   "alternate_synopsis":"",
   "name":""
}
```

### GraphQL

```graphql
query MyQuery {
  listSkylarkAsset(language: "en", next_token: "", limit: 1) {
    next_token
    objects {
      external_id
      internal_title
      title
      slug
      duration
      tags {
        objects {
          uid
        }
      }
      episodes {
        objects {
          uid
        }
      }
    }
  }
}
```

#### Output

```json
{
  "data": {
    "listSkylarkAsset": {
      "next_token": "eyJfbGlzdF9rZXkiOiAicGJibDRlam9semh3emU3NHphZTJheHJ0am0jU2t5bGFya0Fzc2V0fGxhbmcjZW4iLCAiX2lkIjogInBiYmw0ZWpvbHpod3plNzR6YWUyYXhydGptIzAxSDUzTVRRNjhENDg1MU5ENDBZR1BYNzVQIiwgIl9zayI6ICJwYmJsNGVqb2x6aHd6ZTc0emFlMmF4cnRqbSMwMUg1M01UUTY4RDQ4NTFORDQwWUdQWDc1UCNlbiJ9",
      "objects": [
        {
          "external_id": "asse_5cab5445a0804af18630bbcacea18466",
          "internal_title": "Aguska Mnich",
          "title": "Aguska Mnich",
          "slug": "aguska-mnich",
          "duration": 684,
          "tags": {
            "objects": []
          },
          "episodes": {
            "objects": [
              {
                "uid": "01H53N4PMPJKVM1PBJXC6G8JVC"
              }
            ]
          }
        }
      ]
    }
  }
}
```


---

## Create Asset

### Legacy Output

```json
{
   "tags":[
      {
         "schedule_urls":[
            "/api/schedules/sche_aeba759af1f44c9ca75564c363c870b6/"
         ],
         "tag_url":"/api/tags/tag__7e83c349050b4369b960479039609dbe/"
      }
   ],
   "schedule_urls":[
      "/api/schedules/sche_fc5be8ad9bdd4bb889c35cdf51d369e9/"
   ],
   "title":"",
   "parent_url":"",
   "language":"en",
   "alternate_synopsis":"",
   "name":"",
   "asset_type_url":"",
   "entitlement":"/distribution/*"
}
```

### GraphQL

```graphql
mutation MyMutation {
  createSkylarkAsset(
    language: "en"
    skylark_asset: {
      external_id: "asse_ext_id",
      slug: "current-both-d",
      internal_title: "",
      availability: {
        link: "{AVAILABILITY_UID}"
      },
      relationships: {
        brands: {
          link: "{SINGLE_BRAND_UID}"
        },
        tags: {
          link: ["YOU", "CAN", "ALSO", "SEND", "ARRAYS"]
        }
      }
    }
  ) {
    uid
    slug
    tags {
      objects {
        uid
      }
    }
  }
}
```

#### Response

```json
{
  "data": {
    "createSkylarkAsset": {
      "uid": "01H54RN5MWZYFG4SSKXPJ55X3S",
      "slug": "current-both-d",
      "tags": {
        "objects": []
      }
    }
  }
}
```

---

## Update Asset

### GraphQL

```graphql
mutation MyMutation {
  updateSkylarkAsset(
    uid: "01H54RN5MWZYFG4SSKXPJ55X3S"
    language: "en"
    skylark_asset: {
      external_id: "asse_ext_id",
      slug: "current-both-d",
      internal_title: "",
      availability: {
        link: "{AVAILABILITY_UID}"
      },
      relationships: {
        brands: {
          link: "{SINGLE_BRAND_UID}"
        },
        tags: {
          link: ["YOU", "CAN", "ALSO", "SEND", "ARRAYS"]
        }
      }
    }
  ) {
    uid
    slug
    tags {
      objects {
        uid
      }
    }
  }
}
```

or using External ID:

```graphql
mutation MyMutation {
  updateSkylarkAsset(
    external_id: "asse_ext_id"
    language: "en"
    ..rest
  )
}
```

#### Response

```json
{
  "data": {
    "updateSkylarkAsset": {
      "uid": "01H54RN5MWZYFG4SSKXPJ55X3S",
      "slug": "current-both-d",
      "tags": {
        "objects": []
      }
    }
  }
}
```

---

## Delete Asset

### GraphQL

#### Using UID

```graphql
mutation MyMutation {
  deleteSkylarkAsset(uid: "01H502WM10WXSCH68J5ZEW7N7Q") {
    uid # GraphQL requires a return field
  }
}
```

#### Using External ID

```graphql
mutation MyMutation {
  deleteSkylarkAsset(external_id: "asse_5cd1826f045449c5afc25798a247b7bd") {
    uid # GraphQL requires a return field
  }
}
```
