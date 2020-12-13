- What room types are present in the sample_airbnb.listingsAndReviews collection?

```javascript
let p = [
  {
    $group: {
      _id: "$room_type",
    },
  },
];

db.keyword.aggregate(p);
```

- What are the differences between using aggregate() and find()?

1. Aggregate can do what find can and more.
2. Aggregate allows us to compute and reshape data in the cursor.

- Which of the following commands will return the name and founding year for the 5 oldest companies in the sample_training.companies collection?

```javascript
db.companies
  .find({ founded_year: { $ne: null } }, { name: 1, founded_year: 1 })
  .sort({ founded_year: 1 })
  .limit(5);
```

or

```javascript
db.companies
  .find({ founded_year: { $ne: null } }, { name: 1, founded_year: 1 })
  .limit(5)
  .sort({ founded_year: 1 });
```

- In what year was the youngest bike rider from the sample_training.trips collection born?

```javascript
db.trips
  .find({ "birth year": { $ne: "" } }, { "birth year": 1 })
  .sort({ "birth year": -1 })
  .limit(1);
```

- If you often do queries like this:

```javascript
db.routes.find({ src_airport: "MUC" }).pretty();
```

An index can make the query faster. An example to help:

```javascript
db.routes.createIndex({ src_airport: -1 });
```
