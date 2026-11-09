# Gentlemen's Club --- Architecture

## Overview

Gentlemen's Club is a barbershop booking platform that brings together a
customer-facing website, an administrative interface, a REST API, a
PostgreSQL database, and a Telegram bot.

The website and Telegram bot use the same backend database so
appointment and reference data can be managed centrally.

## High-level architecture

``` text
                         CUSTOMER
                         /      \
                        /        \
                       v          v
                WEBSITE         TELEGRAM
             (HTML/CSS/JS)        BOT
                       |        (Python)
                       |        (aiogram 3)
                       v          |
                  EXPRESS REST API |
                       |          |
                       +-----+----+
                             |
                             v
                       POSTGRESQL
                        DATABASE

                ADMINISTRATOR
                      |
                      v
              ADMIN DASHBOARD
                      |
                      v
                EXPRESS REST API
```

## Main components

### 1. Frontend

The frontend provides the public website and the administration
interface. It is built with HTML, CSS, and JavaScript.

The public interface lets visitors browse the barbershop's services and
masters and submit appointment requests. The administration interface
provides a protected workspace for managing appointments.

In the Docker deployment, the Express backend serves the frontend files.

### 2. Backend API

The backend is built with Node.js and Express. It exposes REST API
endpoints used by the website, administration interface, and supporting
application logic.

Its responsibilities include:

-   Providing service and master data.
-   Processing appointment-related requests.
-   Handling administrator authentication.
-   Reading and updating application data through Prisma ORM.

### 3. Database

PostgreSQL stores the application's persistent data, including:

-   Services and their details.
-   Masters and their details.
-   Client records.
-   Appointments.
-   Administrator accounts.

Prisma ORM provides the backend with a structured way to access the
database. Database schema changes are managed through Prisma migrations.

### 4. Telegram bot

The Telegram bot is written in Python and uses aiogram 3.

It provides a conversational interface for customers. The bot connects
to the PostgreSQL database and guides users through the available
booking flow, such as choosing a service, a master, and an available
date or time.

### 5. Containerization

Docker Compose is used to run the application components as separate
services:

-   `backend` --- the Node.js API and website delivery.
-   `bot` --- the Telegram bot.
-   `db` --- the PostgreSQL database.

The services communicate over the Docker Compose network. The database
is kept in a Docker volume so its data can persist when containers are
restarted or recreated.

## Typical booking flow

1.  A customer opens the website or starts a conversation with the
    Telegram bot.
2.  The customer reviews the available services and masters.
3.  The customer selects the desired booking details.
4.  The application sends the request to the backend or processes it
    through the bot's database integration.
5.  Booking information is stored in PostgreSQL.
6.  An administrator can review and manage the appointment through the
    administration interface.

## Technology stack

  Area                      Technology
  ------------------------- ------------------------
  Frontend                  HTML, CSS, JavaScript
  Backend runtime           Node.js
  Web framework             Express
  Database                  PostgreSQL
  ORM and migrations        Prisma
  Telegram bot              Python, aiogram 3
  Deployment and services   Docker, Docker Compose

## Deployment and configuration

Runtime configuration and credentials are supplied through environment
variables. Secret values should not be committed to a public repository.

The public portfolio repository contains documentation and selected
screenshots only. The full application source code is maintained
separately in a private repository.

## Notes

This document describes the current project structure at a high level.
Specific endpoints, infrastructure details, and deployment addresses may
change as the project evolves.
