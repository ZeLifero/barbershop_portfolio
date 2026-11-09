# Gentlemen's Club --- Features

## Overview

Gentlemen's Club is a barbershop booking platform designed to make
appointment scheduling convenient for customers and appointment
management straightforward for administrators.

The application combines a public website, an administration dashboard,
a PostgreSQL database, and a Telegram bot.

## Customer-facing website

### Services catalog

Visitors can browse the barbershop's available services and review key
details, including:

-   Service name.
-   Price.
-   Estimated duration.

### Masters catalog

Visitors can view the available barbers and choose a master when
creating an appointment.

### Online appointment booking

The website provides a booking flow in which a customer can:

1.  Select a service.
2.  Choose a master.
3.  Select a date.
4.  Choose an available time slot.
5.  Submit the appointment request.

The booking information is stored in the application's database.

## Administration dashboard

The project includes a separate administration interface.

### Administrator authentication

Access to the dashboard is protected by an authentication flow.
Administrator credentials are checked by the backend, and authenticated
requests use a signed token.

### Appointment management

Administrators can review incoming appointments and manage their booking
statuses through the dashboard.

The dashboard is intended to give staff a central place to keep track of
customer bookings.

## Telegram bot

The Telegram bot provides an alternative way for customers to interact
with the barbershop.

Its booking flow supports guided selection steps, including:

-   Viewing available services.
-   Choosing a master.
-   Selecting a date.
-   Choosing an available time slot.

The bot is implemented in Python with aiogram 3 and connects to the
project's PostgreSQL database.

## Data management

PostgreSQL is used as the central data store for the application.

The database contains records for the main application entities:

-   Clients.
-   Services.
-   Masters.
-   Appointments.
-   Administrators.

Prisma ORM is used by the Node.js backend to work with the database,
while schema changes are managed through migrations.

## Technical and deployment features

-   REST API built with Express.
-   Shared PostgreSQL database for application data.
-   Prisma ORM and database migrations.
-   Dockerized backend, bot, and database services.
-   Environment-based configuration for runtime settings and secrets.

## Project goals

The project demonstrates how several application components can work
together as one service:

-   A responsive customer-facing website.
-   A backend API with authentication and data processing.
-   An administrative interface.
-   A Telegram bot as an additional customer interaction channel.
-   A relational database for persistent application data.
-   Containerized services for a reproducible deployment setup.

## Scope

This document describes the implemented project features at a portfolio
level. Exact behavior and availability may depend on the currently
deployed version.
