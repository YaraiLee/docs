# API Reference

GXChain的节点提供WebSocket和JSONRPC两种接口形式

## 链相关

### `get_chain_id`
获取链id

#### 参数说明

<table>
    <tr>
        <th rowspan="1">请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">get_chain_id</td>
    </tr>
    <tr>
        <td>API Parameters</td>
        <td colspan="2" align="center">空</td>
    </tr>
</table>

#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "get_chain_id", []],
        "id": 1
}' https://node1.gxb.io/rpc
```
**response:**
```json
{
    "id":1,
        "jsonrpc":"2.0",
        "result":"4f7d07969c446f8342033acb3ab2ae5044cbe0fde93db02de75bd17fa8fd84b8" // chain id
}
```

### `get_dynamic_global_properties`
获取动态全局对象, 包括最新区块号、最新区块id、区块头时间等信息

#### 参数说明

<table>
    <tr>
        <th rowspan="1">请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">get_dynamic_global_properties</td>
    </tr>
    <tr>
        <td>API Parameters</td>
        <td colspan="2" align="center">空</td>
    </tr>
</table>

#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "get_dynamic_global_properties", []],
        "id": 1
}' https://node1.gxb.io/rpc
```

**response:**
```json
{
    "id":1,
        "jsonrpc":"2.0",
        "result":{
            "id":"2.1.0",
            "head_block_number":16757465, // 最新区块号
            "head_block_id":"00ffb2d9f6e344f2190a8dfba58baaadd49e76c4", // 最新区块id
            "time":"2019-01-28T06:08:00", // 区块头时间
            "current_witness":"1.6.52", // 打包当前head block的witness id
            "next_maintenance_time":"2019-01-28T06:40:00", // 下次维护周期时间
            "last_budget_time":"2019-01-28T05:40:00", // 上次维护周期时间
            "witness_budget":3065824, // 当前维护周期内, 剩余的节点预算
            "accounts_registered_this_interval":2,
            "recently_missed_count":0, // 节点的最近缺失块数
            "current_aslot":16958091,
            "recent_slots_filled":"340282366920938463463374607431768211455",
            "dynamic_flags":0,
            "last_irreversible_block_num":16757449 // 最后不可逆区块号
        }
}
```


## 区块相关

### `get_block`

通过区块号获取区块信息

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">get_block</td>
    </tr>
    <tr>
        <td rowspan="3" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>block_num</td>
        <td>区块号/区块高度</td>
    </tr>
</table>


#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "get_block", [10000]],
        "id": 1
}' https://node1.gxb.io/rpc
```

**response:**
```json
{
    "id": 1,
        "jsonrpc": "2.0",
        "result": {
            "previous": "0000270f5b219bc4c6996f2cca89b23ef653a2b0", // 前一个区块的block id(block hash)
            "timestamp": "2017-06-10T22:53:45", // 当前区块的timestamp
            "witness": "1.6.23", // 打包当前区块的witness id
            "transaction_merkle_root": "0000000000000000000000000000000000000000", // 当前区块中，交易的merkle根
            "extensions": [],
            "witness_signature": "204e95ba3f871d8f670cc8088d5f563704c9c0c8acd42a80077bd7c6a47ecde095633e6a614c7f73830d972c3b617d5c01e8e0e151bfc489a327103597d3f0c244", // witness签名
            "transactions": [], // 交易列表
            "block_id": "000027100ef5386d4ea4481dc302401de66fe358", // 当前区块的block id
            "signing_key": "GXC7ouC3miJyKrLf1XyeyDv6u5W9Q8BT3WdbJbJYACiFm2Zx8vPna", // 当前witness的signing key
            "transaction_ids": [] // 和交易列表对应的tx id
        }
}
```

### `get_block_header`

根据区块号获取区块头信息

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">get_block_header</td>
    </tr>
    <tr>
        <td rowspan="3" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>block_num</td>
        <td>区块号/区块高度</td>
    </tr>
</table>

#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "get_block_header", [10000]],
        "id": 1
}' https://node1.gxb.io/rpc
```

**response:**
```json
{
    "id": 1,
        "jsonrpc": "2.0",
        "result": {
            "previous": "0000270f5b219bc4c6996f2cca89b23ef653a2b0", // 前一个区块的block id(block hash)
            "timestamp": "2017-06-10T22:53:45", // 当前区块的timestamp
            "witness": "1.6.23", // 打包当前区块的witness id
            "transaction_merkle_root": "0000000000000000000000000000000000000000", // 当前区块中，交易的merkle根
            "extensions": []
        }
}
```
## 交易相关

### `get_transaction_hex`

以16进制形式，返回交易的序列化字符串

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">get_transaction_hex</td>
    </tr>
    <tr>
        <td rowspan="3" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>transaction</td>
        <td>交易消息体</td>
    </tr>
</table>

#### 示例

