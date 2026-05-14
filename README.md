# osTicket Help Desk Lab

[![Docker](https://img.shields.io/badge/Docker-Ready-2496ED?logo=docker&logoColor=white)](https://www.docker.com/)
[![MySQL](https://img.shields.io/badge/MySQL-Database-4479A1?logo=mysql&logoColor=white)](https://www.mysql.com/)
[![osTicket](https://img.shields.io/badge/osTicket-Help%20Desk-1A73E8)](https://osticket.com/)
[![Platform](https://img.shields.io/badge/Platform-Mac%20OS-lightgrey)]()
[![License](https://img.shields.io/badge/License-MIT-green)]()

A beginner-friendly Docker lab that deploys the osTicket help desk application with MySQL using Docker Compose on a local Mac computer.

---

## Overview

This project demonstrates how to deploy a real help desk ticketing system in a containerized environment. It is designed for beginners in IT, help desk, and cybersecurity who want hands-on experience with Docker, MySQL, and ticket management workflows.

By completing this lab, you will:

- Run osTicket in Docker containers.
- Connect osTicket to a MySQL database.
- Access a user-facing support portal.
- Use an admin panel to manage tickets.
- Demonstrate the full ticket lifecycle from creation to resolution.

---

## Demo Screenshots

### User Portal

Add a screenshot of the public support portal here:

```md

```

### Admin Panel

Add a screenshot of the admin ticket dashboard here:![image alt](https://github.com/MaliqueH5/osticket-lab/blob/main/Screenshot%202026-05-14%20at%2001-49-26%20osTicket%20Agent%20Login.png?raw=true)

```md

```

### Ticket Lifecycle Example

Add a screenshot of an open or resolved ticket here:

```md

```

---

## Features

- Docker Compose-based application deployment.
- osTicket help desk portal.
- MySQL-backed persistent data storage.
- User ticket submission and admin response workflow.
- Persistent data via named Docker volumes.
- Beginner-friendly troubleshooting notes.

---

## Skills Demonstrated

- Docker containerization.
- Docker Compose setup.
- MySQL database configuration.
- Web application deployment.
- Troubleshooting deployment errors.
- Ticket lifecycle management.
- Documentation and portfolio building.

---

## Requirements

- Mac computer with Apple Silicon or Intel processor.
- Docker Desktop installed and running.
- At least 5GB of free disk space.
- Internet access to download container images.
- 20–30 minutes to complete.

---

## Architecture

This lab uses two containers:

- **osTicket container**: Runs the help desk web application.
- **MySQL container**: Stores tickets, users, and system data.

The containers communicate over the Docker network created by Docker Compose.

---

## Project Structure

```bash
osticket-lab/
├── .env
├── docker-compose.yml
├── README.md
└── screenshots/
    ├── user-portal.png
    ├── admin-panel.png
    └── ticket-lifecycle.png
```

---

## Environment Variables

Create a `.env` file in the project root:

```env
MYSQL_ROOT_PASSWORD=osticketpass
MYSQL_DATABASE=osticket
MYSQL_USER=osticketuser
MYSQL_PASSWORD=osticketpass
```

---

## Docker Compose Configuration

Create `docker-compose.yml`:

```yaml
version: "3.8"

services:
  osticket:
    image: devinsolutions/osticket:latest
    platform: linux/amd64
    ports:
      - "8080:80"
    environment:
      MYSQL_HOST: mysql
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
    depends_on:
      - mysql

  mysql:
    image: mysql:5.7
    platform: linux/amd64
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
    volumes:
      - mysql_data:/var/lib/mysql

volumes:
  mysql_data:
```

---

## Quick Start

### 1. Create the Project Folder

```bash
mkdir ~/Desktop/osticket-lab
cd ~/Desktop/osticket-lab
```

### 2. Create the `.env` File

```bash
cat > .env << 'EOF'
MYSQL_ROOT_PASSWORD=osticketpass
MYSQL_DATABASE=osticket
MYSQL_USER=osticketuser
MYSQL_PASSWORD=osticketpass
EOF
```

### 3. Create `docker-compose.yml`

```bash
cat > docker-compose.yml << 'EOF'
version: "3.8"

services:
  osticket:
    image: devinsolutions/osticket:latest
    platform: linux/amd64
    ports:
      - "8080:80"
    environment:
      MYSQL_HOST: mysql
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
    depends_on:
      - mysql

  mysql:
    image: mysql:5.7
    platform: linux/amd64
    environment:
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
    volumes:
      - mysql_data:/var/lib/mysql

volumes:
  mysql_data:
EOF
```

### 4. Start the Containers

```bash
docker compose up -d
```

### 5. Verify the Containers

```bash
docker ps
```

---

## Usage

### User Portal

Open:

```text
http://localhost:8080
```

This is the public support portal where users can create tickets.

### Admin Login

Open:

```text
http://localhost:8080/scp/login.php
```

Use the following credentials:

- **Username:** `ostadmin`
- **Password:** `Admin1`

---

## Ticket Lifecycle Demo

### Create a Ticket

Submit a test ticket as a user with the following details:

- Name: John Doe
- Email: johndoe@email.com
- Help Topic: General Inquiry
- Subject: Unable to access my account
- Message: I have been locked out of my account since this morning, please help.

### Manage the Ticket

As an admin:

- Open the ticket from the Tickets list.
- Add a reply.
- Add an internal note if needed.
- Change the status to Resolved.
- Post the update.

---

## Troubleshooting

### Docker not running

Make sure Docker Desktop is open and fully started before running any commands.

### Architecture mismatch

Use `platform: linux/amd64` for Intel-only images on Apple Silicon Macs.

### Volume errors

Ensure the top-level volume name matches the service reference exactly.

### YAML formatting errors

Use spaces, not tabs, and keep indentation consistent.

---

## Shutdown and Restart

### Stop the Containers

```bash
docker compose down
```

### Stop and Remove Data

```bash
docker compose down --volumes
```

### Start Again Later

```bash
docker compose up -d
```

Your saved data remains available unless you remove the volume.

---

## Resume Highlight

- Deployed osTicket help desk system in a Docker containerized environment using Docker Compose and MySQL; documented architecture, troubleshot deployment errors, and demonstrated full ticket lifecycle management.

---

## License

This project is licensed under the MIT License.

---

## Acknowledgments

- osTicket for the help desk application.
- Docker for containerization.
- MySQL for database management.
