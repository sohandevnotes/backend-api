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

* Retrieves data from the `cropsCollection` in MongoDB.
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

* Retrieves data from the `cropsCollection` in MongoDB.
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
    console.log(searchText);
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

* Retrieves data from the `cropsCollection` in MongoDB based on a search query.
* The search is case-insensitive (`$options: "i"`).
* Returns the data in JSON format along with a ✅ success message.
* Responds with a ❌ `500` status code if an error occurs.

---

## **"[GET → QUERY → FINDONE]"** 🔎

### USED: TO GET SPECIFIC DATA USING PARAMETERS

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

* Retrieves specific data from the `cropsCollection` in MongoDB based on the provided `id`.
* The `id` is converted to `ObjectId` for proper MongoDB query filtering.
* Returns the data in JSON format along with a ✅ success message.
* Responds with a ❌ `500` status code if an error occurs.
