---
title: API reference
description: Learn how api works.
---

## Overview

This API allows managing users, instances, and nodes. It requires an API key for all requests, which should be passed in the x-api-key header.

## Authentication
API Key
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
