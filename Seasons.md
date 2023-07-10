# Seasons

Contents:

- [Get Season](#get-season)
- [List Seasons](#list-seasons)
- [Create/Update Season](#createupdate-season)
- [Delete Season](#delete-season)

---

## Get Season

### Legacy

`/api/season/${uid}?fields=`

### GraphQL

```graphql
query MyQuery {
  getSeason(uid: "01H502WM10WXSCH68J5ZEW7N7Q", language: "en") {
  # getSeason(external_id: "seas_5cd1826f045449c5afc25798a247b7bd", language: "it") {
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
  listSeason(language: "en", next_token: "", limit: 10) {
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

Coming soon...


---

## Create/Update Season

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
