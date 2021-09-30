## Lab #1: 3-Nodes Cluster


## Create and start a cluster with 3 nodes with version 19.1.11

```
./roachprod create seungjin-upgrade --nodes 3 --lifetime 72h 
./roachprod stage seungjin-upgrade release v19.1.11
./roachprod start seungjin-upgrade 
```

## Check if all nodes in the cluster is up and running from the terminal and DB Console

```
./roachprod list seungjin-upgrade --details
./roachprod adminui seungjin-upgrade:1
```

## Initialize and run a transaction based workload

```
./roachprod run seungjin-upgrade "./cockroach workload init tpcc”
./roachprod run seungjin-upgrade "./cockroach workload run tpcc”
```

## Log in to SQL and increase the recovery and rebalance rate

```
# This speeds up the recovery process when an existing node is down for an upgrade or a failure

./roachprod sql seungjin-upgrade:1
set cluster setting kv.snapshot_recovery.max_rate='1024mb';
set cluster setting kv.snapshot_rebalance.max_rate='1024mb';
```

## Stop and upgrade the second node to v19.2.12

```
# First verify ranges are adequately replicated from DB Console. 

./roachprod stop seungjin-upgrade:2 
./roachprod stage seungjin-upgrade:2 release v19.2.12
```

## Temporarily stop the third node to simulate a disaster

```
# First verify ranges are adequately replicated from DB Console. 

./roachprod stop seungjin-upgrade:3
```

## Bring back the second node

```
# Confirm the cluster is no longer available from the DB Console. 

./roachprod start seungjin-upgrade:2 
```

## Terminate the cluster in the end

```
# From the DB Console, ensure the second node has been upgraded. 
# Ensure two of the nodes in the cluster is up and running and the cluster is available. 

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
```

## Log in to SQL and increase the recovery and rebalance rate

```
# This speeds up the recovery process when an existing node is down for an upgrade or a failure

./roachprod sql seungjin-upgrade:1
set cluster setting kv.snapshot_recovery.max_rate='1024mb';
set cluster setting kv.snapshot_rebalance.max_rate='1024mb';
```

## Stop and upgrade the second node to v19.2.12

```
# Verify ranges are replicated from DB Console. 

./roachprod stop seungjin-upgrade:2 
./roachprod stage seungjin-upgrade:2 release v19.2.12
```

## Temporarily stop the third node to simulate a disaster

```
# Verify ranges are replicated from DB Console. 

./roachprod stop seungjin-upgrade:3
```

## Bring back the second node

```
# Confirm the cluster is still available and there aren’t any errors. 

./roachprod start seungjin-upgrade:2 
```

## Bring back the third node

```
# From the DB Console, ensure the second node has been upgraded. 

./roachprod start seungjin-upgrade:3
```

## Terminate the cluster in the end

```
# Ensure all of the nodes in the cluster is up and running. 

./roachprod destroy seungjin-upgrade 
```
