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

# Performance Monitoring

## Flamechart

```
Amazon Linux 2: sudo yum install perf
Ubuntu: sudo apt-get install linux-tools-$(uname -r)

git clone https://github.com/brendangregg/FlameGraph.git
sudo perf record -ag -F99 -o perf.data &

# benchmarking your code
pkill perf

# create flamechart: 
perf script -i perf.data | FlameGraph/stackcollapse-perf.pl | FlameGraph/flamegraph.pl > flamegraph.svg

# re-run perf record with --call-graph=dwarf if you corrupt stack trace on x86
```

## Cflag for ARM
- update the Cflags for ARM from -march=armv8-a to -march=armv8-a+crc+crypto -falign-jumps=32 -falign-loops=32 -falign-functions=32 (C/C++ builds with these flags out perform 3%~4% compare original ones)
- -Ofast or a more conservative -O2
- -ftree-vectorize -ftree-vectorizer-verbose=5
- Intel: -msse2

# check with command below for gcc compiler tuning option
```
ubuntu@ip-172-31-19-250:~$ gcc -march=native -Q --help=targetgcc -march=native -Q --help=target | grep -- '-mtune=' | cut -f3
cc1: warning: unrecognized argument to --help= option: ‘targetgcc’
skylake-avx512
  Known valid arguments for -mtune= option:
ubuntu@ip-172-31-19-250:~$ gcc -march=native -Q --help=target | grep -- '-mtune=' | cut -f3
skylake-avx512
  Known valid arguments for -mtune= option:
```
# Lock/Synchronization intensive workload
LSE based locking and synchronization is an order of magnitude faster for highly contended locks with high core counts (e.g. 64 with Graviton2). For workloads that have highly contended locks, compiling with -march=armv8.2-a will enable LSE based atomics and can substantially increase performance. However, this will prevent the code from running on an Arm v8.0 system such as AWS Graviton-based EC2 A1 instances. With GCC 10 and newer an option -moutline-atomics will not inline atomics and detect at run time the correct type of atomic to use. This is slightly worse performing than -march=armv8.2-a but does retain backwards compatibility.

## Python

```
sudo apt-get update
sudo apt-get install -y build-essential wget python-dev zlib1g-dev libbz2-dev libncurses5-dev libreadline-dev libssl-dev libgdbm-dev liblzma-dev libsqlite3-dev tk-dev uuid-dev libffi-dev libexpat1-dev libdb5.3-dev

wget "https://www.python.org/ftp/python/3.8.1/Python-3.8.1.tar.xz"
tar -xf Python-3.8.1.tar.xz
cd Python-3.8.1

# Python binary is built with PGO and LTO optimization enables
./configure --enable-optimizations --with-lto
make clean
make profile-opt
make
sudo make install

# Test
sudo apt-get install -y python3-pip
sudo python3 -m pip install pyperformance
sudo python3 /usr/local/bin/pyperformance run -b json_dumps,django_template,regex_dna
```
