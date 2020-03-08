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

# MP/M Networking

MP/M, where "M" meant "multiuser", was a Digital Research CP/M-derived network
server supporting up to four simultaneous client connections.

To emulate these connections, Z80Pack uses TCP/IP ports, which can be
configured either for emulated local CP/M clients or as telnet ports for
remote connection to the MP/M server. Which ports the server listens to and
which port a client connects on are specified in configuration files stored
in cpmsim/conf.

The example server configuration file specifies four ports as follows:

# Console	telnet flag	TCP/IP port
1		1		4000
2		1		4001
3		0		4002
4		0		4003

The example client configuration file specifies a port for the client, e.g.

# Console	host		TCP/IP port
1		localhost	4002

Z80Pack by default looks in conf/ for the config files, so careful
management of ports and config files is required to run multiple
simultaneous instances of clients and servers.

client_install and server_install place config files in conf/library, and
then drop links to them in conf/ in the same manner as disks/library images
are linked in disks/. Because the configuration files are only read at
start-up, later client and server instances can overwrite conf/ links
without consequence. 

By default, each server is assigned a range of four ports, two configured for
ttelnet and two for local connections, while clients are consigned in pairs
to each server. I.e., clients 1 and 2 connect to server 1, clients 3 and 4
to server 2, and so forth. You are, of course, free to manually adjust these
to suit your needs.

Note also that clients may connected to multiple local and remote servers. E.g.:

# Console	host		TCP/IP port
1		www.sample.org	3901
2               localhost       4006
