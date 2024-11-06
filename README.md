
# Server Tools

A compilation of docker definitions to deploy self hosted tools for ops purposes


## Features

docker compose files for:

- **[Portainer](https://docs.portainer.io/):** Container management.
- **[Nginx Proxy Manager](https://nginxproxymanager.com/guide/):** Hosts configurations (Domains & SSL Certs)


## Installation

For installation you need to have a Linux VPS or similar with a `docker` installed and a user with enough permissions to run it.

**1. Connect to your server**
   ```
   $ ssh -i "YOUR_PEM" ubuntu@YOUR_IP
   ```
**2. Generate you ssh keys** to clone this projects if you don't have one.
   ```bash
   $ ssh-keygen
      ....
   $ cat cat .ssh/id_rsa.pub
      ssh-rsa AAAAB3NzaC1 ....

   # User your public key in your github account or add it to repository as deploy key
   $ git clone git@github.com:reservamos/brain-tools.git
   ```

**3. Create shared network.**
```
$ docker network create nginx-network
```
**4. Start Nginx Proxy.**
  ```
  $ cd proxy-manager
  $ docker compose up -d --build
  ```
#### Default credentials: 
```
Email: admin@example.com
Password: changeme
```

**4. Start Portainer.**
  ```
  $ cd portainer
  $ docker compose up -d --build
  ```

> Remember that both: proxy manager and portainer have a restart policy, if you need to stop them you should use `docker update <container_id> --restart=none` command to disallow the auto-restartings.
> Also remember to reference to localhost porst you need to reference to root docker IP with `ip addr show docker0` normally is `172.17.0.1`


### Shared network
**3. Create a separate network for shared services.**
```
$ docker network create shared-network
```