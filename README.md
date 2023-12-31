# Skylark Legacy -> Skylark GraphQL Translations

Collection of documents translating Skylark Legacy's API calls to Skylark's GraphQL Queries.

Full API documentation: https://docs.skylarkplatform.com/

## Contents:

*Note: Recommend you read the ["Read this first"](#read-this-first) section as it covers a few common parts of Skylark that isn't covered in the individual files.*

- Skylark Builtins
  - [Availability](./Availability.md)
  - [Assets](./Assets.md)
  - [Asset Types](./AssetTypes.md)
  - [Tags](./Tags.md)
- Other
  - [Episodes](./Episodes.md)
  - [Seasons](./Seasons.md)
  - [Brands](./Brands.md)
  - [Tag Categories](./TagCategories.md)


## Read this first:

### Authentication

Making calls to Skylark requires an API key.

A member of the Customer Success team will supply you with a number of API keys with varying levels of permissions.
If you require more, we can generate these for you.

Documentation on how to use the API Keys and what the permission levels mean: https://docs.skylarkplatform.com/docs/authentication

---

### Built-in Skylark Object Types

Some Object Types in your Skylark account are built-in meaning that you are unable to add fields to them.

You can identify these as they are prefixed with `Skylark` or in the Skylark UI have a `sl` following their display name.

Of the Object Types migrated from your Skylark Legacy, only Tags (`SkylarkTag`) are built-in.

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

*Note: Skylark uses the [ULID](https://github.com/ulid/spec) spec for it's UIDs*

#### Using the External ID:

```graphql
query MyQuery {
  getEpisode(external_id: "epis_5af2454064ee4e5eaaab137d46a91f21") {
    uid
    title
  }
}
```

*Note: All objects migrated to your account from Skylark Legacy use their old UID as the External ID.*

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

*Note on `__typename`: In the example above, we're retrieving two fields which are available on all objects regardless of type. `uid` and `__typename`. `__typename` is a built-in GraphQL field which we can use this later to determine the type of the object, in this case it'll be `Episode` or `Movie`.*

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

1. `limit`: The number of items to receive back in a list query. Anything from 1-50 (anything higher will return 50) - Defaults to `10`.
2. `next_token`: See previous section, on subsequent list queries you provide a `next_token` which Skylark uses to get the next page of objects - Defaults to `null`.
3. `language`: The request language - Defaults to the account default (`en` in your case).
