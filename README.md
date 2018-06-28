# Rundeck LDAP / AD Authentication Example

## Configuration

* For LDAP connection use ``docker-compose.yml``. 
* For AD connection use ``docker-compose-ad.yml``


### On Rundeck Container
* LDAP_URL
* LDAP_BIND_USER
* LDAP_BIND_PASSWORD
* LDAP_ROLES_BASE_DN
* LDAP_USER_BASE_DN

### On LDAP Container (for LDAP environment only)

* LDAP_BASE_DN
* LDAP_ADMIN_PASSWORD
* LDAP_DOMAIN

### Users and Roles (for LDAP environment only)

On ``ldap/rundeck.ldif`` it was loaded some roles and users by default, you can change users there or use LDAP Admin GUI.

Default users are:
* username: rundeckadmin, password: Rundeck123. (Admin user)
* username: ruser, password: Rundeck123. (Test user)

On ```rundeck/data/acl``` you can load customs acls policies for rundeck.

## Build

```
docker-compose -f [docker-compose-x] build
```


## Run

```
docker-compose -f [docker-compose-x] up -d
```

Rundeck will start on: `http://localhost:4440`
LDAP Admin GUI will start on: `http://localhost:8080` (LDAP Environment only)


## Stop
```
docker-compose  -f [docker-compose-x] down
```

