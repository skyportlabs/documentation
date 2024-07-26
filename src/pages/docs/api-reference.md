---
title: API reference
description: Learn how api works.
---

## Overview

This API allows managing users, instances, and nodes. It requires an API key for all requests, which should be passed in the x-api-key header.

## Authentication
API Key:
* An API key is required for all endpoints. It ensures that the request is authenticated and authorized.
* Header: x-api-key

---

## User Endpoints

### GET | /api/users
* Retrieves a list of all users.
* Reponse:
  * '200': List of users.
  * '500': Error retrieving users.

### POST | /api/getUser
* Retrieves a user by email or username.
* Request Body:
  * 'type' (string): The search type, either 'email' or 'username'.
  * 'value' (string): The email or username to search for.
* Response:
  * '201': User details.
  * '400': Missing or invalid parameters, or user not found.
  * '500': Error retrieving user.

## Instances Endpoints

## Images Endpoints

### GET | /api/images
* Retrieves a list of available images.
* Response:
  * '200': List of images.
  * '500': Error retrieving images.

## Nodes Endpoints
---

## Error Responses

* '400': Bad Request. The request was invalid or cannot be otherwise served.
* '401': Unauthorized. API key is missing or invalid.
* '500': Internal Server Error. An error occurred on the server.
