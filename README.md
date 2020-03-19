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
<p>
//March 18 2020<br />
//Tested on 4B with 2gb RAM 
</p>

<p>
SDFormatter - erase micro SD card<br />
Raspberry Pi Imager - https://www.raspberrypi.org/downloads/
</p>

<p>
format SD card and run Imager<br />
Choose Ubunutu 18.04.4 32-bit server OS (others may work but this is stable)<br />
then write and insert SD card <br />
make sure ethernet cord is in and power on pi<br />
</p>
  
<p>  
terminal: <br />
//will load then ask for login/pw <br />
//default is ubuntu/ubuntu <br />
</p>
  
<p>  
$sudo apt-get update <br />
$sudo apt-get upgrade //if you get a lock error the OS might automatically be using packmanager <br />
$sudo apt-get install xubuntu-desktop //or desktop enviroment of your choosing <br />
$reboot <br />
</p>

<p>
//can now use wifi<br />
goto:<br />
https://github.com/TrollCoin2/TrollCoin-2.0 click clone/download, download ZIP<br />
</p>

$sudo unzip TrollCoin-2.0-master.zip -d [destination]

//Install dependencies via Terminal:

<p>
$ sudo apt-get install make libqt5webkit5-dev libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools qtcreator libprotobuf-dev protobuf-compiler build-essential libboost-dev libboost-all-dev libboost-system-dev libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev libssl1.0-dev libdb++-dev libstdc++6 libminiupnpc-dev libevent-dev libcurl4-openssl-dev git libpng-dev qrencode libqrencode-dev
</p>
<p>
//In terminal navigate to the TrollCoin-2.0 folder:<br />
$qmake -qt=qt5 "USE_QRCODE=1" "USE_UPNP=1"<br /> 
$make <br />
</p>

<p>
//replace with updated lib <br />
$sudo apt-get remove libssl1.0-dev <br />
$sudo apt-get install libssl-dev 
</p>

<p>
$cd [Trollcoin dir]<br />
$./TrollCoin
</p>

//ready to rock and roll


Build Instructions for Raspberry Pi 3B(non B+) 
================================================

//Aug 30 2018

<p>
SDFormatter - erase micro SD card<br />
(windows) Win32 Disk imager - ubuntu-mate-16.04.2-desktop-armhf version<br />
</p>

write and insert SD card and power on pi

<p>
goto:<br />
https://github.com/TrollCoin2/TrollCoin-2.0<br />
click clone/download, download ZIP<br />
</p>

<p>
terminal:<br />
$sudo unzip TrollCoin-2.0-master.zip -d [destination]<br />
</p>
$sudo apt-get update

<p>
//if firefox not working<br />
$sudo apt-get install qupzilla<br />
</p>

$sudo apt-get install make libqt5webkit5-dev libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools qtcreator libprotobuf-dev protobuf-compiler build-essential libboost-dev libboost-all-dev libboost-system-dev libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev libssl-dev libdb++-dev libstdc++6 libminiupnpc-dev libevent-dev libcurl4-openssl-dev git libpng-dev qrencode libqrencode-dev

<p>
$cd /home/TrollCoin-2.0<br />
$sudo qmake -qt=qt5 "USE_QRCODE=1" "USE_UPNP=1"<br />
$sudo make<br />
</p>

need to have swap usb for wallet not to crash dling blockchain

<p>
$sudo apt install gparted<br />
$sudo gparted<br />
//gui interface right click devices and create linux-swap<br />
//click swapon (wont be permanent need to edit fstab)<br />
</p>

<p>
download vim/nano/txt editor of choice<br />
$sudo apt-get install vim<br />
$sudo vim /etc/fstab<br />
$/dev/[sda1]		swap	swap defaults	0	0<br />          
</p>
<p>
//     maybe diff, <br />
//     can use UU also with command $blkid<br />
</p>
<p>
$cd [Trollcoin dir]<br />
$./TrollCoin<br />
//wait approx 2 weeks for wallet to update at the time of writing<br />
</p>


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
<p>
$sudo apt-get remove libssl-dev<br />
//temporarily remove up to date lib<br />

$sudo apt-get install libssl1.0-dev<br />
//older out of date lib<br />

$sudo make<br />

$sudo apt-get remove libssl1.0-dev<br />
$sudo apt-get install libssl-dev<br />
//replace with updated lib and ready to rock and roll<br />
</p>

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
