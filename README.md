    Let's create a wallet
    $ cleos wallet create
    
    Import private key
    $ cleos wallet import --private-key 5KQwrPbwdL6PhXujxW37FSSQZ1JiwsST4cqQzDeyXtP79zkvFD3 
    
    Eosio account creates an account called eosio.bios
    $ cleos create account eosio eosio.bios EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
    
    We upload the bios contract to the eosio.bios account with permission from eosio.bios
    $ cleos set contract eosio.bios contracts/eosio.bios -p eosio.bios
    
    Eosio creates an account called eosio.msig
    $ cleos create account eosio eosio.msig EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
      
    We then upload the contract eosio.msig into the eosio.msig account  
    $ cleos set contract eosio.msig contracts/eosio.msig -p eosio.msig
    
    Eosio creates an account called eosio.token    
    $ cleos create account eosio eosio.token EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
    
    We then upload the token contract into the account
    $ cleos set contract eosio.token contracts/eosio.token -p eosio.token
    
    We tell the eosio.token contract to create tokens and then issue the tokens to the eosio account
    $ cleos push action eosio.token create '{"issuer":"eosio", "maximum_supply":"1000000000.0000 EOS", "can_freeze":0, "can_recall":0, "can_whitelist":0}' -p eosio.token
    
    Let's issue tokens to the account eosio
    $ cleos push action eosio.token issue '["eosio","1000000000.0000 EOS","deposit started"]' -p eosio
    
    Let's get the balance of the eosio account for the tokens we just created
    $ cleos get currency balance eosio.token eosio EOS

    ################################################################
    
    $ cleos set contract eosio contracts/eosio.system -p eosio
        Usage: cleos system SUBCOMMAND

        Subcommands:
        newaccount                  Create an account, buy ram, stake for bandwidth for the account
        regproducer                 Register a new producer
        unregprod                   Unregister an existing producer
        voteproducer                Vote for a producer
        listproducers               List producers
        delegatebw                  Delegate bandwidth
        undelegatebw                Undelegate bandwidth
        buyram                      Buy RAM
        sellram                     Sell RAM
        claimrewards                Claim producer rewards
        regproxy                    Register an account as a proxy (for voting)
        unregproxy                  Unregister an account as a proxy (for voting)
        canceldelay                 Cancel a delayed transaction

    ################################################################

    $ cleos system newaccount eosio more1 EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV --stake-net '0.001 EOS' --stake-cpu '0.001 EOS' --buy-ram-EOS '0.1 EOS' --transfer -p eosio
    
    ################################################################

    $ cleos get account more1
    privileged: false
    permissions: 
        owner     1:    1 EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
            active     1:    1 EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV
    memory: 
        quota:            6871 bytes    used:            3558 bytes

    net bandwidth:
        staked:          0.0010 EOS           (total stake delegated from account to self)
        delegated:       0.0000 EOS           (total staked delegated to account from others)
        used:             ~0 bytes (past 3 days)   (assuming current congestion and current usage)
        available:        ~379.424697 Gb   (assuming current congestion and 0 usage in current window)

    cpu bandwidth:
        staked:     139770.3940 EOS           (total stake delegated from account to self)
        delegated:  -139770.070 EOS           (total staked delegated to account from others)
        used:      ~0.000000 sec (past 3 days)
        available:        ~471.232227 days

    producers:     <not voted>

    ################################################################
    
    $ cleos system regproducer prod1 EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV http://info.prod1.com -p prod1

    ################################################################
    
    $ cleos system listproducers
    Producer      Producer key                                           Url                                               Total votes
    prod1         EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV  http://info.prod1.com                             0.00000000000000000
    prod2         EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV  http://info.prod2.com                             0.00000000000000000
    prod3         EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV  http://info.prod3.com                             0.00000000000000000
    $ cleos system unregprod prod3 -p prod3
    
    ################################################################
    
    $ cleos system newaccount eosio voter1 EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV --stake-net '0.01 EOS' --stake-cpu '0.01 EOS' --buy-ram-EOS '0.1 EOS' --transfer -p eosio
    
    ################################################################

    $ cleos system newaccount eosio voter2 EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV --stake-net '0.02 EOS' --stake-cpu '0.02 EOS' --buy-ram-EOS '0.1 EOS' --transfer -p eosio
    $ cleos system newaccount eosio voter3 EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV --stake-net '0.02 EOS' --stake-cpu '0.01 EOS' --buy-ram-EOS '0.1 EOS' --transfer -p eosio

    ################################################################
    $ cleos system voteproducer prods voter1 prod1 -p voter1
    $ cleos system voteproducer prods voter2 prod1 -p voter2

    ################################################################

    $ cleos system listproducers
    Producer      Producer key                                           Url                                               Total votes
    prod3         EOS1111111111111111111111111111111114T1Anm             http://info.prod3.com                             0.00000000000000000
    prod2         EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV  http://info.prod2.com                             161362947941973152.00000000000000000
    prod1         EOS6MRyAjQq8ud7hVNYcfnVPJqcVpscN5So8BhtHuGYqET5GDW5CV  http://info.prod1.com                             80681473970986576.00000000000000000


    #################################################################
    $ cleos get table eosio eosio voters
    {
    "rows": [{
        "owner": "more1",
        "proxy": "",
        "producers": [],
        "staked": 20,
        "last_vote_weight": "0.00000000000000000",
        "proxied_vote_weight": "0.00000000000000000",
        "is_proxy": 0,
        "deferred_trx_id": 0,
        "last_unstake_time": "1970-01-01T00:00:00",
        "unstaking": "0.0000 EOS"
        },{
        "owner": "prod1",
        "proxy": "",
        "producers": [],
        "staked": 20,
        "last_vote_weight": "0.00000000000000000",
        "proxied_vote_weight": "0.00000000000000000",
        "is_proxy": 0,
        "deferred_trx_id": 0,
        "last_unstake_time": "1970-01-01T00:00:00",
        "unstaking": "0.0000 EOS"
        },{
        "owner": "prod2",
        "proxy": "",
        "producers": [],
        "staked": 20,
        "last_vote_weight": "0.00000000000000000",
        "proxied_vote_weight": "0.00000000000000000",
        "is_proxy": 0,
        "deferred_trx_id": 0,
        "last_unstake_time": "1970-01-01T00:00:00",
        "unstaking": "0.0000 EOS"
        },{
        "owner": "prod3",
        "proxy": "",
        "producers": [],
        "staked": 20,
        "last_vote_weight": "0.00000000000000000",
        "proxied_vote_weight": "0.00000000000000000",
        "is_proxy": 0,
        "deferred_trx_id": 0,
        "last_unstake_time": "1970-01-01T00:00:00",
        "unstaking": "0.0000 EOS"
        },{
        "owner": "voter1",
        "proxy": "",
        "producers": [
            "prod1"
        ],
        "staked": 200,
        "last_vote_weight": "80681473970986576.00000000000000000",
        "proxied_vote_weight": "0.00000000000000000",
        "is_proxy": 0,
        "deferred_trx_id": 0,
        "last_unstake_time": "1970-01-01T00:00:00",
        "unstaking": "0.0000 EOS"
        },{
        "owner": "voter2",
        "proxy": "",
        "producers": [
            "prod2"
        ],
        "staked": 400,
        "last_vote_weight": "161362947941973152.00000000000000000",
        "proxied_vote_weight": "0.00000000000000000",
        "is_proxy": 0,
        "deferred_trx_id": 0,
        "last_unstake_time": "1970-01-01T00:00:00",
        "unstaking": "0.0000 EOS"
        },{
        "owner": "voter3",
        "proxy": "",
        "producers": [],
        "staked": 300,
        "last_vote_weight": "0.00000000000000000",
        "proxied_vote_weight": "0.00000000000000000",
        "is_proxy": 0,
        "deferred_trx_id": 0,
        "last_unstake_time": "1970-01-01T00:00:00",
        "unstaking": "0.0000 EOS"
        }
    ],
    "more": false
    }

    $ cleos transfer eosio more1 '200 EOS' 'for test' -p eosio
    $ cleos get currency balance eosio.token more1
    200.0000 EOS

    memory: 
        quota:            6871 bytes    used:            3558 bytes

    $ cleos system buyram more1 more1 '1 EOS'

    memory: 
        quota:           75589 bytes    used:            3688 bytes

    $ cleos system sellram more1 68718 -p more1

    $ cleos system delegatebw more1 more1 '1 EOS' '1 EOS' --transfer -p more1

    $ cleos system undelegatebw more1 more1 '1 EOS' '1 EOS' -p more1

    cleos system newaccount greenunicorn groonunicorn EOS8XEsyTW6uzmfuQh4wFMTDZdW3eH9ZtMtumnok4Frc1DJjuLbxN EOS8XEsyTW6uzmfuQh4wFMTDZdW3eH9ZtMtumnok4Frc1DJjuLbxN --stake-net '0.001 SYS' --stake-cpu '0.001 SYS' --buy-ram '0.1 SYS' --transfer -p greenunicorn

    cleos push action eosio.token issue '["groonunicorn""10000.0000 SYS"]' -p eosio

    cleos get currency balance eosio.token greenunicorn SYS

    cleos system regproducer greenunicorn EOS8dPAzA4bgkTNV1nNDHiNzfAqdeSqGc7b17yJ1XuiTDNM7u9DQN  -p greenunicorn