**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "get_transaction_hex", [{"ref_block_num":53237,"ref_block_prefix":892361345,"expiration":"2019-03-07T06:07:21","operations":[[0,{"fee":{"amount":50000,"asset_id":"1.3.1"},"from":"1.2.17","to":"1.2.6","amount":{"amount":100000,"asset_id":"1.3.1"},"extensions":[]}]],"extensions":[],"signatures":[]}]], "id": 1
}' https://node1.gxb.io/rpc
```

**response:**
```
{"id":1,"jsonrpc":"2.0","result":"f5cf815a303519b5805c010050c3000000000000011106a0860100000000000100000000"}
```

## 对象相关

在GXChain里面，通过不同的对象来存储不同类型的数据，点此查看[GXChain上的对象类型](./#_2-gxchain上的对象)

### `get_objects`

根据对象ID获取对象信息

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">get_objects</td>
    </tr>
    <tr>
        <td rowspan="3" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>[对象id]</td>
        <td>数组，可传入多个对应id</td>
    </tr>
</table>

#### 示例

**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "get_objects", [["1.3.1","2.3.1"]]], "id": 1
}' https://node1.gxb.io/rpc
```

**response:**
```json
{
    "id": 1,
        "jsonrpc": "2.0",
        "result": [{ // 1.3.1对象
            "id": "1.3.1",
            "symbol": "GXC",
            "precision": 5,
            "issuer": "1.2.0",
            "options": {
                "max_supply": "10000000000000",
                "market_fee_percent": 0,
                "max_market_fee": 0,
                "issuer_permissions": 69,
                "flags": 0,
                "core_exchange_rate": {
                    "base": {
                        "amount": 100000,
                        "asset_id": "1.3.1"
                    },
                    "quote": {
                        "amount": 100000,
                        "asset_id": "1.3.1"
                    }
                },
                "whitelist_authorities": [],
                "blacklist_authorities": [],
                "whitelist_markets": [],
                "blacklist_markets": [],
                "description": "{\"main\":\"GXC是公信宝基金会在GXChain（公信链）上发行的Token，不仅具有流通价值，同时在公信链上开发、认证应⽤、使⽤链上服务（例如链上转账的矿⼯费）以及使⽤BaaS服务都需要⽀付或燃烧GXC，GXC是作为链上应⽤运⾏使⽤到的Token。 在布洛克城中也可以很方便地利用GXC进行支付结算，如居民之间互相使用GXC进行结算，使用城市公共服务需要用GXC结算，商家提供的服务也需要用GXC来购买等等\",\"short_name\":\"\",\"market\":\"\"}",
                "extensions": []
            },
            "dynamic_asset_data_id": "2.3.1"
        }, { // 2.3.1 对象
            "id": "2.3.1",
                "current_supply": "9958303550217",
                "confidential_supply": 0,
                "accumulated_fees": 0,
                "fee_pool": 0
        }]
}
```

## 账户相关


### `get_account_count`

获取链上帐户总数量

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">get_account_count</td>
    </tr>
    <tr>
        <td>API Parameters</td>
        <td colspan="2" align="center">空</td>
    </tr>
</table>

#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "get_account_count", []],
        "id": 1
}' https://node1.gxb.io/rpc
```

**response:**
```json
{
    "id": 1,
        "jsonrpc": "2.0",
        "result": 1118627 // 链上总帐户数
}
```

### `get_account_by_name`

根据`account_name`获取`account`信息，**不包含**关联对象的信息，如账户资产余额、待解冻余额、忠诚计划冻结余额等

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">get_account_by_name</td>
    </tr>
    <tr>
        <td rowspan="3" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>account_name</td>
        <td>账户名</td>
    </tr>
</table>

#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "get_account_by_name", ["nathan"]],
        "id": 1
}' https://node1.gxb.io/rpc
```
**response:**
```json
{
    "id": 1,
        "jsonrpc": "2.0",
        "result": {
            "id": "1.2.17", // 帐户id
            "membership_expiration_date": "2106-02-07T06:28:15", // 不为1970-01-01T00:00:00， 表示终身会员
            "merchant_expiration_date": "1970-01-01T00:00:00", // 不为1970-01-01T00:00:00， 表示商户
            "datasource_expiration_date": "1970-01-01T00:00:00", // 不为1970-01-01T00:00:00， 表示数据源
            "data_transaction_member_expiration_date": "1970-01-01T00:00:00", // 不为1970-01-01T00:00:00， 在DES 1.0中具有交易确认权限
            "registrar": "1.2.17", // 帐户注册人
            "referrer": "1.2.17", // 帐户推荐人
            "lifetime_referrer": "1.2.17", // 终身会员推荐人
            "merchant_auth_referrer": "1.2.0", // 商户推荐人
            "datasource_auth_referrer": "1.2.0", // 数据源推荐人
            "network_fee_percentage": 2000, // 手续费分成，网络费占比
            "lifetime_referrer_fee_percentage": 8000, // 手续费分成, 终身会员推荐人占比
            "referrer_rewards_percentage": 0, // 手续费分成, 推荐人占比
            "name": "nathan", // 帐户名
            "vm_type": "", // vm类型，保留字段
            "vm_version": "", // vm 版本, 保留字段
            "code": "", // 代码，适用于适用合约帐户
            "code_version": "", // 代码hash
            "abi": { // code对应的abi, 适用于适用合约帐户
                "version": "gxc::abi/1.0",
                "types": [],
                "structs": [],
                "actions": [],
                "tables": [],
                "error_messages": [],
                "abi_extensions": []
            },
            "owner": { // 帐户owner权限, 可以用来修改帐户权限
                "weight_threshold": 1,
                "account_auths": [],
                "key_auths": [
                    ["GXC6cdTzGgTLv7VohhT76o82WmZmTwvijrkr5hJ3k8G2dEREee6wV", 1]
                ],
                "address_auths": []
            },
            "active": { // 帐户的active权限, 可用来花费帐户资金
                "weight_threshold": 1,
                "account_auths": [],
                "key_auths": [
                    ["GXC6cdTzGgTLv7VohhT76o82WmZmTwvijrkr5hJ3k8G2dEREee6wV", 1]
                ],
                "address_auths": []
            },
            "options": {
                "memo_key": "GXC6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV", // memo key
                "voting_account": "1.2.5",
                "num_witness": 0,
                "num_committee": 0,
                "votes": [],
                "extensions": []
            },
            "statistics": "2.6.17", // 帐户统计对象
            "whitelisting_accounts": [],
            "blacklisting_accounts": [],
            "whitelisted_accounts": [],
            "blacklisted_accounts": [],
            "cashback_vb": "1.13.246", // 返现对象id
            "owner_special_authority": [0, {}],
            "active_special_authority": [0, {}],
            "top_n_control_flags": 0
        }
}
```

