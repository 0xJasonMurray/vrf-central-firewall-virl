# Overview
[VIRL](http://virl.cisco.com) mockup of centralized firewall topology using VRFs for security zone isolation.

# Brief Summary of Design

* All Cisco network.   
* Default routes are injected to both the transit core and the firewalls.   
* VRF-lite is used to isolate the different security zones on all devices in the campus.
* P2P sub-interfaces connect all the VRF routing tables (ie. a P2P adjacency is needed for each VRF).  
* OSPF adjacencies are built on all P2P interfaces to exchange routes.
* The default routing table (no VRF) will take the default route directly to the edge-1 device; bypassing the firewall.
* Each of the individual VRF’s will get their default route from firewall-1.  This forces all traffic to the inside interfaces of the firewall for policy enforcement.
    * Traffic from VRF to VRF routes between the inside interfaces on the firewalls.
    * Traffic from VRF to Internet routes through the firewalls.
    * Traffic in the same VRF never has to touch a firewall.

PRO’s for this design:
* Layer 3 fault isolation all the way to the building head-end switches.
* Devices in same security zone don’t need to traverse a firewall saving expensive bandwidth.
* Individual security zones can be pushed to any location.
* Firewalls are not inline to any device, this allows for a firewall bypass when reliability and high speed transfers are more important then centralize security. 
* Supported on all the hardware we are currently using.

CON’s for this design:
* Adding new security zones takes a lot of configuration.
* Burns through P2P IP addresses quickly.  Note: many of the internal subnets are RFC1918 space.  The P2P interfaces could also use RFC1918 space, NAT/PAT will be performed at the edge before leaving campus.  There are approximatly 300 buildings and 15 to 20 unique security zones (VRFs).  All VRFs will be on the core/distribution gear.   We expect between 5 to 10 VRFs on each of the building head-end switches.


# Files
  * Network diagram
  * VIRL configuration file
