# Expansion


## Start private chain locally
Reference [Private Chain](../advanced/private_chain.html)

## Deploy testnet node

Reference [Testnet](../advanced/testnet.html)

## Random number

 We are unable to generate verifiable random numbers on the blockchain. We need to select a fixed seed to generate a random number and generally generate a random sequence through a hash algorithm such as sha256. Therefore, the safety of random numbers and the selection of seeds are crucial. If you choose a variable that can be obtained on the chain as a random number, such as the block id, the number of blocks, the balance of the assets, etc. ,once the random algorithm of the contract is leaked out, the attacker can get the random number before the blockchain and predict the data related to the random number. Therefore, the random number algorithm should be as complex as possible, or we should use out-of-chain data as a random number seed. The following is an example of generating random numbers from out-of-chain data.

- 1. Create a random number for each of the opponents (Alice and Bob) and calculate their hash value.
```bash
Alice:Randomly create a string, for example: "I am Alice" and generate a sha256 hash
zhaoxiangfei@zhaoxiangfeideMacBook-Pro:~$ echo "I am Alice" | shasum -a 256
da161d9ee3c116083030737d5a4d478ee1a7654f8ea51e0513020937a9206b0f

Bob:Randomly create a string, for example: "I am Bob" and generate a sha256 hash
zhaoxiangfei@zhaoxiangfeideMacBook-Pro:~$ echo "I am Bob" | shasum -a 256
77f3bfe06cc926329510b60eba56f80a8d32cf35496587d1444fc690c806c0f9
```
- 2. The opponents each generate their own random number and hash value, and they both submit the hash value to the chain in the first interaction.
```
After the hash value is submitted to the chain, the random string corresponding to the hash value is fixed, but neither one can derive the random string of the opponent based on the hash value.
```

- 3. Both parties submit their own random string, and the contract will check against the submitted string by the hash value of the last commit,then use two hash values and two random strings for splicing to generate a hash sequence as a random number.
```bash
sha256("da161d9ee3c116083030737d5a4d478ee1a7654f8ea51e0513020937a9206b0f"+"77f3bfe06cc926329510b60eba56f80a8d32cf35496587d1444fc690c806c0f9"+"I am Alice"+"I am Bob")
```
- 4.The two sides generate a random sequence through two interactions. When the first interaction ends, the content to be submitted for the second interaction is determined, but the final random sequence has not yet been determined, thus preventing both parties from cheating.

## Contract and distributed storage

Smart contracts bring the possibility of decentralization of complex business logic, and can store relevant business data in the chain and develop decentralized DAPP. The storage on the chain uses RAM resources, which are suitable for storing high-frequency readable and writable data. The RAM on the chain is expensive to store, so some large files do not need to be stored in the chain ram. You can use the distributed storage service provided by GXChian to put large files on [BaaS Storage](../ecosystem/baas_storage.html).

## Contract fee

In order to use blockchain reasonably, every time you call a smart contract, you need to pay certain miner’s fee which include three parts: the base fee (fixed), the memory fee (based on the persistent storage usage), and the CPU fee (billing based on the CPU time occupied by this call), the price of the three types of fees and the CPU limit of the calling contract can be dynamically adjusted by the board. Smart contract fee calculation rules:

Contract Deployment Fee: Base Fee + Transaction Message Size * Unit KB Fee

```cpp
deploy_fee = basic_fee+transaction_size*price_per_kb
```

Contract call fee: Base fee + ram usage + cpu usage

```cpp
transaction_fee = basic_fee + ram_usage * price_per_kb + cpu_usage * price_per_ms
```


## Built-in_api_example

