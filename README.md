## Express Setup
To set up a new express application, in an empty folder follow these steps.

1. Initialize npm which will create a package.json file. You can accept all the defaults.
```
npm init -y
```

2. Install the [express](https://expressjs.com/) library
```
npm install express
```

3. Install [nodemon](https://www.npmjs.com/package/nodemon). This is a utility tool that will automatically restart our express server any time we change code. We use the `--save-dev` flag when installing so that it only installs as a developer dependency, it won't install on a live production version.
```
npm install --save-dev nodemon
```

4. Install the [morgan](https://expressjs.com/en/resources/middleware/morgan.html) middleware. Express middleware allows us to extend express with additional functionality. Morgan is express middleware we can use to have our server automatically log all requests. This helps gives us visibility of what our server is doing.
```
npm install morgan
```

5. Install the [cors](https://expressjs.com/en/resources/middleware/cors.html) middleware. This allows us to make HTTP requests to our API using fetch from the browser.
```
npm install cors
```

> **TIP!** You can install mutiple NPM packages by listing all of them in the same command, for example:
> 
> `npm install express morgan cors`
> 
> We have not included the `nodemon` package in this list because that is installed as a "developer dependency" (something which we only use for local development and which is not needed as part of the deployed production version of the app). This is why the installation command in step 3 above includes the `--save-dev` flag.
>
> If we have multiple packages that we want to install as dev dependencies, then we can also list them all at once but we just need to include the `--save-dev` flag once:
>
> `npm install --save-dev nodemon eslint prettier`

6. Inside a `/src` directory, create two files.

- Create a file that will run our app: `index.js` . This is our *entrypoint* - the source file that will start running our server. This file is commonly referred to as an "app runner".
- Create a file that will define what our app does: `server.js`

7. In the app runner, add this code:

```js
const app = require('./server.js')
const port = 3030

app.listen(port, () => {
 console.log(`Server is running on http://localhost:${port}/`)
})
```

8. In the file that defines what the app does:

```javascript
//Include the express library
const express = require("express")
//Include the morgan middleware
const morgan = require("morgan")
//Include the cors middleware
const cors = require("cors")

//Create a new express application
const app = express()

//Tell express we want to use the morgan library
app.use(morgan("dev"))
//Tell express we want to use the cors library
app.use(cors())
//Tell express to parse JSON in the request body
app.use(express.json())

//Export our app so other files can run it
module.exports = app
```

9. Update your package.json file and replace the "scripts" section with the following:

```json
"scripts": {
   "start" : "npx nodemon ./src/index.js"
},
```

10. Finally, start up our server!
```
npm start
```

If you see `Server is running on http://localhost:3030` in your terminal, your server is now running and *listening* for HTTP requests.

Great work!