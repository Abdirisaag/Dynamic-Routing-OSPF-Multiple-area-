# Dynamic-Routing-OSPF-Multiple-area-
OSPF Multiple area
Assign IP address according to diagram 
==========================================
R1 
====
en 
conf t
hostname R1
int g0/1
ip add 192.168.10.1 255.255.255.0
no shut
int se0/0/0
ip add 203.0.113.1 255.255.255.0
no shut
end

R2
====
en
conf t
hostname R2
int g0/1
ipp add 192.168.20.1 255.255.255.0
no shut
int se0/0/0
ip add 203.0.113.2 255.255.255.0
no shut
int se0/0/1
ip add 203.0.114.1 255.255.255.0
no shut
end

R3
====
en
conf t
hostname R3
int se0/0/1
ip add 203.0.114.2 255.255.255.0
no shut
int g0/1
ip add 192.168.30.1 255.255.255.0
no shut
end

Verify Reacability between 192.168.10.0/24 and 192.168.20.0/24 
=================================
ping 192.168.20.2

Now verify Routing table R1,R2 and R3 
=======================================
Show ip route


Configure OSPF on R1,R2 and R3
=================================
R1
===
en
conf t
router ospf 1
net 192.168.10.0 0.0.0.255 area 1
net 203.0.113.0 0.0.0.255 area 1
end
copy running-config startup-config 

R2
===
en
conf t
router ospf 1
net 192.168.20.0 0.0.0.255 area 0
net 203.0.113.0 0.0.0.255. area 1
net 203.0.114.0 0.0.0.255 area 2
net 192.168.30.0 0.0.0.255 area 2
end
copy running-config startup-config 

R3
====
en
conf t
router ospf 1
net 192.168.30.0 0.0.0.255 area 2
net 203.0.114.0 0.0.0.255 area 2
end
copy running-config startup-config 

Verify routing table and OSPF neighbor
======================================
R1,R2 and R3
==============
Show ip route
show ip ospf neighbor
sh ip ospf datab
