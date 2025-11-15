# API Documentation

## **"[GET → FIND]"**

### Endpoint: `/allcrops`

```javascript
app.get("/allcrops", async (req, res) => {
  try {
    const crops = await cropsCollection.find().toArray();
    res.status(200).json({ message: "Data retrieved successfully", data: crops });
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: "Internal Server Error" });
  }
});
````

### Notes:

* Retrieves data from the `cropsCollection` in MongoDB.
* Returns the data in JSON format along with a success message.
* Responds with a `500` status code if an error occurs.

---

## **"[GET → FIND → SORT]"**

### Endpoint: `/apps`

```javascript
app.get("/apps", async (req, res) => {
  try {
    const crops = await cropsCollection.find().sort({ createdAt: -1 }).toArray();
    res.status(200).json({ message: "Apps retrieved and sorted by creation date", data: crops });
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: "Internal Server Error" });
  }
});
```

### Notes:

* Retrieves data from the `cropsCollection` in MongoDB.
* Sorts the data by `createdAt` in descending order (`-1`).
* Returns the data in JSON format along with a success message.
* Responds with a `500` status code if an error occurs.

````
