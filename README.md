# ZPackScripts
  Various scripts for use with the [Z80Pack simulator](https://github.com/udo-munk/z80pack).

## Z80Pack_Install
   Automates the installation of Z80Pack and the many additional OSes available from
the [Z80Pack website](https://www.autometer.de/unix4fun/z80pack/).

## client_install
   Automates setting up an emulated MP/M client system under Z80Pack.

## server_install
   Automates setting up an emulated MP/M server under Z80Pack.

## zpack_os
   Adds enhancements to the basic Z80Pack OS launch scripts.

# Z80Pack_Install
  When you run this script, you will be presented with two options: install
  Z80Pack, or install additional software and components from the Z80Pack website.
  The first option will verify that you have all necessary dependencies
  installed, then install the full suite of Z80Pack simulators. The second
  will allow you to select from the many additional operating systems and
  other software and components available from the [Z80Pack
  website](https://www.autometer.de/unix4fun/z80pack/).

# ZPack_OS
  Z80Pack uses basic launch scripts to set links to disk images and then
  start the simulator. The *zpack_os* script adds numerous enhancements to
  the start-up process, including use of TMUX sessions if TMUX is installed.
  To take advantage of *zpack_os* the *Z80Pack_Install* script automatically
  updates the stock launch scripts in a minimal way that gracefully degrades
  back to the original script functionality if *zpack_os* isn't found.

  ## Example:
   Here is the original cpm2 launch script:

    #!/bin/sh

    # mount disks
    rm -f disks/drive[abi].dsk
    ln disks/library/cpm2-1.dsk disks/drivea.dsk
    ln disks/library/cpm2-2.dsk disks/driveb.dsk

    ./cpmsim $*

   And here is the updated script:

    #!/bin/bash

    # mount disks
    rm -f disks/drive[abi].dsk
    ln disks/library/cpm2-1.dsk disks/drivea.dsk
    ln disks/library/cpm2-2.dsk disks/driveb.dsk

    simcmd="./cpmsim $*"
    [ -f ./zpack_os ] && . ./zpack_os
    $simcmd

# MP/M and CP/Net Networking

CP/Net is Digital Research's networking technology; MP/M is Multiuser CP/M, which is capable of acting as a server in a CP/Net network. Z80Pack uses TCP ports to facilitate connections between vietualized CP/M clients and
an MP/M server.

_client_install_ and _server_install_ scripts automate setup and port configuration of clients and servers under Z80Pack. Running the scripts repeatedly will install additional clients and servers, which are by default configured as follows:

  Client |   Server  | Port
------------ | ------------ | ----
``cpm2-client1`` | ``mpm-server1`` | ``4002``
``cpm2-client2`` | ``mpm-server1`` | ``4003``
``cpm2-client3`` | ``mpm-server2`` | ``4006``
``cpm2-client4`` | ``mpm-server2`` | ``4007``

and so forth.

Clients may connect to up to four servers; simply manually edit the client's configuration file in conf/library.

Once you have at least one server and client installed, start the network as follows:

* Start the server
  * `./mpm-server1`
  * `MPMLDR`
* Start the client
  * `./cpm2-client1`
  * `CPNETLDR`
* Map / unmap drives
  * `NETWORK C:=B:`
  * `LOCAL C:`
* Check network status
  * `CPNETSTS`
