Upsert means to either insert a new document or to update if there exists a match.

Example of Syntax:

```javascript
db.iot.updateOne(
  // Match
  { sensor: r.sensor, date: r.date, valcount: { $lt: 48 } },
  // Action. If there is no match, new document is created.
  {
    $push: { readings: { v: r.value, t: r.time } },
    $inc: { valcount: 1, total: r.value },
  },
  // set to true to enable upsert behaviour.
  { upsert: true }
);
```

Note:

- By default, upsert is set to **false**, which does not insert a new document when no match is found.
- When upsert is set to false and the query predicate returns an empty cursor then there will be no updated documents as a result of this operation.
- When upsert is set to true and the query predicate returns an empty cursor, the update operation creates a new document using the directive from the query predicate and the update predicate.