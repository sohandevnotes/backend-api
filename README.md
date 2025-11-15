# 🚀 Backend API Setup Guide (Node.js + Express)

This guide walks you step-by-step through creating a basic **Node.js + Express backend API** from scratch.  
Follow each step carefully to set up your project structure, initialize dependencies, and start your development server.


---

## 📌 01. Create `package.json` File

The `package.json` file stores information about your project such as dependencies, scripts, and metadata.

Run:

```bash
npm init -y
````

This will automatically generate a default `package.json` file.

---

## 📌 02. Update `"scripts"` Inside `package.json`

The `scripts` section allows you to run your project using short commands.

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
* **dev** → Uses `nodemon` to auto-reload on file changes
* **test** → Placeholder for future test scripts

---

## 📌 03. Install Express

Express is a lightweight, flexible web framework for building backend APIs.

Install:

```bash
npm install express --save
```

---

## 📌 04. Create `index.js` (Basic Server Setup)

Create a file named **index.js** and add the following:

```javascript
/*** ----------- IMPORTS ----------- ***/
const express = require('express');
const app = express();

/*** ----------- MIDDLEWARE ----------- ***/
app.use(express.json());

/*** ----------- ROUTES ----------- ***/
const port = 3000;

app.get('/', (req, res) => {
  res.send('Hello World!');
});

/*** ----------- SERVER ----------- ***/
app.listen(port, () => {
  console.log(`Example app listening on port ${port}`);
});
```

### ✔️ What this code does:

* Initializes an Express server
* Enables JSON parsing
* Defines a simple GET route
* Starts the server on **port 3000**

---

## 📌 05. Install Nodemon (Auto-Restart During Development)

Nodemon automatically restarts your server whenever you save changes.

Install:

```bash
npm install nodemon --save-dev
```

Run your server in development mode:

```bash
npm run dev
```

---

## 📌 06. Install CORS

CORS (Cross-Origin Resource Sharing) allows your API to be accessed by a frontend running on another domain or port.

Install:

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

## 📌 07. Install DOTENV (For Environment Variables)

DOTENV helps you keep sensitive values like API keys, passwords, and ports hidden inside a `.env` file.

Install:

```bash
npm install dotenv
```

### 📌 Create `.env` file

Example:

```
PORT=3000
```

### 📌 Add DOTENV to `index.js`

```javascript
/*** ----------- IMPORTS ----------- ***/
const express = require('express');
const cors = require('cors');
require("dotenv").config();
const app = express();

/*** ----------- MIDDLEWARE ----------- ***/
app.use(express.json());
app.use(cors());

/*** ----------- ROUTES ----------- ***/
app.get('/', (req, res) => {
  res.send('Hello World!');
});

/*** ----------- SERVER ----------- ***/
const port = process.env.PORT || 3000;
app.listen(port, () => {
  console.log(`Server running on port ${port}`);
});
```

---

## 🎉 You're Ready to Start!

Start the development server:

```bash
npm run dev
```

Start without nodemon:

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
└-- .env   (environment variables)
```

---

## 🙌 Happy Coding!

If you want, I can help you expand this project into a complete production-ready backend:

* Routes & Controllers
* Middlewares
* Database Integration (MongoDB, PostgreSQL, MySQL, etc.)
* Authentication (JWT, OAuth)
* Environment-Based Config Files
* API Documentation
* Project Architecture Best Practices

Just tell me — I’m here to help! 🚀

```
