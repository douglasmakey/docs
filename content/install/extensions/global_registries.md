+++
date = "2017-04-15T14:39:04+02:00"
title = "Global Registries File"
url = "setup-global-registry-credentials"

[menu.install]
  parent = "install_enterprise"
  identifier = "setup-global-registry-credentials"
  weight = 3
+++

{{% alert enterprise %}}
This feature is only available in the [Enterprise expansion pack](https://drone.io/enterprise/)
{{% /alert %}}

The enterprise expansion pack provides support for global registry credentials, sourced from a yaml file on your server. You should mount the credentials file into your container and specify the path to the file in your configuration.

Example server configuration:

```diff
services:
  drone-server:
    image: drone/drone:{{% version %}}
    ports:
      - 80:8000
    volumes:
      - /var/lib/drone:/var/lib/drone/
+     - /etc/drone-registry.yml:/etc/drone-registry.yml
    restart: always
    environment:
+     DRONE_GLOBAL_REGISTRY=/etc/drone-registry.yml
```

Example registry credentials file:

```nohighlight
- address: docker.io
  username: octocat
  password: correct-horse-batter-staple
- address: gcr.io
  username: _json_key
  password: |
    {
      "private_key_id": "...",
      "private_key": "...",
      "client_email": "...",
      "client_id": "...",
      "type": "..."
    }
```
