# Solution Architecture

The Midrohub Leave Management System uses Microsoft Power Platform to provide a centralised and automated leave management process.

## Architecture Components

### Power Apps
A Canvas App provides the user interface for employees and managers.

- Employees submit and track leave requests.
- Employees view their leave balances and request history.
- Managers review pending requests.
- Managers approve or reject leave requests.
- Role-based navigation provides different experiences for employees and managers.

### Microsoft Dataverse
Dataverse provides the central data layer for the application.

Key tables include:

- Employees
- Leave Requests
- Leave Balances
- Leave Types
- Departments
- Public Holidays
- Approval History

### Power Automate
Power Automate handles the automated leave entitlement update process.

When a leave request is approved, the workflow:

1. Identifies the employee's leave balance.
2. Adds the approved working days to Leave Used.
3. Deducts the approved working days from Leave Remaining.

Rejected requests do not change the employee's leave balance.

## Process Flow

Employee → Power Apps → Dataverse → Manager Review → Approval Decision → Power Automate → Updated Leave Balance

## Business Outcome

The solution replaces manual leave tracking with a centralised application that improves visibility, reduces manual calculations, supports manager approvals, and maintains accurate leave balances.
