# xPDKcheck
Obtaine server topology layout, including:
1. CPU (option -c)
2. kernel (option -k)
3. memory (option -m)
4. NIC (option -n)
5. SPDK (option -s)
6. PMDK (option -p) TBD

by execute simple shell './checker [-option]' you may grab instant system information rather than typing command line by line, thus provide you handy script while tunning system performance like cpu binding, isolation, irq affinity, DPDK/SPDK acceleration, PMDK coding etc.
