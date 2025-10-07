+++
date = '2025-09-10T02:35:11Z'
draft = false
title = 'Exploring Graph Explorer'
featuredImage = '/img/banners/graph-explorer.jpg'
tags = ["Azure", "Graph API"]
categories = ["Development"]
summary = "An overview of Microsoft Graph explorer and their API endpoints."
+++

## Introduction: Why Exploring Graph Explorer Matters

Graph Explorer is a powerful tool for developers and IT professionals to interact with the Microsoft Graph API. It provides a user-friendly interface to test API requests, explore data, and understand the capabilities of Microsoft Graph.

## Prerequisites

You should have some baseline understanding or familiarity with HTTP request methods.
- **GET:** Retrieve data from a specified resource. 
- **POST:** Send data to a server to create a new resource.
- **PUT:** Update an existing resource with new data.
- **PATCH:** Update an existing resource with partial data.
- **DELETE:** Remove a specified resource.

**Permissions**

For practice, we can use the sample tenant, which comes with pre-configured permissions. This allows you to explore various API endpoints without needing to set up your own Azure AD application. 

For production scenarios, you would need to sign into your tenant to obtain the necessary permissions, and consent to the privileges needed to perform your operation.
You can find the permissions for your endpoint in the **Modify permissions** section of the Graph Explorer. (Remember, least privilege access!)

## Getting Started

1. **Open Graph Explorer:** Visit [https://developer.microsoft.com/graph/graph-explorer](https://developer.microsoft.com/graph/graph-explorer).
2. **Browse sample queries:** You can use the left sidebar to select from a variety of pre-built queries.
3. **Run your own queries:** Enter any Microsoft Graph API endpoint in the request bar and click "Run Query".
4. **Sign in for more:** Log in with your Microsoft account to access your own data and try advanced scenarios.

## Example Queries

### GET
To GET a list of Microsoft users in your tenant, you can use the following query:

```HTTP
https://graph.microsoft.com/v1.0/users
```
Now depending on how many users are in your tenant, you may not have seen all of them. Microsoft graph returns 100 users by default. So what if we wanted to see more at a time? (As well as reduce the number of requests we make?)


To do this, we can use the `$top` query parameter to specify the number of users we want to retrieve in a single request. For example, to get 200 users(max 999), we can modify our query like this:

```HTTP
https://graph.microsoft.com/v1.0/users?$top=200
```

By default, Graph API returns a set list of properties for each user. This is where we can introduce the `$select` query parameter to specify which properties we want to retrieve. For example, to get the id, displayName, and userPrincipalName of each user, we can modify our query like this:

```HTTP
https://graph.microsoft.com/v1.0/users?$select=id,displayName,userPrincipalName 
```

### PATCH

Suppose we want to update a user's office location. For example, Clark Kent's current office location is `null`:

<img src="/img/content/clark_kent.png" alt="Clark Kent user details" style="width:300px; border-radius:8px; display:block;" />

To update the office location, use the following PATCH request:

```http
PATCH https://graph.microsoft.com/v1.0/users/clark.kent@domain.com
Content-Type: application/json

{
  "officeLocation": "Metropolis"
}
```

You will receive a `200 OK` response, indicating the update was successful. You can verify the change by performing a GET request on the user.

<img src="/img/content/clark_kent_patch.png" alt="Clark Kent PATCH" style="width:300px; border-radius:8px; display:block;" />


### POST
Post requests are commonly used to create new resources such as creating a user or group or assigning resources such as assigning a license or a role to a user.

For example, to create a new user, you can use the following POST request:

```http
POST https://graph.microsoft.com/v1.0/users
Content-Type: application/json

{
  "accountEnabled": true,
  "displayName": "Hal Jordan",
  "mailNickname": "hal.jordan",
  "userPrincipalName": "hal.jordan@domain.com",
  "passwordProfile": {
    "forceChangePasswordNextSignIn": true,
    "password": "InDarkestD@YInBl@ckestN1ight"
  }
}
```

You will receive a `201 Created` response, indicating the user was successfully created.

<img src="/img/content/hal_jordan_create.png" alt="Hal Jordan POST" style="width:300px; border-radius:8px; display:block;" />

### DELETE
DELETE requests are pretty self-explanatory. They are used to remove resources. For example, to delete the user we just created, you can use the following DELETE request:

```http
DELETE https://graph.microsoft.com/v1.0/users/hal.jordan@domain.com
```

You will receive a `204 No Content` response, indicating the user was successfully deleted.

> [!CAUTION]
> Please be careful when using DELETE requests, as some changes can be permanent.


## Conclusion

Graph Explorer is an essential tool for anyone working with Microsoft Graph. It simplifies learning, testing, and troubleshooting API requests, making it easier to integrate Microsoft 365 data and services into your applications.

## Resources
I reference the Microsoft Graph API documentation quite frequently (because that would be a lot of endpoints to memorize!)

[Microsoft Graph REST API Docs](https://learn.microsoft.com/en-us/graph/api/overview?view=graph-rest-1.0)

Prior to granting permissions, consult the permissions documentation to ensure you assign only the minimum privileges necessary for your task.

[Microsoft Graph Permissions reference](https://learn.microsoft.com/en-us/graph/permissions-reference)
