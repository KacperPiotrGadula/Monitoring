# Azure Metrics

## CosmosDB Avability

```
AzureMetrics 
| where MetricName has "ServiceAvailability"
| project TimeGenerated, ServiceAvailability = toint(Total)
| summarize avgUtilizationPercentage = avg(ServiceAvailability) by bin(TimeGenerated, 5m)
| render timechart  
```

## Service Bus Request InComing

```
AzureMetrics
| where MetricName == "IncomingRequests"
| summarize AverageValue = avg(Total) by bin(TimeGenerated, 10m)
| project TimeGenerated, AverageValue
| render timechart
```