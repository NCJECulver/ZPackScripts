# ZPackScripts
Various scripts for use with the Z80Pack simulator

# Z80Pack_Install
A script to automate the installation of Z80Pack and the many additional OSes available from the Z80Pack website.

# client_install
A script to automate setting up an emulated MP/M client system under Z80Pack.

# server_install
A script to automate setting up an emulated MP/M server under Z80Pack.

# zpack_os
Adds enhancements to the basic Z80Pack OS launch scripts.

# MP/M and CP/Net Networking

MP/M is a multi-user version of CP/M, while CP/Net is Digital Research's
networking technology. Z80Pack uses TCP ports to facilitate network
connections of CP/M-CP/Net clients to MP/M servers. 

client_install and server_install scripts automate the setup and
port configuration of clients and servers under Z80Pack. Running the scripts
repeatedly will install additional clients and servers, which are by default
configured as follows:

cpm2-client1     mpm-server1 port 4002
cpm2-client2     mpm-server1 port 4003
cpm2-client3     mpm-server2 port 4006
cpm2-client4     mpm-server2 port 4007

and so forth.

Clients may connect to up to four servers; simply manually edit the client's
configuration file in conf/library.

Once you have at least one server and client installed, start the network as
follows:

Start the server:      ./mpm-server1
Load MP/M:             MPMLDR
Star the client:       ./cpm2-client1
Load CP/Net:           CPNETLDR
Map a drive:           NETWORK C:=B:
Unmap a drive:         LOCAL C:
Check network status   CPNETSTS
