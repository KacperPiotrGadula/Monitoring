# Monitoring K8S

## Listing of name space with podow status and age

```
KubePodInventory
| summarize arg_max(TimeGenerated, *) by Namespace
| project Namespace, PodStatus, AgeInSecond = tostring(datetime_diff('second', now(), TimeGenerated))
```

## Listing of node pools with statuses and times

```
KubeNodeInventory
| where ClusterName == "<cluster_name>"
| summarize arg_max(TimeGenerated, *) by Computer
| project
    Computer,
    PowerState = case(Status == "Ready", "Running", "Not Running"),
    Time_Date = format_datetime(TimeGenerated, 'ss:mm:HH dd/MM/yyyy')
```

## Extracting project Name, Namespace, PodStatus, ContainerStatus, AgeInDays from workloads:

```
KubePodInventory
| where ClusterName == "<cluster_name>"
| project Name, Namespace, PodStatus, ContainerStatus, AgeInDays = datetime_diff('day', now(), PodCreationTimeStamp)
```

## Listing the current status of all unique ingress instances

```
KubePodInventory
| search "ingress"
| where ClusterName == "<cluster_name>"
| summarize arg_max(TimeGenerated, *) by Name, Namespace
| project Name, Namespace, PodIp, PodStatus, Time_Date = format_datetime(TimeGenerated, 'ss:mm:HH dd/MM/yyyy')
```

## Lists the current status of all unique instances of services

```
KubePodInventory
| search "service"
| where ClusterName == "<cluster_name>"
| summarize arg_max(TimeGenerated, *) by Name, Namespace
| project Name, Namespace, PodIp, PodStatus, Time_Date = format_datetime(TimeGenerated, 'ss:mm:HH dd/MM/yyyy')
```