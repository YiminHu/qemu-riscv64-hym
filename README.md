#qemu-riscv64-hym
Using qemu to run a riscv-linux with helloworld and strace
###############################################################

###0.Get neccessary git repo and prequisite packgages
To begin with, you should clone everything into ./pub/git, 
suppose you are on the course server and now in the  
repo qemu-riscv64-hym:  
``` 
cd pub  
mkdir git  
cd git  
git clone --bare /pub/git/riscv-pk.git  
git clone --bare /pub/git/riscv-gnu-toolchain.git
git clone --bare /pub/git/riscv-linux.git  
git clone --bare /pub/git/riscv-qemu.git  
git clone --bare /home/RV64B/LL1300011764/riscv64/pub/git/strace.git
```
If you are on a machine that is able to access github:  
```
git clone --bare https://github.com/riscv/riscv-pk.git  
git clone --bare https://github.com/riscv/riscv-gnu-toolchain.git  
git clone --bare https://github.com/riscv/riscv-linux.git  
git clone --bare https://github.com/riscv/riscv-qemu.git  
git clone --bare https://github.com/strace/strace.git  
```
But in this cause, riscv-qemu.git need to update a submodule pixman,
so if you are not on the course server, you need to add:`@cd $(DIR_WORKING);git submodule update --init pixman` 
to the last line of qemu-new target in Makefile.  
To install prequiste:  
```  
sudo apt-get install gcc libc6-dev pkg-config bridge-utils uml-utilities zlib1g-dev libglib2.0-dev autoconf automake libtool libsdl1.2-dev  
```
###############################################################

###1.Decide whether to make toolchain

Before you make all the component, you should get riscv complier
ready, which means you should compile the riscv-gnu-toolchain.
But this task is both time consuming and memory consuming. So on
the course server, the pre compiled tools is in:  
``` 
/home/RV64B/LL1300011764/riscv/bin  
```
if you still want to make you own toolchain:  
```  
make toolchain  
```
Note that to make toolchain, it need to update a lot of submodules
so it will take a lot of time downloading.
###############################################################

###2.Make all components

To make everything ready, first set $PATH & $RISCV, to use default
value you can use:  
```  
export RISCV=/home/RV64B/LL1300011764/riscv/  
export PATH=$PATH:$RISCV/bin  
```
or you can modify the environment variable to set your own path.
Then you can start the building process, simply type: 
```  
make  
```
Hopefully,everything will be ready.

###############################################################
###3.Run riscv-linux on qemu

To run, type:  
```  
cd working  
./qemu-riscv64/bin/qemu-system-riscv64 -kernel ./riscv-pk/build/bbl -nographic  
```  
Now you get a riscv-linux with hello and strace in /bin.And you can
try to strace the hello program.
###############################################################
