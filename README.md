# ABSE-DAG-Rider
Apply ABSE to DAG-Dider.

DAG-Dider was taken from https://github.com/Shendor/dag-rider with modifications.

## How to run
Run

```Bash
Cargo build
```

(add --release if you want to run in release mode) and it will generate client and node in the corresponding directory of the target. Run

```Bash
./client -h
```
```Bash
./node -h
```
to view parameter definitions.

The subcommand `generate` provide a way to generate multiple files for multi processes.
It also helps to generate a bunch of bash scripts to run all the nodes.

Example:

Generate relevant configuration files in the current directory (batch size: 10, channel capacity： 1000， 16 processes, 0 fauties):
```Bash
./node generate --batch_size 10 --channel_capacity 1000 --node_count 16
```

This generates the committee.json and run_node.sh configuration files. 
Then run:
```Bash
bash run_node.sh
```
to start all nodes.

You also need to start the clients to send transactions to the node, for example:
```Bash
./client --TRANSACTION_COUNT 100 --TX_SIZE 40 127.0.0.1:8124 
```
Note that the default ports for the nodes start at 8123, where each process occupies three consecutive ports, the second port is used to receive transactions, and you can follow this logic to find the port number of the process you need. You can also write script files to implement the operation of sending a certain number of transactions at regular intervals.

Note: Currently, throughput and latency do not support automatic statistics and may need to be calculated manually.