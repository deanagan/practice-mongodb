- Find companies where permalink is the same as twitter user name

```json
db.companies.find(
  {
    "$expr": {
      "$eq": ["$permalink", "$twitter_username"]
    }
  },
  { "permalink": 1, "twitter_username": 1 } // projection
)
```

- What is the name of the listing in the sample_airbnb.listingsAndReviews dataset that accommodates more than 6 people and has exactly 50 reviews?

```json
db.listingsAndReviews.find(
  {
    "$and": [{ "accommodates": { "$gt": 6 } }, { "reviews": { "$size": 50 } }]
  },
  { "accommodates": 1, "name": 1 }
)
```

- Using the sample_airbnb.listingsAndReviews collection find out how many documents have the "property_type" "House", and include "Changing table" as one of the "amenities"?

```json
db.listingsAndReviews
  .find(
    {
      "$and": [{ "property_type": "House" }, { "amenities": "Changing table" }]
    },
    { "property_type": 1, "amenities": 1 }
  )
  .count()
```

- Get all listings that have "Free parking on premises", "Air conditioning", and "Wifi" as part of their amenities, and have at least 2 bedrooms in the sample_airbnb.listingsAndReviews collection

```json
db.listingsAndReviews
  .find({
    "amenities": {
      "$all": ["Free parking on premises", "Wifi", "Air conditioning"]
    },
    "bedrooms": { "$gte": 2 }
  })
  .pretty()
```

- How many companies in the sample_training.companies collection have offices in the city of Seattle?

```json
db.companies.find(
    {"offices":
        { "$elemMatch": {"city": "Seattle"} }
    }, {"offices": 1}).count();
```

- Which of the following queries will return only the names of companies from the sample_training.companies collection that had exactly 8 funding rounds?

```json
db.companies.find({ "funding_rounds": { "$size": 8 } }, { "name": 1, "_id": 0 })
```

- How many trips in the sample_training.trips collection started at stations that are to the west of the -74 latitude coordinate?

```json
db.trips
  .find({ "start station location.coordinates.0": { "$lte": -74 } })
  .count()
```

- How many inspections from the sample_training.inspections collection were conducted in the city of NEW YORK?

```json
db.inspections.find({ "address.city": "NEW YORK" }).count()
```

- Return the names and addresses of all listings from the sample_airbnb.listingsAndReviews collection where the first amenity in the list is "Internet"?
