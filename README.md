# Simple-network
In this project, I create a simple network with a router, switch and 4 PCs and then configured IP address + DHCP so that each PC can ping to the other.
I have already congfigured these devices, but you can try do it by your-self.

I used router ISR 4321(R0), Switch 2960-24TT and 4 PC-PT.
Copper Straight-Through used to connect these devices.

Step:
- Put the copper at router, choose GigabitEthernet0/0/0 then move to switch and choose FastEthernet0/1.
- From switch, choose FastEthernet 0/2 then move the copper to PC0 and choose FastEthernet0.
- From switch, choose FastEthernet 0/3 then move the copper to PC1 and choose FastEthernet0.
- From switch, choose FastEthernet 0/4 then move the copper to PC2 and choose FastEthernet0.
- From switch, choose FastEthernet 0/5 then move the copper to PC3 and choose FastEthernet0.

Now we move to 'config' step:
In Router, we prompt respectively these commands:
- en
- conf t
- hostname R0
- interface GigabitEthernet0/0
- ip address 192.168.1.1 255.255.255.0 #apply ip address and subnet mask
- no shut
- exit

After that, turn DHCP on the router with these commands:
- ip dhcp pool LAN_POOL # create DHCP pool with the name LAN_POOL
- network 192.168.1.0 255.255.255.0 # Assigning IPs in the range 192.168.1.0/24 (from 192.168.1.2 to 192.168.1.254)
- default-router 192.168.1.1 # default router is R0
- exit

Now, run command 'show run' and you can see GigabitEthernet0/0 port with IP 192.168.1.1 and DHCP are enabled.
Next step is created DHCP IP for each PC.
In PC0, choose Desktop -> IP Configuration -> IPv4 Configuration -> choose DHCP, wait for a second and the IP address will be auto set up.
Do the same for the other PC.
Now I have IP in the order from PC0 - PC3: 192.168.1.5; 192.168.1.4; 192.168.1.3; 192.168.1.2 and ping from PC0 to other PCs. ==> All PCs received IPs by DHCP and successfully pinged each other.
