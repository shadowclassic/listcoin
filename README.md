Listcoin

Built using MinGW and Windows. Changed makefile.mingw.

Requires addnode=x.x.x.x in listcoind.conf to connect nodes and setup network.

Ports:
P2P:51738
RPC:51737
Test P2P:51998
Test RPC:51997

How to build for Windows:


Качаем сразу mingw64 с gcc 4.9, perl

=================================================
сборка boost через консоль Windows

cd C:\deps\boost_1_57_0\
bootstrap.bat mingw
b2 --build-type=complete --with-chrono --with-filesystem --with-program_options --with-system --with-thread toolset=gcc variant=release link=static threading=multi runtime-link=static stage

========================================

сборка leveldb через msys.bat

cd /C/bitcoin-0.8.6/src/leveldb
TARGET_OS=NATIVE_WINDOWS make libleveldb.a libmemenv.a

==================================================
сборка upnp через консоль Windows

http://miniupnp.free.fr/files/download.php?file=miniupnpc-1.9.20141128.tar.gz

cd C:\deps\miniupnpc


mingw32-make -f Makefile.mingw init upnpc-static

=========================================

сборка openssl через msys.bat

perl Configure mingw64 no-shared no-asm
make depend
make

=============================================

сборка libz через msys.bat


tar xvfz zlib-1.2.8.tar.gz
cd zlib-1.2.8
make -f win32/Makefile.gcc



===============================================================

сборка Berkeley DB 4.8.30 через msys.bat

cd /c/develop/deps
tar xvzf db-4.8.30.NC.tar.gz
cd db-4.8.30.NC/build_unix
../dist/configure --enable-mingw --enable-cxx --disable-shared --disable-replication

Исправляем строку 113 в db.h на
typedef uintmax_t db_threadid_t;
или
typedef u_int32_t db_threadid_t;


make

=============================

Сборка всего

DOS prompt:
cd \shadowcoin\src
mingw32-make -f makefile.mingw clean

msys.bat:
cd /shadowcoin/src/leveldb
TARGET_OS=NATIVE_WINDOWS make libleveldb.a libmemenv.a

DOS prompt:
mingw32-make -f makefile.mingw
strip shadowcoind.exe

=============================================================