

- Find companies where permalink is the same as twitter user name

```json
db.companies.find(
    {
        "$expr":
        {
            "$eq": ["$permalink", "$twitter_username"]
        }
    },
    {"permalink": 1, "twitter_username": 1} // projection
)
```


- What is the name of the listing in the sample_airbnb.listingsAndReviews dataset that accommodates more than 6 people and has exactly 50 reviews?

```json
db.listingsAndReviews.find(
    {
        "$and":
        [
            {"accommodates": { "$gt":6}},
            {"reviews": { "$size": 50 } },
        ]
    },
    {"accommodates": 1, "name": 1 }
)

```

- Using the sample_airbnb.listingsAndReviews collection find out how many documents have the "property_type" "House", and include "Changing table" as one of the "amenities"?

```json
db.listingsAndReviews.find(
    {
        "$and":
        [
            {"property_type": "House"},
            { "amenities": "Changing table" },
        ]
    },
    {"property_type": 1, "amenities": 1 }
).count()

```