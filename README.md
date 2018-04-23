

测试


地区   bp_name     角色   

华北  	eoshuabei		boot
华东  	eoshuadong
华南  	eoshuanan
香港  	eostore
东京  	eostore
新加坡  	eostore



#### config.ini关键项
```
genesis-json = /opt/eosio/bin/data-dir/genesis.json     #非BIOS节点不需要此
http-server-address = 0.0.0.0:8888
p2p-listen-endpoint = 0.0.0.0:9876
agent-name = "EOS Test Agent"
p2p-peer-address =
producer-name =
private-key = ["EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV","5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3"]

plugin = eosio::producer_plugin
plugin = eosio::chain_api_plugin
plugin = eosio::wallet_api_plugin
plugin = eosio::account_history_api_plugin
plugin = eosio::http_plugin
```

#### 华北 启动节点 eosio
```
Step 1:
# mkdir -p /eos/data && mkdir -p /eos/blockchain && mkdir -p /eos/wallet

Step 2:
# docker run -d --restart=always --name nodeos \
    -p 8888:8888 -p 9876:9876 \
    -v /eos/data:/opt/eosio/bin/data-dir \
    -v /eos/blockchain:/root/.local/share/eosio/nodeos/data \
    eosio/eos nodeosd.sh --enable-stale-production --producer-name eosio --plugin eosio::chain_api_plugin --plugin eosio::net_api_plugin
# docker logs -f nodeos

Step 3:
# docker run -d --restart=always --name keosd --link nodeos \
    -v /eos/wallet:/root/eosio-wallet \
    -v /eos/data:/opt/eosio/bin/data-dir \
    eosio/eos keosd
# alias cleos='docker exec keosd cleos -H nodeos'
# cleos get info

Step 4:     
# cleos wallet create       # 之后将钱包password记录在Records.txt
说明:必须先创建wallet(default)，并且包含了eosio的私钥和公钥。

Step 5:
# cleos set contract eosio /opt/eosio/bin/data-dir/contracts/eosio.bios

Step 6:新建用户
# cleos create key          # 执行多次 之后将钱包password记录在Records.txt

# cleos wallet import 5Hpv9p4krLHRfzMaRtiP2wUuSJx5QErPx1xyVWRddTCDkemH5kK
# cleos wallet import 5JtRPPPceNvu1hCkXXoANxtCL3VJK1mYNqy82xJTHpvYRPK5dJm
# cleos wallet import 5HvZaSEkvwsWPa11sD7FbEdjiHodo7BvG75c7v9NYHj458hhaLy
# cleos wallet import 5HwKSKA5QfNgAae3WtRt4oW7EV1gzkjA5jd18qj5M1Wp65BdZhC


# cleos create account eosio eoshuabei EOS6LQ6sGUDNYH35opPHwA1sdw8rjtN9s1ZpF1zA8mgHZQ2xoAgk8 EOS6LQ6sGUDNYH35opPHwA1sdw8rjtN9s1ZpF1zA8mgHZQ2xoAgk8
# cleos create account eosio eoshuadong EOS6PGpv1vuLrsDxwjrz7cU47ueKz3twp4Et48qJoPFux2Z6y7bDZ EOS6PGpv1vuLrsDxwjrz7cU47ueKz3twp4Et48qJoPFux2Z6y7bDZ
# cleos create account eosio eoshuanan EOS7Gn3L4Pf7oUgqdaXPKg7SEDAkxiYNntmf83CGHS1Bq5sZfpcft EOS7Gn3L4Pf7oUgqdaXPKg7SEDAkxiYNntmf83CGHS1Bq5sZfpcft
# cleos create account eosio eostore EOS6pB118BPnUySPhojFkwrQ8Kz8sQLqQc41BCcJzvQsK2Wq5X3Dk EOS6pB118BPnUySPhojFkwrQ8Kz8sQLqQc41BCcJzvQsK2Wq5X3Dk 

```  
    
东京节点
```
Step 1:
# mkdir -p /eos/data && mkdir -p /eos/blockchain && mkdir -p /eos/wallet

Step 2:
# docker run -d --restart=always --name nodeos \
    -p 8888:8888 -p 9876:9876 \
    -v /eos/data:/opt/eosio/bin/data-dir \
    -v /eos/blockchain:/root/.local/share/eosio/nodeos/data \
    eosio/eos nodeos --resync \
    --producer-name eostore \
    --plugin eosio::chain_api_plugin \
    --plugin eosio::net_api_plugin \
    --p2p-peer-address 47.104.242.13:9876 \
    --private-key [\"EOS6pB118BPnUySPhojFkwrQ8Kz8sQLqQc41BCcJzvQsK2Wq5X3Dk\",\"5HwKSKA5QfNgAae3WtRt4oW7EV1gzkjA5jd18qj5M1Wp65BdZhC\"]
# docker logs -f nodeos



nodeos --producer-name inita --plugin eosio::chain_api_plugin --plugin eosio::net_api_plugin --http-server-address 127.0.0.1:8889 --p2p-listen-endpoint 127.0.0.1:9877  --config-dir node2 --data-dir node2 --private-key [\"EOS6hMjoWRF2L8x9YpeqtUEcsDKAyxSuM1APicxgRU1E3oyV5sDEg\",\"5JgbL2ZnoEAhTudReWH1RnMuQS6DBeLZt4ucV6t8aymVEuYg7sr\"]


```  
    

