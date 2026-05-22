# Enterprise Service Desk Platform: Production-Ready osTicket Deployment

A production-style help desk ticketing system built with **osTicket** for a fictional company, **Fly MSSP**.  
This project demonstrates the deployment, configuration, operation, and monitoring of an IT support ticketing platform in a local virtualized Linux environment.

---

## System Architecture

<!-- Add System Architecture Image Here -->

--- 

## Project Overview

This repository documents the setup of an enterprise service desk platform using osTicket. The goal of the project was to simulate a real IT support environment where users can open tickets, agents can investigate and respond, and administrators can monitor, verify, and close resolved issues.

The project includes server setup, database configuration, osTicket installation, department and agent configuration, SLA creation, SMTP email setup, ticket lifecycle simulation, and system log analysis.

---

## Key Features Implemented

- Deployed osTicket on an Ubuntu virtual machine
- Configured Apache, MySQL, PHP, and required PHP extensions
- Created a dedicated MySQL database and database user for osTicket
- Set up an admin account and customized helpdesk identity
- Created departments for structured ticket routing
- Created agents and assigned them to departments
- Created help topics to categorize user issues
- Configured SLAs with different response times based on priority
- Configured Gmail SMTP for email notifications
- Opened test tickets through multiple simulated customers
- Responded to tickets through agent accounts
- Verified and closed resolved tickets through the admin account
- Monitored ticket activity through the osTicket dashboard
- Reviewed warning logs such as failed login attempts and invalid CSRF token alerts

---

## Technologies Used

- Ubuntu 24.04
- Oracle VirtualBox
- Apache Web Server
- MySQL
- PHP
- PHP Extensions
- osTicket
- Gmail SMTP
- Local Area Network Deployment

---

## Deployment Summary

### 1. Server and Web Stack Setup

The project began with the installation and configuration of the core LAMP stack:

- Apache was installed and tested using the default Apache landing page.
- MySQL was installed and configured.
- PHP and required extensions were installed to satisfy osTicket requirements.
- Apache was configured to serve the osTicket application.

### 2. Database Configuration

A dedicated MySQL database and user were created for osTicket. This avoids using the MySQL root account for the application and follows better security practice.

Example database components:

```sql
CREATE DATABASE osticket;
CREATE USER 'osticket_user'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON osticket.* TO 'osticket_user'@'localhost';
FLUSH PRIVILEGES;
```

### 3. osTicket Installation

osTicket was downloaded, extracted, and deployed under the Apache web directory. The installer was completed through the browser by configuring:

- Helpdesk URL
- Helpdesk name
- Default email address
- Admin user account
- Database connection details

After installation, the setup directory was removed and configuration file permissions were secured.

---

## osTicket Configuration

### Departments

Three departments were created to separate support responsibilities:

- General IT Support
- Network Operations
- Security Operations

Departments were used to route tickets based on the selected help topic.

### Agents

Multiple agents were created and assigned to departments. This allowed tickets to be viewed and handled by the correct support personnel based on department access.

### Help Topics

Help topics were created for common business support issues, including:

- Account Access
- Feedback
- Network Issue
- Password Reset
- Printer Problem
- Server Down

Each help topic was mapped to an appropriate department and priority so that tickets could be routed consistently.

### Service Level Agreements

Four SLA levels were configured to simulate business response expectations:

| SLA Name | Grace Period | Purpose |
|---|---:|---|
| Emergency | 1 hour | Critical issues such as server downtime |
| High Priority | 4 hours | Serious issues affecting user access or security |
| Normal Priority | 24 hours | Routine support requests |
| Low Priority | 48 hours | Non-urgent requests and feedback |

SLAs helped define when tickets should be treated as urgent or overdue.

### Security Settings

A lockout policy was configured for agent authentication. If failed login attempts exceed the defined limit, the account is temporarily locked for security.

Configured example:

```text
Failed login attempts allowed: 5
Lockout duration: 2 minutes
```

---

## Email Configuration

Gmail SMTP was configured so osTicket could send automatic email notifications to users.

Email notifications were used for:

- Ticket creation confirmation
- Ticket number delivery
- Ticket tracking link
- Agent responses
- Customer follow-ups

This solved the issue of users needing a ticket number later by ensuring the ticket number and tracking link are delivered by email after ticket creation.

---

## Ticket Lifecycle Simulation

The project simulated a realistic support workflow:

1. A customer opened a support ticket.
2. The customer selected a help topic.
3. osTicket assigned the ticket to the correct department.
4. An agent reviewed the ticket from the Agent Panel.
5. The agent replied with a resolution or troubleshooting steps.
6. The customer could view the ticket using their email and ticket number.
7. The admin verified the resolution.
8. The admin closed the ticket.

Six tickets were created using different simulated customers to demonstrate high-volume queue handling and ticket categorization.

Example simulated issues:

- Locked account
- Bad UI/UX feedback
- Slow network speed
- Weak password reset request
- Printer down
- Website returning HTTP 500

---

## Monitoring and Log Analysis

The osTicket dashboard was used to monitor ticket activity, including:

- Opened tickets
- Assigned tickets
- Closed tickets
- Deleted tickets
- Department-level statistics
- Help-topic-level statistics
- Agent activity

System logs were also reviewed to investigate warnings. Examples included:

- Failed user login attempts
- Invalid CSRF token warnings
- Mailer errors

The warning logs were analyzed using timestamp and IP address to determine whether they represented suspicious activity, configuration issues, or false positives.

---

## Skills Demonstrated

- Linux server administration
- LAMP stack deployment
- Web application deployment
- MySQL database setup
- PHP extension troubleshooting
- osTicket configuration
- SMTP email integration
- Ticket queue management
- SLA design
- Role-based access control
- System log analysis
- IT support workflow simulation
- Incident triage and resolution tracking

---

## Disclaimer

This environment is:

- Non-production
- Isolated
- Intended for educational and demonstration purposes
- No real organizational data is used.
