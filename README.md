# xPDKcheck
Obtaine server topology layout, including:
1. CPU (option -c)
2. kernel (option -k)
3. memory (option -m)
4. NIC (option -n)
5. SPDK (option -s)
6. PMDK (option -p) TBD

by execute simple shell './checker [-option]' you may grab instant system information rather than typing command line by line, thus provide you handy script while tunning system performance like cpu binding, isolation, irq affinity, DPDK/SPDK acceleration, PMDK coding etc.

snippet output:
=====           CPU Brief               =====
Logical processors: 72
Physical socket: 2
Siblings in one socket:  36
Cores in one socket:  18
Cores in total: 36
Hyper-Threading: on

=====           CPU Layout               =====
Socket 0:   0  1  2  3  4  5  6  7  8  9  10 11 12 13 14 15 16 17 36 37 38 39 40 41 42 43 44 45 46 47 48 49 50 51 52 53
Socket 1:   18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 54 55 56 57 58 59 60 61 62 63 64 65 66 67 68 69 70 71
NO cpu isolation configured
threads on per cores:
core id           threads
core[36]          10
core[35]          7

...

=====       NIC Cap and DPDK-Support checking         =====
02:00.0 Ethernet controller: Intel Corporation 82599ES 10-Gigabit SFI/SFP+ Network Connection (rev 01)
LnkCap: Port #0, Speed 5GT/s, Width x8, ASPM L0s, Exit Latency L0s unlimited, L1 <8us LnkSta: Speed 5GT/s, Width x8, TrErr- Train- SlotClk+ DLActive- BWMgmt- ABWMgmt- LnkSta2: Current De-emphasis Level: -6dB, EqualizationComplete-, EqualizationPhase1-
NIC supported in current DPDK version

02:00.1 Ethernet controller: Intel Corporation 82599ES 10-Gigabit SFI/SFP+ Network Connection (rev 01)
LnkCap: Port #0, Speed 5GT/s, Width x8, ASPM L0s, Exit Latency L0s unlimited, L1 <8us LnkSta: Speed 5GT/s, Width x8, TrErr- Train- SlotClk+ DLActive- BWMgmt- ABWMgmt- LnkSta2: Current De-emphasis Level: -6dB, EqualizationComplete-, EqualizationPhase1-
NIC supported in current DPDK version

...

MTU/queue per NIC
Try to use command 'echo > $bitmask /proc/irq/$irq_index/smp_affinity' to isolate cpu from interupts
net_device      MTU             queue avai      irq number per queue
====================================================================
eno1            1500            8               9
eno2            1500            8               0
eno3            1500            44              0
eno4            1500            44              0
