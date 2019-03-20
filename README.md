# Redis Sentinel Exporter for Prometheus

This is a simple server that scrapes Redis Sentinel stats and exports them via HTTP for Prometheus consumption.

## modify
```
add the Metric:
- redis_sentinel_master_address{name="xxxx"} 1.02462832e+08
  use the float64 for the master address. like 1.02462832 be the ip address: 10.246.28.32
  
so we can use the alert rules to notice the failover
- name: failover_master
  rules:
  - alert: redis_failover
    expr: changes(redis_sentinel_master_address[2m]) > 0
    labels:
      severity: notification
    annotations:
      description: "Master {{$labels.name}} have been failover {{$value}}" 
      summary: "Master {{$labels.name}} Failover. "
```
## Getting Started

To run it:

```
./redis_sentinel_exporter [flags]
```

Help on flags:

```
./redis_sentinel_exporter --help
```

## Links

* [Grafana Dashboard](https://grafana.com/dashboards/9570)
