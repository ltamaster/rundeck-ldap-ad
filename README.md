# Rundeck LDAP / AD Authentication Example

## Configuration

Set LDAP environment variables on ``docker-compose.yml`` (the default values works)

### On Rundeck Container
* LDAP_URL
* LDAP_BIND_USER
* LDAP_BIND_PASSWORD
* LDAP_ROLES_BASE_DN
* LDAP_USER_BASE_DN

### On LDAP Container

* LDAP_BASE_DN
* LDAP_ADMIN_PASSWORD
* LDAP_DOMAIN


## Build

```
docker-compose build
```


## Run

```
docker-compose up -d
```

Rundeck will start on: `http://localhost:4440`
LDAP Admin GUI will start on: `http://localhost:8080`


## Stop
```
docker-compose down
```