```cpp
#include <graphenelib/system.h>
#include <graphenelib/contract.hpp>
#include <graphenelib/dispatcher.hpp>
#include <graphenelib/print.hpp>
#include <graphenelib/types.h>
#include <graphenelib/multi_index.hpp>
#include <graphenelib/global.h>
#include <graphenelib/asset.h>
#include <graphenelib/crypto.h>

using namespace graphene;

class example : public contract
{
  public:
    example(uint64_t id)
        : contract(id){}

    //current_receiver
    // @abi action
    void examcurr(){
        uint64_t ins_id = current_receiver();
        print("current contract account id: ", ins_id);
    }

    //get_action_asset_id
    // @abi action
    // @abi payable
    void examgetast(){
        uint64_t ast_id = get_action_asset_id();
        print("call action asset id: ",ast_id);
    }

    //get_action_asset_amount
    // @abi action
    // @abi payable
    void examgetamo(){
        uint64_t amount = get_action_asset_amount();
        print("call action asset amount: ",amount);      
    }

    //deposit
    // @abi action
    // @abi payable
    void examdepo(){
        uint64_t ast_id = get_action_asset_id();
        int64_t amount = get_action_asset_amount();

        print("call action asset id: ",ast_id);
        print("\n");
        print("call action asset amount: ",amount);  
    }
    //withdraw_asset
    // @abi action
    void examwith(uint64_t to, uint64_t asset_id, int64_t amount){
        withdraw_asset(_self,to,asset_id,amount);
        print("withdraw_asset example");
    }

    //get_balance
    // @abi action
    void examgetbl(int64_t account, int64_t asset_id){
        int64_t balance = get_balance(account, asset_id);
        print("account balance: ",balance);
    }
    //sha256
    // @abi action
    void examsha25(std::string data){
        checksum256 hash;
        sha256(data.c_str(),data.length(),&hash);
        printhex(hash.hash,32);
    }

    //sha512
    // @abi action
    void examsha512(std::string data){
        checksum512 hash;
        sha512(data.c_str(),data.length(),&hash);
        printhex(hash.hash,64);
    }

    //ripemd160
    // @abi action
    void examripemd(std::string data){
        checksum160 hash;
        ripemd160(data.c_str(),data.length(),&hash);
        printhex(hash.hash,20);
    }

    //verify_signature (other example: redpacket)
    // @abi action
    void examverify(std::string data,signature sig,std::string pk){
        bool result;
        result = verify_signature(data.c_str(), data.length(), &sig, pk.c_str(), pk.length());
        print("verify result: ",result);
    }

    //get_head_block_num
    // @abi action
    void examgetnum(){
        int64_t head_num = get_head_block_num();
        print("head block num: ",head_num);
    }

    //get_head_block_id
    // @abi action
    void examgetid(){
        checksum160 block_hash;
        get_head_block_id(&block_hash);
        printhex(block_hash.hash,20);
    }

    //get_block_id_for_num
    // @abi action
    void examidnum(uint64_t num){
        checksum160 block_hash;
        get_block_id_for_num(&block_hash,num);             
        printhex(block_hash.hash,20);
    }

    //get_head_block_time
    // @abi action
    void examgettime(){
        int64_t head_time;
        head_time = get_head_block_time();
        print("head block time: ",head_time);
    }

    //get_trx_sender
    // @abi action
    void examgettrx(){
        int64_t sender_id;
        sender_id = get_trx_sender();
        print("call action instance id: ",sender_id);
    }

    //get_account_id
    // @abi action
    void examgetacid(std::string data){
        int64_t acc_id;
        acc_id = get_account_id(data.c_str(), data.length());
        print("account id: ",acc_id);
    }

    //get_account_name_by_id
    // @abi action
    void examgetname(int64_t accid){
        char data[13]={0};
        int64_t result;
        result = get_account_name_by_id(data,13,accid);
        prints(data);
    }

    //get_asset_id
    // @abi action
    void examassid(std::string data){
        int64_t assid;
        assid = get_asset_id(data.c_str(),data.length());
        print("asset id: ",assid);
    }

    //read_transaction
    // @abi action
    void examreadtrx(){
        int dwsize;
        dwsize =transaction_size();
        char* pBuffer = new char[dwsize];
        uint32_t size = read_transaction(pBuffer,dwsize);
        print("hex buffer: ");
        printhex(pBuffer,dwsize);
        delete[] pBuffer;
    }

    // @abi action
    void examtrxsize(){
        int dwsize;
        dwsize =transaction_size();
        print("the size of the serialize trx: ",dwsize);
    }

    //expiration
    // @abi action
    void exampira(){
        uint64_t timenum = expiration();
        print("the expiration time: ", timenum);
    }

    //tapos_block_num
    // @abi action
    void examtapnum(){
        uint64_t tapos_num;
        tapos_num = tapos_block_num();
        print("ref block num: ",tapos_num);
    }

    //tapos_block_prefix
    // @abi action
    void examtappre(){
        uint64_t tapos_prefix;
        tapos_prefix = tapos_block_prefix();
        print("ref block id: ",tapos_prefix);
    }

    //graphene_assert
    // @abi action
    void examassert(){
        uint64_t number=1;
        graphene_assert(number == 1, "wrong!");
    }

    //graphene_assert_message
    // @abi action
    void examassmsg(){
        uint64_t number=1;
        std::string msg = "wrong!!!";
        graphene_assert_message(number == 1, msg.c_str(),msg.length());
    }

    //print
    // @abi action
    void examprint(){
        print("example example example!!!");
    }
};

GRAPHENE_ABI(example,(examcurr)(examgetast)(examgetamo)(examdepo)(examwith)(examgetbl)(examsha25)(examsha512)(examripemd)(examverify)(examgetnum)(examgetid)(examidnum)(examgettime)(examgettrx)(examgetacid)(examgetname)(examassid)(examreadtrx)(examtrxsize)(exampira)(examtapnum)(examtappre)(examassert)(examassmsg)(examprint))

```
