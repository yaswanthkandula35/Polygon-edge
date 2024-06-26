# Setting Up a Polygon-edge Node

### Install go
- Make sure that the go version is 1.17 or higher.

### Install polygon-edge
````bash
git clone https://github.com/0xPolygon/polygon-edge.git  
cd polygon-edge  
go build -o polygon-edge main.go  
sudo mv polygon-edge /usr/local/bin/
````

### Initialize the data directory
````bash
polygon-edge secrets init --data-dir <name_of_the_node> --insecure
````
- Store the ouput of the command (Public key, Node ID and BLS Public Key).

### Generate the genesis file
````bash
polygon-edge genesis \  
--consensus ibft \   
--bootnode=<multi_address_1> \  
--bootnode=<multi_address_2> \  
--premine=<public_key_address>:1000000000000000000 \
````
- The format of the multi_address is `/ip4/<ip_address>/tcp/<port>/p2p/<Node_ID>`. Add as many bootnodes as you want.
- The premine flag is optional. If you want to premine, add the public key address of the account and the amount of tokens you want to premine. 
- The above command creates the genesis.json file.
- Example of the genesis command:
  ````bash
  polygon-edge genesis \
  --consensus ibft \
  --bootnode="/ip4/10.147.18.155/tcp/10001/p2p/16Uiu2HAmUrgETWsWrkcodefm348MpNfUWWmaTFhtnU9giTk595EN" \
--bootnode="/ip4/10.147.18.147/tcp/10001/p2p/16Uiu2HAmCNFveoPRf6QgHzmUDrSqXiRcXxWBuqPy1c2xNgs78tWi" \
--bootnode="/ip4/10.147.18.22/tcp/10001/p2p/16Uiu2HAkwaxgWFgvhfduUhc2qT9W4Me7SPxMRWhdSZqfXkTAZggE" \
--bootnode="/ip4/10.147.18.93/tcp/10001/p2p/16Uiu2HAm2F7wiXfj9E5h2bUzYfYumr4L3ZFcgmSYyL2LpcPMUJ76" \
  --premine=0x800285058e7F9b58014D82A1502BAc9F4317cf96:1000000000000000000000 \
  ````
<!-- add example of th genesis command -->

### Start the Node
````bash
polygon-edge server --data-dir ./<name_of_the_node> --chain genesis.json --libp2p 0.0.0.0:<port> --jsonrpc 0.0.0.0:<port2> --grpc-address 0.0.0.0:<port3> -- seal
````
- This command starts the polygon-edge node.
- Example of the start command:
  ````bash
  polygon-edge server --data-dir ./test-chain-1 --chain genesis.json --grpc-address 0.0.0.0:20001 --libp2p 0.0.0.0:10001 --jsonrpc 0.0.0.0:30001 -- seal
  ````
