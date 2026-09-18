# Power Automate

The Midrohub Leave Management System uses Microsoft Power Automate to automate leave entitlement updates after a manager makes a decision.

## Leave Entitlement Approval Update

The main automation is:

**Leave Entitlement Approval Update**

The flow is triggered when a Leave Request record is modified in Microsoft Dataverse.

### Trigger

The flow uses the Dataverse trigger:

**When a row is added, modified or deleted**

Configuration:

- Change type: Modified
- Table: Leave Requests
- Scope: Organization
- Selected column: Status

## Approval Logic

The flow checks whether the Leave Request has been approved.

### If Approved

When the request status is **Approved**:

1. The employee's Leave Balance record is identified.
2. The approved working days are retrieved from the Leave Request.
3. **Used** leave is increased by the approved working days.
4. **Remaining** leave is decreased by the approved working days.
5. **Entitlement** remains unchanged.

Conceptually:

**New Used = Current Used + Approved Working Days**

**New Remaining = Current Remaining − Approved Working Days**

### If Rejected

When the request is rejected:

- The employee's leave balance is not changed.
- No leave days are deducted.

## Automation Flow

```text
Leave Request Modified
        |
        v
Check Status
        |
   +----+----+
   |         |
Approved   Rejected
   |         |
   v         v
Find Leave  No Balance
Balance     Change
   |
   v
Update Used
and Remaining
