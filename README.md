# Best Practices I learned

A list of best practices with explanation which I learned at work from my senior developers and by reading recources. The best practices are divided to general code writing best practices and API best practices. More will be added as we go.

*- API GUY*

## API Best Practices
### Single Purpose Endpoints
Each endpoint should serve a single purpose. If a an endpoint serves multiple purposes it means you should divide it to multiple endpoints.

Example:

Bad
```
// Single endpoint for getting users or a user
GET /api/user
```

Good

```
//Separated endpoints for getting multiple user and a single user

// Get multiple users
GET /api/user

// Get a single user by id
Get /api/user/:id
```

### Handle Undefined Reference
Use logical 'or' to handle undefined data specially when using the data to call other functions. You may handle the empty string in the recieving function
```
// Get user object
const user = getUser(userId);

// Store email in variable
const userEmail = user.email;

// Call a function using 
await storeEmail(userEmail);           

// Causes Reference error
                
```

Good

```
// Get user object
const user = getUser(userId);

// store email or set to empty string if undefined
const userEmail = user.email || '';

// Call a function using the 
await storeEmail(userEmail);           
```

### Validate Requests
Perform validation on the data sent on request instead of checking it inside a function later.

Example:

Bad

```
module.exports = async (req, res) => {
  // Check if email is defined
  if (req.param('email)) {
    // Do stuff
  }
}

```

Good
```
// Check if email is sent in request
req.check('email').notEmpty();
// Do Stuff
```

### Prefer Soft Delete
Choose soft deleting resources, specially resources that are useful for the system or user might want restore.

Example:

Bad
```
User.detroyOne({ id })
```


Good
```
User.updateOne({ id }).set({isDeleted: true})
```

### Use Modules to Avoid Reptition
If the exact same code is being repeated multiple places or is being slightly modified, then it should be made to its own module.
Instead of copy pasting same functions or slightly modifying the functions create a general service (module) from it and call it when required. For instance for using custom format date format, custom created file management, etc.

### Store Shared Variables in A Config File
If the same variable is used in or will be used in different endpoints then it should be stored in a custom config file where all endpoints call it. This will avoid reptition and confusion but most importantly makes the code scalable.

### Use Proper REST Method
When creating APIs use proper REST methods for each enpoint. For Creating a user use POST, for deleting a resource DELETE, and etc.

Example:

Bad

```
// Delete a user using POST
POST /api/deleteuser/:id

```

Good

```
// Delete a user using proper DELETE method

DELETE /api/user/:id
```

## General Best Practices

### Prefer Async
Write asynchronous functions when possible to improve performance.

### Avoid Nesting
Use return statements to avoid nesting if-else statements as much as possible.

### Prefer Template Literals
User template literals instead of string concatination

Example:

Bad

```
const name = 'Jack'
const message = 'Welcome to app, ' + name

```

Good
```
const name = 'Jack'
const message = `Welcome to app, ${name}`

```




