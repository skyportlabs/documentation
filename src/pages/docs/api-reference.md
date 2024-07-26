---
title: API reference
description: Learn how api works.
---

## Overview

This API allows managing users, instances, and nodes. It requires an API key for all requests, which should be passed in the x-api-key header.

## Authentication
API Key
* Header: x-api-key
* Description: An API key is required for all endpoints. It ensures that the request is authenticated and authorized.

---

## Endpoints

User Endpoints

### GET | /api/users
* Retrieves a list of all users.
* Reponse:
  * '200': List of users.
  * '500': Error retrieving users.
