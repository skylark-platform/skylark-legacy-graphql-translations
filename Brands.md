# Brands

Contents:

- [Get Brand](#get-brand)
- [List Brands](#list-brands)
- [Create Brand](#create-brand)
- [Update Brand](#update-brand)
- [Delete Brand](#delete-brand)

---

## Get Brand

### Legacy

`/api/brands/${uid}?fields=`

### GraphQL

```graphql
query MyQuery {
  getBrand(uid: "01H53QSS3GP6DX9YDH83FARHTC", language: "en") {
  # getBrand(external_id: "bran_4e4a9d0e3c054790886684b924e1d13c", language: "en") {
    external_id
    internal_title
    title
    slug
    synopsis
    tags {
      objects {
        uid
      }
    }
    seasons {
      objects {
        uid
      }
    }
  }
}
```

#### Response

```json
{
  "data": {
    "getBrand": {
      "external_id": "bran_72d13e598da7466ba30ef8e072310ce4",
      "internal_title": "Genius of the Ancient World",
      "title": "Genius of the Ancient World",
      "slug": "GOAW-6326195",
      "synopsis": "Between 550 – 450 BC Buddha, Confucius and Socrates each thrust populations towards a new age of reason – so how did they do it?",
      "tags": {
        "objects": []
      },
      "seasons": {
        "objects": [
          {
            "uid": "01H53PHYYC4ME8XDX0ZFYRBH4Y"
          },
          {
            "uid": "01H53PHYWNWHZWR5QC6F33T764"
          }
        ]
      }
    }
  }
}
```

---

## List Brands

### Legacy

`/api/brands/?fields=`


#### Output

```json
{
   "schedule_urls":[
      "/api/schedules/sche_fc5be8ad9bdd4bb889c35cdf51d369e9/"
   ],
   "slug":"current-both-d",
   "title":"current Season BOTH D",
   "language":"en",
   "alternate_synopsis":"",
   "name":""
}
```

### GraphQL

```graphql
query MyQuery {
  listBrand(language: "en", next_token: "", limit: 1) {
    next_token
    objects {
      external_id
      internal_title
      title
      slug
      synopsis
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
    "listBrand": {
      "next_token": "eyJfbGlzdF9rZXkiOiAicGJibDRlam9semh3emU3NHphZTJheHJ0am0jQnJhbmR8bGFuZyNlbiIsICJfaWQiOiAicGJibDRlam9semh3emU3NHphZTJheHJ0am0jMDFINTNRUzlEUTZISlI2VE1YQ0YyUUtOMjMiLCAiX3NrIjogInBiYmw0ZWpvbHpod3plNzR6YWUyYXhydGptIzAxSDUzUVM5RFE2SEpSNlRNWENGMlFLTjIzI2VuIn0=",
      "objects": [
        {
          "external_id": "bran_7067eacc7e87468dac294ab5a85a565b",
          "internal_title": "Can a Computer Write a Hit Musical?",
          "title": "Can a Computer Write a Hit Musical?",
          "slug": "CSSH-7010592",
          "synopsis": "A group of scientists use the computer programme “Android Lloyd Weber” to create a West End musical.",
          "tags": {
            "objects": []
          },
          "episodes": {
            "objects": []
          }
        }
      ]
    }
  }
}
```


---

## Create Brand

### Legacy Output

```json
{
   "title":"current Season BOTH D",
   "language":"en",
   "alternate_synopsis":"",
   "name":""
}
```

### GraphQL

```graphql
mutation MyMutation {
  createBrand(
    language: "en"
    brand: {
      external_id: "bran_ext_id",
      slug: "current-both-d",
      internal_title: "",
      availability: {
        link: "{AVAILABILITY_UID}"
      },
      relationships: {
        seasons: {
          link: "{SINGLE_SEASON_UID}"
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
    "createBrand": {
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

## Update Brand

### GraphQL

```graphql
mutation MyMutation {
  updateBrand(
    uid: "01H54RN5MWZYFG4SSKXPJ55X3S"
    language: "en"
    brand: {
      external_id: "bran_ext_id",
      slug: "current-both-d",
      internal_title: "",
      availability: {
        link: "{AVAILABILITY_UID}"
      },
      relationships: {
        seasons: {
          link: "{SINGLE_SEASON_UID}"
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
  updateBrand(
    external_id: "bran_ext_id"
    language: "en"
    ..rest
  )
}
```

#### Response

```json
{
  "data": {
    "updateBrand": {
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

## Delete Brand

### GraphQL

#### Using UID

```graphql
mutation MyMutation {
  deleteBrand(uid: "01H502WM10WXSCH68J5ZEW7N7Q") {
    uid # GraphQL requires a return field
  }
}
```

#### Using External ID

```graphql
mutation MyMutation {
  deleteBrand(external_id: "bran_5cd1826f045449c5afc25798a247b7bd") {
    uid # GraphQL requires a return field
  }
}
```
