# Adobe Acrobat Sign Integration with Spring MVC, Activiti BPMN, Apache Camel, Groovy & FreeMarker

## Overview

This project demonstrates how to integrate **Adobe Acrobat Sign** into an enterprise Java application built with **Spring MVC**, **Activiti BPMN**, **Apache Camel**, **Groovy**, **FreeMarker (FTL)**, **JavaScript/jQuery**, and **Java**.

The integration is designed as a **workflow-driven solution**, where Adobe Acrobat Sign becomes part of the overall business process rather than just another REST API.

The implementation supports complete document lifecycle management, including PDF generation, agreement creation, embedded or email-based signing, webhook processing, workflow resumption, signed document retrieval, and archival.

---

# Architecture

```
                   User
                     │
               Spring MVC
                     │
            Activiti BPMN Process
                     │
        Service Task (Java/Groovy)
                     │
        Apache Camel Route (Optional)
                     │
        Adobe Acrobat Sign REST API
                     │
      ┌──────────────┴──────────────┐
      │                             │
 Agreement Created          Webhook Callback
      │                             │
      │                    Spring MVC Endpoint
      └──────────────┬──────────────┘
                     │
             Resume Activiti Workflow
                     │
           Download Signed Document
                     │
                 Archive PDF
```

---

# Features

* Adobe Acrobat Sign REST API integration
* OAuth authentication
* PDF upload as transient documents
* Agreement creation
* Embedded signing support
* Email-based signing support
* Activiti BPMN workflow orchestration
* Groovy service task integration
* Apache Camel routing
* Webhook event handling
* Agreement status tracking
* Download completed signed documents
* Database persistence
* FreeMarker-based PDF generation
* JavaScript/jQuery status updates
* Enterprise-ready layered architecture

---

# Technology Stack

## Backend

* Java
* Spring MVC
* Activiti BPMN
* Apache Camel
* Groovy
* FreeMarker (FTL)

## Frontend

* HTML
* JavaScript
* jQuery

## Adobe Services

* Adobe Acrobat Sign REST API
* OAuth Authentication
* Webhooks

## Storage

* MySQL / PostgreSQL
* File System
* Amazon S3 (optional)
* Azure Blob Storage (optional)

---

# End-to-End Workflow

1. User submits a request.
2. Spring MVC starts the Activiti workflow.
3. PDF is generated from a FreeMarker template.
4. PDF is uploaded to Adobe Acrobat Sign.
5. Agreement is created.
6. Agreement ID is stored in Activiti process variables and the database.
7. Workflow enters a wait state.
8. Signer completes the document.
9. Adobe sends a webhook callback.
10. Spring MVC receives the callback.
11. Activiti resumes the workflow.
12. Signed PDF is downloaded.
13. Document is archived.
14. Workflow completes successfully.

---

# Workflow Diagram

```
User
 │
 │ Submit Request
 ▼
Spring MVC
 │
 ▼
Activiti BPMN
 │
 ▼
Generate PDF
 │
 ▼
Upload PDF
 │
 ▼
Create Adobe Agreement
 │
 ▼
Store Agreement ID
 │
 ▼
Wait State
 │
 ▼
Adobe Webhook
 │
 ▼
Resume Workflow
 │
 ▼
Download Signed PDF
 │
 ▼
Archive Document
 │
 ▼
Complete Process
```

---

# Components

## Spring MVC

Responsible for:

* User requests
* REST endpoints
* Webhook endpoints
* Status APIs

---

## Activiti BPMN

Responsible for:

* Business process orchestration
* Wait states
* Process variables
* Workflow continuation

---

## Groovy Service Tasks

Responsible for:

* Calling Spring services
* Workflow scripting
* Business logic

---

## Apache Camel

Optional integration layer providing:

* Routing
* Retry mechanisms
* Logging
* Error handling
* Queueing

---

## FreeMarker

Responsible for generating HTML templates that are converted into PDF documents.

```
FTL Template
      │
      ▼
HTML
      │
      ▼
PDF
```

---

# Adobe Acrobat Sign Integration

The application uses Adobe REST APIs for:

* OAuth Authentication
* Upload Transient Document
* Create Agreement
* Agreement Status
* Embedded Signing
* Download Signed PDF
* Webhook Events

---

# Agreement Lifecycle

```
Generate PDF
      │
Upload Document
      │
Create Agreement
      │
Receive Agreement ID
      │
Store Agreement
      │
Wait for Signature
      │
Webhook Callback
      │
Resume Workflow
      │
Download Signed PDF
      │
Archive
```

---

# Embedded Signing

Instead of sending the signer to an email link, the application can request an embedded signing URL and display the signing experience directly inside the application.

Benefits include:

* Seamless user experience
* Users remain within the application
* No manual PDF upload after signing

---

# Webhook Processing

Adobe sends webhook events such as:

* AGREEMENT_CREATED
* AGREEMENT_VIEWED
* AGREEMENT_SIGNED
* AGREEMENT_COMPLETED
* AGREEMENT_CANCELLED

The application processes these events to:

* Update agreement status
* Resume Activiti workflows
* Download completed documents
* Notify users

---

# Database Schema

Example Agreement table:

| Column              | Description              |
| ------------------- | ------------------------ |
| id                  | Primary Key              |
| employee_id         | Business reference       |
| agreement_id        | Adobe Agreement ID       |
| status              | Current agreement status |
| process_instance_id | Activiti process         |
| document_path       | Stored PDF location      |
| created_date        | Creation timestamp       |
| updated_date        | Last update timestamp    |

---

# Security

Recommended practices:

* Store OAuth credentials securely
* Never hardcode access tokens
* Use HTTPS for all endpoints
* Validate Adobe webhook signatures
* Log agreement lifecycle events
* Implement token refresh
* Apply retry logic with exponential backoff
* Make webhook processing idempotent

---

# Error Handling

The integration should gracefully handle:

* OAuth token expiration
* Upload failures
* Agreement creation failures
* Network timeouts
* Duplicate webhook events
* Adobe rate limiting
* Temporary API failures

---

# Benefits

* Fully automated document workflow
* Enterprise-grade architecture
* Workflow-driven implementation
* Secure digital signatures
* Minimal manual intervention
* Easily extendable
* Scalable integration design

---

# Typical Use Cases

* Employment Contracts
* HR Onboarding
* Vendor Agreements
* Customer Contracts
* Loan Documents
* Insurance Forms
* Compliance Documents
* Internal Approval Workflows

---

# Conclusion

This architecture provides a robust and scalable integration between Adobe Acrobat Sign and an enterprise Java application. By separating responsibilities across Spring MVC, Activiti BPMN, Apache Camel, Groovy, and FreeMarker, the solution delivers a maintainable, secure, and workflow-centric digital signature platform capable of supporting complex business processes while leveraging Adobe Acrobat Sign for legally compliant electronic signatures.
