## Lab #1: 3-Nodes Cluster

## Create and start a cluster with 3 nodes with version 19.1.11

```
./roachprod create seungjin-upgrade --nodes 3 --lifetime 72h 
./roachprod stage seungjin-upgrade release v19.1.11
./roachprod start seungjin-upgrade 
```

## Check if all nodes in the cluster is up and running from the terminal and Admin UI

```
./roachprod list seungjin-upgrade --details
./roachprod adminui seungjin-upgrade:1
```

## Initialize and run a transaction based workload

```
./roachprod run seungjin-upgrade "./cockroach workload init tpcc”
./roachprod run seungjin-upgrade "./cockroach workload run tpcc”
./roachprod run seungjin-upgrade "kv.snapshot_recovery.max_rate=‘1024mb'”
```

## Verify ranges are replicated Admin UI. Stop and upgrade the second node to v19.2.12

```
./roachprod stop seungjin-upgrade:2 
./roachprod stage seungjin-upgrade:2 release v19.2.12
```

## Verify ranges are replicated from Admin UI. Temporarily stop the third node to simulate a disaster

```
./roachprod stop seungjin-upgrade:3
```

## Confirm the cluster is no longer available from the Admin UI. Bring back the second node

```
./roachprod start seungjin-upgrade:2 
```

## From the Admin UI, ensure the second node has been upgraded. Ensure two of the nodes in the cluster is up and running and the cluster is available. Terminate the cluster in the end

```
./roachprod destroy seungjin-upgrade 
```

## Lab #2: 5-Nodes Cluster

## Create and start a cluster with 5 nodes with version 19.1.11

```
./roachprod create seungjin-upgrade --nodes 5 --lifetime 72h 
./roachprod stage seungjin-upgrade release v19.1.11
./roachprod start seungjin-upgrade 
```

## Check if all nodes in the cluster is up and running from the terminal and Admin UI

```
./roachprod list seungjin-upgrade --details
./roachprod adminui seungjin-upgrade:1
```

## Initialize and run a transaction based workload

```
./roachprod run seungjin-upgrade "./cockroach workload init tpcc”
./roachprod run seungjin-upgrade "./cockroach workload run tpcc”
./roachprod run seungjin-upgrade "kv.snapshot_recovery.max_rate=‘1024mb'”
```

## Verify ranges are replicated (Admin UI). Stop and upgrade the second node to v19.2.12

```
./roachprod stop seungjin-upgrade:2 
./roachprod stage seungjin-upgrade:2 release v19.2.12
```

## Verify ranges are replicated (Admin UI). Temporarily stop the third node to simulate a disaster

```
./roachprod stop seungjin-upgrade:3
```

## Confirm the cluster is still available and there aren’t any errors. Bring back the second node

```
./roachprod start seungjin-upgrade:2 
```

## From the Admin UI, ensure the second node has been upgraded. Bring back the third node

```
./roachprod start seungjin-upgrade:3
```

## Ensure all of the nodes in the cluster is up and running. Terminate the cluster in the end

```
./roachprod destroy seungjin-upgrade 
```