### `get_full_accounts`

根据`account_ids 或者 account_names`获取完整账户信息，**包含**关联对象的信息，如账户资产余额，冻结余额等。

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">get_full_accounts</td>
    </tr>
    <tr>
        <td rowspan="4" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>[帐户名或者帐户id]</td>
        <td>数组，可传入帐户名或者帐户id</td>
    </tr>
    <tr>
        <td>bool型</td>
        <td>是否订阅</td>
    </tr>
</table>

#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "get_full_accounts", [["blockcitybp"],false]],
        "id": 1
}' https://node1.gxb.io/rpc
```
**response:**
```json
{
    "id":1,
        "jsonrpc":"2.0",
        "result":[
            [
                "blockcitybp",
            {
                "account":{
                    "id":"1.2.1089881",
                    "membership_expiration_date":"2106-02-07T06:28:15", // 非1970，为终身会员帐户
                    "merchant_expiration_date":"1970-01-01T00:00:00", // 非1970， 为商户
                    "datasource_expiration_date":"1970-01-01T00:00:00", // 非1970， 为数据源
                    "data_transaction_member_expiration_date":"1970-01-01T00:00:00",
                    "registrar":"1.2.1089881", // 帐户注册人
                    "referrer":"1.2.1089881", // 帐户推荐人
                    "lifetime_referrer":"1.2.1089881",
                    "merchant_auth_referrer":"1.2.0",
                    "datasource_auth_referrer":"1.2.0",
                    "network_fee_percentage":2000,
                    "lifetime_referrer_fee_percentage":8000,
                    "referrer_rewards_percentage":1000,
                    "name":"blockcitybp", // 帐户名
                    "vm_type":"",
                    "vm_version":"",
                    "code":"",  // code不为空，为智能合约帐户
                    "code_version":"",
                    "abi":{
                        "version":"gxc::abi/1.0",
                        "types":[

                        ],
                        "structs":[

                        ],
                        "actions":[

                        ],
                        "tables":[

                        ],
                        "error_messages":[

                        ],
                        "abi_extensions":[

                        ]
                    },
                    "owner":{
                        "weight_threshold":1,
                        "account_auths":[

                        ],
                        "key_auths":[
                            [
                                "GXC8XrrSD9LE4UuUvB1QtTA1EhUfjQeJLZwgeP7br56Koh1zrxez7",
                        1
                            ]
                        ],
                        "address_auths":[

                        ]
                    },
                    "active":{
                        "weight_threshold":1,
                        "account_auths":[

                        ],
                        "key_auths":[
                            [
                                "GXC8XrrSD9LE4UuUvB1QtTA1EhUfjQeJLZwgeP7br56Koh1zrxez7",
                        1
                            ]
                        ],
                        "address_auths":[

                        ]
                    },
                    "options":{
                        "memo_key":"GXC8XrrSD9LE4UuUvB1QtTA1EhUfjQeJLZwgeP7br56Koh1zrxez7",
                        "voting_account":"1.2.5",
                        "num_witness":0,
                        "num_committee":0,
                        "votes":[

                        ],
                        "extensions":[

                        ]
                    },
                    "statistics":"2.6.1089881",
                    "whitelisting_accounts":[

                    ],
                    "blacklisting_accounts":[

                    ],
                    "whitelisted_accounts":[

                    ],
                    "blacklisted_accounts":[

                    ],
                    "cashback_vb":"1.13.278",
                    "owner_special_authority":[
                        0,
                    {

                    }
                    ],
                    "active_special_authority":[
                        0,
                    {

                    }
                    ],
                    "top_n_control_flags":0
                },
                "statistics":{
                    "id":"2.6.1089881",
                    "owner":"1.2.1089881",
                    "most_recent_op":"2.9.201931750",
                    "total_ops":13,
                    "removed_ops":0,
                    "total_core_in_orders":0,
                    "lifetime_fees_paid":5153414,
                    "pending_fees":0,
                    "pending_vested_fees":0
                },
                "registrar_name":"blockcitybp",
                "referrer_name":"blockcitybp",
                "lifetime_referrer_name":"blockcitybp",
                "votes":[

                ],
                "cashback_balance":{ // 返现余额，属于待解冻余额的一部分
                    "id":"1.13.278",
                    "owner":"1.2.1089881",
                    "balance":{
                        "amount":1932, // amount精度为5, 转换成正常数量为1932/100000
                        "asset_id":"1.3.1" // 1.3.1 对应 GXC
                    },
                    "policy":[ // 解冻策略, 0表示线性，1表示币天
                        1,
                    {
                        "vesting_seconds":2592000,
                        "start_claim":"1970-01-01T00:00:00",
                        "coin_seconds_earned":"5007744000",
                        "coin_seconds_earned_last_update":"2019-01-16T07:40:00"
                    }
                    ]
                },
                "balances":[ // 余额
                {
                    "id":"2.5.456853",
                    "owner":"1.2.1089881",
                    "asset_type":"1.3.1",
                    "balance":265386
                }
                ],
                "locked_balances":[

                ],
                "vesting_balances":[ // 待解冻余额
                {
                    "id":"1.13.171",
                    "owner":"1.2.1089881",
                    "balance":{
                        "amount":0,
                        "asset_id":"1.3.1"
                    },
                    "policy":[
                        1,
                    {
                        "vesting_seconds":7776000,
                        "start_claim":"1970-01-01T00:00:00",
                        "coin_seconds_earned":"0",
                        "coin_seconds_earned_last_update":"2018-12-27T03:04:21"
                    }
                    ]
                },
                {
                    "id":"1.13.259",
                    "owner":"1.2.1089881",
                    "balance":{
                        "amount":265747140,
                        "asset_id":"1.3.1"
                    },
                    "policy":[
                        1,
                    {
                        "vesting_seconds":86400,
                        "start_claim":"1970-01-01T00:00:00",
                        "coin_seconds_earned":"22960140940800",
                        "coin_seconds_earned_last_update":"2019-01-28T06:11:57"
                    }
                    ]
                },
                {
                    "id":"1.13.278",
                    "owner":"1.2.1089881",
                    "balance":{
                        "amount":1932,
                        "asset_id":"1.3.1"
                    },
                    "policy":[
                        1,
                    {
                        "vesting_seconds":2592000,
                        "start_claim":"1970-01-01T00:00:00",
                        "coin_seconds_earned":"5007744000",
                        "coin_seconds_earned_last_update":"2019-01-16T07:40:00"
                    }
                    ]
                }
                ],
                "pledge_balances":[ // 公信节点抵押资产余额
                {
                    "id":"1.26.1",
                    "owner_account":"1.2.1089881",
                    "amount":{
                        "amount":1000000000,
                        "asset_id":"1.3.1"
                    }
                }
                ],
                "limit_orders":[

                ],
                "call_orders":[

                ],
                "settle_orders":[

                ],
                "proposals":[

                ],
                "assets":[

                ],
                "withdraws":[

                ]
            }
    ]
        ]
}
```

### `is_account_registered`
查询帐户名是否已注册。 若已注册，则返回true，未注册或者帐户名不合法，返回false

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">is_account_registered</td>
    </tr>
    <tr>
        <td rowspan="3" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>account_name</td>
        <td>账户名</td>
    </tr>
</table>

#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "is_account_registered", ["nathan"]],
        "id": 1
}' https://node1.gxb.io/rpc
```

