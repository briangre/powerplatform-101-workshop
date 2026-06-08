# Power Platform 101 — Hands-On Training Workshop

> **Duration:** 4 Hours | **Level:** Beginner | **Format:** Lecture + Hands-On Labs

## Workshop Overview

This workshop introduces the Microsoft Power Platform through a practical, hands-on approach. Attendees will learn the fundamentals of **Canvas Apps**, **Model-Driven Apps**, **Power Automate Cloud Flows**, and **Dataverse** by building a real-world business process: a **Beneficiary Change Request** workflow.

By the end of this workshop, attendees will have built a working solution that:

- Provides an internal intake and processing dashboard for incoming requests (Canvas App)
- Provides an internal review and approval experience (Model-Driven App)
- Automates notifications and status updates when requests are submitted (Power Automate)
- Stores all data in a structured, secure database (Dataverse)

## Who Is This For?

Professionals looking to convert legacy workflow processes (paper forms, email chains, spreadsheets, manual approvals) into modern Power Platform solutions. No prior Power Platform experience required.

## Agenda

| Time | Duration | Module | Type |
|------|----------|--------|------|
| 0:00 | 30 min | [Platform Overview Lecture](01-lecture-platform-overview/README.md) | 📖 Lecture |
| 0:30 | 20 min | [Environment Setup & Navigation](02-lab-environment-setup/README.md) | 🔧 Setup |
| 0:50 | 40 min | [Lab 1: Dataverse Tables & Data Model](03-lab-dataverse-tables/README.md) | 💻 Hands-On |
| 1:30 | 40 min | [Lab 2: Model-Driven App (Review & Approval)](04-lab-model-driven-app/README.md) | 💻 Hands-On |
| 2:10 | 10 min | ☕ **Break** | — |
| 2:20 | 45 min | [Lab 3: Canvas App (Intake & Processing)](05-lab-canvas-app/README.md) | 💻 Hands-On |
| 3:05 | 30 min | [Lab 4: Power Automate (Notifications & Automation)](06-lab-power-automate/README.md) | 💻 Hands-On |
| 3:35 | 15 min | [Lab 5: End-to-End Testing](07-lab-end-to-end-testing/README.md) | 💻 Hands-On |
| 3:50 | 10 min | Wrap-Up, Q&A, & Next Steps | 📖 Discussion |

## Prerequisites

See [Prerequisites](00-prerequisites/README.md) for environment and access requirements.

## Business Scenario: Beneficiary Change Request

> ⚠️ **Training purposes only.** All data used in this workshop is fictional. No real client or beneficiary information should be entered.

A client needs to update the beneficiary on their account. Today this process involves:
- The client sends an email (or paper form) requesting a beneficiary change
- An internal team member manually reads the email and enters the data into a spreadsheet or legacy system
- The request is forwarded via email to a reviewer for approval
- Manual status tracking via email threads
- Email confirmation back to the client

**In this workshop, we'll modernize this entire process using Power Platform.**

## Repository Structure

```
├── 00-prerequisites/          # Setup requirements
├── 01-lecture-platform-overview/  # Lecture outline & talking points
├── 02-lab-environment-setup/  # Environment navigation & solution setup
├── 03-lab-dataverse-tables/   # Lab 1: Build the data model
├── 04-lab-model-driven-app/   # Lab 2: Build the review experience
├── 05-lab-canvas-app/         # Lab 3: Build the intake & processing dashboard
├── 06-lab-power-automate/     # Lab 4: Build automation flows
├── 07-lab-end-to-end-testing/ # Lab 5: Test the full process
├── facilitator-guide/         # Instructor notes & timing
├── resources/                 # Reference links, sample data, images
└── solutions/                 # Starter & completed solution exports
```

## Facilitator Guide

Instructors should review the [Facilitator Guide](facilitator-guide/README.md) before delivering this workshop.
