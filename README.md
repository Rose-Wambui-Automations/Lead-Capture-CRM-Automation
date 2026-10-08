# Lead-Capture-CRM-Automation
The system captures leads through a web form, checks whether the lead already exists, stores new leads in a PostgreSQL database, sends an internal email notification, and automatically acknowledges the lead by email.

https://www.tella.tv/video/lead-automation-workflow-tutorial-e9k9



## Overview

A local, end-to-end lead management automation built with **n8n, PostgreSQL, and Docker**.

The system captures leads through a web form, checks whether the lead already exists, stores new leads in a PostgreSQL database, sends an internal email notification, and automatically acknowledges the lead by email.

The project demonstrates how repetitive lead-management tasks can be automated without relying on spreadsheets or expensive CRM platforms.

## Workflow

```text
Lead Capture Form
        ↓
Duplicate Check
        ↓
      IF
   ↙       ↘
Duplicate   New Lead
   ↓           ↓
  Stop     PostgreSQL
              ↓
       Internal Email
              ↓
       Lead Auto-Reply
```

## Key Features

### 1. Lead Capture

A form built with the **n8n Form Trigger** collects:

* Full Name
* Email
* Phone Number
* Company Name
* Service of Interest

### 2. Duplicate Detection

Before creating a new record, the workflow checks PostgreSQL for an existing lead using the submitted email address.

If a matching email already exists, the workflow stops the duplicate submission from being inserted.

### 3. PostgreSQL CRM Storage

New leads are stored in a local PostgreSQL database containing information such as:

* Lead ID
* Name
* Email
* Phone
* Company
* Service
* Creation timestamp

PostgreSQL functions as the project's lightweight CRM/data store.

### 4. Internal Notification

When a new lead is successfully stored, n8n automatically sends an email notification to the internal team.

This removes the need for someone to manually monitor the form for new submissions.

### 5. Automated Lead Acknowledgement

The system automatically sends an acknowledgement email to the lead after successful processing.

This provides an immediate response while allowing the business team to handle the lead manually afterward.

---

# Tools & Technologies

| Tool                 | Purpose                                          |
| -------------------- | ------------------------------------------------ |
| **n8n**              | Workflow automation and orchestration            |
| **n8n Form Trigger** | Lead capture                                     |
| **PostgreSQL**       | Lead database / CRM storage                      |
| **Docker**           | Containerization                                 |
| **Docker Compose**   | Managing the PostgreSQL container                |
| **SQL**              | Duplicate checking and database operations       |
| **Email / SMTP**     | Internal notifications and lead acknowledgements |
| **Ubuntu / WSL2**    | Local development environment                    |
| **Windows**          | Host operating system                            |

---

# Why This Project Matters

Many small businesses receive leads through forms, websites, social media, or landing pages but still handle the follow-up process manually.

This automation demonstrates how that process can be streamlined:

**Before**

```text
Lead submits form
       ↓
Someone checks submissions
       ↓
Someone checks for duplicates
       ↓
Someone records the lead
       ↓
Someone emails the team
       ↓
Someone replies to the lead
```

**After**

```text
Lead submits form
       ↓
       n8n
       ↓
Duplicate check
       ↓
Database
       ↓
Notification
       ↓
Automatic acknowledgement
```

The result is less repetitive administrative work, faster acknowledgement, and a centralized lead record.

---

# Who This Automation Applies To

This workflow can be adapted for many organizations that receive inbound leads.

### Small Businesses

Useful for businesses receiving inquiries through websites or landing pages.

Examples:

* Consulting companies
* Marketing agencies
* IT service providers
* Accounting firms
* Recruitment agencies
* Cleaning companies
* Construction companies
* Real estate businesses

### Healthcare Organizations

The same architecture can be adapted for appropriate healthcare workflows, provided that the implementation is designed for **HIPAA/privacy requirements** and uses suitable infrastructure and services.

Potential applications include:

* Patient inquiry routing
* Insurance verification requests
* Appointment inquiry intake
* Provider referral intake
* Medical billing service inquiries

### Professional Services

Useful for organizations where every inquiry needs to be recorded and followed up.

Examples:

* Law firms
* Insurance agencies
* Financial service providers
* Business consultants
* Virtual assistant agencies

### Agencies

An agency could use the workflow to automatically capture prospects, identify repeat inquiries, notify the sales team, and acknowledge new prospects.

