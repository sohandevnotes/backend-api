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

## **"[GET → FIND → PROJECT]"** 📂

### USED: TO GET ALL DATA WITH SPECIFIC FIELDS

### Endpoint: `/allcrops`

```javascript
app.get("/allcrops", async (req, res) => {
  try {
    const crops = await cropsCollection
      .find()
      .project({ description: 0, ratings: 0 })
      .toArray();
    res.status(200).json({ message: "✅ Data retrieved with selected fields", data: crops });
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: "❌ Internal Server Error" });
  }
});
```

### 📝 Notes:

* Retrieves all data from `cropsCollection` but excludes `description` and `ratings`.
* Returns JSON data with a ✅ success message.
* Responds with ❌ `500` if an error occurs.

---

## **"[GET → FIND → PROJECT → LIMIT]"** ⏱️

### USED: TO GET LIMITED DATA WITH SPECIFIC FIELDS

### Endpoint: `/apps`

```javascript
app.get("/apps", async (req, res) => {
  try {
    const { limit=0 } = req.query;
    const apps = await appsCollection
      .find()
      .limit(parseInt(limit))
      .project({ description: 0, ratings: 0 })
      .toArray();
    res.status(200).json({ message: "✅ Limited apps retrieved with selected fields", data: apps });
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: "❌ Internal Server Error" });
  }
});
````

### 📝 Notes:

* Retrieves data from `appsCollection` with a **limit** based on query parameter.
* Excludes `description` and `ratings` fields using `.project()`.
* Returns JSON data with a ✅ success message.
* Responds with ❌ `500` if an error occurs.
* Example request: `/apps?limit=5` 🔹 will return only the first 5 apps.

---
## **"[GET → FIND → PROJECT → LIMIT → SKIP]"** ⏱️↔️

### USED: TO GET LIMITED DATA WITH PAGINATION AND SPECIFIC FIELDS

### Endpoint: `/apps`

```javascript
app.get("/apps", async (req, res) => {
  try {
    const { limit = 0, skip = 0 } = req.query;
    const apps = await appsCollection
      .find()
      .limit(parseInt(limit))
      .skip(parseInt(skip))
      .project({ description: 0, ratings: 0 })
      .toArray();

    res.status(200).json({ message: "✅ Apps retrieved with limit & skip applied", data: apps });
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: "❌ Internal Server Error" });
  }
});
````

### 📝 Notes:

* Retrieves data from `appsCollection` with **limit** and **skip** for pagination.
* Excludes `description` and `ratings` fields using `.project()`.
* Returns JSON data with a ✅ success message.
* Responds with ❌ `500` if an error occurs.
* Example request: `/apps?limit=5&skip=10` 🔹 returns 5 apps starting from the 11th item.
---

## **"[GET → FIND → SORT]"** 🔃

### USED: TO GET ALL DATA WITH SORTING

### Endpoint: `/allcrops/sorted`

```javascript
app.get("/allcrops/sorted", async (req, res) => {
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

* Retrieves all data from `cropsCollection`.
* Sorts by `createdAt` in descending order 🔽.
* Returns JSON data with a ✅ success message.
* Responds with ❌ `500` if an error occurs.

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
* Returns JSON data with a ✅ success message.
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

* Retrieves data filtered by `owner.ownerEmail`.
* Returns JSON data with a ✅ success message.
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

* Retrieves specific data using `_id`.
* Converts `id` to `ObjectId` for proper MongoDB queries.
* Returns JSON data with a ✅ success message.
* Responds with ❌ `500` if an error occurs.

```