**response:**
```json
{
	"id": 1,
	"jsonrpc": "2.0",
	"result": true // true表示帐户已被注册
}
```

### `get_key_references`
根据公钥，查询关联的帐户，返回关联的帐户id

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">get_key_references</td>
    </tr>
    <tr>
        <td rowspan="3" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>[公钥]</td>
        <td>数组，传入一系列公钥</td>
    </tr>
</table>

#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "get_key_references", [["GXC7mmfnZWUYtz2tjNGqduZRe2w5x79GCjuoMiVkmEGRE94Vq7gAo"]]],
        "id": 1
}' https://node1.gxb.io/rpc
```

**response:**
```json
{
	"id": 1,
	"jsonrpc": "2.0",
	"result": [
		["1.2.26", "1.2.26"] // 公钥关联的account id
	]
}
```

## 资产相关

### `list_assets`

查询资产, 返回比传入参数大的资产对象

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">list_assets</td>
    </tr>
    <tr>
        <td rowspan="4" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>资产名</td>
        <td>资产符号或者首字符串，比如G</td>
    </tr>
    <tr>
        <td>limit</td>
        <td>返回的结果数量</td>
    </tr>
</table>

#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "list_assets", ["G", 2]],
        "id": 1
}' https://node1.gxb.io/rpc
```

