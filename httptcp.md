# Bullet Points
⦾⦿➼⚫⚪➡•○✯✪✫🌟🎄°
⌛⚡➟⮞➤➣➢✔
# Resources link:
https://www.practicalnetworking.net/index/networking-fundamentals-how-data-moves-through-the-internet/
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

# Everything Routers do to facilitate communication
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


# Packages traveling: Host, Switch, Router, Switch, Host

# Packages traveling: Host, Router, Switch, Router, Router, Host
