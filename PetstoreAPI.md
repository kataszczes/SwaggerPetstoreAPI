- [Introduction](#introduction)
  - [Store](#store)
    - [GET/store/inventory](#getstoreinventory)
    - [GET/store/order/{orderID}](#getstoreorderorderid)
    - [POST/store/order](#poststoreorder)
    - [DELETE/store/order/{orderID}](#deletestoreorderorderid)
    - [Response schema (Properties)](#response-schema-properties)
    - [Status codes](#status-codes)

# Introduction

This is a sample “Petstore” server. You can find out more about Swagger at [swagger.io](http://swagger.io) or on [irc.freenode.net](irc.freenode.net), #swagger. For this sample, you can use the api key **special-key** to test the authorization filters.

## Store
The **Store** entity describes the inventory of the store. It allows to make order operations such as placing and deleting purchase orders as well as searching for orders by ID.
The available endpoints are as follows:
- GET/store/inventory
- GET/store/order/{orderID}
- POST/store/order 
- DELETE/store/order/{orderID}

### GET/store/inventory
Returns pet inventories by status.

<!-- no toc -->#### Parameters
No parameters.

<!-- no toc -->#### Request example
```
curl -X 'GET' \
  'https://petstore.swagger.io/v2/store/inventory' \
  -H 'accept: application/json'
  ```

<!-- no toc -->#### Response example

The response includes the information about 
```
{
"sold": 9,
"шершавый": 1,
  "Added": 1,
  "string": 4,
  "unavailable": 1,
  "rejected": 1,
  "pending": 5,
  "available": 971,
  "adopted": 1,
  "Unavailable": 1
}
```

### GET/store/order/{orderID}
Finds purchase order by ID.

<!-- no toc -->#### Parameters 
>Note: All the required fields are marked with an asterisk (*).

| Parameters    | Description                                                                                                                                      | Type             | Default value |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------- | ------------- |
| **orderID** * | ID of a pet that needs to be fetched. Max 64 bit. To receive a valid response, input value from 1 to 10. Other values will  generate exceptions. | Integer ($int64) | N/A           |

<!-- no toc -->#### Request example 

```
curl -X 'GET' \
  'https://petstore.swagger.io/v2/store/order/10' \
  -H 'accept: application/json'
```

<!-- no toc -->#### Response example 

The response includes the information about 
```
{
  "id": 0,
  "petId": 0,
  "quantity": 0,
  "shipDate": "2025-01-29T09:39:09.021Z",
  "status": "placed",
  "complete": true
}
```

### POST/store/order
Places an order for a pet.

<!-- no toc -->#### Parameters 
>Note: All the required fields are marked with an asterisk (*).

| Parameters | Description                        | Type   | Default value |
| ---------- | ---------------------------------- | ------ | ------------- |
| **body** * | Order placed for purchasing a pet. | object | N/A           |

<!-- no toc -->#### Request example 

```
curl -X 'POST' \
  'https://petstore.swagger.io/v2/store/order' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "id": 0,
  "petId": 0,
  "quantity": 0,
  "shipDate": "2025-01-29T07:22:51.812Z",
  "status": "placed",
  "complete": true
}'
```

<!-- no toc -->#### Response example 

The response includes the information about 
```
{
  "id": 0,
  "petId": 0,
  "quantity": 0,
  "shipDate": "2025-01-29T09:45:09.426Z",
  "status": "placed",
  "complete": true
}
```

### DELETE/store/order/{orderID}
Deletes purchase order by ID.

<!-- no toc -->#### Parameters 
>Note: All the required fields are marked with an asterisk (*).

| Parameters    | Description                                                                                                                                                                 | Type             | Default value |
| ------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | ------------- |
| **orderID** * | ID of the order that needs to be deleted. To receive a valid response, input a positive integer value. Negative or non-integer values will generate API errors. Max 64 bit. | integer ($int64) | N/A           |

<!-- no toc -->#### Request example
```
curl -X 'DELETE' \
  'https://petstore.swagger.io/v2/store/order/1' \
  -H 'accept: application/json'
```

<!-- no toc -->#### Response example

The response includes the information about 

```
{
  "code": 200,
  "type": "unknown",
  "message": "1"
}
```

### Response schema (Properties)
| Property     | Description                                           | Type             | Available values            |
| ------------ | ----------------------------------------------------- | ---------------- | --------------------------- |
| **id**       | ID of the order.                                      | integer ($int64) |                             |
| **petID**    | ID of the pet.                                        | integer ($int64) |                             |
| **quantity** | Quantity of pets ordered.                             | integer ($int32) |                             |
| **shipDate** | Date of shipment. Example: *2025-01-29T07:22:51.812Z* | string           |                             |
| **status**   | Status of the order.                                  | string           | placed, approved, delivered |
| **complete** | Indicates if the order is completed or not.           | boolean          |                             |

### Status codes

| Code    | Meaning              | How to handle (if applicable)                                                                                                                                                                                                                                                              |
| ------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **200** | Successful operation |                                                                                                                                                                                                                                                                                            |
| **400** | Invalid ID           | Indicates that the server couldn't process the request due to a client error (e.g. malformed request syntax, invalid request message framing, or deceptive request routing).Check the request URL for errors, make sure all the required fields are present and verify the request format. |
| **404** | Order not found      | Order ID does not exist. Try a different ID.                                                                                                                                                                                                                                               |