**response:**
```json
{
	"id": 1,
	"jsonrpc": "2.0",
	"result": [{
		"id": "1.3.11", // 返回资产1.3.11
		"symbol": "GBA", // 资产名字GBA
		"precision": 5, // 精度
		"issuer": "1.2.1110589", // 资产发行人
		"options": {
			"max_supply": "200000000000000", // 资产最大供应量
			"market_fee_percent": 0,
			"max_market_fee": 0,
			"issuer_permissions": 0,
			"flags": 0,
			"core_exchange_rate": { // 跟GXC的汇率
				"base": {
					"amount": 100000,
					"asset_id": "1.3.1"
				},
				"quote": {
					"amount": 1000000,
					"asset_id": "1.3.11"
				}
			},
			"whitelist_authorities": [],
			"blacklist_authorities": [],
			"whitelist_markets": [],
			"blacklist_markets": [],
			"description": "{\"main\":\"Green Building Asset，简称GBA，是基于公信链的50%免费分发绿色资产。\",\"market\":\"\"}",
			"extensions": []
		},
		"dynamic_asset_data_id": "2.3.11" // 资产对应的动态属性对应id
	}, {
		"id": "1.3.5", // 资产1.3.5
		"symbol": "GCNY", // 资产名字GCNY
		"precision": 5,
		"issuer": "1.2.785392",
		"options": {
			"max_supply": "1000000000000000",
			"market_fee_percent": 0,
			"max_market_fee": 0,
			"issuer_permissions": 79,
			"flags": 0,
			"core_exchange_rate": {
				"base": {
					"amount": 1000000,
					"asset_id": "1.3.1"
				},
				"quote": {
					"amount": 100000,
					"asset_id": "1.3.5"
				}
			},
			"whitelist_authorities": [],
			"blacklist_authorities": [],
			"whitelist_markets": [],
			"blacklist_markets": [],
			"description": "",
			"extensions": []
		},
		"dynamic_asset_data_id": "2.3.5"
	}]
}
```

### `lookup_asset_symbols`

根据资产名称获取资产详情

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">lookup_asset_symbols</td>
    </tr>
    <tr>
        <td rowspan="3" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>[资产名]</td>
        <td>数组，资产符号或者首字符串，比如GXC</td>
    </tr>
</table>

#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "lookup_asset_symbols", [["GXC"]]],
        "id": 1
}' https://node1.gxb.io/rpc
```

**response:**
结果同list_assets

### `get_account_balances`
根据帐户id和资产id获取帐户余额， 如果资产id不指定，返回全部资产余额

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">get_account_balances</td>
    </tr>
    <tr>
        <td rowspan="4" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>account_id</td>
        <td>帐户id</td>
    </tr>
    <tr>
        <td>[asset id]</td>
        <td>数组，资产id</td>
    </tr>
</table>

#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "get_account_balances", ["1.2.42", ["1.3.0", "1.3.1"]]],
        "id": 1
}' https://node1.gxb.io/rpc

```

**response:**
```json
{
    "id":1,
        "jsonrpc":"2.0",
        "result":[
        {
            "amount":"79795227868",
            "asset_id":"1.3.0"  // 1.3.0为NULL资产
        },
        {
            "amount":"3949999988445", // GXC资产精度为5， 实际数量为39499999.88445
            "asset_id":"1.3.1" // 1.3.1 为GXC资产
        }
        ]
}
```

### `get_named_account_balances`

根据帐户名和资产id获取帐户余额， 如果资产id不指定，返回全部资产余额

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">get_named_account_balances</td>
    </tr>
    <tr>
        <td rowspan="4" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>account_name</td>
        <td>账户名</td>
    </tr>
    <tr>
        <td>[asset id]</td>
        <td>数组，资产id</td>
    </tr>
</table>

#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "get_named_account_balances", ["gxbfoundation", ["1.3.0", "1.3.1"]]],
        "id": 1
}' https://node1.gxb.io/rpc

```

**response:**
```json
{
	"id": 1,
	"jsonrpc": "2.0",
	"result": [{
		"amount": "79795227868", // 1.3.0 资产余额
		"asset_id": "1.3.0"
	}, {
		"amount": "3949999988445", // 1.3.1 资产余额, 即GXC资产，由于GXC资产精度为5，所以实际数量为3949999988445 / 100000
		"asset_id": "1.3.1"
	}]
}
```

### `get_vesting_balances`

根据帐户id获取帐户所有的待解冻余额

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">get_vesting_balances</td>
    </tr>
    <tr>
        <td rowspan="3" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>account_id</td>
        <td>帐户id</td>
    </tr>
</table>

#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "get_vesting_balances", ["1.2.748971"]],
        "id": 1
}' https://node1.gxb.io/rpc
```

**response:**
```json
{
    "id":1,
        "jsonrpc":"2.0",
        "result":[
        {
            "id":"1.13.89",
            "owner":"1.2.748971",
            "balance":{
                "amount":0,
                "asset_id":"1.3.0"
            },
            "policy":[
                1,
            {
                "vesting_seconds":7776000,
                "start_claim":"1970-01-01T00:00:00",
                "coin_seconds_earned":"0",
                "coin_seconds_earned_last_update":"2018-11-09T11:29:30"
            }
            ]
        },
        {
            "id":"1.13.123",
            "owner":"1.2.748971",
            "balance":{
                "amount":24657392,
                "asset_id":"1.3.1"
            },
            "policy":[
                1,
            {
                "vesting_seconds":7776000,
                "start_claim":"1970-01-01T00:00:00",
                "coin_seconds_earned":"191735880192000",
                "coin_seconds_earned_last_update":"2018-12-04T07:40:00"
            }
            ]
        },
        {
            "id":"1.13.237",
            "owner":"1.2.748971",
            "balance":{
                "amount":1907009,
                "asset_id":"1.3.1"
            },
            "policy":[
                1,
            {
                "vesting_seconds":2592000,
                "start_claim":"1970-01-01T00:00:00",
                "coin_seconds_earned":"4942967328000",
                "coin_seconds_earned_last_update":"2019-01-28T00:40:00"
            }
            ]
        }
    ]
}
```

