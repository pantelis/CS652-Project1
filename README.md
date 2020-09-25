# Google/Facebook DCN Approaches

Both Google and Facebook found themseves in a position where an ever-expanding datacenter footprint required moving from conventional legacy network architectures to Clos architectures. The main goal both companies aimed for was an easily-extensible network fabric allowing for high bandwidth both internally and externally with a 1P+ bisection bandwidth. 

## Designing the Network

Derivations of the fat tree topology are the name of the game, with each company taking a slightly different approach to designing the network. The goal of both networks is a multi-petabit bisection bandwidth, with each host/server receing a 10G uplink to the fabric and 40G links being used between switches. 

| Company  | Hierarchy | 
|---|---|
| Google (Jupiter)  | Server -> ToR -> Middle Block/Aggregation Block -> Spine Block  |  
| Facebook | Server -> ToR -> Server Pod -> Spine Plane  |  

Google's approach involves taking 32 ToR switches and assigning each 2x10G links to 8 so-called "Middle Blocks". These 8 MBs (grouped into an "Aggregation Block") are each supported by 4 switches. The ABs will uplink via 512x40G links to 256 Spine Blocks, each SB supporting up to 64 ABs with 128x40G total downlinks. 

Facebook's approach involves breaking up the network into "server pods" and "spine planes". A server pod is comprised of up to 48 ToR switches and 4 fabric switches. Each of the 4 fabric switches in a server pod is a part of one of 4 spine planes. Each spine plane is suppored by 48 spine switches that link to the edge. 

Equal-cost multipath routing (ECMP) w/ hashing is used at both companies to ensure load balancing and redundancy.
 
## Deploying Hardware

The key drive for designing these clos networks was affordability and extensibility. From a hardware perspective, instead of purchasing large and expensive proprietary switches and routers from Vendors, each company was able to build a clos network using merchant silicon in custom enclosures. These smaller and relatively inexpensive pieces of equipment allowed the fabric to be quickly upgraded over time in a modular fashion, promoting the idea of a wide network of small inexpensive devices instead of a small newtork of large expensive devices. 

### Google:  Fast Rollouts and Live Tests

Google details the history of their network from 2004-2012 and onwards in multiple revisions: Legacy, Firehouse 1.0 and 1.1, Watchtower, Saturn, and finally Jupiter which is described above. The biggest challenge they faced was reducing the risk involved in rolling out new network infrastructure in production environments without causing outages and putting production server nodes in an experimental networking state. To solve this problem, Google would often redundantly uplink ToR switches to both legacy networks and newer clos fabrics. This allowed their teams to play with the live ammo of new networks without compromising the reliability of production. 

*It is also interesting to note that Google took a very hands-on approach with designing and integrating their own card enclosures during experimentation with various topologies. This is very Google-eque, as they often prefer to design and implement their own solutions instead of turning to the wider market for pre-existing solutions.*


### Facebook: Work Now, Enjoy Later


## Software and Control
