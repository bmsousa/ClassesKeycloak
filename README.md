# keycloak
 MSI-STI Keycloak



## Class 2

Credits to https://github.com/PacktPublishing/Keycloak---Identity-and-Access-Management-for-Modern-Applications-2nd-Edition 

Useful information: https://access.redhat.com/documentation/en-us/red_hat_build_of_keycloak/22.0/html-single/server_guide/index#all-config-

## Step 1 - Build apps (frontend and backend)

```cd apps/backend```
```docker build . -t class2-backend```

```cd ../apps/frontend```
```docker build . -t class2-frontend```


## Step 2 - Start backend

```docker run --rm -it -p 3000:3000 --name class2-backend   class2-backend```


## Step 4 - Start frontend

```docker run --rm -it -p 8000:8000 --name class2-frontend class2-frontend```


## Step 3 start Keycloak
```docker run --rm --name keycloak -p 8080:8080 -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:24.0.2  start-dev```



## Keycloak Production Mode

### Step 1 Build Keycloak (if you want to perform customizations)
The Dockerfile demonstrates how to compile keycloak with support for HTTPS.
```sudo docker build . -t keycloak:24.0.2```

### Step 2 Run with Docker compose
To start with docker compose do:

```docker-compose -f compose.yml up```

### Step 3 Configure DNS resolution
Edit the file **/etc/hosts** and add:
```<IP address> keycloak ```
Where IP Address is the IP address of your machine, or IP from the docker network.

### Step 4 Access the Admin console
In your browser visit the URL:
```https://keycloak:8443```
Accept the security risk, as the certificate will not be considered valid.
