# App Insights

## CPU of Instance

```
InsightsMetrics
| where _ResourceId contains "<Instance_name>"
| where Name == "UtilizationPercentage"
| project TimeGenerated, Computer, UtilizationPercentage = toint(Val)
| summarize avgUtilizationPercentage = avg(UtilizationPercentage) by bin(TimeGenerated, 15m), Computer
| render timechart
```

## Free Memory of instance

```
InsightsMetrics
| where _ResourceId contains "<Instance_name>"
| where Name == "AvailableMB"
| project TimeGenerated, Computer, AvailableMB = toint(Val)
| summarize AvgAvailableMB = avg(AvailableMB) by bin(TimeGenerated, 15m), Computer
| render timechart
```

## Free Diskspace for Instance

```
InsightsMetrics
| where _ResourceId contains "<Instance_name>"
| where Name == "FreeSpacePercentage"
| project TimeGenerated, Computer, FreeSpacePercentage = toint(Val)
| summarize avgFreeSpacePercentage = avg(FreeSpacePercentage) by bin(TimeGenerated, 15m), Computer
| render timechart
```