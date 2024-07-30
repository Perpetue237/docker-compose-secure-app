# docker-compose-secure-app

A Docker Compose setup for securely serving applications with Nginx, featuring HTTPS (TLS) and basic authentication. This project includes configuration for SSL/TLS certificates and user authentication to ensure your application is protected and accessible only to authorized users.

```plaintext
├── app
│   ├── Dockerfile
│   ├── main.py
│   └── requirements.txt
├── auth
├── certs
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

# Generate private key

openssl genrsa -out server.key 2048

# Generate CSR (Certificate Signing Request)

openssl req -new -key server.key -out server.csr

# Generate self-signed certificate

openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt

# Install `htpasswd` Utility

sudo apt-get install apache2-utils

# Create the `.htpasswd` File and user1

mkdir -p ./auth
htpasswd -c ./auth/.htpasswd user1

# Build and Run the Docker Compose Setup

docker-compose build

docker-compose up

# Verify the Setup

[https://localhost:8443](https://localhost:8443)
