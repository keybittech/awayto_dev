---
title: "Installation"
weight: 1
---

### [&#128279;](#installation) Installation

#### Get the code from the repo

```
git clone {{< param "v3Repo" >}}
```

#### Create an .env file

```
cp .env.template .env
```

At the very least, these properties should be set as per your project:
- PROJECT_PREFIX - identifier used in resource creation, best to not use any special characters out of precaution as the identifier is used across the stack for various purposes with varying limitations
- PROJECT_TITLE - literal text used for headers/titles
- DOMAIN_NAME - deployed domain name
- ADMIN_EMAIL - used for certbot registration

