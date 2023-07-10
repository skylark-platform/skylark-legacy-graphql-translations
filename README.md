# Macademia Skylark GraphQL Translations

Collection of documents translating Skylark Legacy's API calls to Skylark's GraphQL Queries.

Full API documentation: https://docs.skylarkplatform.com/

## Read this first:

### Authentication

Making calls to Skylark requires an API key.

A member of the Customer Success team will supply you with a number of API keys with varying levels of permissions.
If you require more, we can generate these for you.

Documentation on how to use the API Keys and what the permission levels mean: https://docs.skylarkplatform.com/docs/authentication

---

### Look up via UID or External ID

There are two ways to retrieve your objects using a `get{OBJECT}` query in Skylark.

#### Using the UID:

```graphql
query MyQuery {
  getEpisode(uid: "01H502WM10WXSCH68J5ZEW7N7Q") {
    uid
    title
  }
}
```

#### Using the External ID:

```graphql
query MyQuery {
  getEpisode(external_id: "epis_5af2454064ee4e5eaaab137d46a91f21") {
    uid
    title
  }
}
```

Note: All objects migrated to your account from Skylark Legacy use their old UID as the External ID.

---

### Determining Object Type in a Search or Set Content query

Listing objects returned as Search results or Set Content works slightly differently than listing out a single object type such as Episodes (`listEpisode`).

This is because at request time we need to tell GraphQL what fields we want back for each object type.

```graphql
query MyQuery {
  getSkylarkSet(uid: "01H502WM10WXSCH68J5ZEW7N7Q") {
    title
    uid
    content {
      objects {
        uid
        __typename
        ... on Episode {
          title
          episode_number
        }
        ... on Movie {
          year_of_release
          synopsis
        }
      }
    }
  }
}
```

*A note on `__typename`*

In the example above, we're getting back two fields which are available on all objects regardless of type. `uid` and `__typename`.
`__typename` is a built-in GraphQL field which we can use this later to determine the type of the object, in this case either `Episode` or `Movie`.

More on this:

1. Set Content documentation: https://docs.skylarkplatform.com/docs/getting-a-set#get-a-set-and-specific-object-fields
2. Search documentation: https://docs.skylarkplatform.com/docs/searching-content

---


### Pagination

The best way to use Pagination is to pass the `next_token` as a variable which may look something like this:

```graphql
query MyQuery($nextToken: String) {
  listSeason(next_token: $nextToken, limit: 10) {
    next_token
    objects {
      uid
    }
  }
}
```

Then in your GraphQL request you pass in the variable:

```json
{
  "nextToken": "your_next_token",
}
```

Note: In your first request, where you don't have a next_token as it's the first page, the `nextToken` variable can either not be sent, be an empty string (`""`) or be `null`.

More on pagination: https://docs.skylarkplatform.com/docs/introduction-6#get-next-paginated-data-page

---

### Common Query arguments

1. `limit`: The number of items to receive back in a list query. Anything from 1-50 (anything higher will return 50).
2. `next_token`: See previous section, on subsequent list queries you provide a `next_token` which Skylark uses to get the next page of objects.
3. `language`: The request language. If this isn't supplied it will default to the default account language of `en`.
