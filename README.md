My-codes-about-Contiki
======================

The whole Contiki-OS is too big and not necessary to be included here. I followed all instructions at http://www.contiki-os.org/start.html to install and configure it.

The two files included are originally in:
    contiki/core/net/rpl/rpl-icmp6.c (for sinkhole attack) 
    contiki/core/net/uip6.c (for selective-forwarding attack)
Replacing corresponding file makes mote’s code malicious. The example codes I used to simulate are:
    contiki/examples/ipv6/rpl-boarder-router/boarder-router.c 
    contiki/examples/ipv6/sky-websense/sky-websense.c

Steps to simulate:

1. Open Contiki and Cooja, create new simulations
2. Add a mote, the type is Sky: open the ‘boarder-router.c’, compile it and create the mote
3. Set the mote to server mode, open tunslip6 to complete configuration by creating a new terminal and using the following commands:
    cd /home/user/contiki/examples/ipv6/rpl-border-router
    make connect-router-cooja TARGET=sky
4. Add several Sky motes: open ‘sky-websense.c’, compile it and create motes.
5. Replace corresponding files to the attack you want to demonstrate
6. Add a malicious Sky mote: same as step #4.
7. Drag motes to proper positions, some setting in ‘View’ toolbar  can be modified to see radio environment, data path and mote type, etc.
8. Start simulation, you can see blue arrows representing packages.
9. There will be few packets after first 30s, the setting up phase. You can use ‘ping6 aaaa::212:740?:?:?0?’ command in a new terminal to create data flows (? represents number on the mote, e.g., mote #1 has an ipv6 address aaaa::212:7401:1:101). You can also visit web servers in the motes by entering URL like http://[aaaa::212:7402:2:202]  (represents web server in mote #2) to create one-time data flow.
