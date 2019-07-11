# Txid query plugin tutorial

## 1. Overview

A lightweight txid query plugin that gets the `transaction` structure via txid and uses the levedb database to store only the transactions in the irreversible block. With the leveldb database, there is no need to start additional processes, and the `witness_node` program provides API interface queries.

Plugin name: `query_txid_plugin`

Database: `leveldb`

Configuration:

| BlockChain | Ram | Disk |
| :--- | :--- | :-- |
| Mainnet | 32G | 1T |
| Testnet | 16G | 500G |


## 2. Compilation and startup

The release program does not include the plugin. If you want to use the plugin, please follow the steps below to compile the duration_node program with the plugin.

### 2.1 Compilation

#### 1. Download leveldb dependencies and install

``` sh
# install leveldb
wget https://github.com/google/leveldb/archive/v1.20.tar.gz
tar xvf v1.20.tar.gz
rm -f v1.20.tar.gz
cd leveldb-1.20
make
sudo scp -r out-static/lib* out-shared/lib* "/usr/local/lib"
cd include
sudo scp -r leveldb /usr/local/include
sudo ldconfig
```
```sh
# install snappy
git clone https://github.com/google/snappy.git
cd snappy
mkdir build
cd build && cmake ../
sudo make install
```

#### 2. Open compile option, support leveldb plugin

Modify the `gxb-core/CMakeLists.txt` file as follows to enable compilation options

```cpp
set( LOAD_TXID_PLUGIN 1)
```

#### 3. Compile the witness_node program with plugins

Compile in Ubuntu environment: [Build Ubuntu](https://github.com/gxchain/gxb-core/wiki/BUILD_UBUNTU)

Compile in MacOS environment: [Build OSX](https://github.com/gxchain/gxb-core/wiki/BUILD_OS_X)

### 2.2 Start

#### 1. Start the witness_node program with plugins

When starting the `witness_node` program, add the `plugins` parameter with the following parameters:

```bash
--plugins "witness query_txid data_transaction"
```

#### 2. Verify that the plugin is working properly

In the current directory, the `trx_entry.db` file is generated.

## 3. Instructions for using the plugin

Use the `get_transaction_rows` interface to get the transaction structure based on txid, as shown in the following example:

```bash
➜ curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "get_transaction_rows", ["730ab1d94b77232c04f79a83480bf5b2721d0837"]],
        "id": 1
}' 127.0.0.1:28090 | json_pp
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  1094  100   934  100   160  92907  15915 --:--:-- --:--:-- --:--:--  101k
{
   "jsonrpc" : "2.0",
   "id" : 1,
   "result" : {
      "ref_block_num" : 133,
      "expiration" : "2017-12-14T03:45:00",
      "signatures" : [
         "2067dc299394b083c2138ba60df4839dbe0795efeecf29f8585955b975f3390c6d10bc55de4717c32770803fdc61364400e994a0194039f800058bccadec9e3686"
      ],
      "extensions" : [],
      "operation_results" : [
         [
            1,
            "1.2.20"
         ]
      ],
      "ref_block_prefix" : 636542480,
      "operations" : [
         [
            5,
            {
               "extensions" : {},
               "owner" : {
                  "weight_threshold" : 1,
                  "address_auths" : [],
                  "key_auths" : [
                     [
                        "GXC7vSbriJrEia1kK3A9sQ2LS8e9qmB7hojnkakJ39zomAba5jTek",
                        1
                     ]
                  ],
                  "account_auths" : []
               },
               "referrer" : "1.2.17",
               "name" : "gxb-forum",
               "referrer_percent" : 1000,
               "registrar" : "1.2.17",
               "active" : {
                  "weight_threshold" : 1,
                  "account_auths" : [],
                  "address_auths" : [],
                  "key_auths" : [
                     [
                        "GXC7vSbriJrEia1kK3A9sQ2LS8e9qmB7hojnkakJ39zomAba5jTek",
                        1
                     ]
                  ]
               },
               "fee" : {
                  "amount" : 114453,
                  "asset_id" : "1.3.0"
               },
               "options" : {
                  "num_committee" : 0,
                  "votes" : [],
                  "memo_key" : "GXC7vSbriJrEia1kK3A9sQ2LS8e9qmB7hojnkakJ39zomAba5jTek",
                  "voting_account" : "1.2.5",
                  "num_witness" : 0,
                  "extensions" : []
               }
            }
         ]
      ]
   }
}
```
