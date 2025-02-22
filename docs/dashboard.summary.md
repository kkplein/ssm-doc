# Summary Dashboard

## CPU Usage

The CPU Usage graph shows how much of the overall CPU time is used by the server.  It has 4 components: system, user, iowait and softirq.

System
: The proportion of time the CPU spent inside the Linux kernel for operations like context switching, memory allocation and queue handling.

User
: The time spent in the user space.  Normally, most of the MySQL CPU time is in user space, a too high value may indicate an indexing issue.

Iowait
: The time the CPU spent waiting for disk IO requests to complete.  A high value of iowait indicates a disk bound load.

Softirq
: The portion of time the CPU spent servicing software interrupts generated by the device drivers.  A high value of *softirq* may indicates a poorly configured device.  The network is generally the main source of high softirq values.  Be aware the graph presents global values, while there may be a lot of unused CPU, a single core may be saturated.  Look for any quantity saturating at 100/(cpu core count).

## Processes

The Processes metric shows how many processes/threads are either in the kernel run queue (runnable state) or in the blocked queue (waiting for I/O).

When the number of process in the runnable state is constantly higher than the number of CPU cores available, the load is CPU bound.

When the number of process blocked waiting for I/O is large, the load is disk bound.

The running average of the sum of these two quantities is the basis of the loadavg metric.

## Network Traffic

The Network Traffic graph shows the rate of data transferred over the network. Outbound is the data sent by the server while Inbound is the data received by the server.

Look for signs of saturation given the capacity of the network devices. If the outbound rate is constantly high and close to saturation and you have plenty of available CPU, you should consider activating the compression option on the MySQL clients and slaves.

## I/O Activity

The I/O Activity graph shows the rates of data read from (Page In) and written to (Page Out) the all the disks as collected from the vmstat bi and bo columns.

## Disk Latency

The Disk Latency graph shows the average time to complete read an write operations to the disks.

There is one data series per operation type (Read or Write) per disk mounted to the server.

High latency values, typically more than 15 ms,  are an indication of a disk bound workload saturating the storage subsystem or, a faulty/degraded hardware.

## MySQL Queries

The MySQL Queries graph shows the rate of queries processed by MySQL.  The rate of queries is a rough indication of the MySQL Server load.

## InnoDB Row Operations

The InnoDB Row Operations graph shows the rate of rows processed by InnoDB.  It is a good indication of the MySQL Server load.  A high value of Rows read, which can easily be above a million, is an indication of poor queries or deficient indexing.

The amounts of rows inserted, updated and deleted help appreciate the server write load.

## Top MySQL Commands

The Top MySQL Commands graph shows the rate of the various kind of SQL statements executed on the MySQL Server.

## Top MySQL Handlers

The Top MySQL Handlers graph shows the rate of the various low level storage engine handler calls. The most important ones to watch are *read_next* and *read_rnd_next*.

A high values for read_rnd_next is an indication there are table scans while a high value of read_next is an indication of index scans.