## 公信节点相关

### `get_trust_nodes`

获取所有的公信节点所属帐户id

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">get_trust_nodes</td>
    </tr>
    <tr>
        <td>API Parameters</td>
        <td colspan="2" align="center">空</td>
    </tr>
</table>


#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "get_trust_nodes", []],
        "id": 1
}' https://node1.gxb.io/rpc
```
**response:**
```json
{
   "id":1,
   "jsonrpc":"2.0",
   "result":[
      "1.2.3429",
      "1.2.3431",
      "1.2.3432",
      "1.2.3433",
      "1.2.3434",
      "1.2.748971",
      "1.2.1090296",
      "1.2.1090419",
      "1.2.1061353",
      "1.2.1090653",
      "1.2.1090792",
      "1.2.1090458",
      "1.2.1091083",
      "1.2.1092168",
      "1.2.1106749"
   ]
}
```
### `get_witness_by_account`

根据`account_id`获取`公信节点`信息，包括节点公钥、总票数、缺块数等

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">get_witness_by_account</td>
    </tr>
    <tr>
        <td rowspan="3" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>account_id</td>
        <td>帐户id</td>
    </tr>
</table>

#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "get_witness_by_account", ["1.2.748971"]],
        "id": 1
}' https://node1.gxb.io/rpc
```

**response:**
```json
{
    "id":1,
        "jsonrpc":"2.0",
        "result":{
            "id":"1.6.35",
            "witness_account":"1.2.748971", // 所属帐户
            "last_aslot":0,
            "signing_key":"GXC5YFfb3LtUDnHCu4bTfSMUxoVMz2xwnCbTT99oAdVPCcB2nMKz9", // 签署区块的公钥
            "vote_id":"1:56", // witness的vote id
            "total_votes":"82099555219", // 得票总数
            "url":".",
            "total_missed":0, // 总的缺失块数
            "last_confirmed_block_num":0, // 最后一次打包的区块
            "is_valid":true // witness状态
        }
}
```

### `lookup_vote_ids`

根据vote_id返回所属公信节点的信息, 返回对应的worker对象

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">lookup_vote_ids</td>
    </tr>
    <tr>
        <td rowspan="3" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>[vote_id]</td>
        <td>数组，投票id</td>
    </tr>
</table>


#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "lookup_vote_ids", [["1:22", "0:72"]]],
        "id": 1
}' https://node1.gxb.io/rpc
```


## 智能合约相关

### `serialize_contract_call_args`
以16进制形式，返回智能合约调用参数的序列化字符串
#### 参数说明
<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">serialize_contract_call_args</td>
    </tr>
    <tr>
        <td rowspan="5" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>contract_name</td>
        <td>合约账户名</td>
    </tr>
    <tr>
        <td>method</td>
        <td>方法名</td>
    </tr>
    <tr>
        <td>json_args</td>
        <td>合约方法对应的参数，key-value json字符串，可以为""</td>
    </tr>
</table>


#### 示例
**request:**
```bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "serialize_contract_call_args", ["gxc-redpacket", "issue", "{\"pubkey\":\"GXC5NEGqM8BTnMm5NT7Vv2Shxh4eg4tk1kfmAUf3EGHtksig5vZdN\", \"number\":10}"]],
        "id": 1
}' https://node1.gxb.io
```

**response:**
```
{"id":1,"jsonrpc":"2.0","result":"35475843354e4547714d3842546e4d6d354e54375676325368786834656734746b316b666d41556633454748746b73696735765a644e0a00000000000000"}
```

### `get_table_rows_ex`
`get_table_rows`的扩展接口，提供更丰富的查询功能。（参数字段不传时，使用默认值）

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">get_table_rows_ex</td>
    </tr>
    <tr>
        <td rowspan="5" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>contract_name</td>
        <td>合约账户名</td>
    </tr>
    <tr>
        <td>table_name</td>
        <td>表名</td>
    </tr>
    <tr>
        <td>get_table_rows_params</td>
        <td>参数对象，可以为{}</td>
    </tr>
</table>

get_table_rows_params参数说明：
```
lower_bound， 查询时指定的key最小值, 默认为0
upper_bound， 查询时指定的key最大值，默认为-1，即最大的无符号整形
limit， 查询时指定返回limit条，默认返回10条
index_position， 查询时指定的index，默认为1，即第1个索引
reverse， 查询结果按key的倒序输出，默认为0，即按key从小到大输出
get_table_rows_params所有的参数都有默认值，如无需要改变默认值，可以不传入
```

#### 示例
**request:**
```bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "get_table_rows_ex", ["gdice", "prizepool", {"lower_bound":0,"upper_bound":-1,"limit":20}]],
        "id": 1
}' https://node1.gxb.io
```

**response:**
```json
{
	"id": 1,
	"jsonrpc": "2.0",
	"result": {
		"rows": [{
			"pool": {
				"amount": "3294138495",
				"asset_id": 1
			},
			"totalbet": "30845491144",
			"betcount": 38425,
			"wincount": 31459,
			"minbet": 50000,
			"minbank": 10000000,
			"investtotalpercent": 2643728290,
			"profit": 462683014
		}, {
			"pool": {
				"amount": 0,
				"asset_id": 2
			},
			"totalbet": 0,
			"betcount": 0,
			"wincount": 0,
			"minbet": 1000000,
			"minbank": 100000000,
			"investtotalpercent": 0,
			"profit": 0
		}, {
			"pool": {
				"amount": "100000000000",
				"asset_id": 14
			},
			"totalbet": 0,
			"betcount": 0,
			"wincount": 0,
			"minbet": 10000000,
			"minbank": 1000000000,
			"investtotalpercent": 100000000,
			"profit": 0
		}],
		"more": false
	}
}
```

## 广播手续费接口

### `get_required_fees`

根据交易内容，获取交易结构所需支付手续费数额

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">get_required_fees</td>
    </tr>
    <tr>
        <td rowspan="4" >API Parameters</td>   
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>operations</td>
        <td>交易结构体</td>
    </tr>
    <tr>
        <td>asset_id</td>
        <td>资产编号</td>
    </tr>
</table>


#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc":"2.0",
    "method":"call",
    "params":[0,"get_required_fees",[[[0,{"fee":{"amount":1000,"asset_id":"1.3.1"},"from":"1.2.955603","to":"1.2.1122226","amount":{"amount":40000,"asset_id":"1.3.1"},"extensions":[]}]],"1.3.1"]],
    "id":1
}' https://node1.gxb.io/rpc
```

