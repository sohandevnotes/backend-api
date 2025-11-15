**Basic "GET"**:

```javascript
app.get("/apps", async (req, res) => {
  try {
    const apps = await appsCollection.find().toArray();
    res.send(apps);
  } catch (error) {
    console.error(error);
    res.status(500).json({ error: "Internal Server Error" });
  }
});
```

---

### Notes:

* Retrieves data from the `appsCollection` in MongoDB.
* Returns the data in JSON format.
* Responds with a `500` status code if an error occurs.
