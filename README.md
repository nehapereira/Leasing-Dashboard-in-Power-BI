# Leasing-Dashboard-in-Power-BI

## Dataset: On data.world. Will put the file in the repository. The second table was made so I can learn Excel and Data Modeling in Power BI. 

## Problem Statement

In the dynamic and competitive real estate leasing market, property management companies often struggle with efficiently managing and visualizing extensive leasing data. Challenges include tracking various metrics such as occupancy rates, financial performance across different properties, and lease renewal statuses. 
Traditional methods can lead to delayed decision-making and missed opportunities due to the inability to quickly access and interpret key data points. 
This complexity requires a solution that not only consolidates and simplifies data access but also enhances the ability to make informed decisions promptly.

## DAX Measures

Active Leases = CALCULATE(COUNT('Lease Dataset'[Tenant Name])+0,'Lease Dataset'[Effective Date]<=MAX('Date'[Date]) && 'Lease Dataset'[Scheduled Termination Date]>MAX('Date'[Date]))

Gross Leasable Area % = [Occupied Units]/[Total Units]

New Leases = Var _Max = max('Date'[Date]) 
VAR Result=CALCULATE(COUNTROWS('Lease Dataset')+0,YEAR('Lease Dataset'[Effective Date])=YEAR(MAX('Date'[Date])))
return Result

Occupied Units = Var _Max = max('Date'[Date]) 
VAR Result=CALCULATE(DISTINCTCOUNT('Lease Dataset'[Unit Code]) + 0, 'Lease Dataset'[Effective Date]<=_Max && 'Lease Dataset'[Scheduled Termination Date]>=_Max)
return Result

Rent per Sq. m = DIVIDE(SUM('Lease Dataset'[Annual Rent]),SUM('Lease Dataset'[Area (sq. m)]),0)

Total Annual Rent = SUM('Lease Dataset'[Annual Rent])

Total Units = COUNT('Unit Code'[Unit Num]) + 0

Vacant Units = [Total Units]-[Occupied Units]
