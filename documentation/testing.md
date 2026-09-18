# Testing

The Midrohub Leave Management System was tested across employee and manager workflows to verify functionality, validation, navigation, and automated leave balance updates.

## Employee Testing

- Submitted leave requests successfully.
- Verified automatic working-day calculations.
- Confirmed weekends are excluded from working-day calculations.
- Verified insufficient leave balance prevents submission.
- Confirmed employees can view pending, approved, and rejected requests.
- Verified empty-state screens display correctly when no requests exist.

## Manager Testing

- Verified managers can access the manager dashboard.
- Confirmed pending requests appear in the manager queue.
- Tested approving a leave request.
- Tested rejecting a leave request.
- Confirmed approved requests are removed from the pending queue.
- Confirmed rejected requests are removed from the pending queue.

## Leave Balance Testing

- Verified approved leave reduces the employee's remaining balance.
- Verified approved leave increases the employee's used leave.
- Confirmed entitlement remains unchanged.
- Confirmed rejected requests do not change the leave balance.

## Automation Testing

The Power Automate workflow was tested after manager approval.

Expected result:

- Leave Request status = Approved
- Used balance increases by the approved working days.
- Remaining balance decreases by the approved working days.

The workflow was successfully tested against the Dataverse Leave Balance table.