---

# Alternative Tools

The project currently uses a deliberately simple local stack, but the same workflow can be built using different tools.

## Lead Capture Alternatives

Instead of the n8n Form Trigger:

* Typeform
* Tally
* Jotform
* Webflow Forms
* WordPress Forms
* HubSpot Forms
* Custom HTML forms
* Website webhooks

## Database / CRM Alternatives

Instead of PostgreSQL:

* HubSpot CRM
* Salesforce
* Zoho CRM
* Pipedrive
* MySQL
* MariaDB
* Supabase
* Airtable

PostgreSQL was selected for this project because it provides a real relational database while keeping the project local and under direct control.

## Notification Alternatives

Instead of email:

* Slack
* Microsoft Teams
* Discord
* Telegram
* SMS
* WhatsApp Business
* Microsoft Outlook

## Automation Alternatives

Instead of n8n:

* Zapier
* Make
* Power Automate
* Pipedream
* Workato

n8n was selected because it supports self-hosted/local automation and provides considerable flexibility for technical workflows.

---

# Example Business Use Case

Imagine a small medical billing company receives inquiries from potential clients.

A prospect submits:

```text
Name: John Smith
Email: john@example.com
Company: ABC Medical Group
Service: Medical Billing
```

The automation:

1. Receives the submission.
2. Checks whether the email already exists.
3. If it is a duplicate, stops processing.
4. If it is a new lead, creates a database record.
5. Sends an internal notification.
6. Sends an acknowledgement to the prospect.

A human employee can then focus on **qualifying and converting the lead instead of performing repetitive administrative tasks.**

---

# Technical Architecture

```text
                    ┌──────────────────┐
                    │   Lead submits   │
                    │      form        │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │  n8n Form        │
                    │     Trigger      │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │ Duplicate Check  │
                    │   PostgreSQL     │
                    └────────┬─────────┘
                             │
                       ┌─────┴─────┐
                       │           │
                    Duplicate    New Lead
                       │           │
                       ▼           ▼
                     STOP    ┌──────────────┐
                             │  PostgreSQL  │
                             │    INSERT    │
                             └──────┬───────┘
                                    │
                                    ▼
                             ┌──────────────┐
                             │ Internal     │
                             │ Email Alert  │
                             └──────┬───────┘
                                    │
                                    ▼
                             ┌──────────────┐
                             │ Lead Auto-   │
                             │   Reply      │
                             └──────────────┘
```

---

# Deployment

The project was developed locally using:

* Windows
* WSL2
* Ubuntu
* Docker
* Docker Compose
* n8n
* PostgreSQL

This makes the project suitable for local development, demonstrations, and portfolio purposes.

For production deployment, additional considerations would include:

* Authentication
* HTTPS
* Secure credential management
* Database backups
* Monitoring
* Error handling
* Logging
* Rate limiting
* Data retention policies
* Access control
* Privacy/security requirements

---

# Future Improvements

Potential Version 2 improvements include:

* Add a CRM such as HubSpot
* Add Slack or Microsoft Teams notifications
* Add lead scoring
* Add automatic lead assignment
* Add follow-up reminders
* Add error handling and retry workflows
* Add an admin dashboard
* Add analytics and reporting
* Add AI-powered lead classification
* Automatically categorize leads by service
* Automatically summarize lead inquiries
* Route high-value leads to specific team members

## Future AI Enhancement

The workflow could eventually include an AI layer:

```text
Lead Form
    ↓
Duplicate Check
    ↓
AI Lead Classification
    ↓
Lead Scoring
    ↓
PostgreSQL / CRM
    ↓
Intelligent Routing
    ↓
Notification
    ↓
Personalized Auto-Reply
```

For example, an AI model could analyze a lead's message and classify it as:

* High priority
* Medium priority
* Low priority

It could also identify the service requested and generate a more personalized acknowledgement.

---

# Project Objective

The primary objective of this project was to demonstrate practical automation skills by replacing a repetitive manual lead-management process with an automated workflow.

It demonstrates experience with:

* Workflow orchestration
* API/integration concepts
* Relational databases
* SQL
* Conditional logic
* Data persistence
* Email automation
* Docker
* Local infrastructure
* Business process automation

---

## Project Status

**Version:** 1.0

**Status:** Completed and tested locally.

**Core workflow:** Fully operational.

**Environment:** Local / self-hosted development environment.
