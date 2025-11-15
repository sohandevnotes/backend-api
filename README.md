Here is your cleaned, corrected, and properly formatted **README.md**, including fixes for duplicate sections, improved explanations, and clean markdown formatting.
I also corrected your numbering and description for CORS.

---

# 🚀 Backend API Setup Guide (Node.js + Express)

This guide walks you step-by-step through creating a basic **Node.js + Express backend API** from scratch.
Follow each step carefully to set up your project structure, initialize packages, and start your development server.

---

## 📌 01. Create `package.json` File

The `package.json` file stores information about your project, including dependencies, scripts, and metadata.

Run:

```bash
npm init -y
```

This will automatically generate a default `package.json` file.

---

## 📌 02. Update `"scripts"` Inside `package.json`

The `scripts` section lets you define commands to run your project easily.

Add or update:

```json
"scripts": {
  "start": "node index.js",
  "dev": "nodemon index.js",
  "test": "echo \"Error: no test specified\" && exit 1"
}
```

### ✔️ What these scripts do?

* **start** → Runs the server using Node.js
* **dev** → Uses `nodemon` so your server auto-reloads when files change
* **test** → Placeholder for automated tests

---

## 📌 03. Install Express

Express is a lightweight web framework that makes building backend APIs simple and efficient.

Install it:

```bash
npm install express --save
```

---

## 📌 04. Create `index.js` (Basic Server Setup)

This file is the entry point of your backend application.
Create a file named `index.js` and add the following:

```javascript
const express = require('express');
const app = express();
app.use(express.json());
const port = 3000;

app.get('/', (req, res) => {
  res.send('Hello World!');
});

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`);
});
```

### ✔️ What this code does:

* Creates an Express server
* Adds JSON body parsing (`express.json()`)
* Defines a GET route (`/`)
* Starts the server on **port 3000**
* Logs a startup message

---

## 📌 05. Install Nodemon (for Auto-Restart in Development)

Nodemon automatically restarts your server whenever you modify your code — extremely useful during development.

```bash
npm install nodemon --save-dev
```

Then run your server with:

```bash
npm run dev
```

---

## 📌 06. Install CORS

CORS (Cross-Origin Resource Sharing) allows your backend API to be accessed from other domains (e.g., frontend apps).

Install CORS:

```bash
npm install cors
```

### 📌 Add CORS to `index.js`

```javascript
/*** ----------- IMPORTS ----------- ***/
const express = require('express');
const cors = require('cors');
const app = express();

/*** ----------- MIDDLEWARE ----------- ***/
app.use(express.json());
app.use(cors());

/*** ----------- ROUTES ----------- ***/
app.get('/', (req, res) => {
  res.send('Hello World!');
});

/*** ----------- SERVER ----------- ***/
const port = 3000;
app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

---

## 🎉 You're Ready to Start!

Run the development server:

```bash
npm run dev
```

Or start without nodemon:

```bash
npm start
```

---

## 🧩 Recommended Folder Structure

```
project-folder/
│-- package.json
│-- index.js
│-- node_modules/
└-- .env   (optional for environment variables)
```

---

## 🙌 Happy Coding!

If you'd like, I can help you expand this into a complete backend architecture:

* Routes
* Controllers
* Middleware
* Services
* Database (MongoDB, PostgreSQL, MySQL, etc.)
* Authentication (JWT, OAuth)
* Project Best Practices

Just let me know — I’d be happy to help! 🚀
