# Kyve-points-exporter
> Simple exporter to check your points for staker pools

## Install  

### Download exporter: 
```bash 
wget https://github.com/prometheus-community/json_exporter/releases/download/v0.6.0/json_exporter-0.6.0.linux-amd64.tar.gz
```

### Run
```bash
./json_exporter --config.file config/config.yml
```

## Usage 
### Config example 
```yml
modules:
  default:
    metrics:
    - name: staker_pools
      type: object
      path: '{.staker.pools[*]}'
      help: Accumulated points for staker pools
      labels:
        pool_id: '{.pool.id}'
        name: '{.pool.name}'
        valaddress: '{.valaddress}'
      values:
        points: '{.points}'
```

### Example of a request:
```bash 
curl "http://localhost:7979/probe?module=default&target=https://api-eu-1.kyve.network/kyve/query/v1beta1/staker/<your_validator_address>"
```

Where ```<your_validator_address>``` is the address of your validator.

### Metrics expose example 
```
# HELP staker_pools_points Accumulated points for staker pools
# TYPE staker_pools_points untyped
staker_pools_points{name="Archway",pool_id="2",valaddress="kyve1mexx659tur2pjl7t3uw54qz7p83pxzqprz728e"} 0
staker_pools_points{name="Archway // State-Sync",pool_id="4",valaddress="kyve1x3el3e472xuycwm4ushluk8pz2hqas30x729pf"} 0
staker_pools_points{name="Axelar",pool_id="3",valaddress="kyve1meul0rhp09gflv3usfdjrqzlyx6r5gxddw7zqh"} 0
staker_pools_points{name="Celestia",pool_id="9",valaddress="kyve17l8fnm0j8hxy5gwgy0290fw03cyrwrjefrnvf4"} 0
staker_pools_points{name="Celestia // State-Sync",pool_id="10",valaddress="kyve1cy78qv97vmv2wjh4qprxqcsppg3w937g2uthp6"} 0
staker_pools_points{name="Cosmos Hub",pool_id="0",valaddress="kyve1ucwlrnkul6ytq8apzeuu6t3svvm74rf0zn8cy7"} 0
staker_pools_points{name="Cronos",pool_id="5",valaddress="kyve1dwwduejtg5c2w364664zajj6psh3xtwky32u33"} 0
staker_pools_points{name="Cronos // State-Sync",pool_id="6",valaddress="kyve1lehtu2eyywdurvd87uas08rlrm4y527sdvv9w5"} 0
staker_pools_points{name="Noble",pool_id="7",valaddress="kyve1x30ul204wtn8y0a3e3p6w532ek0h737ldgtn0y"} 0
staker_pools_points{name="Noble // State-Sync",pool_id="8",valaddress="kyve1g422nznmzr2ds89exrk2lqgdfn4fdpcyjv278j"} 0
staker_pools_points{name="Osmosis",pool_id="1",valaddress="kyve17slfz0wad485cq555xyc9gnk06j303tyx8k3df"} 0
```