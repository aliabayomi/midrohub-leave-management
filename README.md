# Midrohub Leave Management System

A Power Apps and Dataverse leave management system designed to streamline employee leave requests, manager approvals, leave balance tracking, and automated entitlement updates.

## Project Overview

The Midrohub Leave Management System is a business-focused application built with Microsoft Power Platform.

It provides employees with a simple interface to submit and track leave requests, while managers can review pending requests and approve or reject them. Approved leave automatically updates the employee's leave balance through Power Automate.

## Business Problem

Traditional leave management processes can rely heavily on emails, spreadsheets, and manual calculations. This can make it difficult to:

- Track employee leave requests
- Manage approval workflows
- Maintain accurate leave balances
- Prevent employees from requesting more leave than they have available
- Give employees visibility of their request history

This project addresses these challenges through a centralised Power Platform solution.

## Key Features

### Employee Features

- Employee dashboard
- Leave balance overview
- Submit leave requests
- Automatic working-day calculation
- Leave balance validation
- View pending requests
- View approved requests
- View rejected requests
- View request details and status

### Manager Features

- Manager dashboard
- View pending team leave requests
- Review individual leave requests
- Approve leave requests
- Reject leave requests
- View approved requests
- View rejected requests
- Empty-state screens when no requests are available

### Automation

Power Automate is used to automate leave entitlement updates.

When a leave request is approved:

- Leave Used is increased by the approved working days
- Leave Remaining is decreased by the approved working days
- Leave Entitlement remains unchanged

Rejected requests do not affect the employee's leave balance.

## Technology Stack

| Technology | Purpose |
|---|---|
| Microsoft Power Apps | Application interface and user experience |
| Microsoft Dataverse | Data storage and relational data model |
| Power Automate | Approval-related automation and leave balance updates |
| Power Fx | Business logic, validation and navigation |

## Dataverse Data Model

The solution uses Dataverse tables to manage the core business data, including:

- Employees
- Leave Requests
- Leave Balances
- Leave Types
- Departments
- Public Holidays
- Approval History

Relationships between these tables allow employee information, leave requests and leave balances to be managed within a structured data model.

## Business Rules

The application includes several business rules:

1. Employees must have a leave balance for the relevant leave year.
2. Requested working days cannot exceed the employee's remaining leave balance.
3. Working days are calculated automatically from the selected start and end dates.
4. Weekends are excluded from working-day calculations.
5. Managers can approve or reject pending requests.
6. Approved requests update the employee's leave balance automatically.
7. Rejected requests do not reduce the employee's leave balance.

## Application Workflow

```text
Employee submits leave request
              |
              v
       Leave Request
              |
              v
     Manager Pending Queue
              |
        +-----+-----+
        |           |
     Approve      Reject
        |           |
        v           v
 Update Leave    No Balance
   Balance        Change
        |
        v
  Approved Request
