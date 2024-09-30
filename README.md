<p align="center">
	 <a href="https://www.buymeacoffee.com/suchorski" target="_blank">
	 	 <img src="https://cdn.buymeacoffee.com/buttons/v2/default-red.png" alt="Buy Me A Coffee" width="150" >
	 </a>
<p>

# Keycloak + MariaDB + Nginx + Certbot + Mail in a Docker Compose stack

## Introduction

This project is a complete stack for running a secure Keycloak server with MariaDB as database and Nginx as reverse proxy with SSL enabled.

## Prerequisites

* Docker Engine
* Docker Compose
* A valid domain name

## Installation

1. Clone this repository on your local computer;
2. Create a `.env` and configure it according to your needs (see below);
3. Run `docker compose -f docker-compose-ssl.yml up -d` to generate the SSL certificates;
4. Run `docker compose -f docker-compose-ssl.yml down` to stop the container;
5. Run `docker compose up -d` to start the stack;
6. Configure the `crontab` to renew the SSL certificates automatically each 12 hours with the command: `docker compose -f /path/to/docker-compose.yml up certbot && docker compose -f /path/to/docker-compose.yml exec nginx nginx -s reload`.

## Informations

### Keycloak

Default admin username and password is: `admin`.

### Mail server

You can use mail SMTP hostname as `mail` and port `25` without authentication to send mails from Keycloak.

## Configuration

### Environment variables

The environment variables are set in the `.env` file. The following variables are available:

| **Variable** | **Description** | **Default value** | **Required** |
|---|---|---|---|
| KEYCLOAK_DOMAIN | The domain to be used as Keycloak URL |  | Yes |
| CERTBOT_LETSENCRYPT_EMAIL | The email to be used for Let's Encrypt registration |  | Yes |
| SUBNET | The subnet to be used by the containers | 172.16.0.0/29 | No |
| KEYCLOAK_VERSION | The Keycloak version to be used | latest | No |
| MARIADB_VERSION | The MariaDB version to be used | latest | No |
| MARIADB_ROOT_PASSWORD | The password to be used for the MariaDB root user | toor | No |
| MARIADB_KEYCLOAK_PASSWORD | The password to be used for the Keycloak user in MariaDB | keycloak | No |
| NGINX_VERSION | The Nginx version to be used | latest | No |
| CERTBOT_VERSION | The Certbot version to be used | latest | No |

## Contributing

If you find this project useful here's how you can help:

* Send a Pull Request with your awesome new features and bug fixes
* Help new users with issues

## License

MIT. See `LICENSE` for more details.
