# Ritual is the solution.
Ritual is the network for open AI infrastructure. We build groundbreaking, new architecture on a crowdsourced governance layer aimed to handle safety, funding, alignment, and model evolution.

## Step-by-Step Setup Guide
1. Update and Upgrade Packages:
```sh
sudo apt update && sudo apt upgrade -y
```
2.Install Required Packages:
```sh
sudo apt install -y curl git jq lz4 build-essential tmux
```
Installs essential development tools (curl, git, jq, lz4, build-essential) and tmux.
3.Install git-all Package:
```sh
sudo apt install git-all
```
Installs a comprehensive set of Git tools including additional plugins and features.

4.Install Docker:
```sh
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```
Installs prerequisites for adding Docker's official repository.

Add Docker's Official GPG Key:
```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```
Add Docker APT Repository:
```sh
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
Adds Docker's APT repository to your system's software sources.

Update Package List Again:
```sh
sudo apt update
```
Updates the package list to include Docker packages from the newly added repository.

Install Docker Community Edition (CE):
```sh
sudo apt install docker-ce
```
Run Docker Hello World Container:
```sh
sudo docker run hello-world
```
<img width="1295" alt="Screenshot 2024-06-28 at 2 12 57 AM" src="https://github.com/0xHawre/RItual-nodes-/assets/131952165/364740e7-09b8-4cb6-8f67-a47e6ab97357">

5.Clone the GitHub Repository:
```sh
git clone https://github.com/ritual-net/infernet-container-starter && cd infernet-container-starter
```
This command clones the repository https://github.com/ritual-net/infernet-container-starter to your current directory (.), and then changes into the infernet-container-starter directory.

6.Start a tmux Session:
```sh
tmux new-session -s ritual
```
tmux is a terminal multiplexer that allows you to create and manage multiple terminal sessions within a single terminal window or SSH session.
new-session creates a new tmux session.
-s ritual names the session as ritual.

7. Run the node
```sh
project=hello-world make deploy-container
```
<img width="850" alt="Screenshot 2024-06-28 at 2 16 17 AM" src="https://github.com/0xHawre/RItual-nodes-/assets/131952165/751236c7-fac2-455b-b645-bb043222f718">
check out block numbers should be number not ERR

go to https://basescan.org/address/0x8d871ef2826ac9001fb2e33fdd6379b6aabf449c#writeContract
![Screenshot 2024-06-28 at 2 19 14 AM](https://github.com/0xHawre/RItual-nodes-/assets/131952165/535e1c57-cfea-43d0-9ab8-66777bc1626a)

connect wallet (you will need privat key so use a new wallet and make sure you have at least 10$ balance in ETH at base network)

![Screenshot 2024-06-28 at 3 27 05 AM](https://github.com/0xHawre/RItual-nodes-/assets/131952165/906e0ba9-fa91-467a-b7d0-8acdb5b624f1)
 input your wallet’s public address into the “node (address)” field of the “registerNode” function and confirm the transaction. After waiting for 1 hour, proceed to activate your node using the “activateNode” function. This process is important for integrating your node with the network.

# now  we need to config node 
```sh
nano ~/infernet-container-starter/deploy/config.json
```
1.change "registry_address": "0x663F3ad617193148711d28f5334eE4Ed07016602", to  "registry_address": "0x3B1554f346DFe5c482Bb4BA31b880c1C18412170",
2.change rpc_url to https://base-rpc.publicnode.com
3.change private_key to your wallet's private key.
"Note: Make sure to start your private keys with '0x'. For example, '0xdsjflkjflk….fddfsdaf'."
Press crtl+x press y  press enter

```sh
nano ~/infernet-container-starter/projects/hello-world/contracts/Makefile
```
1.change sender's address to your wallet's private key. 
"Note: Make sure to start your private keys with '0x'. For example, '0xdsjflkjflk….fddfsdaf'."
2.change RPC_URL to https://base-rpc.publicnode.com
Press crtl+x press y  press enter

```sh
nano ~/infernet-container-starter/projects/hello-world/contracts/script/Deploy.s.sol
```
1.change  "registry_address": address   to  0x3B1554f346DFe5c482Bb4BA31b880c1C18412170
2.change private_key to your wallet's private key.
"Note: Make sure to start your private keys with '0x'. For example, '0xdsjflkjflk….fddfsdaf'."
Press crtl+x press y  press enter



```sh
docker compose down
```
<img width="818" alt="Screenshot 2024-06-28 at 2 58 42 AM" src="https://github.com/0xHawre/RItual-nodes-/assets/131952165/c095010d-5ceb-47c8-9daa-b637392fc612">


```sh
docker compose up -d
```
<img width="818" alt="Started" src="https://github.com/0xHawre/RItual-nodes-/assets/131952165/39eec99d-af27-4a2c-a797-f1323d741d87">

```sh

docker restart infernet-node
docker restart hello-world
docker restart deploy-redis-1
docker restart infernet-anvil
docker restart deploy-fluentbit-1
```

output like :
output like 
infernet-node
hello-world
deploy-redis-1
infernet-anvil
deploy-fluentbit-1

back to yore home and cret foudry file 
```sh
cd && mkdir foundry &&  cd foundry
```

install foundry 
```sh
curl -L https://foundry.paradigm.xyz | bash
```

run foundrt 
```sh
source ~/.bashrc  &&
foundryup
```

<img width="818" alt="Portable and nodular toolkit" src="https://github.com/0xHawre/RItual-nodes-/assets/131952165/b5a6d947-0260-4328-b95f-5fa09a04cee3">

go back to the nfernet-container file 
```sh
cd  &&  cd infernet-container-starter/projects/hello-world/contracts/lib/
```

delet  forge-std  and nfernet-sdk
```sh
rm -r forge-std && rm -r infernet-sdk
```

compile code 
```sh
forge install --no-commit foundry-rs/forge-std
```
install sdk 
```sh
forge install --no-commit ritual-net/infernet-sdk
```

back to infernet-container-starter
```sh
cd && cd infernet-container-starter
```

run!
```sh
project=hello-world make deploy-contracts
```

<img width="818" alt="Script ran successtully" src="https://github.com/0xHawre/RItual-nodes-/assets/131952165/fd42d290-f02f-4261-8d47-5fc20b6ccfa0">

copy deployed sayshello address(in this case is 0xEB98450529626d294f17fBA0235650193b8be8A1)

edit solidity contract 
```sh
nano ~/infernet-container-starter/projects/hello-world/contracts/script/CallContract.s.sol
```
 SaysGM saysGm = SaysGM(0x13D69Cf7d6CE4218F646B759Dcf334D82c023d8e); replace deployed sayshello address insted this address 

 Press crtl+x  press y press enter

 deploy contract 
 ```sh
make call-contract project=hello-world
```
and DONE
checking logs 


```sh
docker logs infernet-node 
```

<img width="1566" alt="Screenshot 2024-06-28 at 3 10 11 AM" src="https://github.com/0xHawre/RItual-nodes-/assets/131952165/88f1f35f-33c8-4218-9a23-6c46225d758c">


```sh
docker logs infernet-anvil 
```

<img width="1566" alt="Screenshot 2024-06-28 at 3 10 30 AM" src="https://github.com/0xHawre/RItual-nodes-/assets/131952165/aa8c8408-f17c-4cc9-8863-90ce92b66553">

make sure each time blocks go forword 
happy running  <3












