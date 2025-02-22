# FHWA Blockchain Deployment Documentation
Please follow the following the hands on tutorial for deploying the project:


## Prerequisites
 - OS: Ubuntu 16.04 LTS, also know as Ubuntu Xential.
 - Git: Any version later than 2.7.

## Presetup  
Please clone our project by using the following command: 

`git clone https://github.com/wYaobiz/Hyperledger-Indy-Tutorial`

Run the bash script to download required components and libraries, and set up the environment.

`sudo bash prerequisites.sh`

## Generating public info using private/secret seed value
To formlized the pool, we needs four nodes, which consists of one trustee node and three stewards in Indy network. 

- Trustee: An Identity Owner entrusted with specific identity control responsibilities by another Identity Owneror with specific governance responsibilities by a Governance Framework. 
- Steward: An Organization approved by the Sovrin Foundation to operate a Node. 


Both trustee and steward can be validator nodes. 

Seed is a 32 character long value which acts as an actor’s/component’s private information which is not shareable with others for security reasons. By using seed value, we can generate public information and can share those public information via agents or other mediums.

By calling “get_did_and_verkey.py” with 32 character long seed value, different actors can see their DID (Decentralized Identity) and verification keys.

### Trustee 
First and foremost actors of our network are trustees. Domain ledger transactions start with trustee. In domain ledger, a trustee can add new stewards too. Both trustee and stewards have power to write on domain ledger. We have one trustee with seed value “T0003000u0I000D000F000g0Trustee1” by using the command: 

`python3 get_did_and_verkey.py --seed T0003000u0I000D000F000g0Trustee1`

### Stewards 1, 2, and 3
Stewards have power to write on both domain ledger and pool ledger. A steward can add a new node by using pool ledger transactions. A steward can add only one node and so each steward can add its only node into networks. We use three stewards with seed values by using the following command:

`python3 get_did_and_verkey.py --seed 100A000000300000c0000000Steward1`

`python3 get_did_and_verkey.py --seed 300600b0D030000000z00000Steward2`

`python3 get_did_and_verkey.py --seed v000K00l0000S000000e0000Steward3`

### Nodes:
Every node is a network component which holds ledgers. Users need to initialize each node by calling “init_indy_node.py” with the node name and node’s seed value. We set up three nodes by using seed with value through the following command: 

`sudo python3 init_indy_node.py --name Node1 --seed 4000F000u00000D0000000g0000Node1`

`sudo python3 init_indy_node.py --name Node2 --seed T00000000u0000I0000v0003000Node2`

`sudo python3 init_indy_node.py --name Node3 --seed 300000A00u000z0000600003000Node3`

## Single Host Network Development:
To run the network on a single host, we can use the following command to clear whatever we have done in the previous steps and initialize nodes and generate ledger:

`sudo python3 clear_setup.py --full True --network sandbox`

`sudo bash single_host_generation.sh`

We use the following command to start each nodes. 

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
To host the network on multiple hosts, we have to follow the each command in this section. To use your own IP, then you have to edit the “- -ips” flag of multi_host_host1_generation.sh, multi_host_host2_generation.sh, multi_host_host3_generation.sh files. Actually for each node, you have to write that node’s generation file so that no one will be able to know that node’s seed value. 

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
Once the network has been set up, we can use the following command to run a test sample. 

`python3 -m src.sdk_sample`
