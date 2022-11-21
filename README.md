## Zeeka Network

[Discord](https://discord.gg/eT96kE6V) | [Website](https://zeeka.io/) | [Github](https://github.com/zeeka-network)
| --- | --- | ---
#### Active version incentive Tetnet run 21.11.22 !
![image](https://user-images.githubusercontent.com/57448493/192145552-6eed7477-d72a-4089-bf94-172f4deec8ff.png)

Zeeka (ℤ) is a cryptocurrency that aims to create a lightweight and scalable blockchain with extensive use of zero-knowledge proof technology.

Zeeka offers a new concept called Zero Contracts. Zero contracts are the equivalent of smart contracts in some major blockchain systems such as Ethereum. These contracts will be expressed as mathematical constraints instead of virtual machine byte codes, such as the Ethereum virtual machine.

Zeeka will incorporate concepts previously used as privacy layer or L2 solutions in other chains into the core of the new blockchain, aiming to create a more scalable network with better privacy.

At this point, it is possible to help the project in-house. There are 3 forms to fill out:

1. Community member form (for moderators):https://docs.google.com/forms/d/e/1FAIpQLSdz129RVXCPLIipF2evu5HDblo5iXdVBtk-3RO6XzKYCAVGlQ/viewform

2. Contributions form:https://docs.google.com/forms/d/e/1FAIpQLSewVt8hRnRcufFOLCm9E9tNSeQ9FgWBjmygyIScA6_c5H7NPg/viewform

3. Testnet submission form:https://docs.google.com/forms/d/e/1FAIpQLSdZVJmcL5X83zDUdRIJxuWiSi8hvmocEM7Ut8E0m97-cmdgcQ/alreadyresponded

***
#### 1. Server Preparation
```
sudo apt update && sudo apt upgrade -y
sudo apt install wget jq git libssl-dev cmake -y
```
#### 2.Install Rust
```
. <(wget -qO- https://raw.githubusercontent.com/letsnode/Utils/main/installers/rust.sh)
```

#### Очистим сервер от старой версии.
```
systemctl stop zeekad zorod uzid
systemctl disable zeekad zorod uzid
rm -rf $HOME/.bazuka*
rm -rf $HOME/bazuka
rm -rf $HOME/zoro
rm -rf $HOME/uzi-miner
rm -rf $HOME/.zoro
rm /etc/systemd/system/zeekad.service
rm /etc/systemd/system/zorod.service 
rm /etc/systemd/system/uzid.service
systemctl daemon-reload
```
#### 3.Clone a repository with a node
```
git clone https://github.com/ziesha-network/bazuka
```
#### 4.Перейти в папку bazuka,компиляция и установка
```
cd bazuka
git pull origin master
cargo update
cargo install --path .
```

#### View software bazuka
```
/root/bazuka/target/release/bazuka -h
```

#### 5.Initialize a node
```
bazuka init --listen 0.0.0.0:8765 --db ~/.bazuka --network groth --external ВАШ-iP:8765 --bootstrap 65.108.193.133:8765 --mnemonic "Сид фраза кратна 6 словам"
```

#### 6.Create a service file
```
sudo tee <<EOF >/dev/null /etc/systemd/system/zeeka.service
[Unit]
Description=Zeeka node
After=network.target

[Service]
User=$USER
ExecStart=`RUST_LOG=info which bazuka` node start --discord-handle Ваш ник дискорда 
Restart=on-failure
RestartSec=3
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF
```
#### 7.Run the service
```
sudo systemctl daemon-reload
sudo systemctl enable zeeka
sudo systemctl restart zeeka
```
Add a command to view the log of a node in the system as a variable
```
. <(wget -qO- https://raw.githubusercontent.com/AlexM-dev/Utils/main/commands/insert_variable.sh) -n zeeka_log -v "sudo journalctl -fn 100 -u zeeka" -a
```
#### View logs
```
zeeka_log
```
![Screenshot_2](https://user-images.githubusercontent.com/57448493/203043786-13920c84-4b91-44f5-829e-d87fdac7d60f.png)

Copy the data to a safe place!!!

#### Delete a node 
```
systemctl stop  zeeka zoro uzi
systemctl disable zeeka zoro uzi
rm -rf /root/bazuka
rm -rf /root/.bazuka-debug
rm -rf /root/zoro
rm -rf /root/uzi
rm ~/.bazuka.yaml
```

#### Update version 
```
rm ~/.bazuka.yaml
sudo systemctl stop zeeka 
cd bazuka
git pull origin master
cargo install --path
```

#### Useful Commands
```
Useful commands:
bazuka deposit Deposit funds to a Zero-Contract

bazuka help Prints this message or the help of the given subcommand(s)

bazuka init Initialize node/wallet

bazuka node Run node

bazuka rsend Send funds through a regular-transaction

bazuka status Get status of a node

bazuka withdraw Withdraw funds from a Zero-Contract

bazuka zsend Send funds through a zero-transaction
```
