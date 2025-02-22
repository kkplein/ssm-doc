# Prometheus Exporters Overview

The Prometheus Exporters Overview dashboard provides the summary of how exporters are used across the selected hosts.

## Prometheus Exporters Summary

This section provides a summary of how exporters are used across the selected hosts. It includes the average usage of CPU and memory as well as the number of hosts being monitored and the total number of running exporters.

### Metrics in this section

* **Avg CPU Usage per Host** shows the average CPU usage in percent per host for all exporters.
* **Avg Memory Usage per Host** shows the Exporters average Memory usage per host.
* **Monitored Hosts** shows the number of monitored hosts that are running Exporters.
* **Exporters Running** shows the total number of Exporters running with this SSM Server instance.

!!! alert alert-info "Note"
    The CPU usage and memory usage do not include the additional CPU and memory usage required to produce metrics by the application or operating system.

## Prometheus Exporters Resource Usage by Host

This section shows how resources, such as CPU and memory, are being used by the exporters for the selected hosts.

### Metrics in this section

* **CPU Usage** plots the Exporters’ CPU usage across each monitored host (by default, All hosts).
* **Memory Usage** plots the Exporters’ Memory usage across each monitored host (by default, All hosts).

## Prometheus Exporters Resource Usage by Type

This section shows how resources, such as CPU and memory, are being used by the exporters for host types: MySQL, MongoDB, ProxySQL, and the system.

### Metrics in this section

* **CPU Cores Used** shows the Exporters’ CPU Cores used for each type of Exporter.
* **Memory Usage** shows the Exporters’ memory used for each type of Exporter.

## List of Hosts

At the bottom, this dashboard shows details for each running host.

* **CPU Used** show the CPU usage as a percentage for all Exporters.
* **Mem Used** shows total Memory Used by Exporters.
* **Exporters Running** shows the number of Exporters running.
* **RAM** shows the total amount of RAM of the host.
* **Virtual CPUs** shows the total number of virtual CPUs on the host.

You can click the value of the CPU Used, Memory Used, or Exporters Running column to open the Prometheus Exporter Status for further analysis.
