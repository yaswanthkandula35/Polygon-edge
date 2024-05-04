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
  --bootnode="/ip4/127.0.0.1/tcp/10001/p2p/16Uiu2HAm1qywzWk8tFe1QhvfVuBcQfQ1zqjs67owpEM8NqUcUsRt" \
  --bootnode="/ip4/127.0.0.1/tcp/10002/p2p/16Uiu2HAmHAEeyCiaQ5B4d2ESeVJ1QwBXZLxHwe546oRHAA9dYYQ9" \
  --bootnode="/ip4/127.0.0.1/tcp/10003/p2p/16Uiu2HAmMznsbWMraJqngiMwEdQRg23o6UsUvdHaxg5StLzoH2vM" \
  --bootnode="/ip4/127.0.0.1/tcp/10004/p2p/16Uiu2HAm5oVbhWMpDQKK8mvd77LBcgdrn9yRSK1yyQXeP5sTL5Ei" \
  --premine=0x800285058e7F9b58014D82A1502BAc9F4317cf96:1000000000000000000000 \
  ````
<!-- add example of th genesis command -->

### Start the Node
````bash
polygon-edge server --data-dir ./<name_of_the_node> --chain genesis.json --libp2p :<port> --jsonrpc :<port2> --grpc-address :<port3> -- seal
````
- This command starts the polygon-edge node.
- Example of the start command:
  ````bash
  polygon-edge server --data-dir ./node-1 --chain genesis.json --grpc-address :20001 --libp2p :10001 --jsonrpc :30001 -- seal
  ````
<!-- add example of the start command -->
