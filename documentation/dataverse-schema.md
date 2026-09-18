# Dataverse Schema

The Midrohub Leave Management System uses Microsoft Dataverse as its central data layer.

## Core Tables

| Table | Purpose |
|---|---|
| Employees | Stores employee information and manager relationships. |
| Leave Requests | Stores employee leave applications, dates, leave type, reason, status, and working days. |
| Leave Balances | Tracks annual entitlement, leave used, and remaining leave. |
| Leave Types | Defines the available leave categories. |
| Departments | Stores organisational department information. |
| Public Holidays | Supports holiday-related leave calculations and management. |
| Approval History | Provides a record of leave approval activity. |

## Key Relationships

- **Employees → Leave Requests:** An employee can submit multiple leave requests.
- **Employees → Leave Balances:** Each employee has a leave balance for the relevant leave year.
- **Employees → Manager:** Employees can be associated with a manager to support the approval process.
- **Leave Requests → Leave Types:** Each request is associated with a specific leave type.

## Leave Request Data

The Leave Requests table captures:

- Employee
- Leave Type
- Start Date
- End Date
- Reason
- Status
- Working Days
- Leave Request Number

Working days are calculated automatically in Power Apps, with weekends excluded from the calculation.

## Leave Balance Management

Leave balances contain:

- Employee
- Leave Year
- Entitlement
- Used
- Remaining

When a leave request is approved, Power Automate updates the employee's **Used** and **Remaining** balance automatically.

Rejected requests do not reduce the employee's leave balance.
