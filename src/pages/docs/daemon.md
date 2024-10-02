---
title: Installation
description: Learn how to install Skyport Daemon.
---

## Dependencies

* Node.js `v18` and higher (Nodejs `v22` recommended).
* Docker (or Docker Desktop on Windows / macOS)

### Example Dependency Installation

The commands below are simply an example of how you might install these dependencies on Ubuntu 24.04. Please consult with your
operating system's package manager to determine the correct packages to install.

```sh
# Ubuntu/Debian
curl -sSL https://get.docker.com/ | CHANNEL=stable bash

sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_16.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list

sudo apt update
sudo apt install -y nodejs git
```

## Installation

The following commands will download the Skyport Daemon into /etc/skyportd and use npm to install the required packages:

``` bash
cd /etc
git clone --branch v0.2.2 https://github.com/skyportlabs/skyportd
cd skyportd
npm install
```

You can then add the node to the panel and get the configuration command by clicking the "Configure" button. Once you have executed this command, you are ready to start the Daemon.

### Setup Complete

All you need to do now is start `skyportd`:
```bash
node .
```

### For Production Applications

To deploy `skyportd` efficiently in production, using PM2 or alternatives is recommended. Below are the standard PM2 setup steps.

Run the following command to install PM2:
```bash
npm install pm2@latest -g
```

After this, run `skyportd` using PM2:
```bash
pm2 start index.js
```

### Advanced Users: Auto-Run on Startup

With the PM2 process running in the background, run the following command:
```bash
pm2 startup
```

Then, to 'freeze' the running processes, run the following command:
```bash
pm2 save
```

This will ensure the PM2 process automatically respawns on startup.
