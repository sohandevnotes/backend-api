## **"[GET → FIND]"** 🔍

### USED: TO GET ALL DATA

### Endpoint: `/allcrops`

```javascript
app.get("/allcrops", async (req, res) => {
  try {
    const crops = await cropsCollection.find().toArray();
    res.status(200).json({ message: "✅ Data retrieved successfully", data: crops });
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: "❌ Internal Server Error" });
  }
});
````

### 📝 Notes:

* Retrieves all data from the `cropsCollection` in MongoDB.
* Returns the data in JSON format along with a ✅ success message.
* Responds with a ❌ `500` status code if an error occurs.

---

## **"[GET → FIND → SORT]"** 🔃

### USED: TO GET ALL DATA WITH SORTING

### Endpoint: `/allcrops`

```javascript
app.get("/allcrops", async (req, res) => {
  try {
    const crops = await cropsCollection.find().sort({ createdAt: -1 }).toArray();
    res.status(200).json({ message: "✅ Apps retrieved and sorted by creation date", data: crops });
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: "❌ Internal Server Error" });
  }
});
```

### 📝 Notes:

* Retrieves all data from the `cropsCollection` in MongoDB.
* Sorts the data by `createdAt` in descending order (`-1`) 🔽.
* Returns the data in JSON format along with a ✅ success message.
* Responds with a ❌ `500` status code if an error occurs.

---

## **"[GET → QUERY → FIND]"** 🔎

### USED: TO GET DATA BY SEARCHING

### Endpoint: `/cropsSearch`

```javascript
app.get("/cropsSearch", async (req, res) => {
  try {
    const searchText = req.query.search;
    const result = await cropsCollection
      .find({ name: { $regex: searchText, $options: "i" } })
      .toArray();
    res.status(200).json({ message: "✅ Search results found", data: result });
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: "❌ Internal Server Error" });
  }
});
```

### 📝 Notes:

* Retrieves data based on a search query from `cropsCollection`.
* Case-insensitive search (`$options: "i"`).
* Returns JSON data along with a ✅ success message.
* Responds with ❌ `500` if an error occurs.

---

## **"[GET → QUERY → FIND BY EMAIL]"** 📧

### USED: TO GET DATA BY OWNER EMAIL

### Endpoint: `/myposts`

```javascript
app.get("/myposts", async (req, res) => {
  try {
    const email = req.query.email;
    const filter = { "owner.ownerEmail": email };

    const result = await cropsCollection.find(filter).toArray();
    res.status(200).json({ message: "✅ Data retrieved for the given email", data: result });
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: "❌ Internal Server Error" });
  }
});
```

### 📝 Notes:

* Retrieves data filtered by `owner.ownerEmail` from `cropsCollection`.
* Returns JSON data along with a ✅ success message.
* Responds with ❌ `500` if an error occurs.

---

## **"[GET → QUERY → FINDONE]"** 🔎

### USED: TO GET SPECIFIC DATA USING PARAMS

### Endpoint: `/crops/:id`

```javascript
app.get("/crops/:id", async (req, res) => {
  try {
    const { id } = req.params;
    const objectId = new ObjectId(id);
    const filter = { _id: objectId };

    const result = await cropsCollection.findOne(filter);
    res.status(200).json({ message: "✅ Specific crop data retrieved", data: result });
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: "❌ Internal Server Error" });
  }
});
```

### 📝 Notes:

* Retrieves specific data from `cropsCollection` using `_id`.
* Converts `id` to `ObjectId` for MongoDB queries.
* Returns JSON data along with a ✅ success message.
* Responds with ❌ `500` if an error occurs.
