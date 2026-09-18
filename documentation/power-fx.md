# Power Fx

Power Fx is used throughout the application to implement business rules, calculations, validation, navigation, and user-specific views.

## Working-Day Calculation

The application automatically calculates working days between the selected start and end dates.

Weekends are excluded from the calculation.

```powerfx
With(
    {
        StartDate: DateValue3.SelectedDate,
        EndDate: DateValue4.SelectedDate
    },
    If(
        EndDate < StartDate,
        Blank(),
        CountRows(
            Filter(
                Sequence(DateDiff(StartDate, EndDate) + 1),
                Weekday(
                    DateAdd(StartDate, Value - 1, TimeUnit.Days),
                    StartOfWeek.Monday
                ) <= 5
            )
        )
    )
)
```
## Leave Balance Validation
Before a leave request is submitted, Power Apps checks whether the employee has sufficient remaining leave.

```powerfx
With(
    {
        leaveBalance: LookUp(
            'Leave Balances',
            Employee.'Employee Name' = frmLeaveRequest.Updates.Employee.'Employee Name' &&
            'Leave Year' = Year(frmLeaveRequest.Updates.'Start Date')
        ),
        requestedDays: Value(frmLeaveRequest.Updates.'Working Days')
    },
    If(
        IsBlank(leaveBalance),
        Notify(
            "No leave balance found for this employee.",
            NotificationType.Error
        ),
        requestedDays > leaveBalance.Remaining,
        Notify(
            "Insufficient leave balance. You have " &
            leaveBalance.Remaining &
            " days remaining.",
            NotificationType.Error
        ),
        SubmitForm(frmLeaveRequest)
    )
)
```
## Leave Balance Validation
Before a leave request is submitted, Power Apps checks whether the employee has sufficient remaining leave.
## Approve
```powerfx
Patch(
    'Leave Requests',
    varSelectedRequest,
    {
        Status: 'Status (Leave Requests)'.Approved
    }
)
```

## Reject
```powerfx
Patch(
    'Leave Requests',
    varSelectedRequest,
    {
        Status: 'Status (Leave Requests)'.Rejected
    }
)
```
User-Specific Views

The application uses
```
User().FullName
```
 and Dataverse relationships to display the appropriate requests and leave information for the logged-in employee.
