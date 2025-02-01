# HRAnalytics-AtliQ
Real dataset for employee presence from a company called AtliQ and perform data analysis in Power BI.

![HR Analytics Dashboard](https://github.com/Niteesh011/HRAnalytics-AtliQ-/blob/main/Dashboard.png)

# DAX Queries used
// Attendance Percentage Calculation
Attendace % = 
DIVIDE([Present Days], [Office Working days], 0)

// Count of Values
Count = COUNT('Final Data'[Value])

// Home-From-Work-Home Count
HFWH Count = CALCULATE([Count], 'Final Data'[Value] = "HWFH")

// Calculation of Office Working Days
Office Working days = 
VAR totaldays = [Count]
VAR nonworkdays = CALCULATE([Count], 'Final Data'[Value] IN {"HO", "WO"})
RETURN totaldays - nonworkdays

// Calculation of Present Days
Present Days = CALCULATE([Count], 'Final Data'[Value] IN {"P", "WFH"})

// Sick Leave Percentage
SL % = DIVIDE('Measures (2)'[SL Count], [Office Working days])

// Sick Leave Count
SL Count = SUM('Final Data'[SL Count])

// Work-From-Home Percentage
WFH % = DIVIDE([WFH Count], 'Measures (2)'[Present Days], 0)

// Work-From-Home Count
WFH Count = SUM('Final Data'[WFH Count])

