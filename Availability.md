# Availability

*Availability is a built-in Skylark Object Type*

Availability replaces and combines Schedules and Licenses into one simple way to determine which user's have access and can see each object.

More on Availability: https://docs.skylarkplatform.com/docs/introduction-to-availability

Contents:

- [Get Always Availability](#get-always--forever-availability)

---

## Get "Always & Forever" Availability

### Legacy

`/api/schedules/{'always'}`

### GraphQL

```graphql
query MyQuery {
  getAvailability(external_id: "skylark_legacy_ingest_availability") {
    uid
    title
    slug
    start
    end
    timezone
  }
}
```

We've preconfigured all migrated objects to have an "Always & Forever" Availability assigned to them. This means they're available to all customers with no end date.

You can see above we're accessing it using the pre-defined External ID `skylark_legacy_ingest_availability`. You can change this to whatever you want (e.g. `always`).

Alternatively, you can use an Availability's UID to fetch it (`uid: ""`).
