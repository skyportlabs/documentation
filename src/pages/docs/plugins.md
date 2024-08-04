---
title: Plugin development
description: Learn how to make Skyport Plugins.
---

## Plugins API Documentation

### Overview

This guide details how to create and manage plugins for our system. Plugins extend and customize the core application's functionality.

### Plugin Structure

A typical plugin includes several key files:

- `manifest.json`: Metadata and configuration for the plugin.
- `index.js`: The main entry point for the plugin's code.
- `router.js`: Defines the express routes for the plugin.

### Example Plugin

Here is an example of a simple plugin:

#### `manifest.json`

```json
{
    "name": "Example Plugin",
    "version": "1.0.0",
    "description": "Description of the Example Plugin",
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

In the `manifest.json`, you can configure the metadata for the Skyport Plugin Manager. Key fields include:

- `"main": "index.js"`: Specifies the main file to initialize the plugin.
- `"router": "example"`: Sets a prefix for all express routes. For instance, a route defined as `"/"` will be accessible at `"/example"`.
- `"adminsidebar"`: Links to add to the Admin Sidebar, useful for plugin settings.
- `"sidebar"`: Links for the user sidebar.
- `"instancesidebar"`: Links for the instance navigation bar. You can include placeholders like `%id%` which will be replaced with the instance ID. FontAwesome icons can be used for sidebar entries.

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

### Conclusion

This documentation covers the basics of creating and managing plugins within the system. By following the provided structure and guidelines, you can extend the core application's functionality to suit your needs.
