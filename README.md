# PartitionKV
## 1 Introduction
A DRAM-NVM-SSD key-value store based on the LSM-tree.


## 2 Compilation and Run
### 2.1 Tools
PartitionKV acesses NVM via [PMDK](https://github.com/pmem/pmdk) and uses the B+ tree of the third-party library tlx(https://github.com/tlx/tlx). To run PartitionKV, please install PMDK and tlx first.

### 2.2 Configuration

To run PartitionKV, please modify the configuration in ``memory/nvm_module.cc``.
```
const char * PM_FILE_NAME="/mnt/pmemdir/pm_log";
```


### 2.3 Compilation
We only support Makefile instead of cmake currently.
```
> make -j64   
```


### 2.4 Run
We use db_bench for testing.
```
./db_bench ----benchmarks= "fillrandom,stats,readrandom,stats" --dbname=/mnt/data_02/dbbench --max_background_flushes=5 --max_background_compactions=1 --target_file_size_base=16777216 --max_bytes_for_level_base=8589934592
```

