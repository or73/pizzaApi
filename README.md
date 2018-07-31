API for a Pizza-Delivery Company
=
---

## Table of Contents

1. [Server Ports](#server-ports)

2. [Folders Structure](#folders-structure)

3. **[Controllers and Objects](#controllers-and-objects-structures)** ⇒ | [<code>User</code>](#user) | [<code>Menu</code>](#item) | [<code>Order</code>](#order) | [<code>Shopping Cart</code>](#shoppingCart) |	
4. **[Menu's Methods](#menus-methods)** ⇒ | [<code>POST</code>](#menu-post) | [<code>GET</code>](#menu-get) | [<code>PUT</code>](#menu-put) | [<code>DELETE</code>](#menu-delete) |

5. **[Order's Methods](#orders-methods)** ⇒ | [<code>POST</code>](#order-post) | [<code>GET</code>](#order-get) |

6. **[ShoppingCart's Methods](#shoppingcart-methods)** ⇒ | [<code>POST</code>](#shoppingcart-post) | [<code>GET</code>](#shoppingcart-get) | [<code>PUT</code>](#shoppingcart-put) | [<code>DELETE</code>](#shoppingcart-delete) |

7. **[Token's Methods](#tokens-methods)** ⇒ | [<code>POST</code>](#token-post)   [<code>GET</code>](#token-get) | [<code>PUT</code>](#token-put) | [<code>DELETE</code>](#token-delete) |

8. **[User's Methods](#users-methods)** ⇒ | [<code>POST</code>](#user-post) | [<code>GET</code>](#user-get) | [<code>PUT</code>](#user-put) | [<code>DELETE</code>](#user-delete) |

---

# Server-Ports  

| Protocol   | Port          | Port             |
| ---        | ---           | ---              |
| http       | 3000          | 5000             |
| https      | 3001          | 5001             |
| **`mode`** | **`Staging`** | **`Production`** |
---

# Folders-Structure  
    
* [config](https://github.com/or73/apipizzacompany/tree/master/config)    
    * [config.js](https://github.com/or73/apipizzacompany/blob/master/config/config.js)   
* [controllers](https://github.com/or73/apipizzacompany/tree/master/controllers)
    * [menu.js](https://github.com/or73/apipizzacompany/blob/master/controllers/menu.js)
    * [order.js]()
    * [shoppingCart.js]()
    * [tokens.js](https://github.com/or73/apipizzacompany/blob/master/controllers/tokens.js)
    * [users.js](https://github.com/or73/apipizzacompany/blob/master/controllers/users.js)
* [lib](https://github.com/or73/apipizzacompany/tree/master/lib)
    * [authentication.js](https://github.com/or73/apipizzacompany/blob/master/lib/authentication.js)
    * [helpers.js](https://github.com/or73/apipizzacompany/blob/master/lib/helpers.js)
    * [router.js](https://github.com/or73/apipizzacompany/blob/master/lib/router.js)
* [app.js](https://github.com/or73/apipizzacompany/blob/master/app.js)

---   
# Database / Files Structure and Relations
![Structure and Relations](https://github.com/or73/pizzaApi/blob/master/apiPizzaDeliveryDBStructure_md.png)

---

# Controllers-and-Objects-Structures   

## Menu   

**Contains several items, and each item structure is**:  

```javascript
{
	id:	"itemId",
	name: "item name",
	price: 123
}
```   
| Field | Type   |
|---    | ---    |
| id    | string |
| name  | string |
| price | number |

## Order   

```javascript
{
   id,
   items,
   iat,
   price,
   paymentProcessed
}
```   
| Field            | Type    |
|---               | ---     |
| id               | string  |
| items            | array   |
| iat              | string  |
| price            | number  |
| paymentProcessed | boolean |

## Shopping-Cart   

```javascript
{
  id,
  items,
  iat,
  price,
  paymenProcessed
}
```
| Field            | Type    |
|---               | ---     |
| id               | string  |
| items            | array   |
| price            | number  |
| paymentProcessed | boolean |

## User  

```javascript
{
	"name": "user name ",   
	"email": "valid@email.com",
	"address": "must be a valid string",
	"password": "must be a valid string"
}
```   
| Field    | Type   |
|---       | ---    |
| name     | string |
| email    | string |
| address  | string |
| password | string |

## Token   

```javascript
{
	email: "valid@usermail.com",
	tokenId: xxxxxxxxxxx,
	expires: 123456
}
```   
| Field   | Type   |
|---      | ---    |
| email   | string |
| tokenId | string |
| expires | number |

---

# Menus-Methods 
## menu-POST
**(Request that the resource at the URI do something with the provided entity)**       
      
| Path   | Parameters            | Headers | e.g.                       |
| ---    | ---                   | ---     | ---                        |
| /menus | name **`(required)`** | None    | http://localhos:3000/menus |
|        | price**`(required)`** |         |                            |
   
   
### menu-post-Response   
Stores information of required token   

```javascript
{
    statusCode: 200,
    message: 'Item created successfully',
    data: {
       id,
       price,
       name
    }
}
```

### menu-post-Errors    
   
| Error | Parameters                                            |
| ---   | ---                                                   |
| 404   | No data available. Item was not created               |
| 412   | Invalid argument.  Missing or invalid required fields |
| 451   | File or directory already exists                      |

---  
      
## menu-GET
**(Retrieve information)**
If the item exists, then returns all information associated with item, except the id.  Otherwise, returns an error message.

| Path             | Parameters            | Headers | e.g.                                      |
| ---              | ---                   | ---     | ---                                       |
| /menus?id=string | name **`(required)`** | None    | http://localhost:3000/menus?name=itemName |
| /menus?all       | None                  | None    | http://localhost:3000/menus?all           |
   
   
### menu-get-Response   
**For path: /items?id=itemId**   (Retrieves information of a specific item)   

```javascript
{
    statusCode: 200,
    message: 'Item fetched successfully',
    data: {
       id,
       price,
       name
    }
}
```   

**For path /items?all**   (Retrieves a list of all items that exist, but the query must contains a valid token or it returns an error message)   

```javascript
{
   statusCode: 200,
   message: 'List of menu items fetched successfully'
   data: {
          items: [
                 {
                    id,
                    price,
                    name
                  }, {
                    id,
                    price,
                    name
                  }
          ]
   }
}
```

### menu-get-Errors    
      
| Error | Parameters                                            |
| ---   | ---                                                   |
| 404   | No such file or directory.  Menu item does not exist  |
| 404   | No data available.  Menu items list was not fetched   |
| 412   | Invalid argument.  Missing or invalid required fields |

---   

## menu-PUT
**(Store an entity at a URI)**
Updates 'name' and 'price' fields of an item.  A valid id must be send or an error message will be return.

| Path             | Parameters             |  Headers                 | e.g.                                  |
| ---              | ---                    | ---                      | ---                                   |
| /menus?id=string | name **`(required)`**  | email **`(required)`**   | http://localhost:3000/menus?id=orange |
|                  | price **`(required)`** | tokenId **`(required)`** |                                       |

### menu-put-Response
```javascript
{
   statusCode: 200,
   message: 'Item of menu updated successfully',
   data: {
      id,
      price,
      name
   }
}
```   

### menu-put-Errors    
      
| Error | Parameters                                                                         |
| ---   | ---                                                                                |
| 403   | Permission denied... insufficient permissions.  A valid token or email is required |
| 403   | Permission denied... Insufficient permissions                                      |
| 404   | No data available.  Token not found                                                |
| 404   | No data available.  Item was not found                                             |
| 404   | No data available.  Item was not updated                                           |
| 412   | Invalid argument.  Missing or invalid required fields.                             |
| 428   | Timer expired.   Token expired                                                     |

---   

## menu-DELETE
**(Request that a resource be removed)**   
Remove the item provided, and update all menus and user's cartItems which contains provided item and remove it.

| Path             | Parameters |  Headers               | e.g.                                  |
| ---              | ---        | ---                    | ---                                   |
| /menus?id=string | None       | token **`(required)`** | http://localhost:3000/menus?id=itemId |
|                  |            | email **`(required)`** |                                       |

### menu-delete-Response
```javascript
{
   statusCode: 200,
   message: 'Item deleted successfully',
   data: { }
}
```   

### menu-delete-Errors    
      
| Error | Parameters                                                           |
| ---   | ---                                                                  |
| 403   | Permission denied... insufficiente permissions.  Unauthorized access |
| 404   | No such file or directory.  Item could not be deleted                |
| 404   | No data available.  Token not found                                  |
| 412   | Invalid argument.  Missing or invalid required fields                |
| 428   | Timer expired.   Token expired                                       |

---  

# ShoppingCart-Methods 
## shoppingCart-POST
**(Request that the resource at the URI do something with the provided entity)**       
      
| Path                                                 | Parameters            | Headers                | e.g.                               |
| ---                                                  | ---                   | ---                    | ---                                |
| /shoppingCarts                                       | None                  | email **`(required)`** | http://localhos:3000/shoppingCarts |
|                                                      |                       | token **`(required)`** |                                    |
| /shoppingCarts?item=<item Name>&qtty=<integer value> | item **`(required)`** | email **`(required)`** | http://localhost:3000/shoppingCarts?item=tomatoe&qtty=10 |
|                                                      | qtty **`(required)`** | token **`(required)`** |                                    |
   
   
### shoppingCart-post-Response   
Stores information of required token   
   
**For path: /shoppingCarts**
```javascript
{
    statusCode: 200,
    message: 'Shopping Cart created successfully',
    data: {
       id,
       price,
       name
    }
}
```

**For path: /shoppingCarts?item=<item Name>&qtty=<integer value>**
```javascript
{
    statusCode: 200,
    message: 'Product added to Shopping Cart, successfully',
    data: {
       id,
       price,
       name
    }
}
```

### shoppingCart-post-Errors    
   
| Error | Parameters                                                                        |
| ---   | ---                                                                               |
| 403   | Permission denied... insufficient permissions                                     |
| 404   | No data available.  Token not found                                               |
| 404   | Required file does not exist                                                      |
| 404   | Shopping cart was not created                                                      |
| 412   | Invalid argument.  Missing or invalid required fields                             |
| 428   | Timer expired.  Token expired                                                     |
| 451   | File or directory already exist                                                   |
| 451   | File or directory already exist.  Item already exist in carg... use update option |

---  
      
## shoppingCart-GET
**(Retrieve information)**
If the item exists, then returns all information associated with item, except the id.  Otherwise, returns an error message.

| Path                     | Parameters            | Headers | e.g.                                              |
| ---                      | ---                   | ---     | ---                                               |
| /shoppingCarts?id=string | name **`(required)`** | None    | http://localhost:3000/shoppingCarts?name=itemName |
| /shoppingCarts?all       | None                  | None    | http://localhost:3000/shoppingCarts?all           |
   
   
### shoppingCart-get-Response   
**For path: /shoppingCarts?id=itemId**   (Retrieves information of a specific item)   

```javascript
{
    statusCode: 200,
    message: 'Shopping Cart Item fetched successfully',
    data: {
       id,
       price,
       name
    }
}
```   

**For path /shoppingCarts?all**   (Retrieves a list of all items that exist, but the query must contains a valid token or it returns an error message)   

```javascript
{
   statusCode: 200,
   message: 'Shopping Cart list fetched successfully'
   data: {
          items: [
                 {
                    id,
                    price,
                    name
                  }, {
                    id,
                    price,
                    name
                  }, ...
          ]
   }
}
```

### shoppingCart-get-Errors    
      
| Error | Parameters                                            |
| ---   | ---                                                   |
| 403   | Permission denied.... insufficient permissions        |
| 404   | No such file or directory.  Menu item does not exist  |
| 404   | No data available.  Menu items list was not fetched   |
| 412   | Invalid argument.  Missing or invalid required fields |
| 428   | Timer expired.  Token expired                         |

---   

## shoppingCart-PUT
**(Store an entity at a URI)**
Updates 'name' and 'price' fields of an item.  A valid id must be send or an error message will be return.

| Path                     | Parameters                 |  Headers                 | e.g.                                          |
| ---                      | ---                        | ---                      | ---                                           |
| /shoppingCarts?id=string | Array containing objects:  | email **`(required)`**   | http://localhost:3000/shoppingCarts?id=orange |
|                          |  [ {                       | tokenId **`(required)`** |                                               |
|                          |      name **`(required)`** |                          |                                               |
|                          |      qtty **`(required)`** |                          |                                               |
|                          |    }, ..., {               |                          |                                               |
|                          |      name **`(required)`** |                          |                                               |
|                          |      qtty **`(required)`** |                          |                                               |
|                          |  } ]                       |                          |                                               |

### shoppingCart-put-Response
```javascript
{
   statusCode: 201,
   message: 'Shopping Cart was updated successfully',
   data: {
      id,
      email,
      items: [ {
                 name,
                 price,
                 qtty,
                 total
               }, ..., {
                 name,
                 price,
                 qtty,
                 total
               }
             ]
   }
}
```   

### shoppingCart-put-Errors    
      
| Error | Parameters                                                                         |
| ---   | ---                                                                                |
| 403   | Permission denied... insufficient permissions.  A valid token or email is required |
| 403   | Permission denied... Insufficient permissions                                      |
| 404   | No data available.  Token not found                                                |
| 404   | No such file or directory.                                                         |
| 404   | No data available.  Item was not found                                             |
| 404   | No data available.  Item was not updated                                           |
| 412   | Invalid argument.  Missing or invalid required fields.                             |
| 428   | Timer expired.   Token expired                                                     |

---   

## shoppingCart-DELETE
**(Request that a resource be removed)**   
Remove the item provided, and update all menus and user's cartItems which contains provided item and remove it.

| Path                     | Parameters           |  Headers               | e.g.                                          |
| ---                      | ---                  | ---                    | ---                                           |
| /shoppingCarts?id=itemId | None                 | token **`(required)`** | http://localhost:3000/shoppingCarts?id=itemId |
|                          |                      | email **`(required)`** |                                               |
| /shoppingCarts?id=itemId | items [ item1, ... ] | token **`(required)`** | http://localhost:3000/shoppingCarts?id=itemId |
|                          |                      | email **`(required)`** |                                               |

### shoppingCart-delete-Response
**Delete a Shopping Cart: /shoppingCarts?id=itemId**
```javascript
{
   statusCode: 200,
   message: 'Shopping Cart deleted successfully',
   data: { }
}
```   
**Delete items from a Shopping Cart: For /shopingCarts?id=itemId**
```javascript
{
   statusCode: 200,
   message: 'Shopping Cart items deleted successfully',
   data: { 
      id,
      mail,
      items
   }
}
```   

### shoppingCart-delete-Errors    
      
| Error | Parameters                                                           |
| ---   | ---                                                                  |
| 403   | Permission denied... insufficiente permissions.  Unauthorized access |
| 404   | No such file or directory.  Item could not be deleted                |
| 404   | No data available.  Token not found                                  |
| 406   | No items found in Shopping Cart to delete                            |
| 412   | Invalid argument.  Missing or invalid required fields                |
| 428   | Timer expired.   Token expired                                       |

--- 

# Orders-Methods 
## order-POST
**(Request that the resource at the URI do something with the provided entity)**   
Will create an order with the items on cart    
      
| Path    | Parameters | Headers                    | e.g.                        |
| ---     | ---        | ---                        | ---                         |
| /orders | None       | tokenId **`(required)`** | http://localhos:3000/orders |
   
   
### order-post-Response   

```javascript
{
    statusCode: 200,
    message: 'Order created',
    data: {
       id,
       items,
       iat,
       price,
       paymentProcessed
    }
}
```

### order-post-Errors    
   
| Error | Parameters                                   |
| ---   | ---                                          |
| 400   | Required fields missing or they were invalid |
| 400   | Payment not processed                        |
| 400   | No items on cart to place an order           |
| 400   | Order already exists                         |
| 500   | Insufficient permissions                     |

---  
      
## order-GET
**(Retrieve information)**
If the cart exists, then returns all information associated with cart.  Otherwise, returns an error message.

| Path    | Parameters            | Headers                    | e.g.                                    |
| ---     | ---                   | ---                        | ---                                     |
| /orders | id **`(required)`** | tokenId **`(required)`** | http://localhost:3000/orders/id=orderId |
   
   
### order-get-Response   

```javascript
{
    statusCode: 200,
    message: 'Order fetched correctly',
    data: {
       id,
       items,
       iat,
       price,
       paymentProcessed
    }
}
```   

### order-get-Errors    
      
| Error | Parameters                                   |
| ---   | ---                                          |
| 400   | Required fields missing or they were invalid |
| 403   | Unauthorized access                          |
| 404   | Order not found                              |
| 500   | Insufficient permissions                     |

---   

# Tokens-Methods  
## token-POST   
**(Request that the resource at the URI do something with the provided entity)**       
      
| Path    | Parameters              | Headers | e.g.                         |
| ---     | ---                     | ---     | ---                          |
| /tokens | email **`required`**    | None    | http://localhost:3000/tokens |
|         | password **`required`** |         |                              |
   
   
### token-post-Response   
Stores information of required token   
   
```javascript
{
    statusCode: 200,
    message: 'User logged in',
    data: {
       id,
       email,
       expires
    }
}
```
   
### token-post-Errors    
   
| Error | Parameters                                               |
| ---   | ---                                                      |
| 400   | Token was not created                                    |
| 404   | No data available.  Token was not created                |
| 404   | No such file or directory.  Required file does not exist |
| 412   | Invalid argument.  Missing or invalid required fields    |
| 451   | File or directory already exists                         |

---  
      
## token-GET   
**(Retrieve information)**   
If the token exists, then returns all information associated with token, except the id.  Otherwise, returns an error message.   
   
| Path              | Parameters               |  Headers | e.g.                                    |
| ---               | ---                      | ---      | ---                                     |
| /tokens?id=string | tokenId **`required`**   | None     | http://localhost:3000/tokens?id=tokenId |
| /tokens?all       | tokenId **`(required)`** | None     | http://localhost:3000/users?all         |
   
   
### token-get-Response    
**For path: /tokens?id=tokenId**   (Retrieves information of a specific token)   
   
```javascript
{
    statusCode: 200,
    message: 'Token fetched successfully',
    data: {
       id,
       email,
       expires
    }
}
```   
   
**For path /tokens?all**   (Retrieves a list of all tokens that exist, but the query must contains a valid token or it returns an error message)   
   
```javascript
{
   statusCode: 200,
   message: 'Tokens list fetched successfully'
   data: {
          items: [
                 {                         
                         email,
                         expires
                  }, {
                         email,
                         expires
                  }
          ]
   }
}
```   
   
### token-get-Errors    
      
| Error | Parameters                                               |
| ---   | ---                                                      |
| 404   | No data available. Token was not fetched                 |
| 404   | No such file or directory.  Required file does not exist |
| 404   | No data available. Token list was not fetched            |
| 412   | Invalid argument.  Missing or invalid required fields    |

---      
   
## token-PUT
**(Store an entity at a URI)**   
Updates 'expires' field of a token, resets it and assigns it a new life time.  A valid token must be send or an error message will be return.   
   
| Path              | Parameters |  Headers | e.g.                                    |
| ---               | ---        | ---      | ---                                     |
| /tokens?id=string | expires    | None     | http://localhost:3000/tokens?id=tokenId |   
   
> Resets 'expires' field, and assigns it a new life time.   
   
### token-put-Response   

```javascript
{
   statusCode: 200,
   message: 'Token time has been reset successfully',
   data: {
      id,
      email,
      expires
   }
}
```     
   
### token-put-Errors    
      
| Error | Parameters                                                              |
| ---   | ---                                                                     |
| 403   | Permission denied... Insufficient permissions                           |
| 403   | Permission denied... Insufficient permissions. Token time was not reset |
| 404   | No data available.  Token was not found                                 |
| 404   | No such file or directory.  Required file does not exist                |
   
---      
   
## token-DELETE   
**(Request that a resource be removed)**     
   
| Path              | Parameters |  Headers | e.g.                                    |
| ---               | ---        | ---      | ---                                     |
| /tokens?id=string | None       | None     | http://localhost:3000/tokens?id=tokenId |   
   
### token-delete-Response   
   
```javascript
{
   statusCode: 200,
   message: 'Token deleted successfully',
   data: { }
}
```      
   
### token-delete-Errors    
      
| Error | Parameters                                            |
| ---   | ---                                                   |
| 403   | Permission denied... Insufficient permissions         |
| 404   | No data available. Toke, was not found                |
| 404   | No such file or directory                             |
| 405   | Operation not permitted.  Tokes has not been deleted  |
| 412   | Invalid argument.  Missing or invalid required fields |
   
---   

# Users-Methods  

## user-POST   

**(Request that the resource at the URI do something with the provided entity)**       

      
| Path   | Parameters                | Headers | e.g.                        |
| ---    | ---                       | ---     | ---                         |
| /users | email **`(required)`**    | None    | http://localhost:3000/users |
|        | name **`(required)`**     |         |                             |
|        | password **`(required)`** |         |                             |
|        | address **`(required)`**  |         |                             |
  
### user-post-Response   

Stores information of required user   

```javascript
{
    statusCode: 200,
    message: 'User created successfully',
    data: {
       email,
       address,
       name
    }
}
```

   
### user-post-Errors    
   
| Error | Parameters                                               |
| ---   | ---                                                      |
| 400   | Token was not created                                    |
| 404   | No data available.  Token was not created                |
| 404   | No data available.  User was not created                 |
| 404   | No such file or directory.  Required file does not exist |
| 412   | Invalid argument.  Missing or invalid required fields    |
| 451   | File or directory already exists                         |
   
---     
      
## user-GET   
**(Retrieve information)**   
If the mail exists, then returns all information associated with user, except the password.  Otherwise, returns an error message.   
   
| Path                           | Parameters             |  Headers                 | e.g.                                                |
| ---                            | ---                    | ---                      | ---                                                 |
| /users?mail=some@validmail.com | email **`required`**   | tokenId **`(required)`** | http://localhost:3000/users?mail=some@validmail.com |
| /users?all                     |  None                  | tokenId **`(required)`** | http://localhost:3000/users?all                     |
|                                |                        | email **`(required)`**   |
   
   
### user-get-Response   
**For path: /users?email=some@validmail.com**   (Retrieves information of a specific user)    
   
```javascript
{
    statusCode: 200,
    message: 'User fetched correctly',
    data: {
       email,
       address,
       name,
    }
}
```   

**For path /users?all**   (Retrieves a list of all users that exist, but the query must contains a valid token and its email, or it returns an error message)      

```javascript
{
   statusCode: 200,
   message: 'Returning all available users data'
   data: {
          items: [
                 {
                         email,
                         address,
                         name,
                  }, {
                         email,
                         address,
                         name,
                  }
          ]
   }
}
```

### user-get-Errors    
      
| Error | Parameters                                                                              |
| ---   | ---                                                                                     |
| 403   | Permission denied... Insufficient permissions.  Some provided values were not validated |
| 403   | Permission denied... Insufficient permissions                                           |
| 404   | No data available.  User was not fetched                                                |
| 404   | No data available.  Token not found                                                     |
| 404   | No data available.  User list was not fetched                                           |
| 404   | No such file or directory.  Required file does not exist                                |
| 412   | Invalid argument.  Required fields missing or invalid                                   |
| 428   | Timer expired.   Token expired                                                          |
   
---      
   
## user-PUT  
**(Store an entity at a URI)**   
Updates all or some fields of a user.  A valid token must be send or an error message will be return.   
   
| Path                            | Parameters |  Headers                 | e.g.                                                  |
| ---                             | ---        | ---                      | ---                                                   |
| /users?email=some@validmail.com | email      | tokenId **`(required)`** | http://localhost:3000/users?email=some@validemail.com |
|                                 | name       |                          |                                                       |
|                                 | address    |                          |                                                       |   

> At least one field (parameter) must be provided, or returns an error message.   

   

### user-put-Response   

```javascript
{
   statusCode: 200,
   message: 'User updated successfully',
   data: {
      email,
      address,
      name
   }
}
```   
   
### user-put-Errors    
      
| Error | Parameters                                                        |
| ---   | ---                                                               |
| 403   | Permission denied... Insufficient permissions.  Email is required |
| 403   | Permission denied... Insufficient permissions.  Token is required |
| 403   | Permission denied... Insufficient permissions                     |
| 403   | Permission denied... Insufficient permissions                     |
| 404   | No data available.  User not found                                |
| 404   | No data available.  User has not been updated                     |
| 404   | No data available.  Token not found                               |
| 404   | No such file or directory.  Required file does not exist          |
| 405   | Operation not permitted.  Email cannot be updated                 |
| 412   | Invalid argument.  Missing or invalid required fields             |
| 428   | Timer expired.   Token expired                                    |
   
---      
   
## user-DELETE   
**(Request that a resource be removed)**   
   
| Path                            | Parameters |  Headers                 | e.g.                                                  |
| ---                             | ---        | ---                      | ---                                                   |
| /users?email=some@validmail.com | None       | tokenId **`(required)`** | http://localhost:3000/users?email=some@validemail.com |   

### user-delete-Response   

```javascript
{
   statusCode: 200,
   message: 'User deleted successfully',
   data: { }
}
```   
   
### user-delete-Errors    
      
| Error | Parameters                                                                |
| ---   | ---                                                                       |
| 403   | Permission denied... Insufficient permissions                             |
| 404   | No data available.  Token not found                                       |
| 404   | No such file or directory                                                 |
| 405   | Operation not permitted. User associated with email has not been deleted  |
| 405   | Operation not permitted. Token associated with email has not been deleted |
| 405   | Operation not permitted. User associated with email does not exist        |
| 412   | Invalid argument.  Missing or invalid required fields                     |
| 428   | Timer expired.   Token expired                                                          |

---   
