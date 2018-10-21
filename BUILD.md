We are building xayagamelib with MSYS2 under mingw64 enviroiment with all tools already installed. Some dependecies can be download with pacman
directly, some are need to be builded like:

argtabel2
cmake . -G"MSYS Makefiles" -DCMAKE_INSTALL_PREFIX=$MINGW_PREFIX
make
install

json-rpc-cpp
cmake . -G"MSYS Makefiles" -DCMAKE_INSTALL_PREFIX=$MINGW_PREFIX -DREDIS_SERVER=NO -DREDIS_CLIENT=NO  -DCOMPILE_STUBGEN=NO -DCOMPILE_EXAMPLES=NO -DCOMPILE_TESTS=NO -DBUILD_STATIC_LIBS=YES -DHUNTER_ENABLED=YES
make
install

glog
./autogen.sh
cmake . -G"MSYS Makefiles" -DCMAKE_INSTALL_PREFIX=$MINGW_PREFIX
make
install

manually copy file 'libglog.pc' into \msys64\mingw64\lib\pkgconfig

googletest
cmake . -G"MSYS Makefiles" -DCMAKE_INSTALL_PREFIX=$MINGW_PREFIX
make
install

THEN, we go for libxayagame:

libxayagame
as we compiled json-rpc-cpp without stubgen, we need to manually copy files into rpc-stub generated elsewhere
also remove AX_CHECK_COMPILE_FLAG([-Werror], [CXXFLAGS+=" -Werror"]) flash from configure.ac for now

./configure
make
make install
