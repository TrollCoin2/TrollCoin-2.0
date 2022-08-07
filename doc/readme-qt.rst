TrollCoin-qt: Qt5 GUI for TrollCoin
===================================

Build instructions
===================

Debian
-------

First, make sure that the required packages for Qt5 development of your
distribution are installed, for Debian and Ubuntu these are:

::

    apt-get install qt5-default qt5-qmake qtbase5-dev-tools qttools5-dev-tools \
        build-essential libboost-dev libboost-system-dev \
        libboost-filesystem-dev libboost-program-options-dev libboost-thread-dev \
        libssl-dev libdb++-dev libminiupnpc-dev

then execute the following:

::

    qmake
    make

Alternatively, install Qt Creator and open the `trollcoin-qt.pro` file.

An executable named `trollcoin-qt` will be built.


Windows
--------

Windows build instructions to build a 64-bit binary. These are compiled natively on Windows,
not cross-compiled from Linux:

- Download and install `msys2`_ and `7zip`_.
- Open a mingw64 shell (C:/msys64/mingw64.exe) and cd into the trollcoin source directory
- Run

::

    pacman -Syy --noconfirm mingw-w64-x86_64-gcc make patch ruby python
    wget https://github.com/miurahr/aqtinstall/releases/download/v2.1.0/aqt.exe
    ./aqt install-tool --outputdir c:/Qt windows desktop tools_mingw qt.tools.win64_mingw810


Build Qt statically
^^^^^^^^^^^^^^^^^^^^^^

This allows to distribute a single .exe in the end, otherwise many Qt dlls need to be distributed alongside the .exe.
If this is not required, you can simply install the regular `Qt installer`_ and build with that.

::

    wget https://gist.githubusercontent.com/mrfaptastic/80e909c9a8237994471bce2d17657779/raw/62596d3986b6e655f260efb51a2a9e630cd24a20/qt-windows10-static-build.ps1
    patch < doc/qt-windows10-static-build.ps1.patch
    powershell -File qt-windows10-static-build.ps1 -NoPause -QtVersion 5.9.9 -QtSrcUrl https://download.qt.io/archive/qt/5.9/5.9.9/single/qt-everywhere-opensource-src-5.9.9.zip


Build dependencies
^^^^^^^^^^^^^^^^^^

Download the dependencies from the linked URLs, extract the archives and then run the
commands below in the respective extracted folder.

