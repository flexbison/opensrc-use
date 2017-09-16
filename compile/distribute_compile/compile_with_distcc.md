                                          # distcc use guide 
## install
  The first choose is to install by apt-get install. also be installed by source

## config

## cconfig server

   in /etc/rc.local file. add the fllowing code.

   distccd --daemon --user nobody --allow 192.168.0.0/24

   explain:24 mean mask first 3 segment addr. mea 255.255.255.0
           nobody is a use already exit in your linux system.

### config client

  in ~/.bashrc file, add the following code.

  DISTCC_HOST="localhost 192.168.0.2 192.168.0.3 192.168.0.254"
  DISTCC_VERBOSE=1
  DISTCC_LOG="/home/ditcc.log"
  export DISTCC_HOST PATH DISTCC_VERBOSE DISTCC_LOG

### use in real project

  CXX=/yourpath/ditcc/g++
  CC=/yourpath/ditcc/gcc
  cmake ..

  make -jXX

  explain: XX hit is cpu (core+2)*computer

### monitor compile
  distccmon-text 1

  explain: print distcc state each 1 min.

### work with ccache
  you can use ccache firstly. and then use distacc
