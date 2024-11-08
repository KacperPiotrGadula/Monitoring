# App Insights

## CPU of Instance

```InsightsMetrics
| where _ResourceId contains "<Instance name>"
| where Name == "UtilizationPercentage"
| project TimeGenerated, Computer, UtilizationPercentage = toint(Val)
| summarize avgUtilizationPercentage = avg(UtilizationPercentage) by bin(TimeGenerated, 15m), Computer
| render timechart```