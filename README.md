# Supported tags
- latest, alpine

# What is Let's Encrypt?
Let's Encrypt is a certificate authority that launched on April 12, 2016 that provides free X.509 certificates for Transport Layer Security (TLS) encryption via an automated process designed to eliminate the current complex process of manual creation, validation, signing, installation, and renewal of certificates for secure websites.

# How to use this image
Start the Letsencrypt instance as follows:

    docker run -it -d -p 80:80 -v ./ssl:/etc/letsencrypt --name letsencrypt hoadx/letsencrypt


# Docker Compose
A docker-compose.yml looks like this:

    letsencrypt:
      container_name: letsencrypt
      image: hoadx/letsencrypt
      ports:
      #  - "80:80"
        - "443:443"
      volumes:
        - ./ssl:/etc/letsencrypt



# Generate Let's Encrypt certificate
    docker exec -it letsencrypt \
      certbot \
      certonly \
      --manual \
      --email example@example.com \
      --agree-tos \
      --manual-public-ip-logging-ok \
      --domains example.com


    docker exec -it letsencrypt \
      certbot \
      certonly \
      --standalone \
      --preferred-challenges tls-sni-01
      #--preferred-challenges http-01
      --email example@example.com \
      --agree-tos \
      --manual-public-ip-logging-ok \
      --domains example.com
