# Seasons

Contents:

- [Get Season](#get-season)
- [List Seasons](#list-seasons)
- [Create Season](#create-season)
- [Update Season](#update-season)
- [Delete Season](#delete-season)

---

## Get Season

### Legacy

`/api/season/${uid}?fields=`

### GraphQL

```graphql
query MyQuery {
  getSeason(uid: "01H53QP93EVAFMBVCDTD81KVPY", language: "en") {
  # getSeason(external_id: "seas_955a7cf27167466fa0191793a27f3c25", language: "it") {
    internal_title
    title
    synopsis
    season_number
    number_of_episodes
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
    "getSeason": {
      "internal_title": "The Magic of Houdini",
      "title": "The Magic of Houdini",
      "synopsis": "English comedian Alan Davies presents the extraordinary life and legacy of Hungarian-born illusionist and stunt performer Harry Houdini.",
      "season_number": null,
      "number_of_episodes": null,
      "tags": {
        "objects": []
      }
    }
  }
}
```

---

## List Seasons

### Legacy

`/api/seasons/?fields=`


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
  listSeason(language: "en", next_token: "", limit: 1) {
    next_token
    objects {
      slug
    	internal_title
      title
      synopsis
      brands(limit: 1) {
        objects {
          uid
        }
      }
      tags {
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
    "listSeason": {
      "next_token": "eyJfbGlzdF9rZXkiOiAicGJibDRlam9semh3emU3NHphZTJheHJ0am0jU2Vhc29ufGxhbmcjZW4iLCAiX2lkIjogInBiYmw0ZWpvbHpod3plNzR6YWUyYXhydGptIzAxSDUzUEhBVkIxSFpKUUNORkc5QUFYUEozIiwgIl9zayI6ICJwYmJsNGVqb2x6aHd6ZTc0emFlMmF4cnRqbSMwMUg1M1BIQVZCMUhaSlFDTkZHOUFBWFBKMyNlbiJ9",
      "objects": [
        {
          "slug": "POFO-8682546",
          "internal_title": "Power and Football - Season 1",
          "title": "Power and Football",
          "synopsis": "Power and Football explores how football unites the World like no other sport - kicking down the barriers of language, culture and race.",
          "brands": {
            "objects": [
              {
                "uid": "01H53QSQAGFGSF0R26QTY5T4MC"
              }
            ]
          },
          "tags": {
            "objects": []
          }
        }
      ]
    }
  }
}
```


---

## Create Season

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
mutation MyMutation {
  createSeason(
    language: "en"
    season: {
      external_id: "seas_ext_id",
      slug: "current-both-d",
      synopsis: "",
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
  }
}
```

---

## Update Season

### GraphQL

```graphql
mutation MyMutation {
  updateSeason(
    uid: "01H53QSQAGFGSF0R26QTY5T4MC",
    language: "en"
    season: {
      external_id: "seas_ext_id",
      slug: "current-both-d",
      synopsis: "",
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
  }
}
```

or using External ID:

```graphql
mutation MyMutation {
  updateSeason(
    external_id: "seas_ext_id"
    language: "en"
    ..rest
  )
}
```

---

## Delete Season

### GraphQL

#### Using UID

```graphql
mutation MyMutation {
  deleteSeason(uid: "01H502WM10WXSCH68J5ZEW7N7Q") {
    uid # GraphQL requires a return field
  }
}
```

#### Using External ID

```graphql
mutation MyMutation {
  deleteSeason(external_id: "seas_5cd1826f045449c5afc25798a247b7bd") {
    uid # GraphQL requires a return field
  }
}
```