**response:**
```json
{
    "id":1,
    "jsonrpc":"2.0",
    "result":[
        {
            "amount":1000,
            "asset_id":"1.3.1"
        }
    ]
}
```



## 广播接口

### `broadcast_transaction`

异步api，向网络广播一笔带签名的交易，但不等待交易执行的结果

::: tip Tips
[如何发起链上交易？](../advanced/send_transaction.md)
:::

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">2</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">broadcast_transaction</td>
    </tr>
    <tr>
        <td rowspan="3" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>signed_trx</td>
        <td>带签名的交易消息体</td>
    </tr>
</table>

#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [2,"broadcast_transaction",[{"ref_block_num":3698,"ref_block_prefix":1780126622,"expiration":"2018-12-18T10:56:09","operations":[[0,{"fee":{"amount":1000,"asset_id":"1.3.1"},"from":"1.2.17","to":"1.2.6","amount":{"amount":1000000,"asset_id":"1.3.1"},"extensions":[]}]],"extensions":[],"signatures":["204444e23dff4e911e33d4059b36c91f7d4f85022c90ebd3e509f9b2caeb6bca273c8616ebd4f0786ac03b3ef2796a56d754de301e97aff0e43df6f3dfb12d1e62"]}]],
        "id": 1
}' https://node23.gxb.io/rpc
```

### `broadcast_transaction_synchronous`

同步api，向网络广播一笔带签名的交易，并同步的等待交易结果，视网络及交易确认等因素需要等待2秒左右

::: tip Tips
[如何发起链上交易？](../advanced/send_transaction.md)
:::

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">2</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">broadcast_transaction_synchronous</td>
    </tr>
    <tr>
        <td rowspan="3" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>signed_trx</td>
        <td>带签名的交易消息体</td>
    </tr>
</table>


#### 示例
**request:**
``` bash
    curl --data '{
        "jsonrpc": "2.0",
            "method": "call",
            "params": [2,"broadcast_transaction_synchronous",[{"ref_block_num":63524,"ref_block_prefix":3478923091,"expiration":"2019-01-21T07:59:24","operations":[[0,{"fee":{"amount":1000,"asset_id":"1.3.1"},"from":"1.2.22","to":"1.2.18","amount":{"amount":100000,"asset_id":"1.3.1"},"extensions":[]}]],"extensions":[],"signatures":["20165321fabdce0ca561370ba547738be12a33b929b17889845ab9b8c1a4ed2fa04bc555205bc945cf6f0129765a0f1c06265437c111957a4008167ef720c49f71"]}]],
            "id": 1
    }' https://node23.gxb.io/rpc
```

**response:**
```json
{
    "id": 1,
        "jsonrpc": "2.0",
        "result": {
            "id": "8e2a0d30d68a6a34f58cece5b7879d8a8ec123bd", // txid
            "block_num": 10680361,
            "trx_num": 0,
            "trx": {
                "ref_block_num": 63524,
                "ref_block_prefix": 3478923091,
                "expiration": "2019-01-21T07:59:24",
                "operations": [
                    [0, {
                        "fee": {
                            "amount": 1000,
                            "asset_id": "1.3.1"
                        },
                        "from": "1.2.22",
                        "to": "1.2.18",
                        "amount": {
                            "amount": 100000,
                            "asset_id": "1.3.1"
                        },
                        "extensions": []
                    }]
                ],
                "extensions": [],
                "signatures": ["20165321fabdce0ca561370ba547738be12a33b929b17889845ab9b8c1a4ed2fa04bc555205bc945cf6f0129765a0f1c06265437c111957a4008167ef720c49f71"],
                "operation_results": [
                    [0, {}]
                ]
            }
        }
}
```

## 抵押投票查询接口
### `get_staking_objects`

根据账户返回抵押投票对象

#### 参数说明

<table>
    <tr>
        <th rowspan="1">请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">get_staking_objects</td>
    </tr>
    <tr>
        <td rowspan="3" >API Parameters</td>
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>account_id</td>
        <td>账户ID</td>
    </tr>
</table>

#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "get_staking_objects",["1.2.22"]],
        "id": 1
}' https://testnet.gxchain.org | json_pp
```

