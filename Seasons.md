# Seasons

## List Seasons

### Legacy

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
query LIST_SEASON {
  listSeason(language: "en", next_token: "") {
    objects {
      brands(limit: 1) {
        objects {
          uid
        }
      }
      slug
      title
      title_short
      synopsis
      synopsis_short
      internal_title
      tags {
        objects {
          uid
        }
      }
    }
    next_token
  }
}
```
