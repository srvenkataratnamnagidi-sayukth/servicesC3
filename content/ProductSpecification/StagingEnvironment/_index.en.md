---
title: Staging Environment
tags : ["Composing"]
weight: 5
---
Staging Environment is a single server instance will all the components.
This is exposed to all the Developers, DevOps team can update the builds on demand.

## Environment Details
### How to access the Server
The server is hosted on a GCP VM. The following are steps to update the build on the server
1. Login to GCP using the account name ***devops1@shadkona.com*** with password ***1!Qdesigner***
2. SSH to the GCP VM named **GramSevak**
3. Got the source code folder and get the latest code & start the deployment script
```
cd /opt/devops
git pull
cd gramsevak
sh deploy.sh
```
4. Once the build is deployed, please check the [Staging URL] (https://gramsevak.ts.gov9.in) and validate your functionality
{{% children  %}}
