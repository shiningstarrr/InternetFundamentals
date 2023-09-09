# Bullet Points
⦾⦿➼⚫⚪➡•○✯✪✫🌟🎄°
⌛⚡➟⮞➤➣➢✔
# Resources link:
🎄 https://www.practicalnetworking.net/index/networking-fundamentals-how-data-moves-through-the-internet/
🎄 https://www.youtube.com/playlist?list=PLIFyRwBY_4bRLmKfP1KnZA6rZbRHtxmXi

# Network devices
- Host
    ✫ Host is any device which send or receive traffic
    ✫ Clients initiat requests, Servers respond.
    ✫ Hosts on a network share the same IP address space
- IP Address
    ✫ IP Address is the identity of the host.
- Network
    ✫ Network is what transports traffic between Hosts
    ✫ Grouping of hosts which require similar connectivity
- Repeater
    ✫ Data crossing a wire decays as it travels
    ✫ Repeaters regenerate signals which allow communications across greater distances.
- Hub: 
    ✫ Hubs are multi-port Repeaters 
    ✫ Facilitates scaling communication between additional hosts
    ✫ Everyone receives everyone else's data
- Bridge
    ✫ Bridges sit between Hub-connected hosts
    ✫ Bridges only have two ports
    ✫ Bridges learn which hosts are on each side
- Switch
    ✫ Swiches facilitate communication within a network
    ✫ Switches are a combination of Hubs and Bridges
    ✫ Multiple ports
    ✫ Learn which hosts are on each port
- Router
    ✫ Router facilitate communication between networks
    ✫ Provide traffic control points(security, filtering, redirecting)
    ✫ Routers learn(have IP address) which networks they are attached to, and they ar stored in a routing table.
- Routing is the process of moving data between network, switching is the process of moving data within networks.
- Subnet Mask: segregates an IP address into network bits that identify the network and host bits. Ex: 2555.255.255.0 or /24
- DNS: A protocol which converts a Domain Name into an IP address. Example: www.PracticalNetworking.net -> 192.249.124.38
# OSI Model
- OSI Reference Model: 
    layer 1 - Pysical - Transporting Bits
        ° Computer data exists in the form of Bits (1's and 0's)
        ° Something has to transport those bits between hosts
        ° L1 technologies: Cables, Wifi, Repeater
    layer 2 - Data Link - Hop to Hop
        ° Interacts with the Wire: i.e.Network Interface Cards, Wifi access cards.
        ° Addressing Scheme - MAC addresses: 48 bits, represented as 12 hex digits.
        ° L2 technologies: NICs, Switches
        ° Often communication between hosts require multiple hops.
    layer 3 - Network - End to End
        ° Addressing Scheme - IP adresses: 32 bits
        ° L3 technologies: Routers, Hosts
        ° ARP: Address Resolution Protocol: links a L3 address to a L2 address.
    layer 4 - Transport - Service to Service
        ° Distinguish data streams
        ° Addressing Scheme - Ports: 0-65535 - TCP (favors reliability), 0-65535 - UDP (favors efficiency)
        ° Servers listen for requests to pre-defined Ports
        ° Clients select random Port for each connection: Response traffic will arrive on this port. For all connections, always a source port and destination port involved.
        ° About Port number: https://www.techtarget.com/searchnetworking/definition/port-number
    layer 5 - Session, layer 6 - Presentation, layer 7 - Application
        ° Other Networking Models combine these into one layer - Application
- Purpose of Networking: Allow two hosts to share data with one another.

