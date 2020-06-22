# Create an API Mongodb, Express and Node (AMEN) stack.

Walkthrough to build AMEN code base from scratch.
1. Create a Project AMEN directory and set-up with Github
2. Build and Run the base Node application

- Separate configuration from code
- Encrypt and secure secrets in GitHub
- Create a Docker images for API code 

## 1. Create a Project AMEN directory and set-up with Github
Create a directory skeleton and README file and add to a new repo in Github.
This will be project AMEN - a base for Mongodb, Express and Node.
```
mkdir amen
cd amen
touch README.md
touch .gitignore
```
Create a README.md file and add some text to it.

Create a repo in Github and commit a file.
```
git init
git add README.md
git commit -m "first commit"
# USER = GitHub username or email address
# REPO = name of repo to create on GitHub e.g. amen
curl -u 'USER' https://api.github.com/user/repos -d '{"name":"REPO"}'
git remote add origin https://github.com/cg2p/amen.git
git push -u origin master
```

## 2. Build and Run the base Node application
Basic tutorial. Initialise npm to install with first modules. Purpose of doing this in pieces is to show how to add in modules as you build the full stack.

```
cd amen
npm init --yes
npm install -g npm
npm install --save http
npm install --save mongoose
npm install --save dotenv
```

Now create .js files to organise the application
```
touch server.js
touch db.js
touch config.js
touch .env
```
Starting code

`.env`
```
// .env
SECRET_API_KEY_DEV=
SECRET_API_KEY_TEST=testsecret
```

`config.js`
```
// config.js
const env = process.env.NODE_ENV; // 'dev' or 'test'

const dev = {
 app: {
   port: parseInt(process.env.DEV_APP_PORT) || 3000
 },
 db: {
   host: process.env.DEV_DB_HOST || 'localhost',
   port: parseInt(process.env.DEV_DB_PORT) || 27017,
   name: process.env.DEV_DB_NAME || 'db'
 }
};
const test = {
 app: {
   port: parseInt(process.env.TEST_APP_PORT) || 3000
 },
 db: {
   host: process.env.TEST_DB_HOST || 'localhost',
   port: parseInt(process.env.TEST_DB_PORT) || 27017,
   name: process.env.TEST_DB_NAME || 'test'
 }
};

const config = {
 dev,
 test
};

module.exports = config[env];
```

`db.js`
```
// db.js
const mongoose = require('mongoose');
const config = require('./config');

const { db: { host, port, name } } = config;
const connectionString = `mongodb://${host}:${port}/${name}`;
mongoose.set('useNewUrlParser', true);
mongoose.connect(connectionString);
```

`app.js`
```
// app.js
const http = require('http');
const db = require('./db');
const config = require('./config');

const requestHandler = (request, response) => {
    console.log(request.url)
    response.end('Hello AMEN Server!')
  }
  
const app = http.createServer(requestHandler)

  
app.listen(config.app.port, (err) => {
    if (err) {
      return console.log('something bad happened', err)
    }
  
    console.log(`secret key is ${config.keys.secretKey} !!`) // to show dotenv working
    console.log(`server is listening on ${config.app.port}`)
  })
  
```

Ensure package.json has correct run scripts
```
...
"scripts": {
    "dev": "NODE_ENV=dev node app.js",
    "test": "NODE_ENV=test node app.js"
  },
...
```

Start mongodb and run the app. Test at http://localhost:3000/
```
# terminal window 1 
mongod &

# terminal window 2
npm run dev
```
Update GitHub by addung updated files to master branch
```
git add .
git commit -m "base node app"
git push -u origin master
```

In case node_modules get added to repo
```
git rm -r --cached node_modules
git commit -m 'Remove the now ignored directory node_modules'
git push origin master
```

## 3. Add in database functions


## 4. Add in API routes
Example API route setup using [Restify](http://restify.com/)
```
cd amen
npm uninstall http
npm install --save restify
```

```
// apiserver.js
const restify = require('restify');
const db = require('./db');
const config = require('./config');

const requestHandler = (request, response) => {
    console.log(request.url)
    response.end('Hello AMEN Server!')
  }
  
const apiserver = restify.createServer({
  name: 'myapp',
  version: '1.0.0'
});

apiserver.use(restify.plugins.acceptParser(apiserver.acceptable));
apiserver.use(restify.plugins.queryParser());
apiserver.use(restify.plugins.bodyParser());

apiserver.get('/', function (req, res, next) {
  res.send("ping!");
  return next();
});

apiserver.get('/echo/:name', function (req, res, next) {
  res.send(req.params);
  return next();
});

apiserver.listen(config.app.port, (err) => {
    if (err) {
      return console.log('something bad happened', err)
    }
  
    console.log('%s %s listening', apiserver.name, apiserver.version);
  })
```

## x. Test client
test node api client
```
mkdir amen-client
cd amen-client
touch client.js
npm init --yes
npm install -g npm
npm install --save axios
```

`client.js`
```
const axios = require('axios');

const axiosClient = axios.create({
  baseURL: 'http://localhost:3000',
  /* other custom settings */
});

axiosClient.get('/echo/hello')
  .then(function (response) {
    // handle success
    console.log("name is %s", response.data.name);
  })
  .catch(function (error) {
    // handle error
    console.log(error);
  })
  .finally(function () {
    //console.log("always executed");
  });
```

`npm run client.js`
