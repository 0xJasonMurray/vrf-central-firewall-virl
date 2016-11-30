# Overview
[VIRL](http://virl.cisco.com) mockup of centralized firewall topology using VRFs for security zone isolation.

**Please note, this is a lab configuration and not meant to be a best practice design.   The primary goal was to build a proof-of-concept using VRFs for security zone isolation.**

![topology](https://github.com/duxklr/vrf-central-firewall-virl/blob/master/vrf-central-firewall-virl.png)

# Brief Summary of Design

* Default routes are injected to both the transit core and the firewalls.   
* VRF-lite is used to isolate the different security zones on all devices in the campus.
* P2P sub-interfaces connect the adjacent VRF routing tables (ie. a P2P adjacency for each VRF).  
* OSPF adjacencies are built on all P2P interfaces to exchange routes.
* The default routing table (no VRF) will take the default route towards the edge-1 device; bypassing the firewall.
* Each of the individual VRF’s will get their default route from firewall-1.  This directs all traffic to the inside interfaces of the firewall for policy enforcement.
    * Traffic from VRF to VRF routes between the inside interfaces on the firewalls.
    * Traffic from VRF to Internet routes through the firewalls.
    * Traffic in the same VRF never has to touch a firewall.

# Files
  * Network diagram
  * VIRL configuration file; includes individual router and firewall configurations.
