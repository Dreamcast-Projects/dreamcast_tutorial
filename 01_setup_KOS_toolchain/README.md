# How to compile the KOS toolchain
*The following has been tested under Linux Mint 18 on 9/9/2018*

## 01_setup_KOS_toolchain

First, navigate toward the folder `01_setup_KOS_toolchain`.
In order to execute the script, you'll neet to set the execute flag on `kos_setup_script.sh`.

In a terminal, type `chmod +x kos_setup_script.sh` then run it using `./kos_setup_script.sh`

This script will take a long time to complete (10~ mins on Intel i3 6100) as it is downloading a bunch of dependencies and installing them.

### Known Issues

You might have some problem with `make_banner.sh`. If you do, delete the content of both `make_banner.sh` and `banner.h` and type run the script again using `./kos_setup_script.sh`


### Compiling done.

When KOS is fully compiled, it should open a web browser and print this message in the terminal :

` Welcome to KOS! Please check out the example in /opt/toolchains/dc/kos/examples/dreamcast/kgl/nehe/nehe02 to get started. After editing main.c, type "make" to create an ELF executable. Run it using an emulator.
KOS documentation is at http://gamedev.allusion.net/docs/kos-current. When you start a new shell, please type -source /opt/toolchains/dc/kos/environ.sh- in order to set the environment variables.
`
### Source environ.sh

In order for your toolchain to work properly, you'll need to source the `environ.sh` file. If you want to source it automatically, you can edit your `.bashrc` file using your favorite file editor and add
`source /opt/toolchains/dc/kos/environ.sh` at the end of the file.

Otherwise, just make sure you run `source /opt/toolchains/dc/kos/environ.sh` in the terminal where you'll be compiling your Dreamcast programs.

You can test that your environ file is source by running `echo $KOS_BASE` and getting your KOS path in the terminal. You can also move to the KOS folder by typing `cd $KOS_BASE`.

### Compile an example!
Let's try to compile the Hello World exemple.

`cd $KOS_BASE/examples/dreamcast/hello` and run `make`

You should get something like this :

`rm -f hello.elf romdisk.*
kos-cc  -c hello.c -o hello.o
/opt/toolchains/dc/kos/utils/genromfs/genromfs -f romdisk.img -d romdisk -v -x .svn
0    rom 5b9594b5         [0xffffffff, 0xffffffff] 37777777777, sz     0, at 0x0     
1    .                    [0x801     , 0x381647  ] 0040755, sz     0, at 0x20    
1    ..                   [0x801     , 0x38163b  ] 0040755, sz     0, at 0x40     [link to 0x20    ]
1    .keepme              [0x801     , 0x38164f  ] 0100644, sz     0, at 0x60    
/opt/toolchains/dc/kos/utils/bin2o/bin2o romdisk.img romdisk romdisk.o
kos-cc -o hello.elf hello.o romdisk.o
`

Bravo! You compiled your first Dreamcast program.
