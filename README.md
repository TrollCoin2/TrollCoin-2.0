# **TrollCoin (TROLL) Version 2.1.1.0**

TrollCoin Integration/Staging Tree
================================
![TROLL logo](https://avatars2.githubusercontent.com/u/16044831?v=3&u=c30f9a963a650436d286920035513bc94828d560&s=140)

**Copyright (c) 2015 The TrollCoin Developers**

#### What is TrollCoin?
----------------
* Algorithm: Scrypt
* Coin Suffix: TROLL
* PoW Period: 7,777,777 Blocks
* PoW Target Spacing: 60 Seconds
* PoW Difficulty Retarget: 10 Blocks
* PoW Reward per Block: 125 TROLL
* Full Confirmation: 10 Blocks
* Maturity: 77 Blocks
* PoS Target Spacing: 64 Seconds
* PoS Difficulty Retarget: 10 Blocks
* PoS Reward: 7 TROLL Static PoS Reward
* Minimum Confirmations for Stake: 777 Blocks
* PoS Min: 1 Hour
* PoS Max: Unlimited
* Total Coins: 900,000,000 TROLL
* Block Size: 7MB (7X Bitcoin Core)


TrollCoin is a digital currency that enables instant payments to anyone, anywhere in the world. TrollCoin uses peer-to-peer technology over ClearNet to operate with no central authority (centralisation): managing transactions and issuing currency (TROLL) are carried out collectively by the TrollCoin network. TrollCoin is the name of open source software which enables the use of the currency TROLL.



**MainNet Parameters**
P2P Port = 15000
RPC Port = 17000


**TestNet Parameters**
P2P Port = 25000
RPC Port = 27000



Build Instructions for Qt5 Linux Wallet (Ubuntu)
================================================
//Install dependencies via Terminal:

$ ```
sudo apt-get install make libqt5webkit5-dev libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools qtcreator libprotobuf-dev protobuf-compiler build-essential libboost-dev libboost-all-dev libboost-system-dev libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev libssl-dev libdb++-dev libstdc++6 libminiupnpc-dev libevent-dev libcurl4-openssl-dev git libpng-dev qrencode libqrencode-dev
```

//In terminal navigate to the TrollCoin-2.0 folder:


```
cd /home/TrollCoin-2.0
```

//Then:


```
qmake -qt=qt5 "USE_QRCODE=1" "USE_UPNP=1"
```

//Then:


```
make
```
//This will compile and build the Qt Wallet which takes a little while, please be patient.

//When finished you will have a file called TrollCoin - Simply Double Click

//end of guide



Build Instructions for Terminal Based Linux Wallet (Ubuntu)
===========================================================
//Install dependencies via Terminal:


```
sudo apt-get install build-essential libboost-all-dev libssl-dev libcurl4-openssl-dev libminiupnpc-dev libdb++-dev libstdc++6 make
```

//In terminal navigate to the TrollCoin-2.0 folder:


```
cd /home/TrollCoin-2.0/src/
```

//Enter into the terminal:

 
```
make -f makefile.unix USE_UPNP=1
```

//This will produce a file named trollcoind which is the command line instance of TrollCoin

//Now type:


```
strip trollcoind
```

//When finished you will have a file called trollcoind

//To run TrollCoin


```
./trollcoind &
```

//It will complain about having no trollcoin.conf file, we'll edit the one provided and move it into place


```
cd ..
nano trollcoin.conf
```

//Edit the Username and Password fields to anything you choose (but remember them) then save the file

 
```
mv trollcoin.conf /home/.trollcoin/
cd src/
./trollcoind &
```

//The server will start. Here are a few commands, google for more.

```
./trollcoind getinfo
./trollcoind getmininginfo
./trollcoind getnewaddresss
```
//end of guide
