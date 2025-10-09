# JavaScript/Node.js Cheat Sheet

## Table of Contents
- [JavaScript Basics](#javascript-basics)
- [Variables & Data Types](#variables--data-types)
- [Functions](#functions)
- [Arrays & Objects](#arrays--objects)
- [Control Flow](#control-flow)
- [Promises & Async/Await](#promises--asyncawait)
- [ES6+ Features](#es6-features)
- [DOM Manipulation](#dom-manipulation)
- [Node.js Basics](#nodejs-basics)
- [NPM & Package Management](#npm--package-management)
- [File System Operations](#file-system-operations)
- [HTTP & Express.js](#http--expressjs)
- [Environment & Configuration](#environment--configuration)
- [Testing](#testing)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

## JavaScript Basics

### Running JavaScript
```javascript
// In browser console
console.log('Hello World');

// In Node.js
node script.js

// In HTML file
<script src="script.js"></script>
<script>
  console.log('Inline JavaScript');
</script>
```

### Comments
```javascript
// Single line comment

/*
Multi-line comment
Can span multiple lines
*/

/**
 * JSDoc comment for documentation
 * @param {string} name - The name parameter
 * @returns {string} A greeting message
 */
```

## Variables & Data Types

### Variable Declarations
```javascript
// Modern ES6+ (recommended)
let mutableVariable = 'can be changed';
const immutableVariable = 'cannot be changed';

// Older syntax (avoid in modern code)
var oldStyleVariable = 'function-scoped';

// Multiple declarations
let a = 1, b = 2, c = 3;
const { name, age } = person; // Destructuring
```

### Primitive Data Types
```javascript
// String
const name = 'John';
const template = `Hello ${name}!`; // Template literal

// Number
const integer = 42;
const float = 3.14;
const scientific = 2e3; // 2000

// Boolean
const isActive = true;
const isComplete = false;

// Undefined and Null
let undefinedVar;
const nullVar = null;

// Symbol (ES6)
const uniqueId = Symbol('id');

// BigInt (ES2020)
const bigNumber = 123456789012345678901234567890n;
```

### Type Checking
```javascript
// typeof operator
typeof 'hello';        // 'string'
typeof 42;             // 'number'
typeof true;           // 'boolean'
typeof undefined;      // 'undefined'
typeof null;           // 'object' (known quirk)
typeof {};             // 'object'
typeof [];             // 'object'
typeof function(){};   // 'function'

// Better type checking
Array.isArray([]);           // true
Number.isInteger(42);        // true
Object.prototype.toString.call(null); // '[object Null]'
```

## Functions

### Function Declarations
```javascript
// Function declaration (hoisted)
function greet(name) {
  return `Hello, ${name}!`;
}

// Function expression
const greet = function(name) {
  return `Hello, ${name}!`;
};

// Arrow function (ES6)
const greet = (name) => `Hello, ${name}!`;
const greet = name => `Hello, ${name}!`; // Single parameter
const add = (a, b) => a + b;             // Single expression

// Multi-line arrow function
const processData = (data) => {
  const processed = data.map(item => item * 2);
  return processed.filter(item => item > 10);
};
```

### Advanced Function Features
```javascript
// Default parameters
function greet(name = 'World') {
  return `Hello, ${name}!`;
}

// Rest parameters
function sum(...numbers) {
  return numbers.reduce((total, num) => total + num, 0);
}

// Destructuring parameters
function createUser({ name, email, age = 18 }) {
  return { name, email, age };
}

// Higher-order functions
const multiplyBy = (factor) => (number) => number * factor;
const double = multiplyBy(2);
console.log(double(5)); // 10

// Immediately Invoked Function Expression (IIFE)
(function() {
  console.log('This runs immediately');
})();
```

## Arrays & Objects

### Array Methods
```javascript
const numbers = [1, 2, 3, 4, 5];
const fruits = ['apple', 'banana', 'orange'];

// Adding/Removing elements
fruits.push('grape');           // Add to end
fruits.unshift('kiwi');         // Add to beginning  
fruits.pop();                   // Remove from end
fruits.shift();                 // Remove from beginning
fruits.splice(1, 2, 'mango');   // Remove/insert at index

// Iteration methods
numbers.forEach(num => console.log(num));
const doubled = numbers.map(num => num * 2);
const evens = numbers.filter(num => num % 2 === 0);
const sum = numbers.reduce((total, num) => total + num, 0);

// Search methods
fruits.includes('apple');       // true/false
fruits.indexOf('banana');       // index or -1
fruits.find(fruit => fruit.startsWith('a')); // first match
fruits.findIndex(fruit => fruit === 'orange'); // index of match

// Array manipulation
const combined = [...fruits, ...numbers]; // Spread operator
const sliced = fruits.slice(1, 3);        // Extract portion
```

### Object Operations
```javascript
// Object creation
const person = {
  name: 'John',
  age: 30,
  city: 'New York'
};

// Property access
console.log(person.name);     // Dot notation
console.log(person['name']);  // Bracket notation
const prop = 'age';
console.log(person[prop]);    // Dynamic property

// Object methods
Object.keys(person);          // ['name', 'age', 'city']
Object.values(person);        // ['John', 30, 'New York']  
Object.entries(person);       // [['name', 'John'], ...]

// Object manipulation
const updatedPerson = { ...person, age: 31 }; // Spread operator
const { name, ...rest } = person;             // Destructuring

// Object.assign for merging
const merged = Object.assign({}, person, { country: 'USA' });
```

### Destructuring
```javascript
// Array destructuring
const [first, second, ...rest] = [1, 2, 3, 4, 5];
const [a, , c] = [1, 2, 3]; // Skip elements

// Object destructuring  
const { name, age } = person;
const { name: fullName, age: years } = person; // Rename
const { country = 'USA' } = person;            // Default value

// Nested destructuring
const user = {
  id: 1,
  profile: {
    name: 'John',
    contact: { email: 'john@example.com' }
  }
};
const { profile: { name, contact: { email } } } = user;
```

## Control Flow

### Conditional Statements
```javascript
// if/else
if (age >= 18) {
  console.log('Adult');
} else if (age >= 13) {
  console.log('Teenager');
} else {
  console.log('Child');
}

// Ternary operator
const status = age >= 18 ? 'Adult' : 'Minor';

// Switch statement
switch (day) {
  case 'monday':
  case 'tuesday':
    console.log('Weekday');
    break;
  case 'saturday':
  case 'sunday':
    console.log('Weekend');
    break;
  default:
    console.log('Unknown day');
}
```

### Loops
```javascript
// for loop
for (let i = 0; i < 5; i++) {
  console.log(i);
}

// for...of loop (values)
for (const item of array) {
  console.log(item);
}

// for...in loop (keys/indices)
for (const key in object) {
  console.log(key, object[key]);
}

// while loop
let i = 0;
while (i < 5) {
  console.log(i);
  i++;
}

// do...while loop
do {
  console.log('Runs at least once');
} while (false);

// forEach (arrays)
array.forEach((item, index) => {
  console.log(index, item);
});
```

## Promises & Async/Await

### Promises
```javascript
// Creating a Promise
const myPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    const success = Math.random() > 0.5;
    if (success) {
      resolve('Operation successful');
    } else {
      reject(new Error('Operation failed'));
    }
  }, 1000);
});

// Using Promises
myPromise
  .then(result => console.log(result))
  .catch(error => console.error(error))
  .finally(() => console.log('Always runs'));

// Promise.all (all must succeed)
Promise.all([promise1, promise2, promise3])
  .then(results => console.log(results));

// Promise.allSettled (wait for all, regardless of outcome)
Promise.allSettled([promise1, promise2, promise3])
  .then(results => console.log(results));

// Promise.race (first to complete)
Promise.race([promise1, promise2, promise3])
  .then(result => console.log(result));
```

### Async/Await
```javascript
// Async function
async function fetchData() {
  try {
    const response = await fetch('https://api.example.com/data');
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Error fetching data:', error);
    throw error;
  }
}

// Using async function
async function main() {
  try {
    const data = await fetchData();
    console.log(data);
  } catch (error) {
    console.error('Main error:', error);
  }
}

// Async arrow function
const fetchUserData = async (userId) => {
  const response = await fetch(`/users/${userId}`);
  return response.json();
};

// Parallel async operations
async function fetchMultipleData() {
  const [users, posts, comments] = await Promise.all([
    fetchUsers(),
    fetchPosts(), 
    fetchComments()
  ]);
  return { users, posts, comments };
}
```

## ES6+ Features

### Template Literals
```javascript
const name = 'John';
const age = 30;

// Multi-line strings
const message = `
  Hello ${name}!
  You are ${age} years old.
  Next year you'll be ${age + 1}.
`;

// Tagged template literals
function highlight(strings, ...values) {
  return strings.reduce((result, string, i) => {
    return result + string + (values[i] ? `<mark>${values[i]}</mark>` : '');
  }, '');
}

const highlighted = highlight`Hello ${name}, you are ${age} years old`;
```

### Classes
```javascript
// Class declaration
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  // Method
  greet() {
    return `Hello, I'm ${this.name}`;
  }

  // Getter
  get info() {
    return `${this.name} (${this.age})`;
  }

  // Setter
  set birthYear(year) {
    this.age = new Date().getFullYear() - year;
  }

  // Static method
  static createAnonymous() {
    return new Person('Anonymous', 0);
  }
}

// Inheritance
class Student extends Person {
  constructor(name, age, grade) {
    super(name, age);
    this.grade = grade;
  }

  greet() {
    return `${super.greet()}, I'm a student in grade ${this.grade}`;
  }
}
```

### Modules
```javascript
// export.js
export const PI = 3.14159;
export function square(x) { return x * x; }
export default class Calculator { /* ... */ }

// import.js
import Calculator, { PI, square } from './export.js';
import * as math from './math.js';
import { square as sq } from './export.js'; // Rename import

// Dynamic imports
async function loadModule() {
  const module = await import('./dynamic-module.js');
  module.doSomething();
}
```

### Other ES6+ Features
```javascript
// Set
const uniqueNumbers = new Set([1, 2, 3, 3, 4]);
uniqueNumbers.add(5);
uniqueNumbers.has(3); // true

// Map  
const userRoles = new Map();
userRoles.set('john', 'admin');
userRoles.set('jane', 'user');

// WeakMap and WeakSet (garbage collected when refs are gone)
const weakMap = new WeakMap();
const weakSet = new WeakSet();

// Optional Chaining (ES2020)
const user = { profile: { name: 'John' } };
console.log(user.profile?.name);        // 'John'
console.log(user.profile?.age);         // undefined
console.log(user.nonexistent?.name);    // undefined

// Nullish Coalescing (ES2020)
const defaultName = user.name ?? 'Anonymous';
const config = { timeout: user.timeout ?? 5000 };
```

## DOM Manipulation

### Selecting Elements
```javascript
// Single element selectors
const element = document.getElementById('myId');
const element = document.querySelector('.class-name');
const element = document.querySelector('#myId');
const element = document.querySelector('div[data-id="123"]');

// Multiple element selectors  
const elements = document.getElementsByClassName('class-name');
const elements = document.getElementsByTagName('div');
const elements = document.querySelectorAll('.class-name');

// Traversal
const parent = element.parentNode;
const children = element.children;
const siblings = element.nextElementSibling;
const previous = element.previousElementSibling;
```

### Modifying Elements
```javascript
// Content manipulation
element.textContent = 'New text content';
element.innerHTML = '<strong>New HTML content</strong>';

// Attribute manipulation
element.getAttribute('data-id');
element.setAttribute('data-id', '123');
element.removeAttribute('data-id');
element.hasAttribute('data-id');

// Class manipulation
element.classList.add('new-class');
element.classList.remove('old-class');
element.classList.toggle('active');
element.classList.contains('active');

// Style manipulation
element.style.color = 'red';
element.style.backgroundColor = 'blue';
element.style.cssText = 'color: red; background: blue;';

// Creating and inserting elements
const newElement = document.createElement('div');
newElement.textContent = 'New element';
parent.appendChild(newElement);
parent.insertBefore(newElement, referenceElement);
```

### Event Handling
```javascript
// Adding event listeners
element.addEventListener('click', function(event) {
  console.log('Element clicked');
  event.preventDefault(); // Prevent default behavior
  event.stopPropagation(); // Stop event bubbling
});

// Arrow function event listener
element.addEventListener('click', (event) => {
  console.log('Clicked:', event.target);
});

// Event delegation (for dynamic content)
document.addEventListener('click', function(event) {
  if (event.target.matches('.button')) {
    console.log('Button clicked');
  }
});

// Removing event listeners
function handleClick(event) {
  console.log('Clicked');
}
element.addEventListener('click', handleClick);
element.removeEventListener('click', handleClick);

// Common events
element.addEventListener('load', handler);
element.addEventListener('DOMContentLoaded', handler);
element.addEventListener('resize', handler);
element.addEventListener('scroll', handler);
element.addEventListener('keydown', handler);
element.addEventListener('submit', handler);
```

## Node.js Basics

### Getting Started
```bash
# Check Node.js version
node --version
node -v

# Check npm version  
npm --version

# Run JavaScript file
node app.js

# Start Node.js REPL
node

# Run with debugging
node --inspect app.js
```

### Core Modules
```javascript
// File System
const fs = require('fs');
const fsPromises = require('fs').promises;

// Path utilities
const path = require('path');

// HTTP
const http = require('http');
const https = require('https');

// URL utilities
const url = require('url');

// Query string utilities  
const querystring = require('querystring');

// Operating System
const os = require('os');

// Process
// process is a global object
console.log(process.env.NODE_ENV);
console.log(process.argv);

// Events
const EventEmitter = require('events');
```

### Module System
```javascript
// CommonJS (traditional Node.js)
// exporting
module.exports = {
  add: (a, b) => a + b,
  subtract: (a, b) => a - b
};

// Or
exports.add = (a, b) => a + b;
exports.subtract = (a, b) => a - b;

// importing
const { add, subtract } = require('./math');
const math = require('./math');

// ES Modules (modern, with .mjs or "type": "module" in package.json)
// exporting
export const add = (a, b) => a + b;
export default class Calculator { /* ... */ }

// importing  
import { add } from './math.js';
import Calculator from './calculator.js';
```

## NPM & Package Management

### Package.json
```json
{
  "name": "my-app",
  "version": "1.0.0",
  "description": "My Node.js application",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js",
    "test": "jest",
    "build": "webpack --mode production"
  },
  "dependencies": {
    "express": "^4.18.0",
    "lodash": "~4.17.21"
  },
  "devDependencies": {
    "nodemon": "^2.0.15",
    "jest": "^27.0.0"
  },
  "engines": {
    "node": ">=14.0.0"
  }
}
```

### NPM Commands
```bash
# Initialize new project
npm init
npm init -y  # Skip questions

# Install packages
npm install express              # Install and add to dependencies
npm install --save express       # Same as above
npm install --save-dev jest      # Install as dev dependency  
npm install -g nodemon          # Install globally
npm install                     # Install all dependencies from package.json

# Install specific versions
npm install express@4.18.0      # Specific version
npm install express@latest      # Latest version
npm install express@^4.0.0      # Compatible version

# Uninstall packages
npm uninstall express
npm uninstall --save-dev jest
npm uninstall -g nodemon

# List packages
npm list                        # Local packages
npm list -g                     # Global packages
npm list --depth=0             # Top level only

# Update packages
npm update                      # Update all packages
npm update express             # Update specific package
npm outdated                   # Show outdated packages

# Run scripts
npm start                       # Run start script
npm run dev                     # Run custom script
npm test                        # Run test script

# Other useful commands
npm audit                       # Check for vulnerabilities
npm audit fix                   # Fix vulnerabilities automatically
npm cache clean --force         # Clear npm cache
npm info express               # Show package information
```

### Package-lock.json
```bash
# Ensure exact versions are installed
npm ci                          # Clean install from lock file
npm install --frozen-lockfile   # Don't update lock file
```

## File System Operations

### Reading Files
```javascript
const fs = require('fs');
const fsPromises = require('fs').promises;
const path = require('path');

// Synchronous (blocking)
try {
  const data = fs.readFileSync('file.txt', 'utf8');
  console.log(data);
} catch (error) {
  console.error('Error reading file:', error);
}

// Asynchronous with callbacks
fs.readFile('file.txt', 'utf8', (error, data) => {
  if (error) {
    console.error('Error reading file:', error);
    return;
  }
  console.log(data);
});

// Asynchronous with Promises
fsPromises.readFile('file.txt', 'utf8')
  .then(data => console.log(data))
  .catch(error => console.error('Error reading file:', error));

// Asynchronous with async/await
async function readFileAsync() {
  try {
    const data = await fsPromises.readFile('file.txt', 'utf8');
    console.log(data);
  } catch (error) {
    console.error('Error reading file:', error);
  }
}
```

### Writing Files
```javascript
// Write file (overwrites existing)
fs.writeFileSync('output.txt', 'Hello World');

// Async write
fs.writeFile('output.txt', 'Hello World', 'utf8', (error) => {
  if (error) {
    console.error('Error writing file:', error);
  } else {
    console.log('File written successfully');
  }
});

// Promise-based write
await fsPromises.writeFile('output.txt', 'Hello World', 'utf8');

// Append to file
fs.appendFileSync('log.txt', 'New log entry\n');
await fsPromises.appendFile('log.txt', 'New log entry\n');
```

### Directory Operations
```javascript
// Check if file/directory exists
fs.existsSync('path/to/file');
await fsPromises.access('path/to/file'); // Throws if doesn't exist

// Get file stats
const stats = fs.statSync('file.txt');
console.log(stats.isFile());      // true
console.log(stats.isDirectory()); // false
console.log(stats.size);          // file size in bytes

// Create directory
fs.mkdirSync('new-folder');
fs.mkdirSync('nested/folder/structure', { recursive: true });

// Read directory contents
const files = fs.readdirSync('.');
const filesAsync = await fsPromises.readdir('.');

// Remove files and directories
fs.unlinkSync('file.txt');        // Delete file
fs.rmdirSync('folder');           // Delete empty directory  
fs.rmSync('folder', { recursive: true, force: true }); // Delete recursively
```

### Path Operations
```javascript
const path = require('path');

// Path manipulation
path.join('/users', 'john', 'documents', 'file.txt');
path.resolve('file.txt');                    // Absolute path
path.dirname('/users/john/file.txt');        // '/users/john'
path.basename('/users/john/file.txt');       // 'file.txt'
path.extname('/users/john/file.txt');        // '.txt'

// Parse path
const parsed = path.parse('/users/john/file.txt');
// { root: '/', dir: '/users/john', base: 'file.txt', ext: '.txt', name: 'file' }

// Path constants
console.log(__dirname);  // Current directory
console.log(__filename); // Current file path
console.log(process.cwd()); // Current working directory
```

## HTTP & Express.js

### Basic HTTP Server
```javascript
const http = require('http');
const url = require('url');

// Create server
const server = http.createServer((req, res) => {
  const parsedUrl = url.parse(req.url, true);
  const { pathname, query } = parsedUrl;
  const method = req.method;

  // Set response headers
  res.setHeader('Content-Type', 'application/json');
  res.setHeader('Access-Control-Allow-Origin', '*');

  // Handle routes
  if (pathname === '/' && method === 'GET') {
    res.statusCode = 200;
    res.end(JSON.stringify({ message: 'Hello World' }));
  } else if (pathname === '/api/users' && method === 'GET') {
    res.statusCode = 200;
    res.end(JSON.stringify({ users: [] }));
  } else {
    res.statusCode = 404;
    res.end(JSON.stringify({ error: 'Not Found' }));
  }
});

// Start server
const PORT = process.env.PORT || 3000;
server.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

### Express.js Framework
```bash
# Install Express
npm install express
npm install --save-dev nodemon  # For development
```

```javascript
const express = require('express');
const app = express();

// Middleware
app.use(express.json());                    // Parse JSON bodies
app.use(express.urlencoded({ extended: true })); // Parse form data
app.use(express.static('public'));          // Serve static files

// Custom middleware
app.use((req, res, next) => {
  console.log(`${new Date().toISOString()} - ${req.method} ${req.path}`);
  next(); // Continue to next middleware
});

// Routes
app.get('/', (req, res) => {
  res.json({ message: 'Hello World' });
});

app.get('/users/:id', (req, res) => {
  const { id } = req.params;
  const { include } = req.query;
  res.json({ id, include });
});

app.post('/users', (req, res) => {
  const userData = req.body;
  // Process user creation
  res.status(201).json({ message: 'User created', user: userData });
});

app.put('/users/:id', (req, res) => {
  const { id } = req.params;
  const updates = req.body;
  // Update user
  res.json({ message: 'User updated', id, updates });
});

app.delete('/users/:id', (req, res) => {
  const { id } = req.params;
  // Delete user
  res.status(204).end();
});

// Error handling middleware
app.use((error, req, res, next) => {
  console.error(error.stack);
  res.status(500).json({ error: 'Internal Server Error' });
});

// 404 handler
app.use((req, res) => {
  res.status(404).json({ error: 'Not Found' });
});

// Start server
const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server running on port ${PORT}`);
});
```

### Advanced Express Features
```javascript
// Router
const express = require('express');
const userRouter = express.Router();

userRouter.get('/', (req, res) => {
  res.json({ users: [] });
});

userRouter.post('/', (req, res) => {
  res.status(201).json({ message: 'User created' });
});

app.use('/api/users', userRouter);

// Middleware for authentication
const authenticate = (req, res, next) => {
  const token = req.headers.authorization;
  if (!token) {
    return res.status(401).json({ error: 'No token provided' });
  }
  // Verify token logic here
  req.user = { id: 1, name: 'John' }; // Decoded user info
  next();
};

app.get('/protected', authenticate, (req, res) => {
  res.json({ message: 'Protected route', user: req.user });
});

// CORS middleware
const cors = require('cors');
app.use(cors({
  origin: 'http://localhost:3000',
  credentials: true
}));
```

## Environment & Configuration

### Environment Variables
```javascript
// Access environment variables
const port = process.env.PORT || 3000;
const dbUrl = process.env.DATABASE_URL;
const nodeEnv = process.env.NODE_ENV || 'development';

// Using dotenv package
npm install dotenv

// .env file
PORT=3000
DATABASE_URL=mongodb://localhost:27017/myapp
API_SECRET=your-secret-key
NODE_ENV=development

// Load environment variables
require('dotenv').config();
// Or at the top of your main file
const dotenv = require('dotenv');
dotenv.config();

// Using config with different environments
// config/development.json
{
  "db": {
    "host": "localhost",
    "port": 27017
  },
  "server": {
    "port": 3000
  }
}

// Load config
const config = require('config');
const dbHost = config.get('db.host');
```

### Command Line Arguments
```javascript
// Access command line arguments
console.log(process.argv);
// node app.js --port 3000 --env production
// process.argv = ['node', '/path/to/app.js', '--port', '3000', '--env', 'production']

// Parse arguments manually
const args = process.argv.slice(2);
const port = args[args.indexOf('--port') + 1];

// Using commander package for complex CLI
const { program } = require('commander');

program
  .option('-p, --port <number>', 'port number', '3000')
  .option('-e, --env <string>', 'environment', 'development');

program.parse();
const options = program.opts();
console.log(options.port, options.env);
```

## Testing

### Jest Testing Framework
```bash
# Install Jest
npm install --save-dev jest

# Package.json script
{
  "scripts": {
    "test": "jest",
    "test:watch": "jest --watch",
    "test:coverage": "jest --coverage"
  }
}
```

```javascript
// math.js
function add(a, b) {
  return a + b;
}

function subtract(a, b) {
  return a - b;
}

module.exports = { add, subtract };

// math.test.js
const { add, subtract } = require('./math');

describe('Math functions', () => {
  test('adds 1 + 2 to equal 3', () => {
    expect(add(1, 2)).toBe(3);
  });

  test('subtracts 5 - 2 to equal 3', () => {
    expect(subtract(5, 2)).toBe(3);
  });

  test('handles edge cases', () => {
    expect(add(0, 0)).toBe(0);
    expect(add(-1, 1)).toBe(0);
    expect(() => add('a', 'b')).toThrow(); // If function validates input
  });
});

// Async testing
async function fetchUser(id) {
  const response = await fetch(`/api/users/${id}`);
  return response.json();
}

test('fetches user data', async () => {
  const user = await fetchUser(1);
  expect(user).toHaveProperty('id', 1);
  expect(user).toHaveProperty('name');
});

// Mock functions
const mockCallback = jest.fn();
mockCallback.mockReturnValue(42);
expect(mockCallback()).toBe(42);
expect(mockCallback).toHaveBeenCalled();
```

### Testing Express Apps
```javascript
// app.test.js
const request = require('supertest');
const app = require('./app'); // Your Express app

describe('API endpoints', () => {
  test('GET / returns hello message', async () => {
    const response = await request(app)
      .get('/')
      .expect(200)
      .expect('Content-Type', /json/);
    
    expect(response.body).toEqual({ message: 'Hello World' });
  });

  test('POST /users creates a user', async () => {
    const userData = { name: 'John', email: 'john@example.com' };
    
    const response = await request(app)
      .post('/users')
      .send(userData)
      .expect(201);
    
    expect(response.body.user).toMatchObject(userData);
  });
});
```

## Best Practices

### Code Organization
```javascript
// Use consistent naming conventions
const userName = 'john';           // camelCase for variables
const MAX_RETRY_COUNT = 3;         // UPPERCASE for constants
const UserService = require('./UserService'); // PascalCase for classes

// File and folder structure
project/
├── src/
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── middleware/
│   ├── services/
│   └── utils/
├── tests/
├── config/
└── public/

// Use modules for organization
// userController.js
exports.getUser = async (req, res) => {
  // Implementation
};

exports.createUser = async (req, res) => {
  // Implementation  
};

// Avoid deep nesting
// Bad
if (user) {
  if (user.profile) {
    if (user.profile.address) {
      return user.profile.address.city;
    }
  }
}

// Good
return user?.profile?.address?.city || 'Unknown';
```

### Error Handling
```javascript
// Always handle errors
async function riskyOperation() {
  try {
    const result = await someAsyncOperation();
    return result;
  } catch (error) {
    console.error('Operation failed:', error.message);
    throw new Error(`Failed to complete operation: ${error.message}`);
  }
}

// Custom error classes
class ValidationError extends Error {
  constructor(message) {
    super(message);
    this.name = 'ValidationError';
  }
}

class NotFoundError extends Error {
  constructor(resource) {
    super(`${resource} not found`);
    this.name = 'NotFoundError';
  }
}

// Global error handlers for Express
app.use((error, req, res, next) => {
  if (error instanceof ValidationError) {
    return res.status(400).json({ error: error.message });
  }
  
  if (error instanceof NotFoundError) {
    return res.status(404).json({ error: error.message });
  }
  
  console.error('Unexpected error:', error);
  res.status(500).json({ error: 'Internal server error' });
});
```

### Performance Tips
```javascript
// Use const and let instead of var
const immutableValue = 'constant';
let mutableValue = 'variable';

// Prefer array methods over loops when possible
const doubled = numbers.map(n => n * 2);
const evens = numbers.filter(n => n % 2 === 0);

// Debounce expensive operations
function debounce(func, delay) {
  let timeoutId;
  return function (...args) {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => func.apply(this, args), delay);
  };
}

const debouncedSearch = debounce(searchFunction, 300);

// Use object destructuring for cleaner code
// Instead of
function processUser(user) {
  const name = user.name;
  const email = user.email;
  const age = user.age;
}

// Use
function processUser({ name, email, age }) {
  // Implementation
}

// Cache expensive computations
const memoize = (fn) => {
  const cache = new Map();
  return (...args) => {
    const key = JSON.stringify(args);
    if (cache.has(key)) {
      return cache.get(key);
    }
    const result = fn(...args);
    cache.set(key, result);
    return result;
  };
};

const expensiveFunction = memoize((n) => {
  // Expensive computation
  return n * n;
});
```

### Security Best Practices
```javascript
// Input validation
const validator = require('validator');

function validateEmail(email) {
  return validator.isEmail(email);
}

function sanitizeInput(input) {
  return validator.escape(input); // Escape HTML entities
}

// Environment variables for secrets
const JWT_SECRET = process.env.JWT_SECRET;
const API_KEY = process.env.API_KEY;

// Rate limiting
const rateLimit = require('express-rate-limit');

const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100 // limit each IP to 100 requests per windowMs
});

app.use(limiter);

// Helmet for security headers
const helmet = require('helmet');
app.use(helmet());

// HTTPS in production
if (process.env.NODE_ENV === 'production') {
  app.use((req, res, next) => {
    if (req.header('x-forwarded-proto') !== 'https') {
      res.redirect(`https://${req.header('host')}${req.url}`);
    } else {
      next();
    }
  });
}
```

## Troubleshooting

### Common Issues

#### Module Not Found
```bash
# Error: Cannot find module './myModule'
# Solutions:
1. Check file path and extension
2. Ensure the file exists
3. Check case sensitivity (Linux/Mac)
4. Clear node_modules and reinstall
npm install

# For ES modules, include file extension
import { myFunction } from './myModule.js'; // Note the .js
```

#### Port Already in Use
```bash
# Error: EADDRINUSE: address already in use :::3000
# Solutions:

# Find process using the port
lsof -ti:3000
netstat -tulpn | grep 3000

# Kill the process
kill -9 $(lsof -ti:3000)

# Or use a different port
const PORT = process.env.PORT || 3001;
```

#### Memory Leaks
```javascript
// Common causes and solutions

// 1. Event listeners not removed
// Bad
element.addEventListener('click', handler);

// Good  
element.addEventListener('click', handler);
// Later, when element is no longer needed:
element.removeEventListener('click', handler);

// 2. Timers not cleared
// Bad
setInterval(() => {
  // Some operation
}, 1000);

// Good
const intervalId = setInterval(() => {
  // Some operation  
}, 1000);
// Later:
clearInterval(intervalId);

// 3. Global variables
// Avoid creating unnecessary global variables
// Use modules and proper scoping

// Monitor memory usage
process.memoryUsage();
// { rss: 123456, heapUsed: 789012, heapTotal: 1234567, external: 8901 }
```

#### Debugging Techniques
```javascript
// Console debugging
console.log('Debug info:', variable);
console.table(arrayOfObjects);
console.time('operation');
// ... code to measure
console.timeEnd('operation');

// Node.js debugger
node --inspect app.js
// Then open Chrome DevTools

// VS Code debugging (launch.json)
{
  "type": "node",
  "request": "launch",
  "name": "Launch Program",
  "program": "${workspaceFolder}/app.js"
}

// Using debug module
const debug = require('debug')('app:server');
debug('Server starting on port %d', port);

# Set DEBUG environment variable
DEBUG=app:* node app.js
```

#### Async/Await Issues
```javascript
// Common mistake: not awaiting async functions
// Bad
async function badExample() {
  fetchData(); // Missing await!
  console.log('This runs before fetchData completes');
}

// Good
async function goodExample() {
  await fetchData();
  console.log('This runs after fetchData completes');
}

// Handling multiple async operations
// Sequential (slower)
const user = await fetchUser(id);
const posts = await fetchPosts(user.id);

// Parallel (faster)
const [user, posts] = await Promise.all([
  fetchUser(id),
  fetchPosts(id)
]);

// Error handling in async functions
async function properErrorHandling() {
  try {
    const result = await riskyOperation();
    return result;
  } catch (error) {
    console.error('Error occurred:', error);
    throw error; // Re-throw if needed
  }
}
```

#### Package Version Conflicts
```bash
# Check for outdated packages
npm outdated

# Update packages
npm update

# Fix vulnerabilities
npm audit
npm audit fix

# Clear cache if issues persist
npm cache clean --force

# Delete node_modules and reinstall
rm -rf node_modules package-lock.json
npm install

# Check for duplicate packages
npm ls --depth=0
```

#### Performance Issues
```javascript
// Profile performance
console.time('slow-operation');
// ... slow code
console.timeEnd('slow-operation');

// Use Node.js profiler
node --prof app.js
# Run your app, then:
node --prof-process isolate-0x... > processed.txt

// Memory profiling
const v8 = require('v8');
const fs = require('fs');

// Take heap snapshot
const heapSnapshot = v8.writeHeapSnapshot();
console.log('Heap snapshot written to', heapSnapshot);

// Monitor event loop
const { monitorEventLoopDelay } = require('perf_hooks');
const h = monitorEventLoopDelay({ resolution: 20 });
h.enable();
setTimeout(() => {
  h.disable();
  console.log(h.mean); // Event loop delay
}, 10000);
```