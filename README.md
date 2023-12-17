# nodejs-scaler
Node.js, Express.js repo to learn backend development from Scaler by Mrinal Bhattacharya

## Module 3: Node Module System

### 3.1 The global object
- Like 'window.name' in a browser 'global.name' is not defined within a filename because of modular system of Node.js.
- Contents are containerized in a file's scope and objects are not added universally.

### 3.2 Modules and Modularity
- Contents of each file/ the file itself won't affect each other.
- Contents can be shared. Suppose we have one file 'calculator.js' and one 'test.js' then content among these files can be shared by doing this:
```js
// calculator.js
// --------------
function add(a, b) {
    console.log(a + b);
} 

module.exports = {
    addition: add
}

// test.js
// --------------
const calculator = require("./calculator");

calculator.addition(3, 4); // O/P: 7
```
### 3.3 Child Process Module
- Child process is a node module which is used to create a sub-process within a script. (Refer folder 3/3.3).

### 3.4 OS Module
- Used to get info about the system in which environment is being run. (Refer folder 3/3.4).

### 3.5 Path Module
- Used to deal with paths of files and folders. (Refer folder 3/3.5).

### 3.6 FS Modules with Files
- Used to manipulate/create files in the system. (Refer folder 3/3.6).

### 3.7 FS Modules with Directories
- Used to manipulate/create folders/directories in the system. (Refer folder 3/3.7).

## Module 4: Node Package Manager(NPM)

### 4.1 Introduction to NPM
- Basically a store to install various modules as per requirement.
- Completely OpenSource and you can publish your own modules as well.
- Info is available on https://www.npmjs.com

### 4.2 How to install and use NPM Packages
- To start a npm project
```
$ npm init
```
- Some questions will be asked fill them up
- Now to install a package use
```
$ npm i figlet
```
- 'figlet' is the package 

### 4.3 About .gitignore
- A special file used in git version control.
- It tells which files are needed to be ignored while being pushed to the repository.
- For e.g. there is no point in uploading the 'node_modules' folder as people can download the dependencies themselves using 'package.json' file.

### 4.4 Semantic Versioning
- Versioning is mostly done in this format '^x.y.z' e.g. '^1.5.2'
- 'x' represents major release, 'y' represents minor release and 'z' represents patches.
- '^'(Caret) character represents that for a particular project only this major release version should be used.
- '~'(Tilde) character represents that for a particular project only this exact major and minor release versions should be used upto some patch. e.g '~1.0.4'(means upto 1.0.4).

### 4.5  Publish NPM Package
- Create npm account and add it with
```
$ npm adduser
```
- Now to publish your package/module use
```
$ npm publish
```
## Module 5: Express

### 5.1 Introduction to Express
- Express is a framework built for Node.js. Used for server-side development.
- Features:
    - Fast in the sense of development by removing boilerplate and saving time.
    - Middlewares: For handling requests efficiently and in an organized manner.
    - Routing: Handling urls according to requests. (GET, POST, PUT, etc.)
    - Templates and Scalability.

### 5.2 Express installation
```
$ npm i express
```

### 5.3 Express Usage
- Refer 5/5.3 please

### 5.4 Nodemon
- Stands for 'node-mon'itor
- Used for testing and debugging.
- There is no need to refresh again and again after changes
- Installation: 
```
$ npm -i nodemon
```
- Usage:
```
$ nodemon app.js
```
- Setup package.json:
```json
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "nodemon app.js",
    "start": "node app.js"
},
```
```sh
$ npm start dev
```

### 5.5 Port Environment Variable
- Used when dynamic port generation during hosting
- Ex:
```js
const port = process.env.PORT || 5000; // taking care of dynamic port assignment
app.listen(port, () => console.log(`App listening on port ${port}`));
```

### 5.6 Route parameters &
### 5.7 Handling Multiple Routes
```js
app.get('/courses/:id', (req, res) => {
    let course = courses.find(course => course.id === parseInt(req.params.id));

    if (!course)
    {
        res.status(404).send("Course not found!");
    }
    else
    {
        res.send(course.name);
    }
})
```
### 5.8 Postman (Tool to send post requests)
- For sending POST requests use Postman. Download & Use.
- P.S: ThunderClient is lighter than Postman and available on VSCode. 

### 5.9 POST(CREATE), PUT(UPDATE) & DELETE(DELETE) HTTP methods
- Refer 5/5.3

## Module 6: Middlewares

### 6.1 What are Middlewares?
- Heart of Express.
- Middlewares are the reason why Express is so popular.
- Whenever a request is made, it won't produce a response immediately.
- A response will be passed to multiple middlewares before producing a response.
- They are similar to functions and one middleware transfers control to another.
- In 5/5.3 `express.json()` is used, it's a middleware used to parse data in JSON.

### 6.2 Custom Middleware
- We can make our own middlewares.
- `next` parameter must be used to transfer control.
- We should store our middlewares in different files inside a 'middleware' folder.
- Refer `5/5.3/middlewares` and `5/5.3/app.js`

### 6.3 Third-Party Middlewares
- Visit [`express.js`](https://expressjs.com/en/resources/middleware.html) website for info about middlewares.
- We have used a simple middleware `morgan` in 5/5.3
- It is used to generate log of requests in the console.

## Module 7: Asynchronous Programming

### 7.1 Introduction
- Synchronous means in sequence and Asynchronous means without sequence or maybe simultaneously.
- Synchronous programming is not very efficient, while Asynchronous programming is.
- As some requests may take a long time to respond it's better to run other tasks concurrently. (Non-Blocking Code)
- Asynchronous Programming saves time but utilizes more resources.
- JavaScript is a single threaded programming language but still capable of Asynchronous programming.

### 7.2 Reading files, Synchronously & Asynchronously
- We can read files using 'fs' module as previously mentioned.
- `readFileSync()` for reading synchronously and `readFile()` for asynchronously.
- Similar syntax for other file operations.
- `readFile()` requires a callback function as used in `7/7.2`.

### 7.3 Understanding Event Loop & Previous Module (7.2)
- `Call Stack`: The call stack is used by JavaScript to keep track of multiple function calls. We use call stack for memorizing which function is running right now. [`GFG`](https://www.geeksforgeeks.org/what-is-the-call-stack-in-javascript/)
- Non-async functions will directly execute from the call stack. (e.g. `console.log("First Line...")`)
- Call Stack doesn't execute async functions. It sends it to `Node APIs`.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://github.com/peetank/nodejs-scaler/blob/main/images/diagram-dark.png" height="650px">
  <img alt="Diagram1" src = "https://github.com/peetank/nodejs-scaler/blob/main/images/diagram-light.png" height = "650px" >
</picture>

- Async functions are later on loaded onto the `Call Queue` in a random order. 
- If you run multiple times `7/7.2/syncFile.js`, you will see File2 data might appear above File1's.
- Then the `Event Loop` makes sure that the call stack is empty and starts loading the async functions from the callback queue onto the call stack, execution happens and when the call stack is empty sends the next async function from the queue.
- [`Verbose Explanation`](https://www.webdevolution.com/blog/Javascript-Event-Loop-Explained)
