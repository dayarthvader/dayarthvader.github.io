---
layout: post
title: firewall-iptables-netfilter-overiew 
---

[firewall-iptables-netfilter-overview](https://github.com/dayarthvader/firewall-iptables-netfilter-overview)  
# Firewall.
A firewall a security system that monitors and controls the flow of network traffic, incoming and outgoing, based on a pre-defined set of security rules. Firewall typically stays as a barrier between a trusted internal network (Home of corporate LAN) and untrusted external network (internet).

# Netfilter.
A firewall function is realised in the linux using a subystem called as the netfilter. A software firewall to be more specific. It is the most trusted framework for building firewall solutions that are based on Linux operating system. Netfilter is a kernel component of the Linux with the following specific functionality.

1. Packet filtering -- Allow and deny packet entry or relaying of packets.
2. Network and Port address translation -- proxy/gateway/routing like functions.
3. Port forwarding -- a specific kind of routing, request forwarding on a selected port.
4. Packet alteration -- Intentional alteration of the bytes in the header of a IP packet, before or after routing decision.

# iptables.
iptables command is a command line interface(userspace tool) for accessing the netfilter functions of the linux kernel. With the help of the iptables command one can configure the netfilter( in the kernel space), for most of the practical purposes when referring to iptables, one means to configuring the netfilter subsystem. invocation of iptables/netfilter calls for root privileges.

#Netfilter chains.
Every packet is analysed/inspected to assertain whether the packet is allowed to be processed further or blocked. iptables organises its rules with the help of tables, in each of the tables, rules are further organised within specific chains. Rules are placed wihin a specific chain of a specific table.

Within a chain, every packet is considered for evaluation rule by rule from the top of the chain. If the matching condition is satisfied, the said target is executed. If no condition is matched, the default policy for the chain is applied, the possible policies being DROP, ACCEPT. DEFAULT being another option

## Available (Built-in) chains.
1. INPUT       - Filtering incoming packets (DROPping or ACCEPTing) when the host is the destination of the ip packet.
2. OUTPUT      - Filtering outgoing packets (DROPping or ACCEPTing) when the host is the source of the ip packet.
3. FORWARD     - Filtering routed packets when the host is not the destination of the ip packete.
4. PREROUTING  - Used for DNAT / Port forwarding when packet headers to be modified and forwarded further (proxy/gateway) 
5. POSTROUTING - Used for SNAT (MASQUERADE) 

The above chains can't be removed or renamed. The chains are always specified in bigger case while the filters are specified in small letters. User defined and custom chains are possible too. To be explored in the later notes.

## Available (Built-in) tables.
1. filter - is a default table. built-in chains INPUT,OUTPUT and FORWARD.
2. nat - specialised for SNAT/DNAT - built-in chains PREROUTING for DNAT, POSTROUTING for SNAT, OUTPUT locally generated packets.
3. mangle - specialised for packet alteration - alter header fields such as tos, ttl, built-in chains being PREROUTING,INPUT,FORWARD,OUTPUT,POSTROUTING.
4. raw - raw table is used to mark the packets for target NOTRACK so that the stateful connection tracking is not applied on the packets. Helps with performance optimisation. Built-in chains - PREROUTING and OUTPUT.

## Chain traversal
1. Incoming traffic is filtered on the INPUT chain of the filter table.
2. Outgoing traffic is filtered on the OUPPUT chaing of the filter table.
3. Routed traffic is filtered on the FORWARD chain of the filter table.
4. SNAT/MASQUERADE is performed on the POSTROUTING CHAIN of the nat table.
5. DNAT/Port forwarding is performed on the PREROUTING CHAIN of the nat table.
6. To modify valued from the packet's headers, add rules to the mangle table.
7. To skip the connection tracking add rules with NOTRACK target to the raw table.

## Other notes and commands
### Command options
1. -A - Append a rule to the end of the file
2. -I - Insert a rule in the selected chain on a specified position. (top of the chain if the position is not specified)
3. -L - List all the rules in the selected chain.
4. -F - Flush the selected chain, all chains are flushed if no chain is specified.
5. -Z - Zero the packet and byte counters in specified chain, all chains if none specified.
6. -N - Create a new user-defined chain.
7. -X - Delete the user defined chain specified in the command.
8. -P - Set the policy for built-in chain(INPUT, OUTPUT or FORWARD)
9. -D - delete one or more rules from the selected chain.
10. -R - Replace a rule in the specified chain.
11. -S - print all rules in the selected chain.

### List the rules
list all the all rules in the filter table
```
iptables -L
```   
list verbose version, number of packets etc ...
```
iptables -L -v
```
list numeric format and verbose
```
iptables -L -v -n
```
quite a few flags exist to specify matching conditions such as source address, destination address, protocols and protocol states etc ...

* -P option can be used in INPUT, OUTPUT, FORWARD chains
* Configuring netfilter using iptables is not persistant. The rules can not be retained accross reboots.
* To preserve the rules accross reboots, we could add commands to a script and run them during bootup.
* `iptables-save` can be used to pull currently configured rules and write them to a file for restore later.
* `iptables-restore` can be used to configure the rules stored in the file to the netfilter.
* `iptables-persistent` utility can be used in debian based systems to automatically load the firewall upon boot up.
* `/etc/iptables/rules.v4` will be used the utility to load the rules.
* `iptables-save > /etc/iptables/rules.v4` saves the current configuration to a file for reloading on the next boot.
* RHEL/Centos have other ways to achieve the same.
