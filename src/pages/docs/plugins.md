---
title: Plugin development
description: Learn how to make Skyport Plugins.
---

# Plugins API Documentation

## Overview

This documentation provides details on creating and managing plugins for our system. Plugins allow you to extend and customize the functionality of the core application.

## Plugin Structure

A plugin consists of several key files:

- `manifest.json`: Defines the plugin's metadata and configuration.
- `index.js`: The main entry point for the plugin's code.
- `router.js`: Defines the express routes for the plugin.

### Example Plugin

Here is an example of a simple plugin:

#### `manifest.json`

```json
{
    "name": "Example Plugin",
    "version": "1.0.0",
    "description": "The Description of the Example Plugin",
    "author": "privt00",
    "main": "index.js",
    "router": "example",
    "adminsidebar": {
        "example url": "/example"
    },
    "sidebar": {
        "example url": "/example"
    },
    "instancesidebar": {
        "example url": {
            "url": "/instance/%id%/example",
            "icon": "fa-solid fa-folder"
        }
    }
}
```

#### `index.js`

```javascript
const express = require('express');
const router = require('./router');
const settings = require('./settings');

function register(addonManager) {
    // Plugin registration logic
    addonManager.registerSettings(settings);
    // console.log('Advanced plugin loaded!');
}

module.exports = {
    register,
    router
};
```

#### `router.js`

```javascript
const express = require('express');
const router = express.Router();
const middleware = require('./middleware');

router.use(middleware);

router.get('/', (req, res) => {
    res.render('index', { user: req.user });
});

module.exports = router;
```

#### `middleware.js`

```javascript
module.exports = function(req, res, next) {
    // Middleware logic
    console.log('Middleware executed for:', req.url);
    next();
};
```

#### `settings.js`

```javascript
module.exports = {
    option1: true,
    option2: "default"
};
```

