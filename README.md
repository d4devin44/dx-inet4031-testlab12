# Docker Lab: Containerizing a Three-Tier Application
**INET 4031 - Introductions to Systems**

This lab introduces Docker and Docker Compose by having you containerize a
real, multi-service application. You will package three components: Apache,
Flask, and MariaDB. These will be packaged into separate containers and wired together so they function as a complete application.

The application code and scaffolding are provided. Your job is to complete the Dockerfiles, verify the stack runs correctly, and document your work below.

> **Directions and explanations for this lab are on the repository Wiki.**
> Refer to the Wiki pages for step-by-step instructions.

---

*The sections below are for you to fill out. Replace each placeholder with your own content before submitting. Having a detailed README is the best practice for showing your work in future GitHub repositories.*

---

# Project Overview

This application is an IT support ticket management system built on a three-tier architecture, with each tier running as its own containerized service through Docker Compose. 

The first tier is the frontend, a web-based interface where users can browse existing tickets and submit new ones. The second tier is a backend API that sits between the interface and the data layer, handling all incoming requests and applying any necessary business logic. The third tier is a database that provides persistent storage for ticket data, ensuring nothing is lost if containers are restarted. 

The overarching goal of the lab is to get students to understand how these three components each serve their own purposes and can be utiliozed together through Docker Compose.

# Prerequisites

The following required components that should be installed before running the application is: 

- Docker
- Docker Compose
- Git
- Linux 

# Getting Started

Steps in bringing the stack from a fresh clone:

1. Clone the repository by using "git clone cd inet4031-testlab12"

2. Initiate the containers by using "docker compose up -d"

3. Check to see that all services are running by using "docker compose ps"

These three services should appear and be reported as running and "healthy"

- web
- app
- db


# Configuration

The purpose of the .env file is to enable configuration without users having to modify the application code. In the case that something is invalid or missing, health checks will report as failed.  

The .env file contains the following variables:
- database host
- database username
- database name
- database password


# Verification
To confirm if the stack is functioning properly: 

1. Container Status — docker compose ps
All three containers (web, app, and db) should appear as running and healthy.

2. Frontend Response — curl http://localhost:80/
A successful response will return an HTML output, confirming the frontend is working.

3. Health Check — curl http://localhost:80/health
The expected response is {"database":"connected","status":"healthy"}, which confirms that the API is running and has successfully connected to the database.

4. Retrieve Tickets — curl http://localhost:80/api/tickets
This should return a JSON array containing the existing tickets.

5. Create a Ticket — curl -X POST http://localhost:80/api/tickets -H "Content-Type: application/json" -d '{"title": "My first ticket", "description": "Testing the API"}'
A successful response will return {"id": <id>, "message": "Ticket created successfully"}, confirming the API can accept and store new tickets.

6. Automated Check — ./check.sh
Running this script will validate all of the above conditions automatically, including service health, API functionality, and data persistence.


# Feedback (Optional)

<!-- Do you have any feedback you would like to give us after completing this lab? What are some things you enjoyed? What about others that you felt was lackluster? Or maybe there was something that we missed that you'd love for us to touch on! This will help us improve the INET 4031 lab experience. We appreciate everything we can get!  -->
