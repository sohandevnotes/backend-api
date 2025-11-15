Below is the **updated and expanded `.md` documentation**, rewritten to match your **final backend output** exactly.
It includes all steps from project setup to reaching the **final working backend** you showed.

You can copy–paste this as your final Markdown documentation file.

---

# 🚀 Hero Apps Backend — Full Setup Guide (Node.js + Express + MongoDB)

This guide walks you through the complete process of creating the **Hero Apps Backend Server**, including Express setup, MongoDB connection, middlewares, routes, and environment variables.

By the end of this guide, your project will match the **final backend code** shown.

---

# ✅ 01. Initialize Project & Create `package.json`

Run:

```bash
npm init -y
```

This generates a default `package.json`.

---

# ✅ 02. Install Required Dependencies

Run:

```bash
npm install express cors dotenv mongodb
```

For development auto-restart:

```bash
npm install --save-dev nodemon
```

---

# ✅ 03. Update `scripts` in `package.json`

```json
"scripts": {
  "start": "node index.js",
  "dev": "nodemon index.js"
}
```

---

# ✅ 04. Create `.env` File

Inside the project folder, create `.env`:

```
PORT=5000
URI=your-mongodb-connection-string-here
```

---

# ✅ 05. Create `index.js` (Final Server Code)

Create a file named **index.js** and paste the ENTIRE final backend code:

```javascript
//Definition & imports
const express = require("express");
const cors = require("cors");
const { MongoClient, ServerApiVersion, ObjectId } = require("mongodb");
const app = express();

// Middlewares
require("dotenv").config();
app.use(cors());
app.use(express.json());

app.use(async (req, res, next) => {
  console.log(
    `⚡ ${req.method} - ${req.path} from ${
      req.host
    } at ⌛ ${new Date().toLocaleString()}`
  );
  next();
});

//ports & clients
const port = process.env.PORT || 5000;
const uri = process.env.URI;
const client = new MongoClient(uri, {
  serverApi: {
    version: ServerApiVersion.v1,
    strict: true,
    deprecationErrors: true,
  },
});

//listeners
client
  .connect()
  .then(() => {
    app.listen(port, () => {
      console.log(`Hero Apps Server listening ${port}`);
      console.log(`Hero Apps Server Connected with DB`);
    });
  })
  .catch((err) => {
    console.log(err);
  });

//DB & collections
const database = client.db("heroAppsDB");
const appsCollection = database.collection("apps");

//Apps Route
app.get("/apps", async (req, res) => {
  try {
    const apps = await appsCollection.find().toArray();
    res.send(apps);
  } catch (error) {
    console.log(error);
    res.status(500).json({ error: "Internal Server Error" });
  }
});

app.get("/apps/:id", async (req, res) => {
  try {
    const appId = req.params.id;

    if (appId.length != 24) {
      res.status(400).json({ error: "Invalid ID" });
      return;
    }

    const query = new ObjectId(appId);
    const app = await appsCollection.findOne({ _id: query });
    res.json(app);
  } catch (error) {
    console.log(error);
    res.status(500).json({ error: "Internal Server Error" });
  }
});

// Basic routes
app.get("/", (req, res) => {
  res.json({ status: "ok", message: "Hero Apps Server" });
});

//404
app.all(/.*/, (req, res) => {
  res.status(404).json({
    status: 404,
    error: "API not found",
  });
});
```

---

# ✅ 06. Start the Server

### Development (with auto-restart)

```bash
npm run dev
```

### Production

```bash
npm start
```

---

# 📁 Recommended Folder Structure

```
project-folder/
│-- index.js
│-- package.json
│-- .env
│-- node_modules/
└── README.md  (this file)
```

---

# 🎉 Your Backend Is Ready!

Your server now includes:

✔ Express server
✔ CORS enabled
✔ DOTENV for secure config
✔ MongoDB connection with async client
✔ Auto-logging middleware
✔ `/apps` route
✔ `/apps/:id` route with validation
✔ Root route `/`
✔ 404 catch-all route
✔ Production & dev scripts

---

Lets Goo! 🚀
