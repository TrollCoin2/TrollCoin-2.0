# **TrollCoin (TROLL) Version 2.1.0.0**

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

Build Instructions for Raspberry Pi 4B 
================================================

//March 18 2020
//Tested on 4B with 2gb RAM 

SDFormatter - erase micro SD card
Raspberry Pi Imager - https://www.raspberrypi.org/downloads/

format SD card and run Imager
Choose Ubunutu 18.04.4 32-bit server OS (others may work but this is stable)
then write and insert SD card 
make sure ethernet cord is in and power on pi

terminal:
//will load then ask for login/pw
//default is ubuntu/ubuntu

$sudo apt-get update
$sudo apt-get upgrade //if you get a lock error the OS might automatically be using packmanager
$sudo apt-get install xubuntu-desktop //or desktop enviroment of your choosing
$reboot

//can now use wifi
goto:
https://github.com/TrollCoin2/TrollCoin-2.0
click clone/download, download ZIP

$sudo unzip TrollCoin-2.0-master.zip -d [destination]

//Install dependencies via Terminal:

$ sudo apt-get install make libqt5webkit5-dev libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools qtcreator libprotobuf-dev protobuf-compiler build-essential libboost-dev libboost-all-dev libboost-system-dev libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev libssl1.0-dev libdb++-dev libstdc++6 libminiupnpc-dev libevent-dev libcurl4-openssl-dev git libpng-dev qrencode libqrencode-dev

//In terminal navigate to the TrollCoin-2.0 folder:
$qmake -qt=qt5 "USE_QRCODE=1" "USE_UPNP=1"
$make

//replace with updated lib
$sudo apt-get remove libssl1.0-dev
$sudo apt-get install libssl-dev

$cd [Trollcoin dir]
$./TrollCoin


//ready to rock and roll


Build Instructions for Raspberry Pi 3B(non B+) 
================================================

//Aug 30 2018

SDFormatter - erase micro SD card
(windows) Win32 Disk imager - ubuntu-mate-16.04.2-desktop-armhf version

write and insert SD card and power on pi


goto:
https://github.com/TrollCoin2/TrollCoin-2.0
click clone/download, download ZIP

terminal:
$sudo unzip TrollCoin-2.0-master.zip -d [destination]

$sudo apt-get update

//if firefox not working
$sudo apt-get install qupzilla

$sudo apt-get install make libqt5webkit5-dev libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools qtcreator libprotobuf-dev protobuf-compiler build-essential libboost-dev libboost-all-dev libboost-system-dev libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev libssl-dev libdb++-dev libstdc++6 libminiupnpc-dev libevent-dev libcurl4-openssl-dev git libpng-dev qrencode libqrencode-dev
//click yes

$cd /home/TrollCoin-2.0
$sudo qmake -qt=qt5 "USE_QRCODE=1" "USE_UPNP=1"
$sudo make


need to have swap usb for wallet not to crash dling blockchain

$sudo apt install gparted
$sudo gparted
//gui interface right click devices and create linux-swap
//click swapon (wont be permanent need to edit fstab)

download vim/nano/txt editor of choice
$sudo apt-get install vim
$sudo vim /etc/fstab
$/dev/[sda1]		swap	swap defaults	0	0          
//     maybe diff, 
//     can use UU also with command $blkid


$cd [Trollcoin dir]
$./TrollCoin
//wait approx 2 weeks for wallet to update at the time of writing


Build Instructions for Qt5 Linux Wallet (Ubuntu)
================================================
//Install dependencies via Terminal:

$ sudo apt-get install make libqt5webkit5-dev libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools qtcreator libprotobuf-dev protobuf-compiler build-essential libboost-dev libboost-all-dev libboost-system-dev libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev libssl-dev libdb++-dev libstdc++6 libminiupnpc-dev libevent-dev libcurl4-openssl-dev git libpng-dev qrencode libqrencode-dev

//In terminal navigate to the TrollCoin-2.0 folder:

$ cd /home/TrollCoin-2.0

//Then:

$ qmake -qt=qt5 "USE_QRCODE=1" "USE_UPNP=1"

//Then:

$ make

//This will compile and build the Qt Wallet which takes a little while, please be patient.

//When finished you will have a file called TrollCoin - Simply Double Click

//end of guide

Build Instructions for Qt5 Linux Wallet (Ubuntu) [MODERN] 
================================================
//tested 1/28/2019 on linux mint 19

//same as above except package "libssl-dev" causes a big NUM error. 

$sudo apt-get remove libssl-dev
//temporarily remove up to date lib

$sudo apt-get install libssl1.0-dev
//older out of date lib

$sudo make

$sudo apt-get remove libssl1.0-dev
$sudo apt-get install libssl-dev
//replace with updated lib and ready to rock and roll


Build Instructions for Terminal Based Linux Wallet (Ubuntu)
===========================================================
//Install dependencies via Terminal:

$ sudo apt-get install build-essential libboost-all-dev libssl-dev libcurl4-openssl-dev libminiupnpc-dev libdb++-dev libstdc++6 make 

//In terminal navigate to the TrollCoin-2.0 folder:

$ cd /home/TrollCoin-2.0/src/

//Enter into the terminal:

$ make -f makefile.unix USE_UPNP=1

//This will produce a file named trollcoind which is the command line instance of TrollCoin

//Now type:

$ strip trollcoind

//When finished you will have a file called trollcoind

//To run TrollCoin

$ ./trollcoind & 

//It will complain about having no trollcoin.conf file, we'll edit the one provided and move it into place

$ cd ..
$ nano trollcoin.conf

//Edit the Username and Password fields to anything you choose (but remember them) then save the file

$ mv trollcoin.conf /home/.trollcoin/
$ cd src/
$ ./trollcoind &

//The server will start. Here are a few commands, google for more.

$ ./trollcoind getinfo
$ ./trollcoind getmininginfo
$ ./trollcoind getnewaddresss

//end of guide
