### 01. Create "package.json" file

```bash
npm init -y
```


### 02. Update "package.json >> scripts" file

```bash
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
```


### 03. Install 'express npm package"
```bash
npm install express --save
```


### 04. Install 'index.js" file with initial stracture
```bash
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```

