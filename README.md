<h1>Listcoin</h1>

Ports:<br>
P2P:51738<br>
RPC:51737<br>
Test P2P:51998<br>
Test RPC:51997<br>

Requires addnode=x.x.x.x in listcoind.conf to connect nodes and setup network.<br>

===================================================

<h1>Сборка Ubuntu</h1>

Зависимости:<br>
sudo apt-get install build-essential libtool autotools-dev autoconf pkg-config libssl-dev libboost-all-dev libdb5.3++-dev<br> libminiupnpc-dev<br>

LevelDB:<br>
cd src/leveldb<br>
make -f Makefile libleveldb.a libmemenv.a<br>


Сборка всего:<br>
cd src/<br>
make -f makefile.unix<br>


=============================================================

<h1>How to build for Windows:</h1>

Качаем сразу mingw64 с gcc 4.9, perl<br>

=================================================
сборка boost через консоль Windows<br>

cd C:\deps\boost_1_57_0\ <br>
bootstrap.bat mingw<br>
b2 --build-type=complete --with-chrono --with-filesystem --with-program_options --with-system --with-thread toolset=gcc<br> variant=release link=static threading=multi runtime-link=static stage<br>

========================================

сборка leveldb через msys.bat<br>

cd /C/bitcoin-0.8.6/src/leveldb<br>
TARGET_OS=NATIVE_WINDOWS make libleveldb.a libmemenv.a<br>

==================================================
сборка upnp через консоль Windows<br>

http://miniupnp.free.fr/files/download.php?file=miniupnpc-1.9.20141128.tar.gz<br>

cd C:\deps\miniupnpc<br>


mingw32-make -f Makefile.mingw init upnpc-static<br>

=========================================

сборка openssl через msys.bat<br>

perl Configure mingw64 no-shared no-asm<br>
make depend<br>
make<br>

=============================================

сборка libz через msys.bat<br>


tar xvfz zlib-1.2.8.tar.gz<br>
cd zlib-1.2.8<br>
make -f win32/Makefile.gcc<br>



===============================================================

сборка Berkeley DB 4.8.30 через msys.bat<br>

cd /c/develop/deps<br>
tar xvzf db-4.8.30.NC.tar.gz<br>
cd db-4.8.30.NC/build_unix<br>
../dist/configure --enable-mingw --enable-cxx --disable-shared --disable-replication<br>

Исправляем строку 113 в db.h на<br>
typedef uintmax_t db_threadid_t;<br>
или<br>
typedef u_int32_t db_threadid_t;<br>


make<br>

=============================

Сборка всего<br>

DOS prompt:<br>
cd \shadowcoin\src<br>
mingw32-make -f makefile.mingw clean<br>

msys.bat:<br>
cd /shadowcoin/src/leveldb<br>
TARGET_OS=NATIVE_WINDOWS make libleveldb.a libmemenv.a<br>

DOS prompt:<br>
mingw32-make -f makefile.mingw<br>
strip shadowcoind.exe<br>

=============================================================
