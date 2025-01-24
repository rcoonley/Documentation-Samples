---
title: XYZ Cloud Servers API Documentation
layout: xyz-cloud-v1.0
version: v1.0
lang: en
---

# XYZ Cloud Servers API Documentation
---

Welcome to the Application Programming Interface (API) documentation for your XYZ Cloud Servers account! You can use this API to program virtually any task you can perform in your account's control panel, including management of your IP addresses, networks, network rules, backups, and virtual machines.

- [XYZ Cloud Servers API Documentation](#xyz-cloud-servers-api-documentation)
  - [Getting Started](#getting-started)
    - [API Requirements](#api-requirements)
    - [Authentication](#authentication)
      - [Authentication Example](#authentication-example)
    - [Generating an API Key](#generating-an-api-key)
- [API Reference](#api-reference)
    - [Enpdoint Definitions](#endpoint-definitions)
  - [Requests](#requests)
    - [Query Operations](#query-operations)
      - [Filtering](#filtering)
    - [Read Operations](#read-operations)
    - [Create Operations](#create-operations)
    - [Update Operations](#update-operations)
    - [Delete Operations](#delete-operations)
    - [Action Operations](#action-operations)
  - [Responses](#responses)

<br/>
 
<a id="getting-started-">

## Getting Started</a>

This documentation is intended for developers using the XYZ API. Based on REST (Representation State Transfer) principles, our dynamic web service makes it easy to navigate to resources and program tasks.

From the base URL, you can authenticate and navigate through the API resources in a web browser. For the HTML view of the API, go to [https://api.xyzcloudservers.net/vi/](https://api.xyzcloudservers.net/vi/).

To get started, review the [requirements](#requirements") and generate an [API key](#generating-an-api-key). 

 <br/>
 
 <a id="requirements">

### API Requirements</a>

To use this API, you will need:
* An XYZ Cloud Servers account
* An understanding of the XYZ Cloud Servers application
* Familiarity with JSON, programming languages, web services, and HTTP methods

In addition, you might want to have:
* An up-to-date of a modern web browser, such as Google Chrome
* An integrated development environment (IDE) for your preferred scripting language
* A REST client, such as Postman or Swagger

> [!NOTE]
> You can choose whichever API client and programming language you want to use to interact with the API. An API client is software that lets you interact with the API through a user interface.

<br/>

<a id="authentication">

### Authentication</a>

Before you can use the XYZ Cloud Servers API, you must generate an API key to validate your requests. An API key consists of an access key (username) anda secret key (password). Each time you send a request to the server, The web service uses HTTP basic authentication to securely pass your credentials over HTTP, use HTTPS with SSL on **TCP port 443**.

HTTP basic authorization appends your access key with a colon and concatenates your secret key before transmission. Then it uses the Base64 algorithm to encode the resulting string. The HTTP header tranmits the encoded string, and the web service reads and validates it.

<br/>

<a id="auth-example">

#### Authentication Example</a>

```Javascript
accessKey = "your-access-key"
secretKey = "your-secret-key"
inputString = accessKey + ":" + secretKey // "your-access-key:your-secret-key"
base64 = base64_encode(inputString); // "eW91ci1hY2N1c3Mta2V50nlvdXItc2VjcmV0LWtle/q=="
authorizationHeader = "Basic" + base64; // "Basic eW91ci1hY2N1c3Mta2V50nlvdXItc2VjcmV0LWtleQ=="
```

All request headers should contain authorization.

```Javascript
Authorization: Basic eW91ci1hY2N1c3Mta2V50nlvdXItc2VjcmV0LWtleQ==
```
 <br/>
 
 <a id="generating-an-api-key">

### Generating an API Key</a>

To generate your API key:
1. Log in to [XYZ Cloud Servers](https://www.XYZcompany.com/login).
2. Go to the **API** tab.
3. Click **Manage API Keys**.
4. In the **API Keys** section, click **Create API Key**. Your access key and secret key display.
5. Click **Download Key** to generate a CSV file that contains your authentication credentials. We recommend you save this file in a secure place, as there is no option to retrieve it later.

6. Click **Close**.

<br/>
   
***Generating Additional API Keys***

To generate another API key, repeat steps 4 through 6. 

<br/>

***Deleting an API Key***

To delete an existing API key, click **Make inactive**.

<br/>

<a id="api-reference">

# API Reference</a>
---

This API reference contains detailed information about the methods, URLs, request types, response codes, and fields for each operation. It also includes examples of JSON requests and responses.

<br/>

<a id="endpoint-definitions">

### Endpoint Definitions</a>

API endpoints are URLs you can use to access functions and resources. 

Refer to this table for definitions of the terms the API endpoints use.

<br/>

**Table 1: Endpoint Definitions**

| **Term**        | **Definition** |   
| ------------- | ------------- | 
| Action | An **action** performs an operation on a collection or resource beyond the scope of standard methods, and then returns a result. | 
| Collection | A **collection** is a group of related resources. It consists of the representation of each resource and any additional information. |  
| Identifier | Every resource in a collection has a unique **identifier** that the web service assigns to it |   
| Method | You can use the following HTTP **methods** to make a request: `GET`, `POST`, `PUT`, and `DELETE`. |
| Resource | A **resource** is any object or concept in the application, such as a database or network. |
| Representation | A **representation** describes a resource. The API transfers representations of your resources between you and the server. Most representations of resources contain a series of attributes (key-value pairs). Resources return these representations: `id`, `type`, `rev`, `links`, and `actions`.| 
| Schema | A **schema** defines the available operations for a resource. | 
| Self | Each resource contains a **self** link, which is a URL that displays the canonical location for the resource. | 

<br/>

<a id="requests">

## Requests</a>

This section provides information about the API requests you can make. The following table provides an overview of each operation, while the subsequent sections describe each operation in detail. 

> [!NOTE]
> An ellipses in a URL represents a placeholder for the base URL: [https://api.cloud.xyzcompany.com/v1/](https://api.cloud.xyzcompany.com/v1/).<br/> 
> Required fields display in **boldface** type.

<br/>

**Table 2. Overview of Operations**

| **Operation** | **HTTP Method** | **Request URL** | **Description** |
| ------------- | ------------- | ------------- | ------------- | 
| Query | GET | .../{collection} | Returns a collection of resources. |
| Read | GET | .../{collection}/{resourceid} | Returns a single resource. |
| Create  | POST | .../{collection} | Creates a new resource. |
| Update | PUT | .../{collection} <br/>.../{collection}/{resourceid} | Updates an existing resource. |
| Delete | DELETE | .../{collection} <br/>.../{collection}/{resourceid} | Deletes a resource. |
| Action | POST | .../{collection} <br/> .../{collection}/{resourceid} | Performs an action on a resource or collection. |

<br />

<a id="query-operations">

### Query Operations</a>

A query operation displays all of the resources in a collection. A GET request on the base URL returns the collection of resources for that API version.

<br/>

**Example Request**

```Javascript
GET /v1/folders HTTP/1.1
Accept: application/json
...
```

<br/>

**Example Response**

```Javascript
HTTP/1.1 200 OK
Content-Type: application/json
...

{
  "type":"collection",
  "resourceType":"folder",
  "data":[
    {
      "type":"folder", "id: "b1b2e7006be", "name": "Documents", "links": {/*...*/}, "actions":  {/*...*/},
      /*more folder resources...*/
    }],
  "links": 
  {
    "self":"https://base/v1/folders",
    ...         
  },
  "actions": 
  {
    "deleteAll":"https://base/v1/folders/deleteALL",
    ...
  },
  "filters": 
  {
    /*see filters*/
  }
}
```

<br/>

<a id="filtering">

#### Filtering</a>

The schema of a collection indicates whether filtering is supported. If a collection supports filtering, its response has a "filter" object and an attribute for each field you can filter. If you applied a filter to a field, the value is an array that describes the filter. If you did not apply a filter, the value is null. You can combine filters with "AND," but not "OR."

In addition, if a collection supports filtering, its documentation includes a table that describes which modifiers are supported and which options are allowed, if any.

<br/>

**Table 3. Descriptions of modifiers for filters**

| **Modifier**        | **Description** |   
| ------------- | ------------- | 
| eq | equal to |
| ne | not equal to |
| lt | less than |
| lte | less than or equal to |
| gt | greater than |
| gte | greater than or equal to |
| prefix | starts with |
| like | matches |
| notlike | does not match |
| null | value is empty|
| notnull | value is not empty |

<br/>

**Example Response**
```Javascript
{
  /*...*/
  "filters": {
    "name": {"modifiers":["ne", "prefix", "suffix", wildcards: true),
    "date": {"modifiers":["lt", "gt", "let", "gte", "prefix"]},
    "size": {"modifiers":["lt", "gt", "lte", "gte"]},
    "shared": {"options":["public", "private"]},
    /*...*/
  },
  /*...*/  
}
```

<br/>

<a id="read-operations">

### Read Operations</a>

Use read operations to display a single resource in a collection.

<br/>

<a id="API-versions">

#### API Versions</a>

Use a GET requeest on the base URL to return a colletion of API version resources. A GET request on the base URL of a particular API version returns a resource that contains links to all available resources.

<br />

**Example Request**

```Javascript
GET /v1 HTTP/1.1
...
```

<br/>

**Example Response**

```Javascript
HTTP/1.1 200 OK
Content-Type: application/json
...

{
   "id":"v1",
   "depracated":true,
   "links": {
      "file":"{base_url}/files",
      "folder":"{base_url}/folders"
   },
}
```
<br/>

<a id="single-resource">

#### Single Resource</a>

Use a GET request on the URL of a single resource to return a representation of that resource.

**Example Request**

```Javascript
GET /v1/files/blb2e7006be HTTP/1.1
...
```

<br/>

**Example Response**
```Javascript
HTTP/1.1 200 OK
Content-Type: application/json
...

{
   "id":"blb2e7006be",
   "type":"file",
   ...
}
```
<br/>

<a id="create-operations">

### Create Operations</a>

*Add content.* 

<br/>

<a id="Update-operations">

### Update Operations</a>

*Add content.* 

<br/>

<a id="delete-operations">

### Delete Operations</a>

*Add content.* 

<br/>

<a id="action-operations">

### Action Operations</a>

*Add content.* 

<br/>

<a id="responses">

## Responses</a>
You will receive an HTTP response for each request you make. The responses contain status codes that indicate the results of your requests.

In general, you will receive these types of responses:
* 200s: Successful requests
* 300s: Redirects 
* 400s: Unsuccessful requests due to client-side errors
* 500s: Unsuccessful requests due to server-side errors

<br/>

**Table 4. Status Codes**

| **Status Code** | **Response** | **Description** | 
| ------------- | ------------- | ------------- |
| 200 | OK | Your request was successful. |
| 201 | Created | Your request to create a new resource was successful. For more information, see the Location header. |
| 202 | Accepted | The server received your request but didn't complete it yet. |
| 204 | No Content | Your request was successful, but there is no content in the server's response. |
| 301 | Moved Permanently | The resource you requested is permanently stored eleswhere. For more information, see the Location header. |
| 302 | Found | The resource you requested is temporarily stored elsewhere. For more information, see the Location header. |
| 304 | Not Modified | You submitted a conditional GET request that didn't modify the resource. |
| 400 | Bad Request | You submitted an invalid request. |
| 401 | Unauthorized | Your authentication information is invalid or expired, or you didn't include it. |
| 403 | Forbidden | The web service validated your authentication information, but you don't have user access to the requested resource. |
| 404 | Not Found | The server could not find your request. |
| 405 | Method Not Allowed | The HTTP method you requested is not allowed for the specified URL. |
| 406 | Not Acceptable | The web service doesn't support the content type you requested. |
| 409 | Conflict | You implemented resource versioning, but your request conflicts with the current state. |
| 410 | Gone | The web service no longer supports the API version you requested, or the resource you requested no longer exists. |
| 500 | Internal Server Error | The server could not complete your request. Please contact technical support for assistance at [APIsupport@xyzcompany.com](email:APIsupport@xyzcompany.com). |
| 503 | Service Unavailable | The web service is temporarily unavailable due to maintenance or server overload. Please try your request again later. |









