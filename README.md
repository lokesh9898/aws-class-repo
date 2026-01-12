# PMM Grafana Alerts

This repository contains Grafana unified alerting rules for monitoring MySQL using PMM (Percona Monitoring and Management).

---

## Overview

The goal of this project is to:
- Manage Grafana alert rules using Terraform
- Monitor MySQL metrics exposed by PMM
- Use Grafana Unified Alerting (Grafana 11.x)

---

## Architecture

```

MySQL
↓
mysqld_exporter (PMM)
↓
Prometheus / Mimir
↓
Grafana Alerts

```

---

## Prerequisites

- Grafana >= 11.x
- PMM Server >= 3.x
- Terraform >= 1.5
- Prometheus datasource configured in Grafana
- MySQL exporter version >= 0.17.2

---

## Repository Structure

```

.
├── main.tf
├── variables.tf
├── alerts.tf
├── outputs.tf
└── README.md

````

---

## Installation

```bash
terraform init
terraform plan
terraform apply
````

---

## Configuration

Example variables:

```hcl
folder_uid        = "mysql-alerts"
interval_seconds = 60
datasource_uid   = "prometheus"
```

---

## Alerts Included

* MySQL Instance Down
* MySQL Threads Running High
* MySQL Connections Usage
* MySQL Replication Lag

---

## Metrics Used

Common PMM MySQL metrics:

* mysql_up
* mysql_global_status_threads_running
* mysql_global_status_connections
* mysql_global_variables_max_connections

> Note: info_schema metrics are disabled by default in mysqld_exporter >= 0.15

---

## Validation

Check metrics:

```promql
mysql_up
```

Check alerts:

```
Grafana → Alerting → Alert rules
```

---

## Troubleshooting

**No data**

* Verify datasource UID
* Confirm exporter is running
* Check scrape interval

**Alert not firing**

* Ensure `instant = false`
* Check evaluation interval
* Validate PromQL expression

---

## Maintainer

SRE / Platform Team

---

## License

MIT License