# Everything Hosts do to speak on the internet
- Scenario 1: Hosts connected directly to each other(on the same network):
    1. Both hosts have a NIC, and therefore a MAC address
    2. Both hosts are configured with an IP address and a Subnet Mask
    3. Host A has some Data to send to Host B
    4. Host A knows the IP address of Host B, so Host A can create the L3 header to attach to the Data
    5. Host A does not know Host B's MAC address: Host A must use Address Resolution Protocol(ARP)
        ➢ ARP Request asks for the MAC address associated with target IP
            a. ARP Request includes sender's MAC address
            b. ARP Request is a broadcast-sent to everyone on the network: destination MAC address: ffff.ffff.ffff, and reserved MAC address to send a packet to everyone on the local network
        ➢ ARP IP/MAC Mappings are stored in an ARP Cache
        ➢ Host B responds by sending an ARP Response(include B's MAC and IP address)
        ➢ Host A populates it's ARP cache with Host B's IP/MAC mapping
    6. Host A uses ARP to resolve target's MAC address, and creates L2 header
    7. Data is sent to Host B (Data->L3->L2)
        ➢ L2 header is discarded
        ➢ L3 header is discarded
        ➢ Data is processed by Application
- Scenario 2: Host connected through a Router(in a foreign network):
    1. Host A, Host C, and the Router have MAC and IP addresses
    2. Host A has some data to send to Host C
        ➢ Host A knows Host C's IP address which provided by the User or the Application
        ➢ Host A knows Host C's IP address is on a foreign network
    3. Host A creates a L3 header: Layer 3 - end to end
    4. Host A needs to create a L2 header: Layer 2- hop to hop
    5. Host A uses ARP to resolve the MAC address of the Router's IP
        ➢ Router IP address is configured as the Default Gateway
    6. Host A creats L2 header: layer 2 and Data is sent to the Router
        ➢ L2 header is discarded
        ➢ Router takes over from this point
        ➢ Host A's job is done
    7. ARP mapping can be used for any host in foreign networks
    8. Host A's first step when sending data is always the same: determine if target IP is on local or foreign network
        ➢ foreign - ARP for Default Gateway IP
        ➢ Local - ARP for Target IP

# Everything Switches do to facilitate communication
- Switching is the process of moving data within network, and devices communicating through a switch belong to the same IP network.
- Switches are L2 devices - they only use L2 header to make decisions
- Switches use and maintain MAC Address Table: Mapping of Switch Ports to MAC address
- Switches perform three actions: 
    ➢ Learn: Update MAC Address Table with mapping of switch ports to Source MAC
    ➢ Flood: Duplicate and send frame out all swtich ports (except receiving port)
    ➢ Forward: Use MAC Address Table to deliver Frame to appropriate switch port
- Process would be identical if Host D was a Router connected to the internet
- Traffic going through the switch
    ➢ Switch has a MAC address and is configured with an IP address
    ➢ Switch essentially acts as a host in the network
- Unicast Frame vs Broadcast Frame:
    ➢ Unicast Frame - destination MAC address is a host: Switch will flood only if MAC address in not in the table
    ➢ Broadcast Frame - destination MAC address of FFFF.FFFF.FFFF: always Flooded
- VLANs - Virtual Local Area Networks
    ➢ Divides Switch Ports into isolated groups
    ➢ Divides Switches into multiple "mini-switches"
    ➢ Switches do all three actions within each VLAN
- Multiple Switches:
    ➢ Switches maintain independent MAC address Tables
    ➢ Switches perform switch actions indepently

# Everything Routers do to facilitate communication
- RFC: Internet Protocol
- Routers are connected to a network and have an IP address and a MAC address.
- Routers forward packets not destined to themselves.
- Routers maintain a map of all the Networks they know about
    ➢ Routing Table can be populated via three methods:
        1. Directly Connected - Routes for the Networks which are attached
        2. Static Routes - Routes manuelly provided by an Administrator
        3. Dynamic Routes - Routes learned automatically from other routers
- Routers also have ARP Table - mapping of L3 to L2 address
    ➢ Everything with an IP address has an ARP Table
    ➢ Start Empty - populated as needed with network traffic
- Complete process of sending data between Host A and Host C:
    1. Host A has data to send to Host C, and constructs the L3 header.
    2. Host A knows packet must be sent to Default Gateway(R1)
    3. Host A cannot construct L2 header since no ARP entry for Gateway's IP address(R1)
    4. Host A sends ARP Request for 10.0.44.1
    5. R1 populates its ARP Table with entry for 10.0.44.9
    6. R1 sends ARP Response
    7. Host populates its ARP Table with entry for 10.0.44.1
    8. Host A constructs L2 header. Host A send packet to R1.
    9. Router1 receives packet. R1 discards L2 header.
    10. R1 look up Destination IP in Routing Table
        ➢ Packet's next hop is to 10.0.55.2
    11. R1 cannot construct L2 header
    12. R1 sends ARP Request for 10.0.55.2
    13. R2 populates its ARP Table with entry for 10.0.55.1
    14. R2 sends ARP Response. R1 populates its ARP Table with entry for 10.0.55.2
    15. R1 constructs L2 header. R1 sends packet to R2
    16. R2 receives packet. R2 discards L2 header. R2 looks up Destination in Routing Table and find the final hop.
    17. R2 cannot construct L2 header since No ARP entry for 10.0.66.7. R2 sends ARP Request for 10.0.66.7.
    18. Host C populates its ARP Table with entry for 10.0.66.7. Host C sends ARP Response. R2 populates its ARP Table with entry for 10.0.66.7
    19. Host C receives packet. Host C discards L2 header. Host C discards L3 header. Host C processes data.

# Network Protocols - ARP, FTP, SMTP, HTTP, SSL, TSL, HTTPS, DNS, DHCP
- Protocols: Set of rules and messages that form an Internet Standard
    ➢ ARP - Address Resolution Protocol (defined by RFC-826): Resolves IP to MAC mappings
    ➢ FTP - File Transfer Protocol
    ➢ SMTP - Simple Mail Transfer Protocol
    ➢ HTTP - Hyper Text Transfer Protocol
    ➢ SSL - Secure Sockets Layer
    ➢ TSL - Transport Layer Security
    ➢ HTTP - HTTP secured with SSL/TSL
    ➢ TCP - Transmission Control Protocol
    ➢ DNS - Domain Name System: converts Domain Names into IP addresses. Ex: site.com/email.com -> 160.8.23.154
    ➢ DHCP - Dynamic Host Configuration Protocol: provides IP/SM/DG/DNS for Clients
- Every host needs four items for Internet Connection:
    ➢ Ip Address - Host's Identity on the Internet
    ➢ Subnet mask - Determine speak to foreign network or not
    ➢ Default Gateway - Router's IP Address
    ➢ DNS Server IP(s) - Translate domain name into IP Address

# Packages traveling: Host, Router, Switch, Router, Router, Host
- Data moves through networks based upon three tables:
    ➢ MAC Address Table - Mapping of Switch Port to MAC Address
    ➢ ARP Table/Cache - Mapping of IP address to MAC address
    ➢ Routing Table - Mapping of IP Network to Interface or Next Router
    