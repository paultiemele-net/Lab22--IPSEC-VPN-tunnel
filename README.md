# Lab22--IPSEC-VPN-tunnel
Establish a secure site-to-site IPsec VPN tunnel between two LANs located behind Router 1 and Router 3, allowing devices on PC1 (10.10.10.2/24) to communicate with devices on PC2 (40.40.40.2/24) securely over an untrusted WAN.

Topology:

Router 1 (R1)

LAN: 10.10.10.1/24 → PC1 gateway

WAN: 20.20.20.1/24

Router 2 (R2)

WAN: 20.20.20.2/24 → connects R1 to R3

WAN: 30.30.30.2/24

Router 3 (R3)

LAN: 40.40.40.1/24 → PC2 gateway

WAN: 30.30.30.1/24

Key Steps and Concepts:

LAN and WAN Interfaces Configuration:
Each router has LAN interfaces with assigned IPs and DHCP configured (for the local network), and WAN interfaces for inter-router connectivity.

Dynamic Routing (OSPF):
OSPF is configured on the WAN links to ensure that routers know the routes to reach each other dynamically. This allows traffic to find the proper path toward the VPN endpoints.

Static Routes for VPN:
Static routes are configured on R1 and R3 to point toward the remote LANs via the intermediate WAN IP addresses, ensuring that VPN traffic knows the next hop.

IPsec VPN Configuration:

ACLs: Define which traffic should be encrypted (LAN-to-LAN).

ISAKMP Policy: AES-256 encryption, pre-shared key, DH group 5.

Pre-shared Keys: Must match on both VPN endpoints.

Transform Set: Defines encryption (AES-256) and integrity (SHA-HMAC).

Crypto Map: Binds the VPN configuration to the WAN interface.

Verification:

Commands like show crypto isakmp sa and show crypto ipsec sa verify that the VPN tunnel is established.

Ping between PC1 and PC2 confirms end-to-end connectivity through the VPN tunnel.

Outcome:
After configuration, PC1 in LAN1 (10.10.10.0/24) can securely communicate with PC2 in LAN2 (40.40.40.0/24) over the IPsec VPN, while WAN traffic remains encrypted and protected.
