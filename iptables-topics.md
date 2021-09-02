# Terminology:

**Tables:** Tables are files that join similar actions. A table consists of several chains.

**Chains:** A chain is a string of rules. When a packet is received, iptables finds the appropriate table, then runs it through the chain of rules until it finds a match. Within each iptables table, rules are further organized within separate chains. Chains map to netfilter hooks.

**Rules:** A rule is a statement that tells the system what to do with a packet. Rules can block one type of packet, or forward another type of packet. The outcome, where a packet is sent, is called a target.

**Targets:** A target is a decision of what to do with a packet. Typically, this is to accept it, drop it, or reject it (which sends an error back to the sender).

So, basically the structure is:

                                                           iptables -> Tables -> Chains -> Rules

# Basic operations:
## Listing rules (-L)
Additional options to extend the information:

**-v** — Displays verbose output, such as the number of packets and bytes each chain has seen, the number of packets and bytes each rule has matched, and which interfaces apply to a particular rule.

**-x** — Expands numbers into their exact values. On a busy system, the number of packets and bytes seen by a particular chain or rule may be abbreviated using K (thousands), M (millions), and G (billions) at the end of the number. This option forces the full number to be displayed.

**-n** — Displays IP addresses and port numbers in numeric format, rather than the default hostname and network service format.

**--line-numbers** — Lists rules in each chain next to their numeric order in the chain. This option is useful when attempting to delete the specific rule in a chain or to locate where to insert a rule within a chain.

**-t** — Specifies a table name.

### List a table (-t) content
iptables -t raw -D tetherctrl_raw_PREROUTING 1
### List with row numbers (––line–numbers)
sudo iptables –L ––line–numbers
### Add rules with comment 
$ sudo iptables -A INPUT -p tcp --dport 22 -m comment --comment "allow ssh"
### Remove rule with row number
iptables –D <Chain> <Number>
e.g. iptables –D INPUT 1 
  

# Features 
## Conection Tracking
Connection tracking means that the engine keeps a record of all currently open connections (stateful inspection).
With connection tracking, the engine can verify that the connection proceeds according to the protocol standards. Connection tracking is also required for changing addresses using NAT and enforcing some other connection-related settings. By default, connection tracking is on.

**Raw** table is responsible for setting rules for this functionality. This table allows you to configure exemptions from connection tracking. 
This table uses builtin chains like Prerouting and Output chains.

You can inspect and restrict connections to services based on their connection state. A module within iptables uses a method called connection tracking to store information about incoming connections. You can allow or deny access based on the following connection states:
  
NEW — A packet requesting a new connection, such as an HTTP request.
  
ESTABLISHED — A packet that is part of an existing connection.
  
RELATED — A packet that is requesting a new connection but is part of an existing connection. For example, FTP uses port 21 to establish a connection, but data is transferred on a different port (typically port 20).
  
INVALID — A packet that is not part of any connections in the connection tracking table.
  
You can use the stateful functionality of iptables connection tracking with any network protocol, even if the protocol itself is stateless (such as UDP). The following example shows a rule that uses connection tracking to forward only the packets that are associated with an established connection:
  

**Refs:**
* https://phoenixnap.com/kb/iptables-tutorial-linux-firewall
  https://www.thegeekstuff.com/2011/01/iptables-fundamentals/
* https://www.digitalocean.com/community/tutorials/a-deep-dive-into-iptables-and-netfilter-architecture
* https://home.regit.org/netfilter-en/secure-use-of-helpers/
* http://help.stonesoft.com/onlinehelp/StoneGate/SMC/6.1.3/GUID-0CD08BDC-EDE6-43F1-8F72-DACADB0C5BAB.html
* https://iximiuz.com/en/posts/laymans-iptables-101/  
