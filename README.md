# Hyperledger-Indy-Tutorial
Please follow the following tutorial for running the project:

https://medium.com/@taseen.junaid/hyperledger-indy-custom-network-with-indy-node-plenum-protocol-ledger-85fd10eb5bf5


## Presetup 
`git clone https://github.com/wYaobiz/Hyperledger-Indy-Tutorial`

`sudo bash prerequisites.sh`

## Generating public info using private/secret seed value
### Trustee 
`python3 get_did_and_verkey.py --seed T0003000u0I000D000F000g0Trustee1`

### Stewards 1, 2, and 3
`python3 get_did_and_verkey.py --seed 100A000000300000c0000000Steward1`

`python3 get_did_and_verkey.py --seed 300600b0D030000000z00000Steward2`

`python3 get_did_and_verkey.py --seed v000K00l0000S000000e0000Steward3`

### Nodes:
`sudo python3 init_indy_node.py --name Node1 --seed 4000F000u00000D0000000g0000Node1`

`sudo python3 init_indy_node.py --name Node2 --seed T00000000u0000I0000v0003000Node2`

`sudo python3 init_indy_node.py --name Node3 --seed 300000A00u000z0000600003000Node3`

## Single Host Network Development:
`sudo python3 clear_setup.py --full True --network sandbox`

`sudo bash single_host_generation.sh`

For Node 1:
`sudo python3 start_indy_node.py Node1 0.0.0.0 9701 0.0.0.0 9702`

For Node 2: 
`sudo python3 start_indy_node.py Node2 0.0.0.0 9703 0.0.0.0 9704`

For Node 3:
`sudo python3 start_indy_node.py Node3 0.0.0.0 9705 0.0.0.0 9706`

Check the node information:
`sudo python3 validator_info.py`

To restart the stopped node: 
`sudo bash restart_indy_node.sh`


## Multi Hosts Network Development
### Host 1
`sudo python3 clear_setup.py --full True --network sandbox`

`sudo bash multi_host_host1_generation.sh`

`sudo python3 start_indy_node.py Node1 0.0.0.0 9701 0.0.0.0 9702`

To check node information and to restart stopped node
`sudo python3 validator_info.py`

`sudo bash restart_indy_node.sh`

### Host 2
`sudo python3 clear_setup.py --full True --network sandbox`

`sudo bash multi_host_host1_generation.sh`

`sudo python3 start_indy_node.py Node2 0.0.0.0 9703 0.0.0.0 9704`

To check node information and to restart stopped node
`sudo python3 validator_info.py`

`sudo bash restart_indy_node.sh`


### Host 3
`sudo python3 clear_setup.py --full True --network sandbox`

`sudo bash multi_host_host1_generation.sh`

`sudo python3 start_indy_node.py Node3 0.0.0.0 9705 0.0.0.0 9706`

To check node information and to restart stopped node
`sudo python3 validator_info.py`
`sudo bash restart_indy_node.sh`


## Testing with SDK Applications
`python3 -m src.sdk_sample`
