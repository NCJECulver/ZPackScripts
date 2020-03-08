# ZPackScripts
  Various scripts for use with the [Z80Pack simulator](https://github.com/udo-munk/z80pack).

## Z80Pack_Install
   Automates the installation of Z80Pack and the many additional OSes available from the [Z80Pack website](https://www.autometer.de/unix4fun/z80pack/).

## client_install
   Automates setting up an emulated MP/M client system under Z80Pack.

## server_install
   Automates setting up an emulated MP/M server under Z80Pack.

## zpack_os
   Adds enhancements to the basic Z80Pack OS launch scripts.

# Z80Pack_Install
  When you run this script, a check will be performed to ensure your system has all the dependencies it needs to build Z80Pack, and then present you with a choice of installing the Z80Pack family of simulators, or additional operating systems, software or components from the Z80Pack website. 

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