**response:**
```json
{
   "id" : 1,
   "result" : [
      {
         "amount" : {
            "asset_id" : "1.3.1", //资产类别
            "amount" : 1000000    //抵押数量
         },
         "program_id" : "1",      //账户抵押第一项
         "weight" : 1,            //抵押权重
         "id" : "1.27.0",         //抵押对象
         "staking_days" : 90,     //抵押时长(天)
         "create_date_time" :    "2020-01-16T08:40:33",   //创建时间
         "trust_node" : "1.6.2",  //抵押节点
         "owner" : "1.2.22",      
         "is_valid" : true        //是否有效
      },
      {
         "amount" : {
            "asset_id" : "1.3.1",
            "amount" : 1500000
         },
         "program_id" : "2",
         "weight" : 2,
         "id" : "1.27.1",
         "staking_days" : 360,
         "create_date_time" : "2020-01-16T09:10:00",
         "trust_node" : "1.6.2",
         "is_valid" : true,
         "owner" : "1.2.22"
      },
      {
         "amount" : {
            "amount" : 900000000,
            "asset_id" : "1.3.1"
         },
         "program_id" : "3",
         "weight" : 4,
         "id" : "1.27.62",
         "staking_days" : 720,
         "owner" : "1.2.22",
         "is_valid" : true,
         "trust_node" : "1.6.55",
         "create_date_time" : "2020-01-17T05:06:03"
      },
      {
         "id" : "1.27.63",
         "amount" : {
            "asset_id" : "1.3.1",
            "amount" : 1000000
         },
         "weight" : 1,
         "program_id" : "4",
         "trust_node" : "1.6.1",
         "owner" : "1.2.22",
         "is_valid" : false,
         "create_date_time" : "2020-01-17T07:08:48",
         "staking_days" : 15
      },
      {
         "staking_days" : 15,
         "create_date_time" : "2020-02-18T11:41:54",
         "owner" : "1.2.22",
         "is_valid" : true,
         "trust_node" : "1.6.82",
         "amount" : {
            "amount" : "3640000000",
            "asset_id" : "1.3.1"
         },
         "program_id" : "4",
         "weight" : 1,
         "id" : "1.27.10110"
      }
   ],
   "jsonrpc" : "2.0"
}
```
### `get_staking_objects_by_witness`

根据节点ID返回指定指定位置和数量的抵押对象

#### 参数说明

<table>
    <tr>
        <th>请求参数</th>
        <th colspan="2">请求参数说明</th>
    </tr>
    <tr>
        <td>API Id</td>
        <td colspan="2" align="center">0</td>
    </tr>
    <tr>
        <td>API Name</td>
        <td colspan="2" align="center">get_staking_objects_by_witness</td>
    </tr>
    <tr>
        <td rowspan="5" >API Parameters</td>   
    </tr>
    <tr>
        <th>API参数</th>
        <th>API参数说明</th>
    </tr>
    <tr>
        <td>witness_id</td>
        <td>节点ID</td>
    </tr>
    <tr>
        <td>start</td>
        <td>起始对象ID</td>
    </tr>
    <tr>
        <td>limit</td>
        <td>返回抵押对象数量，最多100个</td>
    </tr>
    
</table>


#### 示例
**request:**
``` bash
curl --data '{
    "jsonrpc": "2.0",
        "method": "call",
        "params": [0, "get_staking_objects_by_witness",["1.6.1","1.27.2","3"]],
        "id": 1
}' https://testnet.gxchain.org | json_pp
```

**response:**
```json
{
   "id" : 1,
   "jsonrpc" : "2.0",
   "result" : {
      "next_id" : "1.27.65",
      "records" : [
         {
            "create_date_time" : "2020-01-17T02:19:12",  //生成时间
            "staking_days" : 360,   //抵押天数
            "owner" : "1.2.3946",   //拥有账户
            "weight" : 2,           //抵押权重
            "amount" : {
               "amount" : 2400001,  //抵押数量
               "asset_id" : "1.3.1"
            },
            "id" : "1.27.2",        //抵押对象
            "is_valid" : true,      //是否有效
            "trust_node" : "1.6.1", //抵押节点
            "program_id" : "2" 
         },
         {
            "owner" : "1.2.3950",
            "staking_days" : 720,
            "create_date_time" : "2020-01-17T04:59:18",
            "weight" : 4,
            "amount" : {
               "asset_id" : "1.3.1",
               "amount" : 1000000000
            },
            "program_id" : "3",
            "id" : "1.27.42",
            "is_valid" : true,
            "trust_node" : "1.6.1"
         },
         {
            "amount" : {
               "asset_id" : "1.3.1",
               "amount" : 1000000
            },
            "is_valid" : false,
            "id" : "1.27.63",
            "trust_node" : "1.6.1",
            "program_id" : "4",
            "create_date_time" : "2020-01-17T07:08:48",
            "staking_days" : 15,
            "owner" : "1.2.22",
            "weight" : 1
         }
      ],
      "more" : true      //是否还有更多抵押项
   }
}
```