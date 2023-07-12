# Episodes

Contents:

- [Get Episode](#get-episode)
- [List Episodes](#list-episodes)
- [Create Episode](#create-episode)
- [Update Episode](#update-episode)
- [Delete Episode](#delete-episode)

Related:

- [Asset](./Assets.md)
- [Season](./Seasons.md)

---

## Get Episode

### Legacy

`/api/episodes/${uid}?fields=`

### GraphQL

```graphql
query MyQuery {
  getEpisode(uid: "01H53N53PM87T9D5HX0XB1HTRE", language: "en") {
  # getEpisode(external_id: "epis_4e4a9d0e3c054790886684b924e1d13c", language: "en") {
    external_id
    internal_title
    title
    synopsis
    slug
    episode_number
    tags {
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
    "getEpisode": {
      "external_id": "epis_bb05726f231b46dcaecc51874bf25917",
      "internal_title": "Stepping Into The Unknown",
      "title": "Stepping Into The Unknown",
      "synopsis": "It's the British Trampoline Championships, and Theo is competing for the first time in a synchro pair!",
      "slug": "test",
      "episode_number": 5,
      "tags": {
        "objects": []
      }
    }
  }
}
```

---

## List Episodes

### Legacy

`/api/episodes/?fields=`


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
   "slug":"",
   "title":"",
   "parent_url":"",
   "language":"en",
   "alternate_synopsis":"",
   "name":"",
   "synopsis":"",
   "episode_number":""
}
```

### GraphQL

```graphql
query MyQuery {
  listEpisode(language: "en", next_token: "", limit: 1) {
    next_token
    objects {
      external_id
      internal_title
      title
      synopsis
      slug
      episode_number
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
    "listEpisode": {
      "next_token": "eyJfbGlzdF9rZXkiOiAicGJibDRlam9semh3emU3NHphZTJheHJ0am0jRXBpc29kZXxsYW5nI2VuIiwgIl9pZCI6ICJwYmJsNGVqb2x6aHd6ZTc0emFlMmF4cnRqbSMwMUg1M040UEsyWlpRNEtUWlNGNzlFRFk5WSIsICJfc2siOiAicGJibDRlam9semh3emU3NHphZTJheHJ0am0jMDFINTNONFBLMlpaUTRLVFpTRjc5RURZOVkjZW4ifQ==",
      "objects": [
        {
          "external_id": "epis_c776277d289847efa3e2eb3fb2cd9fd0",
          "internal_title": "Back To the Moon",
          "title": "Back To the Moon",
          "synopsis": "Half a century since the last Apollo mission landed on the moon, astrophysicist Alan Duffy takes us inside the new space race.",
          "slug": "test",
          "episode_number": 6,
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

## Create Episode

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
   "slug":"",
   "title":"",
   "parent_url":"",
   "language":"en",
   "alternate_synopsis":"",
   "name":"",
   "synopsis":"",
   "episode_number":""
}
```

### GraphQL

```graphql
mutation MyMutation {
  createEpisode(
    language: "en"
    episode: {
      external_id: "asse_ext_id",
      slug: "current-both-d",
      episode_number: 1,
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
    "createEpisode": {
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

## Update Episode

### GraphQL

```graphql
mutation MyMutation {
  updateEpisode(
    uid: "01H53QSQAGFGSF0R26QTY5T4MC",
    language: "en"
    episode: {
      external_id: "epis_ext_id",
      slug: "current-both-d",
      episode_number: 1,
      synopsis: "",
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
  }
}
```

or using External ID:

```graphql
mutation MyMutation {
  updateEpisode(
    external_id: "epis_ext_id"
    language: "en"
    ..rest
  )
}
```

---

## Delete Episode

### GraphQL

#### Using UID

```graphql
mutation MyMutation {
  deleteEpisode(uid: "01H502WM10WXSCH68J5ZEW7N7Q") {
    uid # GraphQL requires a return field
  }
}
```

#### Using External ID

```graphql
mutation MyMutation {
  deleteEpisode(external_id: "epis_5cd1826f045449c5afc25798a247b7bd") {
    uid # GraphQL requires a return field
  }
}
```
