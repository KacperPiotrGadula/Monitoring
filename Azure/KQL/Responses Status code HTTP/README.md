# Responses Status Code HTTP 20*, 40*, 50*

## Create https response code from http in timechart for one endpoint

```
AppDependencies
| where Target !contains ":"
| where DependencyType contains "HTTP"
| where ResultCode !has "Faulted" and ResultCode !has "Canceled"
| where Target contains "FQDN of endpoints" //url of endpoint with you would like to resoltce code monitoring
| where substring(ResultCode, 0, 1) in ("2", "4", "5")
| extend CodeCategory = case(
    substring(ResultCode, 0, 1) == "2","20*",
    substring(ResultCode, 0, 1) == "4","40*",
    substring(ResultCode, 0, 1) == "5","50*",
    "Other"
    )
| summarize Count = count() by bin(TimeGenerated, 1m), CodeCategory
| project TimeGenerated, Count, CodeCategory
| render timechart
```

## Create table with responce status code for one endpoint

```
AppDependencies
| where Target !contains ":"
| where DependencyType contains "HTTP"
| where ResultCode !has "Faulted" and ResultCode !has "Canceled"
| where Target contains "FQDN of endpoints" ////url of endpoint with you would like to resoltce code monitoring
| summarize Count = dcount(Data) by Target, ResultCode, Data, TimeGenerated
| sort by TimeGenerated desc 
```

## Check full of endpoint for tool

```
AppDependencies
| where Target !contains ":"
| where DependencyType contains "HTTP"
| where ResultCode !has "Faulted" and ResultCode !has "Canceled"
| summarize Count = dcount(Data) by Target, ResultCode
| order by Target, ResultCode
| sort by Count desc
```