Build boost (version 1.55.0 https://sourceforge.net/projects/boost/files/boost/1.55.0):

::

    ./bootstrap.sh --with-toolset=mingw --prefix=C:/boost --with-libraries=system,filesystem,program_options,thread,chrono
    sed -i "s/mingw/gcc/g" project-config.jam
    ./b2 install

Build libdb (version 5.3.28 https://github.com/berkeleydb/libdb/releases/tag/v5.3.28):

::

    cd build_unix
    ../dist/configure --prefix=/c/libdb --enable-mingw --enable-cxx
    make -j
    make install

Build openssl (version 1.0.2u https://www.openssl.org/source/old/1.0.2/openssl-1.0.2u.tar.gz):

::

    mkdir -p /c/openssl
    ./Configure --prefix=/c/openssl --openssldir=/c/openssl no-shared --release mingw64
    make
    make install

Build miniupnpc (version 2.2.3 http://miniupnp.free.fr/files/download.php?file=miniupnpc-2.2.3.tar.gz):

::


    make -f Makefile.mingw
    mkdir -p /c/miniupnpc/{include/miniupnpc,lib}
    cp include/* /c/miniupnpc/include/miniupnpc
    cp *.a /c/miniupnpc/lib

Build qrencode (version 4.1.1 https://fukuchi.org/works/qrencode/qrencode-4.1.1.tar.gz):

::

    ./configure --prefix=/c/qrencode --disable-shared
    make -j
    make install


Build trollcoin
^^^^^^^^^^^^^^^

::

    export PATH=/c/Qt/Static/5.9.9/bin:$PATH
    qmake "USE_UPNP=1" "USE_QRCODE=1" "BOOST_LIB_PATH=C:\boost\lib" "BOOST_LIB_SUFFIX=-mgw121-mt-1_55" "BOOST_INCLUDE_PATH=C:\boost\include\boost-1_55" "OPENSSL_LIB_PATH=C:\openssl\lib" "OPENSSL_INCLUDE_PATH=C:\openssl\include" "BDB_LIB_PATH=C:\libdb\lib" "BDB_INCLUDE_PATH=C:\libdb\include" "MINIUPNPC_LIB_PATH=C:\miniupnpc\lib" "MINIUPNPC_INCLUDE_PATH=C:\miniupnpc\include" "QRENCODE_LIB_PATH=C:\qrencode\lib" "QRENCODE_INCLUDE_PATH=C:\qrencode\include"
    make


.. _`msys2`: https://www.msys2.org/
.. _`7zip`: https://www.7-zip.org/
.. _`Qt installer`: https://www.qt.io/download-thank-you?os=windows&hsLang=en


Mac OS X
--------

- Download and install the `Qt Mac OS X SDK`_. It is recommended to also install Apple's Xcode with UNIX tools.

- Download and install `MacPorts`_.

- Execute the following commands in a terminal to get the dependencies:

::

	sudo port selfupdate
	sudo port install boost db48 miniupnpc

- Open the .pro file in Qt Creator and build as normal (cmd-B)

.. _`Qt Mac OS X SDK`: http://qt-project.org/downloads
.. _`MacPorts`: http://www.macports.org/install.php


Build configuration options
============================

UPNnP port forwarding
---------------------

To use UPnP for port forwarding behind a NAT router (recommended, as more connections overall allow for a faster and more stable trollcoin experience), pass the following argument to qmake:

::

    qmake "USE_UPNP=1"

(in **Qt Creator**, you can find the setting for additional qmake arguments under "Projects" -> "Build Settings" -> "Build Steps", then click "Details" next to **qmake**)

This requires miniupnpc for UPnP port mapping.  It can be downloaded from
http://miniupnp.tuxfamily.org/files/.  UPnP support is not compiled in by default.

Set USE_UPNP to a different value to control this:

+------------+--------------------------------------------------------------------------+
| USE_UPNP=- | no UPnP support, miniupnpc not required;                                 |
+------------+--------------------------------------------------------------------------+
| USE_UPNP=0 | (the default) built with UPnP, support turned off by default at runtime; |
+------------+--------------------------------------------------------------------------+
| USE_UPNP=1 | build with UPnP support turned on by default at runtime.                 |
+------------+--------------------------------------------------------------------------+

Notification support for recent (k)ubuntu versions
---------------------------------------------------

To see desktop notifications on (k)ubuntu versions starting from 10.04, enable usage of the
FreeDesktop notification interface through DBUS using the following qmake option:

::

    qmake "USE_DBUS=1"

Generation of QR codes
-----------------------

libqrencode may be used to generate QRCode images for payment requests. 
It can be downloaded from http://fukuchi.org/works/qrencode/index.html.en, or installed via your package manager. Pass the USE_QRCODE 
flag to qmake to control this:

+--------------+--------------------------------------------------------------------------+
| USE_QRCODE=0 | (the default) No QRCode support - libarcode not required                 |
+--------------+--------------------------------------------------------------------------+
| USE_QRCODE=1 | QRCode support enabled                                                   |
+--------------+--------------------------------------------------------------------------+


Berkely DB version warning
==========================

A warning for people using the *static binary* version of TrollCoin on a Linux/UNIX-ish system (tl;dr: **Berkely DB databases are not forward compatible**).

The static binary version of TrollCoin is linked against libdb 5.0 (see also `this Debian issue`_).

Now the nasty thing is that databases from 5.X are not compatible with 4.X.

If the globally installed development package of Berkely DB installed on your system is 5.X, any source you
build yourself will be linked against that. The first time you run with a 5.X version the database will be upgraded,
and 4.X cannot open the new format. This means that you cannot go back to the old statically linked version without
significant hassle!

.. _`this Debian issue`: http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=621425

Ubuntu 11.10 warning
====================

Ubuntu 11.10 has a package called 'qt-at-spi' installed by default.  At the time of writing, having that package
installed causes trollcoin-qt to crash intermittently.  The issue has been reported as `launchpad bug 857790`_, but
isn't yet fixed.

Until the bug is fixed, you can remove the qt-at-spi package to work around the problem, though this will presumably
disable screen reader functionality for Qt apps:

::

    sudo apt-get remove qt-at-spi

.. _`launchpad bug 857790`: https://bugs.launchpad.net/ubuntu/+source/qt-at-spi/+bug/857790
