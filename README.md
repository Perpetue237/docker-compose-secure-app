# docker-compose-secure-app

A Docker Compose setup for securely serving applications using Nginx with HTTPS (TLS) and basic authentication. This project configures SSL/TLS certificates and user authentication to protect and restrict access to your application.
- [docker-compose-secure-app](#docker-compose-secure-app)
  - [Project Structure](#project-structure)
  - [Setup Instructions](#setup-instructions)
    - [Generate SSL Certificates](#generate-ssl-certificates)
    - [Install `htpasswd` Utility](#install-htpasswd-utility)
    - [Create the `.htpasswd` File and user1](#create-the-htpasswd-file-and-user1)
  - [Build and Run the Docker Compose Setup](#build-and-run-the-docker-compose-setup)
- [Verify the Setup](#verify-the-setup)
  - [License](#license)


## Project Structure

```plaintext
├── app
│   ├── Dockerfile
│   ├── main.py
│   └── requirements.txt
├── auth            # .htpasswd for user authentication (not in Git)
├── certs           #  SSL/TLS certificates (not in Git)
│   ├── server.crt
│   ├── server.csr
│   └── server.key
├── docker-compose.yml
├── LICENSE
├── nginx
│   ├── Dockerfile
│   └── nginx.conf
└── README.md
```

## Setup Instructions
### Generate SSL Certificates

```sh

openssl genrsa -out certs/server.key 2048
openssl req -new -key certs/server.key -out certs/server.csr
openssl x509 -req -days 365 -in certs/server.csr -signkey certs/server.key -out certs/server.crt
```

### Install `htpasswd` Utility

sudo apt-get install apache2-utils

### Create the `.htpasswd` File and user1

mkdir -p ./auth
htpasswd -c ./auth/.htpasswd user1

## Build and Run the Docker Compose Setup

docker-compose build

docker-compose up

# Verify the Setup

[https://localhost:8443](https://localhost:8443)

>**Note:** 
>- The auth and certs directories are included in .gitignore for security reasons.
>- Ensure that ports 8080 and 8443 are available on your host machine.

## License

Distributed under the Apache License. See [LICENSE](LICENSE) for more information.
