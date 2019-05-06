# SysDump

script option as follows:
```shell
        -a: show all set of system information
        -c: show cpu layout
        -k: show kernel parameters
        -d: show disk layout
        -m: show memory layout
        -n: show nic layout
        -s: show spdk layout
        -f: [filename] dump info to file
```

by execute simple shell './checker [-option]' you may grab instant system information rather than typing command line by line, thus provide you handy script while tunning system performance like cpu binding, isolation, irq affinity, DPDK/SPDK acceleration, PMDK coding etc.
